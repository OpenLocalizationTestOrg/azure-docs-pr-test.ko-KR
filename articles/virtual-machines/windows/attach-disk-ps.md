---
title: "데이터 디스크 tooa PowerShell을 사용 하 여 Azure에 Windows VM aaaAttach | Microsoft Docs"
description: "어떻게 tooattach 새로운 또는 기존의 데이터 디스크 tooa Windows VM hello 리소스 관리자 배포 모델에 PowerShell을 사용 합니다."
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
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="c91da-103">데이터 디스크 tooa Windows VM 연결 PowerShell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c91da-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="c91da-104">이 문서에 신규 및 기존 tooattach tooa PowerShell을 사용 하는 Windows 가상 컴퓨터 디스크 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="c91da-105">VM에서 관리 디스크를 사용하는 경우 관리 데이터 디스크를 추가로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="c91da-106">또한 관리 되지 않는 데이터 디스크 tooa 저장소 계정에 관리 되지 않는 디스크를 사용 하는 VM을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="c91da-107">이 작업을 수행 하기 전에 다음 팁을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="c91da-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="c91da-108">hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="c91da-109">자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c91da-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="c91da-110">프리미엄 저장소 toouse 프리미엄 저장소가 필요 합니다 처럼 hello DS 시리즈 또는 GS 시리즈 가상 컴퓨터 v M 크기를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="c91da-111">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="c91da-112">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="c91da-113">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c91da-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c91da-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c91da-114">Before you begin</span></span>
<span data-ttu-id="c91da-115">PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="c91da-116">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="c91da-117">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c91da-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="c91da-118">빈 데이터 디스크 tooa 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="c91da-119">이 예에서는 빈 데이터 tooadd tooan 기존 가상 컴퓨터 디스크 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="c91da-120">관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="c91da-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="c91da-121">저장소 계정에서 비관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="c91da-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="c91da-122">Hello 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="c91da-122">Initialize hello disk</span></span>

<span data-ttu-id="c91da-123">Tooinitialize 빈 디스크를 추가한 후 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="c91da-124">tooinitialize hello 디스크 tooa VM 및 사용 하 여 디스크 관리에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="c91da-125">를 활성화 한 경우 WinRM 및 hello VM에 인증서를 만들 때 원격 PowerShell tooinitialize hello 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="c91da-126">또한 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="c91da-127">hello 스크립트 파일에이 코드 tooinitialize hello 디스크와 같은 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="c91da-128">기존 데이터 디스크 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="c91da-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="c91da-129">또한 관리 되는 데이터 디스크 tooa 가상 컴퓨터로 기존 VHD를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="c91da-130">관리 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="c91da-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c91da-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c91da-131">Next steps</span></span>

<span data-ttu-id="c91da-132">[스냅숏](snapshot-copy-managed-disk.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c91da-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
