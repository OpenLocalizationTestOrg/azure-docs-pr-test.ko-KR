---
title: "Azure Advisor 비용 권장 사항 | Microsoft Docs"
description: "Azure Advisor를 사용하여 Azure 배포 비용을 최적화합니다."
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="36bba-103">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="36bba-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="36bba-104">Advisor는 유휴 및 사용 미달 리소스를 식별하여 전체적인 Azure 사용을 최적화하고 줄이는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="36bba-105">Advisor 대시보드의 **비용** 탭에서 비용 관련 권장 지침을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Advisor 비용 탭](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="36bba-107">사용률이 낮은 인스턴스의 크기를 조정하여 가상 컴퓨터 소비 최적화</span><span class="sxs-lookup"><span data-stu-id="36bba-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="36bba-108">특정 응용 프로그램 시나리오에서는 기본적으로 사용률이 낮을 수 있으나 가상 컴퓨터의 크기와 수를 관리하여 비용을 절감할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="36bba-109">Advisor는 14일 동안 가상 컴퓨터 사용량을 모니터링하고 사용률이 낮은 가상 컴퓨터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="36bba-110">4일 이상 CPU 사용률이 5% 이하이고 네트워크 사용량이 7MB 이하인 가상 컴퓨터는 사용률이 낮은 가상 컴퓨터로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="36bba-111">Advisor에는 가상 컴퓨터를 계속 실행할 때의 예상 비용이 표시되므로 해당 가상 컴퓨터를 종료하거나 크기를 조정하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![가상 컴퓨터의 크기를 조정하기 위한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="36bba-113">비용 효율적인 솔루션을 사용하여 여러 SQL Database의 성능 목표 관리</span><span class="sxs-lookup"><span data-stu-id="36bba-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="36bba-114">Advisor는 Elastic Database 풀을 만들 경우 도움이 되는 SQL Server 인스턴스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="36bba-115">Elastic Database 풀은 다양한 사용 패턴을 지닌 여러 데이터베이스에 대한 성능 목표를 관리하기 위한 간단하고 비용 효율적인 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="36bba-116">Azure 탄력적 풀에 대한 자세한 내용은 [Azure 탄력적 풀이란?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bba-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Elastic Database 풀에 대한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="36bba-118">Azure Advisor에서 비용 권장 사항에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="36bba-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="36bba-119">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="36bba-120">왼쪽 창에서 **더 많은 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="36bba-121">서비스 메뉴 창의 **모니터링 및 관리** 아래에서 **Azure Advisor**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="36bba-122">Advisor 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="36bba-123">Advisor 대시보드에서 **비용** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="36bba-124">권장 사항을 받아보려는 구독을 선택하고 **권장 사항 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="36bba-125">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="36bba-126">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="36bba-127">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-127">This is a *one-time operation*.</span></span> <span data-ttu-id="36bba-128">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bba-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36bba-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36bba-129">Next steps</span></span>

<span data-ttu-id="36bba-130">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bba-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="36bba-131">Advisor 소개</span><span class="sxs-lookup"><span data-stu-id="36bba-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="36bba-132">시작</span><span class="sxs-lookup"><span data-stu-id="36bba-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="36bba-133">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="36bba-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="36bba-134">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="36bba-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="36bba-135">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="36bba-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
