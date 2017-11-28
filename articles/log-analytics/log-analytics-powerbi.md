---
title: "Log Analytics 데이터를 Power BI로 내보내기 | Microsoft Docs"
description: "Power BI는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.  Log Analytics는 시각화 및 분석 도구를 활용할 수 있도록 OMS 리포지토리에서 Power BI로 데이터를 지속적으로 내보낼 수 있습니다.  이 문서에서는 Power BI에 일정한 간격으로 자동으로 내보내는 Log Analytics에서 쿼리를 구성하는 방법을 설명합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="eb940-105">Log Analytics 데이터를 Power BI로 내보내기</span><span class="sxs-lookup"><span data-stu-id="eb940-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="eb940-106">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 Log Analytics 데이터를 Power BI로 내보내는 이 프로세스가 더 이상 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="eb940-107">그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="eb940-108">업그레이드 후 Azure Log Analytics는 Application Insights와 같은 플랫폼을 사용하며, [Application Insights 쿼리를 Power BI로 내보내는 프로세스](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)와 같은 프로세스를 사용하여 Log Analytics 쿼리를 Power BI로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="eb940-109">해당 문서의 설명에 따라 분석 콘솔을 사용하여 쿼리를 내보낼 수도 있고, 로그 검색 포털의 화면 위쪽에 있는 **Power BI** 단추를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="eb940-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="eb940-111">Log Analytics는 시각화 및 분석 도구를 활용할 수 있도록 OMS 리포지토리에서 Power BI로 데이터를 자동으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="eb940-112">Log Analytics로 Power BI를 구성할 때 해당 결과를 Power BI의 해당 데이터 집합으로 내보내는 로그 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="eb940-113">쿼리 및 내보내기는 Log Analytics에 의해 수집된 최신 데이터로 데이터 집합을 최신 상태로 유지하도록 정의한 일정에 따라 계속해서 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics에서 Power BI로](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="eb940-115">Power BI 일정</span><span class="sxs-lookup"><span data-stu-id="eb940-115">Power BI Schedules</span></span>
<span data-ttu-id="eb940-116">*Power BI 일정* 에는 OMS 리포지토리에서 Power BI의 해당 데이터 집합으로 데이터 집합을 내보내는 로그 검색 및 데이터 집합을 최신으로 유지하는 이 검색 실행 빈도를 정의하는 일정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="eb940-117">데이터 집합의 필드는 로그 검색에서 반환되는 레코드의 속성과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="eb940-118">검색이 다양한 종류의 레코드를 반환하는 경우 데이터 집합은 포함된 각 레코드 형식의 모든 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="eb940-119">[Measure](log-analytics-search-reference.md#measure)와 같은 명령을 사용하여 모든 통합을 수행하는 것과 달리 원시 데이터를 반환하는 로그 검색 쿼리를 사용하는 것이 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="eb940-120">원시 데이터에서 Power BI의 모든 집계와 계산을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="eb940-121">OMS 작업 영역을 Power BI에 연결</span><span class="sxs-lookup"><span data-stu-id="eb940-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="eb940-122">Log Analytics에서 Power BI로 내보내려면 다음 절차를 사용하여 Power BI 계정에 OMS 작업 영역을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="eb940-123">OMS 콘솔에서 **설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="eb940-124">**계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="eb940-125">**작업 영역 정보** 섹션에서 **Connect to Power BI Account**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="eb940-126">Power BI 계정에 대한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="eb940-127">Power BI 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="eb940-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="eb940-128">다음 절차를 사용하여 각 데이터 집합에 대한 Power BI 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="eb940-129">OMS 콘솔에서 **로그 검색** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="eb940-130">새 쿼리를 입력하거나 **Power BI**로 내보내려는 데이터를 반환하는 저장된 검색을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="eb940-131">페이지 맨 위에 있는 **Power BI** 단추를 클릭하여 **Power BI** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="eb940-132">다음 테이블에 정보를 제공하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="eb940-133">속성</span><span class="sxs-lookup"><span data-stu-id="eb940-133">Property</span></span> | <span data-ttu-id="eb940-134">설명</span><span class="sxs-lookup"><span data-stu-id="eb940-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb940-135">이름</span><span class="sxs-lookup"><span data-stu-id="eb940-135">Name</span></span> |<span data-ttu-id="eb940-136">Power BI 일정의 목록을 볼 때 일정을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="eb940-137">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="eb940-137">Saved Search</span></span> |<span data-ttu-id="eb940-138">실행할 로그 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-138">The log search to run.</span></span>  <span data-ttu-id="eb940-139">현재 쿼리를 선택하거나 드롭다운 상자에서 기존 저장된 검색을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="eb940-140">일정</span><span class="sxs-lookup"><span data-stu-id="eb940-140">Schedule</span></span> |<span data-ttu-id="eb940-141">저장된 검색을 실행하고 Power BI 데이터 집합으로 내보내는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="eb940-142">값은 15분에서 24시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="eb940-143">데이터 집합 이름</span><span class="sxs-lookup"><span data-stu-id="eb940-143">Dataset Name</span></span> |<span data-ttu-id="eb940-144">Power BI의 데이터 집합 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="eb940-145">존재하지 않는 경우 생성되고 존재하는 경우 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="eb940-146">Power BI 일정 보기 및 제거</span><span class="sxs-lookup"><span data-stu-id="eb940-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="eb940-147">다음 절차를 사용하여 기존 Power BI 일정의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="eb940-148">OMS 콘솔에서 **설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="eb940-149">**Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-149">Select **Power BI**.</span></span>

<span data-ttu-id="eb940-150">일정의 세부 정보 외에도 지난 주에 일정이 실행된 횟수와 마지막 동기화의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="eb940-151">동기화에 오류가 발견되면 링크를 클릭하여 오류의 세부 정보로 레코드에 대한 로그 검색을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="eb940-152">**열 제거**의 **X**를 클릭하여 일정을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="eb940-153">**끄기**를 선택하여 일정을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="eb940-154">일정을 수정하려면 제거하고 새 설정으로 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Power BI 일정](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="eb940-156">샘플 연습</span><span class="sxs-lookup"><span data-stu-id="eb940-156">Sample walkthrough</span></span>
<span data-ttu-id="eb940-157">다음 섹션은 Power BI 일정을 만들고 해당 데이터 집합을 사용하여 간단한 보고서를 만드는 예제를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="eb940-158">이 예제에서는 컴퓨터 집합에 대한 모든 성능 데이터가 Power BI로 내보내진 다음 프로세서 사용률을 표시하는 꺾은선형 그래프가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="eb940-159">로그 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="eb940-159">Create log search</span></span>
<span data-ttu-id="eb940-160">데이터 집합에 보낼 데이터에 대한 로그 검색을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="eb940-161">이 예제에서는 *srv*로 시작하는 이름의 컴퓨터에 대한 모든 성능 데이터를 반환하는 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI 일정](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="eb940-163">Power BI 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="eb940-163">Create Power BI Search</span></span>
<span data-ttu-id="eb940-164">**Power BI** 단추를 클릭하여 Power BI 대화 상자를 열고 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="eb940-165">이 검색이 시간당 한 번씩 실행되길 원하고 *Contoso Perf*라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="eb940-166">원하는 데이터를 만드는 검색 열기가 이미 있으므로 *저장된 검색* 에 대한 **현재 검색 쿼리 사용**의 기본값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="eb940-168">Power BI 검색 확인</span><span class="sxs-lookup"><span data-stu-id="eb940-168">Verify Power BI Search</span></span>
<span data-ttu-id="eb940-169">일정을 올바르게 만들었는지 확인하려면 OMS 대시보드의 **설정** 타일 아래에서 Power BI 검색의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="eb940-170">동기화가 실행되었음을 보고할 때까지 몇 분 정도 기다렸다가 이 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="eb940-172">Power BI의 데이터 집합 확인</span><span class="sxs-lookup"><span data-stu-id="eb940-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="eb940-173">[powerbi.microsoft.com](http://powerbi.microsoft.com/) 에 계정으로 로그인하고 왼쪽 창 맨 아래의 **데이터 집합** 으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="eb940-174">내보내기가 성공적으로 실행되었음을 나타내는 *Contoso Perf* 가 나열된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI 데이터 집합](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="eb940-176">데이터 집합 기반 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="eb940-176">Create report based on dataset</span></span>
<span data-ttu-id="eb940-177">이 데이터 집합에 포함된 필드를 보려면 **Contoso Perf** 데이터 집합을 선택한 다음 오른쪽 **필드** 창에서 **결과**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="eb940-178">각 컴퓨터에 대한 프로세서 사용률을 보여 주는 꺾은선형 그래프를 만들려면 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="eb940-179">선 차트 시각화를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="eb940-180">**ObjectName**을 **Report level filter**로 끌어 놓고 **Processor**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="eb940-181">**CounterName**을 **Report level filter**로 끌어 놓고 **% Processor Time**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="eb940-182">**CounterValue**를 **Values**로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="eb940-183">**Computer**를 **Legend**로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="eb940-184">**TimeGenerated**를 **Axis**로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="eb940-185">데이터 집합의 데이터로 결과 꺾은선형 그래프가 표시된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Power BI 꺾은선형 그래프](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="eb940-187">보고서 저장</span><span class="sxs-lookup"><span data-stu-id="eb940-187">Save the report</span></span>
<span data-ttu-id="eb940-188">화면 맨 위에 있는 저장 단추를 클릭하여 보고서를 저장하고 왼쪽 창의 보고서 섹션에 나열된 것을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Power BI 보고서](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="eb940-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb940-190">Next steps</span></span>
* <span data-ttu-id="eb940-191">Power BI로 내보낼 수 있는 쿼리를 작성하려면 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb940-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="eb940-192">Log Analytics 내보내기를 기준으로 시각화를 작성하려면 [Power BI](http://powerbi.microsoft.com) 에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="eb940-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
