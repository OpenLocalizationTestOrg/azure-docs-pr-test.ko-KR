---
title: "Azure Redis Cache에 대해 지역에서 복제를 구성하는 방법 | Microsoft Docs"
description: "지역 간에 Azure Redis Cache 인스턴스를 복제하는 방법을 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: 71b0d4add7e642487f6d67cda692c500ee78b0e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-geo-replication-for-azure-redis-cache"></a><span data-ttu-id="7ff5c-103">Azure Redis Cache에 대해 지역에서 복제를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="7ff5c-103">How to configure Geo-replication for Azure Redis Cache</span></span>

<span data-ttu-id="7ff5c-104">지역에서 복제는 두 개의 프리미엄 계층 Azure Redis Cache 인스턴스를 연결하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-104">Geo-replication provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="7ff5c-105">한 캐시는 주 연결된 캐시로 지정하고 다른 캐시는 보조 연결된 캐시로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-105">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="7ff5c-106">보조 연결된 캐시는 읽기 전용이 되고 주 캐시에 쓴 데이터는 보조 연결된 캐시에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-106">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="7ff5c-107">이 기능은 Azure 지역 간에 캐시를 복제하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-107">This functionality can be used to replicate a cache across Azure regions.</span></span> <span data-ttu-id="7ff5c-108">이 문서에서는 프리미엄 계층 Azure Redis Cache 인스턴스에 대해 지역에서 복제를 구성하는 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-108">This article provides a guide to configuring Geo-replication for your Premium tier Azure Redis Cache instances.</span></span>

## <a name="geo-replication-prerequisites"></a><span data-ttu-id="7ff5c-109">지역에서 복제 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7ff5c-109">Geo-replication prerequisites</span></span>

<span data-ttu-id="7ff5c-110">두 캐시 간에 지역에서 복제를 구성하려면 다음 필수 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-110">To configure Geo-replication between two caches, the following prerequisites must be met:</span></span>

- <span data-ttu-id="7ff5c-111">두 캐시 모두 [프리미엄 계층](cache-premium-tier-intro.md) 캐시여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-111">Both caches must be [Premium tier](cache-premium-tier-intro.md) caches.</span></span>
- <span data-ttu-id="7ff5c-112">두 캐시 모두 동일한 Azure 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-112">Both caches must be in the same Azure subscription.</span></span>
- <span data-ttu-id="7ff5c-113">보조 연결된 캐시는 주 연결된 캐시와 동일한 가격 책정 계층이거나 더 큰 가격 책정 계층이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-113">The secondary linked cache must be either the same pricing tier or a larger pricing tier than the primary linked cache.</span></span>
- <span data-ttu-id="7ff5c-114">주 연결된 캐시에서 클러스터링을 사용하는 경우 보조 연결된 캐시는 분할된 데이터베이스 수가 주 연결된 캐시와 동일한 클러스터링을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-114">If the primary linked cache has clustering enabled, the secondary linked cache must have clustering enabled with the same number of shards as the primary linked cache.</span></span>
- <span data-ttu-id="7ff5c-115">두 캐시 모두 만들어야 하며 실행 중 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-115">Both caches must be created and in a running state.</span></span>
- <span data-ttu-id="7ff5c-116">어느 캐시에서도 지속성을 사용하도록 설정하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-116">Persistence must not be enabled on either cache.</span></span>
- <span data-ttu-id="7ff5c-117">동일한 VNET에 있는 캐시 간의 지역에서 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-117">Geo-replication between caches in the same VNET is supported.</span></span> <span data-ttu-id="7ff5c-118">VNET의 리소스가 TCP 연결을 통해 서로 연결할 수 있는 방식으로 두 VNET이 구성된 경우에는 다른 VNET에 있는 캐시 간의 지역에서 복제도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-118">Geo-replication between caches in different VNETs is also supported, as long as the two VNETs are configured in such a way that resources in the VNETs are able to reach each other via TCP connections.</span></span>

<span data-ttu-id="7ff5c-119">지역에서 복제를 구성한 후에는 연결된 캐시 쌍에 다음과 같은 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-119">After Geo-replication is configured, the following restrictions apply to your linked cache pair:</span></span>

