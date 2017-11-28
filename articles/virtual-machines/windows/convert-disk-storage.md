---
title: "Azure 관리 디스크 저장소를 표준에서 프리미엄으로, 또 그 반대로 변환 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Azure 관리 디스크를 표준에서 프리미엄으로, 또 그 반대로 변환하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 9e5c73ceb0ff7d9c18c9cf7128b69e40b9796874
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="d9051-103">Azure 관리 디스크 저장소를 표준에서 프리미엄으로, 또 그 반대로 변환</span><span class="sxs-lookup"><span data-stu-id="d9051-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="d9051-104">Managed Disks는 [프리미엄](../../storage/storage-premium-storage.md)(SSD 기반) 및 [표준](../../storage/storage-standard-storage.md)(HDD 기반)이라는 두 가지 저장소 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="d9051-105">성능 요구 사항에 따라 최소한의 가동 중지 시간으로 두 가지 옵션 사이를 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="d9051-106">이 기능은 관리되지 않는 디스크에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="d9051-107">하지만 두 옵션 사이를 쉽게 전환하도록 [관리 디스크로 변환](convert-unmanaged-to-managed-disks.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="d9051-108">이 문서는 Azure PowerShell을 사용하여 관리 디스크를 표준에서 프리미엄으로, 또 그 반대로 변환하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="d9051-109">설치 또는 업그레이드가 필요한 경우 [Azure PowerShell 설치 및 구성](/powershell/azure/install-azurerm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9051-109">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d9051-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d9051-110">Before you begin</span></span>

* <span data-ttu-id="d9051-111">변환은 기존 유지 관리 기간 동안 디스크 저장소의 마이그레이션을 예약하도록 VM의 재시작이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="d9051-112">관리되지 않는 디스크를 사용하는 경우 이 문서를 사용하여 두 가지 저장소 옵션 사이로 전환하려면 먼저 [관리 디스크로 변환](convert-unmanaged-to-managed-disks.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="d9051-113">VM의 모든 관리 디스크를 표준에서 프리미엄으로, 또 그 반대로 변환</span><span class="sxs-lookup"><span data-stu-id="d9051-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="d9051-114">다음 예제에서는 VM의 모든 디스크를 표준에서 프리미엄 저장소로 전환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="d9051-115">프리미엄 관리 디스크를 사용하려면 VM에서 프리미엄 저장소를 지원하는 [VM 크기](sizes.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="d9051-116">또한 이 예제에서는 프리미엄 저장소를 지원하는 크기로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-116">This example also switches to a size that supports premium storage.</span></span>

```powershell
# Name of the resource group that contains the VM
$rgName = 'yourResourceGroup'

# Name of the your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard to premium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate the VM before changing the size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in the resource group of the VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong to the selected VM, convert to premium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="d9051-117">관리 디스크를 표준에서 프리미엄으로, 또 그 반대로 변환</span><span class="sxs-lookup"><span data-stu-id="d9051-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="d9051-118">개발/테스트 워크로드의 경우 비용을 줄이기 위해 표준 및 프리미엄 디스크를 혼합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="d9051-119">더 나은 성능을 요구하는 디스크만 프리미엄 저장소로 업그레이드하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="d9051-120">다음 예제에서는 VM의 단일 디스크를 표준에서 프리미엄 저장소로, 또 그 반대로 전환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="d9051-121">프리미엄 관리 디스크를 사용하려면 VM에서 프리미엄 저장소를 지원하는 [VM 크기](sizes.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="d9051-122">또한 이 예제에서는 프리미엄 저장소를 지원하는 크기로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-122">This example also switches to a size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains the managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get the ARM resource to get name and resource group of the VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate the VM before changing the storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update the storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="d9051-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9051-123">Next steps</span></span>

<span data-ttu-id="d9051-124">[스냅숏](snapshot-copy-managed-disk.md)을 사용하여 VM의 읽기 전용 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9051-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

