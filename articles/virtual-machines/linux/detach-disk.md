---
title: "Linux VM에서 데이터 디스크 분리 - Azure | Microsoft Docs"
description: "CLI 2.0 또는 Azure Portal을 사용하여 Azure의 가상 컴퓨터에서 디스크를 분리하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="74255-103">Linux 가상 컴퓨터에서 데이터 디스크를 분리하는 방법</span><span class="sxs-lookup"><span data-stu-id="74255-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="74255-104">가상 컴퓨터에 연결된 데이터 디스크가 더 이상 필요하지 않은 경우 쉽게 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="74255-105">디스크를 분리하면 가상 컴퓨터에서 디스크가 제거되지만, 저장소에서는 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="74255-106">디스크를 분리해도 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="74255-107">프리미엄 저장소를 구독하는 경우 디스크에 대한 저장소 요금이 계속 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="74255-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="74255-108">자세한 내용은 [프리미엄 저장소 사용 시 가격 책정 및 청구](../../storage/common/storage-premium-storage.md#pricing-and-billing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74255-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="74255-109">디스크에 있는 기존 데이터를 다시 사용하려는 경우 동일한 또는 다른 가상 컴퓨터에 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="74255-110">CLI 2.0을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="74255-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="74255-111">디스크가 저장소에 유지되지만 더 이상 가상 컴퓨터에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="74255-112">포털을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="74255-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="74255-113">포털 허브에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="74255-114">분리할 데이터 디스크가 있는 가상 컴퓨터를 선택하고 **중지**를 클릭하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="74255-115">가상 컴퓨터 블레이드에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="74255-116">**디스크** 블레이드 상단에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="74255-117">**디스크** 블레이드에서 분리할 데이터 디스크의 맨 오른쪽에 있는 ![분리 단추 이미지](./media/detach-disk/detach.png) 분리 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="74255-118">디스크를 제거한 후에 블레이드 상단에서 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="74255-119">가상 컴퓨터 블레이드에서 **개요**를 클릭한 다음 블레이드 상단에서 **시작** 단추를 클릭하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74255-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="74255-120">디스크가 저장소에 유지되지만 더 이상 가상 컴퓨터에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="74255-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74255-121">Next steps</span></span>
<span data-ttu-id="74255-122">데이터 디스크를 다시 사용하려는 경우 [다른 VM에 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74255-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

