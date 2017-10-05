---
title: "Azure Advisor 성능 권장 사항 | Microsoft Docs"
description: "Advisor를 사용하여 Azure 배포 성능을 최적화합니다."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="09ad4-103">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="09ad4-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="09ad4-104">Azure Advisor 성능 권장 사항은 업무에 중요한 응용 프로그램의 속도 및 응답성을 향상시키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="09ad4-105">Advisor 대시보드의 **성능** 탭에서 Advisor를 사용하여 성능 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Advisor 성능 탭](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="09ad4-107">SQL DB Advisor로 데이터베이스 성능 개선</span><span class="sxs-lookup"><span data-stu-id="09ad4-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="09ad4-108">Advisor는 모든 Azure 리소스에 대한 권장 사항을 일관되고 통합된 보기로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="09ad4-109">SQL Database Azure와 통합되므로 SQL Azure Database의 성능을 향상시키기 위한 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="09ad4-110">SQL Database Advisor는 사용 기록을 분석하여 SQL Azure Database의 성능을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="09ad4-111">그런 후 데이터베이스의 일반적인 워크로드를 실행하는 데 가장 적합한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="09ad4-112">권장 사항을 가져오려면 데이터베이스에 일주일의 사용 기간이 필요하고, 그 기간 내에 일관된 활동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="09ad4-113">SQL Database Advisor는 일관성 있는 쿼리 패턴을 임의 활동 버스트보다 더욱 쉽게 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="09ad4-114">SQL Database Advisor에 대한 자세한 내용은 [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ad4-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL Database 권장 사항](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="09ad4-116">Redis Cache 성능 및 안정성 향상</span><span class="sxs-lookup"><span data-stu-id="09ad4-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="09ad4-117">Advisor는 높은 메모리 사용량, 서버 부하, 네트워크 대역폭 또는 많은 수의 클라이언트 연결이 성능이 부정적인 영향을 미칠 수 있는 Redis Cache 인스턴스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="09ad4-118">또한 Advisor는 잠재적인 문제를 방지하는 데 도움이 되는 모범 사례 권장 사항도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="09ad4-119">Redis Cache 권장 사항에 대한 자세한 내용은 [r](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ad4-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="09ad4-120">App Service 성능 및 안정성 향상</span><span class="sxs-lookup"><span data-stu-id="09ad4-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="09ad4-121">Azure Advisor는 App Services 환경을 개선하고 관련 플랫폼 기능을 검색하기 위한 모범 사례 권장 사항을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="09ad4-122">App Services 권장 사항 예제:</span><span class="sxs-lookup"><span data-stu-id="09ad4-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="09ad4-123">완화 옵션을 사용하여 메모리나 CPU 리소스가 앱 런타임에서 소모되는 인스턴스 검색</span><span class="sxs-lookup"><span data-stu-id="09ad4-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="09ad4-124">Web Apps 및 데이터베이스를 함께 배치할 때 성능을 향상시키고 비용을 절감할 수 있는 인스턴스 검색</span><span class="sxs-lookup"><span data-stu-id="09ad4-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="09ad4-125">App Services 권장 사항에 대한 자세한 내용은 [Azure App Service에 대한 모범 사례](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ad4-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="09ad4-126">![App Services 권장 사항](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="09ad4-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="09ad4-127">Advisor에서 성능 권장 사항에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="09ad4-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="09ad4-128">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="09ad4-129">왼쪽 창에서 **더 많은 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="09ad4-130">서비스 메뉴 창의 **모니터링 및 관리** 아래에서 **Azure Advisor**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="09ad4-131">Advisor 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="09ad4-132">Advisor 대시보드에서 **성능** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="09ad4-133">권장 사항을 받아보려는 구독을 선택하고 **권장 사항 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="09ad4-134">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="09ad4-135">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="09ad4-136">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-136">This is a *one-time operation*.</span></span> <span data-ttu-id="09ad4-137">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ad4-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09ad4-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09ad4-138">Next steps</span></span>

<span data-ttu-id="09ad4-139">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09ad4-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="09ad4-140">Advisor 소개</span><span class="sxs-lookup"><span data-stu-id="09ad4-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="09ad4-141">Advisor 시작</span><span class="sxs-lookup"><span data-stu-id="09ad4-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="09ad4-142">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="09ad4-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="09ad4-143">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="09ad4-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="09ad4-144">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="09ad4-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

