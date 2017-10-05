---
title: "Azure에서 일반화된 VM의 관리되지 않는 이미지 만들기 | Microsoft Docs"
description: "Azure에서 VM의 여러 복사본을 만드는 데 사용할 일반화된 Windows VM의 관리되지 않는 이미지를 만듭니다."
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
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="3d8e9-103">Azure VM에서 관리되지 않는 VM 이미지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3d8e9-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="3d8e9-104">이 문서에서는 저장소 계정을 사용하여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-104">This article covers using storage accounts.</span></span> <span data-ttu-id="3d8e9-105">저장소 계정 대신 관리 디스크 및 관리되는 이미지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="3d8e9-106">자세한 내용은 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](capture-image-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="3d8e9-107">이 문서에서는 저장소 계정을 사용하여 일반화된 Azure VM 이미지를 만드는 데 Azure PowerShell을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="3d8e9-108">그런 다음 이미지를 사용하여 다른 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="3d8e9-109">이 이미지에는 OS 디스크를 비롯해 가상 컴퓨터에 연결된 데이터 디스크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="3d8e9-110">새 VM을 만들 때 해당 리소스를 설정해야 하므로 이미지는 가상 네트워크 리소스를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3d8e9-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3d8e9-111">Prerequisites</span></span>
<span data-ttu-id="3d8e9-112">Azure PowerShell 버전 1.0.x 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="3d8e9-113">PowerShell을 아직 설치하지 않은 경우 설치 단계에 대해서는 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="3d8e9-114">VM 일반화</span><span class="sxs-lookup"><span data-stu-id="3d8e9-114">Generalize the VM</span></span> 
<span data-ttu-id="3d8e9-115">이 섹션에서는 이미지로 사용하기 위해 Windows 가상 컴퓨터를 일반화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="3d8e9-116">VM을 일반화하면 여러 정보 중에서 모든 개인 계정 정보가 제거되고 이미지로 사용할 컴퓨터가 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="3d8e9-117">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="3d8e9-118">가상 컴퓨터에서 실행되는 서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="3d8e9-119">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="3d8e9-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d8e9-120">Azure에 VHD를 처음으로 업로드하는 경우 Sysprep을 실행하기 전에 [VM을 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="3d8e9-121">`sudo waagent -deprovision+user`을 사용하여 Linux VM을 일반화한 다음 PowerShell을 사용하여 VM을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="3d8e9-122">VM을 캡처하는 데 CLI를 사용하는 방법에 대한 정보는 [Azure CLI를 사용하여 Linux 가상 컴퓨터를 일반화하고 캡처하는 방법](../linux/capture-image.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="3d8e9-123">Windows 가상 컴퓨터에 로그인</span><span class="sxs-lookup"><span data-stu-id="3d8e9-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="3d8e9-124">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="3d8e9-125">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 `sysprep.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="3d8e9-126">**시스템 준비 도구** 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="3d8e9-127">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="3d8e9-128">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-128">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="3d8e9-130">Sysprep이 완료되면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3d8e9-131">Azure에 VHD를 업로드하거나 VM에서 이미지를 만드는 작업을 완료할 때까지 VM을 다시 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="3d8e9-132">VM이 실수로 다시 시작되면 Sysprep을 실행하여 다시 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="3d8e9-133">Azure PowerShell에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="3d8e9-134">Azure PowerShell을 열고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="3d8e9-135">Azure 계정 자격 증명을 입력하기 위한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="3d8e9-136">사용 가능한 구독에 대한 구독을 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="3d8e9-137">구독 ID를 사용하여 올바른 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="3d8e9-138">VM의 할당을 취소하고 상태를 일반화됨으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="3d8e9-139">VM 리소스 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="3d8e9-140">Azure Portal의 VM에 대한 *상태*가 **중지됨**에서 **중지됨(할당 취소됨)**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="3d8e9-141">가상 컴퓨터의 상태를 **일반화됨**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="3d8e9-142">VM의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-142">Check the status of the VM.</span></span> <span data-ttu-id="3d8e9-143">VM에 대한 **OSState/일반화됨** 섹션은 **DisplayStatus**를 **VM 일반화됨**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="3d8e9-144">이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-144">Create the image</span></span>

<span data-ttu-id="3d8e9-145">이 명령을 사용하여 대상 저장소 컨테이너에서 관리되지 않는 가상 컴퓨터 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="3d8e9-146">이미지는 원래 가상 컴퓨터와 동일한 저장소 계정에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="3d8e9-147">`-Path` 매개 변수는 원본 VM에 대한 JSON 템플릿의 복사본을 로컬 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="3d8e9-148">`-DestinationContainerName` 매개 변수는 이미지를 유지할 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="3d8e9-149">컨테이너가 없으면 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="3d8e9-150">JSON 파일 템플릿에서 이미지의 URL을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="3d8e9-151">이미지의 전체 경로에 대한 **resources** > **storageProfile** > **osDisk** > **image** > **uri** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="3d8e9-152">이미지의 URL은 `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="3d8e9-153">포털에서 URI를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="3d8e9-154">이미지는 저장소 계정에서 **시스템** 라는 컨테이너에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="3d8e9-155">이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-155">Create a VM from the image</span></span>

<span data-ttu-id="3d8e9-156">이제 관리되지 않는 이미지에서 하나 이상의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="3d8e9-157">VHD의 URI 설정</span><span class="sxs-lookup"><span data-stu-id="3d8e9-157">Set the URI of the VHD</span></span>

<span data-ttu-id="3d8e9-158">VHD에 대한 URI는 형식: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="3d8e9-159">이 예에서는 **myVHD**로 명명된 VHD가 **mycontainer** 컨테이너의 **mystorageaccount** 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="3d8e9-160">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-160">Create a virtual network</span></span>
<span data-ttu-id="3d8e9-161">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 vNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3d8e9-162">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-162">Create the subnet.</span></span> <span data-ttu-id="3d8e9-163">다음 예제에서는 **10.0.0.0/24** 주소 접두사가 있는 **myResourceGroup** 리소스 그룹에 **mySubnet**으로 명명된 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3d8e9-164">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-164">Create the virtual network.</span></span> <span data-ttu-id="3d8e9-165">다음 예제에서는 **10.0.0.0/16** 주소 접두사가 있는 **미국 서부** 위치에 **myVnet**으로 명명된 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3d8e9-166">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="3d8e9-167">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3d8e9-168">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-168">Create a public IP address.</span></span> <span data-ttu-id="3d8e9-169">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3d8e9-170">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-170">Create the NIC.</span></span> <span data-ttu-id="3d8e9-171">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3d8e9-172">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="3d8e9-173">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 보안 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3d8e9-174">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3d8e9-175">NSG에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="3d8e9-176">가상 네트워크에 대한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="3d8e9-177">완료된 가상 네트워크에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="3d8e9-178">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3d8e9-178">Create the VM</span></span>
<span data-ttu-id="3d8e9-179">다음 PowerShell에서는 가상 컴퓨터 구성을 완료하고 관리되지 않는 이미지를 새 설치에 대한 소스로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="3d8e9-180">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="3d8e9-180">Verify that the VM was created</span></span>
<span data-ttu-id="3d8e9-181">완료되면 새로 만든 VM은 [Azure 포털](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3d8e9-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d8e9-182">Next steps</span></span>
<span data-ttu-id="3d8e9-183">Azure PowerShell을 사용하여 새 가상 컴퓨터를 관리하려면 [Azure Resource Manager 및 PowerShell을 사용하여 가상 컴퓨터 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d8e9-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


