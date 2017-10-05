---
title: "Azure Redis Cache 크기를 조정하는 방법 | Microsoft Docs"
description: "Azure Redis Cache 인스턴스 크기를 조정하는 방법에 대해 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="23ae8-103">Azure Redis Cache 크기를 조정하는 방법</span><span class="sxs-lookup"><span data-stu-id="23ae8-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="23ae8-104">Azure Redis Cache에는 캐시 크기 및 기능을 유연하게 선택할 수 있는 다양한 캐시 제품이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="23ae8-105">캐시를 만든 후 응용 프로그램 요구 사항이 변경되면 캐시의 크기 및 가격 책정 계층의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="23ae8-106">이 문서에서는 Azure Portal에서, Azure PowerShell 및 Azure CLI와 같은 도구를 사용하여 캐시 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="23ae8-107">크기를 조정하는 경우</span><span class="sxs-lookup"><span data-stu-id="23ae8-107">When to scale</span></span>
<span data-ttu-id="23ae8-108">Azure Redis Cache의 [모니터링](cache-how-to-monitor.md) 기능을 사용하여 캐시의 상태 및 성능을 모니터링하고 캐시 크기를 조정해야 하는 경우를 결정하는데 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="23ae8-109">다음 메트릭을 모니터링하면 크기를 조정해야 하는지 결정하는데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="23ae8-110">Redis 서버 부하</span><span class="sxs-lookup"><span data-stu-id="23ae8-110">Redis Server Load</span></span>
* <span data-ttu-id="23ae8-111">메모리 사용량</span><span class="sxs-lookup"><span data-stu-id="23ae8-111">Memory Usage</span></span>
* <span data-ttu-id="23ae8-112">네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="23ae8-112">Network Bandwidth</span></span>
* <span data-ttu-id="23ae8-113">CPU 사용량</span><span class="sxs-lookup"><span data-stu-id="23ae8-113">CPU Usage</span></span>

