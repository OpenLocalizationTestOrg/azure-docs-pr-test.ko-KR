---
title: "Azure Log Analytics에서 로그 검색을 사용하여 데이터 찾기 | Microsoft Docs"
description: "로그 검색을 사용하면 사용자 환경 내에서 여러 소스의 컴퓨터 데이터를 서로 연결하고 결합할 수 있습니다."
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
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="cd471-103">Log Analytics에서 로그 검색을 사용하여 데이터 찾기</span><span class="sxs-lookup"><span data-stu-id="cd471-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="cd471-104">이 문서에서는 Log Analytics에서 최신 쿼리 언어를 사용하는 로그 검색에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="cd471-105">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 [Log Analytics의 로그 검색 이해(신규)](log-analytics-log-search-new.md)를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="cd471-106">Log Analytics의 핵심은 사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결하고 결합할 수 있게 하는 로그 검색 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="cd471-107">솔루션도 로그 검색에서 제공되어 특정 문제 영역 주위에 피벗된 메트릭을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="cd471-108">검색 페이지에서, 쿼리를 만든 다음 검색 시 패싯 컨트롤을 사용하여 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="cd471-109">변환, 필터링 및 결과를 보고하는 고급 쿼리를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="cd471-110">일반적인 로그 검색 쿼리는 대부분의 솔루션 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="cd471-111">OMS 콘솔에서는 로그 검색을 사용하여 타일을 클릭하거나 다른 항목을 확인하여 항목에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="cd471-112">이 자습서에서는 로그 검색을 사용하는 경우 모든 기본 사항을 설명하는 예제를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="cd471-113">간단하고 실용적인 예제부터 시작하고 이를 확장하므로 구문을 사용하여 데이터에서 원하는 통찰력을 추출하는 방법에 대한 실용적인 사용 사례를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="cd471-114">검색 기술을 숙지한 후에 [Log Analytics log search reference](log-analytics-search-reference.md)(Log Analytics 로그 검색 참조)를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="cd471-115">기본 필터 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-115">Use basic filters</span></span>
<span data-ttu-id="cd471-116">먼저 알아야 할 점은 검색 쿼리의 첫 번째 부분("|" 세로줄 문자 앞에 나오는)은 항상 *필터*라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="cd471-117">TSQL에서 WHERE 절로 생각할 수 있으며 이는 OMS 데이터 저장소에서 *어떤* 데이터의 하위 집합을 가져올지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="cd471-118">데이터 저장소에 대한 검색은 대개 추출하려는 데이터의 특성을 지정하므로 쿼리가 WHERE 절과 함께 시작하는 것이 자연스럽습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="cd471-119">사용할 수 있는 가장 기본적인 필터는 ‘오류’ 또는 ‘시간 제한’ 또는 컴퓨터 이름과 같은 *키워드*입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="cd471-120">이러한 유형의 간단한 쿼리는 일반적으로 동일한 결과 집합 내에서 다양한 모양의 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="cd471-121">Log Analytics는 시스템에 다양한 데이터 *유형* 이 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="cd471-122">단순 검색을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-122">To conduct a simple search</span></span>
1. <span data-ttu-id="cd471-123">OMS 포털에서 **로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="cd471-124">![검색 타일](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="cd471-125">쿼리 필드에서 `error`를 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="cd471-126">![검색 오류](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="cd471-127">예를 들어, 다음 이미지에서 `error`에 대한 쿼리는 100,000건의 **이벤트** 레코드(로그 관리에서 수집), 18건의 **ConfigurationAlert** 레코드(구성 평가에서 생성) 및 12건의 **ConfigurationChange** 레코드(변경 내용 추적에서 캡처)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="cd471-128">![검색 결과](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="cd471-129">이러한 필터는 실제로 개체 유형/클래스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="cd471-130">*유형* 은 한 개의 태그, 속성 또는 문자열/이름/범주이며 하나의 데이터에 첨부됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="cd471-131">시스템의 일부 문서는 **Type:ConfigurationAlert**로 태그가 지정되고 일부는 **Type:Perf** 또는 **Type:Event** 등으로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="cd471-132">각 검색 결과, 문서, 레코드 또는 항목은 각 데이터에 대한 원시 속성 및 값을 표시하고 필드에 지정된 값이 있는 레코드만 검색하려는 경우 필드 이름을 사용하여 필터에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="cd471-133">*유형*은 실제로 모든 레코드가 있는 필드이며 다른 필드와 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="cd471-134">형식 필드의 값을 기반으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="cd471-135">해당 레코드를 다른 형태 또는 모습을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-135">That record will have a different shape or form.</span></span> <span data-ttu-id="cd471-136">부수적으로, **Type=Perf** 또는 **Type=Event**는 성능 데이터 또는 이벤트를 쿼리하는 방법을 알아보아야 하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="cd471-137">필드 이름 뒤 또는 값 앞에 콜론 (:) 또는 등호 (=) 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="cd471-138">**Type:Event** and **Type=Event** 는 의미가 동일하며 선호하는 스타일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="cd471-139">따라서 Type=Perf 레코드에 'CounterName'이라는 필드가 있는 경우 `Type=Perf CounterName="% Processor Time"`와 비슷한 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="cd471-140">이렇게 하면 성능 카운터 이름이 "% 프로세서 시간"인 성능 데이터만 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="cd471-141">프로세서 시간 성능 데이터를 검색 하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-141">To search for processor time performance data</span></span>
* <span data-ttu-id="cd471-142">검색 쿼리 필드에 `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="cd471-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="cd471-143">또한 더욱 구체적 지정이 가능하여 쿼리에서 Windows 성능 카운터인 **InstanceName=_'Total'**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="cd471-144">또한 패싯 및 다른 **field:value**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="cd471-145">필터는 쿼리 표시줄의 필터에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="cd471-146">다음 그림에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-146">You can see this in the following image.</span></span> <span data-ttu-id="cd471-147">아무것도 입력하지 않고 쿼리에 **InstanceName:’_Total’**을 추가하려는 경우 클릭할 위치를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![검색 패싯](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="cd471-149">쿼리는 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="cd471-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="cd471-150">이 예제에서 이 결과를 얻으려면 **Type=Perf** 를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="cd471-151">필드 CounterName 및 InstanceName는 Type=Perf의 레코드에만 존재하므로 쿼리는 더 긴 이전과 같은 결과를 반환할 만큼 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="cd471-152">쿼리에서 모든 필터가 서로 *AND* 에 있는 것으로 평가되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="cd471-153">효과적으로 기준에 더 많은 필드를 더할수록 더 구체적이고 구체화된 결과는 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="cd471-154">예를 들어 쿼리 `Type=Event EventLog="Windows PowerShell"`는 `Type=Event AND EventLog="Windows PowerShell"`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="cd471-155">Windows PowerShell 이벤트 로그에서 로그인되고 수집된 모든 이벤트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="cd471-156">동일한 패싯을 반복해서 선택하여 필터를 여러 번 추가하는 경우 이는 순수하게 외관상의 문제입니다. 검색 표시줄을 채울 수 있지만 암시적 AND 연산자가 항상 있기 때문에 여전히 동일한 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="cd471-157">NOT 연산자를 명시적으로 사용하여 쉽게 암시적 AND 연산자를 역방향으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="cd471-158">예:</span><span class="sxs-lookup"><span data-stu-id="cd471-158">For example:</span></span>

<span data-ttu-id="cd471-159">`Type:Event NOT(EventLog:"Windows PowerShell")` 또는 이와 동일한 `Type=Event EventLog!="Windows PowerShell"`은 Windows PowerShell 로그가 아닌 다른 모든 로그의 모든 이벤트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="cd471-160">또는 'OR'같은 다른 부울 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="cd471-161">다음 쿼리는 어떤 EventLog가 응용 프로그램 OR 시스템인지에 대한 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="cd471-162">위의 쿼리를 사용하여 동일한 결과 집합에서 두 로그 항목을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="cd471-163">그러나 암시적 AND 상태로 두어 OR을 제거하면 BOTH 로그에 속하는 이벤트 로그 항목이 없기 때문에 다음의 쿼리는 결과를 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="cd471-164">각 이벤트 로그 항목은 두 로그 중 하나에 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="cd471-165">추가 필터 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-165">Use additional filters</span></span>
<span data-ttu-id="cd471-166">다음 쿼리는 데이터를 전송하는 모든 컴퓨터에 대한 2개의 이벤트 로그에 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![검색 결과](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="cd471-168">필드 또는 필터 중 하나를 선택하면 다른 모두를 제외하고 특정 컴퓨터에 대한 쿼리 범위가 좁혀집니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="cd471-169">결과 쿼리는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="cd471-170">암시적 AND 때문에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="cd471-171">각 쿼리는 다음과 같은 명시적 순서로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="cd471-172">괄호에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="cd471-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="cd471-173">이벤트 로그 필드와 마찬가지로 OR을 추가하여 특정 컴퓨터 집합에 대한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="cd471-174">예:</span><span class="sxs-lookup"><span data-stu-id="cd471-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="cd471-175">마찬가지로 다음 쿼리는 선택한 두 컴퓨터에 **CPU 시간 (%)** 을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="cd471-176">필드 형식</span><span class="sxs-lookup"><span data-stu-id="cd471-176">Field types</span></span>
<span data-ttu-id="cd471-177">필터를 만들 때 로그 검색에서 반환된 다양한 유형의 필드로 작업할 때의 차이점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="cd471-178">**검색 가능한 필드**는 검색 결과에 파란색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="cd471-179">검색 조건에서 다음과 같은 필드에 국한되는 검색 가능한 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="cd471-180">**자유 텍스트 검색 가능 필드**는 검색 결과에서 회색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="cd471-181">검색 가능한 필드와 같은 필드에만 해당되는 검색 조건은 이러한 필드에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="cd471-182">이러한 필드는 다음과 같은 모든 필드에서 쿼리를 수행할 때만 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="cd471-183">부울 연산자</span><span class="sxs-lookup"><span data-stu-id="cd471-183">Boolean operators</span></span>
<span data-ttu-id="cd471-184">날짜/시간 및 숫자 필드를 사용하여 *보다 큼*, *보다 작음*, *보다 작거나 같음*을 사용하는 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="cd471-185">쿼리 검색 표시줄에서 >, < , >=, <= , != 와 같은 간단한 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="cd471-186">특정 기간에 특정 이벤트 로그를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="cd471-187">예를 들어 지난 24시간을 다음 mnemonic 식으로 표현합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="cd471-188">부울 연산자를 사용하여 검색하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-188">To search using a boolean operator</span></span>
* <span data-ttu-id="cd471-189">검색 쿼리 필드에 `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="cd471-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="cd471-190">![부울 값을 사용하여 검색](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="cd471-191">시간 간격을 그래픽으로 제어할 수 있지만, 그렇게 하려는 대부분의 시간에 쿼리에 직접 하는 시간 필터를 포함하여 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="cd471-192">예를 들어 이 방식은 대시보드 페이지에서 *전역* 시간 선택기와 무관하게 각 타일에 대한 시간을 재정의할 수 있는 경우 대시보드와 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="cd471-193">자세한 내용은 [대시보드에서 시간 문제](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cd471-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="cd471-194">시간별로 필터링하는 경우 두 기간(OMS 포털(S1)에서 지정한 기간, 쿼리(S2)에 지정한 기간)의 *교집합*에 대한 결과를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![교집합](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="cd471-196">즉, 기간이 교차하지 않을 경우, 예를 들어 OMS 포털에서 **이번 주**를 선택하고 쿼리에서는 **지난 주**를 정의하는 경우 교집합이 없으므로 결과가 수신되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="cd471-197">TimeGenerated 필드에 사용되는 비교 연산자가 다른 경우에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="cd471-198">예를 들어 숫자 필드를 사용하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-198">For example, with numeric fields.</span></span>

<span data-ttu-id="cd471-199">예를 들어 구성 평가 경고는 다음의 심각도 값을 가진다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="cd471-200">0 = 정보</span><span class="sxs-lookup"><span data-stu-id="cd471-200">0 = Information</span></span>
* <span data-ttu-id="cd471-201">1 = 경고</span><span class="sxs-lookup"><span data-stu-id="cd471-201">1 = Warning</span></span>
* <span data-ttu-id="cd471-202">2 = 중요</span><span class="sxs-lookup"><span data-stu-id="cd471-202">2 = Critical</span></span>

<span data-ttu-id="cd471-203">경고 및 중요한 알림을 쿼리하고 다음 쿼리로 정보를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="cd471-204">범위 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-204">You can also use range queries.</span></span> <span data-ttu-id="cd471-205">즉, 시퀀스에서 값의 시작 및 끝 범위를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="cd471-206">예를 들어 EventID가 보다 2100 이상이지만 2199 미만일 때 Operations Manager 이벤트 로그에서 이벤트를 하려는 경우 다음의 쿼리는 이벤트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="cd471-207">사용해야 하는 범위 구문은 콜론(:) field:value 구분이고 등호(=)는 *아닙니다* .</span><span class="sxs-lookup"><span data-stu-id="cd471-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="cd471-208">아래쪽과 위쪽의 범위 끝을 대괄호로 묶고 두 마침표(..)로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="cd471-209">검색 결과 조작</span><span class="sxs-lookup"><span data-stu-id="cd471-209">Manipulate search results</span></span>
<span data-ttu-id="cd471-210">데이터를 검색할 때 검색 쿼리를 구체화하고 결과를 어느 정도 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="cd471-211">결과를 검색할 때 이를 변환하는 명령을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="cd471-212">Log Analytics 검색에서 명령은 세로줄 문자(|) 뒤에 *와야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="cd471-213">필터는 쿼리 문자열의 첫번째 부분에 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="cd471-214">작업하는 데이터 집합을 정의하고 이러한 결과를 명령으로 "파이프"합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="cd471-215">다음 명령을 추가하려면 파이프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="cd471-216">이것은 Windows PowerShell 파이프라인과 대강 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="cd471-217">일반적으로 Log Analytics 검색 언어는 PowerShell 스타일을 따르고 지침도 IT 전문가와 비슷하게 하며 학습 곡선을 보다 쉽게 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="cd471-218">명령은 동사의 이름이 있으므로 수행할 작업을 쉽게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="cd471-219">정렬</span><span class="sxs-lookup"><span data-stu-id="cd471-219">Sort</span></span>
<span data-ttu-id="cd471-220">정렬 명령을 사용하면 하나 또는 여러 필드에서 정렬 순서를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="cd471-221">기본적으로 사용하지 않아도 시간 내림차순으로 정렬되도록 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="cd471-222">가장 최근의 결과가 검색 결과 위쪽에 항상 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="cd471-223">즉, `Type=Event EventID=1234` 로 검색을 실행하면 실제로 실행되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="cd471-224">로그를 잘 알고 있다면 경험 형식 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="cd471-225">예를 들어 Windows 이벤트 뷰어에서 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="cd471-226">정렬을 사용하여 결과를 반환하는 방식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="cd471-227">다음 예제는 이 작동 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="cd471-228">위의 간단한 예제는 명령이 작동하는 방법을 보여줍니다. 필터가 반환하는 결과의 형태를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="cd471-229">제한 및 위쪽</span><span class="sxs-lookup"><span data-stu-id="cd471-229">Limit and top</span></span>
<span data-ttu-id="cd471-230">덜 알려진 다른 명령에는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="cd471-231">제한은 PowerShell같은 동사입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="cd471-232">제한은 TOP 명령과 기능적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="cd471-233">다음 쿼리는 동일한 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="cd471-234">Top을 사용하여 검색하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-234">To search using top</span></span>
* <span data-ttu-id="cd471-235">검색 쿼리 필드에 `Type=Event EventID=600 | Top 1` 을 입력합니다</span><span class="sxs-lookup"><span data-stu-id="cd471-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="cd471-236">![상위 검색](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="cd471-237">위의 이미지에서 EventID=600인 레코드는 358개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="cd471-238">왼쪽에서 필드, 패싯 및 필터는 항상 쿼리의 *필터 부분으로* 반환된 결과에 대한 정보를 표시하며 이는 모든 파이프 문자 앞에 오는 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="cd471-239">**결과** 창은 예제 명령이 결과를 모양을 만들고 변환하기 때문에 가장 최근 1개의 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="cd471-240">여기서</span><span class="sxs-lookup"><span data-stu-id="cd471-240">Select</span></span>
<span data-ttu-id="cd471-241">SELECT 명령은 PowerShell에서 Select-Object 처럼 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="cd471-242">자신의 원래 속성을 모두 갖지 않는 필터된 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="cd471-243">대신 지정한 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="cd471-244">선택 명령을 사용하는 검색을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-244">To run a search using the select command</span></span>
1. <span data-ttu-id="cd471-245">검색에서 `Type=Event` 을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="cd471-246">있는 모든 속성을 보려면 결과 중 하나에서 **+자세히 표시** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="cd471-247">그 중 일부를 명시적으로 선택하고 쿼리가 `Type=Event | Select Computer,EventID,RenderedDescription`로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="cd471-248">![선택 검색](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="cd471-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="cd471-249">검색 출력을 제어하고 탐색을 위한 중요 데이터의 일부만 선택하려는 경우 특히 유용한 명령으로 종종 전체 레코드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="cd471-250">이 기능은 다른 유형의 레코드들이 *일부* 공통 속성이 있지만 *일부* 속성은 공통이 아닌 경우에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="cd471-251">CSV 파일로 내보낸 다음 Excel에서 massaged되는 경우 테이블처럼 더 자연스럽게 보이거나 잘 작동하는 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="cd471-252">측정값 명령 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-252">Use the measure command</span></span>
<span data-ttu-id="cd471-253">MEASURE는 Log Analytics 검색에서 가장 용도가 많은 명령 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="cd471-254">데이터에 통계 *함수* 를 적용하고 지정된 필드가 그룹화된 결과를 집계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="cd471-255">측정값이 지원하는 여러 통계 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="cd471-256">개수() 측정</span><span class="sxs-lookup"><span data-stu-id="cd471-256">Measure count()</span></span>
<span data-ttu-id="cd471-257">작업할 첫번째 통계 함수에서 이해하기 가장 간단한 것은 *count()* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="cd471-258">`Type=Event`과 같은 모든 검색 쿼리에서 나온 결과는 검색 결과의 왼쪽에 패싯이라고 하는 필터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="cd471-259">필터는 실행된 검색에서 결과에 지정된 필드에 의해 값의 분포를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="cd471-261">예를 들어, 위의 이미지에서는 **컴퓨터** 필드가 표시되고 결과에서 거의 73만 9천개까지 이벤트를 보여줍니다. 해당 레코드에는 **컴퓨터** 필드에 대한 68개의 고유한 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="cd471-262">타일은 **컴퓨터** 필드에 기록되는 가장 일반적인 5개의 값인 상위 5개만을 표시하며) 해당 필드에 특정 값을 포함하는 문서 수를 기준으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="cd471-263">이 이미지에 있는 거의 369,000개 이미지 중 90,000개는 OpsInsights04.contoso.com 컴퓨터에서, 83,000개는 DB03.contoso.com 컴퓨터 등에서 생성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="cd471-264">타일이 상위 5개만 표시하므로 모든 값을 보려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="cd471-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="cd471-265">개수() 함수를 사용하여 측정값 명령으로 수행할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="cd471-266">이 함수는 매개 변수를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="cd471-267">방금 이 경우에 **컴퓨터** 필드를 기준으로 그룹화하려는 필드를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="cd471-269">하지만 **컴퓨터**는 각 데이터*에서* 사용되는 필드입니다. 관련된 관계 데이터베이스가 없고 별도의 **컴퓨터** 개체는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="cd471-270">데이터에 *있는* 값은 해당 값이 생성된 엔티티, 데이터의 다양한 특성 및 측면(따라서 *패싯*이라고 함)을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="cd471-271">그러나 다른 필드에 의해 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="cd471-272">또한 measure 명령으로 파이프되는 거의 739,000개 이벤트의 원래 결과에도 **EventID**라는 필드가 있기 때문에 동일한 기법을 적용하여 해당 필드별로 그룹화하고 EventID별로 이벤트의 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="cd471-273">특정 값을 포함하는 실제 레코드 개수에 관심이 없지만 대신 값 자체의 목록을 원하는 경우 끝부분에 *선택* 명령을 추가하고 첫 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="cd471-274">쿼리에서 더 복잡해 지고 미리 결과를 정렬할 수 있습니다. 또는 그리드의 열을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="cd471-275">측정값 개수를 사용하여 검색</span><span class="sxs-lookup"><span data-stu-id="cd471-275">To search using measure count</span></span>
* <span data-ttu-id="cd471-276">검색 쿼리 필드에 `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="cd471-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="cd471-277">쿼리의 끝에 `| Select EventID` 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="cd471-278">마지막으로 쿼리의 끝에 `| Sort EventID asc` 을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="cd471-279">몇가지 중요한 사항 및 강조를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="cd471-280">첫 번째로 표시되는 결과는 원래 원시 결과가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="cd471-281">대신 집계된 결과이며 기본적으로 그룹의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="cd471-282">이는 문제가 아니지만 집계/통계 함수의 결과로서 즉석에서 생성되는 원래 원시 모양과 달라진  매우 다른 모양의 데이터를 조작한다는 점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="cd471-283">두 번째로 **개수 측정** 은 현재 상위 100개의 고유한 결과만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="cd471-284">이 제한은 다른 통계 함수에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="cd471-285">따라서 측정값 개수()를 적용하기 전에 특정 항목을 검색하려면 일반적으로 보다 정밀한 필터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="cd471-286">측정값 명령과 최대 및 최소 함수 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="cd471-287">**Measure Max()** 및 **Measure Min()**이 유용한 다양한 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="cd471-288">그러나 각 함수는 서로 반대이므로 최대()를 설명하고 최소()를 직접 시험해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="cd471-289">보안 이벤트를 쿼리할 경우 **레벨** 속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="cd471-290">예:</span><span class="sxs-lookup"><span data-stu-id="cd471-290">For example:</span></span>

```
Type=SecurityEvent
```

![측정값 개수 시작 검색](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="cd471-292">공통 컴퓨터, 필드별 그룹에서 모든 보안 이벤트에 대해 가장 높은 값을 보려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![측정값 최대 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="cd471-294">**레벨** 레코드가 있는 컴퓨터의 경우 대부분은 레벨 8 이상이며 레벨 16도 많습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![최대 시간이 생성된 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="cd471-296">이 함수는 숫자와 잘 작동하지만 DateTime 필드와도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="cd471-297">각 컴퓨터에 인덱싱된 데이터의 모든 부분에 대한 마지막 또는 가장 최근 타임스탬프를 확인하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="cd471-298">예: 각 컴퓨터에 대해 가장 최근 보고된 보안 이벤트는 무엇이었습니까?</span><span class="sxs-lookup"><span data-stu-id="cd471-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="cd471-299">측정값 명령과 평균 함수 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="cd471-300">측정값을 사용한 평균() 통계 함수를 사용하면 일부 필드에 대한 평균값을 계산하고 동일한 또는 다른 필드 결과를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="cd471-301">다양한 성능 데이터와 같은 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="cd471-302">성능 데이터를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-302">We'll start with performance data.</span></span> <span data-ttu-id="cd471-303">OMS는 현재 Windows 및 Linux 컴퓨터 양쪽 모두에 대한 성능 카운터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="cd471-304">*모든* 성능 데이터를 검색하려면 가장 기본적인 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="cd471-306">가장 먼저 Log Analytics에 세 가지 관점이 표시되는 것을 볼 수 있습니다. 즉, 목록에는 차트에 사용된 실제 레코드가 표시되고 표에는 성능 카운터 데이터가 테이블 형식으로 표시되며 메트릭에는 성능 카운터가 차트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="cd471-307">위 이미지에서 다음과 같은 내용을 나타내는 표시된 필드의 두 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="cd471-308">첫 번째 집합은 쿼리 필터에서 Windows 성능 카운터 이름, 개체 이름 및 인스턴스 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="cd471-309">가장 일반적으로 사용할 패싯/필터 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="cd471-310">**CounterValue**는 카운터의 실제 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="cd471-311">이 예에서 이 값은 *75*입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="cd471-312">**TimeGenerated**는 24시간 형식으로 12:51입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="cd471-313">다음은 메트릭의 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-313">Here's a view of the metrics in a graph.</span></span>

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="cd471-315">Perf 레코드 모양을 읽고 다른 검색 방법에 대해 읽은 후 이러한 종류의 숫자 데이터를 집계하려면 measure Avg()를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="cd471-316">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue 검색](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="cd471-318">이 예제에서 CPU 총 시간 성능 카운터를 선택하고 컴퓨터에 의해 평균을 냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="cd471-319">최근 6시간으로 결과의 범위를 좁히려면, 시간 필터 제어를 사용하거나 쿼리에 다음과 같이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="cd471-320">측정값 명령과 평균 함수 사용를 사용하여 검색하려면</span><span class="sxs-lookup"><span data-stu-id="cd471-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="cd471-321">검색 쿼리 박스에 `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="cd471-322">컴퓨터 *간에* 데이터를 집계하고 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="cd471-323">예를 들어 각 노드가 서로 동일한 종류의 일부 팜에서 호스트 집합이 있고 이들이 모두 같은 유형의 작업을 한다고 가정하면 부하가 대략적으로 분산되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="cd471-324">다음의 쿼리로 이동하는 하나에 모든 카운터를 가져오고 전체 팜에 대한 평균을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="cd471-325">다음 예제로 컴퓨터를 선택하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="cd471-326">컴퓨터가 있으므로 또한 2개의 핵심 성과 지표 (KPI) 즉, CPU 사용량 % 및 % 사용 가능한 디스크 공간을 선택하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="cd471-327">따라서 쿼리의 부분은 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="cd471-328">이제 다음 예제로 컴퓨터 및 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="cd471-329">매우 구체적인 선택을 하기 때문에 **평균() 측정** 명령이 컴퓨터로 평균이 아닌 팜 전체에서 단순히 CounterName로 그룹화하여 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="cd471-330">예:</span><span class="sxs-lookup"><span data-stu-id="cd471-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="cd471-331">사용자 환경 KPI의 간단한 보기를 제공하므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![avg 그룹화 검색](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="cd471-333">대시보드에서 검색 쿼리를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="cd471-334">예를 들어 검색 쿼리를 저장하고 여기에서 *Web Farm KPIs*라는 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="cd471-335">대시보드 사용에 대해 자세히 알아보려면 [Log Analytics에서 사용자 지정 대시보드 만들기](log-analytics-dashboards.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd471-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![avg 대시보드 검색](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="cd471-337">측정값 명령과 합계 함수 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="cd471-338">합계 함수는 측정값 명령의 다른 함수와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="cd471-339">합계 함수를 사용하는 방법에 대한 예제는 [Microsoft Azure Operational Insights의 W3C IIS 로그 검색](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="cd471-340">숫자, 날짜 시간 및 텍스트 문자열이 포함된  Max() 및 Min()을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="cd471-341">텍스트 문자열을 이용하여 사전순으로 정렬하고 처음 및 마지막을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="cd471-342">그러나 숫자 필드가 아닌 어느 것도 합계()를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="cd471-343">평균()에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="cd471-344">measure 명령과 percentile 함수 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="cd471-345">percentile 함수는 숫자 필드에만 사용할 수 있다는 면에서 Avg() 및 Sum()과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="cd471-346">숫자 필드에 1과 99 사이의 모든 백분위 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="cd471-347">**percentile** 및 **pct** 명령을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="cd471-348">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="cd471-349">Where 명령 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-349">Use the where command</span></span>
<span data-ttu-id="cd471-350">명령이 필터와 같이 작동하지만 쿼리의 시작 부분에서 필터링된 원시 결과와 반대로 파이프라인에 적용하여 측정값 명령이 생성한 집계된 결과를 자세히 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="cd471-351">예:</span><span class="sxs-lookup"><span data-stu-id="cd471-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="cd471-352">다음 예제로 다른 파이프 "|" 문자 및 Where 명령을 추가하여 평균 CPU가 80% 이상인 컴퓨터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="cd471-353">Microsoft System Center Operations Manager에 익숙하다면 where 명령을 관리 팩 측면에서 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="cd471-354">예제가 규칙인 경우 쿼리의 첫번째 부분이 데이터 원본이고 where 명령은 조건 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="cd471-355">**내 대시보드**에서 컴퓨터 CPU가 과도하게 사용되는 경우 참조하는 모니터로서 쿼리를 타일로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="cd471-356">대시보드에 대해 자세히 알아보려면 [Log Analytics에서 사용자 지정 대시보드 만들기](log-analytics-dashboards.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd471-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="cd471-357">또한 모바일 앱을 사용하여 대시보드를 만들고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="cd471-358">자세한 내용은 [OMS Mobile App](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)(OMS 모바일 앱)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd471-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="cd471-359">다음 이미지의 아래쪽 두 타일에서 목록을 표시한 모니터를 숫자로 볼 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="cd471-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="cd471-360">기본적으로 항상 수는 0으로, 목록은 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="cd471-361">그렇지 않은 경우 경고 조건을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="cd471-362">필요한 경우 이것을 사용하여 압력을 받는 컴퓨터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![모바일 대시보드](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="cd471-364">in 연산자 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-364">Use the in operator</span></span>
<span data-ttu-id="cd471-365">*IN* 연산자와 *NOT IN* 연산자를 사용하면 인수로 다른 검색이 포함된 검색인 하위 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="cd471-366">이러한 연산자는 다른 *기본* 또는 *외부* 검색 내 중괄호 {} 안에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="cd471-367">하위 검색의 결과(흔히, 고유한 결과 목록)는 기본 검색의 인수로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="cd471-368">검색 식에 직접적으로 설명할 수 없는, 하지만 검색을 통해 생성될 수 있는 데이터의 하위 집합에 맞추기 위해 하위 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="cd471-369">예를 들어, *보안 업데이트가 없는 컴퓨터*에서 모든 이벤트를 찾는 검색을 사용하려면 해당 호스트에 속하는 이벤트를 찾기 전에 *보안 업데이트가 없는 컴퓨터*를 먼저 식별하는 하위 검색을 디자인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="cd471-370">따라서 다음 쿼리를 통해 *현재 필수 보안 업데이트가 누락된 컴퓨터* 를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="cd471-372">목록이 확보되면, 이 검색을 컴퓨터에 대한 이벤트를 찾는 외부(기본) 검색에 컴퓨터 목록을 제공하는 내부 검색으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="cd471-373">그렇게 하려면 내부 검색을 괄호로 묶고 그 결과를 IN 연산자를 사용하는 외부 검색 필터/필드에 가능한 값으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="cd471-374">쿼리는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="cd471-376">또한, 시스템 업데이트 평가에서 24시간마다 모든 컴퓨터의 스냅숏을 만들기 때문에, 내부 검색에 사용되는 시간 필터에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="cd471-377">하루 동안만 검색하면 내부 쿼리를 보다 가볍고 정확하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="cd471-378">대신, 외부 검색은 마지막 7일간의 이벤트를 검색하는, 사용자 인터페이스의 시간 선택을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="cd471-379">time 연산자에 대한 자세한 내용은 [부울 연산자](#boolean-operators) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd471-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="cd471-380">내부 검색의 결과를 외부 검색에 대한 필터 값으로만 사용하기 때문에, 외부 검색에 명령을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="cd471-381">예를 들어, 위의 이벤트를 다른 measure 명령을 사용하여 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="cd471-383">일반적으로, Log Analytics에 서비스 쪽 제한 시간이 있고 소량의 결과를 반환하기 때문에 내부 쿼리가 신속하게 실행되기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="cd471-384">내부 쿼리가 더 많은 결과를 반환하면, 결과 목록이 잘리고, 이렇게 되면 외부 검색이 잘못된 결과를 반환하도록 유발할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="cd471-385">또 다른 규칙은 내부 검색이 현재 *집계된* 결과를 제공해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="cd471-386">즉, *measure* 명령을 포함해야 합니다. 현재는 외부 검색에 원시 결과를 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="cd471-387">또한, IN 연산자는 하나만 있어야 하고 쿼리의 마지막 필터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="cd471-388">여러 개의 IN 연산자에 OR을 사용할 수 없습니다. 이것은 근본적으로 하위 검색을 여러 개 실행하지 못하도록 합니다. 중요한 점은 각 외부 검색에 대한 하위/내부 검색은 하나만 가능하다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="cd471-389">이러한 제한이 있더라도, IN을 사용하면 다양한 종류의 상호 관련 검색이 가능하며, 컴퓨터, 사용자, 또는 파일(데이터에 포함된 필드면 무엇이든) 같은 그룹과 유사한 것을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="cd471-390">다음은 추가적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-390">Here are more examples:</span></span>

<span data-ttu-id="cd471-391">**자동 업데이트 설정이 비활성화된 컴퓨터에 누락된 모든 업데이트**</span><span class="sxs-lookup"><span data-stu-id="cd471-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="cd471-392">**SQL Server(=SQL 평가가 실행된)를 실행하는 컴퓨터의 모든 오류 이벤트**</span><span class="sxs-lookup"><span data-stu-id="cd471-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="cd471-393">**도메인 컨트롤러(=AD 평가가 실행된)인 컴퓨터의 모든 보안 이벤트**</span><span class="sxs-lookup"><span data-stu-id="cd471-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="cd471-394">**BACONLAND\jochan 계정이 로그인된 컴퓨터에 또 어떤 계정이 로그인되어 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="cd471-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="cd471-395">distinct 명령 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-395">Use the distinct command</span></span>
<span data-ttu-id="cd471-396">이름에서 알 수 있듯이, 이 명령은 필드의 고유 값 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="cd471-397">매우 간단하지만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="cd471-398">아래에서 볼 수 있듯이, measure count() 명령을 사용하면 같은 결과를 낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="cd471-400">고유 값 목록에만 관심이 있고 그 값을 포함하는 문서의 수에는 관심이 없다면, DISTINCT는 보다 읽기 쉽고 깔끔한 결과와 짧은 구문을 제공합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="cd471-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="cd471-402">measure 명령과 함께 countdistinct 함수 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="cd471-403">countdistinct 함수는 각 그룹에 포함된 고유 값의 수를 셉니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="cd471-404">예를 들어, 각 유형에 대해 보고하는 고유한 컴퓨터의 수를 계산하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="cd471-406">measure interval 명령 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-406">Use the measure interval command</span></span>
<span data-ttu-id="cd471-407">실시간에 가까운 성능 데이터 수집을 통해, Log Analytics의 모든 성능 카운터를 수집하고 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="cd471-408">간단하게 **Type:Perf** 쿼리만 입력하면, Log Analytics 환경의 카운터와 서버 수를 기반으로 수천 개의 메트릭 그래프가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="cd471-409">주문형 메트릭 집계를 통해, 대략적인 수준에서 환경의 전반적인 메트릭을 살펴볼 수 있고 필요에 따라 보다 세부적인 데이터를 깊게 파고들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="cd471-410">모든 컴퓨터를 통틀어 평균 CPU가 어떻게 되는지 알아야 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="cd471-411">모든 컴퓨터의 평균 CPU를 살펴보는 것은 결과가 완화될 수 있기 때문에 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="cd471-412">보다 자세히 알아보기 위해서는, 결과를 기간이 더 짧은 청크로 집계하고, 여러 차원에 걸쳐 시계열을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="cd471-413">예를 들어, 모든 컴퓨터에 대한 시간당 평균 CPU 사용률을 다음과 같이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![평균 간격 측정](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="cd471-415">기본적으로, 이러한 결과는 다중 계열 대화형 꺾은선형 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="cd471-416">이 차트는 계열 전환(y 축 재조정 포함), 확대/축소 및 가리킴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="cd471-417">필요한 경우 원시 데이터를 볼 수 있도록, 테이블 표시 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="cd471-418">다른 필드를 기준으로 그룹화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-418">You can also group by other fields.</span></span> <span data-ttu-id="cd471-419">이 예제에서는, 특정 컴퓨터 한 대에 대한 모든 % 카운터를 살펴보고 있으며, 모든 카운터의 시간당 70 백분위 수가 무엇인지 알고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="cd471-420">이 쿼리는 성능 카운터로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="cd471-421">모든 메트릭에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-421">You can apply them to any metric.</span></span> <span data-ttu-id="cd471-422">이 예제에서, W3C IIS 로그를 보고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="cd471-423">5분 간격으로 각 요청을 처리하는데 소요되는 최대 시간이 얼마인지 알아 보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="cd471-424">한 쿼리에 여러 집계 사용</span><span class="sxs-lookup"><span data-stu-id="cd471-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="cd471-425">measure 명령에 집계 절을 여러 개 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="cd471-426">각 절에는 개별적으로 별칭을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="cd471-427">별칭을 지정하지 않으면, 사용된 집계 함수가 필드 이름이 됩니다(예: avg(CounterValue)의 경우 "avg(CounterValue)").</span><span class="sxs-lookup"><span data-stu-id="cd471-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="cd471-429">다른 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="cd471-430">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd471-430">Next steps</span></span>
<span data-ttu-id="cd471-431">로그 검색에 대한 자세한 내용은 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cd471-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="cd471-432">[Log Analytics의 사용자 지정 필드](log-analytics-custom-fields.md) 를 사용하여 로그 검색을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="cd471-433">Log Analytics에 제공되는 모든 검색 필드 및 패싯을 보려면 [Log Analytics log search reference](log-analytics-search-reference.md) (Log Analytics 로그 검색 참조)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="cd471-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
