---
title: "Azure Redis Cache를 관리하는 방법 | Microsoft Docs"
description: "Azure Redis Cache 다시 부팅 및 업데이트 예약과 같은 관리 작업을 수행하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3352fec59d7dfbfab9b0416992a60f11d0ec2402
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-administer-azure-redis-cache"></a><span data-ttu-id="580af-103">Azure Redis Cache를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="580af-103">How to administer Azure Redis Cache</span></span>
<span data-ttu-id="580af-104">이 토픽에서는 [재부팅](#reboot) 및 Azure Redis Cache 인스턴스의 [업데이트 예약](#schedule-updates)과 같은 관리 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-104">This topic describes how to perform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span></span>

## <a name="reboot"></a><span data-ttu-id="580af-105">Reboot</span><span class="sxs-lookup"><span data-stu-id="580af-105">Reboot</span></span>
<span data-ttu-id="580af-106">**재부팅** 블레이드에서는 하나 이상의 캐시 노드를 재부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-106">The **Reboot** blade allows you to reboot one or more nodes of your cache.</span></span> <span data-ttu-id="580af-107">이 다시 부팅 기능을 사용하면 캐시 노드에 오류가 발생하는 경우 응용 프로그램의 복원력을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-107">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

<span data-ttu-id="580af-109">다시 부팅할 노드를 선택하고 **다시 부팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-109">Select the nodes to reboot and click **Reboot**.</span></span>

![Reboot](./media/cache-administration/redis-cache-reboot.png)

<span data-ttu-id="580af-111">클러스터링이 설정된 프리미엄 캐시를 사용하는 경우 재부팅할 캐시 분할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-111">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

<span data-ttu-id="580af-113">하나 이상의 캐시 노드를 다시 부팅하려면 원하는 노드를 선택하고 **다시 부팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-113">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="580af-114">클러스터링이 설정된 프리미엄 캐시를 사용하는 경우 다시 부팅할 원하는 분할을 선택하고 **다시 부팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-114">If you have a premium cache with clustering enabled, select the desired shards to reboot and then click **Reboot**.</span></span> <span data-ttu-id="580af-115">몇 분 후 선택된 노드가 다시 부팅되고, 다시 몇 분 후에 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-115">After a few minutes, the selected nodes reboot, and are back online a few minutes later.</span></span>

<span data-ttu-id="580af-116">클라이언트 응용 프로그램에 미치는 영향은 다시 부팅하는 노드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="580af-116">The impact on client applications varies depending on which nodes that you reboot.</span></span>

* <span data-ttu-id="580af-117">**마스터** - 마스터 노드를 다시 부팅하는 경우 Azure Redis Cache가 복제본 노드로 장애 조치(failover)되고 해당 노드가 마스터로 승격됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-117">**Master** - When the master node is rebooted, Azure Redis Cache fails over to the replica node and promotes it to master.</span></span> <span data-ttu-id="580af-118">이 장애 조치(failover) 동안에는 짧은 시간 동안 캐시에 연결되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-118">During this failover, there may be a short interval in which connections may fail to the cache.</span></span>
* <span data-ttu-id="580af-119">**슬레이브** - 슬레이브 노드를 다시 부팅하는 경우는 일반적으로 캐시 클라이언트에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-119">**Slave** - When the slave node is rebooted, there is typically no impact to cache clients.</span></span>
* <span data-ttu-id="580af-120">**마스터 및 슬레이브 모두** - 두 캐시 노드가 모두 다시 부팅되면 캐시의 모든 데이터가 유실되고, 주 노드가 다시 온라인 상태가 될 때까지 캐시에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-120">**Both master and slave** - When both cache nodes are rebooted, all data is lost in the cache and connections to the cache fail until the primary node comes back online.</span></span> <span data-ttu-id="580af-121">[데이터 지속성](cache-how-to-premium-persistence.md)을 구성한 경우 캐시가 다시 온라인 상태가 되면 가장 최근의 백업을 복원하지만 가장 최근의 백업이 손실된 후에 발생한 캐시가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-121">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup is restored when the cache comes back online, but any cache writes that occurred after the most recent backup are lost.</span></span>
* <span data-ttu-id="580af-122">**클러스터링이 설정된 프리미엄 캐시 노드** - 클러스터링이 설정된 프리미엄 캐시 중 하나 이상의 노드를 다시 부팅하면 선택한 노드에서도 해당하는 노드 또는 클러스터링되지 않은 캐시의 노드를 다시 부팅할 때와 같은 동작이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="580af-122">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, the behavior for the selected nodes is the same as when you reboot the corresponding node or nodes of a non-clustered cache.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="580af-123">이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-123">Reboot is now available for all pricing tiers.</span></span>
> 
> 

## <a name="reboot-faq"></a><span data-ttu-id="580af-124">다시 부팅 FAQ</span><span class="sxs-lookup"><span data-stu-id="580af-124">Reboot FAQ</span></span>
* [<span data-ttu-id="580af-125">응용 프로그램을 테스트하려는 경우 어떤 노드를 다시 부팅해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="580af-125">Which node should I reboot to test my application?</span></span>](#which-node-should-i-reboot-to-test-my-application)
* [<span data-ttu-id="580af-126">캐시를 다시 부팅하여 클라이언트 연결을 끊을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-126">Can I reboot the cache to clear client connections?</span></span>](#can-i-reboot-the-cache-to-clear-client-connections)
* [<span data-ttu-id="580af-127">다시 부팅하는 경우 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="580af-127">Will I lose data from my cache if I do a reboot?</span></span>](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [<span data-ttu-id="580af-128">PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-128">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="580af-129">어떤 가격 책정 계층에서 다시 부팅 기능을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-129">What pricing tiers can use the reboot functionality?</span></span>](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-to-test-my-application"></a><span data-ttu-id="580af-130">응용 프로그램을 테스트하려는 경우 어떤 노드를 다시 부팅해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="580af-130">Which node should I reboot to test my application?</span></span>
<span data-ttu-id="580af-131">캐시의 주 노드 장애 시 응용 프로그램의 복원력을 테스트하려면 **마스터** 노드를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-131">To test the resiliency of your application against failure of the primary node of your cache, reboot the **Master** node.</span></span> <span data-ttu-id="580af-132">캐시의 보조 노드 장애 시 응용 프로그램의 복원력을 테스트하려면 **슬레이브** 노드를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-132">To test the resiliency of your application against failure of the secondary node, reboot the **Slave** node.</span></span> <span data-ttu-id="580af-133">캐시 전체의 장애 시 응용 프로그램의 복원력을 테스트하려면 **두** 노드를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-133">To test the resiliency of your application against total failure of the cache, reboot **Both** nodes.</span></span>

### <a name="can-i-reboot-the-cache-to-clear-client-connections"></a><span data-ttu-id="580af-134">캐시를 다시 부팅하여 클라이언트 연결을 끊을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-134">Can I reboot the cache to clear client connections?</span></span>
<span data-ttu-id="580af-135">예, 캐시를 다시 부팅하면 모든 클라이언트 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="580af-135">Yes, if you reboot the cache all client connections are cleared.</span></span> <span data-ttu-id="580af-136">다시 부팅은 클라이언트 응용 프로그램의 논리 오류나 버그로 인해 모든 클라이언트 연결이 다 소비된 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-136">Rebooting can be useful in the case where all client connections are used up due to a logic error or a bug in the client application.</span></span> <span data-ttu-id="580af-137">각 가격 책정 계층에는 다양한 크기의 [클라이언트 연결 제한](cache-configure.md#default-redis-server-configuration)이 있으며 이러한 제한에 도달하면 추가적인 클라이언트 연결이 더 이상 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-137">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for the various sizes, and once these limits are reached, no more client connections are accepted.</span></span> <span data-ttu-id="580af-138">캐시를 다시 부팅하면 모든 클라이언트 연결을 끊을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-138">Rebooting the cache provides a way to clear all client connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="580af-139">캐시를 다시 부팅하여 클라이언트 연결의 선택을 취소하는 경우 Redis 노드가 다시 온라인 상태가 되면 StackExchange.Redis가 자동으로 다시 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-139">If you reboot your cache to clear client connections, StackExchange.Redis automatically reconnects once the Redis node is back online.</span></span> <span data-ttu-id="580af-140">기본 문제가 해결되지 않으면 클라이언트 연결은 계속 소비될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="580af-140">If the underlying issue is not resolved, the client connections may continue to be used up.</span></span>
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a><span data-ttu-id="580af-141">다시 부팅하는 경우 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="580af-141">Will I lose data from my cache if I do a reboot?</span></span>
<span data-ttu-id="580af-142">**마스터** 및 **슬레이브** 노드를 둘 다 다시 부팅하는 경우 캐시(또는 클러스터링이 설정된 프리미엄 캐시를 사용하는 해당 분할)의 모든 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-142">If you reboot both the **Master** and **Slave** nodes, all data in the cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span></span> <span data-ttu-id="580af-143">[데이터 지속성](cache-how-to-premium-persistence.md)을 구성한 경우 캐시가 다시 온라인 상태가 되면 가장 최근의 백업을 복원하지만 수행된 백업이 손실된 후에 발생한 캐시가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-143">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup will be restored when the cache comes back online, but any cache writes that have occurred after the backup was made are lost.</span></span>

<span data-ttu-id="580af-144">노드 중 하나만 다시 부팅하는 경우 일반적으로는 데이터가 손실되지 않지만 여전히 손실될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-144">If you reboot just one of the nodes, data is not typically lost, but it still may be.</span></span> <span data-ttu-id="580af-145">예를 들어 캐시 쓰기가 진행 중일 때 마스터 노드를 다시 부팅하면 캐시 쓰기의 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-145">For example if the master node is rebooted and a cache write is in progress, the data from the cache write is lost.</span></span> <span data-ttu-id="580af-146">데이터 손실이 발생할 수 있는 또 다른 시나리오는 노드 하나를 다시 부팅하는 동시에 오류로 인해 다른 노드가 작동 중단되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="580af-146">Another scenario for data loss would be if you reboot one node and the other node happens to go down due to a failure at the same time.</span></span> <span data-ttu-id="580af-147">데이터 손실의 가능한 원인에 대한 자세한 내용은 [내 Redis 데이터에서 무엇이 변경되었나요?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580af-147">For more information about possible causes for data loss, see [What happened to my data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span></span>

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="580af-148">PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-148">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="580af-149">예, PowerShell 소개는 [Redis Cache를 다시 부팅하려면](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580af-149">Yes, for PowerShell instructions see [To reboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span></span>

### <a name="what-pricing-tiers-can-use-the-reboot-functionality"></a><span data-ttu-id="580af-150">어떤 가격 책정 계층에서 다시 부팅 기능을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-150">What pricing tiers can use the reboot functionality?</span></span>
<span data-ttu-id="580af-151">모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-151">Reboot is available for all pricing tiers.</span></span>

## <a name="schedule-updates"></a><span data-ttu-id="580af-152">업데이트를 예약</span><span class="sxs-lookup"><span data-stu-id="580af-152">Schedule updates</span></span>
<span data-ttu-id="580af-153">**업데이트 예약** 블레이드에서는 프리미엄 계층 캐시의 유지 관리 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-153">The **Schedule updates** blade allows you to designate a maintenance window for your Premium tier cache.</span></span> <span data-ttu-id="580af-154">유지 관리 기간이 지정되면 이 기간 동안 Redis 서버 업데이트가 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-154">When the maintenance window is specified, any Redis server updates are made during this window.</span></span> 

> [!NOTE] 
> <span data-ttu-id="580af-155">유지 관리 기간은 Redis 서버 업데이트에만 적용되며 Azure 업데이트나 캐시를 호스트하는 VM의 운영 체제에 대한 업데이트에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-155">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![업데이트 예약](./media/cache-administration/redis-schedule-updates.png)

<span data-ttu-id="580af-157">유지 관리 기간을 지정하려면 원하는 요일을 선택하고 각 요일의 유지 관리 기간 시작 시간을 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="580af-157">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="580af-158">유지 관리 기간 시간은 UTC로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="580af-158">Note that the maintenance window time is in UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="580af-159">업데이트를 위한 기본 유지 관리 기간은 5시간입니다.</span><span class="sxs-lookup"><span data-stu-id="580af-159">The default maintenance window for updates is five hours.</span></span> <span data-ttu-id="580af-160">이 값은 Azure 포털에서는 구성할 수 없지만 PowerShell에서 [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet의 `MaintenanceWindow` 매개 변수를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-160">This value is not configurable from the Azure portal, but you can configure it in PowerShell using the `MaintenanceWindow` parameter of the [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet.</span></span> <span data-ttu-id="580af-161">자세한 내용은 [PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580af-161">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span></span>
> 
> 

## <a name="schedule-updates-faq"></a><span data-ttu-id="580af-162">업데이트 예약 FAQ</span><span class="sxs-lookup"><span data-stu-id="580af-162">Schedule updates FAQ</span></span>
* [<span data-ttu-id="580af-163">일정 업데이트 기능을 사용하지 않으면 업데이트가 언제 발생하나요?</span><span class="sxs-lookup"><span data-stu-id="580af-163">When do updates occur if I don't use the schedule updates feature?</span></span>](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [<span data-ttu-id="580af-164">예약된 유지 관리 기간 동안에는 어떤 유형의 업데이트가 진행되나요?</span><span class="sxs-lookup"><span data-stu-id="580af-164">What type of updates are made during the scheduled maintenance window?</span></span>](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [<span data-ttu-id="580af-165">PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-165">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span></span>](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="580af-166">어떤 가격 책정 계층에서 업데이트 예약 기능을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-166">What pricing tiers can use the schedule updates functionality?</span></span>](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature"></a><span data-ttu-id="580af-167">일정 업데이트 기능을 사용하지 않으면 업데이트가 언제 발생하나요?</span><span class="sxs-lookup"><span data-stu-id="580af-167">When do updates occur if I don't use the schedule updates feature?</span></span>
<span data-ttu-id="580af-168">유지 관리 기간을 지정하지 않으면, 언제든지 업데이트가 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-168">If you don't specify a maintenance window, updates can be made at any time.</span></span>

### <a name="what-type-of-updates-are-made-during-the-scheduled-maintenance-window"></a><span data-ttu-id="580af-169">예약된 유지 관리 기간 동안에는 어떤 유형의 업데이트가 진행되나요?</span><span class="sxs-lookup"><span data-stu-id="580af-169">What type of updates are made during the scheduled maintenance window?</span></span>
<span data-ttu-id="580af-170">예약된 유지 관리 기간 동안에는 Redis 서버 업데이트만 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="580af-170">Only Redis server updates are made during the scheduled maintenance window.</span></span> <span data-ttu-id="580af-171">유지 관리 기간이 Azure 업데이트 또는 VM 운영 체제에 대한 업데이트에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-171">The maintenance window does not apply to Azure updates or updates to the VM operating system.</span></span>

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="580af-172">PowerShell, CLI 또는 기타 관리 도구를 사용하여 관리되는 예약된 업데이트를 수행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-172">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="580af-173">예, 다음 PowerShell cmdlet을 사용하여 예약된 업데이트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-173">Yes, you can manage your scheduled updates using the following PowerShell cmdlets:</span></span>

* [<span data-ttu-id="580af-174">Get-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="580af-174">Get-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [<span data-ttu-id="580af-175">New-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="580af-175">New-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [<span data-ttu-id="580af-176">New-AzureRmRedisCacheScheduleEntry</span><span class="sxs-lookup"><span data-stu-id="580af-176">New-AzureRmRedisCacheScheduleEntry</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [<span data-ttu-id="580af-177">Remove-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="580af-177">Remove-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-the-schedule-updates-functionality"></a><span data-ttu-id="580af-178">어떤 가격 책정 계층에서 업데이트 예약 기능을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="580af-178">What pricing tiers can use the schedule updates functionality?</span></span>
<span data-ttu-id="580af-179">**업데이트 예약** 기능은 프리미엄 가격 책정 계층에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580af-179">The **Schedule updates** feature is only available in the premium pricing tier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="580af-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="580af-180">Next steps</span></span>
* <span data-ttu-id="580af-181">[Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md) 기능에 대해 더 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="580af-181">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span></span>

