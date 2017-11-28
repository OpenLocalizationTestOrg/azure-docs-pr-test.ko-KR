---
title: "Azure Redis Cache에 대 한 지리적 복제 aaaHow tooconfigure | Microsoft Docs"
description: "어떻게 tooreplicate Azure Redis 캐시 인스턴스를 여러 지리적 지역에 알아봅니다."
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
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a><span data-ttu-id="cf758-103">어떻게 Azure Redis Cache에 대 한 지리적 복제 tooconfigure</span><span class="sxs-lookup"><span data-stu-id="cf758-103">How tooconfigure Geo-replication for Azure Redis Cache</span></span>

<span data-ttu-id="cf758-104">지역에서 복제는 두 개의 프리미엄 계층 Azure Redis Cache 인스턴스를 연결하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-104">Geo-replication provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="cf758-105">캐시가 하나는 기본 연결 된 캐시 hello 및 hello hello 보조 연결 캐시로 다른으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-105">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="cf758-106">hello 보조 연결 된 캐시는 읽기 전용 및 서 면된 toohello 기본 캐시는 데이터 toohello 보조 연결 된 캐시를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-106">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="cf758-107">이 기능은 Azure 지역에서 사용 되는 tooreplicate 캐시 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-107">This functionality can be used tooreplicate a cache across Azure regions.</span></span> <span data-ttu-id="cf758-108">이 문서에서는 프리미엄 계층 Azure Redis 캐시 인스턴스에 대 한 가이드 tooconfiguring 지리적 복제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-108">This article provides a guide tooconfiguring Geo-replication for your Premium tier Azure Redis Cache instances.</span></span>

## <a name="geo-replication-prerequisites"></a><span data-ttu-id="cf758-109">지역에서 복제 필수 조건</span><span class="sxs-lookup"><span data-stu-id="cf758-109">Geo-replication prerequisites</span></span>

<span data-ttu-id="cf758-110">두 개의 캐시 hello 다음 필수 구성 요소 간의 tooconfigure 지리적 복제를 충족 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-110">tooconfigure Geo-replication between two caches, hello following prerequisites must be met:</span></span>

- <span data-ttu-id="cf758-111">두 캐시 모두 [프리미엄 계층](cache-premium-tier-intro.md) 캐시여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-111">Both caches must be [Premium tier](cache-premium-tier-intro.md) caches.</span></span>
- <span data-ttu-id="cf758-112">두 캐시는 hello에 있어야 합니다. 동일한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="cf758-112">Both caches must be in hello same Azure subscription.</span></span>
- <span data-ttu-id="cf758-113">hello 보조 연결 된 캐시 해야 수 있거나 hello 가격 계층 또는 기본 연결 된 캐시 hello 보다 더 큰 가격 책정 계층을 동일한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-113">hello secondary linked cache must be either hello same pricing tier or a larger pricing tier than hello primary linked cache.</span></span>
- <span data-ttu-id="cf758-114">Hello 기본 연결 된 캐시의 클러스터링을 사용, 연결 된 캐시를 보조 hello 가져야 클러스터링을 hello로 사용 hello 기본 연결 된 캐시와 같은 수의 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-114">If hello primary linked cache has clustering enabled, hello secondary linked cache must have clustering enabled with hello same number of shards as hello primary linked cache.</span></span>
- <span data-ttu-id="cf758-115">두 캐시 모두 만들어야 하며 실행 중 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-115">Both caches must be created and in a running state.</span></span>
- <span data-ttu-id="cf758-116">어느 캐시에서도 지속성을 사용하도록 설정하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-116">Persistence must not be enabled on either cache.</span></span>
- <span data-ttu-id="cf758-117">동일한 VNET은 지원 되는 hello에 대 한 캐시 간의 지리적 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-117">Geo-replication between caches in hello same VNET is supported.</span></span> <span data-ttu-id="cf758-118">다른 Vnet에 캐시 간의 지리적 복제도 지원 됩니다 hello Vnet의 리소스 수 tooreach 있는 방식으로 구성 된 두 hello Vnet으로 TCP 연결을 통해 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-118">Geo-replication between caches in different VNETs is also supported, as long as hello two VNETs are configured in such a way that resources in hello VNETs are able tooreach each other via TCP connections.</span></span>

