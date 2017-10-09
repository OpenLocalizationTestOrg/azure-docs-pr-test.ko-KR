---
title: "Azure에서 일반화 된 VM의 관리 되지 않는 이미지 aaaCreate | Microsoft Docs"
description: "Azure에서의 일반화 된 Windows VM toouse toocreate 비관리 이미지로 VM의 여러 복사본을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="2ab7f-103">Azure VM에서 toocreate 관리 되지 않는 VM 이미지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2ab7f-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="2ab7f-104">이 문서에서는 저장소 계정을 사용하여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-104">This article covers using storage accounts.</span></span> <span data-ttu-id="2ab7f-105">저장소 계정 대신 관리 디스크 및 관리되는 이미지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="2ab7f-106">자세한 내용은 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](capture-image-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="2ab7f-107">이 문서에서는 Azure PowerShell toocreate toouse 저장소 계정을 사용 하 여 일반화 된 Azure VM의 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="2ab7f-108">그런 다음 다른 VM 이미지 toocreate hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="2ab7f-109">hello 이미지 hello OS 디스크 및 연결 된 toohello 가상 컴퓨터는 hello 데이터 디스크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="2ab7f-110">새 VM을 hello를 만들 때 이러한 리소스는 tooset 필요 하므로, hello 이미지 hello 가상 네트워크 리소스를 포함 하지 않습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ab7f-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ab7f-111">Prerequisites</span></span>
<span data-ttu-id="2ab7f-112">Toohave Azure PowerShell 버전 1.0. x 이상 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="2ab7f-113">PowerShell을 아직 설치 하지 않은 경우 읽기 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 설치 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="2ab7f-114">Hello VM 일반화</span><span class="sxs-lookup"><span data-stu-id="2ab7f-114">Generalize hello VM</span></span> 
<span data-ttu-id="2ab7f-115">이 섹션에서는 toogeneralize 이미지 형식으로 사용할 Windows 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="2ab7f-116">VM 일반화 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="2ab7f-117">Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="2ab7f-118">Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="2ab7f-119">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="2ab7f-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ab7f-120">업로드 하는 경우 프로그램 VHD tooAzure hello에 대 한 처음으로, 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="2ab7f-121">사용 하 여 Linux VM을 일반화할 수 있습니다 `sudo waagent -deprovision+user` 다음 PowerShell toocapture hello VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="2ab7f-122">Hello CLI toocapture VM을 사용 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 toogeneralize 및 사용 하 여 Linux 가상 컴퓨터 캡처 hello Azure CLI ](../linux/capture-image.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="2ab7f-123">Windows 가상 컴퓨터 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="2ab7f-124">Hello 명령 프롬프트 창을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="2ab7f-125">Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="2ab7f-126">Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="2ab7f-127">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="2ab7f-128">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-128">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="2ab7f-130">Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2ab7f-131">업로드 완료 hello VHD tooAzure 또는 hello VM에서에서 이미지를 만들 때까지 VM hello를 다시 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="2ab7f-132">Hello VM 실수로 가져옵니다 다시 시작, 실행 Sysprep toogeneralize 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="2ab7f-133">PowerShell tooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="2ab7f-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="2ab7f-134">Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="2ab7f-135">Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="2ab7f-136">사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="2ab7f-137">Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정</span><span class="sxs-lookup"><span data-stu-id="2ab7f-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="2ab7f-138">Hello VM 할당 취소 하 고 hello 상태 toogeneralized 설정</span><span class="sxs-lookup"><span data-stu-id="2ab7f-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="2ab7f-139">Hello VM 리소스 할당이 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="2ab7f-140">hello *상태* hello Azure에에서 VM hello에 대 한 포털에서 변경 **Stopped** 너무**중지 됨 (할당 취소 됨)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="2ab7f-141">Hello 가상 컴퓨터의 hello 상태를 너무 설정**일반화 됨으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="2ab7f-142">Hello VM의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-142">Check hello status of hello VM.</span></span> <span data-ttu-id="2ab7f-143">hello **OSState/일반화** hello VM hello 있어야에 대 한 섹션 **DisplayStatus** 도**VM 일반화**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="2ab7f-144">Hello 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-144">Create hello image</span></span>

<span data-ttu-id="2ab7f-145">이 명령을 사용 하 여 hello 대상 저장소 컨테이너에 관리 되지 않는 가상 컴퓨터 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="2ab7f-146">hello 이미지가 만들어지고 hello에 동일한 저장소 계정으로 원본 가상 컴퓨터가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="2ab7f-147">hello `-Path` hello 소스 VM tooyour 로컬 컴퓨터에 대 한 hello JSON 서식 파일의 복사본을 저장 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="2ab7f-148">hello `-DestinationContainerName` 매개 변수는 hello 컨테이너 되도록 toohold 이미지의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="2ab7f-149">Hello 컨테이너가 존재 하지 않는 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="2ab7f-150">Hello JSON 파일 서식 파일에서 이미지의 hello URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="2ab7f-151">Toohello 이동 **리소스** > **storageProfile** > **osDisk** > **이미지**  >  **uri** hello 전체 경로 대 한 이미지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="2ab7f-152">다음과 같은 hello 이미지의 URL hello: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="2ab7f-153">또한 hello URI hello 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="2ab7f-154">hello 이미지는 복사한 tooa 컨테이너인 **시스템** 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="2ab7f-155">Hello 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-155">Create a VM from hello image</span></span>

<span data-ttu-id="2ab7f-156">이제 hello 관리 되지 않는 이미지에서 하나 이상의 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="2ab7f-157">Hello hello VHD의 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="2ab7f-158">VHD toouse hello에 대 한 hello URI는 hello 형식: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="2ab7f-159">이 예에서 hello 라는 VHD **myVHD** hello 저장소 계정에는 **mystorageaccount** hello 컨테이너에 **mycontainer**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="2ab7f-160">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-160">Create a virtual network</span></span>
<span data-ttu-id="2ab7f-161">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="2ab7f-162">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-162">Create hello subnet.</span></span> <span data-ttu-id="2ab7f-163">hello 다음 샘플 서브넷을 만듭니다. 명명 된 **mySubnet** hello 리소스 그룹에 **myResourceGroup** hello 주소 접두사와 **10.0.0.0/24**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="2ab7f-164">Hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-164">Create hello virtual network.</span></span> <span data-ttu-id="2ab7f-165">hello 다음 샘플 가상 네트워크를 만들어 명명 된 **myVnet** hello에 **West US** hello 주소 접두사를 사용 하 여 위치 **10.0.0.0/16**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="2ab7f-166">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="2ab7f-167">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="2ab7f-168">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-168">Create a public IP address.</span></span> <span data-ttu-id="2ab7f-169">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="2ab7f-170">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-170">Create hello NIC.</span></span> <span data-ttu-id="2ab7f-171">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="2ab7f-172">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="2ab7f-173">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="2ab7f-174">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="2ab7f-175">Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="2ab7f-176">Hello 가상 네트워크에 대 한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="2ab7f-177">가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="2ab7f-178">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab7f-178">Create hello VM</span></span>
<span data-ttu-id="2ab7f-179">hello 다음 PowerShell hello 가상 컴퓨터 구성 및 관리 되지 않는 이미지를 새로 설치 하는 hello에 대 한 hello 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="2ab7f-180">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-180">Verify that hello VM was created</span></span>
<span data-ttu-id="2ab7f-181">새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:</span><span class="sxs-lookup"><span data-stu-id="2ab7f-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="2ab7f-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ab7f-182">Next steps</span></span>
<span data-ttu-id="2ab7f-183">Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [Azure 리소스 관리자 및 PowerShell을 사용 하 여 가상 컴퓨터를 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab7f-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


