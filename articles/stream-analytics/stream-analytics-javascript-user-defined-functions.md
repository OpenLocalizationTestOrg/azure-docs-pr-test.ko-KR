---
title: "aaaAzure 스트림 분석 JavaScript 사용자 정의 함수가 | Microsoft Docs"
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
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="23bfb-104">Azure Stream Analytics JavaScript 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="23bfb-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="23bfb-105">Azure Stream Analytics에서는 JavaScript로 작성된 사용자 정의 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="23bfb-106">풍부한 hello와 **문자열**, **RegExp**, **수학**, **배열**, 및 **날짜** 메서드는 복잡 한 데이터 변환에 대 한 스트림 분석 작업에 쉽게 toocreate 있게 JavaScript에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="23bfb-107">JavaScript 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="23bfb-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="23bfb-108">JavaScript 사용자 정의 함수는 외부 연결이 필요 없는 상태 비저장, 계산 전용 스칼라 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="23bfb-109">hello 함수 값만 값일 수는 스칼라 (단일)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="23bfb-110">JavaScript 사용자 정의 함수 tooa 작업을 추가한 후에 기본 제공 스칼라 함수 처럼 hello 쿼리에서 아무 곳 이나 hello 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="23bfb-111">다음은 JavaScript 사용자 정의 함수가 유용할 수 있는 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="23bfb-112">정규식 함수를 가진 문자열을 구문 분석 및 조작(예: **Regexp_Replace()** 및 **Regexp_Extract()**)</span><span class="sxs-lookup"><span data-stu-id="23bfb-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="23bfb-113">데이터 디코딩 및 인코딩(예: 2진을 16진으로 변환)</span><span class="sxs-lookup"><span data-stu-id="23bfb-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="23bfb-114">JavaScript **Math** 함수로 수학 계산 수행</span><span class="sxs-lookup"><span data-stu-id="23bfb-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="23bfb-115">정렬, 조인, 찾기 및 채우기 등의 배열 작업 수행</span><span class="sxs-lookup"><span data-stu-id="23bfb-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="23bfb-116">다음은 Stream Analytics에서 JavaScript 사용자 정의 함수로 수행할 수 없는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="23bfb-117">외부 REST 끝점 호출(예: 역방향 IP 조회 수행 또는 외부 원본에서 참조 데이터 끌어오기)</span><span class="sxs-lookup"><span data-stu-id="23bfb-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="23bfb-118">입력/출력에서 사용자 지정 이벤트 형식 직렬화 또는 역직렬화 수행</span><span class="sxs-lookup"><span data-stu-id="23bfb-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="23bfb-119">사용자 지정 집계 만들기</span><span class="sxs-lookup"><span data-stu-id="23bfb-119">Create custom aggregates</span></span>