<span data-ttu-id="cf758-119">지리적 복제를 구성한 후 hello 다음과 같은 제한 사항이 적용 tooyour 연결 된 캐시 쌍:</span><span class="sxs-lookup"><span data-stu-id="cf758-119">After Geo-replication is configured, hello following restrictions apply tooyour linked cache pair:</span></span>

- <span data-ttu-id="cf758-120">hello 보조 연결 된 캐시는 읽기 전용입니다. 여기에서 읽을 수 있지만 모든 데이터 tooit를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-120">hello secondary linked cache is read-only; you can read from it, but you can't write any data tooit.</span></span> 
- <span data-ttu-id="cf758-121">Hello 링크를 추가 하기 전에 hello 보조 연결 된 캐시에 있는 모든 데이터가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-121">Any data that was in hello secondary linked cache before hello link was added is removed.</span></span> <span data-ttu-id="cf758-122">하지만 Hello 지리적 복제는 이후에 제거, hello hello 보조 연결 된 캐시에 남아 있는 데이터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-122">If hello Geo-replication is subsequently removed however, hello replicated data remains in hello secondary linked cache.</span></span>
- <span data-ttu-id="cf758-123">시작할 수 없습니다는 [크기 조정 작업이](cache-how-to-scale.md) 어느 캐시 또는 [hello 분할 영역 수를 변경](cache-how-to-premium-clustering.md) hello 캐시에는 클러스터링을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="cf758-123">You can't initiate a [scaling operation](cache-how-to-scale.md) on either cache or [change hello number of shards](cache-how-to-premium-clustering.md) if hello cache has clustering enabled.</span></span>
- <span data-ttu-id="cf758-124">어느 캐시에서도 지속성을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-124">You can't enable persistence on either cache.</span></span>
- <span data-ttu-id="cf758-125">사용할 수 있습니다 [내보내기](cache-how-to-import-export-data.md#export) 어느 캐시와만 할 수 있습니다 하지만 [가져오기](cache-how-to-import-export-data.md#import) 기본 hello에 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-125">You can use [Export](cache-how-to-import-export-data.md#export) with either cache, but you can only [Import](cache-how-to-import-export-data.md#import) into hello primary linked cache.</span></span>
- <span data-ttu-id="cf758-126">연결 된 캐시 또는 hello 지역 간 복제 링크를 제거할 때까지, 포함 된 hello 리소스 그룹을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-126">You can't delete either linked cache, or hello resource group that contains them, until you remove hello Geo-replication link.</span></span> <span data-ttu-id="cf758-127">자세한 내용은 참조 [이유 hello 작업 실패 않았지만 toodelete 내 연결 된 캐시를 려 하면?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span><span class="sxs-lookup"><span data-stu-id="cf758-127">For more information, see [Why did hello operation fail when I tried toodelete my linked cache?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span></span>
- <span data-ttu-id="cf758-128">두 개의 캐시 hello 서로 다른 지역에 있는 경우 네트워크 송신 비용 toohello 데이터 영역 toohello 보조 연결 된 캐시에 걸쳐 복제 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-128">If hello two caches are in different regions, network egress costs will apply toohello data replicated across regions toohello secondary linked cache.</span></span> <span data-ttu-id="cf758-129">자세한 내용은 참조 [않는 손실이 tooreplicate 내 데이터 Azure 지역에 걸쳐?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span><span class="sxs-lookup"><span data-stu-id="cf758-129">For more information, see [How much does it cost tooreplicate my data across Azure regions?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span></span>
- <span data-ttu-id="cf758-130">기본 캐시 hello (및 해당 복제본) 다운 된 경우에 없는 자동 장애 조치 toohello 보조 연결 된 캐시입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-130">There is no automatic failover toohello secondary linked cache if hello primary cache (and its replica) go down.</span></span> <span data-ttu-id="cf758-131">순서 toofailover 클라이언트 응용 프로그램에서 toomanually hello 지리적 복제 연결 제거 해야 하 고 hello 클라이언트 응용 프로그램 toohello 캐시 하는 지점 였던 hello 보조 연결 된 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-131">In order toofailover client applications, you would need toomanually remove hello Geo-replication link and point hello client applications toohello cache that was formerly hello secondary linked cache.</span></span> <span data-ttu-id="cf758-132">자세한 내용은 참조 [어떻게 toohello 보조 연결 된 캐시 장애 조치할 작동 합니까?](#how-does-failing-over-to-the-secondary-linked-cache-work)</span><span class="sxs-lookup"><span data-stu-id="cf758-132">For more information, see [How does failing over toohello secondary linked cache work?](#how-does-failing-over-to-the-secondary-linked-cache-work)</span></span>

## <a name="add-a-geo-replication-link"></a><span data-ttu-id="cf758-133">지역에서 복제 링크 추가</span><span class="sxs-lookup"><span data-stu-id="cf758-133">Add a Geo-replication link</span></span>

1. <span data-ttu-id="cf758-134">두 개의 프리미엄 캐시 지리적 복제를 함께 toolink 클릭 **지리적 복제** hello 캐시 하기 위한 기본 연결 hello로의 hello 리소스 메뉴에서를 캐시 한 다음 클릭 **추가 캐시 복제 링크**hello에서 **지리적 복제** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-134">toolink two premium caches together for geo-replication, click **Geo-replication** from hello Resource menu of hello cache intended as hello primary linked cache, and then click **Add cache replication link** from hello **Geo-replication** blade.</span></span>

    ![링크 추가](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. <span data-ttu-id="cf758-136">Hello에서 원하는 hello 보조 캐시의 hello 이름을 클릭 **호환 캐시** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-136">Click hello name of hello desired secondary cache from hello **Compatible caches** list.</span></span> <span data-ttu-id="cf758-137">원하는 캐시 hello 목록에 표시 되지 않으면 해당 hello 확인 [지리적 복제 필수 구성 요소](#geo-replication-prerequisites) hello 원하는 보조 캐시 충족에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-137">If your desired cache isn't displayed in hello list, verify that hello [Geo-replication prerequisites](#geo-replication-prerequisites) for hello desired secondary cache are met.</span></span> <span data-ttu-id="cf758-138">지역에 따라 toofilter hello 캐시 hello hello에 캐시 된 hello 맵 toodisplay에서 원하는 지역을 클릭 **호환 캐시** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-138">toofilter hello caches by region, click hello desired region in hello map toodisplay only those caches in hello **Compatible caches** list.</span></span>

    ![지역에서 복제 호환되는 캐시](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    <span data-ttu-id="cf758-140">Hello 상황에 맞는 메뉴를 사용 하 여 hello 보조 캐시에 대 한 프로세스 또는 뷰 세부 정보를 연결 하는 hello를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-140">You can also initiate hello linking process or view details about hello secondary cache by using hello context menu.</span></span>

    ![지역에서 복제 상황에 맞는 메뉴](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. <span data-ttu-id="cf758-142">클릭 **링크** toolink 함께 두 개의 캐시 hello 및 hello 복제 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-142">Click **Link** toolink hello two caches together and begin hello replication process.</span></span>

    ![캐시 연결](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. <span data-ttu-id="cf758-144">Hello에 hello 복제 프로세스의 hello 진행률을 볼 수 있습니다 **지리적 복제** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-144">You can view hello progress of hello replication process on hello **Geo-replication** blade.</span></span>

    ![연결 상태](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    <span data-ttu-id="cf758-146">Hello hello에 상태 연결을 볼 수 있습니다 **개요** 블레이드 두 hello 기본 및 보조 캐시에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-146">You can also view hello linking status on hello **Overview** blade for both hello primary and secondary caches.</span></span>

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    <span data-ttu-id="cf758-148">Hello 복제 프로세스가 완료 되 면 hello **상태 연결** 쪽 변경**Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-148">Once hello replication process is complete, hello **Link status** changes too**Succeeded**.</span></span>

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    <span data-ttu-id="cf758-150">Hello 링크 프로세스, 하는 동안 hello 기본 연결 된 캐시를 계속 사용 하기 위해 사용할 수 있지만 hello 링크 프로세스 완료 될 때까지 hello 보조 연결 된 캐시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-150">During hello linking process, hello primary linked cache remains available for use but hello secondary linked cache is not available until hello linking process completes.</span></span>

## <a name="remove-a-geo-replication-link"></a><span data-ttu-id="cf758-151">지역에서 복제 링크 제거</span><span class="sxs-lookup"><span data-stu-id="cf758-151">Remove a Geo-replication link</span></span>

1. <span data-ttu-id="cf758-152">지리적 복제를 중지 하 고 두 개의 캐시 간의 tooremove hello 링크 클릭 **캐시의 연결을 해제** hello에서 **지리적 복제** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-152">tooremove hello link between two caches and stop Geo-replication, click **Unlink caches** from hello **Geo-replication** blade.</span></span>
    
    ![캐시 연결 해제](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    <span data-ttu-id="cf758-154">Hello 연결 해제 프로세스가 완료 되 면 hello 보조 캐시를 사용할 수 모두 읽기에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-154">When hello unlinking process completes, hello secondary cache is available for both reads and writes.</span></span>

>[!NOTE]
><span data-ttu-id="cf758-155">Hello 지리적 복제 링크가 제거 됩니다 hello hello 보조 캐시에 남아 있는 hello 기본 연결 된 캐시에서에서 데이터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-155">When hello Geo-replication link is removed, hello replicated data from hello primary linked cache remains in hello secondary cache.</span></span>
>
>

## <a name="geo-replication-faq"></a><span data-ttu-id="cf758-156">지역에서 복제 FAQ</span><span class="sxs-lookup"><span data-stu-id="cf758-156">Geo-replication FAQ</span></span>

- [<span data-ttu-id="cf758-157">표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-157">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [<span data-ttu-id="cf758-158">내 캐시는 hello 연결 또는 연결 해제 프로세스 중에 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-158">Is my cache available for use during hello linking or unlinking process?</span></span>](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [<span data-ttu-id="cf758-159">둘 이상의 캐시를 함께 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-159">Can I link more than two caches together?</span></span>](#can-i-link-more-than-two-caches-together)
- [<span data-ttu-id="cf758-160">서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-160">Can I link two caches from different Azure subscriptions?</span></span>](#can-i-link-two-caches-from-different-azure-subscriptions)
- [<span data-ttu-id="cf758-161">크기가 다른 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-161">Can I link two caches with different sizes?</span></span>](#can-i-link-two-caches-with-different-sizes)
- [<span data-ttu-id="cf758-162">클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-162">Can I use Geo-replication with clustering enabled?</span></span>](#can-i-use-geo-replication-with-clustering-enabled)
- [<span data-ttu-id="cf758-163">VNET의 캐시에 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-163">Can I use Geo-replication with my caches in a VNET?</span></span>](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [<span data-ttu-id="cf758-164">PowerShell 또는 Azure CLI toomanage 지리적 복제를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-164">Can I use PowerShell or Azure CLI toomanage Geo-replication?</span></span>](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [<span data-ttu-id="cf758-165">비용은 얼마 입니까 것 tooreplicate 내 데이터 Azure 지역에 걸쳐?</span><span class="sxs-lookup"><span data-stu-id="cf758-165">How much does it cost tooreplicate my data across Azure regions?</span></span>](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [<span data-ttu-id="cf758-166">연결 된 캐시 내 toodelete 시도 hello 작업 실패 이유는?</span><span class="sxs-lookup"><span data-stu-id="cf758-166">Why did hello operation fail when I tried toodelete my linked cache?</span></span>](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [<span data-ttu-id="cf758-167">보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-167">What region should I use for my secondary linked cache?</span></span>](#what-region-should-i-use-for-my-secondary-linked-cache)
- [<span data-ttu-id="cf758-168">장애 조치 toohello 보조 연결 된 캐시는 어떻게 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-168">How does failing over toohello secondary linked cache work?</span></span>](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a><span data-ttu-id="cf758-169">표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-169">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>

<span data-ttu-id="cf758-170">아니요, 지역에서 복제는 프리미엄 계층 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-170">No, Geo-replication is only available for Premium tier caches.</span></span>

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a><span data-ttu-id="cf758-171">내 캐시는 hello 연결 또는 연결 해제 프로세스 중에 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-171">Is my cache available for use during hello linking or unlinking process?</span></span>

- <span data-ttu-id="cf758-172">지리적 복제를 위한 두 개의 캐시를 함께 연결을 하는 경우 hello 기본 연결 된 캐시를 계속 사용 하기 위해 사용할 수 있지만 hello 링크 프로세스 완료 될 때까지 hello 보조 연결 된 캐시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-172">When linking two caches together for Geo-replication, hello primary linked cache remains available for use but hello secondary linked cache is not available until hello linking process completes.</span></span>
- <span data-ttu-id="cf758-173">두 개의 캐시 간의 hello 지역 간 복제 링크를 제거할 때 두 캐시에 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-173">When removing hello Geo-replication link between two caches, both caches remain available for use.</span></span>

### <a name="can-i-link-more-than-two-caches-together"></a><span data-ttu-id="cf758-174">둘 이상의 캐시를 함께 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-174">Can I link more than two caches together?</span></span>

<span data-ttu-id="cf758-175">아니요, 지역에서 복제를 사용하는 경우 두 개의 캐시만 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-175">No, when using Geo-replication you can only link two caches together.</span></span>

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a><span data-ttu-id="cf758-176">서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-176">Can I link two caches from different Azure subscriptions?</span></span>

<span data-ttu-id="cf758-177">없음, 모두 캐시는 hello에 있어야 합니다. 동일한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="cf758-177">No, both caches must be in hello same Azure subscription.</span></span>

### <a name="can-i-link-two-caches-with-different-sizes"></a><span data-ttu-id="cf758-178">크기가 다른 두 캐시를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-178">Can I link two caches with different sizes?</span></span>

<span data-ttu-id="cf758-179">예, 연결 된 보조 hello로 캐시는 hello 기본 연결 된 캐시 보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-179">Yes, as long as hello secondary linked cache is larger than hello primary linked cache.</span></span>

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a><span data-ttu-id="cf758-180">클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-180">Can I use Geo-replication with clustering enabled?</span></span>

<span data-ttu-id="cf758-181">예, hello를 보유 하는 두 캐시 같은 수의 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-181">Yes, as long as both caches have hello same number of shards.</span></span>

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a><span data-ttu-id="cf758-182">VNET의 캐시에 지역에서 복제를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-182">Can I use Geo-replication with my caches in a VNET?</span></span>

<span data-ttu-id="cf758-183">예, VNET의 캐시에 대한 지역에서 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-183">Yes, Geo-replication of caches in VNETs are supported.</span></span> 

- <span data-ttu-id="cf758-184">동일한 VNET은 지원 되는 hello에 대 한 캐시 간의 지리적 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-184">Geo-replication between caches in hello same VNET is supported.</span></span>
- <span data-ttu-id="cf758-185">다른 Vnet에 캐시 간의 지리적 복제도 지원 됩니다 hello Vnet의 리소스 수 tooreach 있는 방식으로 구성 된 두 hello Vnet으로 TCP 연결을 통해 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-185">Geo-replication between caches in different VNETs is also supported, as long as hello two VNETs are configured in such a way that resources in hello VNETs are able tooreach each other via TCP connections.</span></span>

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a><span data-ttu-id="cf758-186">PowerShell 또는 Azure CLI toomanage 지리적 복제를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-186">Can I use PowerShell or Azure CLI toomanage Geo-replication?</span></span>

<span data-ttu-id="cf758-187">관리할 수 있습니다이 이번에 지리적 복제를 사용 하 여 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-187">At this time you can only manage Geo-replication using hello Azure portal.</span></span>

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a><span data-ttu-id="cf758-188">비용은 얼마 입니까 것 tooreplicate 내 데이터 Azure 지역에 걸쳐?</span><span class="sxs-lookup"><span data-stu-id="cf758-188">How much does it cost tooreplicate my data across Azure regions?</span></span>

<span data-ttu-id="cf758-189">지리적 복제를 사용할 때는 hello 기본 연결 된 캐시에서 데이터는 복제 된 toohello 보조 연결 캐시입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-189">When using Geo-replication, data from hello primary linked cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="cf758-190">Hello에 캐시는 hello 두 연결 되어 있는 경우 동일한 Azure 지역 hello 데이터 전송에 대 한 요금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-190">If hello two linked caches are in hello same Azure region, there is no charge for hello data transfer.</span></span> <span data-ttu-id="cf758-191">Hello 두 연결 되어 있는 경우 다양 한 Azure 지역에 있는 캐시를 hello 지리적 복제 데이터 전송 요금과 해당 데이터 toohello 다른 Azure 지역 복제의 hello 대역폭 비용.</span><span class="sxs-lookup"><span data-stu-id="cf758-191">If hello two linked caches are in different Azure regions, hello Geo-Replication data transfer charge is hello bandwidth cost of replicating that data toohello other Azure region.</span></span> <span data-ttu-id="cf758-192">자세한 내용은 [대역폭 가격 정보](https://azure.microsoft.com/pricing/details/bandwidth/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf758-192">For more information, see [Bandwidth Pricing Details](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a><span data-ttu-id="cf758-193">연결 된 캐시 내 toodelete 시도 hello 작업 실패 이유는?</span><span class="sxs-lookup"><span data-stu-id="cf758-193">Why did hello operation fail when I tried toodelete my linked cache?</span></span>

<span data-ttu-id="cf758-194">두 개의 캐시를 함께 연결를 hello 지역 간 복제 링크를 제거할 때까지 포함 하는 캐시 또는 hello 리소스 그룹을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-194">When two caches are linked together, you can't delete either cache or hello resource group that contains them until you remove hello Geo-replication link.</span></span> <span data-ttu-id="cf758-195">사용 하려는 경우 toodelete hello 리소스 그룹에 하나 또는 둘 다의 hello 연결 캐시, hello hello 리소스 그룹의에서 다른 리소스는 삭제 되지만 hello에 유지 되는 hello 리소스 그룹 `deleting` 상태 및 모든 캐시 hello 리소스 그룹에 연결 hello에 남아 `running` 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-195">If you attempt toodelete hello resource group that contains one or both of hello linked caches, hello other resources in hello resource group are deleted, but hello resource group stays in hello `deleting` state and any linked caches in hello resource group remain in hello `running` state.</span></span> <span data-ttu-id="cf758-196">에 설명 된 대로 hello 리소스 그룹 및 hello toocomplete hello 삭제 연결 hello 지리적 복제 연결 끊기 그 안에 캐시 [지리적 복제 링크가 제거](#remove-a-geo-replication-link)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-196">toocomplete hello deletion of hello resource group and hello linked caches within it, break hello Geo-replication link as described in [Remove a Geo-replication link](#remove-a-geo-replication-link).</span></span>

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a><span data-ttu-id="cf758-197">보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cf758-197">What region should I use for my secondary linked cache?</span></span>

<span data-ttu-id="cf758-198">일반적으로 것이 좋습니다 프로그램 캐시 tooexist hello에 대 한 동일한 멤버에 액세스 하는 hello 응용 프로그램과 같은 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-198">In general, it is recommended for your cache tooexist in hello same Azure region as hello application that accesses it.</span></span> <span data-ttu-id="cf758-199">응용 프로그램에 주 지역과 대체 지역이 있는 경우 주 캐시와 보조 캐시가 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-199">If your application has a primary and fallback region, then your primary and secondary caches should exist in those same regions.</span></span> <span data-ttu-id="cf758-200">쌍을 이루는 지역에 대한 자세한 내용은 [모범 사례 - Azure 쌍을 이루는 지역](../best-practices-availability-paired-regions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf758-200">For more information about paired regions, see [Best Practices – Azure Paired regions](../best-practices-availability-paired-regions.md).</span></span>

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a><span data-ttu-id="cf758-201">장애 조치 toohello 보조 연결 된 캐시는 어떻게 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="cf758-201">How does failing over toohello secondary linked cache work?</span></span>

<span data-ttu-id="cf758-202">지역에서 복제의 초기 릴리스에서 hello Azure Redis Cache Azure 지역에서 자동 장애 조치를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-202">In hello initial release of Geo-replication, Azure Redis Cache does not support automatic failover across Azure regions.</span></span> <span data-ttu-id="cf758-203">지역에서 복제는 주로 재해 복구 시나리오에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-203">Geo-replication is used primarily in a disaster recovery scenario.</span></span> <span data-ttu-id="cf758-204">Distater 복구 시나리오에서 고객 상태가 됩니다 hello 전체 응용 프로그램 스택의 백업 지역에 있으므로 시기를 결정 하는 개별 응용 프로그램 구성 요소는 것이 아니라 조정 된 방식으로 자체적으로 tooswitch tootheir 백업.</span><span class="sxs-lookup"><span data-stu-id="cf758-204">In a distater recovery scenario, customers should bring up hello entire application stack in a backup region in a coordinated manner rather than letting individual application components decide when tooswitch tootheir backups on their own.</span></span> <span data-ttu-id="cf758-205">이 특히 관련 된 tooRedis입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-205">This is especially relevant tooRedis.</span></span> <span data-ttu-id="cf758-206">Redis의 hello 주요 이점 중 하나는 매우 짧은 대기 시간의 저장소 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-206">One of hello key benefits of Redis is that it is a very low-latency store.</span></span> <span data-ttu-id="cf758-207">Redis에서 사용 하는 응용 프로그램 장애 tooa 다른 Azure 지역의 조치 하지만 hello 계산 계층도 하지 않습니다, 그리고 이동 시간 라운드 추가 hello 성능에 거의 영향을 갖기 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-207">If Redis used by an application fails over tooa different Azure region but hello compute tier does not, hello added round trip time would have a noticeable impact on performance.</span></span> <span data-ttu-id="cf758-208">이러한 이유로 같은 tooavoid Redis 장애 조치 자동으로 tootransient 가용성 문제 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-208">For this reason, we would like tooavoid Redis failing over automatically due tootransient availability issues.</span></span>

<span data-ttu-id="cf758-209">현재 tooinitiate hello 장애 조치 해야 tooremove hello 지리적 복제 hello Azure 포털에에서 연결 하 고 다음 hello Redis 클라이언트에서 연결 끝점 hello hello 기본 연결 된 캐시 (이전 링크) toohello 보조 데이터베이스에서 변경 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-209">Currently, tooinitiate hello failover, you need tooremove hello Geo-replication link in hello Azure portal, and then change hello connection end-point in hello Redis client from hello primary linked cache toohello (formerly linked) secondary cache.</span></span> <span data-ttu-id="cf758-210">두 개의 캐시 된 연결을 끊을 hello hello 복제본 일반 상태일 때는 읽기 / 쓰기 캐시 다시 및 Redis 클라이언트에서 직접 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-210">When hello two caches are disassociated, hello replica becomes a regular read-write cache again and accepts requests directly from Redis clients.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf758-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf758-211">Next steps</span></span>

<span data-ttu-id="cf758-212">Hello에 대 한 자세한 [Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf758-212">Learn more about hello [Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

