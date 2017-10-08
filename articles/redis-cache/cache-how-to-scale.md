---
title: Azure Redis Cache aaaHow tooScale | Microsoft Docs
description: "자세한 방법을 tooscale Azure Redis 캐시 인스턴스"
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
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="f590c-103">Azure Redis 캐시 하는 tooScale 방법</span><span class="sxs-lookup"><span data-stu-id="f590c-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="f590c-104">Azure Redis 캐시 캐시 크기 및 기능의 hello 선택에 유연성을 제공 하는 다른 캐시 기능에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="f590c-105">캐시를 만든 후에 hello 크기와 hello 응용 프로그램의 hello 요구 사항을 변경 하는 경우의 가격 책정 hello 캐시의 계층을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="f590c-106">이 문서에서는 어떻게 tooscale hello Azure 포털을 사용 하 여 캐시는 Azure PowerShell 및 Azure CLI 등을 도구를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="f590c-107">때 tooscale</span><span class="sxs-lookup"><span data-stu-id="f590c-107">When tooscale</span></span>
<span data-ttu-id="f590c-108">Hello를 사용할 수 있습니다 [모니터링](cache-how-to-monitor.md) 의 Azure Redis Cache toomonitor 캐시의 상태와 성능을 hello 기능과 tooscale 캐시 hello 하는 시기를 결정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="f590c-109">모니터링 수 hello 다음 메트릭을 toohelp tooscale 해야 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="f590c-110">Redis 서버 부하</span><span class="sxs-lookup"><span data-stu-id="f590c-110">Redis Server Load</span></span>
* <span data-ttu-id="f590c-111">메모리 사용량</span><span class="sxs-lookup"><span data-stu-id="f590c-111">Memory Usage</span></span>
* <span data-ttu-id="f590c-112">네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="f590c-112">Network Bandwidth</span></span>
* <span data-ttu-id="f590c-113">CPU 사용량</span><span class="sxs-lookup"><span data-stu-id="f590c-113">CPU Usage</span></span>

