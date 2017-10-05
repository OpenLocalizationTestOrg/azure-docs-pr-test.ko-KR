---
title: "Operations Management Suite에서 B2B 메시지에 대한 쿼리 - Azure Logic Apps | Microsoft Docs"
description: "Operations Management Suite에서 AS2, X12 및 EDIFACT 메시지를 추적하는 쿼리 만들기"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="ade06-103">OMS(Microsoft Operations Management Suite)에서 AS2, X12 및 EDIFACT 메시지에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="ade06-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="ade06-104">[OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)에서 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)를 사용하여 추적 중인 AS2, X12 또는 EDIFACT 메시지를 찾기 위해 특정 조건에 따라 작업을 필터링하는 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="ade06-105">예를 들어 특정 교환 컨트롤 번호에 따라 메시지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="ade06-106">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ade06-106">Requirements</span></span>

* <span data-ttu-id="ade06-107">진단 로깅과 함께 설정된 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="ade06-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="ade06-108">[논리 앱을 만드는 방법](../logic-apps/logic-apps-create-a-logic-app.md) 및 [해당 논리 앱에 대한 로깅을 설정하는 방법](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="ade06-109">모니터링 및 로깅을 사용하여 설정된 통합 계정.</span><span class="sxs-lookup"><span data-stu-id="ade06-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="ade06-110">[통합 계정을 만드는 방법](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) 및 [해당 계정에 대한 모니터링 및 로깅을 설정하는 방법](../logic-apps/logic-apps-monitor-b2b-message.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="ade06-111">아직 없는 경우 [Log Analytics에 진단 데이터를 게시](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)하고 [OMS에서 메시지 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ade06-112">이전 요구 사항을 충족한 후 [OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)에 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="ade06-113">OMS에서 B2B 통신 추적에 대해 동일한 OMS 작업 영역을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="ade06-114">OMS 작업 영역이 없는 경우 [OMS 작업 영역을 만드는 방법](../log-analytics/log-analytics-get-started.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="ade06-115">Operations Management Suite 포털에서 필터로 메시지 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="ade06-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="ade06-116">이 예제는 해당 교환 컨트롤 번호에 따라 메시지를 찾는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="ade06-117">OMS 작업 영역 이름을 알고 있으면 작업 영역 홈페이지(`https://{your-workspace-name}.portal.mms.microsoft.com`)로 이동하고 4단계에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="ade06-118">그렇지 않은 경우 1단계에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="ade06-119">[Azure Portal](https://portal.azure.com)에서 **더 많은 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="ade06-120">"로그 분석"에 대해 검색한 후 다음과 같이 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Log Analytics 찾기](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="ade06-122">**Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![OMS 작업 영역 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="ade06-124">**관리** 아래에서 **OMS 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![OMS 포털 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="ade06-126">OMS 홈페이지에서 **로그 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-126">On your OMS home page, choose **Log Search**.</span></span>

   ![OMS 홈페이지에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="ade06-128">또는</span><span class="sxs-lookup"><span data-stu-id="ade06-128">-or-</span></span>

   ![OMS 홈 메뉴에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="ade06-130">검색 상자에 찾으려는 필드를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="ade06-131">입력을 시작할 때 OMS는 사용할 수 있는 가능한 일치 및 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="ade06-132">[Log Analytics에서 데이터를 찾는 방법](../log-analytics/log-analytics-log-searches.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="ade06-133">이 예제에서는 **Type=AzureDiagnostics**로 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![쿼리 문자열 입력 시작](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="ade06-135">왼쪽 모음에서 보려는 시간 프레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="ade06-136">쿼리에 필터를 추가하려면 **+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-136">To add a filter to your query, choose **+Add**.</span></span>

   ![쿼리에 필터 추가](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="ade06-138">**필터 추가** 아래에서 원하는 필터를 찾을 수 있도록 필터 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="ade06-139">필터를 선택하고 **+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="ade06-140">교환 컨트롤 번호를 찾기 위해 이 예제에서는 "교환"이라는 단어를 검색하고 필터로 **event_record_messageProperties_interchangeControlNumber_s**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![필터 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="ade06-142">왼쪽 모음에서 사용하려는 필터 값을 선택하고 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="ade06-143">이 예제에서는 원하는 메시지에 대한 교환 컨트롤 번호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-143">This example selects the interchange control number for the messages we want.</span></span>

   ![필터 값 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="ade06-145">이제 작성 중인 쿼리로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-145">Now return to the query that you're building.</span></span> <span data-ttu-id="ade06-146">선택한 필터 이벤트 및 값으로 쿼리가 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="ade06-147">이제 이전 결과 또한 필터링되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-147">Your previous results are now filtered too.</span></span>

    ![필터링된 결과와 함께 쿼리로 돌아가기](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="ade06-149">나중에 사용할 쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="ade06-149">Save your query for future use</span></span>

1. <span data-ttu-id="ade06-150">**로그 검색** 페이지의 쿼리에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="ade06-151">쿼리에 이름을 지정하고 범주를 선택하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![쿼리에 이름 및 범주 지정](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="ade06-153">쿼리를 보려면 **즐겨찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-153">To view your query, choose **Favorites**.</span></span>

   !["즐겨찾기" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="ade06-155">**저장된 검색** 아래에서 결과를 볼 수 있도록 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="ade06-156">서로 다른 결과를 찾을 수 있도록 쿼리를 업데이트하려면 쿼리를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-156">To update the query so you can find different results, edit the query.</span></span>

   ![쿼리 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="ade06-158">Operations Management Suite 포털의 저장된 쿼리 찾기 및 실행</span><span class="sxs-lookup"><span data-stu-id="ade06-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="ade06-159">OMS 작업 영역 홈페이지(`https://{your-workspace-name}.portal.mms.microsoft.com`)를 열고 **로그 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![OMS 홈페이지에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="ade06-161">또는</span><span class="sxs-lookup"><span data-stu-id="ade06-161">-or-</span></span>

   ![OMS 홈 메뉴에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="ade06-163">**로그 검색** 홈페이지에서 **즐겨찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   !["즐겨찾기" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="ade06-165">**저장된 검색** 아래에서 결과를 볼 수 있도록 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="ade06-166">서로 다른 결과를 찾을 수 있도록 쿼리를 업데이트하려면 쿼리를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ade06-166">To update the query so you can find different results, edit the query.</span></span>

   ![쿼리 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="ade06-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ade06-168">Next steps</span></span>

* [<span data-ttu-id="ade06-169">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="ade06-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="ade06-170">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="ade06-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="ade06-171">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="ade06-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)