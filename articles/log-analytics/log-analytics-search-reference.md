---
title: "aaaAzure 로그 분석 검색 참조 | Microsoft Docs"
description: "로그 분석 검색 참조 hello hello 검색 언어에 설명 하 고 데이터 검색 및 필터링 식을 toohelp 검색 범위 좁히기 때 사용할 수 있는 hello 일반 쿼리 구문 옵션을 제공 합니다."
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
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="ae7fe-103">Log Analytics 검색 참조</span><span class="sxs-lookup"><span data-stu-id="ae7fe-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="ae7fe-104">이 문서에서는 로그 분석에 hello 현재 쿼리 언어를 사용 하 여 로그 검색을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="ae7fe-105">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 너무 참조 해야 하는 다음[hello 새 언어에 대 한 언어 참조 hello](https://go.microsoft.com/fwlink/?linkid=856079)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[hello language reference for hello new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="ae7fe-106">hello 검색 언어에 대 한 참조 섹션에 설명 hello 일반 쿼리 구문 옵션 데이터 검색 및 필터링 식을 toohelp 검색 범위 좁히기 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-106">hello following reference section about search language describes hello general query syntax options you can use when searching for data and filtering expressions toohelp narrow your search.</span></span> <span data-ttu-id="ae7fe-107">검색 된 hello 데이터에서 tootake 동작을 사용할 수 있는 명령을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-107">It also describes commands that you can use tootake action on hello data retrieved.</span></span>

<span data-ttu-id="ae7fe-108">검색을 반환 하는 hello 필드에 대 한 읽을 수 있으며 hello 패싯 데 도움이 되는 검색 데이터의 hello와 유사한 범주에 대 한 자세한 [검색 필드 및 패싯 참조 섹션](#search-field-and-facet-reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-108">You can read about hello fields returned in searches, and hello facets that help you discover more about similar categories of data, in hello [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="ae7fe-109">일반 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-109">General query syntax</span></span>
<span data-ttu-id="ae7fe-110">hello 일반 쿼리 하기 위한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-110">hello syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="ae7fe-111">필터 식 hello (`filterExpression`) hello에 대 한 "where" 조건을 hello 쿼리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-111">hello filter expression (`filterExpression`) defines hello "where" condition for hello query.</span></span> <span data-ttu-id="ae7fe-112">hello 명령은 hello 쿼리에 의해 반환 된 toohello 결과 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-112">hello commands apply toohello results returned by hello query.</span></span> <span data-ttu-id="ae7fe-113">여러 개의 명령은 hello 세로줄 문자 (|)로 구분 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-113">Multiple commands must be separated by hello pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="ae7fe-114">일반 구문 예제</span><span class="sxs-lookup"><span data-stu-id="ae7fe-114">General syntax examples</span></span>
<span data-ttu-id="ae7fe-115">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-115">Examples:</span></span>

```
system
```

<span data-ttu-id="ae7fe-116">이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 검색 용어 또는 전체 텍스트 인덱싱된 모든 필드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-116">This query returns results that contain hello word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7fe-117">모든 필드가 이러한 방식으로 인덱싱되지 않는 hello 가장 일반적인 텍스트 필드 (예: 설명 및 이름) 일반적으로.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-117">Not all fields are indexed this way, but hello most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="ae7fe-118">이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 및 *오류*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-118">This query returns results that contain hello words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="ae7fe-119">이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 및 *오류*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-119">This query returns results that contain hello words *system* and *error*.</span></span> <span data-ttu-id="ae7fe-120">다음 hello 하 여 hello 결과 정렬 *ManagementGroupName* 필드 (오름차순), 한 다음 hello *TimeGenerated* (내림차순) 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-120">It then sorts hello results by hello *ManagementGroupName* field (in ascending order), and then by hello *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="ae7fe-121">처음 10 개 결과가 hello이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-121">It takes only hello first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae7fe-122">모든 hello 필드 이름 및 hello 문자열 및 텍스트 필드에 대 한 hello 값은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-122">All hello field names and hello values for hello string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="ae7fe-123">필터 식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-123">Filter expressions</span></span>
<span data-ttu-id="ae7fe-124">다음 하위 섹션으로 구성 하는 hello에 hello 필터 식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-124">hello following subsections explain hello filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="ae7fe-125">문자열 리터럴</span><span class="sxs-lookup"><span data-stu-id="ae7fe-125">String literals</span></span>
<span data-ttu-id="ae7fe-126">문자열 리터럴을 키워드 또는 미리 정의 된 데이터 형식 (예를 들어 숫자 또는 날짜)으로 hello 파서에서 인식 되지 않는 모든 문자열.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-126">A string literal is any string that is not recognized by hello parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="ae7fe-127">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="ae7fe-128">이 쿼리는 발생하는 5개 단어를 모두 포함하는 결과를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="ae7fe-129">복잡 한 문자열 검색 tooperform hello 문자열을 리터럴을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-129">tooperform a complex string search, enclose hello string literal in quotation marks.</span></span> <span data-ttu-id="ae7fe-130">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="ae7fe-131">*Windows Server*와 정확히 일치하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="ae7fe-132">숫자</span><span class="sxs-lookup"><span data-stu-id="ae7fe-132">Numbers</span></span>
<span data-ttu-id="ae7fe-133">hello 파서는 숫자 필드에 대 한 hello 10 진수 정수 및 부동 소수점 수 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-133">hello parser supports hello decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="ae7fe-134">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="ae7fe-135">날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="ae7fe-135">Dates and times</span></span>
<span data-ttu-id="ae7fe-136">Hello 시스템 데이터의 모든 부분을 *TimeGenerated* hello 원래 날짜 및 hello 레코드의 시간을 나타내는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-136">Every piece of data in hello system has a *TimeGenerated* property, which represents hello original date and time of hello record.</span></span> <span data-ttu-id="ae7fe-137">또한 일부 데이터 형식에 더 많은 날짜 및 시간 필드가 있을 수 있습니다(예를 들어 *LastModified*).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="ae7fe-138">타임 라인 hello **차트/시간** Azure 로그 분석에 선택 기가 (따라 toohello 현재 실행 중인 쿼리에) 시간에 따른 결과의 분포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-138">hello timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according toohello current query being run).</span></span> <span data-ttu-id="ae7fe-139">이 hello 기반 *TimeGenerated* 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-139">This is based on hello *TimeGenerated* field.</span></span> <span data-ttu-id="ae7fe-140">날짜 및 시간 필드는 쿼리 toorestrict hello 쿼리 tooa 특정 시간 내에 사용할 수 있는 특정 문자열 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-140">Date and time fields have a specific string format that can be used in queries toorestrict hello query tooa particular timeframe.</span></span> <span data-ttu-id="ae7fe-141">구문 toorefer toorelative 사이의 시간 간격 (예를 들어 "3 일 전 및 2 시간 전")를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-141">You can also use syntax toorefer toorelative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="ae7fe-142">hello 다음은 날짜 및 시간에 유효한 형식의 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-142">hello following are valid forms of syntax for dates and times:</span></span>

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


