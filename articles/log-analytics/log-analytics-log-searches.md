---
title: "Azure 로그 분석에서 로그 검색을 사용 하 여 aaaFind 데이터 | Microsoft Docs"
description: "로그 검색 toocombine 사용 하면 사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결 하 고 있습니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="ddaf9-103">Log Analytics에서 로그 검색을 사용하여 데이터 찾기</span><span class="sxs-lookup"><span data-stu-id="ddaf9-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="ddaf9-104">이 문서에서는 로그 분석에 hello 현재 쿼리 언어를 사용 하 여 로그 검색을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="ddaf9-105">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 너무 참조 해야 하는 다음[로그 분석 (새)에 있는 이해 로그 검색](log-analytics-log-search-new.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="ddaf9-106">사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결 하 고 로그 분석의 hello 핵심은 toocombine 수 있는 hello 로그 검색 기능.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="ddaf9-107">솔루션에서 특정 문제 영역 주위에 피벗 된 메트릭을 하면 로그 검색 toobring 제공 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="ddaf9-108">Hello 검색 페이지에서 쿼리를 만들 수 있습니다 및 다음 검색 하는 경우 필터링 할 수 있습니다 hello 결과 패싯 컨트롤을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="ddaf9-109">또한 결과 tootransform 고급 쿼리, 필터 및 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="ddaf9-110">일반적인 로그 검색 쿼리는 대부분의 솔루션 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="ddaf9-111">Hello OMS 콘솔에서 타일을 클릭 하거나 로그 검색을 사용 하 여 hello 항목에 대 한 세부 정보 tooview을 tooother 항목에서 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="ddaf9-112">이 자습서에서는 살펴봅니다 예제 toocover 모든 hello 기본 로그 검색을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="ddaf9-113">다음에 빌드 방법을 toouse hello 구문 tooextract hello insights에서에서 원하는 hello 데이터에 대 한 실용적인 사용 사례에 대 한 이해가 얻을 수 있도록 알아보고 간단 하 고 실용적인 예제부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="ddaf9-114">검색 기법을 알아본 후 hello을 검토할 수 있습니다 [로그 분석 로그 검색 참조](log-analytics-search-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="ddaf9-115">기본 필터 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-115">Use basic filters</span></span>
<span data-ttu-id="ddaf9-116">hello 먼저 tooknow는 hello 첫 번째 부분의 앞 검색 쿼리를 "|" 세로줄 문자는 항상 한 *필터*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="ddaf9-117">TSQL에서 WHERE 절로 결정의 생각할 수 *어떤* hello OMS 데이터 저장소에서 데이터 toopull의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="ddaf9-118">Hello 데이터 저장소에서 검색은 대개 지정 하므로 쿼리가 WHERE 절 hello로 시작 하는 자연 tooextract, 원하는 hello 데이터의 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="ddaf9-119">hello 사용할 수 있는 가장 기본적인 필터는 *키워드*'오류' 또는 '시간 제한' 또는 컴퓨터 이름과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="ddaf9-120">이러한 유형의 간단한 쿼리는 일반적으로 다양 한 도형을 반환할 hello 내 데이터의 동일한 결과 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="ddaf9-121">로그 분석에 다른 때문에 이것이 *형식* hello 시스템의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="ddaf9-122">단순 검색 tooconduct</span><span class="sxs-lookup"><span data-stu-id="ddaf9-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="ddaf9-123">Hello OMS 포털에서 클릭 **로그 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="ddaf9-124">![검색 타일](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="ddaf9-125">Hello 쿼리 필드에 입력 `error` 클릭 하 고 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="ddaf9-126">![검색 오류](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="ddaf9-127">에 대 한 예를 들어 hello 쿼리 `error` hello 다음 이미지 반환 100000 **이벤트** 레코드 (로그 관리에서 수집), 18 **ConfigurationAlert** 레코드 (구성으로 생성 합니다. 평가) 및 12 **ConfigurationChange** 레코드 (hello 변경 내용 추적에서 캡처) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="ddaf9-128">![검색 결과](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="ddaf9-129">이러한 필터는 실제로 개체 유형/클래스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="ddaf9-130">*형식* 은 한 개의 태그, 또는 속성, 또는 문자열/이름/범주 이며 있는 tooa 하나의 데이터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="ddaf9-131">Hello 시스템의 일부 문서 분류 **유형: ConfigurationAlert** 고 일부는 **유형: 성능**, 또는 **유형: 이벤트**등.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="ddaf9-132">각 검색 결과, 문서, 레코드 또는 항목의 데이터를 이러한 각 작업에 대 한 hello 원시 속성 및 해당 값 표시 및 사용 하 여 이러한 필드 이름은 toospecify hello 필터에서 tooretrieve hello 레코드만 하려는 경우 여기서 hello 필드에 지정 된이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="ddaf9-133">*유형*은 실제로 모든 레코드가 있는 필드이며 다른 필드와 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="ddaf9-134">Hello 형식 필드의 hello 값을 기준으로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="ddaf9-135">해당 레코드를 다른 형태 또는 모습을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-135">That record will have a different shape or form.</span></span> <span data-ttu-id="ddaf9-136">참고로, **유형 = Perf**, 또는 **유형 =** 성능 데이터 또는 이벤트에 대 한 toolearn tooquery 할 hello 구문 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="ddaf9-137">Hello 필드 이름 및 hello 값 앞에 콜론 (:) 또는 등호 (=) 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="ddaf9-138">**Type: Event** 및 **유형 =** 에 해당 하는 의미를 선택할 수 있습니다 hello 원하는 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="ddaf9-139">따라서 경우 hello 형식 = Perf 레코드 'CounterName' 라는 필드가 있는 다음 비슷한 쿼리를 작성할 수 있습니다 `Type=Perf CounterName="% Processor Time"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="ddaf9-140">이렇게 하면 있습니다 hello 성능 데이터만 hello 성능 카운터 이름 "% Processor Time"입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="ddaf9-141">프로세서 시간 성능 데이터에 대 한 toosearch</span><span class="sxs-lookup"><span data-stu-id="ddaf9-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="ddaf9-142">Hello 검색 쿼리 필드에 입력`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="ddaf9-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="ddaf9-143">더 정확 하 게 하 고 사용할 수도 있습니다 **InstanceName = _'total '** Windows 성능 카운터는 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="ddaf9-144">또한 패싯 및 다른 **field:value**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="ddaf9-145">hello 필터 hello 쿼리 표시줄에 tooyour 필터를 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="ddaf9-146">다음 이미지는 hello에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-146">You can see this in hello following image.</span></span> <span data-ttu-id="ddaf9-147">표시 여기서 tooclick tooadd **InstanceName: '_Total'** 아무것도 입력 하지 않고 toohello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![검색 패싯](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="ddaf9-149">쿼리는 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="ddaf9-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="ddaf9-150">이 예제에서는 toospecify 없는 **유형 = Perf** tooget toothis 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="ddaf9-151">Hello 필드 CounterName 및 InstanceName 종류의 레코드에만 존재 하므로 = Perf, hello 쿼리는 모호한 tooreturn hello 동일한 결과 더 긴 이전과 hello:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="ddaf9-152">이 hello 쿼리에서 모든 hello 필터에 있는 것으로 평가 되기 때문 *AND* 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="ddaf9-153">효과적으로 hello toohello 조건을 추가 하면 필드 더 할수록 더 구체적이 고 구체화 된 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="ddaf9-154">예를 들어 hello 쿼리 `Type=Event EventLog="Windows PowerShell"` 는 너무 동일`Type=Event AND EventLog="Windows PowerShell"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="ddaf9-155">로그인 하 고 hello Windows PowerShell 이벤트 로그에서 수집 된 모든 이벤트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="ddaf9-156">추가 하는 경우 필터를 여러 번 반복 해 서 hello 동일한 패싯을 다음 hello 문제는 순수 하 게 외관상 hello 검색 표시줄을 채울 수 있지만 여전히 결과 반환 hello 같은 hello 암시적 AND 연산자가 항상 있기 때문에 선택 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="ddaf9-157">NOT 연산자를 명시적으로 사용 하 여 쉽게 암시적 AND 연산자 hello를 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="ddaf9-158">예:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-158">For example:</span></span>

<span data-ttu-id="ddaf9-159">`Type:Event NOT(EventLog:"Windows PowerShell")`또는 이와 동등한 `Type=Event EventLog!="Windows PowerShell"` hello Windows PowerShell 로그 되지 않은 모든 로그에서 모든 이벤트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="ddaf9-160">또는 'OR'같은 다른 부울 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="ddaf9-161">hello 다음 쿼리는 hello에 대 한 이벤트 로그는 두 응용 프로그램 또는 시스템 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="ddaf9-162">위의 쿼리는 hello를 사용 하 여 항목 얻을 수 있습니다 both 로그에 대 한 hello에서 동일한 결과 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="ddaf9-163">그러나 hello 또는 hello 암시적 AND 두어 위치를 제거 하면 다음 hello 다음 쿼리 생성 하지 않습니다 결과 tooBOTH 로그에 속하는 이벤트 로그 항목이 없기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="ddaf9-164">각 이벤트 로그 항목 tooonly hello 두 로그 중 하나 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="ddaf9-165">추가 필터 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-165">Use additional filters</span></span>
<span data-ttu-id="ddaf9-166">hello 다음 쿼리는 반환 데이터를 전송 하는 모든 hello 컴퓨터에 대 한 2 개의 이벤트 로그에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![검색 결과](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="ddaf9-168">Hello 필드 또는 필터 중 하나를 선택 하면 hello 쿼리 tooa 제외 특정 컴퓨터를 모든 다른 좁혀집니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="ddaf9-169">hello 결과 쿼리는 hello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="ddaf9-170">Hello 때문에 해당 하는 toohello 다음 변수인 암시적 and.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="ddaf9-171">각 쿼리 명시적 순서에 따라 hello에 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="ddaf9-172">참고 hello 괄호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="ddaf9-173">Hello 이벤트 로그 필드와 마찬가지로 추가 하 여 특정 컴퓨터 집합에 대 한 데이터를 검색할 수 있습니다 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="ddaf9-174">예:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="ddaf9-175">마찬가지로, 다음 쿼리 반환이이 hello **CPU 시간 %** hello 두 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="ddaf9-176">필드 형식</span><span class="sxs-lookup"><span data-stu-id="ddaf9-176">Field types</span></span>
<span data-ttu-id="ddaf9-177">필터를 만들 때 다양 한 유형의 필드를 로그 검색에서 반환 된 작업의 hello 차이 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="ddaf9-178">**검색 가능한 필드**는 검색 결과에 파란색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="ddaf9-179">Hello 다음과 같은 검색 조건 특정 toohello 필드에 검색 가능한 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="ddaf9-180">**자유 텍스트 검색 가능 필드**는 검색 결과에서 회색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="ddaf9-181">검색 가능한 필드와 같은 검색 조건 특정 toohello 필드와 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="ddaf9-182">값 형식은 hello 다음과 같은 모든 필드에서 쿼리를 수행할 때 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="ddaf9-183">부울 연산자</span><span class="sxs-lookup"><span data-stu-id="ddaf9-183">Boolean operators</span></span>
<span data-ttu-id="ddaf9-184">날짜/시간 및 숫자 필드를 사용하여 *보다 큼*, *보다 작음*, *보다 작거나 같음*을 사용하는 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="ddaf9-185">와 같은 간단한 연산자를 사용할 수 있습니다 >, <>, =, < =,! = hello 쿼리 검색 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="ddaf9-186">특정 기간에 특정 이벤트 로그를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="ddaf9-187">예를 들어 hello 지난 24 시간 동안은 표현 다음 mnemonic 식 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="ddaf9-188">부울 연산자를 사용 하 여 toosearch</span><span class="sxs-lookup"><span data-stu-id="ddaf9-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="ddaf9-189">Hello 검색 쿼리 필드에 입력`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="ddaf9-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="ddaf9-190">![부울 값을 사용하여 검색](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="ddaf9-191">제어할 수 있지만 시간 간격을 그래픽으로 hello 하 고 대부분의 시간 toodo 발생 하는 이점을 tooincluding hello 쿼리에 직접 시간 필터를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="ddaf9-192">예를 들어이 방식은 효과적 hello에 관계 없이 각 타일에 대 한 hello 시간을 재정의할 수 대시보드와 *글로벌* hello 대시보드 페이지에서 시간 선택기입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="ddaf9-193">자세한 내용은 [대시보드에서 시간 문제](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="ddaf9-194">시간별으로 필터링 하는 경우 유의 hello에 대 한 결과 얻을 *교차* hello의 두 기간의: hello OMS 포털 (S1)에 지정 된 hello 및 hello 쿼리 (S2)에 지정 된 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![교집합](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="ddaf9-196">즉, hello 기간이 교차 하지 않는, 예를 들어 선택할 수 있는 hello OMS 포털의 경우 **이번 주** hello 쿼리에서 정의 하는 경우 **지난주**, 교차가 없습니다 및 사용자가 없습니다 어떤 결과도 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="ddaf9-197">Hello TimeGenerated 필드에 사용 되는 비교 연산자가 다른 경우에도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="ddaf9-198">예를 들어 숫자 필드를 사용하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-198">For example, with numeric fields.</span></span>

<span data-ttu-id="ddaf9-199">예를 들어을 가진다 고 구성 평가 경고 심각도 값을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="ddaf9-200">0 = 정보</span><span class="sxs-lookup"><span data-stu-id="ddaf9-200">0 = Information</span></span>
* <span data-ttu-id="ddaf9-201">1 = 경고</span><span class="sxs-lookup"><span data-stu-id="ddaf9-201">1 = Warning</span></span>
* <span data-ttu-id="ddaf9-202">2 = 중요</span><span class="sxs-lookup"><span data-stu-id="ddaf9-202">2 = Critical</span></span>

<span data-ttu-id="ddaf9-203">경고 및 위험 경고에 대 한 쿼리 및 다음 쿼리는 hello 쿼리하고 정보를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="ddaf9-204">범위 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-204">You can also use range queries.</span></span> <span data-ttu-id="ddaf9-205">즉, 시퀀스에 있는 값의 hello 시작 및 끝 범위를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="ddaf9-206">예를 들어 여기서 hello hello Operations Manager 이벤트 로그에서 이벤트를 하려는 경우 EventID가 보다 크거나 같은 too2100 넘지 않는, 2199 hello 다음 쿼리는 이벤트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="ddaf9-207">hello 사용 해야 하는 범위 구문은 hello 콜론 (:) field: value 구분 기호 및 *하지* hello 등호 (=) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="ddaf9-208">Hello 범위의 hello 아래쪽과 위쪽 끝 대괄호로 묶고 두 마침표 (.)로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="ddaf9-209">검색 결과 조작</span><span class="sxs-lookup"><span data-stu-id="ddaf9-209">Manipulate search results</span></span>
<span data-ttu-id="ddaf9-210">데이터를 검색할 때 검색 쿼리 toorefine 원하는 고 hello 결과 대 한 제어를 어느 정도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="ddaf9-211">결과가 검색 되 면 명령을 tootransform를 적용할 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="ddaf9-212">로그 분석 검색에서 명령은 *해야* hello 세로줄 문자 (|) 뒤 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="ddaf9-213">필터는 쿼리 문자열의 첫 번째 부분 hello 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="ddaf9-214">작업할 때 hello 데이터 집합을 정의 하 고 "파이프" 합니다 그 결과 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="ddaf9-215">Hello 파이프 tooadd 추가 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="ddaf9-216">이것은 느슨하게 비슷한 toohello Windows PowerShell 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="ddaf9-217">로그 분석 검색 언어 hello toofollow PowerShell 스타일 및 지침 toomake를 시도 하는 일반적으로 it 비슷한 toohello IT 전문가 및 tooease hello 배워야 할 필요성이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="ddaf9-218">명령은 동사의 이름이 있으므로 수행할 작업을 쉽게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="ddaf9-219">정렬</span><span class="sxs-lookup"><span data-stu-id="ddaf9-219">Sort</span></span>
<span data-ttu-id="ddaf9-220">hello 정렬 명령 toodefine hello를 하나 또는 여러 필드에서 순서를 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="ddaf9-221">기본적으로 사용하지 않아도 시간 내림차순으로 정렬되도록 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="ddaf9-222">hello 가장 최근의 결과가 검색 결과의 hello 위쪽에 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="ddaf9-223">즉, `Type=Event EventID=1234` 로 검색을 실행하면 실제로 실행되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="ddaf9-224">Hello 유형의 로그를 잘 알고 있다면 경험을 이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="ddaf9-225">예를 들어 Windows 이벤트 뷰어 안녕하세요에.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="ddaf9-226">Toochange hello 방식으로 결과 반환 하는 정렬을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="ddaf9-227">hello 다음 예제에서는이 과정</span><span class="sxs-lookup"><span data-stu-id="ddaf9-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="ddaf9-228">hello 위의 간단한 예제 알려주는 명령이 작동 하는 방법을 hello 필터를 반환 하는 hello 결과의 hello 형태를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="ddaf9-229">제한 및 위쪽</span><span class="sxs-lookup"><span data-stu-id="ddaf9-229">Limit and top</span></span>
<span data-ttu-id="ddaf9-230">덜 알려진 다른 명령에는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="ddaf9-231">제한은 PowerShell같은 동사입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="ddaf9-232">제한은 TOP 명령과 기능적으로 동일한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="ddaf9-233">hello 쿼리인 hello 동일한 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="ddaf9-234">top를 사용 하 여 toosearch</span><span class="sxs-lookup"><span data-stu-id="ddaf9-234">toosearch using top</span></span>
* <span data-ttu-id="ddaf9-235">Hello 검색 쿼리 필드에 입력`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="ddaf9-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="ddaf9-236">![상위 검색](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="ddaf9-237">위 hello 이미지에서 된 358 천 레코드가 EventID = 600입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="ddaf9-238">필드, 패싯 및 왼쪽 항상 반환 된 hello 결과 대 한 정보를 표시 하는 hello에 대 한 필터 hello *hello 필터 부분에 의해* 모든 파이프 문자 앞 hello 참가 하는 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="ddaf9-239">hello **결과** hello 예제 명령이 모양을 만들고 hello 결과 변환 하기 때문에 창 hello 가장 최근 1 개의 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="ddaf9-240">여기서</span><span class="sxs-lookup"><span data-stu-id="ddaf9-240">Select</span></span>
<span data-ttu-id="ddaf9-241">hello SELECT 명령은 PowerShell에서 Select-object 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="ddaf9-242">자신의 원래 속성을 모두 갖지 않는 필터된 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="ddaf9-243">대신 사용자가 지정한 hello 속성만 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="ddaf9-244">select 명령 hello를 사용 하 여 검색 한 toorun</span><span class="sxs-lookup"><span data-stu-id="ddaf9-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="ddaf9-245">검색에서 `Type=Event` 을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="ddaf9-246">클릭 **+ 자세히 표시** hello 결과 tooview 결과 hello 하는 모든 hello 속성 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="ddaf9-247">그 중 일부를 명시적으로 및 선택 hello 쿼리 변경 내용을 너무`Type=Event | Select Computer,EventID,RenderedDescription`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="ddaf9-248">![선택 검색](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="ddaf9-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="ddaf9-249">이 명령은 toocontrol 검색 출력을 종종 hello 전체 레코드는 아닙니다 하 고 탐색을 위한 중요 데이터의 hello 부분만 선택 하는 경우에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="ddaf9-250">이 기능은 다른 유형의 레코드들이 *일부* 공통 속성이 있지만 *일부* 속성은 공통이 아닌 경우에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="ddaf9-251">는 테이블 처럼 더 자연스럽 게는 출력을 생성 하거나 tooa CSV 파일을 내보낸 다음 Excel에서 massaged 되는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="ddaf9-252">Hello 측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-252">Use hello measure command</span></span>
<span data-ttu-id="ddaf9-253">측정값은 hello 로그 분석 검색에서 가장 용도가 넓은 함수로 명령 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="ddaf9-254">있습니다 tooapply 통계 *함수* tooyour 데이터 및 집계 결과 지정된 된 필드를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="ddaf9-255">측정값이 지원하는 여러 통계 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="ddaf9-256">개수() 측정</span><span class="sxs-lookup"><span data-stu-id="ddaf9-256">Measure count()</span></span>
<span data-ttu-id="ddaf9-257">hello, 첫 번째 통계 함수로 toowork 및 가장 간단한 toounderstand hello 중 하나는 hello *count ()* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="ddaf9-258">와 같은 모든 검색 쿼리에서 나온 결과 `Type=Event`, hello 검색 결과의 왼쪽에 패싯이 라는 필터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="ddaf9-259">hello 필터 실행 된 hello 검색에서 지정된 된 필드 hello 결과에 의해 값의 분포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="ddaf9-261">예를 들어 hello 이미지 위의 살펴보겠습니다 hello **컴퓨터** 필드가 hello 739 천 거의에서 이벤트 내 hello 결과 표시 68 고유한 특정 값에 대 한 hello **컴퓨터** 해당 레코드에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="ddaf9-262">hello 타일이 표시 hello hello 가장 일반적인 5 개의 값인 hello로 작성 된 상위 5 **컴퓨터** 필드), 해당 필드에 특정 값을 포함 하는 문서 hello 수로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="ddaf9-263">Hello 이미지에는 –는 거의 369 천 이벤트 중 90 천 hello OpsInsights04.contoso.com 컴퓨터 83 천 hello DB03.contoso.com 컴퓨터에서에서 제공 하 고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="ddaf9-264">어떻게 할까요 toosee 모든 값 hello 타일 표시 하므로 hello 상위 5?</span><span class="sxs-lookup"><span data-stu-id="ddaf9-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="ddaf9-265">Hello 측정값 즉 명령을 hello count () 함수를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="ddaf9-266">이 함수는 매개 변수를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="ddaf9-267">Hello 필드를 기준으로 – hello toogroup 사용할 지정 **컴퓨터** 이 경우 필드:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="ddaf9-269">하지만 **컴퓨터**는 각 데이터*에서* 사용되는 필드입니다. 관련된 관계 데이터베이스가 없고 별도의 **컴퓨터** 개체는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="ddaf9-270">방금 값 hello *에* , 및 여러 다른 특성과 측면 hello 데이터를 생성 한 엔터티 데이터를 설명할 수 hello 따라서 hello 용어 *패싯*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="ddaf9-271">그러나 다른 필드에 의해 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="ddaf9-272">Hello hello 측정값 명령으로 파이프 하는 거의 739 천 이벤트의 원래 결과는 또한 라는 필드가 있기 때문에 **EventID**를 적용할 수 있습니다 하 여 해당 필드로 동일한 기술을 toogroup hello 하 고 EventID로 이벤트의 개수를 가져올:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="ddaf9-273">경우 특정 값을 포함 하는 hello 실제 레코드 개수에 관심이 모르겠으면 되지만 대신의 목록을 원하는 경우 hello 값 자체를 추가할 수는 *선택* 선택 hello 첫 번째 열 및 hello 끝나기 전에 명령을:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="ddaf9-274">더 복잡해 하 고 미리 hello 쿼리에서 hello 결과 정렬할 수 다음 또는 hello 표의 hello 열을 너무 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="ddaf9-275">측정값 개수를 사용 하 여 toosearch</span><span class="sxs-lookup"><span data-stu-id="ddaf9-275">toosearch using measure count</span></span>
* <span data-ttu-id="ddaf9-276">Hello 검색 쿼리 필드에 입력`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="ddaf9-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="ddaf9-277">추가 `| Select EventID` hello 쿼리의 toohello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="ddaf9-278">마지막으로 추가 `| Sort EventID asc` hello 쿼리의 toohello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="ddaf9-279">몇 가지 중요 한 사항 toonotice 및 강조를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="ddaf9-280">첫째, hello 결과가 표시 되지 않습니다 hello 원래 원시 결과가 더 이상.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="ddaf9-281">대신 집계된 결과이며 기본적으로 그룹의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="ddaf9-282">이 문제가 아니지 하지만 hello 원래 원시 모양과 hello 집계/통계 함수의 결과로 서 hello 즉석에서 생성 되는 매우 다른 모양의 데이터를 상호 작용 하는 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="ddaf9-283">두 번째, **개수 측정** 만 hello 상위 100 고유한 결과 현재 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="ddaf9-284">이 제한은 toohello 다른 통계 함수 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="ddaf9-285">따라서 일반적으로 해야 toouse 보다 정확 하 게 필터 첫 번째 toosearch 특정 항목에 대 한 측정값 개수 ()를 적용 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="ddaf9-286">Hello 측정값 명령으로 hello 최대 및 최소 함수 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="ddaf9-287">**Measure Max()** 및 **Measure Min()**이 유용한 다양한 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="ddaf9-288">그러나 각 함수는 서로 반대이므로 최대()를 설명하고 최소()를 직접 시험해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="ddaf9-289">보안 이벤트를 쿼리할 경우 **레벨** 속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="ddaf9-290">예:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-290">For example:</span></span>

```
Type=SecurityEvent
```

![측정값 개수 시작 검색](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="ddaf9-292">모든 hello 보안에 대해 tooview hello 가장 높은 값을 원하는 경우 사용할 수 이벤트 필드에 따라 hello 그룹, 공용 컴퓨터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![측정값 최대 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="ddaf9-294">Hello 컴퓨터에 대 한 있음을 표시 합니다 **수준** 레코드, 그 중 대부분에는 적어도 수준 8, 수준 16의 많은 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![최대 시간이 생성된 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="ddaf9-296">이 함수는 숫자와 잘 작동하지만 DateTime 필드와도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="ddaf9-297">Hello에 대 한 유용한 toocheck를 마지막 또는 각 컴퓨터에 인덱싱된 데이터의 모든 부분에 대 한 가장 최근 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="ddaf9-298">예를 들어: hello 최신 보안 이벤트를 보고 한 때는 각 컴퓨터에 대 한?</span><span class="sxs-lookup"><span data-stu-id="ddaf9-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="ddaf9-299">Hello 측정값 명령으로 hello avg 함수 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="ddaf9-300">그룹을 기준으로 결과 hello 동일 또는 다른 필드 및 측정값을 사용한 평균 () 통계 함수 hello 있습니다 toocalculate hello 일부 필드에 대 한 평균 값.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="ddaf9-301">다양한 성능 데이터와 같은 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="ddaf9-302">성능 데이터를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-302">We'll start with performance data.</span></span> <span data-ttu-id="ddaf9-303">OMS는 현재 Windows 및 Linux 컴퓨터 양쪽 모두에 대한 성능 카운터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="ddaf9-304">에 대 한 toosearch *모든* 성능 데이터를 hello 가장 기본적인 쿼리는:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="ddaf9-306">hello 먼저 보면 점은 로그 분석에서는 설명 세 가지 관점: hello 차트; 뒤에 실제 레코드가 hello를 보여 주는 보여 주는 목록 성능 카운터 데이터;의 테이블 형식 뷰를 보여 주는 표 및 메트릭을 보여 주는 차트 hello에 대 한 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="ddaf9-307">위 hello 이미지에서 hello 다음 나타내는 표시 된 필드의 두 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="ddaf9-308">첫 번째 집합 hello hello 쿼리 필터에서 Windows 성능 카운터 이름, 개체 이름 및 인스턴스 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="ddaf9-309">Hello 필드로 있습니다 것은 가장 일반적으로 사용할 패싯/필터</span><span class="sxs-lookup"><span data-stu-id="ddaf9-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="ddaf9-310">**CounterValue** hello hello 카운터의 실제 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="ddaf9-311">이 예제에서는 hello 값은 *75*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="ddaf9-312">**TimeGenerated**는 24시간 형식으로 12:51입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="ddaf9-313">다음은 그래프에서 hello 메트릭 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-313">Here's a view of hello metrics in a graph.</span></span>

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="ddaf9-315">Hello Perf 레코드 도형에 대 한 읽기 및 다른 검색 방법에 대 한 읽은 후 측정값 평균 () tooaggregate이이 종류의 숫자 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="ddaf9-316">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue 검색](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="ddaf9-318">이 예제에서는 hello CPU 총 시간 성능 카운터 및 컴퓨터별 평균을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="ddaf9-319">Toonarrow 결과 tooonly hello 지난 6 시간 동안 다운 하려는 경우 hello 시간 필터 컨트롤을 사용 하거나 다음과 같이 쿼리에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="ddaf9-320">toosearch hello avg 함수를 사용 하 여 hello 측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="ddaf9-321">Hello 검색 쿼리 상자에 입력 `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="ddaf9-322">컴퓨터 *간에* 데이터를 집계하고 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="ddaf9-323">예를 들어, 다른 하나 종류의 일부는 같은 tooany 팜에서 호스트 집합이 있는지와 동일한 유형의 작업 및 부하를 대략적으로 분산 해야 하는 모든 hello를 방금 않으므로 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="ddaf9-324">다음 쿼리 평균을 hello 전체 팜에 대 한 hello로 이동 하는 하나에 모든 카운터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="ddaf9-325">다음 예제는 hello로 hello 컴퓨터를 선택 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="ddaf9-326">Tooselect 2 개의 핵심 성과 지표 (Kpi)만 원하는 hello 컴퓨터를가지고: CPU 사용량 % 및 % 사용 가능한 디스크 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="ddaf9-327">따라서 hello 쿼리 부분의 됩니다.:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="ddaf9-328">이제 다음 예제는 hello로 컴퓨터 및 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="ddaf9-329">매우 구체적으로 선택 해야 하므로 hello **avg () 측정** 명령을 반환할 수 있습니다 hello 평균 컴퓨터가 아니라 hello 팜 전체에서 단순히 CounterName로 그룹화 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="ddaf9-330">예:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="ddaf9-331">사용자 환경 KPI의 간단한 보기를 제공하므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![avg 그룹화 검색](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="ddaf9-333">대시보드에서 hello 검색 쿼리를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="ddaf9-334">Hello 검색 쿼리를 저장 하 고 라는 여기에서 대시보드를 만들 수 예를 들어 *웹 팜 Kpi*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="ddaf9-335">대시보드를 사용 하 여에 대 한 더 toolearn 참조 [로그 분석에 사용자 지정 대시보드를 만들](log-analytics-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![avg 대시보드 검색](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="ddaf9-337">Hello sum 함수를 사용 하 여 hello 측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="ddaf9-338">hello sum 함수는 hello 측정값 명령의 유사한 tooother 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="ddaf9-339">Toouse에서 sum 함수 hello 하는 방법에 대 한 예제를 볼 수 [Microsoft Azure Operational Insights의 W3C IIS 로그 검색](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="ddaf9-340">숫자, 날짜 시간 및 텍스트 문자열이 포함된  Max() 및 Min()을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="ddaf9-341">텍스트 문자열을 이용하여 사전순으로 정렬하고 처음 및 마지막을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="ddaf9-342">그러나 숫자 필드가 아닌 어느 것도 합계()를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="ddaf9-343">도 tooAvg() 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="ddaf9-344">Hello 백분위 수 함수 hello 측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="ddaf9-345">숫자 필드에만 사용할 수 있다는 점에서 hello 백분위 수 함수는 유사한 tooAvg() 및 sum ()입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="ddaf9-346">숫자 필드에 1 too99 사이의 모든 백분위 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="ddaf9-347">**percentile** 및 **pct** 명령을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="ddaf9-348">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="ddaf9-349">명령을 경우 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-349">Use hello where command</span></span>
<span data-ttu-id="ddaf9-350">측정값 명령이 – hello 쿼리의 시작 부분에서 필터링 하는 것과 반대로 tooraw 결과로 생성 된 결과 집계 하는 hello 여기서 명령이 필터와 같이 작동 하지만 hello 파이프라인 toofurther 필터에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="ddaf9-351">예:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="ddaf9-352">다른 파이프를 추가할 수 있습니다 "|" 문자 및 hello 명령 tooonly 구할 컴퓨터와 이상 80% 평균 CPU가 다음 예제에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="ddaf9-353">Microsoft System Center-Operations Manager에 잘 알고 있는 관리 팩 측면에서 명령을의 hello 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="ddaf9-354">Hello 예제가 규칙 인 경우 hello 첫번째 hello 쿼리의 부분이 hello 데이터 원본과 hello 명령 hello conditiondetection 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="ddaf9-355">타일로 hello 쿼리를 사용 하 여 **내 대시보드**, 일종의 모니터로 toosee 때 컴퓨터 Cpu 초과 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="ddaf9-356">대시보드에 대 한 자세한 정보는 toolearn 참조 [로그 분석에 사용자 지정 대시보드를 만들](log-analytics-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="ddaf9-357">만들고 및 hello 모바일 앱을 사용 하 여 대시보드를 사용 하 여 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="ddaf9-358">자세한 내용은 [OMS Mobile App](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)(OMS 모바일 앱)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="ddaf9-359">다음 이미지는 hello의 hello 아래쪽 두 타일을 볼 수 있습니다 목록을 표시 한 hello 모니터를 숫자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="ddaf9-360">기본적으로, 항상 hello 숫자 toobe 0을 빈 목록 toobe hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="ddaf9-361">그렇지 않은 경우 경고 조건을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="ddaf9-362">필요한 경우 컴퓨터를 살펴보면 압력을 받고 있기 tootake를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![모바일 대시보드](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="ddaf9-364">Hello를 사용 하 여 in 연산자</span><span class="sxs-lookup"><span data-stu-id="ddaf9-364">Use hello in operator</span></span>
<span data-ttu-id="ddaf9-365">hello *IN* 연산자와 함께 *NOT IN* 는 다른 검색을 인수로 포함 하는 검색 toouse 하위 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="ddaf9-366">이러한 연산자는 다른 *기본* 또는 *외부* 검색 내 중괄호 {} 안에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="ddaf9-367">hello 결과 대체로, 고유한 결과 목록이 며 기본 검색에서 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="ddaf9-368">검색에서 생성할 수 있는 하지만 검색 식에서 직접 설명할 수 없는 데이터의 하위 toomatch 하위 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="ddaf9-369">예를 들어 하나의 검색 toofind 모든 이벤트를 사용 하 여 관심이 있는 경우 *보안 업데이트가 누락 된 컴퓨터*, toodesign를 먼저 식별 하는 대체로 며 필요 *보안 업데이트가 누락 된 컴퓨터*  속하는 toothose 호스트 이벤트를 찾기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="ddaf9-370">따라서 표현할 수 있습니다 *필수 보안 업데이트가 누락 된 현재 컴퓨터* 다음 쿼리에서 hello로:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="ddaf9-372">Hello 목록을 만든 후에 한 해당 컴퓨터에 대 한 이벤트를 찾는 외부 (기본) 검색을 내부 검색 toofeed hello 컴퓨터의 목록으로 hello 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="ddaf9-373">Hello 내부 검색을 중괄호로 묶고 IN 연산자 hello를 사용 하 여 hello 외부 검색에서 필터/필드에 대 한 가능한 값으로 해당 결과 제공 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="ddaf9-374">hello 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="ddaf9-376">또한 공지 hello 시간 때문에 hello 내부 검색에 사용 된 필터 hello 시스템 업데이트 평가 24 시간 마다 모든 컴퓨터의 스냅숏을 만들기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="ddaf9-377">하루에만 검색 하 여 더 간단 하 고 정확한 hello 내부 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="ddaf9-378">hello 외부 검색 대신 사용 하 여 hello 시간 선택을 hello 사용자 인터페이스에서 지난 7 일 동안 hello에서 이벤트를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="ddaf9-379">time 연산자에 대한 자세한 내용은 [부울 연산자](#boolean-operators) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="ddaf9-380">때문에 사용자에 대 한 필터 값으로 hello 내부 검색만 실제로 사용 하 여 hello 결과 hello 외부, hello 외부 검색에 명령을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="ddaf9-381">예를 들어 계속 수 이벤트를 다른 measure 명령으로 위에 그룹 hello:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="ddaf9-383">일반적으로 원하는 내부 쿼리 tooexecute 신속 하 게 및 또한 tooreturn 적은 양의 결과 대 한 로그 분석에는 서비스 쪽 시간 제한이 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="ddaf9-384">Hello 내부 쿼리가 더 많은 결과 반환 하는 경우 hello 결과 목록이 잘리기 있는 발생 시키는 외부 검색 tooreturn hello 잘못 된 결과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="ddaf9-385">다른 규칙은 해당 hello 내부 검색에는 현재 tooprovide 필요한 *집계* 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="ddaf9-386">즉, *measure* 명령을 포함해야 합니다. 현재는 외부 검색에 원시 결과를 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="ddaf9-387">또한 IN 연산자를 하나만 있을 수 있으며 hello hello 쿼리의 마지막 필터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="ddaf9-388">또는 여러 명의 IN 연산자 수 없습니다.-이 기본적으로 실행할 수 없으며 여러 하위 검색: 각 외부 검색에 대 한 중요 한 점은 하나의 하위/내부 검색만 hello 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="ddaf9-389">이러한 제한은 IN 통해 많은 종류의 상관 관계 검색이 가능 및 toodefine 사용 하면 다음과 유사한 toogroups 컴퓨터, 사용자 또는 파일 – 등 어떤 hello 필드 데이터에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="ddaf9-390">다음은 추가적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-390">Here are more examples:</span></span>

<span data-ttu-id="ddaf9-391">**자동 업데이트 설정이 비활성화된 컴퓨터에 누락된 모든 업데이트**</span><span class="sxs-lookup"><span data-stu-id="ddaf9-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="ddaf9-392">**SQL Server(=SQL 평가가 실행된)를 실행하는 컴퓨터의 모든 오류 이벤트**</span><span class="sxs-lookup"><span data-stu-id="ddaf9-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="ddaf9-393">**도메인 컨트롤러(=AD 평가가 실행된)인 컴퓨터의 모든 보안 이벤트**</span><span class="sxs-lookup"><span data-stu-id="ddaf9-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="ddaf9-394">**다른 계정 toohello 로그온 되어 있는 동일한 컴퓨터 BACONLAND\jochan 계정이 로그온가?**</span><span class="sxs-lookup"><span data-stu-id="ddaf9-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="ddaf9-395">Hello distinct 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-395">Use hello distinct command</span></span>
<span data-ttu-id="ddaf9-396">Hello 이름에서 알 수 있듯이이 명령은 필드의 고유 값 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="ddaf9-397">매우 간단하지만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="ddaf9-398">동일한 결과 얻을 수도 measure count () 명령을 사용도 아래와 같이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="ddaf9-400">그러나에 관심이 모든 고유 값 및 해당 값이 있는 문서 hello 수가 아니라 목록만 이면 다음 DISTINCT 및 제공할 수를 출력 하는 쉽고 명확한 tooread 간단한 구문을 아래와 같이.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="ddaf9-402">Hello countdistinct 함수 hello 측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="ddaf9-403">countdistinct 함수 hello hello 각 그룹 내에서 고유 값 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="ddaf9-404">예를 들어, 될 수 toocount hello 수가 고유 컴퓨터 각 형식에 대 한 보고를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="ddaf9-406">Hello 측정 간격 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ddaf9-406">Use hello measure interval command</span></span>
<span data-ttu-id="ddaf9-407">실시간에 가까운 성능 데이터 수집을 통해, Log Analytics의 모든 성능 카운터를 수집하고 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="ddaf9-408">단순히 입력 hello 쿼리 **유형: 성능** 메트릭 그래프 카운터 및 로그 분석 환경에서 서버 hello 수에 따라 수천을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="ddaf9-409">Hello를 살펴볼 수 주문형 메트릭 집계로 높은 수준과 심층 탐구는 데 필요한 만큼 더 세분화 된 데이터에서 사용자 환경에서 전반적인 메트릭.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="ddaf9-410">원하는 tooknow hello 평균 CPU 모든 컴퓨터에서 이란 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="ddaf9-411">모든 컴퓨터에 대 한 평균 CPU hello 살펴보면 아닐 수 있습니다 유용 하므로 결과 매끄럽게 얻을 수 있습니다. 더 세부적으로 toolook를 집계할 수 있습니다 결과 창이 청크를 더 작은 시간과 모양에 시계열에 다른 차원에서.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="ddaf9-412">예를 들어 다음과 같은 모든 컴퓨터에서 CPU 사용량의 hello 시간별 평균을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![평균 간격 측정](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="ddaf9-414">기본적으로, 이러한 결과는 다중 계열 대화형 꺾은선형 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="ddaf9-415">이 차트는 계열 전환(y 축 재조정 포함), 확대/축소 및 가리킴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="ddaf9-416">hello 테이블 표시 옵션은 필요한 경우 hello 원시 데이터를 보기 위해 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="ddaf9-417">다른 필드를 기준으로 그룹화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-417">You can also group by other fields.</span></span> <span data-ttu-id="ddaf9-418">이 예제에서는 하나의 특정 컴퓨터에 대 한 모든 hello % 카운터 보고 하 고 모든 카운터의 시간별 70 백분위 수 hello 란 tooknow 원하는:</span><span class="sxs-lookup"><span data-stu-id="ddaf9-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="ddaf9-419">한 가지 toonote은 이러한 쿼리 제한 tooperformance 카운터 되지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="ddaf9-420">tooany 메트릭을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-420">You can apply them tooany metric.</span></span> <span data-ttu-id="ddaf9-421">이 예제에서, W3C IIS 로그를 보고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="ddaf9-422">각 요청을 처리 하기 위해 5 분 간격에 대해 걸리는 hello 최대 시간 이란 tooknow 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="ddaf9-423">한 쿼리에 여러 집계 사용</span><span class="sxs-lookup"><span data-stu-id="ddaf9-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="ddaf9-424">measure 명령에 집계 절을 여러 개 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="ddaf9-425">각 절에는 개별적으로 별칭을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="ddaf9-426">필드 이름이 사용 된 집계 함수를 hello 됩니다 별칭 hello 결과 부여 되지 않은 경우 (즉, "avg(CounterValue)" avg(CounterValue))에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="ddaf9-428">다른 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="ddaf9-429">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddaf9-429">Next steps</span></span>
<span data-ttu-id="ddaf9-430">로그 검색에 대한 자세한 내용은 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="ddaf9-431">사용 하 여 [로그 분석의 사용자 지정 필드](log-analytics-custom-fields.md) tooextend 로그 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="ddaf9-432">검토 hello [로그 분석 로그 검색 참조](log-analytics-search-reference.md) tooview hello의 모든 필드 및 패싯 로그 분석에서 사용할 수를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaf9-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
