---
title: "aaaCheck 상태 로깅을를 설정 하 고 알림-Azure 논리 앱을 얻는 | Microsoft Docs"
description: "논리 앱에 대한 상태 및 성능 모니터링, 진단 데이터 로그 및 경고 설정"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="962d2-103">상태 모니터링, 진단 로깅 설정, Azure Logic Apps에 대한 경고 설정</span><span class="sxs-lookup"><span data-stu-id="962d2-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="962d2-104">[논리 앱을 만들고 실행](../logic-apps/logic-apps-create-a-logic-app.md)한 후 해당 실행 기록, 트리거 기록, 상태 및 성능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="962d2-105">실시간 이벤트 모니터링 및 보다 풍부한 디버깅은 논리 앱에 대한 [진단 로깅](#azure-diagnostics)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="962d2-106">이런 방식으로 트리거 이벤트, 실행 이벤트 및 작업 이벤트와 같은 [이벤트를 찾고 볼](#find-events) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="962d2-107">또한 Azure Storage 및 Azure Event Hub와 같은 [다른 서비스와 함께 진단 데이터를 사용](#extend-diagnostic-data)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="962d2-108">가능한 다른 문제 또는 오류에 대 한 tooget 알림을 설정 [경고](#add-azure-alerts)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="962d2-109">예를 들어 "한 시간에 5개 이상의 실행이 실패하는 경우"를 검색하는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="962d2-110">[Azure 진단 이벤트 설정 및 속성](#diagnostic-event-properties)을 사용하여 프로그래밍 방식으로 모니터링, 추적 및 로깅을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="962d2-111">논리 앱에 대한 실행 및 트리거 기록 보기</span><span class="sxs-lookup"><span data-stu-id="962d2-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="962d2-112">toofind hello에서 논리 앱 [Azure 포털](https://portal.azure.com), 주요 Azure 메뉴 hello, 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="962d2-113">Hello 검색 상자에 "논리 앱"을 찾아 선택 **논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![논리 앱 찾기](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="962d2-115">Azure 포털 hello Azure 구독과 연결 된 모든 hello 논리 앱을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="962d2-116">논리 앱을 선택한 후 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="962d2-117">Azure 포털 hello hello 실행 기록 및 논리 앱에 대 한 트리거 기록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="962d2-118">예:</span><span class="sxs-lookup"><span data-stu-id="962d2-118">For example:</span></span>

   ![논리 앱 실행 기록 및 트리거 기록](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="962d2-120">**실행 기록** 논리 앱에 대 한 모든 hello 실행을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="962d2-121">**기록 트리거** 논리 앱에 대 한 모든 hello 트리거 활동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="962d2-122">상태 설명은 [논리 앱의 문제 해결](../logic-apps/logic-apps-diagnosing-failures.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="962d2-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="962d2-123">Hello 도구 모음에서 예상 하는 hello 데이터를 찾을 수 없는 경우 선택 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="962d2-124">아래에서 tooview hello 특정 실행에서 단계 **기록 실행**를 실행 하는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="962d2-125">hello 모니터 보기에서를 실행 하는 각 단계를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="962d2-126">예:</span><span class="sxs-lookup"><span data-stu-id="962d2-126">For example:</span></span>

   ![특정 실행에 대한 작업](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="962d2-128">tooget hello 실행 하는 방법에 대 한 자세한 내용은 선택 **실행 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="962d2-129">Hello 단계, 상태, 입력,이 정보를 요약 하 고 hello에 대 한 출력 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   !["실행 세부 정보" 선택](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="962d2-131">예를 들어 hello를 얻을 수 있습니다 실행의 **상관 관계 ID**, hello를 사용 하는 경우에 필요할 수 있는 [논리 앱에 대 한 REST API](https://docs.microsoft.com/rest/api/logic)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="962d2-132">특정 단계에 대 한 세부 정보 tooget 해당 단계를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="962d2-133">이제 해당 단계에 대해 발생한 입력, 출력 및 모든 오류와 같은 세부 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="962d2-134">예:</span><span class="sxs-lookup"><span data-stu-id="962d2-134">For example:</span></span>

   ![단계 세부 정보](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="962d2-136">모든 런타임 세부 정보 및 이벤트 hello 논리 앱 서비스 내에서 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="962d2-137">사용자 tooview 데이터를 요청 하는 경우에 해독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="962d2-138">관련 액세스 toothese 이벤트를 제어할 수 있습니다 [신속히 알아봅니다 액세스 제어 (RBAC)](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="962d2-139">특정 트리거 이벤트에 대 한 세부 정보 tooget toohello 돌아가서 **개요** 창.</span><span class="sxs-lookup"><span data-stu-id="962d2-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="962d2-140">아래 **기록 트리거할**선택, hello 트리거 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="962d2-141">이제 입력 및 출력과 같은 세부 정보를 검토할 수 있습니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-141">You can now review details like inputs and outputs, for example:</span></span>

   ![트리거 이벤트 출력 세부 정보](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="962d2-143">논리 앱에 대한 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="962d2-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="962d2-144">런타임 세부 정보 및 이벤트로 보다 풍부한 디버깅은 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)를 사용하여 진단 로깅을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="962d2-145">로그 분석은 서비스에 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 를 모니터링 하는 클라우드 및 온-프레미스 환경 toohelp의 가용성과 성능을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="962d2-146">시작 하기 전에 toohave OMS 작업 영역 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="962d2-147">자세한 내용은 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="962d2-148">Hello에 [Azure 포털](https://portal.azure.com)찾아 논리 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="962d2-149">Hello 논리 앱 블레이드 메뉴 아래 **모니터링**, 선택 **진단** > **진단 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![진단 설정 tooMonitoring, 진단, 이동](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="962d2-151">**진단 설정** 아래에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![진단 로그 설정](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="962d2-153">표시 된 것 처럼 이제 로깅에 대 한 hello OMS 작업 영역 및 이벤트 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="962d2-154">선택 **tooLog 분석 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="962d2-155">**Log Analytics** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="962d2-156">아래 **OMS 작업 영역**를 로깅에 대 한 OMS 작업 영역 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="962d2-157">아래 **로그**선택, hello **WorkflowRuntime** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="962d2-158">Hello 메트릭 간격을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="962d2-159">완료하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-159">When you're done, choose **Save**.</span></span>

   ![로깅에 대한 OMS 작업 영역 및 데이터 선택](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="962d2-161">이제 트리거 이벤트, 실행 이벤트 및 작업 이벤트에 대한 이벤트 및 기타 데이터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="962d2-162">논리 앱에 대한 이벤트 및 데이터 찾기</span><span class="sxs-lookup"><span data-stu-id="962d2-162">Find events and data for your logic app</span></span>

<span data-ttu-id="962d2-163">이벤트를 실행 하는 트리거 이벤트 및 동작 이벤트와 같은 논리 앱에서 toofind 및 보기 이벤트는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="962d2-164">Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="962d2-165">"로그 분석"에 대해 검색한 후 다음과 같이 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   !["Log Analytics" 선택](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="962d2-167">**Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS 작업 영역 선택](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="962d2-169">**관리** 아래에서 **OMS 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-169">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS 포털" 선택](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="962d2-171">OMS 홈페이지에서 **로그 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-171">On your OMS home page, choose **Log Search**.</span></span>

   ![OMS 홈페이지에서 "로그 검색" 선택](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="962d2-173">또는</span><span class="sxs-lookup"><span data-stu-id="962d2-173">-or-</span></span>

   ![Hello OMS 메뉴에서 "로그 검색"를 선택 합니다.](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="962d2-175">Hello 검색 상자에 원하는 toofind, 필드를 지정 하 고 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="962d2-176">입력을 시작할 때 OMS는 사용할 수 있는 가능한 일치 및 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="962d2-177">Toofind hello 상위 10 개의 이벤트를 발생 한 시간을 입력 하 고이 검색 쿼리를 선택 하는 예를 들어: **범주 WorkflowRuntime = | 최상위 10 개**</span><span class="sxs-lookup"><span data-stu-id="962d2-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![검색 문자열 입력](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="962d2-179">에 대 한 자세한 내용은 [어떻게 로그 분석의 데이터를 toofind](../log-analytics/log-analytics-log-searches.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="962d2-180">Hello 결과 페이지에서 왼쪽된 모음 hello 선택 hello 기간 tooview 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="962d2-181">toorefine 필터를 추가 하 여 쿼리 선택 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![쿼리 결과에 대한 시간 프레임 선택](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="962d2-183">아래 **필터 추가**, 원하는 hello 필터를 찾을 수 있도록 hello 필터 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="962d2-184">Hello 필터를 선택 하 고 선택 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="962d2-185">이 예제를 사용 하 여 단어 "상태" toofind hello 실패 이벤트에서 **AzureDiagnostics**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="962d2-186">여기에 대 한 필터를 hello **status_s** 이미 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-186">Here hello filter for **status_s** is already selected.</span></span>

   ![필터 선택](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="962d2-188">Hello 왼쪽된 모음에서 toouse, 원하고 선택 hello 필터 값 선택 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![필터 값 선택, "적용" 선택](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="962d2-190">이제 만든다면 toohello 쿼리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="962d2-191">선택한 필터 및 값으로 쿼리가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="962d2-192">이제 이전 결과 또한 필터링되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-192">Your previous results are now filtered too.</span></span>

   ![필터링 결과 tooyour 쿼리를 반환 합니다.](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="962d2-194">toosave 이후 사용에 대 한 쿼리 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="962d2-195">자세한 내용은 [어떻게 toosave 쿼리](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="962d2-196">다른 서비스와 함께 진단 데이터를 사용하는 방법 및 위치 확장</span><span class="sxs-lookup"><span data-stu-id="962d2-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="962d2-197">Azure Log Analytics와 마찬가지로 다른 Azure 서비스와 함께 논리 앱의 진단 데이터를 사용하는 방법을 다음과 같이 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="962d2-198">Azure Storage에 Azure 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="962d2-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="962d2-199">Azure 진단 로그 tooAzure 스트림 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="962d2-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="962d2-200">그런 다음 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 및 [Power BI](../log-analytics/log-analytics-powerbi.md)와 같은 다른 서비스의 원격 분석 및 분석을 사용하여 실시간으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="962d2-201">예:</span><span class="sxs-lookup"><span data-stu-id="962d2-201">For example:</span></span>

* [<span data-ttu-id="962d2-202">이벤트 허브 tooStream 분석에서에서 스트림 데이터</span><span class="sxs-lookup"><span data-stu-id="962d2-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="962d2-203">Stream Analytics를 사용하여 스트리밍 데이터 분석 및 Power BI에서 실시간 분석 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="962d2-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="962d2-204">Hello 원하는 옵션을 설정에 따라, 다음 사항을 확인 하면 첫 번째 [Azure 저장소 계정 만들기](../storage/common/storage-create-storage-account.md) 또는 [Azure 이벤트 허브 만들기](../event-hubs/event-hubs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="962d2-205">Toosend 진단 데이터에 대 한 hello 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![데이터는 저장소 계정 또는 이벤트 허브를 tooAzure 보내기](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="962d2-207">보존 기간 toouse 저장소 계정을 선택 하는 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="962d2-208">논리 앱에 대한 경고 설정</span><span class="sxs-lookup"><span data-stu-id="962d2-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="962d2-209">특정 메트릭을 toomonitor 또는 논리 앱에 대 한 임계값이 초과 임계값 설정 [Azure에서 경고](../monitoring-and-diagnostics/monitoring-overview-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="962d2-210">[Azure의 매트릭](../monitoring-and-diagnostics/monitoring-overview-metrics.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="962d2-211">경고 없이 tooset [Azure 로그 분석](../log-analytics/log-analytics-overview.md), 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="962d2-212">더 많은 고급 경고 조건 및 작업은 [Log Analytics도 설정](#azure-diagnostics)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="962d2-213">Hello 논리 앱 블레이드 메뉴 아래 **모니터링**, 선택 **진단** > **규칙 경고** > **추가 경고**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![논리 앱에 대한 경고 추가](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="962d2-215">Hello에 **경고 규칙 추가** 블레이드를 표시 된 것 처럼 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="962d2-216">**리소스** 아래에서 논리 앱을 선택하지 않은 경우 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="962d2-217">경고에 대한 이름 및 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="962d2-218">선택 된 **메트릭을** 나 tootrack 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="962d2-219">선택는 **조건**, 지정는 **임계값** hello 메트릭 및 선택 hello에 대 한 **기간** 이 메트릭을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="962d2-220">Toosend hello 경고에 대 한 메일 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="962d2-221">Hello 경고를 전송에 대 한 다른 전자 메일 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="962d2-222">또한 toosend hello 경고가 넣을 webhook URL을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="962d2-223">예를 들어 이 규칙은 한 시간에 5개 이상의 실행이 실패하는 경우 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![메트릭 경고 규칙 만들기](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="962d2-225">toorun 논리 앱에서 경고를 통해 hello를 포함할 수 있습니다 [요청 트리거](../connectors/connectors-native-reqres.md) 워크플로에서 수 있는 다음이 예제 처럼 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="962d2-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="962d2-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="962d2-227">텍스트 보내기</span><span class="sxs-lookup"><span data-stu-id="962d2-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="962d2-228">메시지 tooa 큐 추가</span><span class="sxs-lookup"><span data-stu-id="962d2-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="962d2-229">Azure 진단 이벤트 설정 및 세부 정보</span><span class="sxs-lookup"><span data-stu-id="962d2-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="962d2-230">논리 앱 및 해당 이벤트, 예를 들어 hello 상태에 대 한 세부 정보를 포함 하는 각 진단 이벤트, 시작 시간, 종료 시간, 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="962d2-231">모니터링, 추적 및 로깅 설정 tooprogrammatically, ou hello로 이러한 세부 정보를 사용할 수 있다 [Azure 논리 앱에 대 한 REST API](https://docs.microsoft.com/rest/api/logic) 및 hello [Azure 진단에 대 한 REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows)합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="962d2-232">예를 들어 hello `ActionCompleted` 이벤트에 hello `clientTrackingId` 및 `trackedProperties` 추적 및 모니터링에 사용할 수 있는 속성:</span><span class="sxs-lookup"><span data-stu-id="962d2-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="962d2-233">`clientTrackingId`: 그렇지 않은 경우 Azure는 자동으로이 ID를 생성 하 고 실행 하는 논리 앱에서 이벤트를 상호 연결 하는 경우 모든 중첩 된 워크플로 포함 하 여 호출 되 hello 논리 앱에서.</span><span class="sxs-lookup"><span data-stu-id="962d2-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="962d2-234">전달 하 여이 ID는 트리거에서 직접 지정할 수 있습니다는 `x-ms-client-tracking-id` hello 트리거 요청에 사용자 지정 ID 값을 가진 헤더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="962d2-235">요청 트리거, HTTP 트리거 또는 웹후크 트리거를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="962d2-236">`trackedProperties`: 논리 앱의 JSON 정의에서 추적 되는 속성 tooactions tootrack 입력 또는 출력 진단 데이터에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="962d2-237">추적 되는 속성에만 한 번의 작업의 입력 및 출력을 추적할 수 있지만 hello를 사용할 수 있습니다 `correlation` 작업 실행 중에 걸쳐 이벤트 toocorrelate의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="962d2-238">tootrack 하나 이상의 속성 추가 hello `trackedProperties` toohello 작업 정의 원하는 섹션과 hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="962d2-239">예를 들어 "order ID"와 같이 tootrack 데이터 원격 분석에서 원하는 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="962d2-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="962d2-240">다음 단계</span><span class="sxs-lookup"><span data-stu-id="962d2-240">Next steps</span></span>

* [<span data-ttu-id="962d2-241">논리 앱 배포 및 릴리스 관리용 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="962d2-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="962d2-242">B2B 시나리오 및 엔터프라이즈 통합 팩</span><span class="sxs-lookup"><span data-stu-id="962d2-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="962d2-243">B2B 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="962d2-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)