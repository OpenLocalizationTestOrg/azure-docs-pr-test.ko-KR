---
title: "데이터 디스크 aaaExpand tooa Windows VM을 Azure에 연결 된 | Microsoft Docs"
description: "PowerShell을 사용 하 여 연결 된 tooa Windows 가상 컴퓨터에 있는 데이터 디스크의 hello 크기를 확장 합니다."
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
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="aa7e3-103">데이터 디스크의 크기를 늘리십시오. hello tooa Windows VM 연결</span><span class="sxs-lookup"><span data-stu-id="aa7e3-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="aa7e3-104">Hello 데이터 연결 된 디스크 tooyour 가상 컴퓨터의 tooincrease hello 크기, 필요한 경우 PowerShell을 사용 하 여 hello 크기를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="aa7e3-105">Hello Azure VM 설정에서 hello 데이터 디스크의 hello 크기를 늘린 후에 hello VM 내에서 tooallocate hello 새 디스크 공간이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="aa7e3-106">관리 되는 데이터 디스크의 Powershell tooincrease hello 크기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="aa7e3-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="aa7e3-107">관리 되는 데이터 디스크를 사용 하 여 hello PowerShell cmdlet을 다음 tooincrease hello 크기:</span><span class="sxs-lookup"><span data-stu-id="aa7e3-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="aa7e3-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="aa7e3-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="aa7e3-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="aa7e3-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="aa7e3-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="aa7e3-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="aa7e3-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="aa7e3-113">hello 다음 스크립트 과정을 안내 합니다 hello VM 정보를 가져오는 hello 데이터 디스크를 선택 하 고 hello 새 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="aa7e3-114">관리 되지 않는 데이터 디스크의 PowerShell tooincrease hello 크기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="aa7e3-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="aa7e3-115">다음 PowerShell cmdlet 사용 하 여 hello 저장소 계정에 관리 되지 않는 데이터 디스크의 tooincrease hello 크기:</span><span class="sxs-lookup"><span data-stu-id="aa7e3-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="aa7e3-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="aa7e3-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="aa7e3-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="aa7e3-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="aa7e3-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="aa7e3-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="aa7e3-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="aa7e3-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="aa7e3-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="aa7e3-122">hello 다음 스크립트 과정을 안내 합니다 hello VM 및 저장소 계정 정보를 얻는 hello 데이터 디스크를 선택 하 고 hello 새 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="aa7e3-123">Hello 할당 되지 않은 디스크 공간 할당</span><span class="sxs-lookup"><span data-stu-id="aa7e3-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="aa7e3-124">적용 하 고 나면 hello 드라이브 보다 큰, tooallocate hello 새 할당 되지 않은 공간 hello VM 내에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="aa7e3-125">tooallocate hello 공간, 디스크 관리 (diskmgmt.msc)를 사용 하 여 toohello VM을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="aa7e3-126">또는 원격 PowerShell tooinitialize hello 디스크를 활성화 한 경우 WinRM 및 hello VM에 인증서를 만들 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="aa7e3-127">또한 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="aa7e3-128">hello 스크립트 파일에이 코드 tooincrease hello 드라이브 할당 toohello 최대 크기 hello 디스크와 같은 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa7e3-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="aa7e3-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa7e3-129">Next Steps</span></span>
- [<span data-ttu-id="aa7e3-130">디스크 및 VHD에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="aa7e3-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
