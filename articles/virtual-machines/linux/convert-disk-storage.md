---
title: "aaaConvert Azure 디스크 저장소를 관리 되는 표준 toopremium에서 그 반대의 | Microsoft Docs"
description: "어떻게 tooconvert Azure 표준 toopremium에서, 또는 그 반대로 Azure CLI를 사용 하 여 디스크 저장소를 관리 합니다."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="d453f-103">Azure 변환 디스크 저장소를 관리 되는 표준 toopremium에서 그 반대의</span><span class="sxs-lookup"><span data-stu-id="d453f-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="d453f-104">Managed Disks는 [프리미엄](../../storage/storage-premium-storage.md)(SSD 기반) 및 [표준](../../storage/storage-standard-storage.md)(HDD 기반)이라는 두 가지 저장소 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="d453f-105">성능 요구 사항에 따라 최소한의 가동 중지 시간 hello 두 옵션 중 적합 한 tooeasily 스위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="d453f-106">이 기능은 관리되지 않는 디스크에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="d453f-107">에 쉽게 하지만 [toomanaged 디스크 변환](convert-unmanaged-to-managed-disks.md) tooeasily hello 두 옵션 사이 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="d453f-108">이 문서에서 표준 toopremium 그 반대의 Azure CLI를 사용 하 여 tooconvert 디스크를 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="d453f-109">Tooinstall 필요 하거나 업그레이드할 참조 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d453f-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d453f-110">Before you begin</span></span>

* <span data-ttu-id="d453f-111">hello 변환 hello VM의 다시 시작이 필요한, 하므로 기존 유지 관리 기간 동안 디스크 저장소의 hello 마이그레이션을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="d453f-112">먼저 관리 되지 않는 디스크를 사용 하는 경우 [toomanaged 디스크 변환](convert-unmanaged-to-managed-disks.md) toouse hello 두 저장소 옵션 중 적합 한이 문서 tooswitch 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="d453f-113">모든 hello convert 관리 디스크 VM의 표준 toopremium에서 그 반대의</span><span class="sxs-lookup"><span data-stu-id="d453f-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="d453f-114">다음 예제는 hello,에서는 보여줍니다 방법을 tooswitch 표준 toopremium 저장소에서 VM의 디스크 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="d453f-115">toouse 프리미엄 관리 디스크 VM 사용 해야 합니다는 [VM 크기](sizes.md) 프리미엄 저장소를 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="d453f-116">이 예제에서는 프리미엄 저장소를 지 원하는 tooa 크기를 전환 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-116">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="d453f-117">관리 되는 디스크 변환에서 표준 toopremium 그 반대의</span><span class="sxs-lookup"><span data-stu-id="d453f-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="d453f-118">개발/테스트 워크 로드에 대 한 toohave 다양 한 표준 및 프리미엄 디스크 tooreduce 비용을 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="d453f-119">더 나은 성능을 요구 하는 hello 디스크만 toopremium 저장소를 업그레이드 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="d453f-120">다음 예제는 hello,에서는 보여줍니다 어떻게 tooswitch VM의 단일 디스크 표준 toopremium 저장소에서 그 반대의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="d453f-121">toouse 프리미엄 관리 디스크 VM 사용 해야 합니다는 [VM 크기](sizes.md) 프리미엄 저장소를 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="d453f-122">이 예제에서는 프리미엄 저장소를 지 원하는 tooa 크기를 전환 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-122">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="d453f-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d453f-123">Next steps</span></span>

<span data-ttu-id="d453f-124">[스냅숏](snapshot-copy-managed-disk.md)을 사용하여 VM의 읽기 전용 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d453f-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

