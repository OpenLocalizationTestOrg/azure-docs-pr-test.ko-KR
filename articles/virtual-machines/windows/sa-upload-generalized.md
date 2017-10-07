---
title: "aaaUpload 일반화 VHD toocreate Azure에서 여러 Vm | Microsoft Docs"
description: "일반화 된 VHD tooan Azure 저장소 계정 toocreate hello 리소스 관리자 배포 모델에 Windows VM toouse를 업로드 합니다."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="251d8-103">일반화 된 VHD tooAzure toocreate 새 VM을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="251d8-104">이 항목에서는 관리 되지 않는 디스크를 일반화 된 tooa 저장소 계정을 업로드 하 고 다음 업로드 hello 디스크를 사용 하 여 새 VM을 만들어 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="251d8-105">일반화된 VHD 이미지에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="251d8-106">저장소 계정에는 특수 한 VHD에서 VM toocreate 참조 [특수 VHD에서 VM 만들기](sa-create-vm-specialized.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="251d8-107">이 항목에서는 저장소 계정을 사용 하 여 있지만 고객 대신 toousing 관리 하는 디스크를 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="251d8-108">전체 연습 tooprepare, 업로드 하 고 사용 하 여 새 VM을 만드는 방법의 디스크 관리에 대 한 참조 [관리 하는 디스크를 사용 하 여 일반화 된 VHD 업로드 tooAzure에서 새 VM 만들기](upload-generalized-managed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="251d8-109">Hello VM 준비</span><span class="sxs-lookup"><span data-stu-id="251d8-109">Prepare hello VM</span></span>

<span data-ttu-id="251d8-110">일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="251d8-111">Toouse hello VHD 이미지 toocreate로 가져오려는 경우에서 새 Vm을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="251d8-112">[Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="251d8-113">Sysprep를 사용 하 여 hello 가상 컴퓨터를 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="251d8-114">Sysprep을 사용하여 Windows 가상 컴퓨터 일반화</span><span class="sxs-lookup"><span data-stu-id="251d8-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="251d8-115">이 섹션에서는 toogeneralize 이미지 형식으로 사용할 Windows 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="251d8-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="251d8-116">Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="251d8-117">Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="251d8-118">Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="251d8-119">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="251d8-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="251d8-120">를 사용 하 여 VHD tooAzure hello에 대 한 처음으로 업로드 하기 전에 Sysprep를 실행 하는 경우 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="251d8-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="251d8-121">Windows 가상 컴퓨터 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="251d8-122">Hello 명령 프롬프트 창을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="251d8-123">Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="251d8-124">Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="251d8-125">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="251d8-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-126">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="251d8-128">Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="251d8-129">업로드 완료 hello VHD tooAzure 또는 hello VM에서에서 이미지를 만들 때까지 VM hello를 다시 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="251d8-130">Hello VM 실수로 가져옵니다 다시 시작, 실행 Sysprep toogeneralize 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="251d8-131">Hello VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="251d8-131">Upload hello VHD</span></span>

<span data-ttu-id="251d8-132">Hello VHD tooan Azure 저장소 계정에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="251d8-133">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="251d8-133">Log in tooAzure</span></span>
<span data-ttu-id="251d8-134">PowerShell 버전 1.4가 없는 이상 읽기 설치 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="251d8-135">Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="251d8-136">Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="251d8-137">사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="251d8-138">Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정</span><span class="sxs-lookup"><span data-stu-id="251d8-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="251d8-139">대체 `<subscriptionID>` hello hello ID로 구독을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="251d8-140">Hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="251d8-140">Get hello storage account</span></span>
<span data-ttu-id="251d8-141">Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="251d8-142">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="251d8-143">tooshow hello 사용 가능한 저장소 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="251d8-144">Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [hello VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션.</span><span class="sxs-lookup"><span data-stu-id="251d8-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="251d8-145">저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="251d8-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="251d8-146">Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="251d8-147">구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:</span><span class="sxs-lookup"><span data-stu-id="251d8-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="251d8-148">리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 서 부** 지역, 유형:</span><span class="sxs-lookup"><span data-stu-id="251d8-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="251d8-149">라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="251d8-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="251d8-150">Hello 업로드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-150">Start hello upload</span></span> 

<span data-ttu-id="251d8-151">사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello 이미지 tooa 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="251d8-152">이 예에서는 업로드 파일 hello **myVHD.vhd** 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 **mystorageaccount** hello에 **myResourceGroup** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="251d8-153">hello 파일 라는 hello 컨테이너에 배치 됨 **mycontainer** hello 새 파일 이름이 됩니다 **myUploadedVHD.vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="251d8-154">성공 하면 다음과 비슷한 toothis 응답 가져오기:</span><span class="sxs-lookup"><span data-stu-id="251d8-154">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="251d8-155">이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="251d8-156">새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-156">Create a new VM</span></span> 

<span data-ttu-id="251d8-157">사용 하 여 hello VHD toocreate 새 VM을 업로드 하는 이제 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="251d8-158">Hello hello VHD의 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="251d8-159">VHD toouse hello에 대 한 hello URI는 hello 형식: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="251d8-160">이 예에서 hello 라는 VHD **myVHD** hello 저장소 계정에는 **mystorageaccount** hello 컨테이너에 **mycontainer**합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="251d8-161">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-161">Create a virtual network</span></span>
<span data-ttu-id="251d8-162">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="251d8-163">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-163">Create hello subnet.</span></span> <span data-ttu-id="251d8-164">hello 다음 샘플 서브넷을 만듭니다. 명명 된 **mySubnet** hello 리소스 그룹에 **myResourceGroup** hello 주소 접두사와 **10.0.0.0/24**합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="251d8-165">Hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-165">Create hello virtual network.</span></span> <span data-ttu-id="251d8-166">hello 다음 샘플 가상 네트워크를 만들어 명명 된 **myVnet** hello에 **West US** hello 주소 접두사를 사용 하 여 위치 **10.0.0.0/16**합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="251d8-167">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="251d8-168">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="251d8-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="251d8-169">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="251d8-169">Create a public IP address.</span></span> <span data-ttu-id="251d8-170">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="251d8-171">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-171">Create hello NIC.</span></span> <span data-ttu-id="251d8-172">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="251d8-173">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="251d8-174">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="251d8-175">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="251d8-176">Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="251d8-177">Hello 가상 네트워크에 대 한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="251d8-178">가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="251d8-179">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="251d8-179">Create hello VM</span></span>
<span data-ttu-id="251d8-180">hello 다음 PowerShell 스크립트에서는 tooset hello 가상 컴퓨터 구성 및 사용 하 여 hello를 새로 설치 하는 hello에 대 한 hello 소스로 VM 이미지를 업로드 하는 방법</span><span class="sxs-lookup"><span data-stu-id="251d8-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



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

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="251d8-181">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-181">Verify that hello VM was created</span></span>
<span data-ttu-id="251d8-182">새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:</span><span class="sxs-lookup"><span data-stu-id="251d8-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="251d8-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="251d8-183">Next steps</span></span>
<span data-ttu-id="251d8-184">Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [Azure 리소스 관리자 및 PowerShell을 사용 하 여 가상 컴퓨터를 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="251d8-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


