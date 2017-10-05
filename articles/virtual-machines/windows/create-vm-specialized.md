---
title: "Azure의 특수한 VHD에서 Windows VM 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 특수한 관리 디스크를 OS 디스크로 연결하여 새 Windows VM을 만듭니다."
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
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="05fc7-103">특수한 디스크에서 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="05fc7-104">Powershell을 사용하여 특수한 관리 디스크를 OS 디스크로 연결하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="05fc7-105">특수한 디스크는 기존 VM의 VHD(가상 하드 디스크) 복사본으로 사용자 계정, 응용 프로그램 및 원본 VM의 기타 상태 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="05fc7-106">특수한 VHD를 사용하여 새 VM을 만드는 경우 새 VM은 원본 VM의 컴퓨터 이름을 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="05fc7-107">다른 컴퓨터 관련 정보도 유지되며, 경우에 따라 이 중복된 정보로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="05fc7-108">VM을 복사할 때 응용 프로그램이 어떤 유형의 컴퓨터 관련 정보에 의존하는지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="05fc7-109">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-109">You have two options:</span></span>
* [<span data-ttu-id="05fc7-110">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="05fc7-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="05fc7-111">기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="05fc7-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="05fc7-112">이 항목에서는 관리 디스크를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="05fc7-113">저장소 계정을 사용해야 하는 레거시 배포가 있는 경우 [저장소 계정의 특수한 VHD에서 VM 만들기](sa-create-vm-specialized.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05fc7-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05fc7-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="05fc7-114">Before you begin</span></span>
<span data-ttu-id="05fc7-115">PowerShell을 사용하는 경우 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="05fc7-116">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05fc7-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="05fc7-117">옵션 1: 특수한 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="05fc7-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="05fc7-118">Hyper-V와 같은 온-프레미스 가상화 도구를 사용하여 만든 특수한 VM 또는 다른 클라우드에서 내보낸 VM에서 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="05fc7-119">VM 준비</span><span class="sxs-lookup"><span data-stu-id="05fc7-119">Prepare the VM</span></span>
<span data-ttu-id="05fc7-120">새 VM을 만드는데 VHD를 그대로 사용하려는 경우 다음 단계가 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="05fc7-121">[Azure에 업로드할 Windows VHD를 준비합니다](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05fc7-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="05fc7-122">Sysprep을 사용하여 VM을 일반화하지 **마십시오**.</span><span class="sxs-lookup"><span data-stu-id="05fc7-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="05fc7-123">모든 게스트 가상화 도구 및 VM에 설치된 에이전트를 제거합니다(예: VMware 도구).</span><span class="sxs-lookup"><span data-stu-id="05fc7-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="05fc7-124">VM이 DHCP를 통해 해당 IP 주소 및 DNS 설정을 가져오도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="05fc7-125">이렇게 하면 서버를 시작할 때 VNet 내의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="05fc7-126">저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="05fc7-126">Get the storage account</span></span>
<span data-ttu-id="05fc7-127">업로드한 VHD를 저장할 Azure Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="05fc7-128">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="05fc7-129">사용 가능한 저장소 계정을 표시하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="05fc7-130">기존 저장소 계정을 사용하려면 [VHD 업로드](#upload-the-vhd-to-your-storage-account) 섹션을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="05fc7-131">저장소 계정을 만들어야 하는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="05fc7-132">저장소 계정을 만들어야 하는 리소스 그룹의 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="05fc7-133">구독의 모든 리소스 그룹을 찾으려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="05fc7-134">*미국 서부* 지역에 *myResourceGroup* 이라는 이름의 리소스 그룹을 만들려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="05fc7-135">[New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 이 리소스 그룹에 *mystorageaccount*라는 이름의 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="05fc7-136">저장소 계정에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="05fc7-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="05fc7-137">[Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet을 사용하여 저장소 계정의 컨테이너에 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="05fc7-138">이 예제에서는 `"C:\Users\Public\Documents\Virtual hard disks\"`에서 *myResourceGroup* 리소스 그룹의 *mystorageaccount*라는 저장소 계정에 파일 *myVHD.vhd*를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="05fc7-139">파일은 *mycontainer*라는 컨테이너에 저장되고 새 파일 이름은 *myUploadedVHD.vhd*가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="05fc7-140">성공하면 다음과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="05fc7-141">이 명령은 네트워크 연결 및 VHD 파일의 크기에 따라 완료하는 데 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="05fc7-142">VHD에서 관리 디스크를 만들려면</span><span class="sxs-lookup"><span data-stu-id="05fc7-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="05fc7-143">[New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)를 사용하여 사용자의 저장소 계정에 있는 특수한 VHD로 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="05fc7-144">이 예에서는 디스크 이름으로 **myOSDisk1**을 사용하고, 디스크를 *StandardLRS* 저장소에 배치하고, 원본 VHD의 URI로 *https://storageaccount.Blob.core.windows.net/vhdcontainer/osdisk.vhd*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="05fc7-145">새 VM에 대한 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="05fc7-146">업로드된 VHD에서 새 OS 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="05fc7-147">옵션 2: 기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="05fc7-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="05fc7-148">VM의 스냅숏을 만든 다음 이 스냅숏을 사용하여 새 관리 디스크 및 새 VM을 만드는 방식으로 관리 디스크를 사용하는 VM의 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="05fc7-149">OS 디스크의 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="05fc7-150">전체 VM(모든 디스크 포함) 또는 단일 디스크의 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="05fc7-151">다음 단계에서는 [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet을 사용하여 VM의 OS 디스크에 대한 스냅숏을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="05fc7-152">일부 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="05fc7-153">VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="05fc7-154">OS 디스크 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="05fc7-155">스냅숏 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="05fc7-156">스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="05fc7-157">스냅숏을 사용하여 고성능이 필요한 VM을 만들려면 `-AccountType Premium_LRS` 매개 변수와 New-AzureRmSnapshot 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="05fc7-158">매개 변수는 스냅숏을 만들어서 프리미엄 Managed Disk로 저장되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="05fc7-159">프리미엄 Managed Disks는 표준 Managed Disks보다 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="05fc7-160">따라서 해당 매개 변수를 사용하기 전에 프리미엄이 필요한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="05fc7-161">스냅숏에서 새 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="05fc7-162">[New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)를 사용하여 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="05fc7-163">이 예제에서는 디스크 이름에 *myOSDisk*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="05fc7-164">새 VM에 대한 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="05fc7-165">OS 디스크 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="05fc7-166">관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="05fc7-167">새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-167">Create the new VM</span></span> 

<span data-ttu-id="05fc7-168">새 VM에서 사용할 네트워킹 및 기타 VM 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="05fc7-169">서브넷 및 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-169">Create the subNet and vNet</span></span>

<span data-ttu-id="05fc7-170">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="05fc7-171">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-171">Create the subNet.</span></span> <span data-ttu-id="05fc7-172">이 예제에서는 **myDestinationResourceGroup** 리소스 그룹에 **mySubNet**으로 명명된 서브넷을 만들고 **10.0.0.0/24**에 대한 서브넷 주소 접두사를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="05fc7-173">VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-173">Create the vNet.</span></span> <span data-ttu-id="05fc7-174">이 예제에서는 가상 네트워크 이름을 **myVnetName**으로, 위치를 **미국 서부**로, 가상 네트워크의 주소 접두사를 **10.0.0.0/16**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="05fc7-175">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="05fc7-176">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 보안 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="05fc7-177">새 VM의 VHD가 기존의 특수한 VM에서 생성되었기 때문에 원본 가상 컴퓨터의 계정을 RDP에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="05fc7-178">이 예제에서는 NSG 이름을 **myNsg**로 설정하고 RDP 규칙 이름을 **myRdpRule**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="05fc7-179">끝점 및 NSG 규칙에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05fc7-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="05fc7-180">공용 IP 주소 및 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="05fc7-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="05fc7-181">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="05fc7-182">공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-182">Create the public IP.</span></span> <span data-ttu-id="05fc7-183">이 예제에서는 공용 IP 주소 이름을 **myIP**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="05fc7-184">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="05fc7-184">Create the NIC.</span></span> <span data-ttu-id="05fc7-185">이 예제에서는 NIC 이름을 **myNicName**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="05fc7-186">VM 이름 및 크기 설정</span><span class="sxs-lookup"><span data-stu-id="05fc7-186">Set the VM name and size</span></span>

<span data-ttu-id="05fc7-187">이 예에서는 VM 이름을 *myVM*으로 설정하고 VM 크기를 *Standard_A2*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="05fc7-188">NIC 추가</span><span class="sxs-lookup"><span data-stu-id="05fc7-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="05fc7-189">OS 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="05fc7-189">Add the OS disk</span></span> 

<span data-ttu-id="05fc7-190">[Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)를 사용하여 OS 디스크를 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="05fc7-191">이 예에서는 디스크 크기를 *128GB*로 설정하고 Managed Disk를 *Windows* OS 디스크로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="05fc7-192">VM 완료</span><span class="sxs-lookup"><span data-stu-id="05fc7-192">Complete the VM</span></span> 

<span data-ttu-id="05fc7-193">방금 만든 [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm) 구성을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="05fc7-194">이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="05fc7-195">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="05fc7-195">Verify that the VM was created</span></span>
<span data-ttu-id="05fc7-196">새로 만든 VM은 [Azure Portal](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="05fc7-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05fc7-197">Next steps</span></span>
<span data-ttu-id="05fc7-198">새 가상 컴퓨터에 로그인하려면 [포털](https://portal.azure.com)에서 VM으로 이동한 다음 **연결**을 클릭하고 원격 데스크톱 RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="05fc7-199">원본 가상 컴퓨터의 계정 자격 증명을 사용하여 새 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="05fc7-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="05fc7-200">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05fc7-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

