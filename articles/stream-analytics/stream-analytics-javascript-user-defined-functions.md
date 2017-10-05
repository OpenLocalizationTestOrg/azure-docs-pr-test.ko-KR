---
title: "Azure Stream Analytics JavaScript 사용자 정의 함수 | Microsoft Docs"
description: "JavaScript 사용자 정의 함수로 고급 쿼리 역학 수행"
keywords: "javascript, 사용자 정의 함수, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="95fce-104">Azure Stream Analytics JavaScript 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="95fce-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="95fce-105">Azure Stream Analytics에서는 JavaScript로 작성된 사용자 정의 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="95fce-106">JavaScript에서 제공하는 풍부한 메서드 집합(**String**, **RegExp**, **Math**, **Array**, **Date**)을 통해 Stream Analytics 작업에서 복잡한 데이터 변환을 쉽게 만들 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="95fce-107">JavaScript 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="95fce-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="95fce-108">JavaScript 사용자 정의 함수는 외부 연결이 필요 없는 상태 비저장, 계산 전용 스칼라 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="95fce-109">함수의 반환 값은 스칼라(단일) 값만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="95fce-110">JavaScript 사용자 정의 함수를 작업에 추가한 후 기본 제공 스칼라 함수처럼 쿼리의 아무 곳에서나 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="95fce-111">다음은 JavaScript 사용자 정의 함수가 유용할 수 있는 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="95fce-112">정규식 함수를 가진 문자열을 구문 분석 및 조작(예: **Regexp_Replace()** 및 **Regexp_Extract()**)</span><span class="sxs-lookup"><span data-stu-id="95fce-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="95fce-113">데이터 디코딩 및 인코딩(예: 2진을 16진으로 변환)</span><span class="sxs-lookup"><span data-stu-id="95fce-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="95fce-114">JavaScript **Math** 함수로 수학 계산 수행</span><span class="sxs-lookup"><span data-stu-id="95fce-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="95fce-115">정렬, 조인, 찾기 및 채우기 등의 배열 작업 수행</span><span class="sxs-lookup"><span data-stu-id="95fce-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="95fce-116">다음은 Stream Analytics에서 JavaScript 사용자 정의 함수로 수행할 수 없는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="95fce-117">외부 REST 끝점 호출(예: 역방향 IP 조회 수행 또는 외부 원본에서 참조 데이터 끌어오기)</span><span class="sxs-lookup"><span data-stu-id="95fce-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="95fce-118">입력/출력에서 사용자 지정 이벤트 형식 직렬화 또는 역직렬화 수행</span><span class="sxs-lookup"><span data-stu-id="95fce-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="95fce-119">사용자 지정 집계 만들기</span><span class="sxs-lookup"><span data-stu-id="95fce-119">Create custom aggregates</span></span>

