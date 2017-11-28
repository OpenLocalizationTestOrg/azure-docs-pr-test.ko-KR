---
title: Azure Redis Cache aaaHow tooconfigure | Microsoft Docs
description: "Azure Redis Cache에 대 한 hello 기본 Redis 구성 이해 하 고 자세한 방법을 tooconfigure Azure Redis 캐시 인스턴스"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="09524-103">Azure Redis 캐시 하는 tooconfigure 방법</span><span class="sxs-lookup"><span data-stu-id="09524-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="09524-104">이 항목에서는 tooreview 및 업데이트 하면 Azure Redis 캐시 인스턴스에 대 한 구성 및 Azure Redis 캐시 인스턴스에 대 한 표지 hello 기본 Redis 서버 구성 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="09524-105">구성 및 프리미엄 캐시 기능 사용에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconfigure 지 속성](cache-how-to-premium-persistence.md), [어떻게 클러스터링 tooconfigure](cache-how-to-premium-clustering.md), 및 [tooconfigure 가상 네트워크를 지 원하는 방법 ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="09524-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="09524-106">Redis 캐시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="09524-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="09524-107">Azure Redis 캐시 설정은 보고 되며 hello에 구성 된 **Redis Cache** hello를 사용 하 여 블레이드 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Redis 캐시 설정](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="09524-109">보고 구성 하는 hello hello를 사용 하 여 설정을 다음 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="09524-110">개요</span><span class="sxs-lookup"><span data-stu-id="09524-110">Overview</span></span>](#overview)
* [<span data-ttu-id="09524-111">활동 로그</span><span class="sxs-lookup"><span data-stu-id="09524-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="09524-112">액세스 제어(IAM)</span><span class="sxs-lookup"><span data-stu-id="09524-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="09524-113">태그</span><span class="sxs-lookup"><span data-stu-id="09524-113">Tags</span></span>](#tags)
* [<span data-ttu-id="09524-114">문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="09524-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="09524-115">설정</span><span class="sxs-lookup"><span data-stu-id="09524-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="09524-116">액세스 키</span><span class="sxs-lookup"><span data-stu-id="09524-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="09524-117">고급 설정</span><span class="sxs-lookup"><span data-stu-id="09524-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="09524-118">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="09524-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="09524-119">규모</span><span class="sxs-lookup"><span data-stu-id="09524-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="09524-120">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="09524-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="09524-121">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="09524-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="09524-122">업데이트 예약</span><span class="sxs-lookup"><span data-stu-id="09524-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="09524-123">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="09524-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="09524-124">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="09524-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="09524-125">방화벽</span><span class="sxs-lookup"><span data-stu-id="09524-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="09524-126">속성</span><span class="sxs-lookup"><span data-stu-id="09524-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="09524-127">잠금</span><span class="sxs-lookup"><span data-stu-id="09524-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="09524-128">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="09524-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="09524-129">관리</span><span class="sxs-lookup"><span data-stu-id="09524-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="09524-130">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="09524-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="09524-131">데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="09524-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="09524-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="09524-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="09524-133">모니터링</span><span class="sxs-lookup"><span data-stu-id="09524-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="09524-134">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="09524-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="09524-135">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="09524-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="09524-136">진단</span><span class="sxs-lookup"><span data-stu-id="09524-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="09524-137">설정 지원 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09524-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="09524-138">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="09524-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="09524-139">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="09524-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="09524-140">개요</span><span class="sxs-lookup"><span data-stu-id="09524-140">Overview</span></span>

<span data-ttu-id="09524-141">**개요**에서는 이름, 포트, 가격 책정 계층 및 선택한 캐시 메트릭과 같은 캐시에 대한 기본 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="09524-142">활동 로그</span><span class="sxs-lookup"><span data-stu-id="09524-142">Activity log</span></span>

<span data-ttu-id="09524-143">클릭 **활동 로그** tooview 작업 캐시에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="09524-144">사용할 수도 있습니다 tooexpand 필터링이 뷰 tooinclude 기타 참고 자료.</span><span class="sxs-lookup"><span data-stu-id="09524-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="09524-145">감사 로그 작업에 대한 자세한 내용은 [Resource Manager를 사용하는 감사 작업](../azure-resource-manager/resource-group-audit.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="09524-146">Azure Redis Cache 이벤트 모니터링에 대한 자세한 내용은 [작업 및 경고](cache-how-to-monitor.md#operations-and-alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="09524-147">액세스 제어(IAM)</span><span class="sxs-lookup"><span data-stu-id="09524-147">Access control (IAM)</span></span>

<span data-ttu-id="09524-148">hello **액세스 제어 (IAM)** 섹션 지원을 제공 역할 기반 액세스 제어 (RBAC)에 대 한 hello Azure 포털 toohelp 조직 충족에 대 한 액세스 관리 요구 사항을 단순히 정확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="09524-149">자세한 내용은 참조 [hello Azure 포털의에서 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="09524-150">태그들</span><span class="sxs-lookup"><span data-stu-id="09524-150">Tags</span></span>

<span data-ttu-id="09524-151">hello **태그** 섹션 리소스 구성할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="09524-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="09524-152">자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="09524-153">문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="09524-153">Diagnose and solve problems</span></span>

<span data-ttu-id="09524-154">클릭 **진단 및 문제 해결** toobe 전략 및 일반적인 문제 해결을 위한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="09524-155">설정</span><span class="sxs-lookup"><span data-stu-id="09524-155">Settings</span></span>
<span data-ttu-id="09524-156">hello **설정을** 섹션 tooaccess 있으며 hello 다음 캐시에 대 한 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="09524-157">액세스 키</span><span class="sxs-lookup"><span data-stu-id="09524-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="09524-158">고급 설정</span><span class="sxs-lookup"><span data-stu-id="09524-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="09524-159">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="09524-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="09524-160">규모</span><span class="sxs-lookup"><span data-stu-id="09524-160">Scale</span></span>](#scale)
* [<span data-ttu-id="09524-161">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="09524-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="09524-162">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="09524-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="09524-163">업데이트 예약</span><span class="sxs-lookup"><span data-stu-id="09524-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="09524-164">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="09524-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="09524-165">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="09524-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="09524-166">방화벽</span><span class="sxs-lookup"><span data-stu-id="09524-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="09524-167">속성</span><span class="sxs-lookup"><span data-stu-id="09524-167">Properties</span></span>](#properties)
* [<span data-ttu-id="09524-168">잠금</span><span class="sxs-lookup"><span data-stu-id="09524-168">Locks</span></span>](#locks)
* [<span data-ttu-id="09524-169">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="09524-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="09524-170">액세스 키</span><span class="sxs-lookup"><span data-stu-id="09524-170">Access keys</span></span>
<span data-ttu-id="09524-171">클릭 **선택키가** tooview 또는 regenerate hello 액세스 캐시에 대 한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="09524-172">이러한 키는 tooyour 캐시를 연결 하는 hello 클라이언트에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Redis 캐시 액세스 키](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="09524-174">고급 설정</span><span class="sxs-lookup"><span data-stu-id="09524-174">Advanced settings</span></span>
<span data-ttu-id="09524-175">hello 다음 설정에 구성 된 hello **고급 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="09524-176">액세스 포트</span><span class="sxs-lookup"><span data-stu-id="09524-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="09524-177">메모리 정책</span><span class="sxs-lookup"><span data-stu-id="09524-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="09524-178">Keyspace 알림(고급 설정)</span><span class="sxs-lookup"><span data-stu-id="09524-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="09524-179">액세스 포트</span><span class="sxs-lookup"><span data-stu-id="09524-179">Access Ports</span></span>
<span data-ttu-id="09524-180">비 SSL 액세스는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="09524-181">tooenable hello 비 SSL 포트를 클릭 하 여 **아니요** 에 대 한 **SSL 통해서만 액세스 허용** hello에 **고급 설정** 블레이드에 대 한 클릭 한 다음 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Redis 캐시 액세스 포트](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="09524-183">메모리 정책</span><span class="sxs-lookup"><span data-stu-id="09524-183">Memory policies</span></span>
<span data-ttu-id="09524-184">hello **최대 메모리 정책**, **maxmemory 예약**, 및 **maxfragmentationmemory 예약** hello 설정을 **고급 설정**블레이드 hello 캐시에 대 한 hello 메모리 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Redis 캐시 Maxmemory 정책](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="09524-186">**최대 메모리 정책** hello 캐시의 제거 정책 hello를 구성 하 고 다음 제거 정책을 hello에서 toochoose 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="09524-187">`volatile-lru`-hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="09524-188">`maxmemory` 정책에 대한 자세한 내용은 [제거 정책](http://redis.io/topics/lru-cache#eviction-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="09524-189">hello **maxmemory 예약** 장애 조치 중 복제와 같은 캐시가 비 작업에 대해 예약 된 mb에서 hello 메모리 양을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="09524-190">이 값으로 설정 하면 보다 일관 된 Redis 서버 환경을 toohave 부하 변경 될 때.</span><span class="sxs-lookup"><span data-stu-id="09524-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="09524-191">이 값은 쓰기 작업이 많은 워크로드에서 더 높게 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="09524-192">이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="09524-193">hello **maxfragmentationmemory 예약** 메모리 조각화에 대 한 예약 된 tooaccommodate은 mb에서 hello 메모리 양을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="09524-194">이 값으로 설정 하면 toohave 보다 일관 된 Redis 서버 환경을 hello 캐시가 가득 차거나 닫기 toofull 및 hello 조각화 비율이 높습니다도 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="09524-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="09524-195">이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="09524-196">새 메모리 예약 값을 선택할 때 한 가지 tooconsider (**maxmemory 예약** 또는 **maxfragmentationmemory 예약**)는 이러한 변경으로 이미 실행 중인 캐시에 미칠 수 있는 많은 양의 데이터가 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="09524-197">예를 들어, 49 g b의 데이터를 53GB 캐시가 hello 예약 값 too8 GB 변경 한 후이 too45 GB 다운 hello 시스템에 대 한 최대 사용 가능한 메모리를 hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="09524-198">경우 현재 `used_memory` 또는 사용자의 `used_memory_rss` 45 GB의 hello 새 제한 보다 더 높은 값은 다음 hello 시스템 있는 tooevict 데이터 둘 다를 때까지 됩니다 `used_memory` 및 `used_memory_rss` 45 GB 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="09524-199">제거는 서버 부하 및 메모리 조각화를 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="09524-200">`used_memory` 및 `used_memory_rss`와 같은 캐시 메트릭에 대한 자세한 내용은 [사용 가능한 메트릭 및 보고 간격](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-201">hello **maxmemory 예약** 및 **maxfragmentationmemory 예약** 설정이 있습니다만 표준 및 프리미엄 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="09524-202">Keyspace 알림(고급 설정)</span><span class="sxs-lookup"><span data-stu-id="09524-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="09524-203">Hello에 알림이 구성 되어 있어 실제로 redis **고급 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="09524-204">키 스페이스 알림에서 특정 이벤트가 발생할 때 클라이언트 tooreceive 알림의 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Redis 캐시 고급 설정](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="09524-206">키 스페이스 알림 및 hello **키 스페이스 알림-이벤트** 설정을 표준 및 프리미엄 캐시에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="09524-207">자세한 내용은 [Redis Keyspace 알림](http://redis.io/topics/notifications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="09524-208">샘플 코드에 대 한 참조 hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) hello에 대 한 파일 [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.</span><span class="sxs-lookup"><span data-stu-id="09524-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="09524-209">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="09524-209">Redis Cache Advisor</span></span>
<span data-ttu-id="09524-210">hello **Redis 캐시 관리자** 블레이드에서 캐시에 대 한 권장 사항을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="09524-211">정상적으로 작동하는 중에는 추천이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-211">During normal operations, no recommendations are displayed.</span></span> 

![권장 사항](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="09524-213">Hello에 경고가 표시 된 높은 메모리 사용량, 네트워크 대역폭, 서버 부하 등 캐시 hello 작업 중에 모든 조건의 상황이 발생 하면 **Redis Cache** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![권장 사항](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="09524-215">Hello에서 추가 정보를 확인할 수 있습니다 **권장 사항을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-215">Further information can be found on hello **Recommendations** blade.</span></span>

![권장 사항](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="09524-217">Hello에 이러한 메트릭을 모니터링할 수 있습니다 [모니터링 차트](cache-how-to-monitor.md#monitoring-charts) 및 [사용 현황 차트](cache-how-to-monitor.md#usage-charts) hello의 섹션 **Redis Cache** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="09524-218">가격 책정 계층마다 클라이언트 연결, 메모리 및 대역폭에 대한 제한이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="09524-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="09524-219">캐시가 오랫동안 이러한 메트릭의 최대 용량에 근접하면 추천이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="09524-220">Hello 메트릭 및 제한 사항을 검토 하 여 hello에 대 한 자세한 내용은 **권장 사항을** 도구 hello 다음 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="09524-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="09524-221">Redis Cache 메트릭</span><span class="sxs-lookup"><span data-stu-id="09524-221">Redis Cache metric</span></span> | <span data-ttu-id="09524-222">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="09524-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="09524-223">네트워크 대역폭 사용량</span><span class="sxs-lookup"><span data-stu-id="09524-223">Network bandwidth usage</span></span> |[<span data-ttu-id="09524-224">캐시 성능 - 사용 가능한 대역폭</span><span class="sxs-lookup"><span data-stu-id="09524-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="09524-225">연결된 클라이언트</span><span class="sxs-lookup"><span data-stu-id="09524-225">Connected clients</span></span> |[<span data-ttu-id="09524-226">기본 Redis 서버 구성 - maxclients</span><span class="sxs-lookup"><span data-stu-id="09524-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="09524-227">서버 부하</span><span class="sxs-lookup"><span data-stu-id="09524-227">Server load</span></span> |[<span data-ttu-id="09524-228">사용 현황 차트 - Redis 서버 부하</span><span class="sxs-lookup"><span data-stu-id="09524-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="09524-229">메모리 사용량</span><span class="sxs-lookup"><span data-stu-id="09524-229">Memory usage</span></span> |[<span data-ttu-id="09524-230">캐시 성능 - 크기</span><span class="sxs-lookup"><span data-stu-id="09524-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="09524-231">tooupgrade 캐시를 클릭 하 여 **지금 업그레이드** toochange hello 가격 책정 계층 및 [배율](#scale) 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="09524-232">가격 책정 계층 선택에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="09524-233">확장</span><span class="sxs-lookup"><span data-stu-id="09524-233">Scale</span></span>
<span data-ttu-id="09524-234">클릭 **배율** tooview 또는 변경 hello 가격 책정 계층에 대 한 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="09524-235">확장에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooScale Azure Redis 캐시](cache-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis Cache 가격 책정 계층](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="09524-237">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="09524-237">Redis Cluster Size</span></span>
<span data-ttu-id="09524-238">클릭 **(미리 보기) Redis 클러스터 크기** toochange hello 클러스터 크기를 실행 중인 premium에 대 한 캐시 클러스터링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="09524-239">Azure Redis Cache 프리미엄 계층 되었습니다 hello 하는 동안 tooGeneral 가용성, hello Redis 클러스터 크기 기능을 해제 하는 현재 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 클러스터 크기](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="09524-241">toochange hello 클러스터 크기 hello 슬라이더를 사용 하거나 hello에 1과 10 사이의 숫자를 입력 **분할 영역 수** 텍스트 상자 **확인** toosave 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-242">Redis 클러스터링은 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="09524-243">자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](cache-how-to-premium-clustering.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="09524-244">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="09524-244">Redis data persistence</span></span>
<span data-ttu-id="09524-245">클릭 **Redis 데이터 지 속성** tooenable, 해제 또는 프리미엄 캐시에 대 한 데이터 지 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="09524-246">Azure Redis Cache는 [RDB 지속성](cache-how-to-premium-persistence.md#configure-rdb-persistence) 또는 [AOF 지속성](cache-how-to-premium-persistence.md#configure-aof-persistence)을 사용하여 Redis 지속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="09524-247">자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 지 속성 tooconfigure](cache-how-to-premium-persistence.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="09524-248">Redis 데이터 지속성은 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="09524-249">업데이트를 예약</span><span class="sxs-lookup"><span data-stu-id="09524-249">Schedule updates</span></span>
<span data-ttu-id="09524-250">hello **업데이트를 예약할** 블레이드 toodesignate 캐시에 대 한 Redis 서버 업데이트에 대 한 유지 관리 기간을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="09524-251">tooRedis 서버 업데이트 및 Azure 업데이트 또는 hello 캐시를 호스트 하는 hello Vm의 toohello 운영 체제를 업데이트 하지 tooany hello 유지 관리 기간에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![업데이트를 예약](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="09524-253">toospecify 유지 관리 기간 hello 원하는 일 수를 확인 합니다. 각 날에 대 한 hello 유지 관리 창 시작 시간을 지정 고를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="09524-254">Hello 유지 관리 기간에 UTC를 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="09524-255">hello **업데이트를 예약할** 기능은 프리미엄 계층 캐시에 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="09524-256">자세한 내용 및 지침은 [Azure Redis Cache 관리 - 업데이트 예약](cache-administration.md#schedule-updates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="09524-257">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="09524-257">Geo-replication</span></span>

<span data-ttu-id="09524-258">hello **지리적 복제** 블레이드 두 프리미엄 계층 Azure Redis Cache 인스턴스 연결을 위한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="09524-259">캐시가 하나는 기본 연결 된 캐시 hello 및 hello hello 보조 연결 캐시로 다른으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="09524-260">hello 보조 연결 된 캐시는 읽기 전용 및 서 면된 toohello 기본 캐시는 데이터 toohello 보조 연결 된 캐시를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="09524-261">이 기능은 Azure 지역에서 사용 되는 tooreplicate 캐시 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-262">**지역에서 복제**는 프리미엄 계층 캐시에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="09524-263">자세한 내용 및 지침에 대 한 참조 [어떻게 Azure Redis Cache에 대 한 지리적 복제 tooconfigure](cache-how-to-geo-replication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="09524-264">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="09524-264">Virtual Network</span></span>
<span data-ttu-id="09524-265">hello **가상 네트워크** 섹션 캐시에 대 한 tooconfigure hello 가상 네트워크 설정을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="09524-266">VNET을 사용 하 여 프리미엄 캐시를 만들기에 대 한 내용은 지원 하 고 해당 설정을 업데이트 하는, 참조 [tooconfigure 가상 네트워크는 프리미엄 Azure Redis Cache에 대 한 지원 방법](cache-how-to-premium-vnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-267">가상 네트워크 설정은 캐시를 만드는 동안 VNET 지원을 통해 구성된 프리미엄 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="09524-268">방화벽</span><span class="sxs-lookup"><span data-stu-id="09524-268">Firewall</span></span>

<span data-ttu-id="09524-269">클릭 **방화벽** tooview 고 프리미엄 Azure Redis Cache에 대 한 방화벽 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![방화벽](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="09524-271">시작 및 끝 IP 주소 범위를 사용하여 방화벽 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="09524-272">방화벽 규칙을 구성 하는 경우 hello 클라이언트 연결만 지정 IP 주소 범위 toohello 캐시에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="09524-273">방화벽 규칙을 저장할 때 연기 되는 짧은 hello 적용 되므로 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="09524-274">이러한 지연 시간은 일반적으로 1분 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-275">방화벽 규칙이 구성된 경우에도 Azure Redis Cache 모니터링 시스템에서의 연결은 항상 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="09524-276">방화벽 규칙은 프리미엄 계층 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="09524-277">properties</span><span class="sxs-lookup"><span data-stu-id="09524-277">Properties</span></span>
<span data-ttu-id="09524-278">클릭 **속성** hello 캐시 끝점 및 포트 등 캐시에 대 한 tooview 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Redis 캐시 속성](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="09524-280">잠금</span><span class="sxs-lookup"><span data-stu-id="09524-280">Locks</span></span>
<span data-ttu-id="09524-281">hello **잠급니다** toolock 구독, 리소스 그룹 또는 리소스 tooprevent 섹션에서는 있습니다 다른 조직의 사용자에 실수로 삭제 하거나 중요 한 리소스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="09524-282">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="09524-283">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="09524-283">Automation script</span></span>

<span data-ttu-id="09524-284">클릭 **자동화 스크립트** toobuild 향후 배포에 배포 된 리소스의 템플릿 내보내기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="09524-285">템플릿 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="09524-286">관리 설정</span><span class="sxs-lookup"><span data-stu-id="09524-286">Administration settings</span></span>
<span data-ttu-id="09524-287">hello 설정을 hello **관리** 섹션 허용 tooperform hello 캐시에 대 한 관리 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![관리](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="09524-289">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="09524-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="09524-290">데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="09524-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="09524-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="09524-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="09524-292">가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="09524-292">Import/Export</span></span>
<span data-ttu-id="09524-293">가져오기/내보내기는 내보내고 Azure 저장소 계정에서 프리미엄 캐시 tooa 페이지 blob에서 Redis 캐시 데이터베이스 (RDB) 스냅숏 내보내기 hello 캐시에 tooimport 및 내보내기 데이터 허용 하는 Azure Redis Cache 데이터 관리 작업.</span><span class="sxs-lookup"><span data-stu-id="09524-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="09524-294">가져오기/내보내기 toomigrate 서로 다른 Azure Redis Cache 인스턴스 간에 사용 하면 또는 hello 캐시 사용 하기 전에 데이터를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="09524-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="09524-295">가져오기에는 클라우드 또는 Linux, Windows 또는 Amazon 웹 서비스 등과 같은 모든 클라우드 공급자에서 실행 되는 Redis를 포함 하 여 환경에서 실행 중인 모든 Redis 서버에서 사용 되는 toobring Redis 호환 RDB 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="09524-296">데이터 가져오기는 쉽게 toocreate 미리 채워진된 데이터와 함께 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="09524-297">Hello 가져오기 프로세스 동안 Azure Redis Cache hello RDB 파일을 Azure 저장소에서 메모리에 로드 한 다음 hello 캐시로 hello 키를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="09524-298">내보내기는 Azure Redis Cache tooRedis 호환 RDB 파일에 저장 된 tooexport hello 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="09524-299">Azure Redis Cache 인스턴스 tooanother 또는 tooanother Redis 서버 하나에서이 기능 toomove 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="09524-300">Hello 내보내기 과정에서 임시 파일 VM 호스트 hello Azure Redis Cache 서버 인스턴스 및 hello 파일은 저장소 계정을 지정 하는 업로드 된 toohello hello에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="09524-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="09524-301">실패 또는 성공 상태가 hello 내보내기 작업이 완료 되 면 hello 임시 파일이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-302">가져오기/내보내기는 프리미엄 계층 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="09524-303">자세한 내용 및 지침은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="09524-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="09524-304">Reboot</span></span>
<span data-ttu-id="09524-305">hello **재부팅** 블레이드 캐시 tooreboot hello 노드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="09524-306">이 다시 부팅 기능을 사용 하면 있습니다 tootest 복구를 위한 응용 프로그램 캐시 노드 오류가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="09524-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="09524-308">프리미엄 캐시 클러스터링을 사용 해야 하는 경우에 hello 캐시 tooreboot의 어떤 분할 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="09524-310">tooreboot 하나 이상의 노드 캐시의 hello 원하는 노드를 선택 하 고 클릭 **재부팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="09524-311">프리미엄 캐시 클러스터링을 사용 해야 하는 경우 hello 분할 tooreboot 선택한 다음 클릭 **재부팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="09524-312">몇 분 후 hello 선택한 노드 다시 부팅 하 고 몇 분 후 다시 온라인 상태로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09524-313">이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="09524-314">자세한 내용 및 지침은 [Azure Redis Cache 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="09524-315">모니터링</span><span class="sxs-lookup"><span data-stu-id="09524-315">Monitoring</span></span>

<span data-ttu-id="09524-316">hello **모니터링** tooconfigure 진단 및 Redis 캐시에 대 한 모니터링 섹션에서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="09524-317">Azure Redis 캐시 모니터링 및 진단에 대 한 자세한 내용은 참조 하십시오. [어떻게 toomonitor Azure Redis 캐시](cache-how-to-monitor.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![진단](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="09524-319">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="09524-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="09524-320">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="09524-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="09524-321">진단</span><span class="sxs-lookup"><span data-stu-id="09524-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="09524-322">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="09524-322">Redis metrics</span></span>
<span data-ttu-id="09524-323">클릭 **메트릭 Redis** 너무[메트릭을 볼](cache-how-to-monitor.md#view-cache-metrics) 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="09524-324">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="09524-324">Alert rules</span></span>

<span data-ttu-id="09524-325">클릭 **규칙 경고** tooconfigure 경고 Redis 캐시 메트릭을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="09524-326">자세한 내용은 [경고](cache-how-to-monitor.md#alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="09524-327">진단</span><span class="sxs-lookup"><span data-stu-id="09524-327">Diagnostics</span></span>

<span data-ttu-id="09524-328">기본적으로 Azure Monitor의 캐시 메트릭은 [30일 동안 저장](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)되었다가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="09524-329">toopersist 30 일 이상에 대 한 사용자 캐시 메트릭을 클릭 **진단** 너무[hello 저장소 계정 구성](cache-how-to-monitor.md#export-cache-metrics) toostore 캐시 진단을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="09524-330">추가 tooarchiving 프로그램 캐시 메트릭을 toostorage 수도 있습니다 [스트리밍할 tooan 이벤트 허브 또는 tooLog 분석 보내기](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="09524-331">설정 지원 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09524-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="09524-332">hello 설정을 hello **지원 + 문제 해결** 섹션 캐시 관련 문제 해결에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![설정 지원 + 문제 해결](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="09524-334">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="09524-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="09524-335">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="09524-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="09524-336">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="09524-336">Resource health</span></span>
<span data-ttu-id="09524-337">**리소스 상태** 기능은 리소스를 감시하고 예상대로 실행되는지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="09524-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="09524-338">Hello Azure 리소스 상태 관리 서비스에 대 한 자세한 내용은 참조 [Azure 리소스 상태 개요](../resource-health/resource-health-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="09524-339">리소스 상태를 현재 없습니다 tooreport 가상 네트워크에서 호스트 되는 Azure Redis 캐시 인스턴스의 hello 상태에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="09524-340">자세한 내용은 [VNET에서 캐시를 호스팅하는 경우 모든 캐시 기능이 작동하나요?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="09524-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="09524-341">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="09524-341">New support request</span></span>
<span data-ttu-id="09524-342">클릭 **새로운 지원 요청** tooopen 캐시에 대 한 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="09524-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="09524-343">기본 Redis 서버 구성</span><span class="sxs-lookup"><span data-stu-id="09524-343">Default Redis server configuration</span></span>
<span data-ttu-id="09524-344">새 Azure Redis Cache 인스턴스는 다음 기본 Redis 구성 값에는 hello로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="09524-345">이 섹션의 hello 설정을 hello를 사용 하 여 변경할 수 없습니다 `StackExchange.Redis.IServer.ConfigSet` 메서드.</span><span class="sxs-lookup"><span data-stu-id="09524-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="09524-346">이 메서드는이 섹션의 hello 명령 중 하나를 예외와 유사한 toohello 다음 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="09524-347">와 같은 구성할 수 있는 모든 값 **최대 메모리 정책**, hello Azure 포털 또는 Azure CLI 또는 PowerShell과 같은 명령줄 관리 도구를 통해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="09524-348">설정</span><span class="sxs-lookup"><span data-stu-id="09524-348">Setting</span></span> | <span data-ttu-id="09524-349">기본값</span><span class="sxs-lookup"><span data-stu-id="09524-349">Default value</span></span> | <span data-ttu-id="09524-350">설명</span><span class="sxs-lookup"><span data-stu-id="09524-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="09524-351">16</span><span class="sxs-lookup"><span data-stu-id="09524-351">16</span></span> |<span data-ttu-id="09524-352">데이터베이스의 hello 기본 수는 16 하지만 가격 책정 계층 다른 숫자에 따라 hello를 구성할 수 있습니다. <sup>1</sup> hello 기본 데이터베이스는 DB 0을 사용 하 여 각 연결 별로 다른 하나를 선택할 수 있습니다 `connection.GetDatabase(dbid)` 여기서 `dbid` 는 사이의 숫자 `0` 및 `databases - 1`합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="09524-353">Hello 가격 책정 계층에 따라 달라 집니다<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="09524-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="09524-354">이 hello 동일 hello에 허용 되는 연결 된 클라이언트의 최대 수 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="09524-355">Hello도 도달 하면 Redis가 닫습니다 모든 hello 새 연결이 'max number of clients reached' 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="09524-356">Redis 어떤 tooremove를 선택 하는 방법에 대 한 최대 메모리 정책은 hello 설정 때 `maxmemory` (hello 캐시 hello 캐시를 만들 때 선택한 기능 hello 크기)에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="09524-357">Azure Redis Cache hello 기본 설정은 `volatile-lru`, LRU 알고리즘을 사용 하 여 설정 하는 만료 된 hello 키를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="09524-358">이 설정은 hello Azure 포털에서에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="09524-359">자세한 내용은 [메모리 정책](#memory-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="09524-360">3</span><span class="sxs-lookup"><span data-stu-id="09524-360">3</span></span> |<span data-ttu-id="09524-361">toosave 메모리, LRU 및 최소 TTL 알고리즘은 정확한 알고리즘이 아니라 근사치로 계산 된 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="09524-362">기본적으로 Redis 검사 세 개의 키 및 선택 hello 하나 덜 최근에 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="09524-363">5, 000</span><span class="sxs-lookup"><span data-stu-id="09524-363">5,000</span></span> |<span data-ttu-id="09524-364">밀리초 단위의 Lua 스크립트 최대 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="09524-365">Hello 최대 실행 시간에 도달 하면 Redis는 스크립트가 허용 된 시간, 최대 hello 후 실행 중인 이며 tooreply tooqueries 오류가 발생 하 여 시작을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="09524-366">500</span><span class="sxs-lookup"><span data-stu-id="09524-366">500</span></span> |<span data-ttu-id="09524-367">스크립트 이벤트 큐의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="09524-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="09524-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="09524-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="09524-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="09524-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="09524-370">hello 클라이언트 출력 버퍼 제한을 사용 될 수 있습니다 (일반적인 이유는 Pub/Sub 클라이언트 메시지를 hello 게시자에서 생성 하는 것에 가능한 한 빨리 사용할 수 없습니다) 몇 가지 이유로 적당히 빠르게 hello 서버에서 데이터를 읽고 있지 않은 클라이언트의 tooforce 연결 해제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="09524-371">자세한 내용은 [http://redis.io/topics/clients](http://redis.io/topics/clients)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="09524-372"><a name="databases"></a>
<sup>1</sup>hello 제한을 `databases` 각 Azure Redis Cache 가격 책정 계층에 대 한 다른 하며 캐시를 만들 때 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="09524-373">되지 않은 경우 `databases` 설정이 지정 캐시 만들기 중 hello 기본값은 16입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="09524-374">기본 및 표준 캐시</span><span class="sxs-lookup"><span data-stu-id="09524-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="09524-375">C0 (250MB) 캐시-too16 데이터베이스를</span><span class="sxs-lookup"><span data-stu-id="09524-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="09524-376">C1 too16 데이터베이스를 캐시-(1GB)</span><span class="sxs-lookup"><span data-stu-id="09524-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="09524-377">C2 too16 데이터베이스를 캐시-(2.5 g B)</span><span class="sxs-lookup"><span data-stu-id="09524-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="09524-378">C3 too16 데이터베이스를 캐시-(6 GB)</span><span class="sxs-lookup"><span data-stu-id="09524-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="09524-379">C4 too32 데이터베이스를 캐시-(13 GB)</span><span class="sxs-lookup"><span data-stu-id="09524-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="09524-380">C5 (26GB) 캐시-too48 데이터베이스를</span><span class="sxs-lookup"><span data-stu-id="09524-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="09524-381">C6 too64 데이터베이스를 캐시-(53 GB)</span><span class="sxs-lookup"><span data-stu-id="09524-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="09524-382">프리미엄 캐시</span><span class="sxs-lookup"><span data-stu-id="09524-382">Premium caches</span></span>
  * <span data-ttu-id="09524-383">P1 (6GB-60 GB)-too16 데이터베이스를</span><span class="sxs-lookup"><span data-stu-id="09524-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="09524-384">P2 (13 GB-130 GB)-too32 데이터베이스를</span><span class="sxs-lookup"><span data-stu-id="09524-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="09524-385">Too48 데이터베이스를 P3 (26GB-260 GB)-</span><span class="sxs-lookup"><span data-stu-id="09524-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="09524-386">Too64 데이터베이스를 P4 (53GB-530 GB)-</span><span class="sxs-lookup"><span data-stu-id="09524-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="09524-387">Redis 클러스터 사용-와 모든 프리미엄 캐시 Redis 클러스터만 지원 0 데이터베이스의 사용 하므로 hello `databases` Redis 클러스터를 사용할 수 있는 모든 프리미엄 캐시는 효과적으로 1과 hello에 대 한 한계 [선택](http://redis.io/commands/select) 명령을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="09524-388">자세한 내용은 참조 [필요 합니까 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="09524-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="09524-389">데이터베이스에 대한 자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="09524-390">hello `databases` 캐시 만들기 중에 구성 하 고 PowerShell, CLI 또는 기타 관리 클라이언트를 사용 하 여만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="09524-391">PowerShell을 사용하여 캐시를 만드는 동안 `databases` 를 구성하는 예제는 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="09524-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients`는 Azure Redis Cache 가격 책정 계층마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="09524-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="09524-393">기본 및 표준 캐시</span><span class="sxs-lookup"><span data-stu-id="09524-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="09524-394">C0 (250MB) 캐시-too256 연결을</span><span class="sxs-lookup"><span data-stu-id="09524-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="09524-395">C1 too1 (1GB) 캐시-, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="09524-396">C2-too2 (2.5 g B) 캐시, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="09524-397">C3 too5 (6GB) 캐시-, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="09524-398">C4 too10 13 4GB 캐시-, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="09524-399">C 5-too15 (26GB) 캐시, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="09524-400">C 6-too20 (53GB) 캐시, 000 연결</span><span class="sxs-lookup"><span data-stu-id="09524-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="09524-401">프리미엄 캐시</span><span class="sxs-lookup"><span data-stu-id="09524-401">Premium caches</span></span>
  * <span data-ttu-id="09524-402">Too7, 500 개의 연결을 P1 (6GB-60 GB)-</span><span class="sxs-lookup"><span data-stu-id="09524-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="09524-403">P2 (13 GB-130 GB)-too15, 000 연결 구성</span><span class="sxs-lookup"><span data-stu-id="09524-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="09524-404">Too30, 000 연결 구성 (26GB-260 GB)-P3</span><span class="sxs-lookup"><span data-stu-id="09524-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="09524-405">Too40, 000 연결을 P4 (53GB-530 GB)-</span><span class="sxs-lookup"><span data-stu-id="09524-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="09524-406">각 캐시 크기를 허용 하지만 *최대* 연결의 특정 수, 각 연결 tooRedis 오버 헤드가 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="09524-407">이러한 오버헤드의 예로 TLS/SSL 암호화의 결과인 CPU 및 메모리 사용량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="09524-408">특정된 캐시 크기에 대 한 최대 연결 제한 hello 부하가 적은 캐시를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="09524-409">하는 경우 연결 오버 헤드가에서 로드할 *플러스* hello 시스템에 대 한 용량을 초과 하는 클라이언트 작업에서의 로드, hello 현재 캐시 크기에 대 한 hello 연결 제한을 초과한 경우에 hello 캐시 용량 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="09524-410">Azure Redis Cache에서 지원되지 않는 Redis 명령</span><span class="sxs-lookup"><span data-stu-id="09524-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="09524-411">구성 및 관리 Azure Redis 캐시 인스턴스의 Microsoft에서 관리 하므로 hello 다음 명령은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="09524-412">Tooinvoke 시도 하면 너무 유사한 오류 메시지가 나타납니다에`"(error) ERR unknown command"`합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="09524-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="09524-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="09524-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="09524-414">BGSAVE</span></span>
> * <span data-ttu-id="09524-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="09524-415">CONFIG</span></span>
> * <span data-ttu-id="09524-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="09524-416">DEBUG</span></span>
> * <span data-ttu-id="09524-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="09524-417">MIGRATE</span></span>
> * <span data-ttu-id="09524-418">저장</span><span class="sxs-lookup"><span data-stu-id="09524-418">SAVE</span></span>
> * <span data-ttu-id="09524-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="09524-419">SHUTDOWN</span></span>
> * <span data-ttu-id="09524-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="09524-420">SLAVEOF</span></span>
> * <span data-ttu-id="09524-421">클러스터 - 클러스트 쓰기 명령은 비활성화되지만, 읽기 전용 클러스터 명령은 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="09524-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="09524-422">Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="09524-423">Redis 콘솔</span><span class="sxs-lookup"><span data-stu-id="09524-423">Redis console</span></span>
<span data-ttu-id="09524-424">안전 하 게 명령을 실행할 수 있습니다 hello를 사용 하 여 tooyour Azure Redis Cache 인스턴스 **Redis 콘솔**, hello 모든 캐시 계층에 대해 Azure 포털에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="09524-425">hello Redis 콘솔에서 작동 하지 않습니다 [VNET](cache-how-to-premium-vnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="09524-426">캐시는 VNET의 일부 이면 hello 캐시 hello VNET에서에서 클라이언트에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="09524-427">Redis 콘솔을 벗어난 hello VNET 로컬 브라우저에서 실행 되므로 tooyour 캐시를 연결할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="09524-428">일부 Redis 명령은 Azure Redis Cache에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="09524-429">Azure Redis Cache에 사용 되지 않는 Redis 명령 목록이 이전 hello 참조 [Azure Redis Cache에서 지원 되지 않는 명령 Redis](#redis-commands-not-supported-in-azure-redis-cache) 섹션.</span><span class="sxs-lookup"><span data-stu-id="09524-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="09524-430">Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="09524-431">tooaccess hello Redis 콘솔 클릭 **콘솔** hello에서 **Redis Cache** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="09524-433">캐시 인스턴스에 대해 tooissue 명령을 단순히 형식 hello 명령 hello 콘솔에 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="09524-435">premium Redis 콘솔 hello를 사용 하 여 캐시 클러스터</span><span class="sxs-lookup"><span data-stu-id="09524-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="09524-436">캐시 클러스터는 premium hello Redis 콘솔을 사용 하 여 명령을 tooa 단일 분할 영역 hello 캐시의 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09524-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="09524-437">먼저 tooissue 명령 tooa 특정 분할 hello 분할 선택에서 클릭 하 여 toohello 원하는 분할 영역을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="09524-439">Tooaccess 연결 된 분할 hello 보다 다른 분할 영역에 저장 된 키를 만들려고 하면 메시지의 뒤에 오류 메시지와 비슷한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="09524-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="09524-440">Hello 이전 예제에서는 분할 영역 1 hello 선택한 분할 영역에는 있지만 `myKey` hello에 표시 된 대로 0, 분할 된 데이터베이스에 있는 `(shard 0)` hello 오류 메시지의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="09524-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="09524-441">이 예제에서는 tooaccess `myKey`선택 합니다 shard 코드 조각 선택기 및 문제 원하는 hello 명령 hello 0 분할 된 데이터베이스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="09524-442">캐시 tooa 새 구독 이동</span><span class="sxs-lookup"><span data-stu-id="09524-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="09524-443">클릭 하 여 캐시 tooa 새 구독을 이동할 수 있습니다 **이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Redis Cache 이동](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="09524-445">하나의 리소스 그룹 tooanother 및 구독을 하나 tooanother에서 리소스를 이동 하는 방법은 참조 하십시오. [리소스 toonew 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09524-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09524-446">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09524-446">Next steps</span></span>
* <span data-ttu-id="09524-447">Redis 명령을 사용하는 방법은 [어떻게 Redis 명령을 실행할 수 있나요?](cache-faq.md#how-can-i-run-redis-commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09524-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

