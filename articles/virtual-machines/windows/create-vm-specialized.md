---
title: "Azure에서 특수화 된 VHD에서 Windows VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 사용 하 여 hello 운영 체제 디스크와 관리 되는 특수 한 디스크를 연결 하 여 새 Windows VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="583bd-103">특수한 디스크에서 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="583bd-104">Powershell을 사용 하 여 hello 운영 체제 디스크와 관리 되는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="583bd-105">특수 한 디스크 hello 사용자 계정 및 응용 프로그램, 원래 VM에서 다른 상태 데이터를 유지 하는 기존 VM에서 가상 하드 디스크 (VHD)의 복사본을입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="583bd-106">특수 한 VHD toocreate 새 VM을 사용 하는 경우 새 VM의 hello 컴퓨터 이름을 그대로 유지 하는 hello hello 원본 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="583bd-107">다른 컴퓨터 관련 정보도 유지되며, 경우에 따라 이 중복된 정보로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="583bd-108">VM을 복사할 때 응용 프로그램이 어떤 유형의 컴퓨터 관련 정보에 의존하는지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="583bd-109">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-109">You have two options:</span></span>
* [<span data-ttu-id="583bd-110">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="583bd-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="583bd-111">기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="583bd-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="583bd-112">이 항목에서는 toouse 디스크를 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="583bd-113">저장소 계정을 사용해야 하는 레거시 배포가 있는 경우 [저장소 계정의 특수한 VHD에서 VM 만들기](sa-create-vm-specialized.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="583bd-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="583bd-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="583bd-114">Before you begin</span></span>
<span data-ttu-id="583bd-115">PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="583bd-116">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="583bd-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="583bd-117">옵션 1: 특수한 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="583bd-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="583bd-118">Hello 하이퍼-V 또는 VM 사설 클라우드에서 다른 클라우드에서 내보낼 처럼 온-프레미스 가상화 도구를 사용 하 여 만든 특수 한 VM에서 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="583bd-119">Hello VM 준비</span><span class="sxs-lookup"><span data-stu-id="583bd-119">Prepare hello VM</span></span>
<span data-ttu-id="583bd-120">Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="583bd-121">[Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="583bd-122">**없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="583bd-123">모든 게스트 가상화 도구와 hello VM (예: VMware 도구)에 설치 된 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="583bd-124">Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="583bd-125">이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="583bd-126">Hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="583bd-126">Get hello storage account</span></span>
<span data-ttu-id="583bd-127">저장소에 필요한 계정 Azure toostore hello에 VHD를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="583bd-128">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="583bd-129">tooshow hello 사용 가능한 저장소 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="583bd-130">Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [VHD 업로드 hello](#upload-the-vhd-to-your-storage-account) 섹션.</span><span class="sxs-lookup"><span data-stu-id="583bd-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="583bd-131">저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="583bd-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="583bd-132">Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="583bd-133">구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:</span><span class="sxs-lookup"><span data-stu-id="583bd-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="583bd-134">리소스 그룹 이름이 toocreate *myResourceGroup* hello에 *미국 서 부* 지역, 유형:</span><span class="sxs-lookup"><span data-stu-id="583bd-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="583bd-135">라는 저장소 계정 만들기 *mystorageaccount* hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="583bd-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="583bd-136">Hello VHD tooyour 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="583bd-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="583bd-137">사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello VHD tooa 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="583bd-138">이 예에서는 업로드 파일 hello *myVHD.vhd* 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 *mystorageaccount* hello에 *myResourceGroup* 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="583bd-139">hello 파일은 라는 hello 컨테이너에 저장 *mycontainer* hello 새 파일 이름이 됩니다 *myUploadedVHD.vhd*합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="583bd-140">성공 하면 다음과 비슷한 toothis 응답 가져오기:</span><span class="sxs-lookup"><span data-stu-id="583bd-140">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="583bd-141">이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete</span><span class="sxs-lookup"><span data-stu-id="583bd-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="583bd-142">Hello VHD에서에서 관리 되는 디스크를 만들려면</span><span class="sxs-lookup"><span data-stu-id="583bd-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="583bd-143">Hello에서 관리 되는 디스크를 만들 사용 하 여 저장소 계정에서 VHD를 특수화할 [새로 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="583bd-144">이 예에서는 **myOSDisk1** hello 디스크 이름에 대 한 설정에서 디스크를 hello *StandardLRS* 저장 및 사용 하 여 *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* hello 원본 VHD에 대 한 URI를 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="583bd-145">Hello에 대 한 새 리소스 그룹을 만들려면 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="583bd-146">만들 hello hello에서 새 운영 체제 디스크는 VHD를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="583bd-147">옵션 2: 기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="583bd-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="583bd-148">Hello, VM의 스냅숏을 수행 하 여 관리 디스크를 사용 하 여 다음 해당 스냅숏 toocreate를 사용 하 여 새 관리 되는 디스크와 새 VM의 VM의 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="583bd-149">Hello OS 디스크에 대 한 스냅숏을 만들려면</span><span class="sxs-lookup"><span data-stu-id="583bd-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="583bd-150">전체 VM(모든 디스크 포함) 또는 단일 디스크의 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="583bd-151">hello 다음 단계 보여 방법을 사용 하 여 VM의 바로 hello OS 디스크의 스냅숏을 tootake hello [새로 AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="583bd-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="583bd-152">일부 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="583bd-153">Hello VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="583bd-154">Hello OS 디스크 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="583bd-155">Hello 스냅숏 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="583bd-156">Hello 스냅숏을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="583bd-157">Hello 매개 변수를 사용 하 여 toouse hello 스냅숏 toocreate toobe 높은 수행 해야 하는 VM을 하려면 `-AccountType Premium_LRS` hello AzureRmSnapshot 새로 만들기 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="583bd-158">hello 매개 변수 hello 스냅숏을 생성 되어 프리미엄 관리 되는 디스크로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="583bd-159">프리미엄 Managed Disks는 표준 Managed Disks보다 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="583bd-160">따라서 프리미엄 hello 매개 변수를 사용 하기 전에 게이트웨이가 필요한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="583bd-161">Hello 스냅숏에서 새 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="583bd-162">사용 하 여 스냅숏 hello에서 관리 되는 디스크를 만들 [새로 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="583bd-163">이 예에서는 *myOSDisk* hello 디스크 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="583bd-164">Hello에 대 한 새 리소스 그룹을 만들려면 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="583bd-165">Hello OS 디스크 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="583bd-166">Hello 관리 되는 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="583bd-167">만들 새 VM hello</span><span class="sxs-lookup"><span data-stu-id="583bd-167">Create hello new VM</span></span> 

<span data-ttu-id="583bd-168">네트워킹 및 hello에서 사용 하는 다른 VM 리소스 toobe 만들 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="583bd-169">Hello 서브넷 및 vNet 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="583bd-170">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="583bd-171">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-171">Create hello subNet.</span></span> <span data-ttu-id="583bd-172">이 예에서는 이라는 서브넷을 만듭니다 **mySubNet**, hello 리소스 그룹에 **myDestinationResourceGroup**, 집합 서브넷 주소 접두사를 너무 hello 및**10.0.0.0/24**합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="583bd-173">Hello vNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-173">Create hello vNet.</span></span> <span data-ttu-id="583bd-174">이 예제에서는 집합에 가상 네트워크 이름 toobe hello **myVnetName**, 위치를 너무 hello**미국 서 부**, hello 가상 네트워크에 대 한 주소 접두사를 너무 hello 및**10.0.0.0/16**합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="583bd-175">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="583bd-176">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="583bd-177">때문에 특수화 된 기존 VM에서 새 VM을 만든 hello에 대 한 VHD를 hello, RDP에 대 한 hello 소스 가상 컴퓨터에서 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="583bd-178">이 예제에서는 집합 hello NSG 이름을 너무**myNsg** 너무 hello RDP 규칙 이름 및**myRdpRule**합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="583bd-179">끝점 및 NSG 규칙에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="583bd-180">공용 IP 주소 및 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="583bd-181">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="583bd-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="583bd-182">Hello 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-182">Create hello public IP.</span></span> <span data-ttu-id="583bd-183">이 예제에서는 hello 공용 IP 주소 이름이 설정 되어 너무**myIP**합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="583bd-184">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="583bd-184">Create hello NIC.</span></span> <span data-ttu-id="583bd-185">이 예제에서는 hello NIC 이름이 설정 되어 너무**myNicName**합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="583bd-186">Hello VM 이름 및 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-186">Set hello VM name and size</span></span>

<span data-ttu-id="583bd-187">이 예제에서는 집합 hello VM 이름을 너무*myVM* 고 hello VM 크기 너무*Standard_A2*합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="583bd-188">Hello NIC를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="583bd-189">Hello OS 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="583bd-189">Add hello OS disk</span></span> 

<span data-ttu-id="583bd-190">Hello OS 디스크 toohello 구성을 사용 하 여 추가 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="583bd-191">이 예에서는 설정 hello 디스크의 hello 크기 너무*128GB* 와 연결 합니다. hello로 관리 되는 디스크는 *Windows* OS 디스크.</span><span class="sxs-lookup"><span data-stu-id="583bd-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="583bd-192">전체 hello VM</span><span class="sxs-lookup"><span data-stu-id="583bd-192">Complete hello VM</span></span> 

<span data-ttu-id="583bd-193">사용 하 여 hello VM 만들기 [새로 AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello 방금 만든 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="583bd-194">이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="583bd-195">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-195">Verify that hello VM was created</span></span>
<span data-ttu-id="583bd-196">Hello 새로 만든 VM hello에 표시 되어야 [Azure 포털](https://portal.azure.com)아래 **찾아보기** > **가상 컴퓨터**, 또는 다음 PowerShell hello를 사용 하 여 명령:</span><span class="sxs-lookup"><span data-stu-id="583bd-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="583bd-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="583bd-197">Next steps</span></span>
<span data-ttu-id="583bd-198">tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="583bd-199">Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="583bd-200">자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="583bd-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

