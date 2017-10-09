---
title: Azure Redis Cache aaaHow tooadminister | Microsoft Docs
description: "Tooperform 관리 작업 같은 재부팅 방법을 자세히 알아보고 Azure Redis Cache에 대 한 일정을 업데이트 합니다."
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a><span data-ttu-id="d445f-103">Azure Redis 캐시 하는 tooadminister 방법</span><span class="sxs-lookup"><span data-stu-id="d445f-103">How tooadminister Azure Redis Cache</span></span>
<span data-ttu-id="d445f-104">이 항목에서는 tooperform 관리와 같은 작업을 설명 [재부팅](#reboot) 및 [업데이트 예약](#schedule-updates) Azure Redis 캐시 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-104">This topic describes how tooperform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span></span>

## <a name="reboot"></a><span data-ttu-id="d445f-105">Reboot</span><span class="sxs-lookup"><span data-stu-id="d445f-105">Reboot</span></span>
<span data-ttu-id="d445f-106">hello **재부팅** 블레이드 있습니다 tooreboot 캐시의 하나 이상의 노드.</span><span class="sxs-lookup"><span data-stu-id="d445f-106">hello **Reboot** blade allows you tooreboot one or more nodes of your cache.</span></span> <span data-ttu-id="d445f-107">이 다시 부팅 기능을 사용 하면 있습니다 tootest 복구를 위한 응용 프로그램 캐시 노드 오류가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="d445f-107">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

<span data-ttu-id="d445f-109">Hello 노드 tooreboot를 선택 하 고 클릭 **재부팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-109">Select hello nodes tooreboot and click **Reboot**.</span></span>

![Reboot](./media/cache-administration/redis-cache-reboot.png)

<span data-ttu-id="d445f-111">프리미엄 캐시 클러스터링을 사용 해야 하는 경우에 hello 캐시 tooreboot의 어떤 분할 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-111">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

<span data-ttu-id="d445f-113">tooreboot 하나 이상의 노드 캐시의 hello 원하는 노드를 선택 하 고 클릭 **재부팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-113">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="d445f-114">프리미엄 캐시 클러스터링을 사용 해야 하는 경우 필요한 hello 분할 영역 tooreboot 선택한 다음 클릭 **재부팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-114">If you have a premium cache with clustering enabled, select hello desired shards tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="d445f-115">몇 분 후 hello 선택한 노드 다시 부팅 하 고 몇 분 후 다시 온라인 상태로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-115">After a few minutes, hello selected nodes reboot, and are back online a few minutes later.</span></span>

<span data-ttu-id="d445f-116">클라이언트 응용 프로그램에 미치는 영향을 hello 다시 부팅 하는 노드를 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-116">hello impact on client applications varies depending on which nodes that you reboot.</span></span>

* <span data-ttu-id="d445f-117">**마스터** -때 hello 마스터 노드는 다시 부팅 된, Azure Redis 캐시 실패 하 toohello 복제본 노드를 통해 및 toomaster 올립니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-117">**Master** - When hello master node is rebooted, Azure Redis Cache fails over toohello replica node and promotes it toomaster.</span></span> <span data-ttu-id="d445f-118">이 장애 조치 하는 동안 짧은 간격으로는 연결이 실패할 수 있다 toohello 캐시 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-118">During this failover, there may be a short interval in which connections may fail toohello cache.</span></span>
* <span data-ttu-id="d445f-119">**슬레이브** -hello 종속 노드를 다시 부팅 하는 경우는 일반적으로 영향 toocache 클라이언트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-119">**Slave** - When hello slave node is rebooted, there is typically no impact toocache clients.</span></span>
* <span data-ttu-id="d445f-120">**마스터 및 슬레이브** -캐시 노드 모두 재부팅 될 때 hello 주 노드가 온라인 상태가 될 때까지 hello 캐시 및 연결 toohello 캐시 실패에서 모든 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-120">**Both master and slave** - When both cache nodes are rebooted, all data is lost in hello cache and connections toohello cache fail until hello primary node comes back online.</span></span> <span data-ttu-id="d445f-121">구성한 경우 [데이터 지 속성](cache-how-to-premium-persistence.md), hello 캐시를 다시 온라인 상태가 되 완전히 hello 가장 최근의 백업 이후에 발생 한 캐시 쓰기가 손실 hello 가장 최근 백업이 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-121">If you have configured [data persistence](cache-how-to-premium-persistence.md), hello most recent backup is restored when hello cache comes back online, but any cache writes that occurred after hello most recent backup are lost.</span></span>
* <span data-ttu-id="d445f-122">**premium의 노드를 클러스터링을 사용 캐시** -하나를 다시 부팅 하거나 클러스터링 하 여 프리미엄 캐시의 노드 선택 hello에 대 한 동작 hello를 사용 하는 경우 노드는 동일한 경우 다시 부팅 하면 hello 해당 노드 또는 클러스터 되지 않은의 노드에으로 hello 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-122">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, hello behavior for hello selected nodes is hello same as when you reboot hello corresponding node or nodes of a non-clustered cache.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d445f-123">이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-123">Reboot is now available for all pricing tiers.</span></span>
> 
> 

## <a name="reboot-faq"></a><span data-ttu-id="d445f-124">다시 부팅 FAQ</span><span class="sxs-lookup"><span data-stu-id="d445f-124">Reboot FAQ</span></span>
* [<span data-ttu-id="d445f-125">노드 하려면 다시 부팅 해야 tootest 내 응용 프로그램과?</span><span class="sxs-lookup"><span data-stu-id="d445f-125">Which node should I reboot tootest my application?</span></span>](#which-node-should-i-reboot-to-test-my-application)
* [<span data-ttu-id="d445f-126">캐시 tooclear 클라이언트 연결의 hello를 다시 부팅할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-126">Can I reboot hello cache tooclear client connections?</span></span>](#can-i-reboot-the-cache-to-clear-client-connections)
* [<span data-ttu-id="d445f-127">다시 부팅하는 경우 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-127">Will I lose data from my cache if I do a reboot?</span></span>](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [<span data-ttu-id="d445f-128">PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-128">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="d445f-129">어떤 가격 책정 계층 hello 다시 부팅 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-129">What pricing tiers can use hello reboot functionality?</span></span>](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a><span data-ttu-id="d445f-130">노드 하려면 다시 부팅 해야 tootest 내 응용 프로그램과?</span><span class="sxs-lookup"><span data-stu-id="d445f-130">Which node should I reboot tootest my application?</span></span>
<span data-ttu-id="d445f-131">캐시를 다시 부팅 hello hello 주 노드의 오류 로부터 응용 프로그램의 tootest hello 복원 력을 **마스터** 노드.</span><span class="sxs-lookup"><span data-stu-id="d445f-131">tootest hello resiliency of your application against failure of hello primary node of your cache, reboot hello **Master** node.</span></span> <span data-ttu-id="d445f-132">다시 부팅 hello hello 보조 노드의 오류 로부터 응용 프로그램의 tootest hello 복원 력을 **슬레이브** 노드.</span><span class="sxs-lookup"><span data-stu-id="d445f-132">tootest hello resiliency of your application against failure of hello secondary node, reboot hello **Slave** node.</span></span> <span data-ttu-id="d445f-133">tootest hello 복원 력 응용 프로그램의 총 오류 로부터 hello 캐시의 다시 부팅 **둘 다** 노드.</span><span class="sxs-lookup"><span data-stu-id="d445f-133">tootest hello resiliency of your application against total failure of hello cache, reboot **Both** nodes.</span></span>

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a><span data-ttu-id="d445f-134">캐시 tooclear 클라이언트 연결의 hello를 다시 부팅할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-134">Can I reboot hello cache tooclear client connections?</span></span>
<span data-ttu-id="d445f-135">예, hello 캐시를 다시 부팅 하는 경우 모든 클라이언트 연결이 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-135">Yes, if you reboot hello cache all client connections are cleared.</span></span> <span data-ttu-id="d445f-136">다시 부팅 하는 hello 경우 기한 tooa 논리 오류 또는 hello 클라이언트 응용 프로그램의 버그 모든 클라이언트 연결이 사용 되는 위치에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-136">Rebooting can be useful in hello case where all client connections are used up due tooa logic error or a bug in hello client application.</span></span> <span data-ttu-id="d445f-137">각 가격 책정 계층에 다른 [클라이언트 연결 제한](cache-configure.md#default-redis-server-configuration) 에 대 한 다양 한 크기 hello 및 이러한 한도 도달한 후 클라이언트 연결이 더 이상 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-137">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for hello various sizes, and once these limits are reached, no more client connections are accepted.</span></span> <span data-ttu-id="d445f-138">Hello 캐시를 다시 부팅 하면 모든 클라이언트 연결 방법을 tooclear 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-138">Rebooting hello cache provides a way tooclear all client connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d445f-139">캐시 tooclear 클라이언트 연결을 다시 부팅 하면 StackExchange.Redis hello Redis 노드가 다시 온라인 상태가 되 면 자동으로 다시.</span><span class="sxs-lookup"><span data-stu-id="d445f-139">If you reboot your cache tooclear client connections, StackExchange.Redis automatically reconnects once hello Redis node is back online.</span></span> <span data-ttu-id="d445f-140">Hello 기본 문제 해결 되지 않으면 hello 클라이언트 연결은 계속 toobe 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-140">If hello underlying issue is not resolved, hello client connections may continue toobe used up.</span></span>
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a><span data-ttu-id="d445f-141">다시 부팅하는 경우 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-141">Will I lose data from my cache if I do a reboot?</span></span>
<span data-ttu-id="d445f-142">두 hello를 다시 부팅 하면 **마스터** 및 **슬레이브** 노드 hello 캐시에 (또는 프리미엄 캐시를 사용 하는 클러스터링을 사용 하는 경우 해당 분할)의 모든 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-142">If you reboot both hello **Master** and **Slave** nodes, all data in hello cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span></span> <span data-ttu-id="d445f-143">구성한 경우 [데이터 지 속성](cache-how-to-premium-persistence.md), hello 가장 최근 백업이 복원 됩니다 hello 캐시 다시 온라인 상태가 되지만 hello 백업을 만든 후에 발생 한 모든 캐시 쓰기 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-143">If you have configured [data persistence](cache-how-to-premium-persistence.md), hello most recent backup will be restored when hello cache comes back online, but any cache writes that have occurred after hello backup was made are lost.</span></span>

<span data-ttu-id="d445f-144">Hello 노드 중 하나를 다시 부팅 하는 경우 데이터가 일반적으로 손실 됩니다. 하지만 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-144">If you reboot just one of hello nodes, data is not typically lost, but it still may be.</span></span> <span data-ttu-id="d445f-145">예를 들어 hello 마스터 노드 다시 부팅 되 고 캐시 쓰기 hello 데이터 hello 캐시 쓰기에서 진행 되는 경우 손실 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-145">For example if hello master node is rebooted and a cache write is in progress, hello data from hello cache write is lost.</span></span> <span data-ttu-id="d445f-146">데이터 손실에 대 한 또 다른 시나리오는 한 노드를 다시 부팅 하 고 다른 hello 노드 발생 toogo 아래로 tooa 오류 hello에 인해 것 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-146">Another scenario for data loss would be if you reboot one node and hello other node happens toogo down due tooa failure at hello same time.</span></span> <span data-ttu-id="d445f-147">데이터 손실에 대 한 가능한 원인에 대 한 자세한 내용은 참조 [Redis에서 발생 했습니다 toomy 데이터?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span><span class="sxs-lookup"><span data-stu-id="d445f-147">For more information about possible causes for data loss, see [What happened toomy data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span></span>

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="d445f-148">PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-148">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="d445f-149">예, PowerShell 명령 참조 [tooreboot Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-149">Yes, for PowerShell instructions see [tooreboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span></span>

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a><span data-ttu-id="d445f-150">어떤 가격 책정 계층 hello 다시 부팅 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-150">What pricing tiers can use hello reboot functionality?</span></span>
<span data-ttu-id="d445f-151">모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-151">Reboot is available for all pricing tiers.</span></span>

## <a name="schedule-updates"></a><span data-ttu-id="d445f-152">업데이트를 예약</span><span class="sxs-lookup"><span data-stu-id="d445f-152">Schedule updates</span></span>
<span data-ttu-id="d445f-153">hello **업데이트를 예약할** 블레이드 toodesignate 프리미엄 계층 캐시에 대 한 유지 관리 기간을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-153">hello **Schedule updates** blade allows you toodesignate a maintenance window for your Premium tier cache.</span></span> <span data-ttu-id="d445f-154">Hello 유지 관리 기간을 지정 하면이 기간 동안 모든 Redis 서버 업데이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-154">When hello maintenance window is specified, any Redis server updates are made during this window.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d445f-155">tooRedis 서버 업데이트 및 Azure 업데이트 또는 hello 캐시를 호스트 하는 hello Vm의 toohello 운영 체제를 업데이트 하지 tooany hello 유지 관리 기간에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-155">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![업데이트를 예약](./media/cache-administration/redis-schedule-updates.png)

<span data-ttu-id="d445f-157">toospecify 유지 관리 기간 hello 원하는 일 수를 확인 합니다. 각 날에 대 한 hello 유지 관리 창 시작 시간을 지정 고를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-157">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="d445f-158">Hello 유지 관리 기간에 UTC를 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-158">Note that hello maintenance window time is in UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="d445f-159">업데이트에 대 한 hello 기본 유지 관리 기간에는 5 개의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-159">hello default maintenance window for updates is five hours.</span></span> <span data-ttu-id="d445f-160">이 값은 hello Azure 포털에서에서 구성할 수 있는 되지 않지만 hello를 사용 하 여 PowerShell에서 구성할 수 있습니다 `MaintenanceWindow` hello의 매개 변수 [새로 AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d445f-160">This value is not configurable from hello Azure portal, but you can configure it in PowerShell using hello `MaintenanceWindow` parameter of hello [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet.</span></span> <span data-ttu-id="d445f-161">자세한 내용은 [PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d445f-161">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span></span>
> 
> 

## <a name="schedule-updates-faq"></a><span data-ttu-id="d445f-162">업데이트 예약 FAQ</span><span class="sxs-lookup"><span data-stu-id="d445f-162">Schedule updates FAQ</span></span>
* [<span data-ttu-id="d445f-163">Hello 일정 업데이트 기능을 사용 하지 않아도 업데이트 발생 시기는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-163">When do updates occur if I don't use hello schedule updates feature?</span></span>](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [<span data-ttu-id="d445f-164">유지 관리 기간을 예약할 hello 중에 어떤 유형의 업데이트가 수행 되 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-164">What type of updates are made during hello scheduled maintenance window?</span></span>](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [<span data-ttu-id="d445f-165">PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-165">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span></span>](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="d445f-166">어떤 가격 책정 계층 hello 일정 업데이트 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-166">What pricing tiers can use hello schedule updates functionality?</span></span>](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a><span data-ttu-id="d445f-167">Hello 일정 업데이트 기능을 사용 하지 않아도 업데이트 발생 시기는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-167">When do updates occur if I don't use hello schedule updates feature?</span></span>
<span data-ttu-id="d445f-168">유지 관리 기간을 지정하지 않으면, 언제든지 업데이트가 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-168">If you don't specify a maintenance window, updates can be made at any time.</span></span>

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a><span data-ttu-id="d445f-169">유지 관리 기간을 예약할 hello 중에 어떤 유형의 업데이트가 수행 되 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-169">What type of updates are made during hello scheduled maintenance window?</span></span>
<span data-ttu-id="d445f-170">만 Redis 서버 hello 예약 된 유지 관리 기간 동안 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-170">Only Redis server updates are made during hello scheduled maintenance window.</span></span> <span data-ttu-id="d445f-171">hello 유지 관리 기간 tooAzure 업데이트는 적용 되지 않습니다 또는 toohello VM 운영 체제를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-171">hello maintenance window does not apply tooAzure updates or updates toohello VM operating system.</span></span>

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="d445f-172">PowerShell, CLI 또는 기타 관리 도구를 사용하여 관리되는 예약된 업데이트를 수행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d445f-172">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="d445f-173">예, PowerShell cmdlet을 다음 hello를 사용 하 여 예약 된 업데이트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-173">Yes, you can manage your scheduled updates using hello following PowerShell cmdlets:</span></span>

* [<span data-ttu-id="d445f-174">Get-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="d445f-174">Get-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [<span data-ttu-id="d445f-175">New-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="d445f-175">New-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [<span data-ttu-id="d445f-176">New-AzureRmRedisCacheScheduleEntry</span><span class="sxs-lookup"><span data-stu-id="d445f-176">New-AzureRmRedisCacheScheduleEntry</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [<span data-ttu-id="d445f-177">Remove-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="d445f-177">Remove-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a><span data-ttu-id="d445f-178">어떤 가격 책정 계층 hello 일정 업데이트 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d445f-178">What pricing tiers can use hello schedule updates functionality?</span></span>
<span data-ttu-id="d445f-179">hello **업데이트를 예약할** 기능은 hello 프리미엄 가격 책정 계층에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-179">hello **Schedule updates** feature is only available in hello premium pricing tier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d445f-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d445f-180">Next steps</span></span>
* <span data-ttu-id="d445f-181">[Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md) 기능에 대해 더 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d445f-181">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span></span>

