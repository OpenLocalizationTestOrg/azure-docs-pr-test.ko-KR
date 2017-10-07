---
title: "Azure 관리자와 함께 aaaGet 시작 | Microsoft Docs"
description: "Azure Adviser를 시작합니다."
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: 30fc8b8f3823f6f047e46cb9000189f3ccb3d514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="3cf0b-103">Azure Adviser 시작</span><span class="sxs-lookup"><span data-stu-id="3cf0b-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="3cf0b-104">Get 권장 사항 hello Azure 포털을 통해 tooaccess 관리자 권장 구성을 구현 하는 방법에 대해 알아봅니다 권장 사항 및 권장 사항 새로 고침에 대 한를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-104">Learn how tooaccess Advisor through hello Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="3cf0b-105">Advisor 권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="3cf0b-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="3cf0b-106">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3cf0b-107">Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-107">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="3cf0b-108">Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-108">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="3cf0b-109">hello 관리자 대시보드 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-109">hello Advisor dashboard is displayed.</span></span>

   ![Hello Azure 포털을 사용 하 여 Azure Advisor 액세스](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="3cf0b-111">Hello 관리자 대시보드에서 tooreceive 권장 사항을 보려는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-111">On hello Advisor dashboard, select hello subscription for which you want tooreceive recommendations.</span></span>  
<span data-ttu-id="3cf0b-112">hello 관리자 대시보드에 선택한 구독에 대 한 개인 설정 된 권장 사항 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-112">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="3cf0b-113">특정 범주에 대 한 권장 사항을 tooget hello 탭 중 하나를 클릭 합니다.: **고가용성**, **보안**, **성능**, 또는 **비용**.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-113">tooget recommendations for a particular category, click one of hello tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="3cf0b-114">관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-114">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="3cf0b-115">구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-115">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="3cf0b-116">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-116">This is a *one-time operation*.</span></span> <span data-ttu-id="3cf0b-117">Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-117">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Advisor 대시보드](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="3cf0b-119">자세한 Advisor 권장 사항 가져오기 및 솔루션 구현</span><span class="sxs-lookup"><span data-stu-id="3cf0b-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="3cf0b-120">hello **권장** Advisor에 블레이드 hello 권장 사항에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-120">hello **Recommendation** blade in Advisor offers additional information about hello recommendation.</span></span> 

1. <span data-ttu-id="3cf0b-121">Toohello 로그인 [Azure 포털](https://portal.azure.com), 한 다음 시작 [Azure 관리자](https://aka.ms/azureadvisordashboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-121">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3cf0b-122">Hello에 **관리자 권장 구성을** 대시보드를 클릭 하 여 **위한 권장 사항 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-122">On hello **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="3cf0b-123">Hello 권장 사항 목록에서 자세히 tooreview 원하는 권장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-123">In hello list of recommendations, click a recommendation that you want tooreview in detail.</span></span>  
<span data-ttu-id="3cf0b-124">hello **권장** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-124">hello **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="3cf0b-125">Hello에 **권장 사항을** 블레이드에서 수행할 tooresolve 잠재적인 문제 또는 비용 절감 영업 기회를 활용 하기 위해 수 있는 동작에 대 한 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-125">On hello **Recommendations** blade, review information about actions that you can perform tooresolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![hello 관리자 권장 구성 블레이드](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="3cf0b-127">Advisor 권장 사항 검색</span><span class="sxs-lookup"><span data-stu-id="3cf0b-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="3cf0b-128">특정 구독 또는 리소스 그룹에 대한 권장 사항을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="3cf0b-129">또한 권장 사항을 상태별로 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="3cf0b-130">Toohello 로그인 [Azure 포털](https://portal.azure.com), 한 다음 시작 [Azure 관리자](https://aka.ms/azureadvisordashboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-130">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3cf0b-131">구독, 리소스 그룹 및 권장 사항 상태(**활성** 또는 **다시 알림**)를 필터링하여 권장 사항을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="3cf0b-132">toodisplay 관리자의 권장 구성 기반으로 하는 목록 검색 필터 조건을 클릭 **위한 권장 사항 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-132">toodisplay a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Advisor 검색 필터 조건](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="3cf0b-134">Advisor 권장 사항 다시 알림 또는 해제</span><span class="sxs-lookup"><span data-stu-id="3cf0b-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="3cf0b-135">Toohello 로그인 [Azure 포털](https://portal.azure.com), 한 다음 시작 [Azure 관리자](https://aka.ms/azureadvisordashboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-135">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3cf0b-136">클릭 **위한 권장 사항 보기**, 권장 사항 hello 목록에서 권장 구성을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-136">Click **Get recommendations**, and then, in hello list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="3cf0b-137">Hello에 **권장** 블레이드에서 클릭 **다시 알림**합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-137">On hello **Recommendation** blade, click **Snooze**.</span></span>  

   ![Advisor 권장 사항 작업 예제](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="3cf0b-139">알림을 기간을 지정 하거나 선택 **Never** toodismiss hello 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-139">Specify a snooze time period, or select **Never** toodismiss hello recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3cf0b-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cf0b-140">Next steps</span></span>

<span data-ttu-id="3cf0b-141">toolearn 관리자에 대 한 자세한 정보를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3cf0b-141">toolearn more about Advisor, see:</span></span>
* [<span data-ttu-id="3cf0b-142">소개 tooAzure 관리자</span><span class="sxs-lookup"><span data-stu-id="3cf0b-142">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="3cf0b-143">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3cf0b-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="3cf0b-144">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3cf0b-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="3cf0b-145">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3cf0b-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="3cf0b-146">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3cf0b-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
