---
title: "Azure에서 Windows VM에 연결된 데이터 디스크 확장 | Microsoft Docs"
description: "PowerShell을 사용하여 Windows 가상 컴퓨터에 연결된 데이터 디스크의 크기를 확장합니다."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: 5529856c2ffcd2942fe3fc2b438f7e3fd16a67b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a><span data-ttu-id="94328-103">Windows VM에 연결된 데이터 디스크의 크기 늘리기</span><span class="sxs-lookup"><span data-stu-id="94328-103">Increase the size of a data disk attached to a Windows VM</span></span>

<span data-ttu-id="94328-104">가상 컴퓨터에 연결된 데이터 디스크의 크기를 늘려야 할 경우 PowerShell을 사용하여 크기를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94328-104">If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell.</span></span> <span data-ttu-id="94328-105">Azure VM 설정에서 데이터 디스크의 크기를 늘린 후에 VM 내에서 새 디스크 공간을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-105">After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.</span></span>


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a><span data-ttu-id="94328-106">Powershell을 사용하여 관리되는 데이터 디스크의 크기 늘리기</span><span class="sxs-lookup"><span data-stu-id="94328-106">Use Powershell to increase the size of a managed data disk</span></span>

<span data-ttu-id="94328-107">관리되는 데이터 디스크의 크기를 늘리려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-107">To increase the size of a managed data disk, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="94328-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="94328-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="94328-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="94328-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="94328-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="94328-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="94328-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="94328-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="94328-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="94328-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="94328-113">다음 스크립트는 VM 정보를 가져오고, 데이터 디스크를 선택하고, 새 크기를 지정하는 과정을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-113">The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select the resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for the data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update the configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start the VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="94328-114">Powershell을 사용하여 관리되지 않는 데이터 디스크의 크기 늘리기</span><span class="sxs-lookup"><span data-stu-id="94328-114">Use PowerShell to increase the size of an unmanaged data disk</span></span>

<span data-ttu-id="94328-115">저장소 계정에서 관리되지 않는 데이터 디스크의 크기를 늘리려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-115">To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="94328-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="94328-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="94328-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="94328-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="94328-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="94328-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="94328-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="94328-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="94328-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="94328-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="94328-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="94328-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="94328-122">다음 스크립트는 VM 및 저장소 계정 정보를 가져오고, 데이터 디스크를 선택하고, 새 크기를 지정하는 과정을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-122">The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk to resize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk to resize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update the configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-the-unallocated-disk-space"></a><span data-ttu-id="94328-123">할당되지 않은 디스크 공간 할당</span><span class="sxs-lookup"><span data-stu-id="94328-123">Allocate the unallocated disk space</span></span>

<span data-ttu-id="94328-124">드라이브를 더 크게 만든 후에는 VM 내에서 할당되지 않은 새 공간을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94328-124">Once you have made the drive larger, you need to allocate the new unallocated space from within the VM.</span></span> <span data-ttu-id="94328-125">공간을 할당하려면 디스크 관리(diskmgmt.msc)를 사용하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94328-125">To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="94328-126">또는 VM을 만들 때 WinRM 및 인증서를 사용하도록 설정한 경우 원격 PowerShell을 사용하여 디스크를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94328-126">Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="94328-127">또한 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94328-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="94328-128">스크립트 파일에는 드라이브 할당을 최대 크기 및 디스크로 늘리는 다음과 같은 코드가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94328-128">The script file can contain something like this code to increase the drive allocation to the maximum size the disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="94328-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94328-129">Next Steps</span></span>
- [<span data-ttu-id="94328-130">디스크 및 VHD에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="94328-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
