---
title: "aaaAzure Advisor 비용 권장 사항을 | Microsoft Docs"
description: "Azure 배포의 Azure 관리자 toooptimize hello 비용을 사용 합니다."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="56286-103">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="56286-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="56286-104">Advisor는 유휴 및 사용 미달 리소스를 식별하여 전체적인 Azure 사용을 최적화하고 줄이는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56286-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="56286-105">Hello에서 권장 사항이 비용 얻을 수 있습니다 **비용** hello 관리자 대시보드에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Advisor 비용 탭](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="56286-107">사용률이 낮은 인스턴스의 크기를 조정하여 가상 컴퓨터 소비 최적화</span><span class="sxs-lookup"><span data-stu-id="56286-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="56286-108">특정 응용 프로그램 시나리오가 발생할 수도 있지만 사용률이 낮은의 설계, hello 크기와 수의 가상 컴퓨터를 관리 하 여 종종 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56286-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="56286-109">Advisor는 14일 동안 가상 컴퓨터 사용량을 모니터링하고 사용률이 낮은 가상 컴퓨터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="56286-110">4일 이상 CPU 사용률이 5% 이하이고 네트워크 사용량이 7MB 이하인 가상 컴퓨터는 사용률이 낮은 가상 컴퓨터로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="56286-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="56286-111">Advisor tooshut 아래쪽 또는 크기를 조정할를 선택할 수 있도록 계속 toorun 가상 컴퓨터의 예상된 비용을 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56286-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![가상 컴퓨터의 크기를 조정하기 위한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="56286-113">여러 SQL 데이터베이스의 비용 효율적인 솔루션 toomanage 성능 목표를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="56286-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="56286-114">Advisor는 Elastic Database 풀을 만들 경우 도움이 되는 SQL Server 인스턴스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="56286-115">탄력적 데이터베이스 풀 사용 패턴을 다양 한 여러 데이터베이스의 성능 목표 hello 간단 하 고 비용 효율적인 솔루션 toomanage를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="56286-116">Azure 탄력적 풀에 대한 자세한 내용은 [Azure 탄력적 풀이란?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56286-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Elastic Database 풀에 대한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="56286-118">Tooaccess는 Azure 관리자의 권장 사항을 비용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="56286-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="56286-119">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="56286-120">Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="56286-121">Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="56286-122">hello 관리자 대시보드 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56286-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="56286-123">Hello 관리자 대시보드에서 hello 클릭 **비용** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="56286-124">Hello 구독 원하는 tooreceive 권장 사항를 클릭 한 다음 선택 **위한 권장 사항 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="56286-125">관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="56286-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="56286-126">구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="56286-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="56286-127">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56286-127">This is a *one-time operation*.</span></span> <span data-ttu-id="56286-128">Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="56286-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56286-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56286-129">Next steps</span></span>

<span data-ttu-id="56286-130">toolearn 관리자 권장 사항에 대해 자세히 알아보려면</span><span class="sxs-lookup"><span data-stu-id="56286-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="56286-131">소개 tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="56286-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="56286-132">시작</span><span class="sxs-lookup"><span data-stu-id="56286-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="56286-133">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="56286-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="56286-134">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="56286-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="56286-135">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="56286-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