<span data-ttu-id="f590c-114">캐시를 응용 프로그램의 요구 사항을 만족 더 이상을 발견할 경우 가격 책정 계층 응용 프로그램에 대 한 적합 한 tooa 더 크거나 작게 캐시를 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="f590c-115">가격 책정 계층 toouse를 캐시 하 결정에 대 한 자세한 내용은 참조 하십시오. [어떤 Redis 캐시 기능 및 크기 사용 해야 합니까](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="f590c-116">캐시 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-116">Scale a cache</span></span>
<span data-ttu-id="f590c-117">tooscale 캐시 [toohello 캐시 찾아보기](cache-configure.md#configure-redis-cache-settings) hello에 [Azure 포털](https://portal.azure.com) 클릭 **배율** hello에서 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![확장](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="f590c-119">Select hello hello에서 가격 책정 계층을 원하는 **가격 책정 계층 선택** 블레이드에 대 한 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![가격 책정 계층 ][redis-cache-pricing-tier-blade]


<span data-ttu-id="f590c-121">Tooa 다른 제한 사항에 따라 hello로 가격 책정 계층을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="f590c-122">더 높은 가격 책정 계층 tooa 더 낮은 가격 책정 계층에서에서 확장할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="f590c-123">업그레이드할 수 없는 **프리미엄** tooa 아래로 캐시 **표준** 또는 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="f590c-124">업그레이드할 수 없는 **표준** tooa 아래로 캐시 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="f590c-125">확장할 수는 **기본** tooa 캐시 **표준** 캐시 있지만 hello hello 크기를 변경할 수 없습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="f590c-126">크기를 다르게 해야 할 경우에 크기 조정 작업의 후속 toohello 원하는 크기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="f590c-127">업그레이드할 수 없는 **기본** 캐시 직접 tooa **프리미엄** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="f590c-128">확장 해야 **기본** 너무**표준** 한 크기 조정 작업에서 **표준** 너무**프리미엄** 후속 배율 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="f590c-129">toohello 아래로 더 큰 크기를 확장할 수 없으며 **C0 (250MB)** 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="f590c-130">Hello 캐시 toohello 새로운 가격 책정 계층, 크기를 조정 하는 동안 한 **배율** hello에 상태가 표시 되 **Redis Cache** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![확장][redis-cache-scaling]

<span data-ttu-id="f590c-132">크기 조정을 완료 되 면 hello 상태에서 변경 **배율** 너무**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="f590c-133">어떻게 tooautomate 크기 조정 작업</span><span class="sxs-lookup"><span data-stu-id="f590c-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="f590c-134">또한 tooscaling에서에서 캐시 인스턴스에 hello Azure 포털, Azure CLI, PowerShell cmdlet을 사용 하 여 크기를 조정 하 고 사용 하 여 Microsoft Azure 관리 라이브러리 (MAML) hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="f590c-135">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="f590c-136">Azure CLI를 사용한 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="f590c-137">MAML을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="f590c-138">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-138">Scale using PowerShell</span></span>
<span data-ttu-id="f590c-139">Hello를 사용 하 여 PowerShell과 함께 Azure Redis 캐시 인스턴스를 확장할 수 있습니다 [집합 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet 때 hello `Size`, `Sku`, 또는 `ShardCount` 속성이 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="f590c-140">hello 다음 예제에서는 어떻게 tooscale 캐시 라는 `myCache` tooa 2.5 g B 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="f590c-141">PowerShell과 함께 확장에 대 한 자세한 내용은 참조 하십시오. [tooscale Redis는 Powershell을 사용 하 여 캐시](cache-howto-manage-redis-cache-powershell.md#scale)합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="f590c-142">Azure CLI를 사용한 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-142">Scale using Azure CLI</span></span>
<span data-ttu-id="f590c-143">tooscale Azure CLI를 사용 하 여 Azure Redis 캐시 인스턴스 호출 hello `azure rediscache set` 명령과 패스에 새 크기, sku 또는 hello에 따라 클러스터 크기를 포함 하는 hello 필요한 구성 변경 내용 원하는 크기 조정 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="f590c-144">Azure CLI을 통한 크기 조정에 대한 자세한 내용은 [기존 Redis Cache의 설정 변경](cache-manage-cli.md#scale)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f590c-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="f590c-145">MAML을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f590c-145">Scale using MAML</span></span>
<span data-ttu-id="f590c-146">tooscale hello를 사용 하 여 Azure Redis 캐시 인스턴스 [Microsoft Azure 관리 라이브러리 (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), 호출 hello `IRedisOperations.CreateOrUpdate` 메서드와 hello hello에 대 한 새 크기를 전달 `RedisProperties.SKU.Capacity`합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="f590c-147">자세한 내용은 참조 hello [관리 Redis Cache MAML를 사용 하 여](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 샘플.</span><span class="sxs-lookup"><span data-stu-id="f590c-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="f590c-148">크기 조정 FAQ</span><span class="sxs-lookup"><span data-stu-id="f590c-148">Scaling FAQ</span></span>
<span data-ttu-id="f590c-149">hello 다음 목록에 포함 되어 Azure Redis 캐시 크기 조정에 대 한 질문과 대답 toocommonly 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="f590c-150">프리미엄 캐시로 확장하거나, 이 캐시를 축소하거나 이 캐시 내에서 크기를 조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="f590c-151">크기 조정 후 용량은 toochange 내 캐시 이름 또는 액세스 키</span><span class="sxs-lookup"><span data-stu-id="f590c-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="f590c-152">크기 조정은 어떻게 수행되나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="f590c-153">크기를 조정하는 동안 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="f590c-154">사용자 지정 데이터베이스 설정이 크기 조정 하는 동안에 영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="f590c-155">크기를 조정하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="f590c-156">지원되지 않는 작업</span><span class="sxs-lookup"><span data-stu-id="f590c-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="f590c-157">크기 조정은 시간이 얼마나 걸리나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="f590c-158">크기 조정이 완료되었는지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="f590c-159">프리미엄 캐시로 확장하거나, 이 캐시를 축소하거나 이 캐시 내에서 크기를 조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="f590c-160">업그레이드할 수 없는 **프리미엄** tooa 아래로 캐시 **기본** 또는 **표준** 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="f590c-161">하나를 확장할 수 **프리미엄** 가격 계층 tooanother 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="f590c-162">업그레이드할 수 없는 **기본** 캐시 직접 tooa **프리미엄** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="f590c-163">먼저에서 확장 해야 **기본** 너무**표준** 한 크기 조정 작업에서 **표준** 너무**프리미엄** 후속에서 크기 조정 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="f590c-164">클러스터링을 사용 하는 경우 만들 때 프로그램 **프리미엄** 수 캐시 [hello 클러스터 크기 변경](cache-how-to-premium-clustering.md#cluster-size)합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="f590c-165">클러스터를 사용하지 않고 캐시를 만든 경우 나중에 클러스터링를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="f590c-166">자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](cache-how-to-premium-clustering.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="f590c-167">크기 조정 후 용량은 toochange 내 캐시 이름 또는 액세스 키</span><span class="sxs-lookup"><span data-stu-id="f590c-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="f590c-168">아니요, 캐시 이름 및 키는 크기 조정 작업을 수행하는 동안 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="f590c-169">크기 조정은 어떻게 수행되나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-169">How does scaling work?</span></span>
* <span data-ttu-id="f590c-170">경우는 **기본** 캐시 크기가 조정 되 tooa 크기가 다양할 종료 되 고 hello 새 크기를 사용 하 여 새 캐시가 프로비저닝되 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="f590c-171">이 시간 동안 hello 캐시를 사용할 수 없어서 hello 캐시의 모든 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="f590c-172">경우는 **기본** 캐시는 크기 조정 된 tooa **표준** 캐시 복제본 캐시를 프로 비전 및 hello 데이터가 hello 기본 캐시 toohello 복제본 캐시에서 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="f590c-173">hello 캐시 남아 hello 프로세스를 확장 하는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="f590c-174">경우는 **표준** 캐시는 다른 크기 조정 된 tooa 크기나 tooa **프리미엄** 캐시 hello 복제본 중 하나가 종료 되 고 다시 이전할 새 크기와 hello 데이터 toohello와 다른 hello를 프로 비전 복제본이 다시 프로 비전 하기 전에 장애 조치, 동안 hello 캐시 노드 중 하나에 오류가 발생 하는 비슷한 toohello 프로세스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="f590c-175">크기를 조정하는 동안 캐시의 데이터가 손실되나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="f590c-176">경우는 **기본** 캐시 크기 조정 된 tooa 새 크기를 모든 데이터는 손실 되며 hello 크기 조정 작업 중 hello 캐시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="f590c-177">경우는 **기본** 캐시는 크기 조정 된 tooa **표준** 캐시, hello hello 캐시 데이터에에서 일반적으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="f590c-178">때는 **표준** 캐시 크기 조정 된 tooa 더 큰 크기 인지, 계층 또는 **프리미엄** 캐시 크기가 조정 되 tooa 더 큰 크기를 모든 데이터는 일반적으로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="f590c-179">크기 조정 하는 경우는 **표준** 또는 **프리미엄** 아래로 tooa 더 작은 크기를 데이터 캐시 hello 캐시에 얼마나 많은 데이터가 있는지에 따라 손실 될 수 있습니다 크기가 조정 되는 경우 toohello 새 크기와 관련 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="f590c-180">키 hello를 사용 하 여 제거 된 데이터를 잃어버린 경우 줄일 때는 [allkeys lru](http://redis.io/topics/lru-cache) 의 제거 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="f590c-181">사용자 지정 데이터베이스 설정이 크기 조정 하는 동안에 영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="f590c-182">일부 가격 책정 계층에는 다른 [제한 데이터베이스](cache-configure.md#databases)이므로 구성 된 hello에 대 한 사용자 지정 값을 아래로 확장 하는 경우는 몇 가지 고려 사항이 `databases` 캐시 만들기 중에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="f590c-183">가격 책정 계층 낮은 tooa 경우 배율 `databases` hello 현재 계층 보다 제한:</span><span class="sxs-lookup"><span data-stu-id="f590c-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="f590c-184">Hello 기본 개수를 사용 하는 경우 `databases` 모든 가격 책정 계층에 대 한 16 인 데이터는 손실 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="f590c-185">사용자 지정 된 수를 사용 하는 경우 `databases` hello 계층 toowhich 조정할 수에 대 한 hello 제한 내에 있게 하는이 `databases` 설정은 그대로 유지 하 고 어떤 데이터도 손실 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="f590c-186">사용자 지정 된 수를 사용 하는 경우 `databases` 하는 hello 제한을 초과 hello 새 계층의 hello `databases` 설정은 hello 새 계층의 toohello 낮아진된 제한 되며 제거 hello 데이터베이스의 모든 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="f590c-187">경우 동일 하거나 더 높은 hello로 가격대 tooa 크기 조정 `databases` hello 현재 계층 보다 프로그램 `databases` 설정은 그대로 유지 하 고 어떤 데이터도 손실 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="f590c-188">표준 및 프리미엄 캐시의 가용성에 대한 SLA는 99.9%이나 데이터 손실에 대한 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="f590c-189">크기를 조정하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="f590c-190">**표준** 및 **프리미엄** 크기 조정 작업이 hello 캐시 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="f590c-191">**기본** 캐시는 작업 tooa 다른 크기, 하는 동안 오프 라인 상태 이지만에서 확장 하는 경우 계속 사용할 수 **기본** 너무**표준**합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="f590c-192">지원되지 않는 작업</span><span class="sxs-lookup"><span data-stu-id="f590c-192">Operations that are not supported</span></span>
* <span data-ttu-id="f590c-193">더 높은 가격 책정 계층 tooa 더 낮은 가격 책정 계층에서에서 확장할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="f590c-194">업그레이드할 수 없는 **프리미엄** tooa 아래로 캐시 **표준** 또는 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="f590c-195">업그레이드할 수 없는 **표준** tooa 아래로 캐시 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="f590c-196">확장할 수는 **기본** tooa 캐시 **표준** 캐시 있지만 hello hello 크기를 변경할 수 없습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="f590c-197">크기를 다르게 해야 할 경우에 크기 조정 작업의 후속 toohello 원하는 크기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="f590c-198">업그레이드할 수 없는 **기본** 캐시 직접 tooa **프리미엄** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="f590c-199">먼저에서 확장 해야 **기본** 너무**표준** 한 크기 조정 작업에서 **표준** 너무**프리미엄** 후속에서 크기 조정 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="f590c-200">toohello 아래로 더 큰 크기를 확장할 수 없으며 **C0 (250MB)** 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="f590c-201">크기 조정 작업이 실패 하면 hello 서비스가 작업 toorevert hello 작업을 시도 및 hello 캐시 toohello 원래 크기 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="f590c-202">크기 조정은 시간이 얼마나 걸리나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-202">How long does scaling take?</span></span>
<span data-ttu-id="f590c-203">약 20 분 hello 캐시에 얼마나 많은 데이터가 있는지에 따라 하나를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="f590c-204">크기 조정이 완료되었는지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f590c-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="f590c-205">Hello Azure 포털에서에서 크기 조정 작업이 진행 중에서 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="f590c-206">크기 조정을 완료 되 면 hello hello 캐시 변경의 상태 너무**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f590c-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



