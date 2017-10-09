---
title: "aaaConvert Azure 디스크 저장소를 관리 되는 표준 toopremium에서 그 반대의 | Microsoft Docs"
description: "어떻게 tooconvert Azure 표준 toopremium에서, 또는 그 반대로 Azure PowerShell을 사용 하 여 디스크를 관리 합니다."
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
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="322bb-103">Azure 변환 디스크 저장소를 관리 되는 표준 toopremium에서 그 반대의</span><span class="sxs-lookup"><span data-stu-id="322bb-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="322bb-104">Managed Disks는 [프리미엄](../../storage/storage-premium-storage.md)(SSD 기반) 및 [표준](../../storage/storage-standard-storage.md)(HDD 기반)이라는 두 가지 저장소 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="322bb-105">성능 요구 사항에 따라 최소한의 가동 중지 시간 hello 두 옵션 중 적합 한 tooeasily 스위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="322bb-106">이 기능은 관리되지 않는 디스크에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="322bb-107">에 쉽게 하지만 [toomanaged 디스크 변환](convert-unmanaged-to-managed-disks.md) tooeasily hello 두 옵션 사이 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="322bb-108">이 문서에서 표준 toopremium 그 반대의 Azure PowerShell을 사용 하 여 tooconvert 디스크를 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="322bb-109">Tooinstall 필요 하거나 업그레이드할 참조 [설치 Azure PowerShell을 구성 하 고](/powershell/azure/install-azurerm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="322bb-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="322bb-110">Before you begin</span></span>

* <span data-ttu-id="322bb-111">hello 변환 hello VM의 다시 시작이 필요한, 하므로 기존 유지 관리 기간 동안 디스크 저장소의 hello 마이그레이션을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="322bb-112">먼저 관리 되지 않는 디스크를 사용 하는 경우 [toomanaged 디스크 변환](convert-unmanaged-to-managed-disks.md) toouse hello 두 저장소 옵션 중 적합 한이 문서 tooswitch 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="322bb-113">모든 hello convert 관리 디스크 VM의 표준 toopremium에서 그 반대의</span><span class="sxs-lookup"><span data-stu-id="322bb-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="322bb-114">다음 예제는 hello,에서는 보여줍니다 방법을 tooswitch 표준 toopremium 저장소에서 VM의 디스크 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="322bb-115">toouse 프리미엄 관리 디스크 VM 사용 해야 합니다는 [VM 크기](sizes.md) 프리미엄 저장소를 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="322bb-116">이 예제에서는 프리미엄 저장소를 지 원하는 tooa 크기를 전환 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="322bb-117">관리 되는 디스크 변환에서 표준 toopremium 그 반대의</span><span class="sxs-lookup"><span data-stu-id="322bb-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="322bb-118">개발/테스트 워크 로드에 대 한 toohave 다양 한 표준 및 프리미엄 디스크 tooreduce 비용을 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="322bb-119">더 나은 성능을 요구 하는 hello 디스크만 toopremium 저장소를 업그레이드 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="322bb-120">다음 예제는 hello,에서는 보여줍니다 어떻게 tooswitch VM의 단일 디스크 표준 toopremium 저장소에서 그 반대의 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="322bb-121">toouse 프리미엄 관리 디스크 VM 사용 해야 합니다는 [VM 크기](sizes.md) 프리미엄 저장소를 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="322bb-122">이 예제에서는 프리미엄 저장소를 지 원하는 tooa 크기를 전환 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="322bb-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="322bb-123">Next steps</span></span>

<span data-ttu-id="322bb-124">[스냅숏](snapshot-copy-managed-disk.md)을 사용하여 VM의 읽기 전용 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="322bb-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

