---
title: "논리 앱에 대 한 통찰력을 aaaMonitor 및 get OMS-Azure 논리 앱을 사용 하 여 실행 | Microsoft Docs"
description: "논리 응용 프로그램이 실행 되 로그 분석 및 Operations Management Suite (OMS) tooget insights 및 문제 해결 및 진단에 대 한 보다 풍부한 디버깅 세부 정보로 모니터링"
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
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="60d66-103">OMS(Operations Management Suite) 및 Log Analytics를 사용한 논리 앱 실행에 관한 모니터링 및 정보 활용</span><span class="sxs-lookup"><span data-stu-id="60d66-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="60d66-104">모니터링 및 다양 한 디버깅 정보에 대 한 켤 수 있습니다 로그 분석 hello에서 논리 앱을 만들 때 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="60d66-105">로그 분석 hello Operations Management Suite (OMS) 포털을 통해 실행 되는 진단 로깅 및 논리 앱에 대 한 모니터링을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="60d66-106">논리 앱 관리 솔루션 tooOMS hello를 추가한 경우에 논리가 응용 프로그램 실행 및 상태, 실행 시간, 다시 전송 상태 및 상관 관계 Id와 같은 특정 세부 정보에 대 한 집계 된 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="60d66-107">이 항목에서는 런타임 이벤트를 볼 수 있으며 논리 앱에 대 한 데이터를 실행 하므로 OMS에서 논리 앱 관리 솔루션 hello tooturn 로그 분석 또는 설치에는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="60d66-108">toomonitor 기존 논리 앱이 너무 다음이 단계를 수행 [진단 로깅을 켜고 논리가 응용 프로그램 런타임 데이터 tooOMS 보낼](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="60d66-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="60d66-109">Requirements</span></span>

<span data-ttu-id="60d66-110">시작 하기 전에 toohave OMS 작업 영역 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="60d66-111">자세한 내용은 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="60d66-112">논리 앱을 만들 때 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="60d66-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="60d66-113">[Azure Portal](https://portal.azure.com)에서 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="60d66-114">**새로 만들기** > **엔터프라이즈 통합** > **논리 앱** > **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![논리 앱 만들기](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="60d66-116">Hello에 **만들기 논리 앱** 페이지에서 표시 된 것 처럼 이러한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="60d66-117">논리 앱의 이름을 입력하고 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="60d66-118">Azure 리소스 그룹을 만들거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="60d66-119">설정 **로그 분석** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="60d66-120">너무 논리 앱에 대 한 데이터를 전송 하려는 선택 hello OMS 작업 영역을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="60d66-121">준비 되 면 선택 **Pin toodashboard** > **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![논리 앱 만들기](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="60d66-123">이 단계를 마치면 Azure에서 OMS 작업 영역에 연결된 논리 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="60d66-124">또한이 단계는 자동으로 OMS 작업 영역에서 hello 논리 앱 관리 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="60d66-125">OMS에서 논리 앱이 실행 tooview [다음이 단계를 계속](#view-logic-app-runs-oms)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="60d66-126">OMS의 hello 논리 앱 관리 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="60d66-127">사용자의 논리 앱을 만들 때 이미 Log Analytics를 켰으면 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="60d66-128">Hello 논리 앱 관리 솔루션을 OMS에 설치 된 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="60d66-129">Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="60d66-130">필터로 “로그 분석”을 검색하고 다음과 같이 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   !["Log Analytics" 선택](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="60d66-132">**Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS 작업 영역 선택](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="60d66-134">**관리** 아래에서 **OMS 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-134">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS 포털" 선택](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="60d66-136">OMS 홈 페이지에 업그레이드 배너 hello 나타나면 선택 hello 배너 OMS 작업 영역을 먼저 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="60d66-137">그런 다음 **솔루션 갤러리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-137">Then choose **Solutions Gallery**.</span></span>

   ![“솔루션 갤러리” 선택](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="60d66-139">아래 **모든 솔루션**찾아 hello에 대 한 hello 타일 선택 **논리 앱 관리** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![“논리 앱 관리” 선택](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="60d66-141">OMS 작업 영역에서 tooinstall hello 솔루션 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![“논리 앱 관리”에 “추가” 선택](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="60d66-143">OMS 작업 영역에서 논리 앱 실행 보기</span><span class="sxs-lookup"><span data-stu-id="60d66-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="60d66-144">tooview hello 개수 및 논리 앱에 대 한 상태 실행 되므로 OMS 작업 영역에 대 한 이동 toohello 개요 페이지.</span><span class="sxs-lookup"><span data-stu-id="60d66-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="60d66-145">Hello에 hello 세부 정보를 검토 **논리 앱 관리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![논리 앱 실행 횟수 및 상태를 보여 주는 개요 타일](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="60d66-147">이 업그레이드 배너 hello 논리 앱 관리 타일 대신 나타나면, OMS 작업 영역을 먼저 업그레이드 hello 배너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > !["OMS 작업 영역" 업그레이드](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="60d66-149">프로그램 논리를 응용 프로그램 실행에 대 한 자세한 정보는 요약 tooview hello 선택 **논리 앱 관리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="60d66-150">여기에서 논리 앱 실행은 이름이나 실행 상태로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![논리 앱 실행에 대한 상태 요약](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="60d66-152">특정 논리 앱 또는 상태, 논리 앱 또는 상태에 대 한 선택 hello 행에 대 한 모든 hello tooview 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="60d66-153">특정 논리 앱에 대 한 모든 hello 실행을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![논리 앱 또는 상태에 대한 실행 보기](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="60d66-155">hello **다시 전송** 열 다시 제출 된 실행에서 발생 하는 실행에 대 한 "예"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="60d66-156">이러한 결과 toofilter, 클라이언트와 서버 쪽 필터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="60d66-157">클라이언트 쪽 필터: 각 열에 대해 원하는 hello 필터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="60d66-158">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-158">Here are some examples:</span></span>

     ![예제 열 필터](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="60d66-160">서버 쪽 필터: toochoose 실행 hello hello 페이지 위쪽에 hello 범위 컨트롤을 사용 하 여 표시 되는 특정 시간 창 또는 toolimit hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="60d66-161">기본적으로 1,000개 레코드가 한 번에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![변경 hello 시간 창](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="60d66-163">모든 tooview hello 로그 검색 페이지를 열고 행 작업 및 특정 실행된을 선택 하기 위한 세부 정보 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="60d66-164">tooview이이 정보는 테이블의 선택 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="60d66-165">toochange hello 쿼리 hello 검색 창에 쿼리 문자열 hello를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="60d66-166">향상된 경험을 위해 **고급 분석**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![논리 앱 실행에 대한 작업 및 세부 정보 보기](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="60d66-168">여기 hello Azure 로그 분석 페이지에서 업데이트할 수 있습니다 쿼리 및 뷰 hello hello 테이블에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="60d66-169">이 쿼리에서 사용 하 여 [Kusto 쿼리 언어](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), tooview 다른 결과 편집할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d66-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics - 쿼리 뷰](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="60d66-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60d66-171">Next steps</span></span>

* [<span data-ttu-id="60d66-172">B2B 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="60d66-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
