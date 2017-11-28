---
title: "스트림 분석의 일반적인 사용 패턴에 대 한 예제 aaaQuery | Microsoft Docs"
description: "일반적인 Azure Stream Analytics 쿼리 패턴"
keywords: "쿼리 예제"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="3c032-104">일반적인 Stream Analytics 사용 패턴에 대한 쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="3c032-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="3c032-105">소개</span><span class="sxs-lookup"><span data-stu-id="3c032-105">Introduction</span></span>
<span data-ttu-id="3c032-106">Azure Stream Analytics에서 쿼리는 SQL 방식 쿼리 언어로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="3c032-107">이러한 쿼리는 hello에 설명 되어 [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="3c032-108">이 문서 윤곽선 솔루션 tooseveral 공통 패턴을 기반으로 실제 시나리오를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="3c032-109">작업을 진행 중 이며 toobe 지속적으로 새 패턴을 사용 하 여 업데이트를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="3c032-110">쿼리 예제: 데이터 형식 변환</span><span class="sxs-lookup"><span data-stu-id="3c032-110">Query example: Convert data types</span></span>
<span data-ttu-id="3c032-111">**설명**: hello 입력 스트림에서 hello 유형의 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="3c032-112">예를 들어 hello 자동차 가중치 문자열로 입력된 스트림을 hello에 나오는 하며 너무 변환 toobe**INT** tooperform **SUM** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="3c032-113">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-113">**Input**:</span></span>

| <span data-ttu-id="3c032-114">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-114">Make</span></span> | <span data-ttu-id="3c032-115">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-115">Time</span></span> | <span data-ttu-id="3c032-116">무게</span><span class="sxs-lookup"><span data-stu-id="3c032-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-117">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-117">Honda</span></span> |<span data-ttu-id="3c032-118">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="3c032-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="3c032-119">"1000"</span></span> |
| <span data-ttu-id="3c032-120">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-120">Honda</span></span> |<span data-ttu-id="3c032-121">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3c032-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="3c032-122">"2000"</span></span> |

<span data-ttu-id="3c032-123">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-123">**Output**:</span></span>

| <span data-ttu-id="3c032-124">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-124">Make</span></span> | <span data-ttu-id="3c032-125">무게</span><span class="sxs-lookup"><span data-stu-id="3c032-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-126">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-126">Honda</span></span> |<span data-ttu-id="3c032-127">3000</span><span class="sxs-lookup"><span data-stu-id="3c032-127">3000</span></span> |

<span data-ttu-id="3c032-128">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="3c032-129">**설명**: 사용 하 여 한 **캐스트** hello에 문을 **가중치** toospecify 필드의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="3c032-130">지원 되는 데이터 형식 목록이 hello 참조 [데이터 형식 (Azure 스트림 분석)](https://msdn.microsoft.com/library/azure/dn835065.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="3c032-131">쿼리 예: Like/Not toodo 패턴 일치와 같은 사용</span><span class="sxs-lookup"><span data-stu-id="3c032-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="3c032-132">**설명**: hello 이벤트 필드 값을 특정 패턴과 일치 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c032-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="3c032-133">예를 들어 hello 결과 번호판 A로 시작 하 고 9 끝나야 하는 반환 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="3c032-134">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-134">**Input**:</span></span>

| <span data-ttu-id="3c032-135">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-135">Make</span></span> | <span data-ttu-id="3c032-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-136">LicensePlate</span></span> | <span data-ttu-id="3c032-137">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-138">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-138">Honda</span></span> |<span data-ttu-id="3c032-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3c032-139">ABC-123</span></span> |<span data-ttu-id="3c032-140">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-141">Toyota</span></span> |<span data-ttu-id="3c032-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3c032-142">AAA-999</span></span> |<span data-ttu-id="3c032-143">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="3c032-144">Nissan</span></span> |<span data-ttu-id="3c032-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="3c032-145">ABC-369</span></span> |<span data-ttu-id="3c032-146">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-147">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-147">**Output**:</span></span>

| <span data-ttu-id="3c032-148">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-148">Make</span></span> | <span data-ttu-id="3c032-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-149">LicensePlate</span></span> | <span data-ttu-id="3c032-150">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-151">Toyota</span></span> |<span data-ttu-id="3c032-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3c032-152">AAA-999</span></span> |<span data-ttu-id="3c032-153">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="3c032-154">Nissan</span></span> |<span data-ttu-id="3c032-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="3c032-155">ABC-369</span></span> |<span data-ttu-id="3c032-156">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-157">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="3c032-158">**설명은**: 사용 하 여 hello **같은** 문 toocheck hello **LicensePlate** 필드 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="3c032-159">A로 시작한 다음 0개 이상의 문자열을 포함하고 a9로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="3c032-160">쿼리 예제: 다른 사례/값(CASE 문)에 대한 논리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="3c032-161">**설명**: 특정 조건에 따라 필드에 대해 다른 계산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="3c032-162">예를 들어 1에 대 한 특별 한 경우와 함께 확인 동일 hello의 개수 자동차를 전달 하는 것에 대 한 설명 문자열을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="3c032-163">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-163">**Input**:</span></span>

| <span data-ttu-id="3c032-164">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-164">Make</span></span> | <span data-ttu-id="3c032-165">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-166">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-166">Honda</span></span> |<span data-ttu-id="3c032-167">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-168">Toyota</span></span> |<span data-ttu-id="3c032-169">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-170">Toyota</span></span> |<span data-ttu-id="3c032-171">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-172">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-172">**Output**:</span></span>

| <span data-ttu-id="3c032-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="3c032-173">CarsPassed</span></span> | <span data-ttu-id="3c032-174">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-175">1 Honda</span></span> |<span data-ttu-id="3c032-176">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="3c032-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="3c032-177">2 Toyotas</span></span> |<span data-ttu-id="3c032-178">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="3c032-179">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="3c032-180">**설명은**: hello **대/소문자** 절 (경우에는 hello 집계 창에 있는 hello 자동차의 hello 수)에 몇 가지 조건에 따라 다른 계산 tooprovide 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="3c032-181">쿼리 예: 데이터 toomultiple 출력 보내기</span><span class="sxs-lookup"><span data-stu-id="3c032-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="3c032-182">**설명**: 송신 데이터 toomultiple 단일 작업에서 대상 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="3c032-183">예를 들어 임계값 기반 경고에 대 한 데이터를 분석 하 고 모든 이벤트 tooblob 저장소를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="3c032-184">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-184">**Input**:</span></span>

| <span data-ttu-id="3c032-185">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-185">Make</span></span> | <span data-ttu-id="3c032-186">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-187">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-187">Honda</span></span> |<span data-ttu-id="3c032-188">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-189">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-189">Honda</span></span> |<span data-ttu-id="3c032-190">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-191">Toyota</span></span> |<span data-ttu-id="3c032-192">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-193">Toyota</span></span> |<span data-ttu-id="3c032-194">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-195">Toyota</span></span> |<span data-ttu-id="3c032-196">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-197">**출력1**:</span><span class="sxs-lookup"><span data-stu-id="3c032-197">**Output1**:</span></span>

| <span data-ttu-id="3c032-198">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-198">Make</span></span> | <span data-ttu-id="3c032-199">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-200">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-200">Honda</span></span> |<span data-ttu-id="3c032-201">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-202">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-202">Honda</span></span> |<span data-ttu-id="3c032-203">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-204">Toyota</span></span> |<span data-ttu-id="3c032-205">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-206">Toyota</span></span> |<span data-ttu-id="3c032-207">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-208">Toyota</span></span> |<span data-ttu-id="3c032-209">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-210">**출력2**:</span><span class="sxs-lookup"><span data-stu-id="3c032-210">**Output2**:</span></span>

| <span data-ttu-id="3c032-211">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-211">Make</span></span> | <span data-ttu-id="3c032-212">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-212">Time</span></span> | <span data-ttu-id="3c032-213">개수</span><span class="sxs-lookup"><span data-stu-id="3c032-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-214">Toyota</span></span> |<span data-ttu-id="3c032-215">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="3c032-216">3</span><span class="sxs-lookup"><span data-stu-id="3c032-216">3</span></span> |

<span data-ttu-id="3c032-217">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="3c032-218">**설명은**: hello **INTO** 절이이 문에의 hello toowrite hello 데이터 toofrom 출력 하는 스트림 분석을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="3c032-219">hello 첫 번째 쿼리는 이름을 tooan 출력을 수신 했습니다. hello 데이터의 통과 **ArchiveOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="3c032-220">hello 두 번째 쿼리는 몇 가지 간단한 집계 및 필터링 및 그 hello 결과 tooa 다운스트림 경고 시스템으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="3c032-221">참고 hello 공통 테이블 식 (Cte)의 hello 결과 다시 사용할 수도 있습니다 (예: **WITH** 문) 여러 출력 문에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="3c032-222">이 옵션에는 추가적인된 이점을 더 적은 판독기 toohello 입력된 소스를 열어 hello에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="3c032-223">예:</span><span class="sxs-lookup"><span data-stu-id="3c032-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="3c032-224">쿼리 예제: 고유 값 계산</span><span class="sxs-lookup"><span data-stu-id="3c032-224">Query example: Count unique values</span></span>
<span data-ttu-id="3c032-225">**설명**: hello hello 스트림의 시간 창 내에서 표시 되는 고유 필드 값 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="3c032-226">예를 들어 개수 고유 하 게 2 초 창의 hello 요금 소 창구를 통과 하는 자동차의 사항</span><span class="sxs-lookup"><span data-stu-id="3c032-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="3c032-227">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-227">**Input**:</span></span>

| <span data-ttu-id="3c032-228">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-228">Make</span></span> | <span data-ttu-id="3c032-229">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-230">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-230">Honda</span></span> |<span data-ttu-id="3c032-231">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-232">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-232">Honda</span></span> |<span data-ttu-id="3c032-233">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-234">Toyota</span></span> |<span data-ttu-id="3c032-235">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-236">Toyota</span></span> |<span data-ttu-id="3c032-237">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-238">Toyota</span></span> |<span data-ttu-id="3c032-239">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3c032-240">**출력:**</span><span class="sxs-lookup"><span data-stu-id="3c032-240">**Output:**</span></span>

| <span data-ttu-id="3c032-241">개수</span><span class="sxs-lookup"><span data-stu-id="3c032-241">Count</span></span> | <span data-ttu-id="3c032-242">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-243">2</span><span class="sxs-lookup"><span data-stu-id="3c032-243">2</span></span> |<span data-ttu-id="3c032-244">2015-01-01T00:오전 12:02.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="3c032-245">1</span><span class="sxs-lookup"><span data-stu-id="3c032-245">1</span></span> |<span data-ttu-id="3c032-246">2015-01-01T00:오전 12:04.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="3c032-247">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="3c032-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="3c032-248">**설명:**
**COUNT (DISTINCT 확인)** 반환 hello hello에 고유 값 수가 **확인** 시간 창 내의 열입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="3c032-249">쿼리 예제: 값이 변경되었는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="3c032-250">**설명**: hello 현재 값과 다른 경우에 이전 값 toodetermine를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="3c032-251">예를 들어 켜져 hello 이전 자동차 hello 현재 자동차 만드는 동일 hello 유료도로 hello?</span><span class="sxs-lookup"><span data-stu-id="3c032-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="3c032-252">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-252">**Input**:</span></span>

| <span data-ttu-id="3c032-253">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-253">Make</span></span> | <span data-ttu-id="3c032-254">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-255">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-255">Honda</span></span> |<span data-ttu-id="3c032-256">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-257">Toyota</span></span> |<span data-ttu-id="3c032-258">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="3c032-259">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-259">**Output**:</span></span>

| <span data-ttu-id="3c032-260">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-260">Make</span></span> | <span data-ttu-id="3c032-261">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-262">Toyota</span></span> |<span data-ttu-id="3c032-263">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="3c032-264">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="3c032-265">**설명은**: 사용 **지연** toopeek hello에 하나의 이벤트 다시 스트림 입력과 hello 가져올 **확인** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="3c032-266">Toohello 비교 **확인** 다른 경우 hello 현재 이벤트 및 출력 hello 이벤트 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="3c032-267">쿼리 예제: 찾기 hello 창에서 첫 번째 이벤트</span><span class="sxs-lookup"><span data-stu-id="3c032-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="3c032-268">**설명**: 매 10 분 간격의 찾기 hello 첫 번째 자동차 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="3c032-269">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-269">**Input**:</span></span>

| <span data-ttu-id="3c032-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-270">LicensePlate</span></span> | <span data-ttu-id="3c032-271">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-271">Make</span></span> | <span data-ttu-id="3c032-272">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3c032-273">DXE 5291</span></span> |<span data-ttu-id="3c032-274">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-274">Honda</span></span> |<span data-ttu-id="3c032-275">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3c032-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3c032-276">YZK 5704</span></span> |<span data-ttu-id="3c032-277">Ford</span><span class="sxs-lookup"><span data-stu-id="3c032-277">Ford</span></span> |<span data-ttu-id="3c032-278">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3c032-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="3c032-279">RMV 8282</span></span> |<span data-ttu-id="3c032-280">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-280">Honda</span></span> |<span data-ttu-id="3c032-281">2015-07-27T00:오전 5:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3c032-282">YHN 6970</span></span> |<span data-ttu-id="3c032-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-283">Toyota</span></span> |<span data-ttu-id="3c032-284">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3c032-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3c032-285">VFE 1616</span></span> |<span data-ttu-id="3c032-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-286">Toyota</span></span> |<span data-ttu-id="3c032-287">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3c032-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3c032-288">QYF 9358</span></span> |<span data-ttu-id="3c032-289">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-289">Honda</span></span> |<span data-ttu-id="3c032-290">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3c032-291">MDR 6128</span></span> |<span data-ttu-id="3c032-292">BMW</span><span class="sxs-lookup"><span data-stu-id="3c032-292">BMW</span></span> |<span data-ttu-id="3c032-293">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3c032-294">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-294">**Output**:</span></span>

| <span data-ttu-id="3c032-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-295">LicensePlate</span></span> | <span data-ttu-id="3c032-296">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-296">Make</span></span> | <span data-ttu-id="3c032-297">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3c032-298">DXE 5291</span></span> |<span data-ttu-id="3c032-299">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-299">Honda</span></span> |<span data-ttu-id="3c032-300">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3c032-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3c032-301">QYF 9358</span></span> |<span data-ttu-id="3c032-302">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-302">Honda</span></span> |<span data-ttu-id="3c032-303">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="3c032-304">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="3c032-305">이제 10 분 간격의 hello 문제 및 찾기 hello 첫 번째 자동차 보기는 특정 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="3c032-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-306">LicensePlate</span></span> | <span data-ttu-id="3c032-307">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-307">Make</span></span> | <span data-ttu-id="3c032-308">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3c032-309">DXE 5291</span></span> |<span data-ttu-id="3c032-310">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-310">Honda</span></span> |<span data-ttu-id="3c032-311">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3c032-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3c032-312">YZK 5704</span></span> |<span data-ttu-id="3c032-313">Ford</span><span class="sxs-lookup"><span data-stu-id="3c032-313">Ford</span></span> |<span data-ttu-id="3c032-314">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3c032-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3c032-315">YHN 6970</span></span> |<span data-ttu-id="3c032-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-316">Toyota</span></span> |<span data-ttu-id="3c032-317">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3c032-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3c032-318">QYF 9358</span></span> |<span data-ttu-id="3c032-319">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-319">Honda</span></span> |<span data-ttu-id="3c032-320">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3c032-321">MDR 6128</span></span> |<span data-ttu-id="3c032-322">BMW</span><span class="sxs-lookup"><span data-stu-id="3c032-322">BMW</span></span> |<span data-ttu-id="3c032-323">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3c032-324">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="3c032-325">쿼리 예제: 찾기 hello 창의 마지막 이벤트</span><span class="sxs-lookup"><span data-stu-id="3c032-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="3c032-326">**설명**: 매 10 분 간격의 찾기 hello 마지막 자동차 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="3c032-327">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-327">**Input**:</span></span>

| <span data-ttu-id="3c032-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-328">LicensePlate</span></span> | <span data-ttu-id="3c032-329">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-329">Make</span></span> | <span data-ttu-id="3c032-330">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3c032-331">DXE 5291</span></span> |<span data-ttu-id="3c032-332">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-332">Honda</span></span> |<span data-ttu-id="3c032-333">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3c032-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3c032-334">YZK 5704</span></span> |<span data-ttu-id="3c032-335">Ford</span><span class="sxs-lookup"><span data-stu-id="3c032-335">Ford</span></span> |<span data-ttu-id="3c032-336">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3c032-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="3c032-337">RMV 8282</span></span> |<span data-ttu-id="3c032-338">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-338">Honda</span></span> |<span data-ttu-id="3c032-339">2015-07-27T00:오전 5:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3c032-340">YHN 6970</span></span> |<span data-ttu-id="3c032-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-341">Toyota</span></span> |<span data-ttu-id="3c032-342">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3c032-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3c032-343">VFE 1616</span></span> |<span data-ttu-id="3c032-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-344">Toyota</span></span> |<span data-ttu-id="3c032-345">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3c032-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3c032-346">QYF 9358</span></span> |<span data-ttu-id="3c032-347">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-347">Honda</span></span> |<span data-ttu-id="3c032-348">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3c032-349">MDR 6128</span></span> |<span data-ttu-id="3c032-350">BMW</span><span class="sxs-lookup"><span data-stu-id="3c032-350">BMW</span></span> |<span data-ttu-id="3c032-351">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3c032-352">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-352">**Output**:</span></span>

| <span data-ttu-id="3c032-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-353">LicensePlate</span></span> | <span data-ttu-id="3c032-354">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-354">Make</span></span> | <span data-ttu-id="3c032-355">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3c032-356">VFE 1616</span></span> |<span data-ttu-id="3c032-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-357">Toyota</span></span> |<span data-ttu-id="3c032-358">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3c032-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3c032-359">MDR 6128</span></span> |<span data-ttu-id="3c032-360">BMW</span><span class="sxs-lookup"><span data-stu-id="3c032-360">BMW</span></span> |<span data-ttu-id="3c032-361">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3c032-362">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="3c032-363">**설명은**: hello 쿼리에서 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="3c032-364">hello 첫 번째 하나 찾습니다 hello 최신 타임 스탬프에서 windows 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="3c032-365">두 번째 단계 조인 hello hello hello 각 창에서 마지막 타임 스탬프와 일치 하는 hello 원래 스트림 toofind hello 이벤트와 함께 hello 첫 번째 쿼리의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="3c032-366">쿼리 예: hello 이벤트가 없는 경우를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="3c032-367">**설명**: 스트림에 특정 조건에 일치하지 않는 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="3c032-368">예를 들어 hello 동일 확인의 연속 된 2 자동차 입력 한 hello 유료도로 hello 내에서 마지막 90 초?</span><span class="sxs-lookup"><span data-stu-id="3c032-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="3c032-369">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-369">**Input**:</span></span>

| <span data-ttu-id="3c032-370">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-370">Make</span></span> | <span data-ttu-id="3c032-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-371">LicensePlate</span></span> | <span data-ttu-id="3c032-372">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-373">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-373">Honda</span></span> |<span data-ttu-id="3c032-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3c032-374">ABC-123</span></span> |<span data-ttu-id="3c032-375">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3c032-376">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-376">Honda</span></span> |<span data-ttu-id="3c032-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3c032-377">AAA-999</span></span> |<span data-ttu-id="3c032-378">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3c032-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-379">Toyota</span></span> |<span data-ttu-id="3c032-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="3c032-380">DEF-987</span></span> |<span data-ttu-id="3c032-381">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="3c032-382">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-382">Honda</span></span> |<span data-ttu-id="3c032-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="3c032-383">GHI-345</span></span> |<span data-ttu-id="3c032-384">2015-01-01T00:오전 12:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="3c032-385">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-385">**Output**:</span></span>

| <span data-ttu-id="3c032-386">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-386">Make</span></span> | <span data-ttu-id="3c032-387">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-387">Time</span></span> | <span data-ttu-id="3c032-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="3c032-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="3c032-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="3c032-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="3c032-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="3c032-391">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-391">Honda</span></span> |<span data-ttu-id="3c032-392">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3c032-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3c032-393">AAA-999</span></span> |<span data-ttu-id="3c032-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3c032-394">ABC-123</span></span> |<span data-ttu-id="3c032-395">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="3c032-396">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="3c032-397">**설명은**: 사용 **지연** toopeek hello에 하나의 이벤트 다시 스트림 입력과 hello 가져올 **확인** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="3c032-398">Toohello 비교 **확인** hello 현재 이벤트과 같은 hello는 이러한 경우 출력 hello 이벤트 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="3c032-399">사용할 수도 있습니다 **지연** hello 이전 자동차에 대 한 tooget 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="3c032-400">쿼리 예: 이벤트 사이의 hello 기간 검색</span><span class="sxs-lookup"><span data-stu-id="3c032-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="3c032-401">**설명**: 지정된 된 이벤트의 hello 기간을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="3c032-402">예를 들어 웹 클릭 동향 들어 hello 시간 기능을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="3c032-403">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-403">**Input**:</span></span>  

| <span data-ttu-id="3c032-404">사용자</span><span class="sxs-lookup"><span data-stu-id="3c032-404">User</span></span> | <span data-ttu-id="3c032-405">기능</span><span class="sxs-lookup"><span data-stu-id="3c032-405">Feature</span></span> | <span data-ttu-id="3c032-406">이벤트</span><span class="sxs-lookup"><span data-stu-id="3c032-406">Event</span></span> | <span data-ttu-id="3c032-407">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="3c032-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3c032-408">RightMenu</span></span> |<span data-ttu-id="3c032-409">시작</span><span class="sxs-lookup"><span data-stu-id="3c032-409">Start</span></span> |<span data-ttu-id="3c032-410">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="3c032-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3c032-411">RightMenu</span></span> |<span data-ttu-id="3c032-412">끝</span><span class="sxs-lookup"><span data-stu-id="3c032-412">End</span></span> |<span data-ttu-id="3c032-413">2015-01-01T00:오전 12:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="3c032-414">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-414">**Output**:</span></span>  

| <span data-ttu-id="3c032-415">사용자</span><span class="sxs-lookup"><span data-stu-id="3c032-415">User</span></span> | <span data-ttu-id="3c032-416">기능</span><span class="sxs-lookup"><span data-stu-id="3c032-416">Feature</span></span> | <span data-ttu-id="3c032-417">기간</span><span class="sxs-lookup"><span data-stu-id="3c032-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="3c032-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3c032-418">RightMenu</span></span> |<span data-ttu-id="3c032-419">7</span><span class="sxs-lookup"><span data-stu-id="3c032-419">7</span></span> |

<span data-ttu-id="3c032-420">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="3c032-421">**설명은**: 사용 하 여 hello **마지막** 마지막 tooretrieve hello 함수 **시간** hello 이벤트 형식이 값 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="3c032-422">hello **마지막** 함수는 **PARTITION BY [사용자]** 고유 사용자 당 결과 hello tooindicate 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="3c032-423">hello 쿼리에 1 시간 사이의 시간 차이 hello에 대 한 최대 임계값 **시작** 및 **중지** 이벤트, 필요에 따라 구성할 수 있지만 **(제한 DURATION(hour, 1)**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="3c032-424">쿼리 예: 검색 조건의 hello 기간</span><span class="sxs-lookup"><span data-stu-id="3c032-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="3c032-425">**설명**: 조건이 발생한 기간을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="3c032-426">예를 들어 버그가 생겨서 모든 자동차의 중량이 정확하지 않은 경우(20,000파운드 이상) 를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="3c032-427">Hello 버그의 toocompute hello 기간을 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="3c032-428">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-428">**Input**:</span></span>

| <span data-ttu-id="3c032-429">계정을</span><span class="sxs-lookup"><span data-stu-id="3c032-429">Make</span></span> | <span data-ttu-id="3c032-430">Time</span><span class="sxs-lookup"><span data-stu-id="3c032-430">Time</span></span> | <span data-ttu-id="3c032-431">무게</span><span class="sxs-lookup"><span data-stu-id="3c032-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-432">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-432">Honda</span></span> |<span data-ttu-id="3c032-433">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="3c032-434">2000</span><span class="sxs-lookup"><span data-stu-id="3c032-434">2000</span></span> |
| <span data-ttu-id="3c032-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-435">Toyota</span></span> |<span data-ttu-id="3c032-436">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3c032-437">25000</span><span class="sxs-lookup"><span data-stu-id="3c032-437">25000</span></span> |
| <span data-ttu-id="3c032-438">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-438">Honda</span></span> |<span data-ttu-id="3c032-439">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="3c032-440">26000</span><span class="sxs-lookup"><span data-stu-id="3c032-440">26000</span></span> |
| <span data-ttu-id="3c032-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-441">Toyota</span></span> |<span data-ttu-id="3c032-442">2015-01-01T00:오전 12:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="3c032-443">25000</span><span class="sxs-lookup"><span data-stu-id="3c032-443">25000</span></span> |
| <span data-ttu-id="3c032-444">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-444">Honda</span></span> |<span data-ttu-id="3c032-445">2015-01-01T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="3c032-446">26000</span><span class="sxs-lookup"><span data-stu-id="3c032-446">26000</span></span> |
| <span data-ttu-id="3c032-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-447">Toyota</span></span> |<span data-ttu-id="3c032-448">2015-01-01T00:오전 12:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="3c032-449">25000</span><span class="sxs-lookup"><span data-stu-id="3c032-449">25000</span></span> |
| <span data-ttu-id="3c032-450">Honda</span><span class="sxs-lookup"><span data-stu-id="3c032-450">Honda</span></span> |<span data-ttu-id="3c032-451">2015-01-01T00:오전 12:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="3c032-452">26000</span><span class="sxs-lookup"><span data-stu-id="3c032-452">26000</span></span> |
| <span data-ttu-id="3c032-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="3c032-453">Toyota</span></span> |<span data-ttu-id="3c032-454">2015-01-01T00:오전 12:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="3c032-455">2000</span><span class="sxs-lookup"><span data-stu-id="3c032-455">2000</span></span> |

<span data-ttu-id="3c032-456">**출력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-456">**Output**:</span></span>

| <span data-ttu-id="3c032-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="3c032-457">StartFault</span></span> | <span data-ttu-id="3c032-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="3c032-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-459">2015-01-01T00:오전 12:02.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="3c032-460">2015-01-01T00:오전 12:07.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="3c032-461">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="3c032-462">**설명은**: 사용 **지연** 을 24 시간 동안 tooview hello 입력된 스트림을 열고 where 인스턴스 **StartFault** 및 **StopFault** hello에 의해 확장 되는 < 20000 가중치를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="3c032-463">쿼리 예제: 누락된 값 입력</span><span class="sxs-lookup"><span data-stu-id="3c032-463">Query example: Fill missing values</span></span>
<span data-ttu-id="3c032-464">**설명**: hello 스트림의 값이 누락 된 이벤트의 경우 정기적으로 포함 된 이벤트 스트림을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="3c032-465">예를 들어 hello 가장 최근에 표시 데이터 요소를 보고 하는 이벤트 5 초 마다를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="3c032-466">**입력**:</span><span class="sxs-lookup"><span data-stu-id="3c032-466">**Input**:</span></span>

| <span data-ttu-id="3c032-467">t</span><span class="sxs-lookup"><span data-stu-id="3c032-467">t</span></span> | <span data-ttu-id="3c032-468">value</span><span class="sxs-lookup"><span data-stu-id="3c032-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="3c032-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="3c032-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="3c032-470">1</span><span class="sxs-lookup"><span data-stu-id="3c032-470">1</span></span> |
| <span data-ttu-id="3c032-471">"2014-01-01T06:오전 1:05"</span><span class="sxs-lookup"><span data-stu-id="3c032-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="3c032-472">2</span><span class="sxs-lookup"><span data-stu-id="3c032-472">2</span></span> |
| <span data-ttu-id="3c032-473">"2014-01-01T06:오전 1:10"</span><span class="sxs-lookup"><span data-stu-id="3c032-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="3c032-474">3</span><span class="sxs-lookup"><span data-stu-id="3c032-474">3</span></span> |
| <span data-ttu-id="3c032-475">"2014-01-01T06:오전 1:15"</span><span class="sxs-lookup"><span data-stu-id="3c032-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="3c032-476">4</span><span class="sxs-lookup"><span data-stu-id="3c032-476">4</span></span> |
| <span data-ttu-id="3c032-477">"2014-01-01T06:오전 1:30"</span><span class="sxs-lookup"><span data-stu-id="3c032-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="3c032-478">5</span><span class="sxs-lookup"><span data-stu-id="3c032-478">5</span></span> |
| <span data-ttu-id="3c032-479">"2014-01-01T06:오전 1:35"</span><span class="sxs-lookup"><span data-stu-id="3c032-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="3c032-480">6</span><span class="sxs-lookup"><span data-stu-id="3c032-480">6</span></span> |

<span data-ttu-id="3c032-481">**출력(처음 10개 행)**:</span><span class="sxs-lookup"><span data-stu-id="3c032-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="3c032-482">windowend</span><span class="sxs-lookup"><span data-stu-id="3c032-482">windowend</span></span> | <span data-ttu-id="3c032-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="3c032-483">lastevent.t</span></span> | <span data-ttu-id="3c032-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="3c032-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c032-485">2014-01-01T14:오전 1:00.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="3c032-486">2014-01-01T14:오전 1:00.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="3c032-487">1</span><span class="sxs-lookup"><span data-stu-id="3c032-487">1</span></span> |
| <span data-ttu-id="3c032-488">2014-01-01T14:오전 1:05.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="3c032-489">2014-01-01T14:오전 1:05.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="3c032-490">2</span><span class="sxs-lookup"><span data-stu-id="3c032-490">2</span></span> |
| <span data-ttu-id="3c032-491">2014-01-01T14:오전 1:10.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="3c032-492">2014-01-01T14:오전 1:10.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="3c032-493">3</span><span class="sxs-lookup"><span data-stu-id="3c032-493">3</span></span> |
| <span data-ttu-id="3c032-494">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3c032-495">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3c032-496">4</span><span class="sxs-lookup"><span data-stu-id="3c032-496">4</span></span> |
| <span data-ttu-id="3c032-497">2014-01-01T14:오전 1:20.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="3c032-498">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3c032-499">4</span><span class="sxs-lookup"><span data-stu-id="3c032-499">4</span></span> |
| <span data-ttu-id="3c032-500">2014-01-01T14:오전 1:25.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="3c032-501">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3c032-502">4</span><span class="sxs-lookup"><span data-stu-id="3c032-502">4</span></span> |
| <span data-ttu-id="3c032-503">2014-01-01T14:오전 1:30.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="3c032-504">2014-01-01T14:오전 1:30.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="3c032-505">5</span><span class="sxs-lookup"><span data-stu-id="3c032-505">5</span></span> |
| <span data-ttu-id="3c032-506">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3c032-507">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3c032-508">6</span><span class="sxs-lookup"><span data-stu-id="3c032-508">6</span></span> |
| <span data-ttu-id="3c032-509">2014-01-01T14:오전 1:40.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="3c032-510">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3c032-511">6</span><span class="sxs-lookup"><span data-stu-id="3c032-511">6</span></span> |
| <span data-ttu-id="3c032-512">2014-01-01T14:오전 1:45.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="3c032-513">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3c032-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3c032-514">6</span><span class="sxs-lookup"><span data-stu-id="3c032-514">6</span></span> |

<span data-ttu-id="3c032-515">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="3c032-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="3c032-516">**설명은**:이 쿼리가 5 초 마다 이벤트를 생성 하 고 출력 hello 이전에 수신 된 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="3c032-517">hello [도약 창](https://msdn.microsoft.com/library/dn835041.aspx "Azure Stream Analytics 도약 창-") 기간 백 hello 쿼리 toofind hello 최신 이벤트 (이 예제의 300 초)을 검색 하는 정도 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c032-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="3c032-518">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="3c032-518">Get help</span></span>
<span data-ttu-id="3c032-519">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c032-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c032-520">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c032-520">Next steps</span></span>
* [<span data-ttu-id="3c032-521">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="3c032-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3c032-522">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="3c032-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3c032-523">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="3c032-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3c032-524">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="3c032-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3c032-525">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="3c032-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

