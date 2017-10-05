---
title: "OMS를 사용한 논리 앱 실행에 관한 모니터링 및 정보 활용 - Azure Logic Apps | Microsoft Docs"
description: "Log Analytics 및 OMS(Operations Management Suite)를 사용한 논리 앱 실행을 모니터링하여 문제 해결과 진단을 위한 정보 및 더 다양한 디버깅 세부 정보를 활용합니다."
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="8df20-103">OMS(Operations Management Suite) 및 Log Analytics를 사용한 논리 앱 실행에 관한 모니터링 및 정보 활용</span><span class="sxs-lookup"><span data-stu-id="8df20-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="8df20-104">모니터링 및 더 다양한 디버깅 정보를 위해 논리 앱을 만들 때 동시에 Log Analytics를 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="8df20-105">Log Analytics는 OMS(Operations Management Suite) 포털을 통해 논리 앱 실행에 대한 진단 로깅 및 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="8df20-106">논리 앱 관리 솔루션을 OMS에 추가하면 논리 앱 실행 및 상태, 실행 시간, 다시 제출 상태 및 상관 관계 ID와 같은 특정 세부 사항에 관한 집계된 상태를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="8df20-107">이 토픽에서는 논리 앱 실행에 관한 런타임 이벤트 및 데이터를 볼 수 있도록 Log Analytics를 켜거나 논리 앱 관리 솔루션을 OMS에 설치하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="8df20-108">기존 논리 앱을 모니터링하려면 다음 단계에 따라 [진단 로깅을 켜서 논리 앱 런타임 데이터를 OMS에 보냅니다](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="8df20-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="8df20-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="8df20-109">Requirements</span></span>

<span data-ttu-id="8df20-110">시작하기 전에 OMS 작업 영역이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="8df20-111">[OMS 작업 영역을 만드는 방법](../log-analytics/log-analytics-get-started.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="8df20-112">논리 앱을 만들 때 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="8df20-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="8df20-113">[Azure Portal](https://portal.azure.com)에서 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="8df20-114">**새로 만들기** > **엔터프라이즈 통합** > **논리 앱** > **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![논리 앱 만들기](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="8df20-116">**논리 앱 만들기** 페이지에서 표시된 것처럼 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="8df20-117">논리 앱의 이름을 입력하고 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="8df20-118">Azure 리소스 그룹을 만들거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="8df20-119">**Log Analytics**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="8df20-120">논리 앱 실행에 대한 데이터를 보내려는 OMS 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="8df20-121">준비가 되면 **대시보드에 고정** > **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![논리 앱 만들기](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="8df20-123">이 단계를 마치면 Azure에서 OMS 작업 영역에 연결된 논리 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="8df20-124">또한 이 단계에서 OMS 작업 영역에 논리 앱 관리 솔루션이 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="8df20-125">OMS에서 논리 앱 실행을 보려면 [다음 단계로 계속 진행합니다](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="8df20-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="8df20-126">OMS에서 논리 앱 관리 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="8df20-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="8df20-127">사용자의 논리 앱을 만들 때 이미 Log Analytics를 켰으면 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="8df20-128">OMS에 논리 앱 관리 솔루션이 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="8df20-129">[Azure Portal](https://portal.azure.com)에서 **더 많은 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="8df20-130">필터로 “로그 분석”을 검색하고 다음과 같이 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   !["Log Analytics" 선택](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="8df20-132">**Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS 작업 영역 선택](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="8df20-134">**관리** 아래에서 **OMS 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-134">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS 포털" 선택](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="8df20-136">OMS 홈페이지에서 업그레이드 배너가 표시되는 경우 OMS 작업 영역을 먼저 업그레이드하도록 배너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="8df20-137">그런 다음 **솔루션 갤러리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-137">Then choose **Solutions Gallery**.</span></span>

   ![“솔루션 갤러리” 선택](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="8df20-139">**모든 솔루션**에서 **논리 앱 관리** 솔루션에 대한 타일을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![“논리 앱 관리” 선택](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="8df20-141">OMS 작업 영역에 솔루션을 설치하려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![“논리 앱 관리”에 “추가” 선택](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="8df20-143">OMS 작업 영역에서 논리 앱 실행 보기</span><span class="sxs-lookup"><span data-stu-id="8df20-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="8df20-144">논리 앱 실행에 대한 횟수 및 상태를 확인하려면 OMS 작업 영역에 대한 개요 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="8df20-145">**논리 앱 관리** 타일에서 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![논리 앱 실행 횟수 및 상태를 보여 주는 개요 타일](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="8df20-147">이 업그레이드 배너가 Logic Apps 관리 타일 대신 표시되는 경우 OMS 작업 영역을 먼저 업그레이드하도록 배너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > !["OMS 작업 영역" 업그레이드](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="8df20-149">논리 앱 실행에 관한 더 많은 정보를 포함한 요약을 보려면 **논리 앱 관리** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="8df20-150">여기에서 논리 앱 실행은 이름이나 실행 상태로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![논리 앱 실행에 대한 상태 요약](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="8df20-152">특정 논리 앱 또는 상태에 대한 모든 실행을 보려면 논리 앱 또는 상태에 대한 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="8df20-153">특정 논리 앱에 대한 모든 실행을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![논리 앱 또는 상태에 대한 실행 보기](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="8df20-155">**다시 제출** 열은 다시 제출된 실행에서 발생한 실행에 대해 “예”를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="8df20-156">이러한 결과를 필터링하기 위해 클라이언트와 서버 쪽 필터링을 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="8df20-157">클라이언트 쪽 필터: 각 열에 대해 원하는 필터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="8df20-158">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-158">Here are some examples:</span></span>

     ![예제 열 필터](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="8df20-160">서버 쪽 필터: 특정 시간 창을 선택하거나 표시되는 실행 횟수를 제한하려면 페이지 맨 위에 있는 범위 컨트롤을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="8df20-161">기본적으로 1,000개 레코드가 한 번에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![시간 변경 창](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="8df20-163">특정 실행에 대한 모든 작업 및 세부 정보를 보려면 행을 선택하여 로그 검색 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="8df20-164">이 정보를 테이블로 보려면 **테이블**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="8df20-165">검색 창에서 쿼리 문자열을 편집하여 쿼리를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="8df20-166">향상된 경험을 위해 **고급 분석**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![논리 앱 실행에 대한 작업 및 세부 정보 보기](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="8df20-168">여기 Azure Log Analytics 페이지에서 쿼리를 업데이트하고 테이블의 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="8df20-169">이 쿼리는 [Kusto 쿼리 언어](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html)를 사용하여 서로 다른 결과를 보려는 경우 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df20-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics - 쿼리 뷰](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="8df20-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8df20-171">Next steps</span></span>

* [<span data-ttu-id="8df20-172">B2B 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="8df20-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