<span data-ttu-id="23bfb-120">처럼 작동 하지만 **Date.GetDate()** 또는 **Math.random()** 차단 되지 않는지 hello 함수 정의에 사용 하면 안 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="23bfb-121">이러한 함수 **없는** 반환 hello 동일 호출 하면 함수 호출의 저널 hello Azure 스트림 분석 서비스를 보관 하지 않습니다 때마다 발생 하 고 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="23bfb-122">함수는 다른 결과가 반환 hello에 동일한 이벤트 또는 hello 스트림 분석 서비스에서 작업을 다시 시작 되 면 반복성 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="23bfb-123">JavaScript 사용자 정의 함수 hello Azure 포털에 추가</span><span class="sxs-lookup"><span data-stu-id="23bfb-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="23bfb-124">toocreate는 간단한 JavaScript 사용자 정의 함수는 기존 스트림 분석 작업에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="23bfb-125">Hello Azure 포털에서에서 스트림 분석 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="23bfb-126">**작업 토폴로지** 아래에서 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="23bfb-127">함수의 빈 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="23bfb-128">toocreate 새 사용자 정의 함수 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="23bfb-129">Hello에 **새 함수** 블레이드에서 대 한 **함수 형식**선택, **JavaScript**합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="23bfb-130">기본 함수 템플릿을 hello 편집기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="23bfb-131">Hello에 대 한 **UDF 별칭**, 입력 **hex2Int**, 다음과 같이 hello 함수 구현 변경:</span><span class="sxs-lookup"><span data-stu-id="23bfb-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="23bfb-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-132">Select **Save**.</span></span> <span data-ttu-id="23bfb-133">사용자가 함수 hello 함수 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="23bfb-134">새 선택 hello **hex2Int** 작동 하 고 hello 함수 정의 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="23bfb-135">모든 함수는 **UDF** 접두사 추가 toohello 함수 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="23bfb-136">너무 필요한*hello 접두사를 포함* 스트림 분석 쿼리에 hello 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="23bfb-137">이 경우 **UDF.hex2Int**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="23bfb-138">쿼리에서 JavaScript 사용자 정의 함수 호출</span><span class="sxs-lookup"><span data-stu-id="23bfb-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="23bfb-139">Hello에서 쿼리 편집기에서 **작업 토폴로지**선택, **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="23bfb-140">쿼리를 편집 하 고 hello 사용자 정의 함수를 다음과 같이 호출:</span><span class="sxs-lookup"><span data-stu-id="23bfb-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="23bfb-141">tooupload hello 예제 데이터 파일을 마우스 오른쪽 단추로 클릭 hello 작업 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="23bfb-142">tootest 선택 쿼리에 **테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="23bfb-143">지원되는 JavaScript 개체</span><span class="sxs-lookup"><span data-stu-id="23bfb-143">Supported JavaScript objects</span></span>
<span data-ttu-id="23bfb-144">Azure Stream Analytics JavaScript 사용자 정의 함수는 표준인 기본 제공 JavaScript 개체를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="23bfb-145">이러한 개체의 목록은 [전역 개체](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23bfb-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="23bfb-146">Stream Analytics 및 JavaScript 형식 변환</span><span class="sxs-lookup"><span data-stu-id="23bfb-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="23bfb-147">Hello 스트림 분석 쿼리 언어 및 JavaScript를 지원 하는 hello 형식에는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="23bfb-148">이 표에서 두 hello 간의 hello 변환 매핑을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="23bfb-149">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="23bfb-149">Stream Analytics</span></span> | <span data-ttu-id="23bfb-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="23bfb-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="23bfb-151">bigint</span><span class="sxs-lookup"><span data-stu-id="23bfb-151">bigint</span></span> | <span data-ttu-id="23bfb-152">숫자 (JavaScript 정수 tooprecisely 2 나타낼 수 있습니다 ^53)</span><span class="sxs-lookup"><span data-stu-id="23bfb-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="23bfb-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="23bfb-153">DateTime</span></span> | <span data-ttu-id="23bfb-154">Date(JavaScript에서는 밀리초만 지원)</span><span class="sxs-lookup"><span data-stu-id="23bfb-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="23bfb-155">double</span><span class="sxs-lookup"><span data-stu-id="23bfb-155">double</span></span> | <span data-ttu-id="23bfb-156">Number</span><span class="sxs-lookup"><span data-stu-id="23bfb-156">Number</span></span>
<span data-ttu-id="23bfb-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="23bfb-157">nvarchar(MAX)</span></span> | <span data-ttu-id="23bfb-158">문자열</span><span class="sxs-lookup"><span data-stu-id="23bfb-158">String</span></span>
<span data-ttu-id="23bfb-159">레코드</span><span class="sxs-lookup"><span data-stu-id="23bfb-159">Record</span></span> | <span data-ttu-id="23bfb-160">Object</span><span class="sxs-lookup"><span data-stu-id="23bfb-160">Object</span></span>
<span data-ttu-id="23bfb-161">배열</span><span class="sxs-lookup"><span data-stu-id="23bfb-161">Array</span></span> | <span data-ttu-id="23bfb-162">배열</span><span class="sxs-lookup"><span data-stu-id="23bfb-162">Array</span></span>
<span data-ttu-id="23bfb-163">NULL</span><span class="sxs-lookup"><span data-stu-id="23bfb-163">NULL</span></span> | <span data-ttu-id="23bfb-164">Null</span><span class="sxs-lookup"><span data-stu-id="23bfb-164">Null</span></span>


<span data-ttu-id="23bfb-165">다음은 JavaScript-Stream Analytics 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="23bfb-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="23bfb-166">JavaScript</span></span> | <span data-ttu-id="23bfb-167">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="23bfb-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="23bfb-168">Number</span><span class="sxs-lookup"><span data-stu-id="23bfb-168">Number</span></span> | <span data-ttu-id="23bfb-169">Bigint (경우 hello 번호가 round 및 long 사이입니다. MinValue 및 long입니다. MaxValue; 그렇지 않으면 double은)</span><span class="sxs-lookup"><span data-stu-id="23bfb-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="23bfb-170">Date</span><span class="sxs-lookup"><span data-stu-id="23bfb-170">Date</span></span> | <span data-ttu-id="23bfb-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="23bfb-171">DateTime</span></span>
<span data-ttu-id="23bfb-172">String</span><span class="sxs-lookup"><span data-stu-id="23bfb-172">String</span></span> | <span data-ttu-id="23bfb-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="23bfb-173">nvarchar(MAX)</span></span>
<span data-ttu-id="23bfb-174">Object</span><span class="sxs-lookup"><span data-stu-id="23bfb-174">Object</span></span> | <span data-ttu-id="23bfb-175">레코드</span><span class="sxs-lookup"><span data-stu-id="23bfb-175">Record</span></span>
<span data-ttu-id="23bfb-176">배열</span><span class="sxs-lookup"><span data-stu-id="23bfb-176">Array</span></span> | <span data-ttu-id="23bfb-177">배열</span><span class="sxs-lookup"><span data-stu-id="23bfb-177">Array</span></span>
<span data-ttu-id="23bfb-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="23bfb-178">Null, Undefined</span></span> | <span data-ttu-id="23bfb-179">NULL</span><span class="sxs-lookup"><span data-stu-id="23bfb-179">NULL</span></span>
<span data-ttu-id="23bfb-180">기타 다른 형식(예: 함수 또는 오류)</span><span class="sxs-lookup"><span data-stu-id="23bfb-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="23bfb-181">지원되지 않음(런타임 오류 발생)</span><span class="sxs-lookup"><span data-stu-id="23bfb-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="23bfb-182">문제 해결</span><span class="sxs-lookup"><span data-stu-id="23bfb-182">Troubleshooting</span></span>
<span data-ttu-id="23bfb-183">JavaScript 런타임 오류, 간주 되 고 hello 활동 로그를 통해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="23bfb-184">hello Azure 포털, go tooyour 작업 및 선택 tooretrieve hello 로그 **활동 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="23bfb-185">기타 JavaScript 사용자 정의 함수 패턴</span><span class="sxs-lookup"><span data-stu-id="23bfb-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="23bfb-186">중첩 된 JSON toooutput 작성</span><span class="sxs-lookup"><span data-stu-id="23bfb-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="23bfb-187">출력 스트림 분석 작업 입력으로 사용 하는 후속 처리 단계 있고 JSON 형식이 필요한 경우에 JSON 문자열 toooutput를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="23bfb-188">hello 다음 예제에서는 호출 hello **JSON.stringify()** toopack 모든 이름/값 쌍의 hello 입력과 출력에는 단일 문자열 값으로 쓸지를 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="23bfb-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="23bfb-189">**JavaScript 사용자 정의 함수 정의:**</span><span class="sxs-lookup"><span data-stu-id="23bfb-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="23bfb-190">**샘플 쿼리:**</span><span class="sxs-lookup"><span data-stu-id="23bfb-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="23bfb-191">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="23bfb-191">Get help</span></span>
<span data-ttu-id="23bfb-192">추가 도움이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23bfb-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23bfb-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23bfb-193">Next steps</span></span>
* [<span data-ttu-id="23bfb-194">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="23bfb-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="23bfb-195">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="23bfb-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="23bfb-196">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="23bfb-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="23bfb-197">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="23bfb-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="23bfb-198">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="23bfb-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