- <span data-ttu-id="7ff5c-120">보조 연결된 캐시는 읽기 전용입니다. 이 캐시에서 읽을 수는 있지만 데이터를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-120">The secondary linked cache is read-only; you can read from it, but you can't write any data to it.</span></span> 
- <span data-ttu-id="7ff5c-121">링크를 추가하기 전에 보조 연결된 캐시에 있던 모든 데이터가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-121">Any data that was in the secondary linked cache before the link was added is removed.</span></span> <span data-ttu-id="7ff5c-122">그러나 이후에 지역에서 복제를 제거하면 복제된 데이터는 보조 연결된 캐시에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-122">If the Geo-replication is subsequently removed however, the replicated data remains in the secondary linked cache.</span></span>
- <span data-ttu-id="7ff5c-123">어느 캐시에서도 [크기 조정 작업](cache-how-to-scale.md)을 시작할 수 없거나 캐시에 클러스터링이 설정된 경우 [분할된 데이터베이스 수를 변경](cache-how-to-premium-clustering.md)할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-123">You can't initiate a [scaling operation](cache-how-to-scale.md) on either cache or [change the number of shards](cache-how-to-premium-clustering.md) if the cache has clustering enabled.</span></span>
- <span data-ttu-id="7ff5c-124">어느 캐시에서도 지속성을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-124">You can't enable persistence on either cache.</span></span>
- <span data-ttu-id="7ff5c-125">[내보내기](cache-how-to-import-export-data.md#export)는 두 캐시에서 사용할 수 있지만 [가져오기](cache-how-to-import-export-data.md#import)는 기본 연결된 캐시에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-125">You can use [Export](cache-how-to-import-export-data.md#export) with either cache, but you can only [Import](cache-how-to-import-export-data.md#import) into the primary linked cache.</span></span>
- <span data-ttu-id="7ff5c-126">지역에서 복제 링크를 제거할 때까지 연결된 캐시 또는 캐시가 포함된 리소스 그룹을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-126">You can't delete either linked cache, or the resource group that contains them, until you remove the Geo-replication link.</span></span> <span data-ttu-id="7ff5c-127">자세한 내용은 [연결된 캐시를 삭제하려고 할 때 작업이 실패한 이유는 무엇인가요?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-127">For more information, see [Why did the operation fail when I tried to delete my linked cache?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span></span>
- <span data-ttu-id="7ff5c-128">두 캐시가 다른 지역에 있는 경우 네트워크 송신 비용이 지역 간에 보조 연결된 캐시로 복제된 데이터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-128">If the two caches are in different regions, network egress costs will apply to the data replicated across regions to the secondary linked cache.</span></span> <span data-ttu-id="7ff5c-129">자세한 내용은 [Azure 지역 간에 데이터를 복제하는 비용은 어느 정도인가요?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-129">For more information, see [How much does it cost to replicate my data across Azure regions?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span></span>
- <span data-ttu-id="7ff5c-130">주 캐시 및 해당 복제본이 중단되는 경우 보조 연결된 캐시로 자동 장애 조치(failover)되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-130">There is no automatic failover to the secondary linked cache if the primary cache (and its replica) go down.</span></span> <span data-ttu-id="7ff5c-131">클라이언트 응용 프로그램을 장애 조치(failover)하려면 지역에서 복제 링크를 수동으로 제거하고 클라이언트 응용 프로그램이 이전의 보조 연결된 캐시였던 캐시를 가리키도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-131">In order to failover client applications, you would need to manually remove the Geo-replication link and point the client applications to the cache that was formerly the secondary linked cache.</span></span> <span data-ttu-id="7ff5c-132">자세한 내용은 [보조 연결된 캐시로 장애 조치(failover)는 어떻게 작동하나요?](#how-does-failing-over-to-the-secondary-linked-cache-work)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-132">For more information, see [How does failing over to the secondary linked cache work?](#how-does-failing-over-to-the-secondary-linked-cache-work)</span></span>

## <a name="add-a-geo-replication-link"></a><span data-ttu-id="7ff5c-133">지역에서 복제 링크 추가</span><span class="sxs-lookup"><span data-stu-id="7ff5c-133">Add a Geo-replication link</span></span>

1. <span data-ttu-id="7ff5c-134">지역에서 복제를 위해 두 프리미엄 캐시를 함께 연결하려면 주 연결된 캐시로 사용된 캐시의 리소스 메뉴에서 **지역에서 복제**를 클릭한 다음 **지역에서 복제** 블레이드에서 **Add cache replication link**(캐시 복제 링크 추가)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-134">To link two premium caches together for geo-replication, click **Geo-replication** from the Resource menu of the cache intended as the primary linked cache, and then click **Add cache replication link** from the **Geo-replication** blade.</span></span>

    ![링크 추가](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. <span data-ttu-id="7ff5c-136">**Compatible caches**(호환되는 캐시) 목록에서 원하는 보조 캐시의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-136">Click the name of the desired secondary cache from the **Compatible caches** list.</span></span> <span data-ttu-id="7ff5c-137">원하는 캐시가 목록에 표시되지 않으면 원하는 보조 캐시에 대한 [지역에서 복제 필수 조건](#geo-replication-prerequisites)이 충족되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-137">If your desired cache isn't displayed in the list, verify that the [Geo-replication prerequisites](#geo-replication-prerequisites) for the desired secondary cache are met.</span></span> <span data-ttu-id="7ff5c-138">지역으로 캐시를 필터링하려면 지도에서 원하는 지역을 클릭하여 해당 캐시만 **Compatible caches**(호환되는 캐시) 목록에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-138">To filter the caches by region, click the desired region in the map to display only those caches in the **Compatible caches** list.</span></span>

    ![지역에서 복제 호환되는 캐시](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    <span data-ttu-id="7ff5c-140">상황에 맞는 메뉴를 사용하여 연결 프로세스를 시작하거나 보조 캐시에 대한 세부 정보를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-140">You can also initiate the linking process or view details about the secondary cache by using the context menu.</span></span>

    ![지역에서 복제 상황에 맞는 메뉴](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. <span data-ttu-id="7ff5c-142">**링크**를 클릭하여 두 캐시를 함께 연결하고 복제 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-142">Click **Link** to link the two caches together and begin the replication process.</span></span>

    ![캐시 연결](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. <span data-ttu-id="7ff5c-144">**지역에서 복제** 블레이드에서 복제 프로세스의 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-144">You can view the progress of the replication process on the **Geo-replication** blade.</span></span>

    ![연결 상태](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    <span data-ttu-id="7ff5c-146">주 캐시와 보조 캐시에 대한 **개요** 블레이드에서 연결 상태를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-146">You can also view the linking status on the **Overview** blade for both the primary and secondary caches.</span></span>

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    <span data-ttu-id="7ff5c-148">복제 프로세스가 완료되면 **링크 상태**가 **성공**으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-148">Once the replication process is complete, the **Link status** changes to **Succeeded**.</span></span>

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    <span data-ttu-id="7ff5c-150">연결 프로세스 중에 주 연결된 캐시는 계속 사용할 수 있지만 보조 연결된 캐시는 연결 프로세스가 완료된 다음에야 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-150">During the linking process, the primary linked cache remains available for use but the secondary linked cache is not available until the linking process completes.</span></span>

## <a name="remove-a-geo-replication-link"></a><span data-ttu-id="7ff5c-151">지역에서 복제 링크 제거</span><span class="sxs-lookup"><span data-stu-id="7ff5c-151">Remove a Geo-replication link</span></span>

1. <span data-ttu-id="7ff5c-152">두 캐시 간 링크를 제거하고 지역에서 복제를 중지하려면 **지역에서 복제** 블레이드에서 **Unlink caches**(캐시 연결 해제)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-152">To remove the link between two caches and stop Geo-replication, click **Unlink caches** from the **Geo-replication** blade.</span></span>
    
    ![캐시 연결 해제](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    <span data-ttu-id="7ff5c-154">연결 해제 프로세스가 완료되면 보조 캐시를 읽기 및 쓰기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-154">When the unlinking process completes, the secondary cache is available for both reads and writes.</span></span>

>[!NOTE]
><span data-ttu-id="7ff5c-155">지역에서 복제 링크를 제거해도 주 연결된 캐시에서 복제된 데이터는 보조 캐시에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-155">When the Geo-replication link is removed, the replicated data from the primary linked cache remains in the secondary cache.</span></span>
>
>

## <a name="geo-replication-faq"></a><span data-ttu-id="7ff5c-156">지역에서 복제 FAQ</span><span class="sxs-lookup"><span data-stu-id="7ff5c-156">Geo-replication FAQ</span></span>

- [<span data-ttu-id="7ff5c-157">표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-157">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [<span data-ttu-id="7ff5c-158">연결 또는 연결 해제 프로세스 중에 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-158">Is my cache available for use during the linking or unlinking process?</span></span>](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [<span data-ttu-id="7ff5c-159">둘 이상의 캐시를 함께 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-159">Can I link more than two caches together?</span></span>](#can-i-link-more-than-two-caches-together)
- [<span data-ttu-id="7ff5c-160">서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-160">Can I link two caches from different Azure subscriptions?</span></span>](#can-i-link-two-caches-from-different-azure-subscriptions)
- [<span data-ttu-id="7ff5c-161">크기가 다른 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-161">Can I link two caches with different sizes?</span></span>](#can-i-link-two-caches-with-different-sizes)
- [<span data-ttu-id="7ff5c-162">클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-162">Can I use Geo-replication with clustering enabled?</span></span>](#can-i-use-geo-replication-with-clustering-enabled)
- [<span data-ttu-id="7ff5c-163">VNET의 캐시에 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-163">Can I use Geo-replication with my caches in a VNET?</span></span>](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [<span data-ttu-id="7ff5c-164">PowerShell 또는 Azure CLI를 사용하여 지역에서 복제를 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-164">Can I use PowerShell or Azure CLI to manage Geo-replication?</span></span>](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [<span data-ttu-id="7ff5c-165">Azure 지역 간에 데이터를 복제하는 비용은 어느 정도인가요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-165">How much does it cost to replicate my data across Azure regions?</span></span>](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [<span data-ttu-id="7ff5c-166">연결된 캐시를 삭제하려고 할 때 작업이 실패한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-166">Why did the operation fail when I tried to delete my linked cache?</span></span>](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [<span data-ttu-id="7ff5c-167">보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-167">What region should I use for my secondary linked cache?</span></span>](#what-region-should-i-use-for-my-secondary-linked-cache)
- [<span data-ttu-id="7ff5c-168">보조 연결된 캐시로 장애 조치(failover)는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-168">How does failing over to the secondary linked cache work?</span></span>](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a><span data-ttu-id="7ff5c-169">표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-169">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>

<span data-ttu-id="7ff5c-170">아니요, 지역에서 복제는 프리미엄 계층 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-170">No, Geo-replication is only available for Premium tier caches.</span></span>

### <a name="is-my-cache-available-for-use-during-the-linking-or-unlinking-process"></a><span data-ttu-id="7ff5c-171">연결 또는 연결 해제 프로세스 중에 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-171">Is my cache available for use during the linking or unlinking process?</span></span>

- <span data-ttu-id="7ff5c-172">지역에서 복제를 위해 두 캐시를 함께 연결하는 경우 주 연결된 캐시는 계속 사용할 수 있지만 보조 연결된 캐시는 연결 프로세스가 완료된 다음에야 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-172">When linking two caches together for Geo-replication, the primary linked cache remains available for use but the secondary linked cache is not available until the linking process completes.</span></span>
- <span data-ttu-id="7ff5c-173">두 캐시 간에 지역에서 복제 링크를 제거하면 두 캐시 모두 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-173">When removing the Geo-replication link between two caches, both caches remain available for use.</span></span>

### <a name="can-i-link-more-than-two-caches-together"></a><span data-ttu-id="7ff5c-174">둘 이상의 캐시를 함께 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-174">Can I link more than two caches together?</span></span>

<span data-ttu-id="7ff5c-175">아니요, 지역에서 복제를 사용하는 경우 두 개의 캐시만 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-175">No, when using Geo-replication you can only link two caches together.</span></span>

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a><span data-ttu-id="7ff5c-176">서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-176">Can I link two caches from different Azure subscriptions?</span></span>

<span data-ttu-id="7ff5c-177">아니요, 두 캐시 모두 동일한 Azure 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-177">No, both caches must be in the same Azure subscription.</span></span>

### <a name="can-i-link-two-caches-with-different-sizes"></a><span data-ttu-id="7ff5c-178">크기가 다른 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-178">Can I link two caches with different sizes?</span></span>

<span data-ttu-id="7ff5c-179">예, 보조 연결된 캐시가 주 연결된 캐시보다 큰 경우 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-179">Yes, as long as the secondary linked cache is larger than the primary linked cache.</span></span>

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a><span data-ttu-id="7ff5c-180">클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-180">Can I use Geo-replication with clustering enabled?</span></span>

<span data-ttu-id="7ff5c-181">예, 두 캐시의 분할된 데이터베이스 수가 동일한 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-181">Yes, as long as both caches have the same number of shards.</span></span>

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a><span data-ttu-id="7ff5c-182">VNET의 캐시에 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-182">Can I use Geo-replication with my caches in a VNET?</span></span>

<span data-ttu-id="7ff5c-183">예, VNET의 캐시에 대한 지역에서 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-183">Yes, Geo-replication of caches in VNETs are supported.</span></span> 

- <span data-ttu-id="7ff5c-184">동일한 VNET에 있는 캐시 간의 지역에서 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-184">Geo-replication between caches in the same VNET is supported.</span></span>
- <span data-ttu-id="7ff5c-185">VNET의 리소스가 TCP 연결을 통해 서로 연결할 수 있는 방식으로 두 VNET이 구성된 경우에는 다른 VNET에 있는 캐시 간의 지역에서 복제도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-185">Geo-replication between caches in different VNETs is also supported, as long as the two VNETs are configured in such a way that resources in the VNETs are able to reach each other via TCP connections.</span></span>

### <a name="can-i-use-powershell-or-azure-cli-to-manage-geo-replication"></a><span data-ttu-id="7ff5c-186">PowerShell 또는 Azure CLI를 사용하여 지역에서 복제를 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-186">Can I use PowerShell or Azure CLI to manage Geo-replication?</span></span>

<span data-ttu-id="7ff5c-187">현재 지역에서 복제는 Azure Portal을 통해서만 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-187">At this time you can only manage Geo-replication using the Azure portal.</span></span>

### <a name="how-much-does-it-cost-to-replicate-my-data-across-azure-regions"></a><span data-ttu-id="7ff5c-188">Azure 지역 간에 데이터를 복제하는 비용은 어느 정도인가요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-188">How much does it cost to replicate my data across Azure regions?</span></span>

<span data-ttu-id="7ff5c-189">지역에서 복제를 사용하면 주 연결된 캐시의 데이터가 보조 연결된 캐시에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-189">When using Geo-replication, data from the primary linked cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="7ff5c-190">두 연결된 캐시가 같은 Azure 지역에 있는 경우 데이터 전송에 대한 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-190">If the two linked caches are in the same Azure region, there is no charge for the data transfer.</span></span> <span data-ttu-id="7ff5c-191">두 연결된 캐시가 다른 Azure 지역에 있는 경우 지역에서 복제 데이터 전송 요금은 해당 데이터를 다른 Azure 지역에 복제하는 대역폭 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-191">If the two linked caches are in different Azure regions, the Geo-Replication data transfer charge is the bandwidth cost of replicating that data to the other Azure region.</span></span> <span data-ttu-id="7ff5c-192">자세한 내용은 [대역폭 가격 정보](https://azure.microsoft.com/pricing/details/bandwidth/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-192">For more information, see [Bandwidth Pricing Details](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache"></a><span data-ttu-id="7ff5c-193">연결된 캐시를 삭제하려고 할 때 작업이 실패한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-193">Why did the operation fail when I tried to delete my linked cache?</span></span>

<span data-ttu-id="7ff5c-194">두 개의 캐시가 함께 연결된 경우 지역에서 복제 링크를 제거할 때까지 연결된 캐시 또는 캐시가 포함된 리소스 그룹을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-194">When two caches are linked together, you can't delete either cache or the resource group that contains them until you remove the Geo-replication link.</span></span> <span data-ttu-id="7ff5c-195">연결된 캐시 중 하나 또는 둘 다를 포함하는 리소스 그룹을 삭제하려고 하면, 리소스 그룹의 다른 리소스는 삭제되지만 해당 리소스 그룹은 `deleting` 상태로 유지되고 이 리소스 그룹의 연결된 캐시는 모두 `running` 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-195">If you attempt to delete the resource group that contains one or both of the linked caches, the other resources in the resource group are deleted, but the resource group stays in the `deleting` state and any linked caches in the resource group remain in the `running` state.</span></span> <span data-ttu-id="7ff5c-196">리소스 그룹 및 연결된 캐시의 삭제를 완료하려면 [지역에서 복제 링크 제거](#remove-a-geo-replication-link)에서 설명한 대로 지역에서 복제 링크를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-196">To complete the deletion of the resource group and the linked caches within it, break the Geo-replication link as described in [Remove a Geo-replication link](#remove-a-geo-replication-link).</span></span>

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a><span data-ttu-id="7ff5c-197">보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-197">What region should I use for my secondary linked cache?</span></span>

<span data-ttu-id="7ff5c-198">일반적으로 캐시는 해당 캐시에 액세스하는 응용 프로그램과 동일한 Azure 지역에 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-198">In general, it is recommended for your cache to exist in the same Azure region as the application that accesses it.</span></span> <span data-ttu-id="7ff5c-199">응용 프로그램에 주 지역과 대체 지역이 있는 경우 주 캐시와 보조 캐시가 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-199">If your application has a primary and fallback region, then your primary and secondary caches should exist in those same regions.</span></span> <span data-ttu-id="7ff5c-200">쌍을 이루는 지역에 대한 자세한 내용은 [모범 사례 - Azure 쌍을 이루는 지역](../best-practices-availability-paired-regions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-200">For more information about paired regions, see [Best Practices – Azure Paired regions](../best-practices-availability-paired-regions.md).</span></span>

### <a name="how-does-failing-over-to-the-secondary-linked-cache-work"></a><span data-ttu-id="7ff5c-201">보조 연결된 캐시로 장애 조치(failover)는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="7ff5c-201">How does failing over to the secondary linked cache work?</span></span>

<span data-ttu-id="7ff5c-202">지역에서 복제의 초기 릴리스에서는 Azure Redis Cache가 Azure 지역 간의 자동 장애 조치(failover)를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-202">In the initial release of Geo-replication, Azure Redis Cache does not support automatic failover across Azure regions.</span></span> <span data-ttu-id="7ff5c-203">지역에서 복제는 주로 재해 복구 시나리오에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-203">Geo-replication is used primarily in a disaster recovery scenario.</span></span> <span data-ttu-id="7ff5c-204">재해 복구 시나리오에서 고객은 개별 응용 프로그램 구성 요소가 백업을 자체적으로 전환할 시기를 결정할 수 있도록 하는 것이 아니라 조정된 방식으로 전체 응용 프로그램 스택을 백업 지역에 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-204">In a distater recovery scenario, customers should bring up the entire application stack in a backup region in a coordinated manner rather than letting individual application components decide when to switch to their backups on their own.</span></span> <span data-ttu-id="7ff5c-205">특히 Redis와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-205">This is especially relevant to Redis.</span></span> <span data-ttu-id="7ff5c-206">Redis의 주요 이점 중 하나는 대기 시간이 매우 짧은 저장소라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-206">One of the key benefits of Redis is that it is a very low-latency store.</span></span> <span data-ttu-id="7ff5c-207">응용 프로그램에서 사용하는 Redis는 다른 Azure 지역으로 장애 조치(failover)되지만 계산 계층은 그렇지 않을 경우 왕복 시간이 추가되어 성능에 크게 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-207">If Redis used by an application fails over to a different Azure region but the compute tier does not, the added round trip time would have a noticeable impact on performance.</span></span> <span data-ttu-id="7ff5c-208">따라서 일시적인 가용성 문제로 인해 Redis에서 자동으로 장애 조치(failover)하는 것을 방지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-208">For this reason, we would like to avoid Redis failing over automatically due to transient availability issues.</span></span>

<span data-ttu-id="7ff5c-209">현재 장애 조치(failover)를 시작하려면 Azure Portal에서 지역에서 복제 링크를 제거하고 Redis 클라이언트에서 연결 끝점을 주 연결된 캐시에서 (이전의 연결된) 보조 캐시로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-209">Currently, to initiate the failover, you need to remove the Geo-replication link in the Azure portal, and then change the connection end-point in the Redis client from the primary linked cache to the (formerly linked) secondary cache.</span></span> <span data-ttu-id="7ff5c-210">두 캐시의 연결이 해제되면 복제본은 다시 일반적인 읽기/쓰기 캐시가 되고 Redis 클라이언트에서 직접 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-210">When the two caches are disassociated, the replica becomes a regular read-write cache again and accepts requests directly from Redis clients.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ff5c-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ff5c-211">Next steps</span></span>

<span data-ttu-id="7ff5c-212">[Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7ff5c-212">Learn more about the [Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

