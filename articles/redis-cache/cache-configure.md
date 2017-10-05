---
title: "Azure Redis 캐시를 구성하는 방법 | Microsoft Docs"
description: "Azure Redis 캐시에 대한 기본 Redis 구성을 이해하고 Azure Redis 캐시 인스턴스를 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="cbc6d-103">Azure Redis 캐시 구성 방법</span><span class="sxs-lookup"><span data-stu-id="cbc6d-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="cbc6d-104">이 항목에서는 Azure Redis Cache 인스턴스에 대한 구성을 검토하고 업데이트하는 방법과 Azure Redis Cache 인스턴스에 대한 기본 Redis 서버 구성을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-105">프리미엄 캐시 기능을 구성하고 사용하는 방법에 대한 자세한 내용은 [지속성을 구성하는 방법](cache-how-to-premium-persistence.md), [클러스터링을 구성하는 방법](cache-how-to-premium-clustering.md) 및 [Virtual Network 지원을 구성하는 방법](cache-how-to-premium-vnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="cbc6d-106">Redis 캐시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="cbc6d-107">Azure Redis Cache 설정은 **리소스 메뉴**를 사용하여 **Redis Cache** 블레이드에서 살펴보고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Redis 캐시 설정](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="cbc6d-109">**리소스 메뉴**를 사용하여 다음 설정을 살펴보고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="cbc6d-110">개요</span><span class="sxs-lookup"><span data-stu-id="cbc6d-110">Overview</span></span>](#overview)
* [<span data-ttu-id="cbc6d-111">활동 로그</span><span class="sxs-lookup"><span data-stu-id="cbc6d-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="cbc6d-112">액세스 제어(IAM)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="cbc6d-113">태그</span><span class="sxs-lookup"><span data-stu-id="cbc6d-113">Tags</span></span>](#tags)
* [<span data-ttu-id="cbc6d-114">문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="cbc6d-115">설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="cbc6d-116">액세스 키</span><span class="sxs-lookup"><span data-stu-id="cbc6d-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="cbc6d-117">고급 설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="cbc6d-118">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="cbc6d-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="cbc6d-119">규모</span><span class="sxs-lookup"><span data-stu-id="cbc6d-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="cbc6d-120">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="cbc6d-121">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="cbc6d-122">업데이트 예약</span><span class="sxs-lookup"><span data-stu-id="cbc6d-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="cbc6d-123">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="cbc6d-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="cbc6d-124">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cbc6d-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="cbc6d-125">방화벽</span><span class="sxs-lookup"><span data-stu-id="cbc6d-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="cbc6d-126">속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="cbc6d-127">잠금</span><span class="sxs-lookup"><span data-stu-id="cbc6d-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="cbc6d-128">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="cbc6d-129">관리</span><span class="sxs-lookup"><span data-stu-id="cbc6d-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="cbc6d-130">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="cbc6d-131">데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="cbc6d-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="cbc6d-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="cbc6d-133">모니터링</span><span class="sxs-lookup"><span data-stu-id="cbc6d-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="cbc6d-134">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="cbc6d-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="cbc6d-135">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="cbc6d-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="cbc6d-136">진단</span><span class="sxs-lookup"><span data-stu-id="cbc6d-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="cbc6d-137">설정 지원 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="cbc6d-138">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="cbc6d-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="cbc6d-139">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="cbc6d-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="cbc6d-140">개요</span><span class="sxs-lookup"><span data-stu-id="cbc6d-140">Overview</span></span>

<span data-ttu-id="cbc6d-141">**개요**에서는 이름, 포트, 가격 책정 계층 및 선택한 캐시 메트릭과 같은 캐시에 대한 기본 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="cbc6d-142">활동 로그</span><span class="sxs-lookup"><span data-stu-id="cbc6d-142">Activity log</span></span>

<span data-ttu-id="cbc6d-143">캐시에 대해 수행된 작업을 보려면 **활동 로그** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="cbc6d-144">또한 다른 리소스를 포함하도록 이 뷰를 확장하려면 필터링을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="cbc6d-145">감사 로그 작업에 대한 자세한 내용은 [Resource Manager를 사용하는 감사 작업](../azure-resource-manager/resource-group-audit.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="cbc6d-146">Azure Redis Cache 이벤트 모니터링에 대한 자세한 내용은 [작업 및 경고](cache-how-to-monitor.md#operations-and-alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="cbc6d-147">액세스 제어(IAM)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-147">Access control (IAM)</span></span>

<span data-ttu-id="cbc6d-148">조직이 액세스 관리에 필요한 요구 사항을 간단하면서도 정밀하게 충족할 수 있도록 Azure Portal의 **액세스 제어(IAM)** 섹션에서 RBAC(역할 기반 액세스 제어)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="cbc6d-149">자세한 내용은 [Azure 포털의 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="cbc6d-150">태그들</span><span class="sxs-lookup"><span data-stu-id="cbc6d-150">Tags</span></span>

<span data-ttu-id="cbc6d-151">**태그** 섹션은 리소스 구성에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="cbc6d-152">자세한 내용은 [태그를 사용하여 Azure 리소스 구성](../azure-resource-manager/resource-group-using-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="cbc6d-153">문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-153">Diagnose and solve problems</span></span>

<span data-ttu-id="cbc6d-154">일반적인 문제 및 이러한 문제를 해결하기 위한 전략을 확인하려면 **문제 진단 및 해결** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="cbc6d-155">설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-155">Settings</span></span>
<span data-ttu-id="cbc6d-156">**설정** 섹션을 사용하여 캐시에 대한 다음 설정에 액세스하고 해당 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="cbc6d-157">액세스 키</span><span class="sxs-lookup"><span data-stu-id="cbc6d-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="cbc6d-158">고급 설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="cbc6d-159">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="cbc6d-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="cbc6d-160">규모</span><span class="sxs-lookup"><span data-stu-id="cbc6d-160">Scale</span></span>](#scale)
* [<span data-ttu-id="cbc6d-161">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="cbc6d-162">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="cbc6d-163">업데이트 예약</span><span class="sxs-lookup"><span data-stu-id="cbc6d-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="cbc6d-164">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="cbc6d-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="cbc6d-165">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cbc6d-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="cbc6d-166">방화벽</span><span class="sxs-lookup"><span data-stu-id="cbc6d-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="cbc6d-167">속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-167">Properties</span></span>](#properties)
* [<span data-ttu-id="cbc6d-168">잠금</span><span class="sxs-lookup"><span data-stu-id="cbc6d-168">Locks</span></span>](#locks)
* [<span data-ttu-id="cbc6d-169">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="cbc6d-170">액세스 키</span><span class="sxs-lookup"><span data-stu-id="cbc6d-170">Access keys</span></span>
<span data-ttu-id="cbc6d-171">**선택키** 를 클릭하여 캐시에 대한 선택키를 보거나 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="cbc6d-172">이러한 키는 캐시에 연결하는 클라이언트에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-172">These keys are used by the clients connecting to your cache.</span></span>

![Redis 캐시 액세스 키](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="cbc6d-174">고급 설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-174">Advanced settings</span></span>
<span data-ttu-id="cbc6d-175">다음 설정은 **고급 설정** 블레이드에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="cbc6d-176">액세스 포트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="cbc6d-177">메모리 정책</span><span class="sxs-lookup"><span data-stu-id="cbc6d-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="cbc6d-178">Keyspace 알림(고급 설정)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="cbc6d-179">액세스 포트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-179">Access Ports</span></span>
<span data-ttu-id="cbc6d-180">비 SSL 액세스는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="cbc6d-181">비 SSL 포트를 사용하도록 설정하려면 **고급 설정 블레이드**의 **SSL을 통해서만 액세스 허용**에서 **아니요**를 클릭한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Redis 캐시 액세스 포트](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="cbc6d-183">메모리 정책</span><span class="sxs-lookup"><span data-stu-id="cbc6d-183">Memory policies</span></span>
<span data-ttu-id="cbc6d-184">**고급 설정** 블레이드의 **Maxmemory 정책**, **maxmemory-reserved** 및 **maxfragmentationmemory-reserved** 설정은 캐시에 대한 메모리 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Redis 캐시 Maxmemory 정책](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="cbc6d-186">**Maxmemory 정책**은 캐시에 대한 제거 정책을 구성하고, 다음 제거 정책 중에서 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="cbc6d-187">`volatile-lru` - 이것이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="cbc6d-188">`maxmemory` 정책에 대한 자세한 내용은 [제거 정책](http://redis.io/topics/lru-cache#eviction-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="cbc6d-189">**maxmemory-reserved** 설정은 장애 조치(failover) 중 복제와 같은 비캐시 작업을 위해 예약되는 메모리의 양을 MB 단위로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="cbc6d-190">이 값을 설정하면 부하가 달라져도 Redis 서버 환경이 더 일관되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="cbc6d-191">이 값은 쓰기 작업이 많은 워크로드에서 더 높게 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="cbc6d-192">이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="cbc6d-193">**maxfragmentationmemory-reserved** 설정은 메모리 조각화를 고려하여 예약된 메모리 양을 MB 단위로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="cbc6d-194">이 값을 설정하면 캐시가 가득 찼거나 거의 가득 찼고 조각화 비율이 높을 때 더욱 일관된 Redis 서버 환경을 갖출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="cbc6d-195">이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="cbc6d-196">새 메모리 예약 값(**maxmemory-reserved** 또는 **maxfragmentationmemory-reserved**)을 선택할 때 고려해야 할 사항 중 하나는 이러한 변경이 이미 많은 양의 데이터로 실행 중인 캐시에 미칠 수 있는 영향력입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="cbc6d-197">예를 들어 49GB의 데이터가 있는 53GB 캐시가 있는 경우 예약 값을 8GB로 변경하면 시스템에 사용 가능한 최대 메모리가 45GB로 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="cbc6d-198">현재 `used_memory` 또는 `used_memory_rss` 값이 새 제한인 45GB보다 높으면 시스템에서 `used_memory`과 `used_memory_rss` 모두가 45GB 미만이 될 때까지 데이터를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="cbc6d-199">제거는 서버 부하 및 메모리 조각화를 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="cbc6d-200">`used_memory` 및 `used_memory_rss`와 같은 캐시 메트릭에 대한 자세한 내용은 [사용 가능한 메트릭 및 보고 간격](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-201">**maxmemory-reserved** 및 **maxfragmentationmemory-reserved** 설정은 Standard 및 Premium 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="cbc6d-202">Keyspace 알림(고급 설정)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="cbc6d-203">Redis keyspace 알림은 **고급 설정** 블레이드에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="cbc6d-204">Keyspace 알림을 사용하면 특정 이벤트가 발생할 때 클라이언트에서 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Redis 캐시 고급 설정](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-206">Keyspace 알림과 **notify-keyspace-events** 설정은 표준 및 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="cbc6d-207">자세한 내용은 [Redis Keyspace 알림](http://redis.io/topics/notifications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="cbc6d-208">샘플 코드는 [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플의 [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="cbc6d-209">Redis 캐시 관리자</span><span class="sxs-lookup"><span data-stu-id="cbc6d-209">Redis Cache Advisor</span></span>
<span data-ttu-id="cbc6d-210">**Redis 캐시 관리자** 블레이드에 캐시에 대한 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="cbc6d-211">정상적으로 작동하는 중에는 추천이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-211">During normal operations, no recommendations are displayed.</span></span> 

![추천](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="cbc6d-213">캐시 작업 중에 높은 메모리 사용량, 높은 네트워크 대역폭, 높은 서버 부하 등의 조건이 발생하면 **Redis Cache** 블레이드에 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![추천](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="cbc6d-215">자세한 내용은 **추천** 블레이드에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-215">Further information can be found on the **Recommendations** blade.</span></span>

![추천](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="cbc6d-217">**Redis Cache** 블레이드의 [모니터링 차트](cache-how-to-monitor.md#monitoring-charts) 및 [사용 현황 차트](cache-how-to-monitor.md#usage-charts) 섹션에서 이러한 메트릭을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="cbc6d-218">가격 책정 계층마다 클라이언트 연결, 메모리 및 대역폭에 대한 제한이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="cbc6d-219">캐시가 오랫동안 이러한 메트릭의 최대 용량에 근접하면 추천이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="cbc6d-220">**추천** 도구에서 검토하는 메트릭 및 제한에 대한 자세한 내용은 다음 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="cbc6d-221">Redis Cache 메트릭</span><span class="sxs-lookup"><span data-stu-id="cbc6d-221">Redis Cache metric</span></span> | <span data-ttu-id="cbc6d-222">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="cbc6d-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="cbc6d-223">네트워크 대역폭 사용량</span><span class="sxs-lookup"><span data-stu-id="cbc6d-223">Network bandwidth usage</span></span> |[<span data-ttu-id="cbc6d-224">캐시 성능 - 사용 가능한 대역폭</span><span class="sxs-lookup"><span data-stu-id="cbc6d-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="cbc6d-225">연결된 클라이언트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-225">Connected clients</span></span> |[<span data-ttu-id="cbc6d-226">기본 Redis 서버 구성 - maxclients</span><span class="sxs-lookup"><span data-stu-id="cbc6d-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="cbc6d-227">서버 부하</span><span class="sxs-lookup"><span data-stu-id="cbc6d-227">Server load</span></span> |[<span data-ttu-id="cbc6d-228">사용 현황 차트 - Redis 서버 부하</span><span class="sxs-lookup"><span data-stu-id="cbc6d-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="cbc6d-229">메모리 사용량</span><span class="sxs-lookup"><span data-stu-id="cbc6d-229">Memory usage</span></span> |[<span data-ttu-id="cbc6d-230">캐시 성능 - 크기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="cbc6d-231">캐시를 업그레이드하려면 **지금 업그레이드**를 클릭하여 [가격 책정 계층](#scale)을 변경하고 캐시 크기를 조정하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="cbc6d-232">가격 책정 계층 선택에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="cbc6d-233">확장</span><span class="sxs-lookup"><span data-stu-id="cbc6d-233">Scale</span></span>
<span data-ttu-id="cbc6d-234">**확장**을 클릭하여 캐시에 대한 가격 책정 계층을 보거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="cbc6d-235">크기 조정에 대한 자세한 내용은 [Azure Redis Cache 크기를 조정하는 방법](cache-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis Cache 가격 책정 계층](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="cbc6d-237">Redis 클러스터 크기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-237">Redis Cluster Size</span></span>
<span data-ttu-id="cbc6d-238">**(미리 보기) Redis 클러스터 크기** 를 클릭하여 클러스터링을 사용하도록 설정되어 있는 실행 중인 프리미엄 캐시에 대한 클러스터 크기를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-239">Azure Redis Cache 프리미엄 계층은 일반 공급으로 출시된 반면 Redis 클러스터 크기 기능은 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 클러스터 크기](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="cbc6d-241">클러스터 크기를 변경하려면 슬라이더를 사용하거나 **분할된 데이터베이스 수** 텍스트 상자에 1에서 10 사이의 수를 입력하고 **확인**을 클릭하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-242">Redis 클러스터링은 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="cbc6d-243">자세한 내용은 [프리미엄 Azure Redis Cache에 클러스터링을 구성하는 방법](cache-how-to-premium-clustering.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="cbc6d-244">Redis 데이터 지속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-244">Redis data persistence</span></span>
<span data-ttu-id="cbc6d-245">**Redis 데이터 지속성** 을 클릭하여 프리미엄 캐시에 대해 데이터 지속성 구성 및 사용 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="cbc6d-246">Azure Redis Cache는 [RDB 지속성](cache-how-to-premium-persistence.md#configure-rdb-persistence) 또는 [AOF 지속성](cache-how-to-premium-persistence.md#configure-aof-persistence)을 사용하여 Redis 지속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="cbc6d-247">자세한 내용은 [프리미엄 Azure Redis Cache에 지속성을 구성하는 방법](cache-how-to-premium-persistence.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="cbc6d-248">Redis 데이터 지속성은 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="cbc6d-249">업데이트를 예약</span><span class="sxs-lookup"><span data-stu-id="cbc6d-249">Schedule updates</span></span>
<span data-ttu-id="cbc6d-250">**업데이트 예약** 블레이드에서는 캐시의 Redis 서버 업데이트에 대한 유지 관리 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-251">유지 관리 기간은 Redis 서버 업데이트에만 적용되며 Azure 업데이트나 캐시를 호스트하는 VM의 운영 체제에 대한 업데이트에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![업데이트 예약](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="cbc6d-253">유지 관리 기간을 지정하려면 원하는 요일을 선택하고 각 요일의 유지 관리 기간 시작 시간을 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="cbc6d-254">유지 관리 기간 시간은 UTC로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-255">**업데이트 예약** 기능은 프리미엄 계층 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="cbc6d-256">자세한 내용 및 지침은 [Azure Redis Cache 관리 - 업데이트 예약](cache-administration.md#schedule-updates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="cbc6d-257">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="cbc6d-257">Geo-replication</span></span>

<span data-ttu-id="cbc6d-258">**지역에서 복제** 블레이드에서는 두 개의 프리미엄 계층 Azure Redis Cache 인스턴스를 연결하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="cbc6d-259">한 캐시는 주 연결된 캐시로 지정하고 다른 캐시는 보조 연결된 캐시로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="cbc6d-260">보조 연결된 캐시는 읽기 전용이 되고 주 캐시에 쓴 데이터는 보조 연결된 캐시에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="cbc6d-261">이 기능은 Azure 지역 간에 캐시를 복제하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-262">**지역에서 복제**는 프리미엄 계층 캐시에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="cbc6d-263">자세한 내용 및 지침은 [Azure Redis Cache에 대해 지역에서 복제를 구성하는 방법](cache-how-to-geo-replication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="cbc6d-264">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="cbc6d-264">Virtual Network</span></span>
<span data-ttu-id="cbc6d-265">**Virtual Network** 섹션에서 캐시의 가상 네트워크 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="cbc6d-266">VNET 지원을 통해 프리미엄 캐시를 만들고 설정을 업데이트하는 방법에 대한 자세한 내용은 [프리미엄 Azure Redis Cache에 가상 네트워크 지원을 구성하는 방법](cache-how-to-premium-vnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-267">가상 네트워크 설정은 캐시를 만드는 동안 VNET 지원을 통해 구성된 프리미엄 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="cbc6d-268">방화벽</span><span class="sxs-lookup"><span data-stu-id="cbc6d-268">Firewall</span></span>

<span data-ttu-id="cbc6d-269">**방화벽**을 클릭하여 프리미엄 Azure Redis Cache에 대한 방화벽 규칙을 보고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![방화벽](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="cbc6d-271">시작 및 끝 IP 주소 범위를 사용하여 방화벽 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="cbc6d-272">방화벽 규칙이 구성되면 지정된 IP 주소 범위의 클라이언트 연결만 캐시에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="cbc6d-273">방화벽 규칙이 저장되면 잠시 지연되었다가 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="cbc6d-274">이러한 지연 시간은 일반적으로 1분 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-275">방화벽 규칙이 구성된 경우에도 Azure Redis Cache 모니터링 시스템에서의 연결은 항상 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="cbc6d-276">방화벽 규칙은 프리미엄 계층 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="cbc6d-277">속성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-277">Properties</span></span>
<span data-ttu-id="cbc6d-278">**속성** 을 클릭하여 캐시 끝점 및 포트를 포함하여 캐시에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Redis 캐시 속성](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="cbc6d-280">잠금</span><span class="sxs-lookup"><span data-stu-id="cbc6d-280">Locks</span></span>
<span data-ttu-id="cbc6d-281">**잠금** 섹션에서는 구독, 리소스 그룹 또는 리소스에 잠금을 설정하여 조직의 다른 사용자가 실수로 중요한 리소스를 삭제 또는 수정하지 못하게 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="cbc6d-282">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="cbc6d-283">자동화 스크립트</span><span class="sxs-lookup"><span data-stu-id="cbc6d-283">Automation script</span></span>

<span data-ttu-id="cbc6d-284">미래 배포를 위해 배포된 리소스의 템플릿을 빌드하고 내보내려면 **자동화 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="cbc6d-285">템플릿 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="cbc6d-286">관리 설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-286">Administration settings</span></span>
<span data-ttu-id="cbc6d-287">**관리** 섹션의 설정을 사용하여 캐시에 대해 다음과 같은 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![관리](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="cbc6d-289">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="cbc6d-290">데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="cbc6d-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="cbc6d-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="cbc6d-292">가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-292">Import/Export</span></span>
<span data-ttu-id="cbc6d-293">Import/Export는 Azure Redis Cache 데이터 관리 작업으로 프리미엄 캐시에서 Azure Storage 계정의 페이지 Blob으로 Redis Cache 데이터베이스(RDB) 스냅숏을 가져오고 내보냄으로써 캐시에서 데이터를 가져오고 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="cbc6d-294">가져오기/내보내기를 통해 다양한 Azure Redis Cache 인스턴스 간에 마이그레이션이 가능하고, 데이터를 사용하기 전에 캐시에 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="cbc6d-295">가져오기는 Linux, Windows 또는 Amazon Web Services 및 기타 클라우드 공급자에서 실행되는 Redis를 비롯한 환경이나 클라우드에서 실행되는 Redis 서버로부터 Redis 호환 RDB 파일을 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="cbc6d-296">데이터 가져오기는 미리 채워진 데이터로 캐시를 만드는 손쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="cbc6d-297">가져오기 프로세스를 진행하는 동안, Azure Redis Cache는 Azure Storage에서 메모리로 RDB 파일을 로드한 다음 키를 캐시에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="cbc6d-298">내보내기를 통해 Azure Redis Cache에 저장된 데이터를 Redis 호환 RDB 파일로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="cbc6d-299">이 기능을 사용하면 Azure Redis Cache 인스턴스에서 다른 인스턴스나 다른 Redis 서버로 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="cbc6d-300">내보내기 프로세스를 진행하는 동안, Azure Redis Cache 서버 인스턴스를 호스트하는 VM에 임시 파일이 생성되고, 지정된 저장소 계정에 그 파일이 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="cbc6d-301">성공 또는 실패 상태로 내보내기 작업이 완료되면, 임시 파일은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-302">가져오기/내보내기는 프리미엄 계층 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="cbc6d-303">자세한 내용 및 지침은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="cbc6d-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="cbc6d-304">Reboot</span></span>
<span data-ttu-id="cbc6d-305">**다시 부팅** 블레이드에서는 캐시 노드를 다시 부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="cbc6d-306">이 다시 부팅 기능을 사용하면 캐시 노드에 오류가 발생하는 경우 응용 프로그램의 복원력을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="cbc6d-308">클러스터링이 설정된 프리미엄 캐시를 사용하는 경우 재부팅할 캐시 분할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="cbc6d-310">하나 이상의 캐시 노드를 다시 부팅하려면 원하는 노드를 선택하고 **다시 부팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="cbc6d-311">클러스터링이 설정된 프리미엄 캐시를 사용하는 경우 다시 부팅할 분할을 선택하고 **다시 부팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="cbc6d-312">몇 분 후 선택된 노드가 재부팅되고, 다시 몇 분 후에 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6d-313">이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="cbc6d-314">자세한 내용 및 지침은 [Azure Redis Cache 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="cbc6d-315">모니터링</span><span class="sxs-lookup"><span data-stu-id="cbc6d-315">Monitoring</span></span>

<span data-ttu-id="cbc6d-316">**모니터링** 섹션에서 Redis 캐시의 진단 및 모니터링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="cbc6d-317">Azure Redis Cache 모니터링 및 진단에 대한 자세한 내용은 [Azure Redis Cache를 모니터링하는 방법](cache-how-to-monitor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![진단](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="cbc6d-319">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="cbc6d-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="cbc6d-320">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="cbc6d-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="cbc6d-321">진단</span><span class="sxs-lookup"><span data-stu-id="cbc6d-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="cbc6d-322">Redis 메트릭</span><span class="sxs-lookup"><span data-stu-id="cbc6d-322">Redis metrics</span></span>
<span data-ttu-id="cbc6d-323">캐시에 대한 [메트릭을 보려면](cache-how-to-monitor.md#view-cache-metrics) **Redis 메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="cbc6d-324">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="cbc6d-324">Alert rules</span></span>

<span data-ttu-id="cbc6d-325">**경고 규칙**을 클릭하여 Redis Cache 메트릭을 기반으로 경고를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="cbc6d-326">자세한 내용은 [경고](cache-how-to-monitor.md#alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="cbc6d-327">진단</span><span class="sxs-lookup"><span data-stu-id="cbc6d-327">Diagnostics</span></span>

<span data-ttu-id="cbc6d-328">기본적으로 Azure Monitor의 캐시 메트릭은 [30일 동안 저장](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)되었다가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="cbc6d-329">30일 이후에도 캐시 메트릭을 유지하려면 **진단**을 클릭하여 캐시 진단을 저장하는 데 사용되는 [저장소 계정을 구성](cache-how-to-monitor.md#export-cache-metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="cbc6d-330">캐시 메트릭을 저장소에 보관할 뿐만 아니라 [파일을 이벤트 허브에 스트리밍하거나 Log Analytics로 보낼 수](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="cbc6d-331">설정 지원 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="cbc6d-332">**설정 지원 + 문제 해결** 섹션의 설정은 캐시로 문제를 해결하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![설정 지원 + 문제 해결](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="cbc6d-334">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="cbc6d-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="cbc6d-335">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="cbc6d-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="cbc6d-336">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="cbc6d-336">Resource health</span></span>
<span data-ttu-id="cbc6d-337">**리소스 상태** 기능은 리소스를 감시하고 예상대로 실행되는지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="cbc6d-338">Azure 리소스 상태 관리 서비스에 대한 자세한 내용은 [Azure 리소스 상태 개요](../resource-health/resource-health-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-339">현재 리소스 상태는 가상 네트워크에서 호스팅되는 Azure Redis Cache 인스턴스의 상태를 보고할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="cbc6d-340">자세한 내용은 [VNET에서 캐시를 호스팅하는 경우 모든 캐시 기능이 작동하나요?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="cbc6d-341">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="cbc6d-341">New support request</span></span>
<span data-ttu-id="cbc6d-342">캐시에 대한 지원 요청을 열려면 **새 지원 요청** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="cbc6d-343">기본 Redis 서버 구성</span><span class="sxs-lookup"><span data-stu-id="cbc6d-343">Default Redis server configuration</span></span>
<span data-ttu-id="cbc6d-344">새 Azure Redis 캐시 인스턴스는 다음과 같은 기본 Redis 구성 값으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-345">이 섹션의 설정은 `StackExchange.Redis.IServer.ConfigSet` 메서드를 사용하여 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="cbc6d-346">이 메서드를 이 섹션의 명령 중 하나와 함께 호출하면 다음과 유사한 예외가 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="cbc6d-347">**max-memory-policy**와 같이 구성 가능한 모든 값은 Azure Portal 또는 명령줄 관리 도구(예: Azure CLI 또는 PowerShell)를 통해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="cbc6d-348">설정</span><span class="sxs-lookup"><span data-stu-id="cbc6d-348">Setting</span></span> | <span data-ttu-id="cbc6d-349">기본값</span><span class="sxs-lookup"><span data-stu-id="cbc6d-349">Default value</span></span> | <span data-ttu-id="cbc6d-350">설명</span><span class="sxs-lookup"><span data-stu-id="cbc6d-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="cbc6d-351">16</span><span class="sxs-lookup"><span data-stu-id="cbc6d-351">16</span></span> |<span data-ttu-id="cbc6d-352">데이터베이스의 기본 수는 16이지만 가격 책정 계층에 따라 다른 숫자를 구성할 수 있습니다.<sup>1</sup> 기본 데이터베이스는 DB 0입니다. `connection.GetDatabase(dbid)`을 사용하여 연결 단위로 다른 데이터베이스를 선택할 수 있습니다. 여기서 `dbid`는 `0`에서 `databases - 1` 사이의 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="cbc6d-353">가격 책정 계층에 따라 달라집니다.<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="cbc6d-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="cbc6d-354">이 값은 동시에 연결이 허용되는 클라이언트의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="cbc6d-355">제한에 도달하면 Redis는 'max number of clients reached' 오류를 반환하고 모든 새 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="cbc6d-356">`maxmemory` 정책은 최대 메모리(캐시를 만들 때 선택한 캐시의 크기)에 도달했을 때 Redis가 어떤 것을 제거할지 선택하는 방법에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="cbc6d-357">Azure Redis Cache를 사용할 때의 기본 설정은 `volatile-lru`로, LRU 알고리즘을 사용하여 만료 설정이 있는 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="cbc6d-358">이 설정은 Azure 포털에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="cbc6d-359">자세한 내용은 [메모리 정책](#memory-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="cbc6d-360">3</span><span class="sxs-lookup"><span data-stu-id="cbc6d-360">3</span></span> |<span data-ttu-id="cbc6d-361">메모리를 절약하기 위해 LRU 및 최소 TTL 알고리즘은 정밀한 알고리즘이 아닌 대략적인 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="cbc6d-362">기본적으로 Redis는 세 개의 키를 확인하고 가장 오래 전에 사용된 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="cbc6d-363">5, 000</span><span class="sxs-lookup"><span data-stu-id="cbc6d-363">5,000</span></span> |<span data-ttu-id="cbc6d-364">밀리초 단위의 Lua 스크립트 최대 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="cbc6d-365">최대 실행 시간에 도달하면 Redis는 허용된 시간 이후에도 실행 중인 스크립트를 기록하고 쿼리에 오류로 응답하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="cbc6d-366">500</span><span class="sxs-lookup"><span data-stu-id="cbc6d-366">500</span></span> |<span data-ttu-id="cbc6d-367">스크립트 이벤트 큐의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="cbc6d-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="cbc6d-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="cbc6d-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="cbc6d-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="cbc6d-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="cbc6d-370">클라이언트 출력 버퍼 제한은 어떤 이유로 서버에서 데이터를 읽는 속도가 충분히 빠르지 않은 클라이언트의 연결을 강제로 끊는 데 사용할 수 있습니다. 속도가 느린 일반적인 이유는 게시/구독 클라이언트가 게시자의 생성 속도만큼 빠르게 메시지를 소화하지 못하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="cbc6d-371">자세한 내용은 [http://redis.io/topics/clients](http://redis.io/topics/clients)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="cbc6d-372"><a name="databases"></a>
<sup>1</sup>`databases`에 대한 제한은 Azure Redis Cache 가격 책정 계층마다 다르며 캐시를 만들 때 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="cbc6d-373">캐시를 만드는 동안 `databases` 설정이 지정되지 않았다면 기본값은 16입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="cbc6d-374">기본 및 표준 캐시</span><span class="sxs-lookup"><span data-stu-id="cbc6d-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="cbc6d-375">C0(250MB) 캐시 - 최대 16개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="cbc6d-376">C1(1GB) 캐시 - 최대 16개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="cbc6d-377">C2(2.5GB) 캐시 - 최대 16개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="cbc6d-378">C3(6GB) 캐시 - 최대 16개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="cbc6d-379">C4(13GB) 캐시 - 최대 32개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="cbc6d-380">C5(26GB) 캐시 - 최대 48개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="cbc6d-381">C6(53GB) 캐시 - 최대 64개의 데이타베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="cbc6d-382">프리미엄 캐시</span><span class="sxs-lookup"><span data-stu-id="cbc6d-382">Premium caches</span></span>
  * <span data-ttu-id="cbc6d-383">P1(6GB-60GB)-최대 16개의 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="cbc6d-384">P2(13GB-130GB)-최대 32개의 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="cbc6d-385">P3(26GB-260GB)-최대 48개의 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="cbc6d-386">P4(53GB-530GB)-최대 64개의 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="cbc6d-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="cbc6d-387">Redis 클러스터를 사용할 수 있는 모든 프리미엄 캐시 - Redis 클러스터는 0 데이터베이스의 사용만을 지원하므로 Redis 클러스터를 사용할 수 있는 모든 프리미엄 캐시에 대한 `databases` 제한은 사실상 1이며 [Select](http://redis.io/commands/select) 명령은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="cbc6d-388">자세한 내용은 [클러스터링을 사용하려면 클라이언트 응용 프로그램을 변경해야 합니까?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="cbc6d-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="cbc6d-389">데이터베이스에 대한 자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-390">`databases` 설정은 캐시를 만드는 동안에만 PowerShell, CLI, 또는 다른 관리 클라이언트를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="cbc6d-391">PowerShell을 사용하여 캐시를 만드는 동안 `databases` 를 구성하는 예제는 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="cbc6d-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients`는 Azure Redis Cache 가격 책정 계층마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="cbc6d-393">기본 및 표준 캐시</span><span class="sxs-lookup"><span data-stu-id="cbc6d-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="cbc6d-394">C0(250MB) 캐시 - 최대 256개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="cbc6d-395">C1(1GB) 캐시 - 최대 1,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="cbc6d-396">C2(2.5GB) 캐시 - 최대 2,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="cbc6d-397">C3(6GB) 캐시 - 최대 5,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="cbc6d-398">C4(13GB) 캐시 - 최대 10,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="cbc6d-399">C5(26GB) 캐시 - 최대 15,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="cbc6d-400">C6(53GB) 캐시 - 최대 20,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="cbc6d-401">프리미엄 캐시</span><span class="sxs-lookup"><span data-stu-id="cbc6d-401">Premium caches</span></span>
  * <span data-ttu-id="cbc6d-402">P1(6GB - 60GB) - 최대 7,500개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="cbc6d-403">P2(13GB - 130GB) - 최대 15,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="cbc6d-404">P3(26GB - 260GB) - 최대 30,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="cbc6d-405">P4(53GB - 530GB) - 최대 40,000개 연결</span><span class="sxs-lookup"><span data-stu-id="cbc6d-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6d-406">각 캐시 크기는 특정 횟수의 연결*까지* 허용하지만 Redis에 대한 각 연결에는 오버헤드가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="cbc6d-407">이러한 오버헤드의 예로 TLS/SSL 암호화의 결과인 CPU 및 메모리 사용량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="cbc6d-408">특정 캐시 크기에 대한 최대 연결 제한은 부하가 적은 캐시를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="cbc6d-409">연결 오버헤드의 부하 *그리고* 클라이언트 작업의 부하가 시스템의 용량을 초과하면 현재 캐시 크기에 대한 연결 제한을 초과하지 않은 경우에도 캐시에 용량 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="cbc6d-410">Azure Redis Cache에서 지원되지 않는 Redis 명령</span><span class="sxs-lookup"><span data-stu-id="cbc6d-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cbc6d-411">Azure Redis Cache 인스턴스를 Microsoft에서 구성하고 관리하기 때문에 다음 명령은 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="cbc6d-412">이러한 명령을 호출하려고 하면 `"(error) ERR unknown command"`와 유사한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="cbc6d-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="cbc6d-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="cbc6d-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="cbc6d-414">BGSAVE</span></span>
> * <span data-ttu-id="cbc6d-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="cbc6d-415">CONFIG</span></span>
> * <span data-ttu-id="cbc6d-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="cbc6d-416">DEBUG</span></span>
> * <span data-ttu-id="cbc6d-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="cbc6d-417">MIGRATE</span></span>
> * <span data-ttu-id="cbc6d-418">저장</span><span class="sxs-lookup"><span data-stu-id="cbc6d-418">SAVE</span></span>
> * <span data-ttu-id="cbc6d-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="cbc6d-419">SHUTDOWN</span></span>
> * <span data-ttu-id="cbc6d-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="cbc6d-420">SLAVEOF</span></span>
> * <span data-ttu-id="cbc6d-421">클러스터 - 클러스트 쓰기 명령은 비활성화되지만, 읽기 전용 클러스터 명령은 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="cbc6d-422">Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="cbc6d-423">Redis 콘솔</span><span class="sxs-lookup"><span data-stu-id="cbc6d-423">Redis console</span></span>
<span data-ttu-id="cbc6d-424">Azure Portal에서 모든 캐시에 대해 제공되는 **Redis 콘솔**을 사용하면 Azure Redis Cache 인스턴스에 대해 안전하게 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="cbc6d-425">Redis 콘솔이 [VNET](cache-how-to-premium-vnet.md)에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="cbc6d-426">캐시가 VNET의 일부인 경우 VNET의 클라이언트만 캐시에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="cbc6d-427">Redis 콘솔은 VNET 외부에 있는 로컬 브라우저에서 실행되기 때문에 캐시에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="cbc6d-428">일부 Redis 명령은 Azure Redis Cache에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="cbc6d-429">Azure Redis Cache에서 사용할 수 없는 Redis 명령 목록은 이전 [Azure Redis Cache에서 지원되지 않는 Redis 명령](#redis-commands-not-supported-in-azure-redis-cache) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="cbc6d-430">Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="cbc6d-431">Redis 콘솔에 액세스하려면 **Redis Cache** 블레이드에서 **콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="cbc6d-433">캐시 인스턴스에 대해 명령을 실행하려면 원하는 명령을 콘솔에 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="cbc6d-435">프리미엄 클러스터형 캐시에서 Redis 콘솔 사용</span><span class="sxs-lookup"><span data-stu-id="cbc6d-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="cbc6d-436">프리미엄 클러스터형 캐시에서 Redis 콘솔을 사용하는 경우 캐시의 단일 분할된 데이터베이스에 대해 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="cbc6d-437">특정 분할된 데이터베이스에 대해 명령을 실행하려면 분할된 데이터베이스 선택에서 원하는 분할된 데이터베이스를 클릭하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Redis 콘솔](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="cbc6d-439">연결된 분할된 데이터베이스가 아닌 다른 분할된 데이터베이스에 저장된 키에 액세스하려고 하면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="cbc6d-440">이전 예제에서 분할된 데이터베이스 1은 선택된 분할된 데이터베이스이지만 `myKey`는 오류 메시지의 `(shard 0)` 부분에 표시된 대로 분할된 데이터베이스 0에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="cbc6d-441">이 예제에서 `myKey`에 액세스하려면 분할된 데이터베이스 선택을 사용하여 분할된 데이터베이스 0을 선택한 다음 원하는 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="cbc6d-442">캐시를 새 구독으로 이동</span><span class="sxs-lookup"><span data-stu-id="cbc6d-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="cbc6d-443">**이동**을 클릭하여 캐시를 새 구독으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Redis Cache 이동](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="cbc6d-445">한 리소스 그룹에서 다른 리소스 그룹으로, 그리고 한 구독에서 다른 구독으로 리소스를 이동하는 방법에 대한 자세한 내용은 [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbc6d-446">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbc6d-446">Next steps</span></span>
* <span data-ttu-id="cbc6d-447">Redis 명령을 사용하는 방법은 [어떻게 Redis 명령을 실행할 수 있나요?](cache-faq.md#how-can-i-run-redis-commands)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc6d-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

