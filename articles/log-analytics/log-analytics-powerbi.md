---
title: "aaaExport 로그 분석 데이터 tooPower BI | Microsoft Docs"
description: "Power BI는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.  로그 분석 지속적으로 내보낼 수 데이터 hello OMS 저장소에서 Power BI로 하므로 해당 시각화 및 분석 도구를 활용할 수 있습니다.  이 문서에서는 일정 한 간격으로 자동으로 BI tooPower를 내보내는 로그 분석의 tooconfigure 쿼리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a><span data-ttu-id="5e928-105">로그 분석 데이터 tooPower BI 내보내기</span><span class="sxs-lookup"><span data-stu-id="5e928-105">Export Log Analytics data tooPower BI</span></span>

>[!NOTE]
> <span data-ttu-id="5e928-106">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 로그 분석 데이터 tooPower BI 내보내기에 대 한이 과정은 더 이상 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data tooPower BI will no longer work.</span></span>  <span data-ttu-id="5e928-107">그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="5e928-108">업그레이드 후 Azure 로그 분석 사용 하 여 hello Application Insights와 같은 플랫폼 및 동일한 프로세스으로 tooexport 로그 분석 쿼리 tooPower BI hello를 사용 하 여 [hello 프로세스 tooexport Application Insights 쿼리 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-108">After upgrade, Azure Log Analytics uses hello same platform as Application Insights, and you use hello same process tooexport Log Analytics queries tooPower BI as [hello process tooexport Application Insights queries tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="5e928-109">해당 문서에 설명 된 대로 hello 분석 콘솔을 사용 하 여 hello 쿼리를 내보낸 하거나 hello를 선택할 수 있습니다 **Power BI** hello hello 로그 검색 포털의 hello 화면 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-109">You can either export hello query using hello Analytics console as described in that article, or you can select hello **Power BI** button at hello top of hello screen in hello Log Search portal.</span></span>



<span data-ttu-id="5e928-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="5e928-111">로그 분석 자동으로 내보낼 수 데이터 hello OMS 저장소에서 Power BI로 하므로 해당 시각화 및 분석 도구를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-111">Log Analytics can automatically export data from hello OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="5e928-112">로그 분석을 Power BI를 구성할 때 Power BI에서 데이터 집합 결과 toocorresponding 내보내기 로그 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-112">When you configure Power BI with Log Analytics, you create log queries that export their results toocorresponding datasets in Power BI.</span></span>  <span data-ttu-id="5e928-113">hello 쿼리 및 내보내기 tooautomatically 로그 분석에 의해 수집 된 hello 최신 데이터와 toodate tookeep hello 데이터 집합을 정의 하는 일정에 따라 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-113">hello query and export continues tooautomatically run on a schedule that you define tookeep hello dataset up toodate with hello latest data collected by Log Analytics.</span></span>

![로그 분석 tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="5e928-115">Power BI 일정</span><span class="sxs-lookup"><span data-stu-id="5e928-115">Power BI Schedules</span></span>
<span data-ttu-id="5e928-116">A *Power BI 일정* hello OMS 리포지토리에 tooa 해당 데이터 집합에서 Power BI 및이 검색은 tookeep hello 데이터 집합 현재을 실행 하는 빈도 정의 하는 일정에서 데이터 집합을 내보내는 로그 검색에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-116">A *Power BI Schedule* includes a log search that exports a set of data from hello OMS repository tooa corresponding dataset in Power BI and a schedule that defines how often this search is run tookeep hello dataset current.</span></span>

<span data-ttu-id="5e928-117">hello 데이터 집합의 hello 필드 hello 로그 검색에서 반환 된 hello 레코드의 hello 속성 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-117">hello fields in hello dataset will match hello properties of hello records returned by hello log search.</span></span>  <span data-ttu-id="5e928-118">Hello 검색 hello 데이터 집합의 모두 포함 되며 다음 다양 한 종류의 레코드를 반환 하는 경우 각각 hello의 hello 속성이 레코드 종류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-118">If hello search returns records of different types then hello dataset will include all of hello properties from each of hello included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="5e928-119">모범 사례 toouse와 같은 명령을 사용 하 여 모든 통합 것과 반대로 tooperforming으로 원시 데이터를 반환 하는 로그 검색 쿼리는 [측정값](log-analytics-search-reference.md#measure)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-119">It is a best practice toouse a log search query that returns raw data as opposed tooperforming any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="5e928-120">Hello 원시 데이터에서 Power BI에서 모든 집계 및 계산을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-120">You can perform any aggregation and calculations in Power BI from hello raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a><span data-ttu-id="5e928-121">OMS 작업 영역 tooPower BI를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-121">Connecting OMS workspace tooPower BI</span></span>
<span data-ttu-id="5e928-122">로그 분석 tooPower BI에서에서 내보낼 수 있습니다, 전에 절차를 수행 하는 hello를 사용 하 여 OMS 작업 영역 tooyour Power BI 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-122">Before you can export from Log Analytics tooPower BI, you must connect your OMS workspace tooyour Power BI account using hello following procedure.</span></span>  

1. <span data-ttu-id="5e928-123">Hello OMS 콘솔에서 클릭 hello **설정** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-123">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="5e928-124">**계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="5e928-125">Hello에 **작업 영역 정보** 섹션 클릭 **tooPower BI 계정 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-125">In hello **Workspace Information** section click **Connect tooPower BI Account**.</span></span>
4. <span data-ttu-id="5e928-126">Power BI 계정에 대 한 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-126">Enter hello credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="5e928-127">Power BI 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="5e928-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="5e928-128">절차를 수행 하는 hello를 사용 하 여 각 데이터 집합에 대 한 Power BI 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-128">Create a Power BI Schedule for each dataset using hello following procedure.</span></span>

1. <span data-ttu-id="5e928-129">Hello OMS 콘솔에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-129">In hello OMS console click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="5e928-130">새 쿼리를 입력 하거나 선택 hello tooexport 너무 되도록 데이터를 반환 하는 저장된 된 검색**Power BI**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-130">Type in a new query or select a saved search that returns hello data that you want tooexport too**Power BI**.</span></span>  
3. <span data-ttu-id="5e928-131">Hello 클릭 **Power BI** hello 페이지 tooopen hello hello 위쪽에 단추 **Power BI** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5e928-131">Click hello **Power BI** button at hello top of hello page tooopen hello **Power BI** dialog.</span></span>
4. <span data-ttu-id="5e928-132">다음 테이블을 클릭 하 여 hello에 hello 정보를 제공 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-132">Provide hello information in hello following table and click **Save**.</span></span>

| <span data-ttu-id="5e928-133">속성</span><span class="sxs-lookup"><span data-stu-id="5e928-133">Property</span></span> | <span data-ttu-id="5e928-134">설명</span><span class="sxs-lookup"><span data-stu-id="5e928-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5e928-135">이름</span><span class="sxs-lookup"><span data-stu-id="5e928-135">Name</span></span> |<span data-ttu-id="5e928-136">이름 tooidentify hello 일정의 Power BI 일정 hello 목록을 볼 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-136">Name tooidentify hello schedule when you view hello list of Power BI schedules.</span></span> |
| <span data-ttu-id="5e928-137">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="5e928-137">Saved Search</span></span> |<span data-ttu-id="5e928-138">로그 검색 toorun hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-138">hello log search toorun.</span></span>  <span data-ttu-id="5e928-139">Hello 현재 쿼리를 선택 하거나 hello 드롭다운 상자에서 기존 저장 된 검색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-139">You can either select hello current query or select an existing saved search from hello dropdown box.</span></span> |
| <span data-ttu-id="5e928-140">일정</span><span class="sxs-lookup"><span data-stu-id="5e928-140">Schedule</span></span> |<span data-ttu-id="5e928-141">얼마나 자주 저장 toorun hello 검색 및 toohello Power BI 데이터 집합을 내보내기.</span><span class="sxs-lookup"><span data-stu-id="5e928-141">How often toorun hello saved search and export toohello Power BI dataset.</span></span>  <span data-ttu-id="5e928-142">hello 값은 15 분에서 24 시간 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-142">hello value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="5e928-143">데이터 집합 이름</span><span class="sxs-lookup"><span data-stu-id="5e928-143">Dataset Name</span></span> |<span data-ttu-id="5e928-144">Power BI의 hello 데이터 집합의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-144">hello name of hello dataset in Power BI.</span></span>  <span data-ttu-id="5e928-145">존재하지 않는 경우 생성되고 존재하는 경우 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="5e928-146">Power BI 일정 보기 및 제거</span><span class="sxs-lookup"><span data-stu-id="5e928-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="5e928-147">절차를 수행 하는 hello 사용 하 여 기존 Power BI 일정의 보기 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-147">View hello list of existing Power BI Schedules with hello following procedure.</span></span>

1. <span data-ttu-id="5e928-148">Hello OMS 콘솔에서 클릭 hello **설정** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-148">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="5e928-149">**Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-149">Select **Power BI**.</span></span>

<span data-ttu-id="5e928-150">또한 hello의 toohello 세부 정보를 예약 하 고 hello 횟수를 일정 hello 지난 주 hello에서 실행 된 hello hello 마지막 동기화 상태를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-150">In addition toohello details of hello schedule, hello number of times that hello schedule has run in hello past week and hello status of hello last sync are displayed.</span></span>  <span data-ttu-id="5e928-151">Hello 동기화 오류가 발생 하면 hello 링크 toorun hello 오류의 세부 정보를 레코드에 대 한 로그 검색 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-151">If hello sync encountered errors, you can click hello link toorun a log search for records with details of hello error.</span></span>

<span data-ttu-id="5e928-152">Hello를 클릭 하 여 일정을 제거할 수 있습니다 **X** hello에 **제거 열**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-152">You can remove a schedule by clicking on hello **X** in hello **Remove column**.</span></span>  <span data-ttu-id="5e928-153">**끄기**를 선택하여 일정을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="5e928-154">toomodify 일정을 제거 하며 hello 새 설정으로 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-154">toomodify a schedule you must remove it and recreate it with hello new settings.</span></span>

![Power BI 일정](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="5e928-156">샘플 연습</span><span class="sxs-lookup"><span data-stu-id="5e928-156">Sample walkthrough</span></span>
<span data-ttu-id="5e928-157">hello 다음 섹션 안내 Power BI 작업을 예약 하 고 해당 데이터 집합 toocreate를 사용 하 여의 예는 간단한 보고서.</span><span class="sxs-lookup"><span data-stu-id="5e928-157">hello following section walks through an example of creating a Power BI Schedule and using its dataset toocreate a simple report.</span></span>  <span data-ttu-id="5e928-158">이 예제에서는 일련의 컴퓨터에 대 한 모든 성능 데이터 내보낸된 tooPower BI 이며 선 그래프 toodisplay 프로세서 사용률을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-158">In this example, all performance data for a set of computers is exported tooPower BI and then a line graph is created toodisplay processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="5e928-159">로그 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="5e928-159">Create log search</span></span>
<span data-ttu-id="5e928-160">Toosend toohello dataset 한다고 hello 데이터에 대 한 로그 검색을 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-160">We start by creating a log search for hello data that we want toosend toohello dataset.</span></span>  <span data-ttu-id="5e928-161">이 예제에서는 *srv*로 시작하는 이름의 컴퓨터에 대한 모든 성능 데이터를 반환하는 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI 일정](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="5e928-163">Power BI 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="5e928-163">Create Power BI Search</span></span>
<span data-ttu-id="5e928-164">Hello 클릭 **Power BI** tooopen hello Power BI 대화 상자 단추 및 hello 필요한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-164">We click hello **Power BI** button tooopen hello Power BI dialog and provide hello required information.</span></span>  <span data-ttu-id="5e928-165">이 검색 toorun 시간 마다 한 번씩 원하는 하 고 라는 데이터 집합을 만들 *Contoso 성능*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-165">We want this search toorun once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="5e928-166">Hello 기본값인 방지 개이므로 이미 hello 데이터를 원하는 만듭니다 hello 검색 열기, *현재 검색 쿼리 사용* 에 대 한 **저장 된 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-166">Since we already have hello search open that creates hello data we want, we keep hello default of *Use current search query* for **Saved Search**.</span></span>

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="5e928-168">Power BI 검색 확인</span><span class="sxs-lookup"><span data-stu-id="5e928-168">Verify Power BI Search</span></span>
<span data-ttu-id="5e928-169">tooverify hello 일정을 올바르게 만든 म, म hello에서 Power BI 검색 hello 목록을 볼 **설정** hello OMS 대시보드에 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-169">tooverify that we created hello schedule correctly, we view hello list of Power BI Searches under hello **Settings** tile in hello OMS dashboard.</span></span>  <span data-ttu-id="5e928-170">몇 분 정도 기다린 하 고 보고 hello 동기화가 실행 될 때까지이 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-170">We wait several minutes and refresh this view until it reports that hello sync has been run.</span></span>

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a><span data-ttu-id="5e928-172">Power BI에서 데이터 집합 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-172">Verify hello dataset in Power BI</span></span>
<span data-ttu-id="5e928-173">이 계정에 로그인 했습니다 [powerbi.microsoft.com](http://powerbi.microsoft.com/) 너무 스크롤하여**데이터 집합** hello hello 왼쪽된 창의 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll too**Datasets** at hello bottom of hello left pane.</span></span>  <span data-ttu-id="5e928-174">해당 hello 볼 수 있습니다 *Contoso 성능* 우리의 내보내기 성공적으로 실행 되었음을 나타내는 데이터 집합 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-174">We can see that hello *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI 데이터 집합](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="5e928-176">데이터 집합 기반 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="5e928-176">Create report based on dataset</span></span>
<span data-ttu-id="5e928-177">Hello 선택 **Contoso 성능** 데이터 집합을 클릭 하 고 **결과** hello에 **필드** 이 데이터 집합의 일부인 hello 오른쪽 tooview hello 필드에는 창입니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-177">We select hello **Contoso Perf** dataset and then click on **Results** in hello **Fields** pane on hello right tooview hello fields that are part of this dataset.</span></span>  <span data-ttu-id="5e928-178">각 컴퓨터에 대 한 선 그래프 보여 주는 프로세서 사용률 toocreate hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-178">toocreate a line graph showing processor utilization for each computer, we perform hello following actions.</span></span>

1. <span data-ttu-id="5e928-179">Hello 꺾은선형 차트 시각화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-179">Select hello Line chart visualization.</span></span>
2. <span data-ttu-id="5e928-180">끌기 **ObjectName** 너무**보고서 수준 필터** 확인 **프로세서**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-180">Drag **ObjectName** too**Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="5e928-181">끌기 **: _total CounterName** 너무**보고서 수준 필터** 확인 **% Processor Time**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-181">Drag **CounterName** too**Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="5e928-182">끌기 **CounterValue** 너무**값**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-182">Drag **CounterValue** too**Values**.</span></span>
5. <span data-ttu-id="5e928-183">끌기 **컴퓨터** 너무**범례**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-183">Drag **Computer** too**Legend**.</span></span>
6. <span data-ttu-id="5e928-184">끌기 **TimeGenerated** 너무**축**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-184">Drag **TimeGenerated** too**Axis**.</span></span>

<span data-ttu-id="5e928-185">이 데이터 집합의 hello 데이터로 해당 hello 결과 선 그래프를 표시 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-185">We can see that hello resulting line graph is displayed with hello data from our dataset.</span></span>

![Power BI 꺾은선형 그래프](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a><span data-ttu-id="5e928-187">Hello 보고서 저장</span><span class="sxs-lookup"><span data-stu-id="5e928-187">Save hello report</span></span>
<span data-ttu-id="5e928-188">Hello를 클릭 하 여 hello 보고서 저장 우리 hello hello 화면 위쪽에 단추를 저장 하 고 hello 왼쪽된 창에서 hello 보고서 섹션에 나열 된 이제 유효성 검사.</span><span class="sxs-lookup"><span data-stu-id="5e928-188">We save hello report by clicking on hello Save button at hello top of hello screen and validate that it is now listed in hello Reports section in hello left pane.</span></span>

![Power BI 보고서](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="5e928-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e928-190">Next steps</span></span>
* <span data-ttu-id="5e928-191">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) toobuild 쿼리 될 수 있는 내보낸 tooPower BI 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-191">Learn about [log searches](log-analytics-log-searches.md) toobuild queries that can be exported tooPower BI.</span></span>
* <span data-ttu-id="5e928-192">에 대 한 자세한 내용은 [Power BI](http://powerbi.microsoft.com) 내보내기 로그 분석에 따라 toobuild 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e928-192">Learn more about [Power BI](http://powerbi.microsoft.com) toobuild visualizations based on Log Analytics exports.</span></span>
