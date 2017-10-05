---
title: "Azure Log Analytics 검색 참조 | Microsoft Docs"
description: "Log Analytics 검색 참조는 검색 언어에 대해 설명하며 데이터를 검색하고 검색 결과를 좁히기 위한 식을 필터링할 때 사용할 수 있는 일반 쿼리 구문 옵션을 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc9c9b0a6292dab256997a86a6db16367fc48cd3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="d2231-103">Log Analytics 검색 참조</span><span class="sxs-lookup"><span data-stu-id="d2231-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="d2231-104">이 문서에서는 Log Analytics에서 최신 쿼리 언어를 사용하는 로그 검색에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="d2231-105">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 [새 언어용 언어 참조](https://go.microsoft.com/fwlink/?linkid=856079)를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [the language reference for the new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="d2231-106">검색 언어에 대한 다음의 참조 섹션은 데이터 및 필터링 식을 검색할 때 사용할 수 있는 일반 쿼리 구문 옵션을 설명하여 검색 범위를 좁힐 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-106">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span></span> <span data-ttu-id="d2231-107">검색된 데이터에 조치로 사용할 수 있는 명령을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-107">It also describes commands that you can use to take action on the data retrieved.</span></span>

<span data-ttu-id="d2231-108">[필드 및 패싯 참조 검색 섹션](#search-field-and-facet-reference)에서 유사한 데이터 범주에 관하여 더 자세한 정보를 검색할 수 있는 검색 및 패싯을 반환하는 필드에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-108">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="d2231-109">일반 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="d2231-109">General query syntax</span></span>
<span data-ttu-id="d2231-110">일반 쿼리에 대한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-110">The syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="d2231-111">필터 식(`filterExpression`)은 쿼리에 "where" 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-111">The filter expression (`filterExpression`) defines the "where" condition for the query.</span></span> <span data-ttu-id="d2231-112">명령은 쿼리에 의해 반환된 결과에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-112">The commands apply to the results returned by the query.</span></span> <span data-ttu-id="d2231-113">여러 명령은 세로줄 문자(|)로 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-113">Multiple commands must be separated by the pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="d2231-114">일반 구문 예제</span><span class="sxs-lookup"><span data-stu-id="d2231-114">General syntax examples</span></span>
<span data-ttu-id="d2231-115">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-115">Examples:</span></span>

```
system
```

<span data-ttu-id="d2231-116">이 쿼리는 전체 텍스트 또는 검색 조건에 인덱싱된 모든 필드에서 단어 *시스템*을 포함하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-116">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="d2231-117">모든 필드가 이러한 방식으로 인덱싱되지 않지만 가장 일반적인 텍스트 필드(예: 설명 및 이름)는 대개 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-117">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="d2231-118">이 쿼리는 *system*과 *error* 단어를 포함하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-118">This query returns results that contain the words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="d2231-119">이 쿼리는 *system*과 *error* 단어를 포함하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-119">This query returns results that contain the words *system* and *error*.</span></span> <span data-ttu-id="d2231-120">그런 다음 *ManagementGroupName* 필드를 기준으로 결과를 정렬한 다음(오름차순) *TimeGenerated* 필드를 기준으로 정렬합니다(내림차순).</span><span class="sxs-lookup"><span data-stu-id="d2231-120">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="d2231-121">처음 10개의 결과만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-121">It takes only the first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2231-122">모든 필드 이름과 문자열 및 텍스트 필드에 대한 값은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-122">All the field names and the values for the string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="d2231-123">필터 식</span><span class="sxs-lookup"><span data-stu-id="d2231-123">Filter expressions</span></span>
<span data-ttu-id="d2231-124">다음 하위 섹션에서 필터 식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-124">The following subsections explain the filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="d2231-125">문자열 리터럴</span><span class="sxs-lookup"><span data-stu-id="d2231-125">String literals</span></span>
<span data-ttu-id="d2231-126">리터럴 문자열은 키워드 또는 미리 정의된 데이터 형식(예: 숫자 또는 날짜)으로 파서에서 인식되지 않은 모든 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-126">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="d2231-127">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="d2231-128">이 쿼리는 발생하는 5개 단어를 모두 포함하는 결과를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="d2231-129">복잡한 문자열 검색을 수행하려면 문자열 리터럴을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-129">To perform a complex string search, enclose the string literal in quotation marks.</span></span> <span data-ttu-id="d2231-130">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="d2231-131">*Windows Server*와 정확히 일치하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="d2231-132">숫자</span><span class="sxs-lookup"><span data-stu-id="d2231-132">Numbers</span></span>
<span data-ttu-id="d2231-133">파서는 숫자 필드에 10 진수 정수 및 부동 소수점 수 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-133">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="d2231-134">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="d2231-135">날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="d2231-135">Dates and times</span></span>
<span data-ttu-id="d2231-136">시스템에서 데이터의 모든 부분에 원래 날짜와 레코드의 시간을 나타내는 *TimeGenerated* 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-136">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span></span> <span data-ttu-id="d2231-137">또한 일부 데이터 형식에 더 많은 날짜 및 시간 필드가 있을 수 있습니다(예를 들어 *LastModified*).</span><span class="sxs-lookup"><span data-stu-id="d2231-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="d2231-138">Log Analytics에서 타임라인 **차트/시간** 선택기는 (현재 실행되는 쿼리에 따라) 시간별 결과 분포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-138">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span></span> <span data-ttu-id="d2231-139">이는 *TimeGenerated* 필드를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-139">This is based on the *TimeGenerated* field.</span></span> <span data-ttu-id="d2231-140">날짜 및 시간 필드는 쿼리에 사용할 수 있는 특정 문자열 형식이 있어서 특정 기간에 쿼리를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-140">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span></span> <span data-ttu-id="d2231-141">또한 상대적 시간 간격을 참조하도록 구문을 사용할 수 있습니다.(예를 들어 "3일 전 및 2시간 전")</span><span class="sxs-lookup"><span data-stu-id="d2231-141">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="d2231-142">다음은 날짜 및 시간에 유효한 형식의 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-142">The following are valid forms of syntax for dates and times:</span></span>

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


<span data-ttu-id="d2231-143">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="d2231-144">이전 명령은 정확하게 2013년 10월 1일 12시 20분이라는 *TimeGenerated* 값으로 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-144">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="d2231-145">또한 파서가 mnemonic 날짜/시간 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-145">The parser also supports the mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="d2231-146">(데이터가 빠른 시스템을 통과하지 않기 때문에 모든 결과를 일시 중단할 가능성이 적습니다.)</span><span class="sxs-lookup"><span data-stu-id="d2231-146">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span></span>

<span data-ttu-id="d2231-147">이러한 예제는 상대 및 절대 날짜에 사용할 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-147">These examples are building blocks to use for relative and absolute dates.</span></span> <span data-ttu-id="d2231-148">다음 세 하위 섹션에서 상대 날짜 범위를 사용하는 예제를 고급 필터에서 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-148">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="d2231-149">날짜/시간 수학</span><span class="sxs-lookup"><span data-stu-id="d2231-149">Date/Time math</span></span>
<span data-ttu-id="d2231-150">간단한 날짜/시간 계산을 사용하여 날짜/시간 수학 연산자로 날짜/시간 값을 오프셋 또는 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-150">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="d2231-151">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="d2231-152">연산자</span><span class="sxs-lookup"><span data-stu-id="d2231-152">Operator</span></span> | <span data-ttu-id="d2231-153">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="d2231-154">날짜/시간을 지정된 단위로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-154">Rounds Date/Time to the specified unit.</span></span> <span data-ttu-id="d2231-155">예를 들어 NOW/DAY는 현재 날짜의 자정으로 현재 날짜/시간을 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-155">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span></span> |
| <span data-ttu-id="d2231-156">+ 또는-</span><span class="sxs-lookup"><span data-stu-id="d2231-156">+ or -</span></span> |<span data-ttu-id="d2231-157">단위의 지정한 수 만큼 날짜/시간을 오프셋합니다 예:NOW+1HOUR는 현재 날짜/시간을 한 시간 앞으로 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-157">Offsets Date/Time by the specified number of units.</span></span> <span data-ttu-id="d2231-158">예를 들어 NOW+1HOUR는 현재 날짜/시간을 한 시간 만큼 앞당겨 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-158">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span></span> <span data-ttu-id="d2231-159">2013-10-01T12:00-10DAYS는 날짜 값을 10일 전으로 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-159">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span></span> |

<span data-ttu-id="d2231-160">날짜/시간 산술 연산자를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-160">You can chain the Date/Time math operators together.</span></span> <span data-ttu-id="d2231-161">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="d2231-162">다음 테이블에서 지원되는 날짜/시간 단위를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-162">The following table lists the supported Date/Time units.</span></span>

| <span data-ttu-id="d2231-163">날짜/시간 단위</span><span class="sxs-lookup"><span data-stu-id="d2231-163">Date/Time unit</span></span> | <span data-ttu-id="d2231-164">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d2231-165">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="d2231-165">YEAR, YEARS</span></span> |<span data-ttu-id="d2231-166">현재 연도를 반올림하거나 지정된 년 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-166">Rounds to current year, or offsets by the specified number of years.</span></span> |
| <span data-ttu-id="d2231-167">MONTH, MONTHS</span><span class="sxs-lookup"><span data-stu-id="d2231-167">MONTH, MONTHS</span></span> |<span data-ttu-id="d2231-168">현재 월을 반올림하거나 지정된 개월 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-168">Rounds to current month, or offsets by the specified number of months.</span></span> |
| <span data-ttu-id="d2231-169">DAY, DAYS, DATE</span><span class="sxs-lookup"><span data-stu-id="d2231-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="d2231-170">현재 날을 반올림하거나 지정된 일 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-170">Rounds to current day of the month, or offsets by the specified number of days.</span></span> |
| <span data-ttu-id="d2231-171">HOUR, HOURS</span><span class="sxs-lookup"><span data-stu-id="d2231-171">HOUR, HOURS</span></span> |<span data-ttu-id="d2231-172">현재 시간을 반올림하거나 지정된 시간 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-172">Rounds to current hour, or offsets by the specified number of hours.</span></span> |
| <span data-ttu-id="d2231-173">MINUTE, MINUTES</span><span class="sxs-lookup"><span data-stu-id="d2231-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="d2231-174">현재 분을 반올림하거나 지정된 분 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-174">Rounds to current minute, or offsets by the specified number of minutes.</span></span> |
| <span data-ttu-id="d2231-175">SECOND, SECONDS</span><span class="sxs-lookup"><span data-stu-id="d2231-175">SECOND, SECONDS</span></span> |<span data-ttu-id="d2231-176">현재 초를 반올림하거나 지정된 초 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-176">Rounds to current second, or offsets by the specified number of seconds.</span></span> |
| <span data-ttu-id="d2231-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="d2231-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="d2231-178">현재 밀리초를 반올림하거나 지정된 밀리초 수 만큼 오프셋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-178">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="d2231-179">필드 패싯</span><span class="sxs-lookup"><span data-stu-id="d2231-179">Field facets</span></span>
<span data-ttu-id="d2231-180">필드 패싯을 사용하여 특정 필드와 해당 정확한 값에 대한 검색 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-180">By using field facets, you can specify the search condition for specific fields and their exact values.</span></span> <span data-ttu-id="d2231-181">이는 인덱스 전반에 걸쳐 여러 용어에 대한 “자유 텍스트” 쿼리를 작성하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-181">This differs from writing "free text" queries for various terms throughout the index.</span></span> <span data-ttu-id="d2231-182">여러 개의 이전 예에서 이 기법을 이미 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="d2231-183">다음은 더 복잡한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-183">The following are more complex examples.</span></span>

<span data-ttu-id="d2231-184">**구문**</span><span class="sxs-lookup"><span data-stu-id="d2231-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="d2231-185">**설명**</span><span class="sxs-lookup"><span data-stu-id="d2231-185">**Description**</span></span>

<span data-ttu-id="d2231-186">특정 값에 대한 필드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-186">Searches the field for the specific value.</span></span> <span data-ttu-id="d2231-187">값은 문자열 리터럴, 숫자 또는 날짜 및 시간일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-187">The value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="d2231-188">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="d2231-189">**구문**</span><span class="sxs-lookup"><span data-stu-id="d2231-189">**Syntax**</span></span>

<span data-ttu-id="d2231-190">*field>value*</span><span class="sxs-lookup"><span data-stu-id="d2231-190">*field>value*</span></span>

<span data-ttu-id="d2231-191">*field<value*</span><span class="sxs-lookup"><span data-stu-id="d2231-191">*field<value*</span></span>

<span data-ttu-id="d2231-192">*field>=value*</span><span class="sxs-lookup"><span data-stu-id="d2231-192">*field>=value*</span></span>

<span data-ttu-id="d2231-193">*field<=value*</span><span class="sxs-lookup"><span data-stu-id="d2231-193">*field<=value*</span></span>

<span data-ttu-id="d2231-194">*field!=value*</span><span class="sxs-lookup"><span data-stu-id="d2231-194">*field!=value*</span></span>

<span data-ttu-id="d2231-195">**설명**</span><span class="sxs-lookup"><span data-stu-id="d2231-195">**Description**</span></span>

<span data-ttu-id="d2231-196">비교를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-196">Provides comparisons.</span></span>

<span data-ttu-id="d2231-197">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="d2231-198">**구문**</span><span class="sxs-lookup"><span data-stu-id="d2231-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="d2231-199">**설명**</span><span class="sxs-lookup"><span data-stu-id="d2231-199">**Description**</span></span>

<span data-ttu-id="d2231-200">패싯 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-200">Provides range faceting.</span></span>

<span data-ttu-id="d2231-201">예:</span><span class="sxs-lookup"><span data-stu-id="d2231-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="d2231-202">IN</span><span class="sxs-lookup"><span data-stu-id="d2231-202">IN</span></span>
<span data-ttu-id="d2231-203">**IN** 키워드를 사용하여 값 목록에서 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-203">The **IN** keyword allows you to select from a list of values.</span></span> <span data-ttu-id="d2231-204">사용하는 구문에 따라 사용자가 제공한 간단한 값 목록이거나 집계 값 목록일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-204">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="d2231-205">구문 1:</span><span class="sxs-lookup"><span data-stu-id="d2231-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="d2231-206">이 구문을 통해 간단한 목록에 모든 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-206">This syntax allows you to include all values in a simple list.</span></span>



<span data-ttu-id="d2231-207">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="d2231-208">구문 2:</span><span class="sxs-lookup"><span data-stu-id="d2231-208">Syntax 2:</span></span>

```
(Outer query) (Field to use with inner query results) IN {Inner query | measure count() by (Field to send to outer query)} (rest  of outer query)  
```

<span data-ttu-id="d2231-209">이 구문을 사용하여 집계를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-209">This syntax allows you to create an aggregation.</span></span> <span data-ttu-id="d2231-210">그런 다음 값의 목록을 집계에서 다른 외부(기본) 검색으로 피드하고 해당 값을 사용하여 이벤트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-210">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="d2231-211">그렇게 하려면 내부 검색을 괄호로 묶고 그 결과를 IN 연산자를 사용하는 외부 검색 필드에 가능한 값으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-211">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span></span>

<span data-ttu-id="d2231-212">내부 쿼리 예제: 다음 집계 쿼리에서 *현재 보안 업데이트가 없는 컴퓨터*:</span><span class="sxs-lookup"><span data-stu-id="d2231-212">Inner query example: *computers currently missing security updates* with the following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="d2231-213">*현재 보안 업데이트가 없는 컴퓨터의 모든 Windows 이벤트*를 검색하는 최종 쿼리는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-213">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="d2231-214">포함</span><span class="sxs-lookup"><span data-stu-id="d2231-214">Contains</span></span>
<span data-ttu-id="d2231-215">**포함** 키워드를 사용하여 지정된 문자열을 포함하는 필드를 가진 레코드를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-215">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span></span> <span data-ttu-id="d2231-216">이는 대/소문자를 구분하고 문자열 필드에 대해서만 작동하며 이스케이프 문자를 포함하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="d2231-217">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="d2231-218">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="d2231-219">이는 문자열 “이벤트”를 포함하는 형식을 가진 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-219">This returns records with a type that contains the string "Event".</span></span> <span data-ttu-id="d2231-220">예를 들어 **이벤트**, **SecurityEvent** 및 **ServiceFabricOperationEvent**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="d2231-221">정규식</span><span class="sxs-lookup"><span data-stu-id="d2231-221">Regular expressions</span></span>
<span data-ttu-id="d2231-222">**Regex** 키워드를 사용하여 정규식을 포함한 필드에 대한 검색 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-222">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span></span> <span data-ttu-id="d2231-223">정규식에 사용할 수 있는 구문에 대한 전체 설명은 [정규식을 사용하여 Log Analytics에서 로그 검색 필터링](log-analytics-log-searches-regex.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2231-223">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="d2231-224">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="d2231-225">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="d2231-226">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="d2231-226">Logical operators</span></span>
<span data-ttu-id="d2231-227">쿼리 언어는 논리 연산자(*AND*, *OR* 및 *NOT*)와 각각의 C-스타일 별칭(*&&*, *||* 및 *!*)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-227">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="d2231-228">이러한 연산자를 그룹화하려면 괄호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-228">You can use parentheses to group these operators.</span></span>

<span data-ttu-id="d2231-229">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="d2231-230">최상위 필터 인수에서 논리 연산자를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-230">You can omit the logical operator for the top-level filter arguments.</span></span> <span data-ttu-id="d2231-231">이 경우 AND 연산자를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-231">In this case, the AND operator is assumed.</span></span>

| <span data-ttu-id="d2231-232">필터 식</span><span class="sxs-lookup"><span data-stu-id="d2231-232">Filter expression</span></span> | <span data-ttu-id="d2231-233">Equivalent to</span><span class="sxs-lookup"><span data-stu-id="d2231-233">Equivalent to</span></span> |
| --- | --- |
| <span data-ttu-id="d2231-234">시스템 오류</span><span class="sxs-lookup"><span data-stu-id="d2231-234">system error</span></span> |<span data-ttu-id="d2231-235">시스템 AND 오류</span><span class="sxs-lookup"><span data-stu-id="d2231-235">system AND error</span></span> |
| <span data-ttu-id="d2231-236">시스템 "Windows Server" OR 심각도:1</span><span class="sxs-lookup"><span data-stu-id="d2231-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="d2231-237">시스템 AND ("Windows Server" OR 심각도:1)</span><span class="sxs-lookup"><span data-stu-id="d2231-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="d2231-238">와일드 카드 사용</span><span class="sxs-lookup"><span data-stu-id="d2231-238">Wildcarding</span></span>
<span data-ttu-id="d2231-239">쿼리 언어는 쿼리의 값에 대해 하나 이상의 문자를 나타내는 (\*) 문자 사용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-239">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="d2231-240">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-240">Example:</span></span>

 <span data-ttu-id="d2231-241">"Redmond-SQL"과 같이 이름에 "SQL"이 포함된 모든 컴퓨터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-241">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="d2231-242">현재 와일드 카드는 따옴표 안에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="d2231-243">예를 들어 `"*This text*"` 메시지는 리터럴(\*) 문자로 사용하는 것(\*)을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-243">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="d2231-244">명령</span><span class="sxs-lookup"><span data-stu-id="d2231-244">Commands</span></span>


<span data-ttu-id="d2231-245">명령은 쿼리에 의해 반환된 결과에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-245">The commands apply to the results that are returned by the query.</span></span> <span data-ttu-id="d2231-246">파이프 문자(|)를 사용하여 검색된 결과에 명령을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-246">Use the pipe character ( | ) to apply a command to the retrieved results.</span></span> <span data-ttu-id="d2231-247">여러 명령은 세로줄 문자로 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-247">Multiple commands must be separated by the pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="d2231-248">명령 이름은 필드 이름 및 데이터와는 달리 대문자 또는 소문자로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-248">Command names can be written in upper case or lower case, unlike the field names and the data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="d2231-249">정렬</span><span class="sxs-lookup"><span data-stu-id="d2231-249">Sort</span></span>
<span data-ttu-id="d2231-250">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="d2231-251">특정 필드에 의한 결과를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-251">Sorts the results by particular fields.</span></span> <span data-ttu-id="d2231-252">결과를 오름차순 또는 내림차순으로 정렬하는 asc/desc 접미사는 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-252">The asc/desc suffix to sort the results in ascending or descending order is optional.</span></span> <span data-ttu-id="d2231-253">누락된 경우 *asc* 정렬 순서를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-253">If it is omitted, the *asc* sort order is assumed.</span></span> <span data-ttu-id="d2231-254">**TimeGenerated** 필드의 경우 *desc* 정렬 순서를 가정하므로 기본적으로 최근 결과를 먼저 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-254">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="d2231-255">위쪽/제한</span><span class="sxs-lookup"><span data-stu-id="d2231-255">Top/Limit</span></span>
<span data-ttu-id="d2231-256">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="d2231-257">상위 N개 결과에 대한 응답을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-257">Limits the response to the top N results.</span></span>

<span data-ttu-id="d2231-258">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="d2231-259">상위 10개의 일치하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-259">Returns the top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="d2231-260">Skip</span><span class="sxs-lookup"><span data-stu-id="d2231-260">Skip</span></span>
<span data-ttu-id="d2231-261">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-261">Syntax:</span></span>

    skip number

<span data-ttu-id="d2231-262">나열된 결과의 수를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-262">Skips the number of results listed.</span></span>

<span data-ttu-id="d2231-263">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="d2231-264">200개 결과에서 시작하여 상위 10개의 일치하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="d2231-265">여기서</span><span class="sxs-lookup"><span data-stu-id="d2231-265">Select</span></span>
<span data-ttu-id="d2231-266">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="d2231-267">선택한 필드에 대한 결과를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-267">Limits results to the fields you choose.</span></span>

<span data-ttu-id="d2231-268">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="d2231-269">*이름* and *심각도*에서 데이터와 유사한 범주를 dill-into하는 검색 및 패싯을 반환하는 필드에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-269">Limits the returned results fields to *Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="d2231-270">측정값</span><span class="sxs-lookup"><span data-stu-id="d2231-270">Measure</span></span>
<span data-ttu-id="d2231-271">*측정값* 명령은 통계 함수를 원시 검색 결과에 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-271">The *measure* command is used to apply statistical functions to the raw search results.</span></span> <span data-ttu-id="d2231-272">이 명령은 데이터에서 *group-by* 보기를 가져오는 데 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-272">This is very useful to get *group-by* views over the data.</span></span> <span data-ttu-id="d2231-273">measure 명령을 사용하는 경우 Log Analytics 검색은 집계된 결과가 포함된 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-273">When you use the measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="d2231-274">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d2231-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="d2231-275">*groupField*를 기준으로 결과를 집계하고 *aggregatedField*를 사용하여 집계된 측정값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-275">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="d2231-276">측정 통계 함수</span><span class="sxs-lookup"><span data-stu-id="d2231-276">Measure statistical function</span></span> | <span data-ttu-id="d2231-277">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d2231-278">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="d2231-278">*aggregateFunction*</span></span> |<span data-ttu-id="d2231-279">집계 함수의 이름(대소문자 구분).</span><span class="sxs-lookup"><span data-stu-id="d2231-279">The name of the aggregate function (case insensitive).</span></span> <span data-ttu-id="d2231-280">다음 집계 함수가 지원됩니다. COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE## 또는 PCT##(##은 1 ~ 99 사이의 숫자).</span><span class="sxs-lookup"><span data-stu-id="d2231-280">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="d2231-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="d2231-281">*aggregatedField*</span></span> |<span data-ttu-id="d2231-282">집계되고 있는 필드.</span><span class="sxs-lookup"><span data-stu-id="d2231-282">The field that is being aggregated.</span></span> <span data-ttu-id="d2231-283">이 필드는 COUNT 집계 함수에 대해 선택적이지만 SUM, MAX, MIN, AVG STDDEV, PERCENTILE## 또는 PCT##(##은 1 ~ 99 사이의 숫자)의 기존 숫자 필드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-283">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="d2231-284">또한 aggregatedField는 **Extend** 지원 함수 중 하나일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-284">The aggregatedField can also be any of the **Extend** supported functions.</span></span> |
| <span data-ttu-id="d2231-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="d2231-285">*fieldAlias*</span></span> |<span data-ttu-id="d2231-286">(선택 사항) 계산된 집계 값의 별칭.</span><span class="sxs-lookup"><span data-stu-id="d2231-286">The (optional) alias for the calculated aggregated value.</span></span> <span data-ttu-id="d2231-287">지정하지 않을 경우 필드 이름은 **AggregatedValue**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-287">If not specified, the field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="d2231-288">*groupField*</span><span class="sxs-lookup"><span data-stu-id="d2231-288">*groupField*</span></span> |<span data-ttu-id="d2231-289">결과 집합을 그룹화하는 기준이 되는 필드의 이름</span><span class="sxs-lookup"><span data-stu-id="d2231-289">The name of the field that the result set is grouped by.</span></span> |
| <span data-ttu-id="d2231-290">*간격*</span><span class="sxs-lookup"><span data-stu-id="d2231-290">*Interval*</span></span> |<span data-ttu-id="d2231-291">**nnnNAME** 형식의 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-291">The time interval, in the format:**nnnNAME**.</span></span> <span data-ttu-id="d2231-292">**nnn**은 양의 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-292">**nnn** is the positive integer number.</span></span> <span data-ttu-id="d2231-293">**NAME**은 간격 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-293">**NAME** is the interval name.</span></span> <span data-ttu-id="d2231-294">지원되는 간격 이름은 대/소문자를 구분하며 MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S] 및 YEAR[S]를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="d2231-295">날짜/시간 그룹 필드에서만 간격 옵션을 사용할 수 있습니다(예: *TimeGenerated* and *TimeCreated*)</span><span class="sxs-lookup"><span data-stu-id="d2231-295">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="d2231-296">현재 서비스에 의해 적용되지 않지만 백 엔드로 전달되는 날짜/시간 없는 필드에 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-296">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span></span> <span data-ttu-id="d2231-297">스키마 유효성 검사를 구현하는 경우 서비스 API는 집계 간격에 대해 날짜/시간 없이 필드를 사용하는 쿼리를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-297">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="d2231-298">현재 *Measure* 구현은 집계 함수를 그룹화하는 간격을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-298">The current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="d2231-299">BY 절을 생략하지만 간격을 지정하는 경우(두 번째 구문처럼) 기본적으로 *TimeGenerated* 필드를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-299">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="d2231-300">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-300">Examples:</span></span>

<span data-ttu-id="d2231-301">**예 1**</span><span class="sxs-lookup"><span data-stu-id="d2231-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="d2231-302">*ObjectID* 에서 경고를 그룹화하고 각 그룹에 대한 경고의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-302">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span></span> <span data-ttu-id="d2231-303">집계된 값을 *Count* 필드(별칭)로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-303">The aggregated value is returned as the *Count* field (alias).</span></span>

<span data-ttu-id="d2231-304">**예 2**</span><span class="sxs-lookup"><span data-stu-id="d2231-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="d2231-305">*TimeGenerated* 필드를 사용하여 1시간 간격으로 경고를 그룹화하고 각 간격의 경고 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-305">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span></span>

<span data-ttu-id="d2231-306">**예 3**</span><span class="sxs-lookup"><span data-stu-id="d2231-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="d2231-307">이전 예제와 동일하지만 집계된 필드 별칭을 사용합니다.(*AlertsPerHour*)</span><span class="sxs-lookup"><span data-stu-id="d2231-307">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="d2231-308">**예제 4**</span><span class="sxs-lookup"><span data-stu-id="d2231-308">**Example 4**</span></span>

    * <span data-ttu-id="d2231-309">| measure count() by TimeCreated interval 5DAYS</span><span class="sxs-lookup"><span data-stu-id="d2231-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="d2231-310">*TimeCreated* 필드를 사용하여 5일 간격으로 결과를 그룹화하고 각 간격의 결과 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-310">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span></span>

<span data-ttu-id="d2231-311">**예제 5**</span><span class="sxs-lookup"><span data-stu-id="d2231-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="d2231-312">워크로드 이름 별로 경고를 그룹화하고 각 워크플로에 대한 최대 경고 심각도 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-312">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="d2231-313">**예제 6**</span><span class="sxs-lookup"><span data-stu-id="d2231-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="d2231-314">이전 예제와 동일하지만 *min* 집계 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-314">Same as the previous example, but with the *min* aggregated function.</span></span>

<span data-ttu-id="d2231-315">**예제 7**</span><span class="sxs-lookup"><span data-stu-id="d2231-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="d2231-316">컴퓨터별로 성능을 그룹화하고 평균(avg)을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-316">Groups Perf by computer, and calculates the average (avg).</span></span>

<span data-ttu-id="d2231-317">**예제 8**</span><span class="sxs-lookup"><span data-stu-id="d2231-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="d2231-318">이전 예제와 동일하지만 *sum*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-318">Same as the previous example, but uses *sum*.</span></span>

<span data-ttu-id="d2231-319">**예제 9**</span><span class="sxs-lookup"><span data-stu-id="d2231-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="d2231-320">이전 예제와 동일하지만 *stddev*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-320">Same as the previous example, but uses *stddev*.</span></span>

<span data-ttu-id="d2231-321">**예제 10**</span><span class="sxs-lookup"><span data-stu-id="d2231-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="d2231-322">이전 예제와 동일하지만 *percentile70*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-322">Same as the previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="d2231-323">**예제 11**</span><span class="sxs-lookup"><span data-stu-id="d2231-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="d2231-324">이전 예제와 동일하지만 *pct70*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-324">Same as the previous example, but uses *pct70*.</span></span> <span data-ttu-id="d2231-325">*PCT##*은 *PERCENTILE##* 함수의 유일한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="d2231-326">**예제 12**</span><span class="sxs-lookup"><span data-stu-id="d2231-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="d2231-327">Computer별로 성능을 그룹화하고 CounterName을 기준으로 그룹화한 다음 평균(avg)을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-327">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span></span>

<span data-ttu-id="d2231-328">**예제 13**</span><span class="sxs-lookup"><span data-stu-id="d2231-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="d2231-329">경고의 최대 수와 상위 5개 워크플로를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-329">Gets the top five workflows with the maximum number of alerts.</span></span>

<span data-ttu-id="d2231-330">**예제 14**</span><span class="sxs-lookup"><span data-stu-id="d2231-330">**Example 14**</span></span>

    * <span data-ttu-id="d2231-331">| measure countdistinct(Computer) by Type</span><span class="sxs-lookup"><span data-stu-id="d2231-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="d2231-332">각 유형에 대해 보고하는 고유 컴퓨터의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-332">Counts the number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="d2231-333">**예제 15**</span><span class="sxs-lookup"><span data-stu-id="d2231-333">**Example 15**</span></span>

    * <span data-ttu-id="d2231-334">| measure countdistinct(Computer) Interval 1HOUR</span><span class="sxs-lookup"><span data-stu-id="d2231-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="d2231-335">매 시간별로 보고하는 고유 컴퓨터의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-335">Counts the number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="d2231-336">**예제 16**</span><span class="sxs-lookup"><span data-stu-id="d2231-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="d2231-337">컴퓨터별로 % Processor Time을 그룹화하고 매 시간당 평균을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-337">Groups % Processor Time by Computer, and returns the average for every hour.</span></span>

<span data-ttu-id="d2231-338">**예제 17**</span><span class="sxs-lookup"><span data-stu-id="d2231-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="d2231-339">W3CIISLog를 메서드별로 그룹화하고 5분마다 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-339">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span></span>

<span data-ttu-id="d2231-340">**예제 18**</span><span class="sxs-lookup"><span data-stu-id="d2231-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="d2231-341">컴퓨터별로 % Processor Time을 그룹화하고 매 시간당 최소값, 평균, 75번째 백분위수 및 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-341">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="d2231-342">**예제 19**</span><span class="sxs-lookup"><span data-stu-id="d2231-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="d2231-343">컴퓨터별로 % Processor Time을 그룹화하고 인스턴스 이름을 기준으로 그룹화한 다음 매 시간당 최소값, 평균, 75번째 백분위수, 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-343">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="d2231-344">**예제 20**</span><span class="sxs-lookup"><span data-stu-id="d2231-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="d2231-345">컴퓨터의 모든 디스크에 대한 분당 최대 디스크 쓰기 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-345">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="d2231-346">Where</span><span class="sxs-lookup"><span data-stu-id="d2231-346">Where</span></span>
<span data-ttu-id="d2231-347">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="d2231-348">*Measure* 명령 뒤에만 사용하여 *Measure* 집계 함수가 만든 집계 결과를 자세히 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-348">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="d2231-349">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="d2231-350">Dedup</span><span class="sxs-lookup"><span data-stu-id="d2231-350">Dedup</span></span>
<span data-ttu-id="d2231-351">구문</span><span class="sxs-lookup"><span data-stu-id="d2231-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="d2231-352">특정 필드의 모든 고유 값에 대해 검색된 첫 번째 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-352">Returns the first document found for every unique value of the given field.</span></span>

<span data-ttu-id="d2231-353">예제:</span><span class="sxs-lookup"><span data-stu-id="d2231-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="d2231-354">이 예제는 EventID마다 한 개의 이벤트(최신 이벤트)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-354">This example returns one event (the latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="d2231-355">Join</span><span class="sxs-lookup"><span data-stu-id="d2231-355">Join</span></span>
<span data-ttu-id="d2231-356">두 쿼리의 결과를 조인하여 단일 결과 집합을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-356">Joins the results of two queries to form a single result set.</span></span>  <span data-ttu-id="d2231-357">다음 표에 설명된 여러 개의 조인 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-357">Supports multiple join types described in the follow table.</span></span>

| <span data-ttu-id="d2231-358">조인 유형</span><span class="sxs-lookup"><span data-stu-id="d2231-358">Join type</span></span> | <span data-ttu-id="d2231-359">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="d2231-360">inner</span><span class="sxs-lookup"><span data-stu-id="d2231-360">inner</span></span> | <span data-ttu-id="d2231-361">두 쿼리 모두 일치하는 값을 가진 레코드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="d2231-362">outer</span><span class="sxs-lookup"><span data-stu-id="d2231-362">outer</span></span> | <span data-ttu-id="d2231-363">두 쿼리 모두에서 모든 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="d2231-364">left</span><span class="sxs-lookup"><span data-stu-id="d2231-364">left</span></span>  | <span data-ttu-id="d2231-365">왼쪽 쿼리의 모든 레코드와 오른쪽 쿼리에서 일치하는 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="d2231-366">조인 기능은 오른쪽 쿼리의 필드가 대상인 경우 **IN** 키워드, **Measure** 명령 또는 **Extend** 명령을 포함하는 쿼리를 현재 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-366">Joins do not currently support queries that include the **IN** keyword, the **Measure** command or the **Extend** command if it targets a field from the right query.</span></span>
- <span data-ttu-id="d2231-367">현재는 조인에 단일 필드만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="d2231-368">단일 검색에서 둘 이상의 조인이 포함되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="d2231-369">**구문**</span><span class="sxs-lookup"><span data-stu-id="d2231-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="d2231-370">**예**</span><span class="sxs-lookup"><span data-stu-id="d2231-370">**Examples**</span></span>

<span data-ttu-id="d2231-371">다른 조인 유형을 설명하려면 MyBackup_CL이라는 사용자 지정 로그에서 수집한 데이터 형식을 각 컴퓨터의 하트비트와 조인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-371">To illustrate the different join types, consider joining a data type collected from a custom log called MyBackup_CL with the heartbeat for each computer.</span></span>  <span data-ttu-id="d2231-372">이러한 데이터 형식에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-372">These datatypes have the following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="d2231-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-373">TimeGenerated</span></span> | <span data-ttu-id="d2231-374">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-374">Computer</span></span> | <span data-ttu-id="d2231-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="d2231-376">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="d2231-377">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-377">srv01.contoso.com</span></span> | <span data-ttu-id="d2231-378">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-378">Success</span></span> |
| <span data-ttu-id="d2231-379">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="d2231-380">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-380">srv02.contoso.com</span></span> | <span data-ttu-id="d2231-381">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-381">Success</span></span> |
| <span data-ttu-id="d2231-382">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="d2231-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-383">srv03.contoso.com</span></span> | <span data-ttu-id="d2231-384">실패</span><span class="sxs-lookup"><span data-stu-id="d2231-384">Failure</span></span> |

<span data-ttu-id="d2231-385">`Type = Hearbeat`(표시된 필드의 하위 집합만)</span><span class="sxs-lookup"><span data-stu-id="d2231-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="d2231-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-386">TimeGenerated</span></span> | <span data-ttu-id="d2231-387">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-387">Computer</span></span> | <span data-ttu-id="d2231-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="d2231-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="d2231-389">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="d2231-390">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-390">srv01.contoso.com</span></span> | <span data-ttu-id="d2231-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="d2231-391">10.10.100.1</span></span> |
| <span data-ttu-id="d2231-392">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="d2231-393">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-393">srv02.contoso.com</span></span> | <span data-ttu-id="d2231-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="d2231-394">10.10.100.2</span></span> |
| <span data-ttu-id="d2231-395">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="d2231-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-396">srv04.contoso.com</span></span> | <span data-ttu-id="d2231-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="d2231-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="d2231-398">내부 조인</span><span class="sxs-lookup"><span data-stu-id="d2231-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="d2231-399">두 데이터 형식 모두에 대해 컴퓨터 필드가 일치하는 다음 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-399">Returns the following records where the computer field matches for both datatypes.</span></span>

| <span data-ttu-id="d2231-400">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-400">Computer</span></span>| <span data-ttu-id="d2231-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-401">TimeGenerated</span></span> | <span data-ttu-id="d2231-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-402">LastBackupStatus</span></span> | <span data-ttu-id="d2231-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-403">TimeGenerated_joined</span></span> | <span data-ttu-id="d2231-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-404">ComputerIP_joined</span></span> | <span data-ttu-id="d2231-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="d2231-406">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-406">srv01.contoso.com</span></span> | <span data-ttu-id="d2231-407">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="d2231-408">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-408">Success</span></span> | <span data-ttu-id="d2231-409">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="d2231-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="d2231-410">10.10.100.1</span></span> | <span data-ttu-id="d2231-411">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-411">Heartbeat</span></span> |
| <span data-ttu-id="d2231-412">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-412">srv02.contoso.com</span></span> | <span data-ttu-id="d2231-413">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="d2231-414">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-414">Success</span></span> | <span data-ttu-id="d2231-415">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="d2231-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="d2231-416">10.10.100.2</span></span> | <span data-ttu-id="d2231-417">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="d2231-418">외부 조인</span><span class="sxs-lookup"><span data-stu-id="d2231-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="d2231-419">두 데이터 형식 모두에 대해 다음 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-419">Returns the following records for both datatypes.</span></span>

| <span data-ttu-id="d2231-420">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-420">Computer</span></span>| <span data-ttu-id="d2231-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-421">TimeGenerated</span></span> | <span data-ttu-id="d2231-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-422">LastBackupStatus</span></span> | <span data-ttu-id="d2231-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-423">TimeGenerated_joined</span></span> | <span data-ttu-id="d2231-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-424">ComputerIP_joined</span></span> | <span data-ttu-id="d2231-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="d2231-426">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-426">srv01.contoso.com</span></span> | <span data-ttu-id="d2231-427">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="d2231-428">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-428">Success</span></span>  | <span data-ttu-id="d2231-429">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="d2231-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="d2231-430">10.10.100.1</span></span> | <span data-ttu-id="d2231-431">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-431">Heartbeat</span></span> |
| <span data-ttu-id="d2231-432">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-432">srv02.contoso.com</span></span> | <span data-ttu-id="d2231-433">4/20/2017 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="d2231-434">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-434">Success</span></span>  | <span data-ttu-id="d2231-435">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="d2231-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="d2231-436">10.10.100.2</span></span> | <span data-ttu-id="d2231-437">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-437">Heartbeat</span></span> |
| <span data-ttu-id="d2231-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-438">srv03.contoso.com</span></span> | <span data-ttu-id="d2231-439">4/20/2017 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="d2231-440">실패</span><span class="sxs-lookup"><span data-stu-id="d2231-440">Failure</span></span>  | <span data-ttu-id="d2231-441">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="d2231-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="d2231-443">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="d2231-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="d2231-444">10.10.100.2</span></span> | <span data-ttu-id="d2231-445">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="d2231-446">왼쪽 조인</span><span class="sxs-lookup"><span data-stu-id="d2231-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="d2231-447">Heartbeat에서 일치하는 필드가 있는 MyBackup_CL에서 다음 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-447">Returns the following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="d2231-448">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-448">Computer</span></span>| <span data-ttu-id="d2231-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-449">TimeGenerated</span></span> | <span data-ttu-id="d2231-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-450">LastBackupStatus</span></span> | <span data-ttu-id="d2231-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-451">TimeGenerated_joined</span></span> | <span data-ttu-id="d2231-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-452">ComputerIP_joined</span></span> | <span data-ttu-id="d2231-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="d2231-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="d2231-454">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-454">srv01.contoso.com</span></span> | <span data-ttu-id="d2231-455">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="d2231-456">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-456">Success</span></span> | <span data-ttu-id="d2231-457">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="d2231-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="d2231-458">10.10.100.1</span></span> | <span data-ttu-id="d2231-459">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-459">Heartbeat</span></span> |
| <span data-ttu-id="d2231-460">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-460">srv02.contoso.com</span></span> | <span data-ttu-id="d2231-461">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="d2231-462">성공</span><span class="sxs-lookup"><span data-stu-id="d2231-462">Success</span></span> | <span data-ttu-id="d2231-463">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="d2231-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="d2231-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="d2231-464">10.10.100.2</span></span> | <span data-ttu-id="d2231-465">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="d2231-465">Heartbeat</span></span> |
| <span data-ttu-id="d2231-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d2231-466">srv03.contoso.com</span></span> | <span data-ttu-id="d2231-467">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="d2231-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="d2231-468">실패</span><span class="sxs-lookup"><span data-stu-id="d2231-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="d2231-469">Extend</span><span class="sxs-lookup"><span data-stu-id="d2231-469">Extend</span></span>
<span data-ttu-id="d2231-470">쿼리에 런타임 필드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-470">Allows you to create run-time fields in queries.</span></span> <span data-ttu-id="d2231-471">런타임 필드는 집계를 수행하기 위한 측정값 명령과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-471">Note that run-time fields cannot be used with the measure command to perform aggregation.</span></span>

<span data-ttu-id="d2231-472">**예 1**</span><span class="sxs-lookup"><span data-stu-id="d2231-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="d2231-473">SQL 평가 권장 사항에 대해 가중 평균 권장 점수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="d2231-474">**예 2**</span><span class="sxs-lookup"><span data-stu-id="d2231-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="d2231-475">바이트가 아닌 KB 단위로 카운터 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="d2231-476">**예 3**</span><span class="sxs-lookup"><span data-stu-id="d2231-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="d2231-477">모든 결과가 0 ~ 100이 되도록 WireData TotalBytes 값을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-477">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="d2231-478">**예제 4**</span><span class="sxs-lookup"><span data-stu-id="d2231-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="d2231-479">50% 미만인 성능 카운터 값을 LOW로 태깅하고 나머지는 HIGH로 태깅합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="d2231-480">**예제 5**</span><span class="sxs-lookup"><span data-stu-id="d2231-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="d2231-481">컴퓨터의 모든 디스크에 대한 분당 최대 디스크 쓰기 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-481">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="d2231-482">**지원되는 함수**</span><span class="sxs-lookup"><span data-stu-id="d2231-482">**Supported functions**</span></span>

| <span data-ttu-id="d2231-483">함수</span><span class="sxs-lookup"><span data-stu-id="d2231-483">Function</span></span> | <span data-ttu-id="d2231-484">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-484">Description</span></span> | <span data-ttu-id="d2231-485">구문 예제</span><span class="sxs-lookup"><span data-stu-id="d2231-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d2231-486">abs</span><span class="sxs-lookup"><span data-stu-id="d2231-486">abs</span></span> |<span data-ttu-id="d2231-487">지정된 값 또는 함수의 절대 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-487">Returns the absolute value of the specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="d2231-488">acos</span><span class="sxs-lookup"><span data-stu-id="d2231-488">acos</span></span> |<span data-ttu-id="d2231-489">값 또는 함수의 아크코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="d2231-490">and</span><span class="sxs-lookup"><span data-stu-id="d2231-490">and</span></span> |<span data-ttu-id="d2231-491">모든 피연산자가 true로 계산될 경우에만 true 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-491">Returns a value of true if and only if all of its operands evaluate to true.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="d2231-492">asin</span><span class="sxs-lookup"><span data-stu-id="d2231-492">asin</span></span> |<span data-ttu-id="d2231-493">값 또는 함수의 아크사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="d2231-494">atan</span><span class="sxs-lookup"><span data-stu-id="d2231-494">atan</span></span> |<span data-ttu-id="d2231-495">값 또는 함수의 아크탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="d2231-496">atan2</span><span class="sxs-lookup"><span data-stu-id="d2231-496">atan2</span></span> |<span data-ttu-id="d2231-497">사각형 좌표 x,y를 극좌표로 변환한 결과의 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-497">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="d2231-498">cbrt</span><span class="sxs-lookup"><span data-stu-id="d2231-498">cbrt</span></span> |<span data-ttu-id="d2231-499">세제곱근입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="d2231-500">ceil</span><span class="sxs-lookup"><span data-stu-id="d2231-500">ceil</span></span> |<span data-ttu-id="d2231-501">정수로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-501">Rounds up to an integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="d2231-502">`ceil(5.6)` 6을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="d2231-503">cos</span><span class="sxs-lookup"><span data-stu-id="d2231-503">cos</span></span> |<span data-ttu-id="d2231-504">각도의 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="d2231-505">cosh</span><span class="sxs-lookup"><span data-stu-id="d2231-505">cosh</span></span> |<span data-ttu-id="d2231-506">쌍곡선 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="d2231-507">def</span><span class="sxs-lookup"><span data-stu-id="d2231-507">def</span></span> |<span data-ttu-id="d2231-508">기본값에 대한 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-508">Abbreviation for default.</span></span> <span data-ttu-id="d2231-509">필드 “field”의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-509">Returns the value of field "field".</span></span> <span data-ttu-id="d2231-510">필드가 없을 경우에는 지정된 기본 값을 반환하며 `exists()==true`일 때 첫 번째 값을 산출합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-510">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span></span> |<span data-ttu-id="d2231-511">`def(rating,5)`.</span><span class="sxs-lookup"><span data-stu-id="d2231-511">`def(rating,5)`.</span></span> <span data-ttu-id="d2231-512">이 def() 함수는 등급을 반환하거나 문서에 지정된 등급이 없는 경우 5를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-512">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span></span> <br> <span data-ttu-id="d2231-513">`def(myfield, 1.0)`은 `if(exists(myfield),myfield,1.0)`와 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-513">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="d2231-514">deg</span><span class="sxs-lookup"><span data-stu-id="d2231-514">deg</span></span> |<span data-ttu-id="d2231-515">라디안을 도로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-515">Converts radians to degrees.</span></span> |`deg(x)` |
| <span data-ttu-id="d2231-516">div</span><span class="sxs-lookup"><span data-stu-id="d2231-516">div</span></span> |<span data-ttu-id="d2231-517">`div(x,y)` 는 x를 y로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="d2231-518">dist</span><span class="sxs-lookup"><span data-stu-id="d2231-518">dist</span></span> |<span data-ttu-id="d2231-519">n차원 공간의 두 벡터(점) 사이의 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-519">Returns the distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="d2231-520">거듭제곱과 두 개 이상의 ValueSource 인스턴스를 가져와 두 벡터 간 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-520">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span></span> <span data-ttu-id="d2231-521">각 ValueSource는 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="d2231-522">전달하는 ValueSource 인스턴스 수는 짝수여야 하며 메서드는 처음 절반이 첫 번째 벡터를 나타내고 나머지 절반이 두 번째 벡터를 나타내는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-522">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span></span> |<span data-ttu-id="d2231-523">`dist(2, x, y, 0, 0)` 각 문서에 대해 (0,0)과 (x,y) 사이의 유클리드 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-523">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="d2231-524">`dist(1, x, y, 0, 0)` 각 문서에 대해 (0,0)과 (x,y) 사이의 맨해턴(taxicab) 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-524">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="d2231-525">`dist(2,,x,y,z,0,0,0)` 각 문서에 대해 (0,0,0)과 (x,y,z) 사이의 유클리드 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="d2231-526">`dist(1,x,y,z,e,f,g)` (x,y,z)와 (e,f,g) 사이의 맨해턴 거리이며 각 문자는 필드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="d2231-527">exists</span><span class="sxs-lookup"><span data-stu-id="d2231-527">exists</span></span> |<span data-ttu-id="d2231-528">필드에 구성원이 있을 경우 TRUE를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-528">Returns TRUE if any member of the field exists.</span></span> |<span data-ttu-id="d2231-529">`exists(author)` 문서의 "author" 필드에 값이 있을 경우 TRUE를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-529">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span></span><br><span data-ttu-id="d2231-530">`exists(query(price:5.00))` "price"가 "5.00"과 일치할 경우 TRUE를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="d2231-531">exp</span><span class="sxs-lookup"><span data-stu-id="d2231-531">exp</span></span> |<span data-ttu-id="d2231-532">x 제곱한 오일러의 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-532">Returns Euler's number raised to power x.</span></span> |`exp(x)` |
| <span data-ttu-id="d2231-533">floor</span><span class="sxs-lookup"><span data-stu-id="d2231-533">floor</span></span> |<span data-ttu-id="d2231-534">정수로 내립니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-534">Rounds down to an integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="d2231-535">`floor(5.6)` 5를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="d2231-536">hypo</span><span class="sxs-lookup"><span data-stu-id="d2231-536">hypo</span></span> |<span data-ttu-id="d2231-537">중간 오버플로 또는 언더플로 없이 sqrt(sum(pow(x,2),pow(y,2)))를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="d2231-538">if</span><span class="sxs-lookup"><span data-stu-id="d2231-538">if</span></span> |<span data-ttu-id="d2231-539">조건부 함수 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-539">Enables conditional function queries.</span></span> <span data-ttu-id="d2231-540">`if(test,value1,value2)`에서 test는 논리적 값 또는 논리적 값(TRUE 또는 FALSE)을 반환하는 식이거나 논리적 값 또는 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-540">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="d2231-541">`value1`은 테스트가 TRUE를 산출하면 함수에서 반환하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-541">`value1` is the value returned by the function if test yields TRUE.</span></span> <span data-ttu-id="d2231-542">`value2`은 테스트가 FALSE를 산출하면 함수에서 반환하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-542">`value2` is the value returned by the function if test yields FALSE.</span></span> <span data-ttu-id="d2231-543">식은 부울 값을 출력하는 함수일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="d2231-544">또한 숫자 값을 반환하는 함수일 수도 있으며, 이 경우 값 0은 FALSE 또는 반환 문자열로 해석되며, 후자의 경우 빈 문자열은 FALSE로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="d2231-545">`if(termfreq(cat,'electronics'),popularity,42)` 이 함수는 각 문서의 cat 필드에 "electronics"라는 단어가 포함되었는지 여부를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span></span> <span data-ttu-id="d2231-546">이 단어가 포함된 경우 인기도 필드의 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-546">If it does, then the value of the popularity field is returned.</span></span> <span data-ttu-id="d2231-547">그렇지 않으면 값 42가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-547">Otherwise, the value of 42 is returned.</span></span> |
| <span data-ttu-id="d2231-548">linear</span><span class="sxs-lookup"><span data-stu-id="d2231-548">linear</span></span> |<span data-ttu-id="d2231-549">`m*x+c`을 구현하며, 여기서 m과 c는 상수이고 x는 임의의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="d2231-550">이 함수는 `sum(product(m,x),c)`과 동일하지만 단일 함수로 구현되므로 약간 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-550">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="d2231-551">`linear(x,m,c) linear(x,2,4)` `2*x+4`를 반환합니다</span><span class="sxs-lookup"><span data-stu-id="d2231-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="d2231-552">ln</span><span class="sxs-lookup"><span data-stu-id="d2231-552">ln</span></span> |<span data-ttu-id="d2231-553">지정된 함수의 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-553">Returns the natural log of the specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="d2231-554">로그</span><span class="sxs-lookup"><span data-stu-id="d2231-554">log</span></span> |<span data-ttu-id="d2231-555">지정된 함수의 로그 밑 10을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-555">Returns the log base 10 of the specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="d2231-556">map</span><span class="sxs-lookup"><span data-stu-id="d2231-556">map</span></span> |<span data-ttu-id="d2231-557">min(포함) 및 max(포함)에 포함되는 입력 함수 x의 모든 값을 지정된 대상에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-557">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span></span> <span data-ttu-id="d2231-558">인수 min 및 max는 상수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-558">The arguments min and max must be constants.</span></span> <span data-ttu-id="d2231-559">인수 대상과 기본값은 상수 또는 함수가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-559">The arguments target and default can be constants or functions.</span></span> <span data-ttu-id="d2231-560">x 값이 min 및 max 사이에 포함되지 않는 경우 x 값이 반환되며 5번째 인수로 지정된 경우는 기본값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-560">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="d2231-561">`map(x,min,max,target) map(x,0,0,1)` 0 ~ 1의 모든 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span></span> <span data-ttu-id="d2231-562">이 함수는 기본값 0을 처리하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="d2231-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` 0 ~ 100 사이의 모든 값을 1로 바꾸고 나머지는 모두 -1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span></span><br>  <span data-ttu-id="d2231-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` 0 ~ 100 사이의 모든 값을 x+599로 바꾸고 나머지 모든 값을 필드 텍스트의 'solr' 용어의 빈도로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span></span> |
| <span data-ttu-id="d2231-565">max</span><span class="sxs-lookup"><span data-stu-id="d2231-565">max</span></span> |<span data-ttu-id="d2231-566">인수 `max(x,y,...)`로 지정되어 여러 번 중첩된 함수 또는 상수의 최대 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-566">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="d2231-567">max 함수는 지정된 상수에서 다른 함수 또는 필드를 "하한값으로 유지"하는 데에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-567">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="d2231-568">단일 다중값 필드의 최대값을 선택할 경우 `field(myfield,max)` 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-568">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="d2231-569">Min</span><span class="sxs-lookup"><span data-stu-id="d2231-569">min</span></span> |<span data-ttu-id="d2231-570">인수 `min(x,y,...)`으로 지정되어 여러 번 중첩된 함수 또는 상수의 최소 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-570">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="d2231-571">min 함수는 상수를 사용하는 함수에서 "상한"을 제공하는 데에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-571">The min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="d2231-572">단일 다중값 필드의 최소값을 선택할 경우 `field(myfield,min)` 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-572">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="d2231-573">mod</span><span class="sxs-lookup"><span data-stu-id="d2231-573">mod</span></span> |<span data-ttu-id="d2231-574">함수 x와 함수 y의 모듈러스를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-574">Computes the modulus of the function x by the function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="d2231-575">ms</span><span class="sxs-lookup"><span data-stu-id="d2231-575">ms</span></span> |<span data-ttu-id="d2231-576">인수간 차이를 밀리초 단위로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="d2231-577">날짜는 Unix 또는 POSIX time epoch인 1970년 1월 1일 자정(UTC) 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-577">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="d2231-578">인수는 상수 날짜 또는 NOW 기준의 인덱싱된 TrieDateField 또는 날짜 연산의 이름이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-578">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="d2231-579">`ms()`는 Epoch 이후의 시간(밀리초)인 `ms(NOW)`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-579">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span></span> <span data-ttu-id="d2231-580">`ms(a)` 는 인수가 나타내는 epoch 이후의 밀리초를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-580">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span></span> <span data-ttu-id="d2231-581">`ms(a,b)`는 a 이전에 b가 발생한 시간(밀리초), 즉, `a - b`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-581">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="d2231-582">not</span><span class="sxs-lookup"><span data-stu-id="d2231-582">not</span></span> |<span data-ttu-id="d2231-583">래핑된 함수의 논리적 부정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-583">The logically negated value of the wrapped function.</span></span> |<span data-ttu-id="d2231-584">`not(exists(author))` `exists(author)`가 false일 경우에만 TRUE입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="d2231-585">또는</span><span class="sxs-lookup"><span data-stu-id="d2231-585">or</span></span> |<span data-ttu-id="d2231-586">논리적 분리.</span><span class="sxs-lookup"><span data-stu-id="d2231-586">A logical disjunction.</span></span> |<span data-ttu-id="d2231-587">`or(value1,value2)` value1 또는 value2가 true일 경우에만 TRUE입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="d2231-588">pow</span><span class="sxs-lookup"><span data-stu-id="d2231-588">pow</span></span> |<span data-ttu-id="d2231-589">지정된 밑에 지정된 값으로 거듭제곱합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-589">Raises the specified base to the specified power.</span></span> <span data-ttu-id="d2231-590">`pow(x,y)` 는 x를 y 거듭제곱합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-590">`pow(x,y)` raises x to the power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="d2231-591">`pow(x,0.5)` sqrt와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-591">`pow(x,0.5)` The same as sqrt.</span></span> |
| <span data-ttu-id="d2231-592">product</span><span class="sxs-lookup"><span data-stu-id="d2231-592">product</span></span> |<span data-ttu-id="d2231-593">쉼표로 구분된 목록으로 지정하는 여러 값 또는 함수의 곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-593">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="d2231-594">`mul(...)` 도 이 함수의 별칭으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="d2231-595">recip</span><span class="sxs-lookup"><span data-stu-id="d2231-595">recip</span></span> |<span data-ttu-id="d2231-596">`recip(x,m,a,b)`를 구현하는 `a/(m*x+b)`를 사용하는 역함수를 수행합니다. 여기서 m, a 및 b는 상수이며 x는 임의의 복소수 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="d2231-597">a와 b가 동일하고 x>=0일 경우 이 함수의 최대값 1은 x가 증가함에 따라 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="d2231-598">a와 b 값을 함께 증가할 경우 전체 함수가 곡선의 평평한 부분으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-598">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span></span> <span data-ttu-id="d2231-599">이러한 속성으로 인해 x가 `rord(datefield)`일 때 더 많은 최근 문서를 출력하는 데 적합한 함수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="d2231-600">rad</span><span class="sxs-lookup"><span data-stu-id="d2231-600">rad</span></span> |<span data-ttu-id="d2231-601">도를 라디안으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-601">Converts degrees to radians.</span></span> |`rad(x)` |
| <span data-ttu-id="d2231-602">rint</span><span class="sxs-lookup"><span data-stu-id="d2231-602">rint</span></span> |<span data-ttu-id="d2231-603">가장 가까운 정수로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-603">Rounds to the nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="d2231-604">`rint(5.6)` 6을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="d2231-605">sin</span><span class="sxs-lookup"><span data-stu-id="d2231-605">sin</span></span> |<span data-ttu-id="d2231-606">각도의 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="d2231-607">sinh</span><span class="sxs-lookup"><span data-stu-id="d2231-607">sinh</span></span> |<span data-ttu-id="d2231-608">각도의 쌍곡선 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="d2231-609">크기 조정</span><span class="sxs-lookup"><span data-stu-id="d2231-609">scale</span></span> |<span data-ttu-id="d2231-610">함수 x의 값을 지정된 minTarget(포함) 및 maxTarget(포함) 안에 포함되도록 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-610">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="d2231-611">현재 구현은 올바른 배율을 선택할 수 있도록 모든 함수 값을 확인하여 min 및 max를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-611">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span></span> <span data-ttu-id="d2231-612">현재 구현은 문서가 삭제된 시기 또는 값이 없는 문서를 구분할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-612">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="d2231-613">그러한 경우는 0.0 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="d2231-614">즉, 일반적으로 모든 값이 0.0보다 클 경우 매핑을 시작하는 최소값이 0.0이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span></span> <span data-ttu-id="d2231-615">그럴 경우에는 해결 방법으로 적절한 `map()` 함수를 사용하여 0.0을 `scale(map(x,0,0,5),1,2)`과 같은 실제 범위 내의 값으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-615">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="d2231-616">`scale(x,1,2)` 모든 값이 1(포함) ~ 2(포함) 사이가 되도록 x 값을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-616">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="d2231-617">sqrt</span><span class="sxs-lookup"><span data-stu-id="d2231-617">sqrt</span></span> |<span data-ttu-id="d2231-618">지정된 값 도는 함수의 제곱근을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-618">Returns the square root of the specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="d2231-619">strdist</span><span class="sxs-lookup"><span data-stu-id="d2231-619">strdist</span></span> |<span data-ttu-id="d2231-620">두 문자열 간의 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-620">Calculates the distance between two strings.</span></span> <span data-ttu-id="d2231-621">Lucene 맞춤법 검사기 StringDistance 인터페이스를 사용하며 해당 패키지에서 사용할 수 있는 모든 구현을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-621">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span></span> <span data-ttu-id="d2231-622">Solr의 리소스 로드 기능을 통해 응용 프로그램을 자체 내에 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-622">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="d2231-623">strdist는 `(string1, string2, distance measure)`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="d2231-624">거리 측정에 가능한 값은 </span><span class="sxs-lookup"><span data-stu-id="d2231-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="d2231-625">jw: Jaro-Winkler</span><span class="sxs-lookup"><span data-stu-id="d2231-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="d2231-626">edit: Levenstein 또는 편집 거리</span><span class="sxs-lookup"><span data-stu-id="d2231-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="d2231-627">ngram입니다(NGramDistance를 지정할 경우 ngram 크기도 선택적으로 전달할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="d2231-627">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span></span> <span data-ttu-id="d2231-628">기본값은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-628">Default is 2.</span></span></li><li><span data-ttu-id="d2231-629">FQN: StringDistance 인터페이스 구현의 정규화된 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-629">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span></span> <span data-ttu-id="d2231-630">인수가 없는 생성자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="d2231-631">sub</span><span class="sxs-lookup"><span data-stu-id="d2231-631">sub</span></span> |<span data-ttu-id="d2231-632">`sub(x,y)`에서 x-y를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="d2231-633">합계</span><span class="sxs-lookup"><span data-stu-id="d2231-633">sum</span></span> |<span data-ttu-id="d2231-634">쉼표로 구분된 목록으로 지정하는 여러 값 또는 함수의 합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-634">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="d2231-635">`add(...)` 도 이 함수의 별칭으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="d2231-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="d2231-636">termfreq</span></span> |<span data-ttu-id="d2231-637">해당 문서에 대해 필드에 용어가 나타나는 횟수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-637">Returns the number of times the term appears in the field for that document.</span></span> |<span data-ttu-id="d2231-638">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="d2231-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="d2231-639">tan</span><span class="sxs-lookup"><span data-stu-id="d2231-639">tan</span></span> |<span data-ttu-id="d2231-640">각도의 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="d2231-641">tanh</span><span class="sxs-lookup"><span data-stu-id="d2231-641">tanh</span></span> |<span data-ttu-id="d2231-642">각도의 쌍곡선 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="d2231-643">검색 필드 및 패싯 참조</span><span class="sxs-lookup"><span data-stu-id="d2231-643">Search field and facet reference</span></span>
<span data-ttu-id="d2231-644">로그 검색을 사용하여 데이터를 찾을 때 결과에 다양한 필드와 패싯이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-644">When you use Log Search to find data, results display various field and facets.</span></span> <span data-ttu-id="d2231-645">일부 정보는 매우 설명적인 것으로 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-645">Some of the information might not appear very descriptive.</span></span> <span data-ttu-id="d2231-646">다음 정보를 사용하여 결과를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-646">Use the following information to help you understand the results.</span></span>

| <span data-ttu-id="d2231-647">필드</span><span class="sxs-lookup"><span data-stu-id="d2231-647">Field</span></span> | <span data-ttu-id="d2231-648">검색 유형</span><span class="sxs-lookup"><span data-stu-id="d2231-648">Search type</span></span> | <span data-ttu-id="d2231-649">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d2231-650">TenantId</span><span class="sxs-lookup"><span data-stu-id="d2231-650">TenantId</span></span> |<span data-ttu-id="d2231-651">모두</span><span class="sxs-lookup"><span data-stu-id="d2231-651">All</span></span> |<span data-ttu-id="d2231-652">데이터를 분할하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-652">Used to partition data.</span></span> |
| <span data-ttu-id="d2231-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2231-653">TimeGenerated</span></span> |<span data-ttu-id="d2231-654">모두</span><span class="sxs-lookup"><span data-stu-id="d2231-654">All</span></span> |<span data-ttu-id="d2231-655">타임라인을 구동하는 데 사용되는 timeselectors입니다.(검색 및 다른 화면에서)</span><span class="sxs-lookup"><span data-stu-id="d2231-655">Used to drive the timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="d2231-656">데이터의 일부가 생성된 때를 나타냅니다.(일반적으로 에이전트에서)</span><span class="sxs-lookup"><span data-stu-id="d2231-656">It represents when the piece of data was generated (typically on the agent).</span></span> <span data-ttu-id="d2231-657">ISO 형식으로 표현되는 시간이며 항상 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-657">The time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="d2231-658">기존 계측(즉, 로그의 이벤트)을 기반으로 하는 유형의 경우, 이는 일반적으로 로그 항목/줄/레코드가 로그된 실제 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-658">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span></span> <span data-ttu-id="d2231-659">관리 팩을 통해 또는 클라우드에서 생성되는 일부 다른 유형의 경우(예를 들어 권고 또는 경고) 시간은 다른 무언가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-659">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span></span> <span data-ttu-id="d2231-660">이는 일부 종류의 구성에 대한 스냅숏을 가진 데이터의 새로운 부분이 수집되거나 권고/경고가 해당 부분을 기반으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-660">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="d2231-661">EventID</span><span class="sxs-lookup"><span data-stu-id="d2231-661">EventID</span></span> |<span data-ttu-id="d2231-662">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-662">Event</span></span> |<span data-ttu-id="d2231-663">Windows 이벤트 로그의 EventID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-663">EventID in the Windows event log.</span></span> |
| <span data-ttu-id="d2231-664">EventLog</span><span class="sxs-lookup"><span data-stu-id="d2231-664">EventLog</span></span> |<span data-ttu-id="d2231-665">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-665">Event</span></span> |<span data-ttu-id="d2231-666">Windows에서 이벤트를 로그한 이벤트 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-666">Event log where the event was logged by Windows.</span></span> |
| <span data-ttu-id="d2231-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="d2231-667">EventLevelName</span></span> |<span data-ttu-id="d2231-668">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-668">Event</span></span> |<span data-ttu-id="d2231-669">중요/경고/정보/성공</span><span class="sxs-lookup"><span data-stu-id="d2231-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="d2231-670">EventLevel</span><span class="sxs-lookup"><span data-stu-id="d2231-670">EventLevel</span></span> |<span data-ttu-id="d2231-671">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-671">Event</span></span> |<span data-ttu-id="d2231-672">중요/경고/정보/성공에 대한 숫자 값입니다(보다 쉽게/보다 읽기 쉬운 쿼리 대신 EventLevelName 사용).</span><span class="sxs-lookup"><span data-stu-id="d2231-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="d2231-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d2231-673">SourceSystem</span></span> |<span data-ttu-id="d2231-674">모두</span><span class="sxs-lookup"><span data-stu-id="d2231-674">All</span></span> |<span data-ttu-id="d2231-675">데이터가 나온 출처입니다(서비스에 대한 연결 모드 면에서).</span><span class="sxs-lookup"><span data-stu-id="d2231-675">Where the data comes from (in terms of attach mode to the service).</span></span> <span data-ttu-id="d2231-676">예를 들어 Microsoft System Center Operations Manager 및 Azure Storage를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="d2231-677">ObjectName</span><span class="sxs-lookup"><span data-stu-id="d2231-677">ObjectName</span></span> |<span data-ttu-id="d2231-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-678">PerfHourly</span></span> |<span data-ttu-id="d2231-679">Windows 성능 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-679">Windows performance object name.</span></span> |
| <span data-ttu-id="d2231-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="d2231-680">InstanceName</span></span> |<span data-ttu-id="d2231-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-681">PerfHourly</span></span> |<span data-ttu-id="d2231-682">Windows 성능 카운터 인스턴스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="d2231-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="d2231-683">CounteName</span></span> |<span data-ttu-id="d2231-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-684">PerfHourly</span></span> |<span data-ttu-id="d2231-685">Windows 성능 카운터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="d2231-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="d2231-686">ObjectDisplayName</span></span> |<span data-ttu-id="d2231-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="d2231-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="d2231-688">Operations Manager의 성능 수집 규칙에 대상이 되는 개체의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-688">Display name of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="d2231-689">Operational Insights에서 검색되었거나 경고가 생성되는 기준이었던 개체의 표시 이름일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-689">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="d2231-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="d2231-690">RootObjectName</span></span> |<span data-ttu-id="d2231-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="d2231-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="d2231-692">Operations Manager의 성능 수집 규칙에 대상이 되는 개체에 대한 상위 요소(이중 호스팅 관계)의 상위 요소의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-692">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="d2231-693">Operational Insights에서 검색되었거나 경고가 생성되는 기준이었던 개체의 표시 이름일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-693">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="d2231-694">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d2231-694">Computer</span></span> |<span data-ttu-id="d2231-695">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="d2231-695">Most types</span></span> |<span data-ttu-id="d2231-696">데이터가 속한 컴퓨터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-696">Computer name that the data belongs to.</span></span> |
| <span data-ttu-id="d2231-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="d2231-697">DeviceName</span></span> |<span data-ttu-id="d2231-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-698">ProtectionStatus</span></span> |<span data-ttu-id="d2231-699">데이터가 속한 컴퓨터 이름입니다('Computer'와 동일).</span><span class="sxs-lookup"><span data-stu-id="d2231-699">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="d2231-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="d2231-700">DetectionId</span></span> |<span data-ttu-id="d2231-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="d2231-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="d2231-702">ThreatStatusRank</span></span> |<span data-ttu-id="d2231-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-703">ProtectionStatus</span></span> |<span data-ttu-id="d2231-704">위협 상태 순위는 위협 상태의 숫자 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-704">Threat status rank is a numerical representation of the threat status.</span></span> <span data-ttu-id="d2231-705">HTTP 응답 코드와 유사한 순위는 숫자 간에 간격을 두어(이는 150인 위협이 없고 위협이 100 또는 0이 아닌 이유임) 새 상태를 추가할 공간을 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-705">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span></span> <span data-ttu-id="d2231-706">위협 상태 및 보호 상태를 롤업하는 경우 그 의도는 선택된 기간 동안 컴퓨터에 있었던 최악의 상태를 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-706">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span></span> <span data-ttu-id="d2231-707">숫자를 통해 다양한 상태 순위를 지정하므로 가장 높은 번호의 레코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-707">The numbers rank the different states, so you can look for the record with the highest number.</span></span> |
| <span data-ttu-id="d2231-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-708">ThreatStatus</span></span> |<span data-ttu-id="d2231-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-709">ProtectionStatus</span></span> |<span data-ttu-id="d2231-710">ThreatStatus에 대한 설명이며, ThreatStatusRank와 1:1 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="d2231-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="d2231-711">TypeofProtection</span></span> |<span data-ttu-id="d2231-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-712">ProtectionStatus</span></span> |<span data-ttu-id="d2231-713">컴퓨터에서 검색된 맬웨어 방지 제품은 없음, Microsoft 맬웨어 제거 도구, Forefront 등입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-713">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="d2231-714">ScanDate</span><span class="sxs-lookup"><span data-stu-id="d2231-714">ScanDate</span></span> |<span data-ttu-id="d2231-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="d2231-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="d2231-716">SourceHealthServiceId</span></span> |<span data-ttu-id="d2231-717">ProtectionStatus, RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="d2231-718">이 컴퓨터의 에이전트에 대한 HealthService ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="d2231-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="d2231-719">HealthServiceId</span></span> |<span data-ttu-id="d2231-720">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="d2231-720">Most types</span></span> |<span data-ttu-id="d2231-721">이 컴퓨터의 에이전트에 대한 HealthService ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="d2231-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="d2231-722">ManagementGroupName</span></span> |<span data-ttu-id="d2231-723">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="d2231-723">Most types</span></span> |<span data-ttu-id="d2231-724">Operations Manager에 연결된 에이전트용 관리 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="d2231-725">그렇지 않은 경우 null/blank입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="d2231-726">ObjectType</span><span class="sxs-lookup"><span data-stu-id="d2231-726">ObjectType</span></span> |<span data-ttu-id="d2231-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="d2231-727">ConfigurationObject</span></span> |<span data-ttu-id="d2231-728">Log Analytics 구성 평가에서 검색된 개체의 형식(Operations Manager 관리 팩의 형식/클래스와 동일)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="d2231-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="d2231-729">UpdateTitle</span></span> |<span data-ttu-id="d2231-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-730">RequiredUpdate</span></span> |<span data-ttu-id="d2231-731">설치되지 않고 발견된 업데이트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-731">Name of the update that was found not installed.</span></span> |
| <span data-ttu-id="d2231-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="d2231-732">PublishDate</span></span> |<span data-ttu-id="d2231-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-733">RequiredUpdate</span></span> |<span data-ttu-id="d2231-734">업데이트가 Microsoft Update에 게시된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-734">When the update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="d2231-735">서버</span><span class="sxs-lookup"><span data-stu-id="d2231-735">Server</span></span> |<span data-ttu-id="d2231-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-736">RequiredUpdate</span></span> |<span data-ttu-id="d2231-737">데이터가 속한 컴퓨터 이름입니다('Computer'와 동일).</span><span class="sxs-lookup"><span data-stu-id="d2231-737">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="d2231-738">제품</span><span class="sxs-lookup"><span data-stu-id="d2231-738">Product</span></span> |<span data-ttu-id="d2231-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-739">RequiredUpdate</span></span> |<span data-ttu-id="d2231-740">업데이트가 적용되는 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-740">Product that the update applies to.</span></span> |
| <span data-ttu-id="d2231-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="d2231-741">UpdateClassification</span></span> |<span data-ttu-id="d2231-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-742">RequiredUpdate</span></span> |<span data-ttu-id="d2231-743">업데이트 유형(예를 들어 업데이트 롤업 또는 서비스 팩)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="d2231-744">KBID</span><span class="sxs-lookup"><span data-stu-id="d2231-744">KBID</span></span> |<span data-ttu-id="d2231-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-745">RequiredUpdate</span></span> |<span data-ttu-id="d2231-746">모범 사례 또는 업데이트를 설명하는 KB 문서 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="d2231-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="d2231-747">WorkflowName</span></span> |<span data-ttu-id="d2231-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-748">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-749">경고를 생성하는 모니터 또는 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-749">Name of the rule or monitor that produced the alert.</span></span> |
| <span data-ttu-id="d2231-750">심각도</span><span class="sxs-lookup"><span data-stu-id="d2231-750">Severity</span></span> |<span data-ttu-id="d2231-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-751">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-752">경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-752">Severity of the alert.</span></span> |
| <span data-ttu-id="d2231-753">우선 순위</span><span class="sxs-lookup"><span data-stu-id="d2231-753">Priority</span></span> |<span data-ttu-id="d2231-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-754">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-755">경고의 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-755">Priority of the alert.</span></span> |
| <span data-ttu-id="d2231-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-756">IsMonitorAlert</span></span> |<span data-ttu-id="d2231-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-757">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-758">이 경고는 모니터(true) 또는 규칙(false)에 의해 생성되었습니까?</span><span class="sxs-lookup"><span data-stu-id="d2231-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="d2231-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="d2231-759">AlertParameters</span></span> |<span data-ttu-id="d2231-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-760">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-761">Log Analytics 경고의 매개 변수가 포함된 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-761">XML with the parameters of the Log Analytics alert.</span></span> |
| <span data-ttu-id="d2231-762">Context</span><span class="sxs-lookup"><span data-stu-id="d2231-762">Context</span></span> |<span data-ttu-id="d2231-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-763">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-764">Log Analytics 경고의 컨텍스트가 포함된 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-764">XML with the context of the Log Analytics alert.</span></span> |
| <span data-ttu-id="d2231-765">워크로드</span><span class="sxs-lookup"><span data-stu-id="d2231-765">Workload</span></span> |<span data-ttu-id="d2231-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-766">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-767">경고가 참조하는 기술 또는 워크로드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-767">Technology or workload that the alert refers to.</span></span> |
| <span data-ttu-id="d2231-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="d2231-768">AdvisorWorkload</span></span> |<span data-ttu-id="d2231-769">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d2231-769">Recommendation</span></span> |<span data-ttu-id="d2231-770">권장 사항이 참조하는 기술 또는 워크로드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-770">Technology or workload that the recommendation refers to.</span></span> |
| <span data-ttu-id="d2231-771">설명</span><span class="sxs-lookup"><span data-stu-id="d2231-771">Description</span></span> |<span data-ttu-id="d2231-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="d2231-772">ConfigurationAlert</span></span> |<span data-ttu-id="d2231-773">경고 설명(간략)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-773">Alert description (short).</span></span> |
| <span data-ttu-id="d2231-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="d2231-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="d2231-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-775">UpdateAgent</span></span> |<span data-ttu-id="d2231-776">WSUS(Windows Server Update Service) 또는 Microsoft Update에서 이 에이전트가 업데이트를 설치한 날은 얼마 전입니까(이 레코드의 TimeGenerated와 관련)?</span><span class="sxs-lookup"><span data-stu-id="d2231-776">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="d2231-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="d2231-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="d2231-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-778">UpdateAgent</span></span> |<span data-ttu-id="d2231-779">DaysSinceLastUpdate에 따라 컴퓨터가 WSUS/Microsoft Update에서 업데이트를 마지막 설치한 것이 얼마 전인지에 대한 시간 버킷의 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="d2231-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="d2231-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="d2231-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-781">UpdateAgent</span></span> |<span data-ttu-id="d2231-782">자동 업데이트가 이 에이전트에서 활성화 또는 비활성화를 확인하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d2231-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="d2231-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="d2231-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="d2231-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-784">UpdateAgent</span></span> |<span data-ttu-id="d2231-785">자동 업데이트가 자동으로 다운로드 및 설치, 다운로드만 또는 확인만 하도록 설정을 확인하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d2231-785">Is automatic update checking set to automatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="d2231-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="d2231-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="d2231-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-787">UpdateAgent</span></span> |<span data-ttu-id="d2231-788">Microsoft 업데이트 에이전트의 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-788">Version number of the Microsoft Update agent.</span></span> |
| <span data-ttu-id="d2231-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="d2231-789">WSUSServer</span></span> |<span data-ttu-id="d2231-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-790">UpdateAgent</span></span> |<span data-ttu-id="d2231-791">어떤 WSUS 서버가 이 업데이트 에이전트를 대상으로 합니까?</span><span class="sxs-lookup"><span data-stu-id="d2231-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="d2231-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="d2231-792">OSVersion</span></span> |<span data-ttu-id="d2231-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-793">UpdateAgent</span></span> |<span data-ttu-id="d2231-794">이 업데이트 에이전트에서 실행 중인 운영 체제의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-794">Version of the operating system this update agent is running on.</span></span> |
| <span data-ttu-id="d2231-795">이름</span><span class="sxs-lookup"><span data-stu-id="d2231-795">Name</span></span> |<span data-ttu-id="d2231-796">Recommendation, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="d2231-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="d2231-797">권장 사항의 이름/제목, 또는 Log Analytics 구성 평가에서 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-797">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="d2231-798">값</span><span class="sxs-lookup"><span data-stu-id="d2231-798">Value</span></span> |<span data-ttu-id="d2231-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="d2231-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="d2231-800">Log Analytics 구성 평가에서 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="d2231-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="d2231-801">KBLink</span></span> |<span data-ttu-id="d2231-802">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d2231-802">Recommendation</span></span> |<span data-ttu-id="d2231-803">모범 사례 또는 업데이트를 설명하는 KB 문서의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-803">URL to the KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="d2231-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-804">RecommendationStatus</span></span> |<span data-ttu-id="d2231-805">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d2231-805">Recommendation</span></span> |<span data-ttu-id="d2231-806">권장 사항은 레코드가 업데이트되는 몇 가지 형식 중 하나이며 단순히 검색 인덱스에 추가되는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-806">Recommendations are among the few types whose records get updated, not just added to the search index.</span></span> <span data-ttu-id="d2231-807">이 상태는 권장 사항이 활성/미결 상태인지 또는 Log Analytics에서 해결되었음을 감지했는지 여부에 따라 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-807">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="d2231-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="d2231-808">RenderedDescription</span></span> |<span data-ttu-id="d2231-809">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-809">Event</span></span> |<span data-ttu-id="d2231-810">Windows 이벤트의 렌더링된 설명(채워진 매개 변수와 재사용된 텍스트)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="d2231-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="d2231-811">ParameterXml</span></span> |<span data-ttu-id="d2231-812">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-812">Event</span></span> |<span data-ttu-id="d2231-813">Windows 이벤트(이벤트 뷰어처럼)의 데이터 섹션에 매개 변수를 사용하는 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-813">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="d2231-814">EventData</span><span class="sxs-lookup"><span data-stu-id="d2231-814">EventData</span></span> |<span data-ttu-id="d2231-815">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-815">Event</span></span> |<span data-ttu-id="d2231-816">Windows 이벤트의 전체 데이터 섹션을 사용하는 XML입니다(이벤트 뷰어처럼).</span><span class="sxs-lookup"><span data-stu-id="d2231-816">XML with the whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="d2231-817">원본</span><span class="sxs-lookup"><span data-stu-id="d2231-817">Source</span></span> |<span data-ttu-id="d2231-818">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-818">Event</span></span> |<span data-ttu-id="d2231-819">이벤트를 생성하는 이벤트 로그 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-819">Event log source that generated the event.</span></span> |
| <span data-ttu-id="d2231-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="d2231-820">EventCategory</span></span> |<span data-ttu-id="d2231-821">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-821">Event</span></span> |<span data-ttu-id="d2231-822">Windows 이벤트 로그에서 직접 가져온 이벤트의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-822">Category of the event, directly from the Windows event log.</span></span> |
| <span data-ttu-id="d2231-823">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="d2231-823">UserName</span></span> |<span data-ttu-id="d2231-824">이벤트</span><span class="sxs-lookup"><span data-stu-id="d2231-824">Event</span></span> |<span data-ttu-id="d2231-825">Windows 이벤트의 사용자 이름(일반적으로 NT AUTHORITY\LOCALSYSTEM)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-825">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="d2231-826">SampleValue</span><span class="sxs-lookup"><span data-stu-id="d2231-826">SampleValue</span></span> |<span data-ttu-id="d2231-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-827">PerfHourly</span></span> |<span data-ttu-id="d2231-828">성능 카운터의 시간별 집계에 대한 평균 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-828">Average value for the hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="d2231-829">Min</span><span class="sxs-lookup"><span data-stu-id="d2231-829">Min</span></span> |<span data-ttu-id="d2231-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-830">PerfHourly</span></span> |<span data-ttu-id="d2231-831">성능 카운터 매시간 집계의 시간 간격의 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-831">Minimum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="d2231-832">max</span><span class="sxs-lookup"><span data-stu-id="d2231-832">Max</span></span> |<span data-ttu-id="d2231-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-833">PerfHourly</span></span> |<span data-ttu-id="d2231-834">성능 카운터 매시간 집계의 시간 간격의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-834">Maximum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="d2231-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="d2231-835">Percentile95</span></span> |<span data-ttu-id="d2231-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-836">PerfHourly</span></span> |<span data-ttu-id="d2231-837">성능 카운터 매시간 집계의 시간 간격의 95번째 백분위 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-837">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="d2231-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="d2231-838">SampleCount</span></span> |<span data-ttu-id="d2231-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="d2231-839">PerfHourly</span></span> |<span data-ttu-id="d2231-840">매시간 집계 레코드를 생성하는 데 사용된 원시 성능 카운터 샘플의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-840">How many raw performance counter samples were used to produce this hourly aggregate record.</span></span> |
| <span data-ttu-id="d2231-841">위협</span><span class="sxs-lookup"><span data-stu-id="d2231-841">Threat</span></span> |<span data-ttu-id="d2231-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-842">ProtectionStatus</span></span> |<span data-ttu-id="d2231-843">발견한 맬웨어의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-843">Name of malware found.</span></span> |
| <span data-ttu-id="d2231-844">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="d2231-844">StorageAccount</span></span> |<span data-ttu-id="d2231-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-845">W3CIISLog</span></span> |<span data-ttu-id="d2231-846">로그를 읽은 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-846">Azure Storage account the log was read from.</span></span> |
| <span data-ttu-id="d2231-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="d2231-847">AzureDeploymentID</span></span> |<span data-ttu-id="d2231-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-848">W3CIISLog</span></span> |<span data-ttu-id="d2231-849">로그가 속한 클라우드 서비스의 Azure 배포 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-849">Azure deployment ID of the cloud service the log belongs to.</span></span> |
| <span data-ttu-id="d2231-850">역할</span><span class="sxs-lookup"><span data-stu-id="d2231-850">Role</span></span> |<span data-ttu-id="d2231-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-851">W3CIISLog</span></span> |<span data-ttu-id="d2231-852">로그가 속한 Azure 클라우드 서비스의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-852">Role of the Azure cloud service the log belongs to.</span></span> |
| <span data-ttu-id="d2231-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="d2231-853">RoleInstance</span></span> |<span data-ttu-id="d2231-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-854">W3CIISLog</span></span> |<span data-ttu-id="d2231-855">로그가 속한 Azure 역할의 RoleInstance입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-855">RoleInstance of the Azure role that the log belongs to.</span></span> |
| <span data-ttu-id="d2231-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="d2231-856">sSiteName</span></span> |<span data-ttu-id="d2231-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-857">W3CIISLog</span></span> |<span data-ttu-id="d2231-858">로그가 속한 IIS 웹 사이트(메타베이스 표기법); 원래 로그에서 s-sitename 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-858">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span></span> |
| <span data-ttu-id="d2231-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="d2231-859">sComputerName</span></span> |<span data-ttu-id="d2231-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-860">W3CIISLog</span></span> |<span data-ttu-id="d2231-861">원래 로그에서 s-computername 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-861">The s-computername field in the original log.</span></span> |
| <span data-ttu-id="d2231-862">sIP</span><span class="sxs-lookup"><span data-stu-id="d2231-862">sIP</span></span> |<span data-ttu-id="d2231-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-863">W3CIISLog</span></span> |<span data-ttu-id="d2231-864">HTTP 요청이 지정된 서버 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-864">Server IP address the HTTP request was addressed to.</span></span> <span data-ttu-id="d2231-865">원래 로그에서 s-ip 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-865">The s-ip field in the original log.</span></span> |
| <span data-ttu-id="d2231-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="d2231-866">csMethod</span></span> |<span data-ttu-id="d2231-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-867">W3CIISLog</span></span> |<span data-ttu-id="d2231-868">HTTP 요청에서 클라이언트가 사용한 HTTP 메서드(예: GET/POST)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-868">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span></span> <span data-ttu-id="d2231-869">원래 로그에서 cs-method입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-869">The cs-method in the original log.</span></span> |
| <span data-ttu-id="d2231-870">cIP</span><span class="sxs-lookup"><span data-stu-id="d2231-870">cIP</span></span> |<span data-ttu-id="d2231-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-871">W3CIISLog</span></span> |<span data-ttu-id="d2231-872">HTTP 요청이 발생한 클라이언트 IP 주소</span><span class="sxs-lookup"><span data-stu-id="d2231-872">Client IP address the HTTP request came from.</span></span> <span data-ttu-id="d2231-873">원래 로그에서 c-ip 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-873">The c-ip field in the original log.</span></span> |
| <span data-ttu-id="d2231-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="d2231-874">csUserAgent</span></span> |<span data-ttu-id="d2231-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-875">W3CIISLog</span></span> |<span data-ttu-id="d2231-876">클라이언트가 선언한 HTTP 사용자 에이전트(브라우저 또는 그렇지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="d2231-876">HTTP User-Agent declared by the client (browser or otherwise).</span></span> <span data-ttu-id="d2231-877">원래 로그에서 cs-user-agent입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-877">The cs-user-agent in the original log.</span></span> |
| <span data-ttu-id="d2231-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-878">scStatus</span></span> |<span data-ttu-id="d2231-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-879">W3CIISLog</span></span> |<span data-ttu-id="d2231-880">서버에서 클라이언트에 반환한 HTTP 상태 코드(예: 200/403/500)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-880">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span></span> <span data-ttu-id="d2231-881">원래 로그에서 cs-status입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-881">The cs-status in the original log.</span></span> |
| <span data-ttu-id="d2231-882">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="d2231-882">TimeTaken</span></span> |<span data-ttu-id="d2231-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-883">W3CIISLog</span></span> |<span data-ttu-id="d2231-884">요청이 완료되는데 얼마나 걸립니까(밀리초).</span><span class="sxs-lookup"><span data-stu-id="d2231-884">How long (in milliseconds) that the request took to complete.</span></span> <span data-ttu-id="d2231-885">원래 로그에서 timetaken 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-885">The timetaken field in the original log.</span></span> |
| <span data-ttu-id="d2231-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="d2231-886">csUriStem</span></span> |<span data-ttu-id="d2231-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-887">W3CIISLog</span></span> |<span data-ttu-id="d2231-888">요청된 상대 URI( 호스트 주소 즉, /search 없이)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="d2231-889">원래 로그에서 cs-uristem 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-889">The cs-uristem field in the original log.</span></span> |
| <span data-ttu-id="d2231-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="d2231-890">csUriQuery</span></span> |<span data-ttu-id="d2231-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-891">W3CIISLog</span></span> |<span data-ttu-id="d2231-892">URI 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-892">URI query.</span></span> <span data-ttu-id="d2231-893">URI 쿼리는 ASP 페이지와 같은 동적 페이지에만 필요하므로 이 필드는 일반적으로 정적 페이지에 대한 하이픈을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="d2231-894">sPort</span><span class="sxs-lookup"><span data-stu-id="d2231-894">sPort</span></span> |<span data-ttu-id="d2231-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-895">W3CIISLog</span></span> |<span data-ttu-id="d2231-896">HTTP 요청이 전송된 서버 포트(선택되었기 때문에 IIS에서 수신함)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-896">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="d2231-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="d2231-897">csUserName</span></span> |<span data-ttu-id="d2231-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-898">W3CIISLog</span></span> |<span data-ttu-id="d2231-899">인증된 사용자 이름(요청이 인증되고 익명이 아닌 경우)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-899">Authenticated user name, if the request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="d2231-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="d2231-900">csVersion</span></span> |<span data-ttu-id="d2231-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-901">W3CIISLog</span></span> |<span data-ttu-id="d2231-902">요청에 사용되는 HTTP 프로토콜 버전(즉, HTTP/1.1)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-902">HTTP Protocol version used in the request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="d2231-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="d2231-903">csCookie</span></span> |<span data-ttu-id="d2231-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-904">W3CIISLog</span></span> |<span data-ttu-id="d2231-905">쿠키 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-905">Cookie information.</span></span> |
| <span data-ttu-id="d2231-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="d2231-906">csReferer</span></span> |<span data-ttu-id="d2231-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-907">W3CIISLog</span></span> |<span data-ttu-id="d2231-908">사용자가 마지막으로 방문한 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-908">Site that the user last visited.</span></span> <span data-ttu-id="d2231-909">이 사이트는 현재 사이트에 링크를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-909">This site provided a link to the current site.</span></span> |
| <span data-ttu-id="d2231-910">csHost</span><span class="sxs-lookup"><span data-stu-id="d2231-910">csHost</span></span> |<span data-ttu-id="d2231-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-911">W3CIISLog</span></span> |<span data-ttu-id="d2231-912">요청된 호스트 헤더(예: www.mysite.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="d2231-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="d2231-913">scSubStatus</span></span> |<span data-ttu-id="d2231-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-914">W3CIISLog</span></span> |<span data-ttu-id="d2231-915">하위 상태 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-915">Substatus error code.</span></span> |
| <span data-ttu-id="d2231-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="d2231-916">scWin32Status</span></span> |<span data-ttu-id="d2231-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-917">W3CIISLog</span></span> |<span data-ttu-id="d2231-918">Windows 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-918">Windows status code.</span></span> |
| <span data-ttu-id="d2231-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="d2231-919">csBytes</span></span> |<span data-ttu-id="d2231-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-920">W3CIISLog</span></span> |<span data-ttu-id="d2231-921">클라이언트에서 서버로 요청에서 보낸 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-921">Bytes sent in the request from the client to the server.</span></span> |
| <span data-ttu-id="d2231-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="d2231-922">scBytes</span></span> |<span data-ttu-id="d2231-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="d2231-923">W3CIISLog</span></span> |<span data-ttu-id="d2231-924">서버에서 클라이언트로 응답에서 다시 반환된 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-924">Bytes returned back in the response from the server to the client.</span></span> |
| <span data-ttu-id="d2231-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="d2231-925">ConfigChangeType</span></span> |<span data-ttu-id="d2231-926">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-926">ConfigurationChange</span></span> |<span data-ttu-id="d2231-927">변경의 유형(예: WindowsServices/소프트웨어)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="d2231-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="d2231-928">ChangeCategory</span></span> |<span data-ttu-id="d2231-929">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-929">ConfigurationChange</span></span> |<span data-ttu-id="d2231-930">변경의 범주(수정/추가/제거됨)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-930">Category of the change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="d2231-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="d2231-931">SoftwareType</span></span> |<span data-ttu-id="d2231-932">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-932">ConfigurationChange</span></span> |<span data-ttu-id="d2231-933">소프트웨어의 종류(업데이트/응용 프로그램)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="d2231-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="d2231-934">SoftwareName</span></span> |<span data-ttu-id="d2231-935">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-935">ConfigurationChange</span></span> |<span data-ttu-id="d2231-936">소프트웨어의 이름(소프트웨어 변경에만 적용)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-936">Name of the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="d2231-937">게시자</span><span class="sxs-lookup"><span data-stu-id="d2231-937">Publisher</span></span> |<span data-ttu-id="d2231-938">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-938">ConfigurationChange</span></span> |<span data-ttu-id="d2231-939">소프트웨어를 게시하는 공급 업체(소프트웨어 변경에만 적용)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-939">Vendor who publishes the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="d2231-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="d2231-940">SvcChangeType</span></span> |<span data-ttu-id="d2231-941">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-941">ConfigurationChange</span></span> |<span data-ttu-id="d2231-942">Windows 서비스에 적용된 변경의 유형(상태/StartupType/경로/ServiceAccount)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="d2231-943">이는 Windows 서비스 변경에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-943">This is only applicable to Windows service changes.</span></span> |
| <span data-ttu-id="d2231-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="d2231-944">SvcDisplayName</span></span> |<span data-ttu-id="d2231-945">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-945">ConfigurationChange</span></span> |<span data-ttu-id="d2231-946">변경된 서비스의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-946">Display name of the service that was changed.</span></span> |
| <span data-ttu-id="d2231-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="d2231-947">SvcName</span></span> |<span data-ttu-id="d2231-948">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-948">ConfigurationChange</span></span> |<span data-ttu-id="d2231-949">변경된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-949">Name of the service that was changed.</span></span> |
| <span data-ttu-id="d2231-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="d2231-950">SvcState</span></span> |<span data-ttu-id="d2231-951">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-951">ConfigurationChange</span></span> |<span data-ttu-id="d2231-952">서비스의 새 (현재) 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-952">New (current) state of the service.</span></span> |
| <span data-ttu-id="d2231-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="d2231-953">SvcPreviousState</span></span> |<span data-ttu-id="d2231-954">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-954">ConfigurationChange</span></span> |<span data-ttu-id="d2231-955">이전에 알려진 서비스의 상태(서비스 상태를 변경한 경우만 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-955">Previous known state of the service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="d2231-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="d2231-956">SvcStartupType</span></span> |<span data-ttu-id="d2231-957">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-957">ConfigurationChange</span></span> |<span data-ttu-id="d2231-958">서비스 시작 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-958">Service startup type.</span></span> |
| <span data-ttu-id="d2231-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="d2231-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="d2231-960">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-960">ConfigurationChange</span></span> |<span data-ttu-id="d2231-961">이전 서비스 시작 유형(서비스 시작 유형을 변경하는 경우만 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="d2231-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="d2231-962">SvcAccount</span></span> |<span data-ttu-id="d2231-963">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-963">ConfigurationChange</span></span> |<span data-ttu-id="d2231-964">서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-964">Service account.</span></span> |
| <span data-ttu-id="d2231-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="d2231-965">SvcPreviousAccount</span></span> |<span data-ttu-id="d2231-966">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-966">ConfigurationChange</span></span> |<span data-ttu-id="d2231-967">이전 서비스 계정(서비스 계정이 변경된 경우만 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="d2231-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="d2231-968">SvcPath</span></span> |<span data-ttu-id="d2231-969">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-969">ConfigurationChange</span></span> |<span data-ttu-id="d2231-970">Windows 서비스의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-970">Path to the executable of the Windows service.</span></span> |
| <span data-ttu-id="d2231-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="d2231-971">SvcPreviousPath</span></span> |<span data-ttu-id="d2231-972">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-972">ConfigurationChange</span></span> |<span data-ttu-id="d2231-973">Windows 서비스에 대한 실행 파일의 이전 경로(이것이 변경된 경우에 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-973">Previous path of the executable for the Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="d2231-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="d2231-974">SvcDescription</span></span> |<span data-ttu-id="d2231-975">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-975">ConfigurationChange</span></span> |<span data-ttu-id="d2231-976">서비스에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-976">Description of the service.</span></span> |
| <span data-ttu-id="d2231-977">이전</span><span class="sxs-lookup"><span data-stu-id="d2231-977">Previous</span></span> |<span data-ttu-id="d2231-978">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-978">ConfigurationChange</span></span> |<span data-ttu-id="d2231-979">이 소프트웨어의 이전 상태(설치됨/설치되지 않음/이전 버전)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="d2231-980">Current</span><span class="sxs-lookup"><span data-stu-id="d2231-980">Current</span></span> |<span data-ttu-id="d2231-981">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="d2231-981">ConfigurationChange</span></span> |<span data-ttu-id="d2231-982">이 소프트웨어의 최근 상태(설치됨/설치되지 않음/현재 버전)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2231-983">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2231-983">Next steps</span></span>
<span data-ttu-id="d2231-984">로그 검색에 대한 자세한 내용은 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2231-984">For additional information about log searches:</span></span>

* <span data-ttu-id="d2231-985">[로그 검색](log-analytics-log-searches.md) 을 숙지하여 솔루션에서 수집한 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-985">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="d2231-986">[Log Analytics의 사용자 지정 필드](log-analytics-custom-fields.md)를 사용하여 로그 검색을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2231-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