<span data-ttu-id="95fce-120">함수 정의에서 차단되지는 않지만 **Date.GetDate()** 또는 **Math.random()**과 같은 함수는 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="95fce-121">이러한 함수는 호출할 때마다 **다른** 결과를 반환하며 Azure Stream Analytics 서비스에서 함수 호출 및 반환된 결과 저널을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="95fce-122">동일한 이벤트에 대해 함수가 다른 결과를 반환하면 사용자 또는 Stream Analytics 서비스에서 작업을 다시 시작할 때 반복성이 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="95fce-123">Azure Portal에서 JavaScript 사용자 정의 함수 추가</span><span class="sxs-lookup"><span data-stu-id="95fce-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="95fce-124">기존 Stream Analytics 작업에서 간단한 JavaScript 사용자 정의 함수를 작성하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="95fce-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="95fce-125">Azure Portal에서 Stream Analytics 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="95fce-126">**작업 토폴로지** 아래에서 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="95fce-127">함수의 빈 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="95fce-128">새 사용자 정의 함수를 만들려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="95fce-129">**새 함수** 블레이드에서 **함수 유형**에 대해 **JavaScript**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="95fce-130">기본 함수 템플릿이 편집기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="95fce-131">**UDF 별칭**의 경우 **hex2Int**를 입력하고 함수 구현을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="95fce-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-132">Select **Save**.</span></span> <span data-ttu-id="95fce-133">함수가 함수의 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="95fce-134">새 **hex2Int** 함수를 선택하고 함수 정의를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="95fce-135">모든 함수는 함수 별칭에 **UDF** 접두사가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="95fce-136">Stream Analytics 쿼리에서 함수를 호출할 때 *접두사를 포함*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="95fce-137">이 경우 **UDF.hex2Int**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="95fce-138">쿼리에서 JavaScript 사용자 정의 함수 호출</span><span class="sxs-lookup"><span data-stu-id="95fce-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="95fce-139">쿼리 편집기에서 **작업 토폴로지** 아래에 있는 **쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="95fce-140">쿼리에 편집하고 다음과 같은 사용자 정의 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="95fce-141">샘플 데이터 파일 업로드하려면 작업 입력을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="95fce-142">쿼리를 테스트하려면 **테스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="95fce-143">지원되는 JavaScript 개체</span><span class="sxs-lookup"><span data-stu-id="95fce-143">Supported JavaScript objects</span></span>
<span data-ttu-id="95fce-144">Azure Stream Analytics JavaScript 사용자 정의 함수는 표준인 기본 제공 JavaScript 개체를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="95fce-145">이러한 개체의 목록은 [전역 개체](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fce-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="95fce-146">Stream Analytics 및 JavaScript 형식 변환</span><span class="sxs-lookup"><span data-stu-id="95fce-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="95fce-147">Stream Analytics 쿼리 언어와 JavaScript가 지원하는 형식 간에는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="95fce-148">이 테이블에는 둘 간의 변환 매핑 목록이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="95fce-149">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="95fce-149">Stream Analytics</span></span> | <span data-ttu-id="95fce-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="95fce-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="95fce-151">bigint</span><span class="sxs-lookup"><span data-stu-id="95fce-151">bigint</span></span> | <span data-ttu-id="95fce-152">Number(JavaScript에서는 정확히 최대 2^53의 정수만 표현할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="95fce-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="95fce-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="95fce-153">DateTime</span></span> | <span data-ttu-id="95fce-154">Date(JavaScript에서는 밀리초만 지원)</span><span class="sxs-lookup"><span data-stu-id="95fce-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="95fce-155">double</span><span class="sxs-lookup"><span data-stu-id="95fce-155">double</span></span> | <span data-ttu-id="95fce-156">Number</span><span class="sxs-lookup"><span data-stu-id="95fce-156">Number</span></span>
<span data-ttu-id="95fce-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="95fce-157">nvarchar(MAX)</span></span> | <span data-ttu-id="95fce-158">문자열</span><span class="sxs-lookup"><span data-stu-id="95fce-158">String</span></span>
<span data-ttu-id="95fce-159">레코드</span><span class="sxs-lookup"><span data-stu-id="95fce-159">Record</span></span> | <span data-ttu-id="95fce-160">Object</span><span class="sxs-lookup"><span data-stu-id="95fce-160">Object</span></span>
<span data-ttu-id="95fce-161">배열</span><span class="sxs-lookup"><span data-stu-id="95fce-161">Array</span></span> | <span data-ttu-id="95fce-162">배열</span><span class="sxs-lookup"><span data-stu-id="95fce-162">Array</span></span>
<span data-ttu-id="95fce-163">NULL</span><span class="sxs-lookup"><span data-stu-id="95fce-163">NULL</span></span> | <span data-ttu-id="95fce-164">Null</span><span class="sxs-lookup"><span data-stu-id="95fce-164">Null</span></span>


<span data-ttu-id="95fce-165">다음은 JavaScript-Stream Analytics 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="95fce-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="95fce-166">JavaScript</span></span> | <span data-ttu-id="95fce-167">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="95fce-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="95fce-168">Number</span><span class="sxs-lookup"><span data-stu-id="95fce-168">Number</span></span> | <span data-ttu-id="95fce-169">Bigint(숫자를 반올림하여 long.MinValue와 long.MaxValue 사이에 있는 경우, 그렇지 않으면 double임)</span><span class="sxs-lookup"><span data-stu-id="95fce-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="95fce-170">Date</span><span class="sxs-lookup"><span data-stu-id="95fce-170">Date</span></span> | <span data-ttu-id="95fce-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="95fce-171">DateTime</span></span>
<span data-ttu-id="95fce-172">String</span><span class="sxs-lookup"><span data-stu-id="95fce-172">String</span></span> | <span data-ttu-id="95fce-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="95fce-173">nvarchar(MAX)</span></span>
<span data-ttu-id="95fce-174">Object</span><span class="sxs-lookup"><span data-stu-id="95fce-174">Object</span></span> | <span data-ttu-id="95fce-175">레코드</span><span class="sxs-lookup"><span data-stu-id="95fce-175">Record</span></span>
<span data-ttu-id="95fce-176">배열</span><span class="sxs-lookup"><span data-stu-id="95fce-176">Array</span></span> | <span data-ttu-id="95fce-177">배열</span><span class="sxs-lookup"><span data-stu-id="95fce-177">Array</span></span>
<span data-ttu-id="95fce-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="95fce-178">Null, Undefined</span></span> | <span data-ttu-id="95fce-179">NULL</span><span class="sxs-lookup"><span data-stu-id="95fce-179">NULL</span></span>
<span data-ttu-id="95fce-180">기타 다른 형식(예: 함수 또는 오류)</span><span class="sxs-lookup"><span data-stu-id="95fce-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="95fce-181">지원되지 않음(런타임 오류 발생)</span><span class="sxs-lookup"><span data-stu-id="95fce-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="95fce-182">문제 해결</span><span class="sxs-lookup"><span data-stu-id="95fce-182">Troubleshooting</span></span>
<span data-ttu-id="95fce-183">JavaScript 런타임 오류는 치명적인 것으로 간주되고 활동 로그를 통해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="95fce-184">Azure Portal에서 로그를 검색하려면 작업으로 이동하고 **활동 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="95fce-185">기타 JavaScript 사용자 정의 함수 패턴</span><span class="sxs-lookup"><span data-stu-id="95fce-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="95fce-186">중첩된 JSON을 출력에 작성</span><span class="sxs-lookup"><span data-stu-id="95fce-186">Write nested JSON to output</span></span>
<span data-ttu-id="95fce-187">Stream Analytics 작업 출력을 입력으로 사용하는 후속 처리 단계가 있고 이것이 JSON 형식을 요구하는 경우 JSON 문자열을 출력에 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="95fce-188">다음 예에서는 **JSON.stringify()** 함수를 호출하여 입력의 모든 이름/값 쌍을 묶고 출력에 단일 문자열 값으로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fce-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="95fce-189">**JavaScript 사용자 정의 함수 정의:**</span><span class="sxs-lookup"><span data-stu-id="95fce-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="95fce-190">**샘플 쿼리:**</span><span class="sxs-lookup"><span data-stu-id="95fce-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="95fce-191">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="95fce-191">Get help</span></span>
<span data-ttu-id="95fce-192">추가 도움이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fce-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95fce-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95fce-193">Next steps</span></span>
* [<span data-ttu-id="95fce-194">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="95fce-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="95fce-195">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="95fce-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="95fce-196">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="95fce-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="95fce-197">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="95fce-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="95fce-198">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="95fce-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
