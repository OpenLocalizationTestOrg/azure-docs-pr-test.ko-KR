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
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a>데이터 디스크의 크기를 늘리십시오. hello tooa Windows VM 연결

Hello 데이터 연결 된 디스크 tooyour 가상 컴퓨터의 tooincrease hello 크기, 필요한 경우 PowerShell을 사용 하 여 hello 크기를 늘릴 수 있습니다. Hello Azure VM 설정에서 hello 데이터 디스크의 hello 크기를 늘린 후에 hello VM 내에서 tooallocate hello 새 디스크 공간이 필요 합니다.


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a>관리 되는 데이터 디스크의 Powershell tooincrease hello 크기를 사용 하 여

관리 되는 데이터 디스크를 사용 하 여 hello PowerShell cmdlet을 다음 tooincrease hello 크기:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [Update-AzureRmDisk](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

hello 다음 스크립트 과정을 안내 합니다 hello VM 정보를 가져오는 hello 데이터 디스크를 선택 하 고 hello 새 크기를 지정 합니다.

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

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a>관리 되지 않는 데이터 디스크의 PowerShell tooincrease hello 크기를 사용 하 여

다음 PowerShell cmdlet 사용 하 여 hello 저장소 계정에 관리 되지 않는 데이터 디스크의 tooincrease hello 크기:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

hello 다음 스크립트 과정을 안내 합니다 hello VM 및 저장소 계정 정보를 얻는 hello 데이터 디스크를 선택 하 고 hello 새 크기를 지정 합니다.

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

## <a name="allocate-hello-unallocated-disk-space"></a>Hello 할당 되지 않은 디스크 공간 할당

적용 하 고 나면 hello 드라이브 보다 큰, tooallocate hello 새 할당 되지 않은 공간 hello VM 내에서 필요 합니다. tooallocate hello 공간, 디스크 관리 (diskmgmt.msc)를 사용 하 여 toohello VM을 연결할 수 있습니다. 또는 원격 PowerShell tooinitialize hello 디스크를 활성화 한 경우 WinRM 및 hello VM에 인증서를 만들 때 사용할 수 있습니다. 또한 사용자 지정 스크립트 확장을 사용할 수 있습니다.

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

hello 스크립트 파일에이 코드 tooincrease hello 드라이브 할당 toohello 최대 크기 hello 디스크와 같은 포함 될 수 있습니다.

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>다음 단계
- [디스크 및 VHD에 대해 자세히 알아보기](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
