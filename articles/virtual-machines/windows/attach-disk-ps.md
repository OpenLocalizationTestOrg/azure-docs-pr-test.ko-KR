---
title: "Azure에서 PowerShell을 사용하여 Windows VM에 데이터 디스크 연결 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 PowerShell을 사용하여 Windows VM에 신규 및 기존 데이터 디스크를 연결하는 방법을 설명합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="b1b8a-103">PowerShell을 사용하여 Windows VM에 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="b1b8a-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="b1b8a-104">이 문서에서는 PowerShell을 사용하여 신규 및 기존 디스크를 Windows 가상 컴퓨터에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="b1b8a-105">VM에서 관리 디스크를 사용하는 경우 관리 데이터 디스크를 추가로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="b1b8a-106">또한 저장소 계정의 비관리 디스크를 사용하는 VM에 비관리 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="b1b8a-107">이 작업을 수행 하기 전에 다음 팁을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="b1b8a-108">가상 컴퓨터의 크기로 연결할 수 있는 디스크 개수가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="b1b8a-109">자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b1b8a-110">Premium Storage를 사용하려면 DS 시리즈 또는 GS 시리즈 가상 컴퓨터처럼 Premium Storage 지원 VM 크기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="b1b8a-111">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="b1b8a-112">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="b1b8a-113">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1b8a-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b1b8a-114">Before you begin</span></span>
<span data-ttu-id="b1b8a-115">PowerShell을 사용하는 경우 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b1b8a-116">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b1b8a-117">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="b1b8a-118">가상 컴퓨터에 빈 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="b1b8a-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="b1b8a-119">이 예에서는 기존 가상 컴퓨터에 빈 데이터 디스크를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="b1b8a-120">관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="b1b8a-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="b1b8a-121">저장소 계정에서 비관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="b1b8a-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="b1b8a-122">디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="b1b8a-122">Initialize the disk</span></span>

<span data-ttu-id="b1b8a-123">빈 디스크를 추가한 후에는 디스크를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="b1b8a-124">디스크를 초기화하려면 VM에 로그인하여 디스크 관리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="b1b8a-125">VM을 만들 때 WinRM 및 인증서를 사용하도록 설정한 경우 원격 PowerShell을 사용하여 디스크를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="b1b8a-126">또한 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="b1b8a-127">스크립트 파일은 디스크를 초기화하기 위해 이 코드와 같은 것을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="b1b8a-128">VM에 기존 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="b1b8a-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="b1b8a-129">기존 VHD를 가상 컴퓨터에 관리 데이터 디스크로 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="b1b8a-130">관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="b1b8a-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="b1b8a-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1b8a-131">Next steps</span></span>

<span data-ttu-id="b1b8a-132">[스냅숏](snapshot-copy-managed-disk.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b8a-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