<span data-ttu-id="23ae8-114">캐시가 더 이상 응용 프로그램 요구 사항을 충족시키지 못한다고 판단되면 응용 프로그램에 적합하도록 더 크거나 더 작은 캐시 가격 책정 계층으로 규모를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="23ae8-115">사용할 캐시 가격 책정 계층 결정에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23ae8-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="23ae8-116">캐시 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-116">Scale a cache</span></span>
<span data-ttu-id="23ae8-117">캐시 크기를 조정하려면 [Azure Portal](cache-configure.md#configure-redis-cache-settings)에서 [캐시를 찾은](https://portal.azure.com) 다음 **리소스 메뉴**에서 **크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![확장](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="23ae8-119">**가격 책정 계층 선택** 블레이드에서 원하는 가격 책정 계층을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![가격 책정 계층 ][redis-cache-pricing-tier-blade]


<span data-ttu-id="23ae8-121">다른 가격 책정 계층으로 크기를 조정할 수 있지만 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="23ae8-122">높은 가격 책정 계층에서 낮은 가격 책정 계층으로 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="23ae8-123">**프리미엄** 캐시에서 **표준** 또는 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="23ae8-124">**표준** 캐시에서 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="23ae8-125">**기본** 캐시에서 **표준** 캐시로 크기를 조정할 수 있지만 동시에 크기를 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="23ae8-126">다른 크기가 필요한 경우 후속 크기 조정 작업을 통해 원하는 크기로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="23ae8-127">**기본** 캐시에서 바로 **프리미엄** 캐시로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="23ae8-128">크기 조정 작업을 통해 **기본**에서 **표준**으로 확장한 다음, 후속 크기 조정 작업을 통해 **표준**에서 **프리미엄**으로 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="23ae8-129">더 큰 크기에서 **C0(250MB)** 크기로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="23ae8-130">새로운 가격 책정 계층으로 캐시 크기를 조정하는 동안에는 **Scaling(크기 조정 중)** 상태가 **Redis Cache** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![확장][redis-cache-scaling]

<span data-ttu-id="23ae8-132">크기 조정이 완료되면 상태가 **Scaling(크기 조정 중)**에서 **실행 중**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="23ae8-133">크기 조정 작업을 자동화하는 방법</span><span class="sxs-lookup"><span data-stu-id="23ae8-133">How to automate a scaling operation</span></span>
<span data-ttu-id="23ae8-134">Azure Portal에서 캐시 인스턴스의 크기를 조정할 뿐만 아니라 PowerShell cmdlet, Azure CLI를 사용하거나 MAML(Microsoft Azure Management Libraries)을 사용하여 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="23ae8-135">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="23ae8-136">Azure CLI를 사용한 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="23ae8-137">MAML을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="23ae8-138">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-138">Scale using PowerShell</span></span>
<span data-ttu-id="23ae8-139">`Size`, `Sku` 또는 `ShardCount` 속성은 수정할 때 [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet를 사용하여 PowerShell을 통해 Azure Redis Cache 인스턴스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="23ae8-140">다음 예제에서는 `myCache` 라는 캐시를 2.5GB 캐시로 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="23ae8-141">PowerShell을 통한 크기 조정에 대한 자세한 내용은 [Powershell을 사용하여 Redis Cache의 크기 조정](cache-howto-manage-redis-cache-powershell.md#scale)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23ae8-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="23ae8-142">Azure CLI를 사용한 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-142">Scale using Azure CLI</span></span>
<span data-ttu-id="23ae8-143">Azure CLI를 사용하여 Azure Redis Cache 인스턴스 크기를 조정하려면 원하는 크기 조정 작업에 따라 `azure rediscache set` 명령을 호출하고 새 크기, SKU, 또는 클러스터 크기를 포함하는 원하는 구성 변경에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="23ae8-144">Azure CLI을 통한 크기 조정에 대한 자세한 내용은 [기존 Redis Cache의 설정 변경](cache-manage-cli.md#scale)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23ae8-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="23ae8-145">MAML을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="23ae8-145">Scale using MAML</span></span>
<span data-ttu-id="23ae8-146">[MAML(Microsoft Azure Management Libraries)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/)를 사용하여 Azure Redis Cache 인스턴스의 크기를 조정하려면 `IRedisOperations.CreateOrUpdate` 메서드를 호출하고 `RedisProperties.SKU.Capacity`에 대한 새 크기를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="23ae8-147">자세한 내용은 [MAML로 Redis Cache 관리](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23ae8-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="23ae8-148">크기 조정 FAQ</span><span class="sxs-lookup"><span data-stu-id="23ae8-148">Scaling FAQ</span></span>
<span data-ttu-id="23ae8-149">다음 목록에는 Azure Redis Cache 크기 조정에 대해 일반적으로 묻는 질문과 답변이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="23ae8-150">프리미엄 캐시로 확장하거나, 이 캐시를 축소하거나 이 캐시 내에서 크기를 조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="23ae8-151">크기를 조정한 후 내 캐시 이름 또는 액세스 키를 변경해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="23ae8-152">크기 조정은 어떻게 수행되나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="23ae8-153">크기를 조정하는 동안 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="23ae8-154">사용자 지정 데이터베이스 설정이 크기 조정 하는 동안에 영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="23ae8-155">크기를 조정하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="23ae8-156">지원되지 않는 작업</span><span class="sxs-lookup"><span data-stu-id="23ae8-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="23ae8-157">크기 조정은 시간이 얼마나 걸리나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="23ae8-158">크기 조정이 완료되었는지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="23ae8-159">프리미엄 캐시로 확장하거나, 이 캐시를 축소하거나 이 캐시 내에서 크기를 조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="23ae8-160">**프리미엄** 캐시에서 **기본** 또는 **표준** 가격 책정 계층으로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="23ae8-161">하나의 **프리미엄** 캐시 가격 책정 계층에서 다른 프리미엄 캐시 가격 책정 계층으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="23ae8-162">**기본** 캐시에서 바로 **프리미엄** 캐시로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="23ae8-163">먼저 크기 조정 작업을 통해 **기본**에서 **표준**으로 확장한 다음, 후속 크기 조정 작업을 통해 **표준**에서 **프리미엄**으로 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="23ae8-164">**프리미엄** 캐시를 만들 때 클러스터링을 사용하도록 설정했으면 [클러스터 크기를 변경](cache-how-to-premium-clustering.md#cluster-size)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="23ae8-165">클러스터를 사용하지 않고 캐시를 만든 경우 나중에 클러스터링를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="23ae8-166">자세한 내용은 [프리미엄 Azure Redis Cache에 클러스터링을 구성하는 방법](cache-how-to-premium-clustering.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23ae8-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="23ae8-167">크기를 조정한 후 내 캐시 이름 또는 액세스 키를 변경해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="23ae8-168">아니요, 캐시 이름 및 키는 크기 조정 작업을 수행하는 동안 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="23ae8-169">크기 조정은 어떻게 수행되나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-169">How does scaling work?</span></span>
* <span data-ttu-id="23ae8-170">**기본** 캐시 크기를 다른 크기로 조정하는 경우 캐시가 종료되고 새 크기를 사용하여 새 캐시를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="23ae8-171">이 시간 동안에는 캐시를 사용할 수 없으며 캐시의 모든 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="23ae8-172">**기본** 캐시를 **표준** 캐시로 확장하는 경우 복제본 캐시가 프로비전되며 데이터가 주 캐시에서 복제본 캐시로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="23ae8-173">크기를 조정하는 동안 캐시를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="23ae8-174">**표준** 캐시 크기를 다른 크기 또는 **프리미엄** 캐시로 조정하는 경우 복제본 중 하나가 종료되고 새 크기로 다시 프로비전되며 데이터가 전송됩니다. 그런 다음 나머지 복제본이 장애 조치(failover)를 수행한 후 다시 프로비전됩니다. 캐시 노드 중 하나에 오류가 발생하면 수행되는 프로세스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="23ae8-175">크기를 조정하는 동안 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="23ae8-176">**기본** 캐시 크기를 새 크기로 조정하는 경우 모든 데이터가 손실되고 크기 조정 작업을 수행하는 동안 캐시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="23ae8-177">**기본** 캐시를 **표준** 캐시로 확장하는 경우 캐시의 데이터가 일반적으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="23ae8-178">**표준** 캐시가 더 큰 크기나 계층으로 확장되거나, **프리미엄** 캐시가 더 크게 확장되는 경우에는 일반적으로 모든 데이터가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="23ae8-179">**표준** 또는 **프리미엄** 캐시를 더 작게 축소하는 경우, 새로 조정된 크기 대비 캐시에 있는 데이터의 양에 따라 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="23ae8-180">크기를 축소하는 경우 데이터가 손실되면 [allkeys-lru](http://redis.io/topics/lru-cache) 제거 정책을 사용하여 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="23ae8-181">사용자 지정 데이터베이스 설정이 크기 조정 하는 동안에 영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="23ae8-182">일부 가격 책정 계층에는 다른 [데이터베이스 제한](cache-configure.md#databases)이 있으므로 캐시 만들기 중에 `databases` 설정에 대한 사용자 지정 값을 구성했다면 규모 축소를 할 때 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="23ae8-183">현재 계층보다 낮은 `databases` 제한을 가진 가격 책정 계층으로 크기를 조정할 때:</span><span class="sxs-lookup"><span data-stu-id="23ae8-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="23ae8-184">모든 가격 계층에 대해 기본값이 16개인 `databases`을 사용하는 경우 데이터 손실은 전혀 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="23ae8-185">크기 조정하는 계층에 대한 제한내에 포함되는 `databases`의 사용자 지정 수를 사용하는 경우, 이 `databases` 설정은 유지되고 데이터 손실은 전혀 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="23ae8-186">새 계층의 제한을 초과하는 `databases`의 사용자 지정 수를 사용하는 경우, `databases` 설정은 새 계층의 제한까지 낮춰지고 제거된 데이터베이스의 모든 데이터는 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="23ae8-187">현재 계층보다 같거나 높은 `databases` 제한을 가진 가격 책정 계층으로 크기를 조정할 때:`databases` 설정은 유지되고 데이터 손실은 전혀 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="23ae8-188">표준 및 프리미엄 캐시의 가용성에 대한 SLA는 99.9%이나 데이터 손실에 대한 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="23ae8-189">크기를 조정하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="23ae8-190">**표준** 및 **프리미엄** 캐시는 크기 조정 작업을 수행하는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="23ae8-191">**기본** 캐시는 다른 크기로 조정하는 동안 오프라인 상태이지만 **기본**에서 **표준**으로 크기를 조정하는 경우에는 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="23ae8-192">지원되지 않는 작업</span><span class="sxs-lookup"><span data-stu-id="23ae8-192">Operations that are not supported</span></span>
* <span data-ttu-id="23ae8-193">높은 가격 책정 계층에서 낮은 가격 책정 계층으로 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="23ae8-194">**프리미엄** 캐시에서 **표준** 또는 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="23ae8-195">**표준** 캐시에서 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="23ae8-196">**기본** 캐시에서 **표준** 캐시로 크기를 조정할 수 있지만 동시에 크기를 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="23ae8-197">다른 크기가 필요한 경우 후속 크기 조정 작업을 통해 원하는 크기로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="23ae8-198">**기본** 캐시에서 바로 **프리미엄** 캐시로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="23ae8-199">먼저 크기 조정 작업을 통해 **기본**에서 **표준**으로 확장한 다음, 후속 크기 조정 작업을 통해 **표준**에서 **프리미엄**으로 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="23ae8-200">더 큰 크기에서 **C0(250MB)** 크기로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="23ae8-201">크기 조정 작업이 실패하면 서비스는 작업을 되돌리려고 하며 캐시는 원래 크기로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="23ae8-202">크기 조정은 시간이 얼마나 걸리나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-202">How long does scaling take?</span></span>
<span data-ttu-id="23ae8-203">크기 조정은 약 20분이 걸립니다. 캐시에 있는 데이터의 양에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="23ae8-204">크기 조정이 완료되었는지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="23ae8-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="23ae8-205">Azure 포털에서 진행 중인 크기 조정 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="23ae8-206">크기 조정이 완료되면 캐시 상태가 **실행 중**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="23ae8-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



