---
title: "Azure 로그 분석에서 aaaUsing hello 로그 검색 포털 | Microsoft Docs"
description: "이 문서에 toocreate 로그를 검색 하 고 hello 로그 검색 포털을 사용 하 여 로그 분석 작업 영역에 저장 된 데이터를 분석 하는 방법을 설명 하는 자습서에 포함 됩니다.  서로 다른 유형의 데이터를 tooreturn 간단한 쿼리를 실행 하 고 결과 분석 hello 자습서에 포함 됩니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="a385c-104">Hello 로그 검색 포털을 사용 하는 Azure 로그 분석에서 로그 검색을 만들려면</span><span class="sxs-lookup"><span data-stu-id="a385c-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="a385c-105">이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 로그 검색 포털 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="a385c-106">Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="a385c-107">작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md) hello hello 로그 검색 포털의 최신 버전에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="a385c-108">이 문서에 toocreate 로그를 검색 하 고 hello 로그 검색 포털을 사용 하 여 로그 분석 작업 영역에 저장 된 데이터를 분석 하는 방법을 설명 하는 자습서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="a385c-109">서로 다른 유형의 데이터를 tooreturn 간단한 쿼리를 실행 하 고 결과 분석 hello 자습서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="a385c-110">직접 수정 하지 않고 hello 쿼리를 수정에 대 한 hello 로그 검색 포털의 기능에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="a385c-111">Hello 쿼리를 직접 편집에 대 한 자세한 내용은 참조 hello [쿼리 언어 참조](https://go.microsoft.com/fwlink/?linkid=856079)합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="a385c-112">hello 로그 검색 포털 대신 hello 고급 분석 포털에서 toocreate 검색 참조 [hello 분석 포털 시작](https://go.microsoft.com/fwlink/?linkid=856587)합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="a385c-113">두 포털 hello를 사용 하 여 동일한 쿼리 언어 tooaccess hello hello 로그 분석 작업 영역에서 같은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a385c-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a385c-114">Prerequisites</span></span>
<span data-ttu-id="a385c-115">이 자습서 쿼리 tooanalyze hello에 대 한 데이터를 생성 하는 하나 이상의 연결 된 원본에 있는 로그 분석 작업 영역이 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="a385c-116">작업 영역에 없으면 무료 하나 만들 수 있습니다에 hello 절차를 사용 하 여 [로그 분석 작업 영역 시작](log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="a385c-117">하나 이상의 연결 [Windows 에이전트](log-analytics-windows-agents.md) 또는 한 개의 [Linux 에이전트](log-analytics-linux-agents.md) toohello 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="a385c-118">열기 hello 로그 검색 포털</span><span class="sxs-lookup"><span data-stu-id="a385c-118">Open hello Log Search portal</span></span>
<span data-ttu-id="a385c-119">Hello 로그 검색 포털을 열어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="a385c-120">Hello Azure 포털 또는 hello OMS 포털에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="a385c-121">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="a385c-122">분석 tooLog 찾아서 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="a385c-123">선택 하거나 **로그 검색** Azure 포털 또는 시작 hello OMS 포털을 선택 하 여 hello에 toostay **OMS 포털** hello 로그 검색 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![로그 검색 단추](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="a385c-125">단순 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="a385c-125">Create a simple search</span></span>
<span data-ttu-id="a385c-126">가장 빠른 방법은 tooretrieve hello와 일부 데이터 toowork 테이블의 모든 레코드를 반환 하는 간단한 쿼리를입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="a385c-127">경우 모든 windows 또는 Linux 클라이언트 연결 된 tooyour 작업 영역 데이터 이벤트 (Windows) 또는 Syslog (Linux) 테이블 하거나 hello에 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="a385c-128">하나의 hello 쿼리 hello 검색 상자에 다음을 입력 하 고 hello 검색 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="a385c-129">Hello 기본 목록 보기에 데이터가 반환 됩니다 하 고 반환 된 총 레코드 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![단순 쿼리](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="a385c-131">만 hello 각 레코드의 첫 번째 몇 가지 속성 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="a385c-132">클릭 **자세히 표시** toodisplay 특정 레코드에 대 한 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="a385c-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![레코드 세부 정보](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="a385c-134">Hello 시간 범위 설정</span><span class="sxs-lookup"><span data-stu-id="a385c-134">Set hello time scope</span></span>
<span data-ttu-id="a385c-135">로그 분석에 의해 수집 된 모든 레코드에는 **TimeGenerated** 해당 hello 레코드가 생성 된 hello 날짜 및 시간을 포함 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="a385c-136">Hello 로그 검색 포털에서 쿼리 된 레코드만 반환는 **TimeGenerated** hello hello 화면의 왼쪽에 표시 되는 hello 시간 범위 내에서.</span><span class="sxs-lookup"><span data-stu-id="a385c-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="a385c-137">Hello 드롭다운을 선택 하거나 hello 슬라이더를 수정 하 여 hello 시간 필터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="a385c-138">hello 슬라이더 hello 상대 hello 범위 내에서 각 시간 세그먼트에 대 한 레코드 수를 표시 하는 막대 그래프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="a385c-139">이 세그먼트는 hello 범위에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="a385c-140">hello 기본 시간 범위는 **1 일**합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="a385c-141">이 값도 변경**7 일**, 및 hello 레코드의 총 수는 증가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![날짜 시간 범위](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="a385c-143">Hello 쿼리의 결과 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-143">Filter results of hello query</span></span>
<span data-ttu-id="a385c-144">Hello에 hello 화면 왼쪽에는 직접 수정 하지 않고 필터링 toohello 쿼리 tooadd 수 있는 hello 필터 창입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="a385c-145">반환 된 hello 레코드의 여러 속성을 해당 레코드 수와 상위 10 개의 값과 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="a385c-146">작업 하는 경우 **이벤트**, 선택 hello 확인란 옆 너무**오류** 아래 **EVENTLEVELNAME**합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="a385c-147">작업 하는 경우 **Syslog**, 선택 hello 확인란 옆 너무**err** 아래 **SEVERITYLEVEL**합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="a385c-148">이 변경의 hello toolimit hello 다음 tooone 결과 tooerror 이벤트 hello 쿼리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="a385c-150">선택 하 여 추가 속성 toohello 필터 창 **toofilters 추가** hello 속성 메뉴에서 hello 레코드 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Toofilter 메뉴 추가](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="a385c-152">동일한 필터를 선택 하 여 hello를 설정할 수 있습니다 **필터** toofilter hello 값이 있는 레코드에 대 한 hello 속성 메뉴에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="a385c-153">Hello를 하나만 **필터** 파란색에 있는 이름 사용 하 여 속성에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="a385c-154">이러한 필드는 검색 조건에 대해 인덱싱되는 *검색 가능* 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="a385c-155">회색 필드는 *텍스트로 검색 가능한 자유* hello에만 있는 필드 **참조 표시** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="a385c-156">이 옵션은 속성에 해당 값이 포함된 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-156">This option returns records that have that value in any property.</span></span>

![필터 메뉴](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="a385c-158">Hello를 선택 하 여 단일 속성에 대 한 hello 결과 그룹화 할 수 있습니다 **그룹화** hello 레코드 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="a385c-159">이렇게 하면 추가 됩니다 한 [요약](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) hello 결과 차트에 표시 하는 연산자 tooyour 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="a385c-160">둘 이상의 속성을 그룹화 할 수 있습니다 하지만 tooedit hello 쿼리를 직접 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="a385c-161">선택 hello 레코드 메뉴 다음 hello hello **컴퓨터** 속성과 선택 **Group by 'Computer'**합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![컴퓨터를 기준으로 그룹화](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="a385c-163">결과 작업</span><span class="sxs-lookup"><span data-stu-id="a385c-163">Work with results</span></span>
<span data-ttu-id="a385c-164">hello 로그 검색 포털에는 다양 한 쿼리 결과 hello 사용 하기 위한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="a385c-165">정렬할 수 있습니다, 필터 및 그룹 tooanalyze hello 데이터 hello 실제 쿼리를 수정 하지 않고 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="a385c-166">기본적으로 쿼리 결과는 정렬되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="a385c-167">tooview hello 데이터를 필터링 및 정렬에 대 한 추가 옵션을 제공 하는 테이블 형식 클릭 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![테이블 보기](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="a385c-169">해당 레코드에 대 한 레코드 tooview hello 세부 정보에서 hello 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![결과 정렬](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="a385c-171">필드의 열 머리글을 클릭하여 필드를 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-171">Sort on any field by clicking on its column header.</span></span>

![결과 정렬](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="a385c-173">Hello 필터 단추를 클릭 하 고 필터 조건을 제공 하 여 hello 열에 특정 값에 hello 결과 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![결과 필터링](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="a385c-175">Hello 결과의 열 머리글 toohello 위쪽을 끌어서 열을 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="a385c-176">여러 열 toohello 위쪽을 끌어서 여러 필드에서 그룹화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![결과 그룹화](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="a385c-178">성능 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="a385c-178">Work with performance data</span></span>
<span data-ttu-id="a385c-179">Windows 및 Linux 에이전트에 대 한 성능 데이터는 hello에 hello 로그 분석 작업 영역에 저장 **성능** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="a385c-180">성능 레코드는 다른 레코드와 비슷하며, 이벤트와 마찬가지로 모든 성능 레코드를 반환하는 단순 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![성능 데이터](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="a385c-182">모든 성능 개체와 카운터의 레코드 수백만 개가 반환된다면 원하는 데이터를 찾기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="a385c-183">동일한 방법을 hello 다음을 입력 하거나 toofilter hello 데이터 위에 사용 하면 쿼리 hello hello 로그 검색 상자에 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="a385c-184">이 경우 Windows 및 Linux 컴퓨터의 프로세서 사용률 레코드만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![프로세서 사용률](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="a385c-186">이 인해 hello 데이터 tooa 특정 카운터에 제한 하기는 하지만 것 여전히 하지 않습니다는 특히 유용 형태로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="a385c-187">Hello 데이터는 꺾은선형 차트를 표시할 수 있지만 toogroup 먼저 컴퓨터와 TimeGenerated 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="a385c-188">여러 필드에 대해 toogroup, 해야 toomodify hello 쿼리를 직접 hello 쿼리 toohello 다음 하므로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="a385c-189">Hello를 사용 하 여이 [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) 함수 hello에 **CounterValue** 속성 toocalculate hello 각 1 시간 동안 평균 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![성능 데이터 차트](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="a385c-191">Hello 데이터를 그룹화 하는 적절 하 게 했으므로 표시할 수 있습니다 시각적 차트에 hello를 추가 하 여 [렌더링](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![꺾은선형 차트](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="a385c-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a385c-193">Next steps</span></span>

- <span data-ttu-id="a385c-194">Hello 로그 분석 쿼리 언어에 대 한 자세한 [hello 분석 포털 시작](https://go.microsoft.com/fwlink/?linkid=856079)합니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="a385c-195">Hello를 사용 하 여 자습서 살펴보면서 [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587) toorun hello 수 있는 동일한 쿼리 및 액세스 hello hello 로그 검색 포털와 동일한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a385c-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