<span data-ttu-id="ae7fe-143">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="ae7fe-144">hello 이전 명령에는 레코드를 반환는 *TimeGenerated* 2013 년 10 월 1 일 12 시 20 정확히의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-144">hello previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="ae7fe-145">hello 파서도 지원 hello mnemonic 날짜/시간 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-145">hello parser also supports hello mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="ae7fe-146">(그럴 가능성은 모든 결과 생성할 데이터 hello 빠른 시스템을 통해 변경할 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="ae7fe-146">(It is unlikely that this will yield any results, because data doesn’t make it through hello system that fast.)</span></span>

<span data-ttu-id="ae7fe-147">다음이 예제는 상대 및 절대 날짜에 대 한 빌딩 블록 toouse 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-147">These examples are building blocks toouse for relative and absolute dates.</span></span> <span data-ttu-id="ae7fe-148">Hello 다음 세 하위 섹션에서 어떻게 toouse에 더 높은 수준의 표시 상대 날짜 범위를 사용 하는 예제 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-148">In hello next three subsections, you'll see how toouse them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="ae7fe-149">날짜/시간 수학</span><span class="sxs-lookup"><span data-stu-id="ae7fe-149">Date/Time math</span></span>
<span data-ttu-id="ae7fe-150">날짜/시간 수학 연산자 toooffset hello를 사용 하 여 또는 간단한 날짜/시간 계산을 사용 하 여 hello 날짜/시간 값을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-150">Use hello Date/Time math operators toooffset or round hello Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="ae7fe-151">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="ae7fe-152">연산자</span><span class="sxs-lookup"><span data-stu-id="ae7fe-152">Operator</span></span> | <span data-ttu-id="ae7fe-153">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="ae7fe-154">날짜/시간 toohello 라운드 단위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-154">Rounds Date/Time toohello specified unit.</span></span> <span data-ttu-id="ae7fe-155">예를 들어 지금 / 일 hello의 현재 날짜/시간 toomidnight hello를 현재 날짜로 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-155">For example, NOW/DAY rounds hello current Date/Time toomidnight of hello current day.</span></span> |
| <span data-ttu-id="ae7fe-156">+ 또는-</span><span class="sxs-lookup"><span data-stu-id="ae7fe-156">+ or -</span></span> |<span data-ttu-id="ae7fe-157">날짜/시간 오프셋 hello 단위 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-157">Offsets Date/Time by hello specified number of units.</span></span> <span data-ttu-id="ae7fe-158">예를 들어 지금 + 1 시간은 오프셋 hello 현재 날짜/시간을 한 시간 빠르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-158">For example, NOW+1HOUR offsets hello current Date/Time by one hour ahead.</span></span> <span data-ttu-id="ae7fe-159">2013-10-01t12: 00-10DAYS hello 날짜 값을 10 일 전으로 오프셋 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-159">2013-10-01T12:00-10DAYS offsets hello Date value back by 10 days.</span></span> |

<span data-ttu-id="ae7fe-160">Hello 날짜/시간 수치 연산자를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-160">You can chain hello Date/Time math operators together.</span></span> <span data-ttu-id="ae7fe-161">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="ae7fe-162">hello 다음 표 hello 지원 되는 날짜/시간 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-162">hello following table lists hello supported Date/Time units.</span></span>

| <span data-ttu-id="ae7fe-163">날짜/시간 단위</span><span class="sxs-lookup"><span data-stu-id="ae7fe-163">Date/Time unit</span></span> | <span data-ttu-id="ae7fe-164">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae7fe-165">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-165">YEAR, YEARS</span></span> |<span data-ttu-id="ae7fe-166">라운드 toocurrent 연도 또는 hello에서 오프셋 년 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-166">Rounds toocurrent year, or offsets by hello specified number of years.</span></span> |
| <span data-ttu-id="ae7fe-167">MONTH, MONTHS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-167">MONTH, MONTHS</span></span> |<span data-ttu-id="ae7fe-168">라운드 toocurrent 월 또는 hello 여 오프셋 개월 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-168">Rounds toocurrent month, or offsets by hello specified number of months.</span></span> |
| <span data-ttu-id="ae7fe-169">DAY, DAYS, DATE</span><span class="sxs-lookup"><span data-stu-id="ae7fe-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="ae7fe-170">라운드 toocurrent 날짜 hello 월 또는 hello 여 오프셋 일 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-170">Rounds toocurrent day of hello month, or offsets by hello specified number of days.</span></span> |
| <span data-ttu-id="ae7fe-171">HOUR, HOURS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-171">HOUR, HOURS</span></span> |<span data-ttu-id="ae7fe-172">라운드 toocurrent 시간 또는 오프셋 hello 하 여 지정 된 시간 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-172">Rounds toocurrent hour, or offsets by hello specified number of hours.</span></span> |
| <span data-ttu-id="ae7fe-173">MINUTE, MINUTES</span><span class="sxs-lookup"><span data-stu-id="ae7fe-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="ae7fe-174">라운드 toocurrent 분 또는 hello 여 오프셋 시간 (분)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-174">Rounds toocurrent minute, or offsets by hello specified number of minutes.</span></span> |
| <span data-ttu-id="ae7fe-175">SECOND, SECONDS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-175">SECOND, SECONDS</span></span> |<span data-ttu-id="ae7fe-176">둘째, toocurrent를 반올림 하거나 지정 된 hello 만큼 오프셋 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-176">Rounds toocurrent second, or offsets by hello specified number of seconds.</span></span> |
| <span data-ttu-id="ae7fe-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="ae7fe-178">라운드 toocurrent 밀리초 또는 hello 여 오프셋 시간 (밀리초)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-178">Rounds toocurrent millisecond, or offsets by hello specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="ae7fe-179">필드 패싯</span><span class="sxs-lookup"><span data-stu-id="ae7fe-179">Field facets</span></span>
<span data-ttu-id="ae7fe-180">패싯 필드를 사용 하 여 특정 필드 및 정확한 값에 대 한 hello 검색 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-180">By using field facets, you can specify hello search condition for specific fields and their exact values.</span></span> <span data-ttu-id="ae7fe-181">이와 달리에서 hello 인덱스 전체에서 다양 한 용어에 "자유 텍스트" 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-181">This differs from writing "free text" queries for various terms throughout hello index.</span></span> <span data-ttu-id="ae7fe-182">여러 개의 이전 예에서 이 기법을 이미 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="ae7fe-183">hello 다음은 더 복잡 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-183">hello following are more complex examples.</span></span>

<span data-ttu-id="ae7fe-184">**구문**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="ae7fe-185">**설명**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-185">**Description**</span></span>

<span data-ttu-id="ae7fe-186">검색 hello hello 특정 값에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-186">Searches hello field for hello specific value.</span></span> <span data-ttu-id="ae7fe-187">문자열 리터럴, 숫자 또는 날짜와 시간 hello 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-187">hello value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="ae7fe-188">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="ae7fe-189">**구문**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-189">**Syntax**</span></span>

<span data-ttu-id="ae7fe-190">*field>value*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-190">*field>value*</span></span>

<span data-ttu-id="ae7fe-191">*field<value*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-191">*field<value*</span></span>

<span data-ttu-id="ae7fe-192">*field>=value*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-192">*field>=value*</span></span>

<span data-ttu-id="ae7fe-193">*field<=value*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-193">*field<=value*</span></span>

<span data-ttu-id="ae7fe-194">*field!=value*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-194">*field!=value*</span></span>

<span data-ttu-id="ae7fe-195">**설명**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-195">**Description**</span></span>

<span data-ttu-id="ae7fe-196">비교를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-196">Provides comparisons.</span></span>

<span data-ttu-id="ae7fe-197">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="ae7fe-198">**구문**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="ae7fe-199">**설명**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-199">**Description**</span></span>

<span data-ttu-id="ae7fe-200">패싯 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-200">Provides range faceting.</span></span>

<span data-ttu-id="ae7fe-201">예:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="ae7fe-202">IN</span><span class="sxs-lookup"><span data-stu-id="ae7fe-202">IN</span></span>
<span data-ttu-id="ae7fe-203">hello **IN** tooselect 값 목록에서 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-203">hello **IN** keyword allows you tooselect from a list of values.</span></span> <span data-ttu-id="ae7fe-204">사용 하는 hello 구문에 따라이 사용자가 제공한 값의 단순 목록 또는 집계에서 값의 목록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-204">Depending on hello syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="ae7fe-205">구문 1:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="ae7fe-206">이 구문은 tooinclude를 간단한 목록 값이 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-206">This syntax allows you tooinclude all values in a simple list.</span></span>



<span data-ttu-id="ae7fe-207">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="ae7fe-208">구문 2:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-208">Syntax 2:</span></span>

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

<span data-ttu-id="ae7fe-209">이 구문은 집계 toocreate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-209">This syntax allows you toocreate an aggregation.</span></span> <span data-ttu-id="ae7fe-210">그런 다음 해당 값이 있는 이벤트를 찾는 다른 외부 (기본) 검색에 해당 집계의 hello 값 목록이 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-210">You can then feed hello list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="ae7fe-211">이렇게 하려면 hello 내부 검색을 중괄호로 묶고 hello IN 연산자를 사용 하 여 hello 외부 검색에서 필드에 대 한 가능한 값으로 해당 결과 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-211">You do this by enclosing hello inner search in braces, and feeding its results as possible values for a field in hello outer search by using hello IN operator.</span></span>

<span data-ttu-id="ae7fe-212">내부 쿼리 예: *현재 보안 업데이트가 누락 된 컴퓨터* 다음 집계 쿼리 hello로:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-212">Inner query example: *computers currently missing security updates* with hello following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="ae7fe-213">hello 찾는 최종 쿼리 *현재 보안 업데이트가 누락 된 컴퓨터에 대 한 모든 Windows 이벤트* hello 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-213">hello final query that finds *all Windows events for computers currently missing security updates* resembles hello following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="ae7fe-214">포함</span><span class="sxs-lookup"><span data-stu-id="ae7fe-214">Contains</span></span>
<span data-ttu-id="ae7fe-215">hello **Contains** toofilter 지정한 문자열을 포함 하는 필드와 레코드에 대 한 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-215">hello **Contains** keyword allows you toofilter for records with a field that contains a specified string.</span></span> <span data-ttu-id="ae7fe-216">이는 대/소문자를 구분하고 문자열 필드에 대해서만 작동하며 이스케이프 문자를 포함하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="ae7fe-217">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="ae7fe-218">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="ae7fe-219">"이벤트" hello 문자열을 포함 하는 형식 가진 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-219">This returns records with a type that contains hello string "Event".</span></span> <span data-ttu-id="ae7fe-220">예를 들어 **이벤트**, **SecurityEvent** 및 **ServiceFabricOperationEvent**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="ae7fe-221">정규식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-221">Regular expressions</span></span>
<span data-ttu-id="ae7fe-222">Hello를 사용 하 여 정규식을 필드에 대 한 검색 조건을 지정할 수 있습니다 **Regex** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-222">You can specify a search condition for a field with a regular expression, by using hello **Regex** keyword.</span></span> <span data-ttu-id="ae7fe-223">정규식에는 데 사용할 수는 hello 구문 설명과 참조 [로그 분석에서 정규식 toofilter 로그 검색을 사용 하 여](log-analytics-log-searches-regex.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-223">For a complete description of hello syntax you can use in regular expressions, see [Using regular expressions toofilter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="ae7fe-224">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="ae7fe-225">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="ae7fe-226">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="ae7fe-226">Logical operators</span></span>
<span data-ttu-id="ae7fe-227">hello 쿼리 언어 지원 hello 논리 연산자 (*AND*, *또는*, 및 *하지*) 및 해당 C 스타일 별칭 (*&&*,  *||* , 및 *!*각각).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-227">hello query languages support hello logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="ae7fe-228">괄호 toogroup 이러한 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-228">You can use parentheses toogroup these operators.</span></span>

<span data-ttu-id="ae7fe-229">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="ae7fe-230">Hello hello 최상위 필터 인수에 대 한 논리 연산자를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-230">You can omit hello logical operator for hello top-level filter arguments.</span></span> <span data-ttu-id="ae7fe-231">이 경우 hello AND 연산자를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-231">In this case, hello AND operator is assumed.</span></span>

| <span data-ttu-id="ae7fe-232">필터 식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-232">Filter expression</span></span> | <span data-ttu-id="ae7fe-233">해당 하는 너무</span><span class="sxs-lookup"><span data-stu-id="ae7fe-233">Equivalent too</span></span>|
| --- | --- |
| <span data-ttu-id="ae7fe-234">시스템 오류</span><span class="sxs-lookup"><span data-stu-id="ae7fe-234">system error</span></span> |<span data-ttu-id="ae7fe-235">시스템 AND 오류</span><span class="sxs-lookup"><span data-stu-id="ae7fe-235">system AND error</span></span> |
| <span data-ttu-id="ae7fe-236">시스템 "Windows Server" OR 심각도:1</span><span class="sxs-lookup"><span data-stu-id="ae7fe-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="ae7fe-237">시스템 AND ("Windows Server" OR 심각도:1)</span><span class="sxs-lookup"><span data-stu-id="ae7fe-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="ae7fe-238">와일드 카드 사용</span><span class="sxs-lookup"><span data-stu-id="ae7fe-238">Wildcarding</span></span>
<span data-ttu-id="ae7fe-239">hello 쿼리 언어를 지 원하는 hello를 사용 하 여 ( \* ) 문자 너무 쿼리에서 값에 대 한 하나 이상의 문자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-239">hello query language supports using hello ( \* ) character too represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="ae7fe-240">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-240">Example:</span></span>

 <span data-ttu-id="ae7fe-241">과 같이"Redmond" hello 이름에 "SQL"로 모든 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-241">Find all computers with "SQL" in hello name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="ae7fe-242">현재 와일드 카드는 따옴표 안에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="ae7fe-243">예를 들어 hello 메시지 `"*This text*"` hello 간주 (\*) 리터럴로 사용할 (\*) 문자.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-243">For example, hello message `"*This text*"` considers hello (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="ae7fe-244">명령</span><span class="sxs-lookup"><span data-stu-id="ae7fe-244">Commands</span></span>


<span data-ttu-id="ae7fe-245">hello 명령은 hello 쿼리에 의해 반환 되는 toohello 결과 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-245">hello commands apply toohello results that are returned by hello query.</span></span> <span data-ttu-id="ae7fe-246">사용 하 여 hello 파이프 문자 (|) tooapply 명령 toohello 결과 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-246">Use hello pipe character ( | ) tooapply a command toohello retrieved results.</span></span> <span data-ttu-id="ae7fe-247">여러 개의 명령은 hello 파이프 문자로 구분 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-247">Multiple commands must be separated by hello pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7fe-248">명령 이름은 대문자 또는 소문자 hello 필드 이름 및 hello 데이터와 달리 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-248">Command names can be written in upper case or lower case, unlike hello field names and hello data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="ae7fe-249">정렬</span><span class="sxs-lookup"><span data-stu-id="ae7fe-249">Sort</span></span>
<span data-ttu-id="ae7fe-250">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="ae7fe-251">특정 필드에 hello 결과 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-251">Sorts hello results by particular fields.</span></span> <span data-ttu-id="ae7fe-252">hello asc/desc 접미사 toosort hello 결과를 오름차순 또는 내림차순 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-252">hello asc/desc suffix toosort hello results in ascending or descending order is optional.</span></span> <span data-ttu-id="ae7fe-253">생략 하는 hello *asc* 정렬 순서를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-253">If it is omitted, hello *asc* sort order is assumed.</span></span> <span data-ttu-id="ae7fe-254">Hello에 대 한 **TimeGenerated** 필드 *desc* 기본적으로 먼저 hello 가장 최근의 결과 반환 하므로 정렬 순서를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-254">For hello **TimeGenerated** field, *desc* sort order is assumed, so it returns hello most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="ae7fe-255">위쪽/제한</span><span class="sxs-lookup"><span data-stu-id="ae7fe-255">Top/Limit</span></span>
<span data-ttu-id="ae7fe-256">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="ae7fe-257">제한 hello 응답 toohello 상위 n 개 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-257">Limits hello response toohello top N results.</span></span>

<span data-ttu-id="ae7fe-258">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="ae7fe-259">반환 결과 일치 하는 상위 10을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-259">Returns hello top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="ae7fe-260">Skip</span><span class="sxs-lookup"><span data-stu-id="ae7fe-260">Skip</span></span>
<span data-ttu-id="ae7fe-261">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-261">Syntax:</span></span>

    skip number

<span data-ttu-id="ae7fe-262">건너뜁니다 hello 나열 된 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-262">Skips hello number of results listed.</span></span>

<span data-ttu-id="ae7fe-263">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="ae7fe-264">200개 결과에서 시작하여 상위 10개의 일치하는 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="ae7fe-265">여기서</span><span class="sxs-lookup"><span data-stu-id="ae7fe-265">Select</span></span>
<span data-ttu-id="ae7fe-266">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="ae7fe-267">선택한 결과 toohello 필드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-267">Limits results toohello fields you choose.</span></span>

<span data-ttu-id="ae7fe-268">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="ae7fe-269">반환 된 결과 필드를 너무 hello 제한*이름* 및 *심각도*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-269">Limits hello returned results fields too*Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="ae7fe-270">측정값</span><span class="sxs-lookup"><span data-stu-id="ae7fe-270">Measure</span></span>
<span data-ttu-id="ae7fe-271">hello *측정값* 명령에 사용 되는 tooapply 통계 함수 toohello 원시 검색 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-271">hello *measure* command is used tooapply statistical functions toohello raw search results.</span></span> <span data-ttu-id="ae7fe-272">이 매우 유용한 tooget *group by* hello 데이터 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-272">This is very useful tooget *group-by* views over hello data.</span></span> <span data-ttu-id="ae7fe-273">Hello 측정값 명령을 사용 하면 로그 분석 검색 집계 된 결과가 포함 된 테이블을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-273">When you use hello measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="ae7fe-274">**구문:**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="ae7fe-275">집계 hello *groupField*를 사용 하 여 hello 집계 측정값을 계산 하 고 *aggregatedField*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-275">Aggregates hello results by *groupField*, and calculates hello aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="ae7fe-276">측정 통계 함수</span><span class="sxs-lookup"><span data-stu-id="ae7fe-276">Measure statistical function</span></span> | <span data-ttu-id="ae7fe-277">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae7fe-278">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-278">*aggregateFunction*</span></span> |<span data-ttu-id="ae7fe-279">hello 이름 (대/소문자 구분) hello 집계 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-279">hello name of hello aggregate function (case insensitive).</span></span> <span data-ttu-id="ae7fe-280">집계 함수를 수행 하는 hello는 지원: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, 백분위 수 # # 또는 PCT # # (# #은 1과 99 사이의 임의의 숫자)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-280">hello following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="ae7fe-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-281">*aggregatedField*</span></span> |<span data-ttu-id="ae7fe-282">집계 중인 hello 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-282">hello field that is being aggregated.</span></span> <span data-ttu-id="ae7fe-283">이 필드는 COUNT 집계 함수 hello에 대 한 선택 사항 이지만 toobe 기존 숫자 필드는 SUM, MAX, MIN, AVG, STDDEV, 백분위 수 # # 또는 PCT # #에 대 한 (# #은 1과 99 사이의 임의의 숫자)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-283">This field is optional for hello COUNT aggregate function, but has toobe an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="ae7fe-284">hello aggregatedField도 중 하나일 수 있습니다 hello **확장** 함수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-284">hello aggregatedField can also be any of hello **Extend** supported functions.</span></span> |
| <span data-ttu-id="ae7fe-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-285">*fieldAlias*</span></span> |<span data-ttu-id="ae7fe-286">hello에 대 한 별칭 (선택 사항)는 hello 집계 값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-286">hello (optional) alias for hello calculated aggregated value.</span></span> <span data-ttu-id="ae7fe-287">지정 하지 않으면 hello 필드 이름이 **AggregatedValue**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-287">If not specified, hello field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="ae7fe-288">*groupField*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-288">*groupField*</span></span> |<span data-ttu-id="ae7fe-289">hello 결과 집합는 hello 필드의 hello 이름으로 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-289">hello name of hello field that hello result set is grouped by.</span></span> |
| <span data-ttu-id="ae7fe-290">*간격*</span><span class="sxs-lookup"><span data-stu-id="ae7fe-290">*Interval*</span></span> |<span data-ttu-id="ae7fe-291">hello 형식에서 hello 시간 간격:**nnnNAME**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-291">hello time interval, in hello format:**nnnNAME**.</span></span> <span data-ttu-id="ae7fe-292">**nnn**hello 양의 정수 번호가입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-292">**nnn** is hello positive integer number.</span></span> <span data-ttu-id="ae7fe-293">**이름** hello 간격 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-293">**NAME** is hello interval name.</span></span> <span data-ttu-id="ae7fe-294">지원되는 간격 이름은 대/소문자를 구분하며 MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S] 및 YEAR[S]를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="ae7fe-295">hello 간격 옵션 날짜/시간 그룹 필드 에서만 사용할 수 있습니다 (예: *TimeGenerated* 및 *TimeCreated*).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-295">hello interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="ae7fe-296">현재, hello 서비스에 의해 적용 되지 않지만 toohello 백 엔드로 전달 되는 날짜/시간 없는 필드에 런타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-296">Currently, this is not enforced by hello service, but a field without Date/Time that is passed toohello back end causes a runtime error.</span></span> <span data-ttu-id="ae7fe-297">Hello 스키마 유효성 검사를 구현 하는 경우 hello 서비스 API는 집계 간격에 대해 날짜/시간 없는 필드를 사용 하는 쿼리를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-297">When hello schema validation is implemented, hello service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="ae7fe-298">현재 hello *측정값* 구현은 임의의 집계 함수에 대 한 간격 그룹화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-298">hello current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="ae7fe-299">Hello BY 절을 생략 하지만 간격을 지정 하 여 (두 번째 구문 처럼), hello *TimeGenerated* 기본적으로 필드를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-299">If hello BY clause is omitted, but an interval is specified (as a second syntax), hello *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="ae7fe-300">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-300">Examples:</span></span>

<span data-ttu-id="ae7fe-301">**예 1**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="ae7fe-302">그룹에서 경고 hello *ObjectID*, hello 각 그룹에 대 한 경고 수를 계산 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-302">Groups hello alerts by *ObjectID*, and calculates hello number of alerts for each group.</span></span> <span data-ttu-id="ae7fe-303">hello 집계 된 값으로 반환 됩니다 hello *Count* 필드 (별칭).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-303">hello aggregated value is returned as hello *Count* field (alias).</span></span>

<span data-ttu-id="ae7fe-304">**예 2**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="ae7fe-305">그룹 1 시간 간격으로 경고 hello를 사용 하 여 hello *TimeGenerated* 필드 및 각 간격의 경고 hello 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-305">Groups hello alerts by 1-hour intervals by using hello *TimeGenerated* field, and returns hello number of alerts in each interval.</span></span>

<span data-ttu-id="ae7fe-306">**예 3**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="ae7fe-307">Hello 이전 예제와 동일 하지만 집계 된 필드 별칭 (*AlertsPerHour*).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-307">Same as hello previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="ae7fe-308">**예제 4**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-308">**Example 4**</span></span>

    * <span data-ttu-id="ae7fe-309">| measure count() by TimeCreated interval 5DAYS</span><span class="sxs-lookup"><span data-stu-id="ae7fe-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="ae7fe-310">Hello를 사용 하 여 5 일 간격으로 hello 결과 그룹화 *TimeCreated* 필드 및 각 간격의 결과의 hello 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-310">Groups hello results by 5-day intervals by using hello *TimeCreated* field, and returns hello number of results in each interval.</span></span>

<span data-ttu-id="ae7fe-311">**예제 5**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="ae7fe-312">그룹 워크 로드 이름 별로 경고를 hello 및 반환 hello 각 워크플로에 대 한 최대 경고 심각도 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-312">Groups hello alerts by workload name, and returns hello maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="ae7fe-313">**예제 6**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="ae7fe-314">Hello 이전 예제와 동일 하지만 hello로 *min* 집계 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-314">Same as hello previous example, but with hello *min* aggregated function.</span></span>

<span data-ttu-id="ae7fe-315">**예제 7**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="ae7fe-316">Perf 컴퓨터 별로 그룹화 하 고 hello 평균 (평균)을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-316">Groups Perf by computer, and calculates hello average (avg).</span></span>

<span data-ttu-id="ae7fe-317">**예제 8**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="ae7fe-318">Hello 이전 예제와 동일 하지만 사용 *sum*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-318">Same as hello previous example, but uses *sum*.</span></span>

<span data-ttu-id="ae7fe-319">**예제 9**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="ae7fe-320">Hello 이전 예제와 동일 하지만 사용 *stddev*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-320">Same as hello previous example, but uses *stddev*.</span></span>

<span data-ttu-id="ae7fe-321">**예제 10**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="ae7fe-322">Hello 이전 예제와 동일 하지만 사용 *percentile70*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-322">Same as hello previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="ae7fe-323">**예제 11**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="ae7fe-324">Hello 이전 예제와 동일 하지만 사용 *pct70*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-324">Same as hello previous example, but uses *pct70*.</span></span> <span data-ttu-id="ae7fe-325">*PCT##*은 *PERCENTILE##* 함수의 유일한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="ae7fe-326">**예제 12**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="ae7fe-327">컴퓨터에서 성능 먼저 그룹화 하 고 다음 CounterName 및 hello 평균 (평균)을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-327">Groups Perf first by Computer and then CounterName, and calculates hello average (avg).</span></span>

<span data-ttu-id="ae7fe-328">**예제 13**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="ae7fe-329">Hello hello 최대 경고 수와 상위 5 개 워크플로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-329">Gets hello top five workflows with hello maximum number of alerts.</span></span>

<span data-ttu-id="ae7fe-330">**예제 14**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-330">**Example 14**</span></span>

    * <span data-ttu-id="ae7fe-331">| measure countdistinct(Computer) by Type</span><span class="sxs-lookup"><span data-stu-id="ae7fe-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="ae7fe-332">Hello 각 형식에 대해 보고 하는 고유 컴퓨터 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-332">Counts hello number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="ae7fe-333">**예제 15**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-333">**Example 15**</span></span>

    * <span data-ttu-id="ae7fe-334">| measure countdistinct(Computer) Interval 1HOUR</span><span class="sxs-lookup"><span data-stu-id="ae7fe-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="ae7fe-335">Hello 매시간에 대 한 보고 하는 고유 컴퓨터 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-335">Counts hello number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="ae7fe-336">**예제 16**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="ae7fe-337">% Processor Time 컴퓨터 별로 그룹화 하 고 1 시간 마다 hello 평균을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-337">Groups % Processor Time by Computer, and returns hello average for every hour.</span></span>

<span data-ttu-id="ae7fe-338">**예제 17**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="ae7fe-339">W3CIISLog 방법으로 그룹화 하 고 5 분 마다에 대 한 hello를 최대 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-339">Groups W3CIISLog by method, and returns hello maximum for every 5 minutes.</span></span>

<span data-ttu-id="ae7fe-340">**예제 18**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="ae7fe-341">컴퓨터 및 반환 hello, 평균, 75th 백분위 수를 최대값과 최소값에 1 시간 마다 하 여 그룹 % 프로세서 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-341">Groups % Processor Time by computer, and returns hello minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="ae7fe-342">**예제 19**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="ae7fe-343">그룹 % Processor Time 먼저 컴퓨터와 인스턴스 이름 및 평균을 반환 hello 최소 75 번째 백분위 수, 및 최대 1 시간 마다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-343">Groups % Processor Time first by computer and then by Instance name, and returns hello minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="ae7fe-344">**예제 20**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="ae7fe-345">컴퓨터에 모든 디스크에 대 한 분당 디스크 쓰기 hello 최대값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-345">Calculates hello maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="ae7fe-346">Where</span><span class="sxs-lookup"><span data-stu-id="ae7fe-346">Where</span></span>
<span data-ttu-id="ae7fe-347">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="ae7fe-348">뒤에 사용할 수는 *측정값* 명령 toofurther 필터 hello 집계 결과 hello *측정값* 집계 함수가 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-348">Can only be used after a *Measure* command toofurther filter hello aggregated results that hello *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="ae7fe-349">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="ae7fe-350">Dedup</span><span class="sxs-lookup"><span data-stu-id="ae7fe-350">Dedup</span></span>
<span data-ttu-id="ae7fe-351">구문</span><span class="sxs-lookup"><span data-stu-id="ae7fe-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="ae7fe-352">Hello 필드의 모든 고 윳 값에 대 한 hello 첫 번째 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-352">Returns hello first document found for every unique value of hello given field.</span></span>

<span data-ttu-id="ae7fe-353">예제:</span><span class="sxs-lookup"><span data-stu-id="ae7fe-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="ae7fe-354">이 예에서는 EventID 당 하나의 이벤트 (hello 최신 이벤트)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-354">This example returns one event (hello latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="ae7fe-355">Join</span><span class="sxs-lookup"><span data-stu-id="ae7fe-355">Join</span></span>
<span data-ttu-id="ae7fe-356">조인 결과를 두 개의 쿼리는 단일 tooform hello 결과 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-356">Joins hello results of two queries tooform a single result set.</span></span>  <span data-ttu-id="ae7fe-357">테이블에 따라 hello에 설명 된 여러 개의 조인 유형을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-357">Supports multiple join types described in hello follow table.</span></span>

| <span data-ttu-id="ae7fe-358">조인 유형</span><span class="sxs-lookup"><span data-stu-id="ae7fe-358">Join type</span></span> | <span data-ttu-id="ae7fe-359">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="ae7fe-360">inner</span><span class="sxs-lookup"><span data-stu-id="ae7fe-360">inner</span></span> | <span data-ttu-id="ae7fe-361">두 쿼리 모두 일치하는 값을 가진 레코드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="ae7fe-362">outer</span><span class="sxs-lookup"><span data-stu-id="ae7fe-362">outer</span></span> | <span data-ttu-id="ae7fe-363">두 쿼리 모두에서 모든 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="ae7fe-364">left</span><span class="sxs-lookup"><span data-stu-id="ae7fe-364">left</span></span>  | <span data-ttu-id="ae7fe-365">왼쪽 쿼리의 모든 레코드와 오른쪽 쿼리에서 일치하는 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="ae7fe-366">조인 hello를 포함 하는 쿼리를 현재 지원 하지 않는 **IN** 키워드, hello **측정값** 명령 또는 hello **확장** hello 오른쪽 쿼리에서 필드 대상으로 하는 경우 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-366">Joins do not currently support queries that include hello **IN** keyword, hello **Measure** command or hello **Extend** command if it targets a field from hello right query.</span></span>
- <span data-ttu-id="ae7fe-367">현재는 조인에 단일 필드만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="ae7fe-368">단일 검색에서 둘 이상의 조인이 포함되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="ae7fe-369">**구문**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="ae7fe-370">**예**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-370">**Examples**</span></span>

<span data-ttu-id="ae7fe-371">tooillustrate hello 다른 조인 유형, 각 컴퓨터에 대 한 MyBackup_CL hello 하트 비트를 사용 하 여 호출 하는 사용자 지정 로그에서 수집 된 데이터 형식에 가입 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-371">tooillustrate hello different join types, consider joining a data type collected from a custom log called MyBackup_CL with hello heartbeat for each computer.</span></span>  <span data-ttu-id="ae7fe-372">이러한 데이터 형식이 같은 데이터가 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-372">These datatypes have hello following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="ae7fe-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-373">TimeGenerated</span></span> | <span data-ttu-id="ae7fe-374">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-374">Computer</span></span> | <span data-ttu-id="ae7fe-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="ae7fe-376">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="ae7fe-377">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-377">srv01.contoso.com</span></span> | <span data-ttu-id="ae7fe-378">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-378">Success</span></span> |
| <span data-ttu-id="ae7fe-379">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="ae7fe-380">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-380">srv02.contoso.com</span></span> | <span data-ttu-id="ae7fe-381">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-381">Success</span></span> |
| <span data-ttu-id="ae7fe-382">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="ae7fe-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-383">srv03.contoso.com</span></span> | <span data-ttu-id="ae7fe-384">실패</span><span class="sxs-lookup"><span data-stu-id="ae7fe-384">Failure</span></span> |

<span data-ttu-id="ae7fe-385">`Type = Hearbeat`(표시된 필드의 하위 집합만)</span><span class="sxs-lookup"><span data-stu-id="ae7fe-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="ae7fe-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-386">TimeGenerated</span></span> | <span data-ttu-id="ae7fe-387">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-387">Computer</span></span> | <span data-ttu-id="ae7fe-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="ae7fe-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="ae7fe-389">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="ae7fe-390">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-390">srv01.contoso.com</span></span> | <span data-ttu-id="ae7fe-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="ae7fe-391">10.10.100.1</span></span> |
| <span data-ttu-id="ae7fe-392">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="ae7fe-393">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-393">srv02.contoso.com</span></span> | <span data-ttu-id="ae7fe-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-394">10.10.100.2</span></span> |
| <span data-ttu-id="ae7fe-395">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="ae7fe-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-396">srv04.contoso.com</span></span> | <span data-ttu-id="ae7fe-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="ae7fe-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="ae7fe-398">내부 조인</span><span class="sxs-lookup"><span data-stu-id="ae7fe-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="ae7fe-399">두 데이터 형식에 대 한 hello 컴퓨터 필드와 일치 하는 레코드를 따라 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-399">Returns hello following records where hello computer field matches for both datatypes.</span></span>

| <span data-ttu-id="ae7fe-400">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-400">Computer</span></span>| <span data-ttu-id="ae7fe-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-401">TimeGenerated</span></span> | <span data-ttu-id="ae7fe-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-402">LastBackupStatus</span></span> | <span data-ttu-id="ae7fe-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-403">TimeGenerated_joined</span></span> | <span data-ttu-id="ae7fe-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-404">ComputerIP_joined</span></span> | <span data-ttu-id="ae7fe-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="ae7fe-406">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-406">srv01.contoso.com</span></span> | <span data-ttu-id="ae7fe-407">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="ae7fe-408">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-408">Success</span></span> | <span data-ttu-id="ae7fe-409">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="ae7fe-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="ae7fe-410">10.10.100.1</span></span> | <span data-ttu-id="ae7fe-411">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-411">Heartbeat</span></span> |
| <span data-ttu-id="ae7fe-412">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-412">srv02.contoso.com</span></span> | <span data-ttu-id="ae7fe-413">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="ae7fe-414">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-414">Success</span></span> | <span data-ttu-id="ae7fe-415">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="ae7fe-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-416">10.10.100.2</span></span> | <span data-ttu-id="ae7fe-417">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="ae7fe-418">외부 조인</span><span class="sxs-lookup"><span data-stu-id="ae7fe-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="ae7fe-419">Hello 두 데이터 형식에 대 한 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-419">Returns hello following records for both datatypes.</span></span>

| <span data-ttu-id="ae7fe-420">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-420">Computer</span></span>| <span data-ttu-id="ae7fe-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-421">TimeGenerated</span></span> | <span data-ttu-id="ae7fe-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-422">LastBackupStatus</span></span> | <span data-ttu-id="ae7fe-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-423">TimeGenerated_joined</span></span> | <span data-ttu-id="ae7fe-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-424">ComputerIP_joined</span></span> | <span data-ttu-id="ae7fe-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="ae7fe-426">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-426">srv01.contoso.com</span></span> | <span data-ttu-id="ae7fe-427">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="ae7fe-428">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-428">Success</span></span>  | <span data-ttu-id="ae7fe-429">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="ae7fe-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="ae7fe-430">10.10.100.1</span></span> | <span data-ttu-id="ae7fe-431">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-431">Heartbeat</span></span> |
| <span data-ttu-id="ae7fe-432">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-432">srv02.contoso.com</span></span> | <span data-ttu-id="ae7fe-433">4/20/2017 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="ae7fe-434">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-434">Success</span></span>  | <span data-ttu-id="ae7fe-435">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="ae7fe-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-436">10.10.100.2</span></span> | <span data-ttu-id="ae7fe-437">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-437">Heartbeat</span></span> |
| <span data-ttu-id="ae7fe-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-438">srv03.contoso.com</span></span> | <span data-ttu-id="ae7fe-439">4/20/2017 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="ae7fe-440">실패</span><span class="sxs-lookup"><span data-stu-id="ae7fe-440">Failure</span></span>  | <span data-ttu-id="ae7fe-441">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="ae7fe-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="ae7fe-443">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="ae7fe-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-444">10.10.100.2</span></span> | <span data-ttu-id="ae7fe-445">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="ae7fe-446">왼쪽 조인</span><span class="sxs-lookup"><span data-stu-id="ae7fe-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="ae7fe-447">Hello 하트 비트에서 일치 하는 모든 필드와 레코드 MyBackup_CL에서 다음을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-447">Returns hello following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="ae7fe-448">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-448">Computer</span></span>| <span data-ttu-id="ae7fe-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-449">TimeGenerated</span></span> | <span data-ttu-id="ae7fe-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-450">LastBackupStatus</span></span> | <span data-ttu-id="ae7fe-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-451">TimeGenerated_joined</span></span> | <span data-ttu-id="ae7fe-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-452">ComputerIP_joined</span></span> | <span data-ttu-id="ae7fe-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="ae7fe-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="ae7fe-454">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-454">srv01.contoso.com</span></span> | <span data-ttu-id="ae7fe-455">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="ae7fe-456">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-456">Success</span></span> | <span data-ttu-id="ae7fe-457">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="ae7fe-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="ae7fe-458">10.10.100.1</span></span> | <span data-ttu-id="ae7fe-459">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-459">Heartbeat</span></span> |
| <span data-ttu-id="ae7fe-460">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-460">srv02.contoso.com</span></span> | <span data-ttu-id="ae7fe-461">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="ae7fe-462">성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-462">Success</span></span> | <span data-ttu-id="ae7fe-463">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="ae7fe-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-464">10.10.100.2</span></span> | <span data-ttu-id="ae7fe-465">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="ae7fe-465">Heartbeat</span></span> |
| <span data-ttu-id="ae7fe-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="ae7fe-466">srv03.contoso.com</span></span> | <span data-ttu-id="ae7fe-467">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="ae7fe-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="ae7fe-468">실패</span><span class="sxs-lookup"><span data-stu-id="ae7fe-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="ae7fe-469">Extend</span><span class="sxs-lookup"><span data-stu-id="ae7fe-469">Extend</span></span>
<span data-ttu-id="ae7fe-470">쿼리에서 런타임 필드를 toocreate 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-470">Allows you toocreate run-time fields in queries.</span></span> <span data-ttu-id="ae7fe-471">참고 hello 측정값 명령 tooperform 집계 된 런타임 필드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-471">Note that run-time fields cannot be used with hello measure command tooperform aggregation.</span></span>

<span data-ttu-id="ae7fe-472">**예 1**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="ae7fe-473">SQL 평가 권장 사항에 대해 가중 평균 권장 점수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="ae7fe-474">**예 2**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="ae7fe-475">바이트가 아닌 KB 단위로 카운터 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="ae7fe-476">**예 3**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="ae7fe-477">눈금이 0에서 100 사이의 모든 결과 되도록 WireData TotalBytes의 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-477">Scales hello value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="ae7fe-478">**예제 4**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="ae7fe-479">50% 미만인 성능 카운터 값을 LOW로 태깅하고 나머지는 HIGH로 태깅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="ae7fe-480">**예제 5**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="ae7fe-481">컴퓨터에 모든 디스크에 대 한 분당 디스크 쓰기 hello 최대값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-481">Calculates hello maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="ae7fe-482">**지원되는 함수**</span><span class="sxs-lookup"><span data-stu-id="ae7fe-482">**Supported functions**</span></span>

| <span data-ttu-id="ae7fe-483">함수</span><span class="sxs-lookup"><span data-stu-id="ae7fe-483">Function</span></span> | <span data-ttu-id="ae7fe-484">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-484">Description</span></span> | <span data-ttu-id="ae7fe-485">구문 예제</span><span class="sxs-lookup"><span data-stu-id="ae7fe-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae7fe-486">abs</span><span class="sxs-lookup"><span data-stu-id="ae7fe-486">abs</span></span> |<span data-ttu-id="ae7fe-487">Hello의 hello 절대 값을 반환 값 또는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-487">Returns hello absolute value of hello specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="ae7fe-488">acos</span><span class="sxs-lookup"><span data-stu-id="ae7fe-488">acos</span></span> |<span data-ttu-id="ae7fe-489">값 또는 함수의 아크코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="ae7fe-490">and</span><span class="sxs-lookup"><span data-stu-id="ae7fe-490">and</span></span> |<span data-ttu-id="ae7fe-491">모든 피연산자 tootrue를 평가 하는 경우에 true 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-491">Returns a value of true if and only if all of its operands evaluate tootrue.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="ae7fe-492">asin</span><span class="sxs-lookup"><span data-stu-id="ae7fe-492">asin</span></span> |<span data-ttu-id="ae7fe-493">값 또는 함수의 아크사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="ae7fe-494">atan</span><span class="sxs-lookup"><span data-stu-id="ae7fe-494">atan</span></span> |<span data-ttu-id="ae7fe-495">값 또는 함수의 아크탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="ae7fe-496">atan2</span><span class="sxs-lookup"><span data-stu-id="ae7fe-496">atan2</span></span> |<span data-ttu-id="ae7fe-497">x, y toopolar 좌표 hello 사각형 좌표로의 hello 변환으로 인해 발생 하는 hello 각도 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-497">Returns hello angle resulting from hello conversion of hello rectangular coordinates x,y toopolar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="ae7fe-498">cbrt</span><span class="sxs-lookup"><span data-stu-id="ae7fe-498">cbrt</span></span> |<span data-ttu-id="ae7fe-499">세제곱근입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="ae7fe-500">ceil</span><span class="sxs-lookup"><span data-stu-id="ae7fe-500">ceil</span></span> |<span data-ttu-id="ae7fe-501">Tooan 정수를 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-501">Rounds up tooan integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="ae7fe-502">`ceil(5.6)` 6을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="ae7fe-503">cos</span><span class="sxs-lookup"><span data-stu-id="ae7fe-503">cos</span></span> |<span data-ttu-id="ae7fe-504">각도의 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="ae7fe-505">cosh</span><span class="sxs-lookup"><span data-stu-id="ae7fe-505">cosh</span></span> |<span data-ttu-id="ae7fe-506">쌍곡선 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="ae7fe-507">def</span><span class="sxs-lookup"><span data-stu-id="ae7fe-507">def</span></span> |<span data-ttu-id="ae7fe-508">기본값에 대한 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-508">Abbreviation for default.</span></span> <span data-ttu-id="ae7fe-509">반환 hello 필드 "field"의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-509">Returns hello value of field "field".</span></span> <span data-ttu-id="ae7fe-510">Hello 필드가 없는 경우 지정 된 hello 기본값을 반환 하 고 hello 첫 번째 값이 생성 위치: `exists()==true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-510">If hello field does not exist, returns hello default value specified and yields hello first value where: `exists()==true`.</span></span> |<span data-ttu-id="ae7fe-511">`def(rating,5)`</span><span class="sxs-lookup"><span data-stu-id="ae7fe-511">`def(rating,5)`.</span></span> <span data-ttu-id="ae7fe-512">이 def() 함수 hello 등급을 반환 하거나 등급이 지정 되지 않은 hello 문서에 지정 된 경우 5를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-512">This def() function returns hello rating, or if no rating is specified in hello document, returns 5.</span></span> <br> <span data-ttu-id="ae7fe-513">`def(myfield, 1.0)`너무`if(exists(myfield),myfield,1.0)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-513">`def(myfield, 1.0)` is equivalent too`if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="ae7fe-514">deg</span><span class="sxs-lookup"><span data-stu-id="ae7fe-514">deg</span></span> |<span data-ttu-id="ae7fe-515">Toodegrees 라디안으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-515">Converts radians toodegrees.</span></span> |`deg(x)` |
| <span data-ttu-id="ae7fe-516">div</span><span class="sxs-lookup"><span data-stu-id="ae7fe-516">div</span></span> |<span data-ttu-id="ae7fe-517">`div(x,y)` 는 x를 y로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="ae7fe-518">dist</span><span class="sxs-lookup"><span data-stu-id="ae7fe-518">dist</span></span> |<span data-ttu-id="ae7fe-519">두 벡터 사이의 (포인트) n 차원 공간의 hello 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-519">Returns hello distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="ae7fe-520">Hello 전원 및 둘 이상의 ValueSource 인스턴스를 사용 하 고 hello 두 벡터 사이의 hello 거리를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-520">Takes in hello power, plus two or more, ValueSource instances, and calculates hello distances between hello two vectors.</span></span> <span data-ttu-id="ae7fe-521">각 ValueSource는 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="ae7fe-522">전달 되는 ValueSource 인스턴스의 수는 짝수 이어야 하며 hello 메서드에서 처음 절반은 hello는 hello 첫 번째 벡터를 나타내고 hello 두 번째 절반 hello 두 번째 벡터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-522">There must be an even number of ValueSource instances passed in, and hello method assumes that hello first half represent hello first vector and hello second half represent hello second vector.</span></span> |<span data-ttu-id="ae7fe-523">`dist(2, x, y, 0, 0)`Hello (0, 0) 사이의 유 클 리 디안 거리를 계산 및 (x, y) 각 문서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-523">`dist(2, x, y, 0, 0)` Calculates hello Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="ae7fe-524">`dist(1, x, y, 0, 0)`계산 (0, 0) 사이의 맨해튼 (택시) 거리 hello 및 (x, y) 각 문서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-524">`dist(1, x, y, 0, 0)` Calculates hello Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="ae7fe-525">`dist(2,,x,y,z,0,0,0)` 각 문서에 대해 (0,0,0)과 (x,y,z) 사이의 유클리드 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="ae7fe-526">`dist(1,x,y,z,e,f,g)` (x,y,z)와 (e,f,g) 사이의 맨해턴 거리이며 각 문자는 필드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="ae7fe-527">exists</span><span class="sxs-lookup"><span data-stu-id="ae7fe-527">exists</span></span> |<span data-ttu-id="ae7fe-528">Hello 필드의 멤버가 있는 경우 TRUE 반환 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-528">Returns TRUE if any member of hello field exists.</span></span> |<span data-ttu-id="ae7fe-529">`exists(author)`Hello "author" 필드에 값이 있는 임의 문서에 대 한 TRUE를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-529">`exists(author)` Returns TRUE for any document that has a value in hello "author" field.</span></span><br><span data-ttu-id="ae7fe-530">`exists(query(price:5.00))` "price"가 "5.00"과 일치할 경우 TRUE를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="ae7fe-531">exp</span><span class="sxs-lookup"><span data-stu-id="ae7fe-531">exp</span></span> |<span data-ttu-id="ae7fe-532">발생 한 toopower 반환 오일러의 수 x.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-532">Returns Euler's number raised toopower x.</span></span> |`exp(x)` |
| <span data-ttu-id="ae7fe-533">floor</span><span class="sxs-lookup"><span data-stu-id="ae7fe-533">floor</span></span> |<span data-ttu-id="ae7fe-534">Tooan 정수로 내림 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-534">Rounds down tooan integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="ae7fe-535">`floor(5.6)` 5를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="ae7fe-536">hypo</span><span class="sxs-lookup"><span data-stu-id="ae7fe-536">hypo</span></span> |<span data-ttu-id="ae7fe-537">중간 오버플로 또는 언더플로 없이 sqrt(sum(pow(x,2),pow(y,2)))를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="ae7fe-538">if</span><span class="sxs-lookup"><span data-stu-id="ae7fe-538">if</span></span> |<span data-ttu-id="ae7fe-539">조건부 함수 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-539">Enables conditional function queries.</span></span> <span data-ttu-id="ae7fe-540">`if(test,value1,value2)`, 테스트 되었거나 tooa 논리 값 또는 논리적 값 (TRUE 또는 FALSE)을 반환 하는 식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-540">In `if(test,value1,value2)`, test is or refers tooa logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="ae7fe-541">`value1`hello 값 함수에서 반환 hello 테스트가 TRUE를 나타낼 경우.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-541">`value1` is hello value returned by hello function if test yields TRUE.</span></span> <span data-ttu-id="ae7fe-542">`value2`hello 값 함수에서 반환 hello 테스트가 FALSE를 나타낼 경우.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-542">`value2` is hello value returned by hello function if test yields FALSE.</span></span> <span data-ttu-id="ae7fe-543">식은 부울 값을 출력하는 함수일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="ae7fe-544">또한 숫자 값을 반환하는 함수일 수도 있으며, 이 경우 값 0은 FALSE 또는 반환 문자열로 해석되며, 후자의 경우 빈 문자열은 FALSE로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="ae7fe-545">`if(termfreq(cat,'electronics'),popularity,42)`이 함수는 hello hello cat 필드에 표시 된 "electronics" 라는 용어가 포함 된 경우 각 문서 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document toosee if it contains hello term "electronics" in hello cat field.</span></span> <span data-ttu-id="ae7fe-546">다음 hello지 않습니다, hello popularity 필드의 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-546">If it does, then hello value of hello popularity field is returned.</span></span> <span data-ttu-id="ae7fe-547">그렇지 않으면 hello 값 42가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-547">Otherwise, hello value of 42 is returned.</span></span> |
| <span data-ttu-id="ae7fe-548">linear</span><span class="sxs-lookup"><span data-stu-id="ae7fe-548">linear</span></span> |<span data-ttu-id="ae7fe-549">`m*x+c`을 구현하며, 여기서 m과 c는 상수이고 x는 임의의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="ae7fe-550">이것은 너무`sum(product(m,x),c)`, 하지만 단일 함수로 구현 되므로 약간 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-550">This is equivalent too`sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="ae7fe-551">`linear(x,m,c) linear(x,2,4)` `2*x+4`를 반환합니다</span><span class="sxs-lookup"><span data-stu-id="ae7fe-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="ae7fe-552">ln</span><span class="sxs-lookup"><span data-stu-id="ae7fe-552">ln</span></span> |<span data-ttu-id="ae7fe-553">반환 hello 자연 로그의 hello 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-553">Returns hello natural log of hello specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="ae7fe-554">로그</span><span class="sxs-lookup"><span data-stu-id="ae7fe-554">log</span></span> |<span data-ttu-id="ae7fe-555">반환 hello 로그 밑수 10을 hello 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-555">Returns hello log base 10 of hello specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="ae7fe-556">map</span><span class="sxs-lookup"><span data-stu-id="ae7fe-556">map</span></span> |<span data-ttu-id="ae7fe-557">Min 및 max (포함) toohello 지정 된 대상에 속하는 입력된 함수 x의 값을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-557">Maps any values of an input function x that fall within min and max, inclusive toohello specified target.</span></span> <span data-ttu-id="ae7fe-558">hello 인수 min 및 max는 상수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-558">hello arguments min and max must be constants.</span></span> <span data-ttu-id="ae7fe-559">상수 또는 함수 hello target 및 기본 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-559">hello arguments target and default can be constants or functions.</span></span> <span data-ttu-id="ae7fe-560">X의 hello 값은 min과 max 사이의 속하지 않을, 하는 경우 다음 x의 hello 값 중 하나가 반환 되는지, 아니면 5 번째 인수로 지정 된 경우 기본값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-560">If hello value of x does not fall between min and max, then either hello value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="ae7fe-561">`map(x,min,max,target) map(x,0,0,1)`값 0 too1로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 too1.</span></span> <span data-ttu-id="ae7fe-562">이 함수는 기본값 0을 처리하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="ae7fe-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)`0부터 100 too1 및 모든 다른 값 너무-1 사이의 모든 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 too1, and all other values too-1.</span></span><br>  <span data-ttu-id="ae7fe-564">`map(x,0,100,sum(x,599),docfreq(text,solr))`0과 100 toox 사이의 모든 값 + 599 및 hello 용어의 'solr' hello 필드 텍스트에 있는 다른 모든 값 toofrequency 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 toox+599, and all other values toofrequency of hello term 'solr' in hello field text.</span></span> |
| <span data-ttu-id="ae7fe-565">max</span><span class="sxs-lookup"><span data-stu-id="ae7fe-565">max</span></span> |<span data-ttu-id="ae7fe-566">반환 hello 다중 중첩 된 함수 또는 상수 인수로 지정 되는 최대 숫자 값: `max(x,y,...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-566">Returns hello maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="ae7fe-567">max 함수 hello "bottoming" 다른 함수에 대 한 유용할 수 있습니다 또는 일부 필드는 상수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-567">hello max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="ae7fe-568">사용 하 여 hello `field(myfield,max)` 구문 hello 단일 다중값된 필드의 최대 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-568">Use hello `field(myfield,max)` syntax for selecting hello maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="ae7fe-569">Min</span><span class="sxs-lookup"><span data-stu-id="ae7fe-569">min</span></span> |<span data-ttu-id="ae7fe-570">반환 값 여러 개의 중첩 된 인수로 지정 된 상수 함수의 hello: `min(x,y,...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-570">Returns hello minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="ae7fe-571">hello min 함수는 상수를 사용 하는 함수에 "상한"을 제공 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-571">hello min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="ae7fe-572">사용 하 여 hello `field(myfield,min)` hello 단일 다중값된 필드의 최소 값을 선택 하기 위한 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-572">Use hello `field(myfield,min)` syntax for selecting hello minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="ae7fe-573">mod</span><span class="sxs-lookup"><span data-stu-id="ae7fe-573">mod</span></span> |<span data-ttu-id="ae7fe-574">Hello 함수 y로 hello 함수 x의 hello 모듈러스를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-574">Computes hello modulus of hello function x by hello function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="ae7fe-575">ms</span><span class="sxs-lookup"><span data-stu-id="ae7fe-575">ms</span></span> |<span data-ttu-id="ae7fe-576">인수간 차이를 밀리초 단위로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="ae7fe-577">상대 toohello Unix 또는 POSIX epoch, UTC 1970 년 1 월 1 일 자정은 하는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-577">Dates are relative toohello Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="ae7fe-578">인수는 날짜나 NOW hello의 이름은 인덱싱된 TrieDateField 또는 날짜 상수는 날짜에 따라 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-578">Arguments may be hello name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="ae7fe-579">`ms()`너무`ms(NOW)`, hello epoch 이후의 시간 (밀리초)의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-579">`ms()` is equivalent too`ms(NOW)`, number of milliseconds since hello epoch.</span></span> <span data-ttu-id="ae7fe-580">`ms(a)`hello 인수를 나타내는 hello epoch 이후의 시간 (밀리초) hello 번호를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-580">`ms(a)` returns hello number of milliseconds since hello epoch that hello argument represents.</span></span> <span data-ttu-id="ae7fe-581">`ms(a,b)`b hello 기간 (밀리초) 반환 하기 전에 발생 a, 즉 `a - b`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-581">`ms(a,b)` returns hello number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="ae7fe-582">not</span><span class="sxs-lookup"><span data-stu-id="ae7fe-582">not</span></span> |<span data-ttu-id="ae7fe-583">hello의 논리적으로 부정 hello 값 래핑된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-583">hello logically negated value of hello wrapped function.</span></span> |<span data-ttu-id="ae7fe-584">`not(exists(author))` `exists(author)`가 false일 경우에만 TRUE입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="ae7fe-585">또는</span><span class="sxs-lookup"><span data-stu-id="ae7fe-585">or</span></span> |<span data-ttu-id="ae7fe-586">논리적 분리.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-586">A logical disjunction.</span></span> |<span data-ttu-id="ae7fe-587">`or(value1,value2)` value1 또는 value2가 true일 경우에만 TRUE입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="ae7fe-588">pow</span><span class="sxs-lookup"><span data-stu-id="ae7fe-588">pow</span></span> |<span data-ttu-id="ae7fe-589">발생 hello 지정 지정 된 기본 toohello 전원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-589">Raises hello specified base toohello specified power.</span></span> <span data-ttu-id="ae7fe-590">`pow(x,y)`y의 거듭제곱을 x toohello를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-590">`pow(x,y)` raises x toohello power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="ae7fe-591">`pow(x,0.5)`sqrt와 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-591">`pow(x,0.5)` hello same as sqrt.</span></span> |
| <span data-ttu-id="ae7fe-592">product</span><span class="sxs-lookup"><span data-stu-id="ae7fe-592">product</span></span> |<span data-ttu-id="ae7fe-593">반환 hello 제품의 다중 값 또는 함수의 쉼표로 구분 된 목록에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-593">Returns hello product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="ae7fe-594">`mul(...)` 도 이 함수의 별칭으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="ae7fe-595">recip</span><span class="sxs-lookup"><span data-stu-id="ae7fe-595">recip</span></span> |<span data-ttu-id="ae7fe-596">`recip(x,m,a,b)`를 구현하는 `a/(m*x+b)`를 사용하는 역함수를 수행합니다. 여기서 m, a 및 b는 상수이며 x는 임의의 복소수 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="ae7fe-597">a와 b가 동일하고 x>=0일 경우 이 함수의 최대값 1은 x가 증가함에 따라 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="ae7fe-598">Hello 값이 늘어나는 고 hello 함수 전체 tooa의 이동에서 b 함께 결과 일반적인 방법 hello 곡선의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-598">Increasing hello value of a and b together results in a movement of hello entire function tooa flatter part of hello curve.</span></span> <span data-ttu-id="ae7fe-599">이러한 속성으로 인해 x가 `rord(datefield)`일 때 더 많은 최근 문서를 출력하는 데 적합한 함수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="ae7fe-600">rad</span><span class="sxs-lookup"><span data-stu-id="ae7fe-600">rad</span></span> |<span data-ttu-id="ae7fe-601">도 tooradians를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-601">Converts degrees tooradians.</span></span> |`rad(x)` |
| <span data-ttu-id="ae7fe-602">rint</span><span class="sxs-lookup"><span data-stu-id="ae7fe-602">rint</span></span> |<span data-ttu-id="ae7fe-603">가장 근접 한 정수로 반올림 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-603">Rounds toohello nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="ae7fe-604">`rint(5.6)` 6을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="ae7fe-605">sin</span><span class="sxs-lookup"><span data-stu-id="ae7fe-605">sin</span></span> |<span data-ttu-id="ae7fe-606">각도의 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="ae7fe-607">sinh</span><span class="sxs-lookup"><span data-stu-id="ae7fe-607">sinh</span></span> |<span data-ttu-id="ae7fe-608">각도의 쌍곡선 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="ae7fe-609">크기 조정</span><span class="sxs-lookup"><span data-stu-id="ae7fe-609">scale</span></span> |<span data-ttu-id="ae7fe-610">Hello 함수 x의 값 크기 조정, hello 사이 지정 된 minTarget와 maxTarget (포함).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-610">Scales values of hello function x, such that they fall between hello specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="ae7fe-611">현재 구현 hello hello 올바른 소수 자릿수를 선택할 수 있도록 모든 hello 함수 값 tooobtain hello min 및 max 트래버스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-611">hello current implementation traverses all of hello function values tooobtain hello min and max, so it can pick hello correct scale.</span></span> <span data-ttu-id="ae7fe-612">문서를 삭제 하는 경우 현재 구현 hello 구분할 수 없습니다 또는 값이 없는 문서.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-612">hello current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="ae7fe-613">그러한 경우는 0.0 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="ae7fe-614">이 값은 일반적으로 0.0 보다 큰 경우 하나는 여전히 결국 0.0에서 min 값 toomap hello으로 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as hello min value toomap from.</span></span> <span data-ttu-id="ae7fe-615">이러한 경우 적절 한 `map()` 함수 다음 그림과 같이 hello 실제 범위 내에 해결 방법 toochange 0.0 tooa 값으로 사용 될 수 있습니다.`scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="ae7fe-615">In these cases, an appropriate `map()` function could be used as a workaround toochange 0.0 tooa value in hello real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="ae7fe-616">`scale(x,1,2)`1과 2 (포함) 사이의 모든 값이 되도록 눈금 x의 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-616">`scale(x,1,2)` Scales hello values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="ae7fe-617">sqrt</span><span class="sxs-lookup"><span data-stu-id="ae7fe-617">sqrt</span></span> |<span data-ttu-id="ae7fe-618">Hello의 반환 hello 제곱근 값 또는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-618">Returns hello square root of hello specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="ae7fe-619">strdist</span><span class="sxs-lookup"><span data-stu-id="ae7fe-619">strdist</span></span> |<span data-ttu-id="ae7fe-620">두 문자열 사이의 hello 거리를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-620">Calculates hello distance between two strings.</span></span> <span data-ttu-id="ae7fe-621">Hello Lucene 맞춤법 검사기 StringDistance 인터페이스를 사용 하 고 해당 패키지에서 사용할 수 있는 hello 구현의 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-621">Uses hello Lucene spell checker StringDistance interface, and supports all of hello implementations available in that package.</span></span> <span data-ttu-id="ae7fe-622">또한 응용 프로그램 tooplug을 로드 기능을 통해 자기 자신, Solr의 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-622">Also allows applications tooplug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="ae7fe-623">strdist는 `(string1, string2, distance measure)`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="ae7fe-624">거리 측정에 가능한 값은 </span><span class="sxs-lookup"><span data-stu-id="ae7fe-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="ae7fe-625">jw: Jaro-Winkler</span><span class="sxs-lookup"><span data-stu-id="ae7fe-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="ae7fe-626">edit: Levenstein 또는 편집 거리</span><span class="sxs-lookup"><span data-stu-id="ae7fe-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="ae7fe-627">ngram: NGramDistance, hello를 지정 하는 경우 선택적으로 전달할 수 ngram 크기도 제공할 hello 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-627">ngram: hello NGramDistance, if specified, can optionally pass in hello ngram size too.</span></span> <span data-ttu-id="ae7fe-628">기본값은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-628">Default is 2.</span></span></li><li><span data-ttu-id="ae7fe-629">FQN: 구현 된 StringDistance 인터페이스 hello에 대 한 이름을 클래스를 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-629">FQN: Fully Qualified class Name for an implementation of hello StringDistance interface.</span></span> <span data-ttu-id="ae7fe-630">인수가 없는 생성자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="ae7fe-631">sub</span><span class="sxs-lookup"><span data-stu-id="ae7fe-631">sub</span></span> |<span data-ttu-id="ae7fe-632">`sub(x,y)`에서 x-y를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="ae7fe-633">sum</span><span class="sxs-lookup"><span data-stu-id="ae7fe-633">sum</span></span> |<span data-ttu-id="ae7fe-634">반환 hello 다중 값 또는 함수의 쉼표로 구분 된 목록에 지정 된의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-634">Returns hello sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="ae7fe-635">`add(...)` 도 이 함수의 별칭으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="ae7fe-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="ae7fe-636">termfreq</span></span> |<span data-ttu-id="ae7fe-637">Hello hello 용어가 나타나는 횟수 해당 문서에 대 한 hello 필드에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-637">Returns hello number of times hello term appears in hello field for that document.</span></span> |<span data-ttu-id="ae7fe-638">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="ae7fe-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="ae7fe-639">tan</span><span class="sxs-lookup"><span data-stu-id="ae7fe-639">tan</span></span> |<span data-ttu-id="ae7fe-640">각도의 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="ae7fe-641">tanh</span><span class="sxs-lookup"><span data-stu-id="ae7fe-641">tanh</span></span> |<span data-ttu-id="ae7fe-642">각도의 쌍곡선 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="ae7fe-643">검색 필드 및 패싯 참조</span><span class="sxs-lookup"><span data-stu-id="ae7fe-643">Search field and facet reference</span></span>
<span data-ttu-id="ae7fe-644">로그 검색 toofind 데이터를 사용할 때 결과가 다양 한 필드 및 패싯을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-644">When you use Log Search toofind data, results display various field and facets.</span></span> <span data-ttu-id="ae7fe-645">Hello 정보 중 일부는 매우 자세히 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-645">Some of hello information might not appear very descriptive.</span></span> <span data-ttu-id="ae7fe-646">다음 정보 toohelp hello 결과 이해 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-646">Use hello following information toohelp you understand hello results.</span></span>

| <span data-ttu-id="ae7fe-647">필드</span><span class="sxs-lookup"><span data-stu-id="ae7fe-647">Field</span></span> | <span data-ttu-id="ae7fe-648">검색 유형</span><span class="sxs-lookup"><span data-stu-id="ae7fe-648">Search type</span></span> | <span data-ttu-id="ae7fe-649">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae7fe-650">TenantId</span><span class="sxs-lookup"><span data-stu-id="ae7fe-650">TenantId</span></span> |<span data-ttu-id="ae7fe-651">모두</span><span class="sxs-lookup"><span data-stu-id="ae7fe-651">All</span></span> |<span data-ttu-id="ae7fe-652">Toopartition 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-652">Used toopartition data.</span></span> |
| <span data-ttu-id="ae7fe-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ae7fe-653">TimeGenerated</span></span> |<span data-ttu-id="ae7fe-654">모두</span><span class="sxs-lookup"><span data-stu-id="ae7fe-654">All</span></span> |<span data-ttu-id="ae7fe-655">Toodrive hello 타임 라인, timeselectors입니다 (검색 및 다른 화면)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-655">Used toodrive hello timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="ae7fe-656">데이터의 hello 일부가 (일반적으로 hello 에이전트)에서 생성 된 때를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-656">It represents when hello piece of data was generated (typically on hello agent).</span></span> <span data-ttu-id="ae7fe-657">ISO 형식으로 표현 되 hello 시간이 며 항상 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-657">hello time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="ae7fe-658">기존 계측 (즉, 로그의 이벤트)를 기반으로 하는 형식의 hello 경우이 일반적으로 hello 해당 hello 로그 항목/라인/레코드가 기록 된 실제 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-658">In hello case of types that are based on existing instrumentation (that is, events in a log), this is typically hello real time that hello log entry/line/record was logged.</span></span> <span data-ttu-id="ae7fe-659">일부 hello에 대 한 다른 형식 (예를 들어 권장 사항 또는 경고) hello 클라우드 또는 관리 팩을 통해 생성 되는 서로 다른 무엇 인가 시간 나타냅니다 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-659">For some of hello other types that are produced either via management packs or in hello cloud (for example, recommendations or alerts), hello time represents something different.</span></span> <span data-ttu-id="ae7fe-660">이 새 데이터 조각 일종의 구성 스냅숏 사용 하 여 수집 된 또는 권장 사항/경고가 그에 따라 생성 된 경우 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-660">This is hello time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="ae7fe-661">EventID</span><span class="sxs-lookup"><span data-stu-id="ae7fe-661">EventID</span></span> |<span data-ttu-id="ae7fe-662">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-662">Event</span></span> |<span data-ttu-id="ae7fe-663">Hello Windows 이벤트 로그에서 EventID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-663">EventID in hello Windows event log.</span></span> |
| <span data-ttu-id="ae7fe-664">EventLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-664">EventLog</span></span> |<span data-ttu-id="ae7fe-665">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-665">Event</span></span> |<span data-ttu-id="ae7fe-666">이벤트 로그에서 Windows hello 이벤트를 로그 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-666">Event log where hello event was logged by Windows.</span></span> |
| <span data-ttu-id="ae7fe-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-667">EventLevelName</span></span> |<span data-ttu-id="ae7fe-668">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-668">Event</span></span> |<span data-ttu-id="ae7fe-669">중요/경고/정보/성공</span><span class="sxs-lookup"><span data-stu-id="ae7fe-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="ae7fe-670">EventLevel</span><span class="sxs-lookup"><span data-stu-id="ae7fe-670">EventLevel</span></span> |<span data-ttu-id="ae7fe-671">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-671">Event</span></span> |<span data-ttu-id="ae7fe-672">중요/경고/정보/성공에 대한 숫자 값입니다(보다 쉽게/보다 읽기 쉬운 쿼리 대신 EventLevelName 사용).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="ae7fe-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ae7fe-673">SourceSystem</span></span> |<span data-ttu-id="ae7fe-674">모두</span><span class="sxs-lookup"><span data-stu-id="ae7fe-674">All</span></span> |<span data-ttu-id="ae7fe-675">Hello 데이터에서 제공 된 위치 (의 측면에서 모드 toohello 서비스 첨부).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-675">Where hello data comes from (in terms of attach mode toohello service).</span></span> <span data-ttu-id="ae7fe-676">예를 들어 Microsoft System Center Operations Manager 및 Azure Storage를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="ae7fe-677">ObjectName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-677">ObjectName</span></span> |<span data-ttu-id="ae7fe-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-678">PerfHourly</span></span> |<span data-ttu-id="ae7fe-679">Windows 성능 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-679">Windows performance object name.</span></span> |
| <span data-ttu-id="ae7fe-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-680">InstanceName</span></span> |<span data-ttu-id="ae7fe-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-681">PerfHourly</span></span> |<span data-ttu-id="ae7fe-682">Windows 성능 카운터 인스턴스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="ae7fe-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-683">CounteName</span></span> |<span data-ttu-id="ae7fe-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-684">PerfHourly</span></span> |<span data-ttu-id="ae7fe-685">Windows 성능 카운터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="ae7fe-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-686">ObjectDisplayName</span></span> |<span data-ttu-id="ae7fe-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="ae7fe-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="ae7fe-688">Operations Manager에서 성능 수집 규칙이 대상으로 하는 hello 개체의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-688">Display name of hello object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="ae7fe-689">또한 Operational Insights에서 검색 되는 hello 개체의 표시 이름을 hello 수 또는 어떤 hello에 대 한 경고가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-689">Could also be hello display name of hello object discovered by Operational Insights, or against which hello alert was generated.</span></span> |
| <span data-ttu-id="ae7fe-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-690">RootObjectName</span></span> |<span data-ttu-id="ae7fe-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="ae7fe-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="ae7fe-692">Hello 부모 (이중 호스팅 관계)에서 Operations Manager에서 성능 수집 규칙이 대상으로 하는 hello 개체의 hello 부모의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-692">Display name of hello parent of hello parent (in a double hosting relationship) of hello object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="ae7fe-693">또한 Operational Insights에서 검색 되는 hello 개체의 표시 이름을 hello 수 또는 어떤 hello에 대 한 경고가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-693">Could also be hello display name of hello object discovered by Operational Insights, or against which hello alert was generated.</span></span> |
| <span data-ttu-id="ae7fe-694">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7fe-694">Computer</span></span> |<span data-ttu-id="ae7fe-695">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-695">Most types</span></span> |<span data-ttu-id="ae7fe-696">Hello 데이터가 속한 컴퓨터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-696">Computer name that hello data belongs to.</span></span> |
| <span data-ttu-id="ae7fe-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-697">DeviceName</span></span> |<span data-ttu-id="ae7fe-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-698">ProtectionStatus</span></span> |<span data-ttu-id="ae7fe-699">컴퓨터 이름 hello 데이터가 너무 속한 ("Computer"와 같음).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-699">Computer name hello data belongs too(same as "Computer").</span></span> |
| <span data-ttu-id="ae7fe-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="ae7fe-700">DetectionId</span></span> |<span data-ttu-id="ae7fe-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="ae7fe-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="ae7fe-702">ThreatStatusRank</span></span> |<span data-ttu-id="ae7fe-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-703">ProtectionStatus</span></span> |<span data-ttu-id="ae7fe-704">위협 상태 순위는 hello 위협 상태의 숫자 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-704">Threat status rank is a numerical representation of hello threat status.</span></span> <span data-ttu-id="ae7fe-705">비슷한 tooHTTP 응답 코드 hello 순위 hello 번호 사이 간격이 발생 했습니다 (위협이 아닌 이유은 150 및 하지 100 또는 0), 방 tooadd는 새 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-705">Similar tooHTTP response codes, hello ranking has gaps between hello numbers (which is why no threats is 150 and not 100 or 0), leaving room tooadd new states.</span></span> <span data-ttu-id="ae7fe-706">위협 상태 및 보호 상태 롤업을 hello 의도 tooshow hello 있었던 최악의 상태를 컴퓨터 hello 된 동안에 hello 특정 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-706">For a rollup of threat status and protection status, hello intention is tooshow hello worst state that hello computer has been in during hello selected time period.</span></span> <span data-ttu-id="ae7fe-707">hello 숫자 순위 hello 다양 한 상태의 번호가 높은 hello hello 레코드를 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-707">hello numbers rank hello different states, so you can look for hello record with hello highest number.</span></span> |
| <span data-ttu-id="ae7fe-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-708">ThreatStatus</span></span> |<span data-ttu-id="ae7fe-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-709">ProtectionStatus</span></span> |<span data-ttu-id="ae7fe-710">ThreatStatus에 대한 설명이며, ThreatStatusRank와 1:1 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="ae7fe-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="ae7fe-711">TypeofProtection</span></span> |<span data-ttu-id="ae7fe-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-712">ProtectionStatus</span></span> |<span data-ttu-id="ae7fe-713">Hello 컴퓨터에서 검색 된 맬웨어 방지 제품: 없음, Microsoft 맬웨어 제거 도구, Forefront, 등에.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-713">Antimalware product that is detected in hello computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="ae7fe-714">ScanDate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-714">ScanDate</span></span> |<span data-ttu-id="ae7fe-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="ae7fe-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="ae7fe-716">SourceHealthServiceId</span></span> |<span data-ttu-id="ae7fe-717">ProtectionStatus, RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-718">이 컴퓨터의 에이전트에 대한 HealthService ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="ae7fe-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="ae7fe-719">HealthServiceId</span></span> |<span data-ttu-id="ae7fe-720">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-720">Most types</span></span> |<span data-ttu-id="ae7fe-721">이 컴퓨터의 에이전트에 대한 HealthService ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="ae7fe-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-722">ManagementGroupName</span></span> |<span data-ttu-id="ae7fe-723">대부분의 형식</span><span class="sxs-lookup"><span data-stu-id="ae7fe-723">Most types</span></span> |<span data-ttu-id="ae7fe-724">Operations Manager에 연결된 에이전트용 관리 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="ae7fe-725">그렇지 않은 경우 null/blank입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="ae7fe-726">ObjectType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-726">ObjectType</span></span> |<span data-ttu-id="ae7fe-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="ae7fe-727">ConfigurationObject</span></span> |<span data-ttu-id="ae7fe-728">Log Analytics 구성 평가에서 검색된 개체의 형식(Operations Manager 관리 팩의 형식/클래스와 동일)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="ae7fe-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="ae7fe-729">UpdateTitle</span></span> |<span data-ttu-id="ae7fe-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-730">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-731">설치 된 발견 된 hello 업데이트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-731">Name of hello update that was found not installed.</span></span> |
| <span data-ttu-id="ae7fe-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-732">PublishDate</span></span> |<span data-ttu-id="ae7fe-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-733">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-734">Hello 업데이트 Microsoft 업데이트에 게시 된 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-734">When hello update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="ae7fe-735">서버</span><span class="sxs-lookup"><span data-stu-id="ae7fe-735">Server</span></span> |<span data-ttu-id="ae7fe-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-736">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-737">컴퓨터 이름 hello 데이터가 너무 속한 ("Computer"와 같음).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-737">Computer name hello data belongs too(same as "Computer").</span></span> |
| <span data-ttu-id="ae7fe-738">제품</span><span class="sxs-lookup"><span data-stu-id="ae7fe-738">Product</span></span> |<span data-ttu-id="ae7fe-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-739">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-740">Hello 업데이트 제품에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-740">Product that hello update applies to.</span></span> |
| <span data-ttu-id="ae7fe-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="ae7fe-741">UpdateClassification</span></span> |<span data-ttu-id="ae7fe-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-742">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-743">업데이트 유형(예를 들어 업데이트 롤업 또는 서비스 팩)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="ae7fe-744">KBID</span><span class="sxs-lookup"><span data-stu-id="ae7fe-744">KBID</span></span> |<span data-ttu-id="ae7fe-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-745">RequiredUpdate</span></span> |<span data-ttu-id="ae7fe-746">모범 사례 또는 업데이트를 설명하는 KB 문서 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="ae7fe-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-747">WorkflowName</span></span> |<span data-ttu-id="ae7fe-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-748">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-749">Hello 규칙 또는 hello 경고를 생성 하는 모니터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-749">Name of hello rule or monitor that produced hello alert.</span></span> |
| <span data-ttu-id="ae7fe-750">심각도</span><span class="sxs-lookup"><span data-stu-id="ae7fe-750">Severity</span></span> |<span data-ttu-id="ae7fe-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-751">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-752">Hello 경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-752">Severity of hello alert.</span></span> |
| <span data-ttu-id="ae7fe-753">우선 순위</span><span class="sxs-lookup"><span data-stu-id="ae7fe-753">Priority</span></span> |<span data-ttu-id="ae7fe-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-754">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-755">Hello 경고의 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-755">Priority of hello alert.</span></span> |
| <span data-ttu-id="ae7fe-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-756">IsMonitorAlert</span></span> |<span data-ttu-id="ae7fe-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-757">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-758">이 경고는 모니터(true) 또는 규칙(false)에 의해 생성되었습니까?</span><span class="sxs-lookup"><span data-stu-id="ae7fe-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="ae7fe-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="ae7fe-759">AlertParameters</span></span> |<span data-ttu-id="ae7fe-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-760">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-761">Hello 로그 분석 경고의 hello 매개 변수를 사용 하 여 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-761">XML with hello parameters of hello Log Analytics alert.</span></span> |
| <span data-ttu-id="ae7fe-762">Context</span><span class="sxs-lookup"><span data-stu-id="ae7fe-762">Context</span></span> |<span data-ttu-id="ae7fe-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-763">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-764">Hello 로그 분석 경고의 hello 컨텍스트를 사용 하 여 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-764">XML with hello context of hello Log Analytics alert.</span></span> |
| <span data-ttu-id="ae7fe-765">워크로드</span><span class="sxs-lookup"><span data-stu-id="ae7fe-765">Workload</span></span> |<span data-ttu-id="ae7fe-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-766">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-767">경고 hello는 기술 또는 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-767">Technology or workload that hello alert refers to.</span></span> |
| <span data-ttu-id="ae7fe-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="ae7fe-768">AdvisorWorkload</span></span> |<span data-ttu-id="ae7fe-769">권장 사항</span><span class="sxs-lookup"><span data-stu-id="ae7fe-769">Recommendation</span></span> |<span data-ttu-id="ae7fe-770">권장 사항 hello는 기술 또는 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-770">Technology or workload that hello recommendation refers to.</span></span> |
| <span data-ttu-id="ae7fe-771">설명</span><span class="sxs-lookup"><span data-stu-id="ae7fe-771">Description</span></span> |<span data-ttu-id="ae7fe-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="ae7fe-772">ConfigurationAlert</span></span> |<span data-ttu-id="ae7fe-773">경고 설명(간략)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-773">Alert description (short).</span></span> |
| <span data-ttu-id="ae7fe-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="ae7fe-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="ae7fe-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-775">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-776">날 (이 레코드의 상대 tooTimeGenerated)가이 에이전트에서 업데이트를 설치한 서버 업데이트 서비스 WSUS (Windows) 또는 Microsoft Update?</span><span class="sxs-lookup"><span data-stu-id="ae7fe-776">How many days ago (relative tooTimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="ae7fe-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="ae7fe-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="ae7fe-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-778">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-779">DaysSinceLastUpdate에 따라 컴퓨터가 WSUS/Microsoft Update에서 업데이트를 마지막 설치한 것이 얼마 전인지에 대한 시간 버킷의 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="ae7fe-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="ae7fe-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="ae7fe-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-781">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-782">자동 업데이트가 이 에이전트에서 활성화 또는 비활성화를 확인하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ae7fe-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="ae7fe-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="ae7fe-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="ae7fe-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-784">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-785">자동 업데이트 검사 집합 tooautomatically 다운로드 및 설치, 다운로드만 또는 확인만?</span><span class="sxs-lookup"><span data-stu-id="ae7fe-785">Is automatic update checking set tooautomatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="ae7fe-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="ae7fe-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="ae7fe-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-787">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-788">Hello Microsoft 업데이트 에이전트의 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-788">Version number of hello Microsoft Update agent.</span></span> |
| <span data-ttu-id="ae7fe-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="ae7fe-789">WSUSServer</span></span> |<span data-ttu-id="ae7fe-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-790">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-791">어떤 WSUS 서버가 이 업데이트 에이전트를 대상으로 합니까?</span><span class="sxs-lookup"><span data-stu-id="ae7fe-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="ae7fe-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="ae7fe-792">OSVersion</span></span> |<span data-ttu-id="ae7fe-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-793">UpdateAgent</span></span> |<span data-ttu-id="ae7fe-794">이 업데이트 에이전트에서 실행 중인 hello 운영 체제의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-794">Version of hello operating system this update agent is running on.</span></span> |
| <span data-ttu-id="ae7fe-795">이름</span><span class="sxs-lookup"><span data-stu-id="ae7fe-795">Name</span></span> |<span data-ttu-id="ae7fe-796">Recommendation, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="ae7fe-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="ae7fe-797">이름/제목 hello 권장 또는 로그 분석 구성 평가에서 hello 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-797">Name/title of hello recommendation, or name of hello property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="ae7fe-798">값</span><span class="sxs-lookup"><span data-stu-id="ae7fe-798">Value</span></span> |<span data-ttu-id="ae7fe-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="ae7fe-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="ae7fe-800">Log Analytics 구성 평가에서 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="ae7fe-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="ae7fe-801">KBLink</span></span> |<span data-ttu-id="ae7fe-802">권장 사항</span><span class="sxs-lookup"><span data-stu-id="ae7fe-802">Recommendation</span></span> |<span data-ttu-id="ae7fe-803">이 모범 사례 또는 업데이트를 설명 하는 URL toohello KB 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-803">URL toohello KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="ae7fe-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-804">RecommendationStatus</span></span> |<span data-ttu-id="ae7fe-805">권장 사항</span><span class="sxs-lookup"><span data-stu-id="ae7fe-805">Recommendation</span></span> |<span data-ttu-id="ae7fe-806">권장 사항을 레코드가 업데이트 되 고 방금 추가한 toohello 검색 인덱스를 가져올 몇 가지 유형 hello 가장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-806">Recommendations are among hello few types whose records get updated, not just added toohello search index.</span></span> <span data-ttu-id="ae7fe-807">로그 분석에 해결 된 것을 감지 했는지 hello 권장 구성을 액티브/열기 인지 또는이 상태가 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-807">This status changes whether hello recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="ae7fe-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="ae7fe-808">RenderedDescription</span></span> |<span data-ttu-id="ae7fe-809">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-809">Event</span></span> |<span data-ttu-id="ae7fe-810">Windows 이벤트의 렌더링된 설명(채워진 매개 변수와 재사용된 텍스트)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="ae7fe-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="ae7fe-811">ParameterXml</span></span> |<span data-ttu-id="ae7fe-812">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-812">Event</span></span> |<span data-ttu-id="ae7fe-813">Windows 이벤트 (이벤트 뷰어 처럼)의 데이터 섹션 hello에에서 hello 매개 변수를 사용 하 여 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-813">XML with hello parameters in hello data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="ae7fe-814">EventData</span><span class="sxs-lookup"><span data-stu-id="ae7fe-814">EventData</span></span> |<span data-ttu-id="ae7fe-815">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-815">Event</span></span> |<span data-ttu-id="ae7fe-816">Windows 이벤트 (이벤트 뷰어 처럼)의 hello 전체 데이터 섹션 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-816">XML with hello whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="ae7fe-817">원본</span><span class="sxs-lookup"><span data-stu-id="ae7fe-817">Source</span></span> |<span data-ttu-id="ae7fe-818">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-818">Event</span></span> |<span data-ttu-id="ae7fe-819">이벤트 로그 소스 hello 이벤트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-819">Event log source that generated hello event.</span></span> |
| <span data-ttu-id="ae7fe-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="ae7fe-820">EventCategory</span></span> |<span data-ttu-id="ae7fe-821">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-821">Event</span></span> |<span data-ttu-id="ae7fe-822">Hello Windows 이벤트 로그에서 직접 hello 이벤트의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-822">Category of hello event, directly from hello Windows event log.</span></span> |
| <span data-ttu-id="ae7fe-823">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ae7fe-823">UserName</span></span> |<span data-ttu-id="ae7fe-824">이벤트</span><span class="sxs-lookup"><span data-stu-id="ae7fe-824">Event</span></span> |<span data-ttu-id="ae7fe-825">Hello Windows 이벤트 (일반적으로 NT AUTHORITY\LOCALSYSTEM)의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-825">User name of hello Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="ae7fe-826">SampleValue</span><span class="sxs-lookup"><span data-stu-id="ae7fe-826">SampleValue</span></span> |<span data-ttu-id="ae7fe-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-827">PerfHourly</span></span> |<span data-ttu-id="ae7fe-828">성능 카운터의 시간별 집계 hello에 대 한 평균 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-828">Average value for hello hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="ae7fe-829">Min</span><span class="sxs-lookup"><span data-stu-id="ae7fe-829">Min</span></span> |<span data-ttu-id="ae7fe-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-830">PerfHourly</span></span> |<span data-ttu-id="ae7fe-831">Hello 성능 카운터 매시간 집계의 시간 간격의 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-831">Minimum value in hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="ae7fe-832">max</span><span class="sxs-lookup"><span data-stu-id="ae7fe-832">Max</span></span> |<span data-ttu-id="ae7fe-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-833">PerfHourly</span></span> |<span data-ttu-id="ae7fe-834">Hello 성능 카운터 매시간 집계의 시간 간격의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-834">Maximum value in hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="ae7fe-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="ae7fe-835">Percentile95</span></span> |<span data-ttu-id="ae7fe-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-836">PerfHourly</span></span> |<span data-ttu-id="ae7fe-837">hello 95 번째 백분위 수 값 hello 성능 카운터 매시간 집계의 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-837">hello 95th percentile value for hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="ae7fe-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="ae7fe-838">SampleCount</span></span> |<span data-ttu-id="ae7fe-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="ae7fe-839">PerfHourly</span></span> |<span data-ttu-id="ae7fe-840">얼마나 많은 원시 성능 카운터 샘플이 된 사용된 tooproduce이 매시간 집계 레코드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-840">How many raw performance counter samples were used tooproduce this hourly aggregate record.</span></span> |
| <span data-ttu-id="ae7fe-841">위협</span><span class="sxs-lookup"><span data-stu-id="ae7fe-841">Threat</span></span> |<span data-ttu-id="ae7fe-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-842">ProtectionStatus</span></span> |<span data-ttu-id="ae7fe-843">발견한 맬웨어의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-843">Name of malware found.</span></span> |
| <span data-ttu-id="ae7fe-844">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="ae7fe-844">StorageAccount</span></span> |<span data-ttu-id="ae7fe-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-845">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-846">Azure 저장소 계정 hello 로그에서 읽은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-846">Azure Storage account hello log was read from.</span></span> |
| <span data-ttu-id="ae7fe-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="ae7fe-847">AzureDeploymentID</span></span> |<span data-ttu-id="ae7fe-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-848">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-849">Hello 클라우드 서비스 hello 로그의 azure 배포 ID에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-849">Azure deployment ID of hello cloud service hello log belongs to.</span></span> |
| <span data-ttu-id="ae7fe-850">역할</span><span class="sxs-lookup"><span data-stu-id="ae7fe-850">Role</span></span> |<span data-ttu-id="ae7fe-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-851">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-852">Hello Azure 클라우드 서비스 hello 로그의 역할에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-852">Role of hello Azure cloud service hello log belongs to.</span></span> |
| <span data-ttu-id="ae7fe-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="ae7fe-853">RoleInstance</span></span> |<span data-ttu-id="ae7fe-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-854">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-855">Hello 로그 hello Azure 역할의 RoleInstance에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-855">RoleInstance of hello Azure role that hello log belongs to.</span></span> |
| <span data-ttu-id="ae7fe-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-856">sSiteName</span></span> |<span data-ttu-id="ae7fe-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-857">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-858">로그 hello 하는 IIS 웹 사이트가 속해 too(metabase notation); hello hello 원래 로그에서 s-sitename 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-858">IIS website that hello log belongs too(metabase notation); hello s-sitename field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-859">sComputerName</span></span> |<span data-ttu-id="ae7fe-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-860">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-861">hello hello 원래 로그에서 s-computername 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-861">hello s-computername field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-862">sIP</span><span class="sxs-lookup"><span data-stu-id="ae7fe-862">sIP</span></span> |<span data-ttu-id="ae7fe-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-863">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-864">서버 IP 주소 hello HTTP 요청이 지정 된입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-864">Server IP address hello HTTP request was addressed to.</span></span> <span data-ttu-id="ae7fe-865">hello hello 원래 로그에서 s-ip 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-865">hello s-ip field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="ae7fe-866">csMethod</span></span> |<span data-ttu-id="ae7fe-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-867">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-868">(예: GET/POST) HTTP 메서드를 hello 클라이언트가 hello HTTP 요청에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-868">HTTP method (for example, GET/POST) used by hello client in hello HTTP request.</span></span> <span data-ttu-id="ae7fe-869">hello 원래 로그에서 cs-method hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-869">hello cs-method in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-870">cIP</span><span class="sxs-lookup"><span data-stu-id="ae7fe-870">cIP</span></span> |<span data-ttu-id="ae7fe-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-871">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-872">클라이언트 IP 주소 hello HTTP 요청에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-872">Client IP address hello HTTP request came from.</span></span> <span data-ttu-id="ae7fe-873">hello hello 원래 로그에서 c-ip 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-873">hello c-ip field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="ae7fe-874">csUserAgent</span></span> |<span data-ttu-id="ae7fe-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-875">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-876">Hello 클라이언트에서 선언한 HTTP 사용자 에이전트 (브라우저 또는 그렇지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-876">HTTP User-Agent declared by hello client (browser or otherwise).</span></span> <span data-ttu-id="ae7fe-877">hello cs-사용자-에이전트 hello 원래 로그에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-877">hello cs-user-agent in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-878">scStatus</span></span> |<span data-ttu-id="ae7fe-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-879">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-880">HTTP 상태 코드 (예를 들어 200/403/500) hello 서버 toohello 클라이언트에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-880">HTTP Status code (for example, 200/403/500) returned by hello server toohello client.</span></span> <span data-ttu-id="ae7fe-881">hello 원래 로그에서 cs-status hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-881">hello cs-status in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-882">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="ae7fe-882">TimeTaken</span></span> |<span data-ttu-id="ae7fe-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-883">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-884">Hello 요청 하는 시간 (밀리초) toocomplete를 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-884">How long (in milliseconds) that hello request took toocomplete.</span></span> <span data-ttu-id="ae7fe-885">hello hello 원래 로그에서 timetaken 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-885">hello timetaken field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="ae7fe-886">csUriStem</span></span> |<span data-ttu-id="ae7fe-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-887">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-888">요청된 상대 URI( 호스트 주소 즉, /search 없이)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="ae7fe-889">hello hello 원래 로그에서 cs-uristem 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-889">hello cs-uristem field in hello original log.</span></span> |
| <span data-ttu-id="ae7fe-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="ae7fe-890">csUriQuery</span></span> |<span data-ttu-id="ae7fe-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-891">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-892">URI 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-892">URI query.</span></span> <span data-ttu-id="ae7fe-893">URI 쿼리는 ASP 페이지와 같은 동적 페이지에만 필요하므로 이 필드는 일반적으로 정적 페이지에 대한 하이픈을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="ae7fe-894">sPort</span><span class="sxs-lookup"><span data-stu-id="ae7fe-894">sPort</span></span> |<span data-ttu-id="ae7fe-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-895">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-896">너무 전송 HTTP 요청을 hello 서버 포트 (및 선택 되었기 때문에 IIS에서 수신함).</span><span class="sxs-lookup"><span data-stu-id="ae7fe-896">Server port that hello HTTP request was sent too(and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="ae7fe-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-897">csUserName</span></span> |<span data-ttu-id="ae7fe-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-898">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-899">인증 된 사용자 이름 hello 요청이 인증 되 고 익명이 아닌 경우.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-899">Authenticated user name, if hello request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="ae7fe-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="ae7fe-900">csVersion</span></span> |<span data-ttu-id="ae7fe-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-901">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-902">Hello 요청 (예: HTTP/1.1)에 사용 되는 HTTP 프로토콜 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-902">HTTP Protocol version used in hello request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="ae7fe-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="ae7fe-903">csCookie</span></span> |<span data-ttu-id="ae7fe-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-904">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-905">쿠키 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-905">Cookie information.</span></span> |
| <span data-ttu-id="ae7fe-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="ae7fe-906">csReferer</span></span> |<span data-ttu-id="ae7fe-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-907">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-908">해당 hello 사용자가 마지막으로 방문한 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-908">Site that hello user last visited.</span></span> <span data-ttu-id="ae7fe-909">이 사이트 링크 toohello 현재 사이트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-909">This site provided a link toohello current site.</span></span> |
| <span data-ttu-id="ae7fe-910">csHost</span><span class="sxs-lookup"><span data-stu-id="ae7fe-910">csHost</span></span> |<span data-ttu-id="ae7fe-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-911">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-912">요청된 호스트 헤더(예: www.mysite.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="ae7fe-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="ae7fe-913">scSubStatus</span></span> |<span data-ttu-id="ae7fe-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-914">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-915">하위 상태 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-915">Substatus error code.</span></span> |
| <span data-ttu-id="ae7fe-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="ae7fe-916">scWin32Status</span></span> |<span data-ttu-id="ae7fe-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-917">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-918">Windows 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-918">Windows status code.</span></span> |
| <span data-ttu-id="ae7fe-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="ae7fe-919">csBytes</span></span> |<span data-ttu-id="ae7fe-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-920">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-921">Hello 클라이언트 toohello 서버 hello 요청에서 보낸 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-921">Bytes sent in hello request from hello client toohello server.</span></span> |
| <span data-ttu-id="ae7fe-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="ae7fe-922">scBytes</span></span> |<span data-ttu-id="ae7fe-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ae7fe-923">W3CIISLog</span></span> |<span data-ttu-id="ae7fe-924">바이트는 hello 서버 toohello 클라이언트로부터 hello 응답에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-924">Bytes returned back in hello response from hello server toohello client.</span></span> |
| <span data-ttu-id="ae7fe-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-925">ConfigChangeType</span></span> |<span data-ttu-id="ae7fe-926">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-926">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-927">변경의 유형(예: WindowsServices/소프트웨어)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="ae7fe-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="ae7fe-928">ChangeCategory</span></span> |<span data-ttu-id="ae7fe-929">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-929">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-930">Hello 변경 (수정/추가/제거 됨)의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-930">Category of hello change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="ae7fe-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-931">SoftwareType</span></span> |<span data-ttu-id="ae7fe-932">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-932">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-933">소프트웨어의 종류(업데이트/응용 프로그램)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="ae7fe-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-934">SoftwareName</span></span> |<span data-ttu-id="ae7fe-935">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-935">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-936">Hello 소프트웨어 (적용 가능한 toosoftware 변경 내용만)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-936">Name of hello software (only applicable toosoftware changes).</span></span> |
| <span data-ttu-id="ae7fe-937">게시자</span><span class="sxs-lookup"><span data-stu-id="ae7fe-937">Publisher</span></span> |<span data-ttu-id="ae7fe-938">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-938">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-939">Hello (적용 가능한 toosoftware 변경 내용만) 소프트웨어를 게시 하는 공급 업체입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-939">Vendor who publishes hello software (only applicable toosoftware changes).</span></span> |
| <span data-ttu-id="ae7fe-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-940">SvcChangeType</span></span> |<span data-ttu-id="ae7fe-941">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-941">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-942">Windows 서비스에 적용된 변경의 유형(상태/StartupType/경로/ServiceAccount)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="ae7fe-943">서비스 변경 내용만 적용 가능한 tooWindows입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-943">This is only applicable tooWindows service changes.</span></span> |
| <span data-ttu-id="ae7fe-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-944">SvcDisplayName</span></span> |<span data-ttu-id="ae7fe-945">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-945">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-946">변경 된 hello 서비스의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-946">Display name of hello service that was changed.</span></span> |
| <span data-ttu-id="ae7fe-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="ae7fe-947">SvcName</span></span> |<span data-ttu-id="ae7fe-948">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-948">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-949">변경 된 hello 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-949">Name of hello service that was changed.</span></span> |
| <span data-ttu-id="ae7fe-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="ae7fe-950">SvcState</span></span> |<span data-ttu-id="ae7fe-951">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-951">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-952">Hello 서비스의 새 (현재) 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-952">New (current) state of hello service.</span></span> |
| <span data-ttu-id="ae7fe-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="ae7fe-953">SvcPreviousState</span></span> |<span data-ttu-id="ae7fe-954">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-954">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-955">이전에 알려진 hello 서비스 (서비스 상태를 변경 하는 경우에 해당)의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-955">Previous known state of hello service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="ae7fe-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-956">SvcStartupType</span></span> |<span data-ttu-id="ae7fe-957">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-957">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-958">서비스 시작 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-958">Service startup type.</span></span> |
| <span data-ttu-id="ae7fe-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="ae7fe-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="ae7fe-960">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-960">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-961">이전 서비스 시작 유형(서비스 시작 유형을 변경하는 경우만 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="ae7fe-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="ae7fe-962">SvcAccount</span></span> |<span data-ttu-id="ae7fe-963">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-963">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-964">서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-964">Service account.</span></span> |
| <span data-ttu-id="ae7fe-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="ae7fe-965">SvcPreviousAccount</span></span> |<span data-ttu-id="ae7fe-966">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-966">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-967">이전 서비스 계정(서비스 계정이 변경된 경우만 해당)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="ae7fe-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="ae7fe-968">SvcPath</span></span> |<span data-ttu-id="ae7fe-969">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-969">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-970">경로 toohello hello Windows 서비스의 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-970">Path toohello executable of hello Windows service.</span></span> |
| <span data-ttu-id="ae7fe-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="ae7fe-971">SvcPreviousPath</span></span> |<span data-ttu-id="ae7fe-972">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-972">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-973">Hello hello Windows 서비스 (이것이 변경 된 경우에 해당)에 대 한 실행 파일의 이전 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-973">Previous path of hello executable for hello Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="ae7fe-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="ae7fe-974">SvcDescription</span></span> |<span data-ttu-id="ae7fe-975">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-975">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-976">Hello 서비스의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-976">Description of hello service.</span></span> |
| <span data-ttu-id="ae7fe-977">이전</span><span class="sxs-lookup"><span data-stu-id="ae7fe-977">Previous</span></span> |<span data-ttu-id="ae7fe-978">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-978">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-979">이 소프트웨어의 이전 상태(설치됨/설치되지 않음/이전 버전)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="ae7fe-980">Current</span><span class="sxs-lookup"><span data-stu-id="ae7fe-980">Current</span></span> |<span data-ttu-id="ae7fe-981">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="ae7fe-981">ConfigurationChange</span></span> |<span data-ttu-id="ae7fe-982">이 소프트웨어의 최근 상태(설치됨/설치되지 않음/현재 버전)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae7fe-983">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae7fe-983">Next steps</span></span>
<span data-ttu-id="ae7fe-984">로그 검색에 대한 자세한 내용은 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-984">For additional information about log searches:</span></span>

* <span data-ttu-id="ae7fe-985">익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview 솔루션에서 수집 된 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-985">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="ae7fe-986">사용 하 여 [로그 분석의 사용자 지정 필드가](log-analytics-custom-fields.md) tooextend 로그 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7fe-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
