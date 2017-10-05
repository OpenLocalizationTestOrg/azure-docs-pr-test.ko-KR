---
title: "일반적인 Stream Analytics 사용 패턴에 대한 쿼리 예제 | Microsoft Docs"
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="c5b4e-104">일반적인 Stream Analytics 사용 패턴에 대한 쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="c5b4e-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="c5b4e-105">소개</span><span class="sxs-lookup"><span data-stu-id="c5b4e-105">Introduction</span></span>
<span data-ttu-id="c5b4e-106">Azure Stream Analytics에서 쿼리는 SQL 방식 쿼리 언어로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="c5b4e-107">이러한 쿼리는 [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx) 가이드에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="c5b4e-108">이 문서에서는 실제 시나리오에 따른 몇 가지 일반적인 쿼리 패턴에 대한 솔루션을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="c5b4e-109">이 작업은 진행 중이며 새 패턴이 지속적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="c5b4e-110">쿼리 예제: 데이터 형식 변환</span><span class="sxs-lookup"><span data-stu-id="c5b4e-110">Query example: Convert data types</span></span>
<span data-ttu-id="c5b4e-111">**설명**: 입력 스트림의 속성 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="c5b4e-112">예를 들어 자동차 무게가 입력 스트림에 문자열 형식으로 설정되면 **합계**를 수행하기 위해 **INT**로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="c5b4e-113">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-113">**Input**:</span></span>

| <span data-ttu-id="c5b4e-114">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-114">Make</span></span> | <span data-ttu-id="c5b4e-115">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-115">Time</span></span> | <span data-ttu-id="c5b4e-116">무게</span><span class="sxs-lookup"><span data-stu-id="c5b4e-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-117">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-117">Honda</span></span> |<span data-ttu-id="c5b4e-118">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="c5b4e-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-119">"1000"</span></span> |
| <span data-ttu-id="c5b4e-120">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-120">Honda</span></span> |<span data-ttu-id="c5b4e-121">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="c5b4e-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-122">"2000"</span></span> |

<span data-ttu-id="c5b4e-123">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-123">**Output**:</span></span>

| <span data-ttu-id="c5b4e-124">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-124">Make</span></span> | <span data-ttu-id="c5b4e-125">무게</span><span class="sxs-lookup"><span data-stu-id="c5b4e-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-126">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-126">Honda</span></span> |<span data-ttu-id="c5b4e-127">3000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-127">3000</span></span> |

<span data-ttu-id="c5b4e-128">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="c5b4e-129">**설명**: **무게** 필드에서 **CAST** 문을 사용하여 해당 데이터 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="c5b4e-130">[데이터 형식(Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx)에서 지원되는 데이터 형식의 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="c5b4e-131">쿼리 예제: 패턴을 일치시키기 위해 Like/Not like를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="c5b4e-132">**설명**: 이벤트의 필드 값이 특정 패턴과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="c5b4e-133">예를 들어 결과가 A로 시작하고 9로 끝나는 번호판을 반환하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="c5b4e-134">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-134">**Input**:</span></span>

| <span data-ttu-id="c5b4e-135">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-135">Make</span></span> | <span data-ttu-id="c5b4e-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-136">LicensePlate</span></span> | <span data-ttu-id="c5b4e-137">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-138">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-138">Honda</span></span> |<span data-ttu-id="c5b4e-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="c5b4e-139">ABC-123</span></span> |<span data-ttu-id="c5b4e-140">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-141">Toyota</span></span> |<span data-ttu-id="c5b4e-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="c5b4e-142">AAA-999</span></span> |<span data-ttu-id="c5b4e-143">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="c5b4e-144">Nissan</span></span> |<span data-ttu-id="c5b4e-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="c5b4e-145">ABC-369</span></span> |<span data-ttu-id="c5b4e-146">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-147">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-147">**Output**:</span></span>

| <span data-ttu-id="c5b4e-148">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-148">Make</span></span> | <span data-ttu-id="c5b4e-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-149">LicensePlate</span></span> | <span data-ttu-id="c5b4e-150">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-151">Toyota</span></span> |<span data-ttu-id="c5b4e-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="c5b4e-152">AAA-999</span></span> |<span data-ttu-id="c5b4e-153">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="c5b4e-154">Nissan</span></span> |<span data-ttu-id="c5b4e-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="c5b4e-155">ABC-369</span></span> |<span data-ttu-id="c5b4e-156">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-157">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="c5b4e-158">**설명**: **LIKE** 문을 사용하여 **LicensePlate** 필드 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="c5b4e-159">A로 시작한 다음 0개 이상의 문자열을 포함하고 a9로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="c5b4e-160">쿼리 예제: 다른 사례/값(CASE 문)에 대한 논리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="c5b4e-161">**설명**: 특정 조건에 따라 필드에 대해 다른 계산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="c5b4e-162">예를 들어 1이라는 특수 사례를 가진 동일한 브랜드의 차가 몇 대 통과했는지에 대한 문자열 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="c5b4e-163">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-163">**Input**:</span></span>

| <span data-ttu-id="c5b4e-164">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-164">Make</span></span> | <span data-ttu-id="c5b4e-165">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-166">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-166">Honda</span></span> |<span data-ttu-id="c5b4e-167">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-168">Toyota</span></span> |<span data-ttu-id="c5b4e-169">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-170">Toyota</span></span> |<span data-ttu-id="c5b4e-171">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-172">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-172">**Output**:</span></span>

| <span data-ttu-id="c5b4e-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="c5b4e-173">CarsPassed</span></span> | <span data-ttu-id="c5b4e-174">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-175">1 Honda</span></span> |<span data-ttu-id="c5b4e-176">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="c5b4e-177">2 Toyotas</span></span> |<span data-ttu-id="c5b4e-178">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="c5b4e-179">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-179">**Solution**:</span></span>

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

<span data-ttu-id="c5b4e-180">**설명**: **CASE** 절을 사용하면 일부 조건에 따른 다른 계산을 제공할 수 있습니다(이 경우에는 집계 창에 있는 자동차의 수).</span><span class="sxs-lookup"><span data-stu-id="c5b4e-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="c5b4e-181">쿼리 예제: 데이터를 여러 출력으로 보내기</span><span class="sxs-lookup"><span data-stu-id="c5b4e-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="c5b4e-182">**설명**: 데이터를 단일 작업에서 여러 출력 대상으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="c5b4e-183">예를 들어 임계점 기반 경고에 대한 데이터를 분석하고 Blob 저장소에 모든 이벤트를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="c5b4e-184">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-184">**Input**:</span></span>

| <span data-ttu-id="c5b4e-185">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-185">Make</span></span> | <span data-ttu-id="c5b4e-186">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-187">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-187">Honda</span></span> |<span data-ttu-id="c5b4e-188">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-189">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-189">Honda</span></span> |<span data-ttu-id="c5b4e-190">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-191">Toyota</span></span> |<span data-ttu-id="c5b4e-192">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-193">Toyota</span></span> |<span data-ttu-id="c5b4e-194">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-195">Toyota</span></span> |<span data-ttu-id="c5b4e-196">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-197">**출력1**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-197">**Output1**:</span></span>

| <span data-ttu-id="c5b4e-198">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-198">Make</span></span> | <span data-ttu-id="c5b4e-199">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-200">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-200">Honda</span></span> |<span data-ttu-id="c5b4e-201">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-202">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-202">Honda</span></span> |<span data-ttu-id="c5b4e-203">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-204">Toyota</span></span> |<span data-ttu-id="c5b4e-205">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-206">Toyota</span></span> |<span data-ttu-id="c5b4e-207">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-208">Toyota</span></span> |<span data-ttu-id="c5b4e-209">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-210">**출력2**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-210">**Output2**:</span></span>

| <span data-ttu-id="c5b4e-211">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-211">Make</span></span> | <span data-ttu-id="c5b4e-212">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-212">Time</span></span> | <span data-ttu-id="c5b4e-213">개수</span><span class="sxs-lookup"><span data-stu-id="c5b4e-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-214">Toyota</span></span> |<span data-ttu-id="c5b4e-215">2015-01-01T00:오전 12:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="c5b4e-216">3</span><span class="sxs-lookup"><span data-stu-id="c5b4e-216">3</span></span> |

<span data-ttu-id="c5b4e-217">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-217">**Solution**:</span></span>

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

<span data-ttu-id="c5b4e-218">**설명**: **INTO** 절은 이 문의 데이터를 어떤 출력에 쓸 것인지에 대한 Stream Analytics을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="c5b4e-219">첫 번째 쿼리는 **ArchiveOutput**이라고 지정한 출력에 받은 통과한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="c5b4e-220">두 번째 쿼리는 일부 간단한 집계와 필터링을 하고 다운스트림 경고 시스템에 결과를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="c5b4e-221">여러 출력 문에서 공통 테이블 식(CTE)(예: **WITH** 문)의 결과를 다시 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="c5b4e-222">이 옵션에는 입력 원본에 대해 더 적은 독자를 여는 추가 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="c5b4e-223">예:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="c5b4e-224">쿼리 예제: 고유 값 계산</span><span class="sxs-lookup"><span data-stu-id="c5b4e-224">Query example: Count unique values</span></span>
<span data-ttu-id="c5b4e-225">**설명**: 시간 창 안의 스트림에 나타나는 고유 필드 값 개수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="c5b4e-226">예를 들어 2초 안에 톨게이트 요금소를 통과한 자동차의 고유한 브랜드는 몇 개입니까?</span><span class="sxs-lookup"><span data-stu-id="c5b4e-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="c5b4e-227">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-227">**Input**:</span></span>

| <span data-ttu-id="c5b4e-228">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-228">Make</span></span> | <span data-ttu-id="c5b4e-229">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-230">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-230">Honda</span></span> |<span data-ttu-id="c5b4e-231">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-232">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-232">Honda</span></span> |<span data-ttu-id="c5b4e-233">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-234">Toyota</span></span> |<span data-ttu-id="c5b4e-235">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-236">Toyota</span></span> |<span data-ttu-id="c5b4e-237">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-238">Toyota</span></span> |<span data-ttu-id="c5b4e-239">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="c5b4e-240">**출력:**</span><span class="sxs-lookup"><span data-stu-id="c5b4e-240">**Output:**</span></span>

| <span data-ttu-id="c5b4e-241">개수</span><span class="sxs-lookup"><span data-stu-id="c5b4e-241">Count</span></span> | <span data-ttu-id="c5b4e-242">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-243">2</span><span class="sxs-lookup"><span data-stu-id="c5b4e-243">2</span></span> |<span data-ttu-id="c5b4e-244">2015-01-01T00:오전 12:02.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="c5b4e-245">1</span><span class="sxs-lookup"><span data-stu-id="c5b4e-245">1</span></span> |<span data-ttu-id="c5b4e-246">2015-01-01T00:오전 12:04.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="c5b4e-247">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c5b4e-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="c5b4e-248">**설명:**
**COUNT(DISTINCT Make)**는 특정 기간 내에서 **Make** 열의 고유한 값 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="c5b4e-249">쿼리 예제: 값이 변경되었는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="c5b4e-250">**설명**: 이전 값을 확인하여 현재 값과 다른지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="c5b4e-251">예를 들어 유료 도로의 이전 자동차는 현재 자동차와 동일한 브랜드인가요?</span><span class="sxs-lookup"><span data-stu-id="c5b4e-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="c5b4e-252">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-252">**Input**:</span></span>

| <span data-ttu-id="c5b4e-253">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-253">Make</span></span> | <span data-ttu-id="c5b4e-254">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-255">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-255">Honda</span></span> |<span data-ttu-id="c5b4e-256">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-257">Toyota</span></span> |<span data-ttu-id="c5b4e-258">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="c5b4e-259">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-259">**Output**:</span></span>

| <span data-ttu-id="c5b4e-260">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-260">Make</span></span> | <span data-ttu-id="c5b4e-261">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-262">Toyota</span></span> |<span data-ttu-id="c5b4e-263">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="c5b4e-264">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="c5b4e-265">**설명**: **LAG**를 사용하여 지난 이벤트의 입력 스트림을 살펴보고, **Make** 값을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="c5b4e-266">그런 다음 현재 이벤트와 출력 이벤트의 **Make** 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="c5b4e-267">쿼리 예제: 창에서 첫 번째 이벤트 찾기</span><span class="sxs-lookup"><span data-stu-id="c5b4e-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="c5b4e-268">**설명**: 매 10분 간격으로 첫 번째 자동차를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="c5b4e-269">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-269">**Input**:</span></span>

| <span data-ttu-id="c5b4e-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-270">LicensePlate</span></span> | <span data-ttu-id="c5b4e-271">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-271">Make</span></span> | <span data-ttu-id="c5b4e-272">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="c5b4e-273">DXE 5291</span></span> |<span data-ttu-id="c5b4e-274">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-274">Honda</span></span> |<span data-ttu-id="c5b4e-275">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="c5b4e-276">YZK 5704</span></span> |<span data-ttu-id="c5b4e-277">Ford</span><span class="sxs-lookup"><span data-stu-id="c5b4e-277">Ford</span></span> |<span data-ttu-id="c5b4e-278">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="c5b4e-279">RMV 8282</span></span> |<span data-ttu-id="c5b4e-280">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-280">Honda</span></span> |<span data-ttu-id="c5b4e-281">2015-07-27T00:오전 5:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="c5b4e-282">YHN 6970</span></span> |<span data-ttu-id="c5b4e-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-283">Toyota</span></span> |<span data-ttu-id="c5b4e-284">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="c5b4e-285">VFE 1616</span></span> |<span data-ttu-id="c5b4e-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-286">Toyota</span></span> |<span data-ttu-id="c5b4e-287">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="c5b4e-288">QYF 9358</span></span> |<span data-ttu-id="c5b4e-289">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-289">Honda</span></span> |<span data-ttu-id="c5b4e-290">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="c5b4e-291">MDR 6128</span></span> |<span data-ttu-id="c5b4e-292">BMW</span><span class="sxs-lookup"><span data-stu-id="c5b4e-292">BMW</span></span> |<span data-ttu-id="c5b4e-293">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="c5b4e-294">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-294">**Output**:</span></span>

| <span data-ttu-id="c5b4e-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-295">LicensePlate</span></span> | <span data-ttu-id="c5b4e-296">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-296">Make</span></span> | <span data-ttu-id="c5b4e-297">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="c5b4e-298">DXE 5291</span></span> |<span data-ttu-id="c5b4e-299">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-299">Honda</span></span> |<span data-ttu-id="c5b4e-300">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="c5b4e-301">QYF 9358</span></span> |<span data-ttu-id="c5b4e-302">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-302">Honda</span></span> |<span data-ttu-id="c5b4e-303">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="c5b4e-304">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="c5b4e-305">이제 10분 간격마다 특정 브랜드의 첫 번째 차를 찾도록 문제를 변경해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="c5b4e-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-306">LicensePlate</span></span> | <span data-ttu-id="c5b4e-307">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-307">Make</span></span> | <span data-ttu-id="c5b4e-308">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="c5b4e-309">DXE 5291</span></span> |<span data-ttu-id="c5b4e-310">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-310">Honda</span></span> |<span data-ttu-id="c5b4e-311">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="c5b4e-312">YZK 5704</span></span> |<span data-ttu-id="c5b4e-313">Ford</span><span class="sxs-lookup"><span data-stu-id="c5b4e-313">Ford</span></span> |<span data-ttu-id="c5b4e-314">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="c5b4e-315">YHN 6970</span></span> |<span data-ttu-id="c5b4e-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-316">Toyota</span></span> |<span data-ttu-id="c5b4e-317">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="c5b4e-318">QYF 9358</span></span> |<span data-ttu-id="c5b4e-319">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-319">Honda</span></span> |<span data-ttu-id="c5b4e-320">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="c5b4e-321">MDR 6128</span></span> |<span data-ttu-id="c5b4e-322">BMW</span><span class="sxs-lookup"><span data-stu-id="c5b4e-322">BMW</span></span> |<span data-ttu-id="c5b4e-323">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="c5b4e-324">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="c5b4e-325">쿼리 예제: 창에서 마지막 이벤트 찾기</span><span class="sxs-lookup"><span data-stu-id="c5b4e-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="c5b4e-326">**설명**: 매 10분 간격마다 마지막 자동차를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="c5b4e-327">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-327">**Input**:</span></span>

| <span data-ttu-id="c5b4e-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-328">LicensePlate</span></span> | <span data-ttu-id="c5b4e-329">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-329">Make</span></span> | <span data-ttu-id="c5b4e-330">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="c5b4e-331">DXE 5291</span></span> |<span data-ttu-id="c5b4e-332">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-332">Honda</span></span> |<span data-ttu-id="c5b4e-333">2015-07-27T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="c5b4e-334">YZK 5704</span></span> |<span data-ttu-id="c5b4e-335">Ford</span><span class="sxs-lookup"><span data-stu-id="c5b4e-335">Ford</span></span> |<span data-ttu-id="c5b4e-336">2015-07-27T00:오전 2:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="c5b4e-337">RMV 8282</span></span> |<span data-ttu-id="c5b4e-338">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-338">Honda</span></span> |<span data-ttu-id="c5b4e-339">2015-07-27T00:오전 5:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="c5b4e-340">YHN 6970</span></span> |<span data-ttu-id="c5b4e-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-341">Toyota</span></span> |<span data-ttu-id="c5b4e-342">2015-07-27T00:오전 6:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="c5b4e-343">VFE 1616</span></span> |<span data-ttu-id="c5b4e-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-344">Toyota</span></span> |<span data-ttu-id="c5b4e-345">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="c5b4e-346">QYF 9358</span></span> |<span data-ttu-id="c5b4e-347">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-347">Honda</span></span> |<span data-ttu-id="c5b4e-348">2015-07-27T00:오후 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="c5b4e-349">MDR 6128</span></span> |<span data-ttu-id="c5b4e-350">BMW</span><span class="sxs-lookup"><span data-stu-id="c5b4e-350">BMW</span></span> |<span data-ttu-id="c5b4e-351">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="c5b4e-352">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-352">**Output**:</span></span>

| <span data-ttu-id="c5b4e-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-353">LicensePlate</span></span> | <span data-ttu-id="c5b4e-354">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-354">Make</span></span> | <span data-ttu-id="c5b4e-355">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="c5b4e-356">VFE 1616</span></span> |<span data-ttu-id="c5b4e-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-357">Toyota</span></span> |<span data-ttu-id="c5b4e-358">2015-07-27T00:오전 9:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="c5b4e-359">MDR 6128</span></span> |<span data-ttu-id="c5b4e-360">BMW</span><span class="sxs-lookup"><span data-stu-id="c5b4e-360">BMW</span></span> |<span data-ttu-id="c5b4e-361">2015-07-27T00:오후 1:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="c5b4e-362">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-362">**Solution**:</span></span>

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

<span data-ttu-id="c5b4e-363">**설명**: 쿼리에서 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="c5b4e-364">첫 번째 단계는 10분 간격으로 최신 타임스탬프를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="c5b4e-365">두 번째 단계는 각 창의 최신 타임스탬프와 일치하는 이벤트를 찾기 위해 원본 스트림을 사용한 첫 번째 쿼리의 결과를 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="c5b4e-366">쿼리 예제: 이벤트의 부재를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="c5b4e-367">**설명**: 스트림에 특정 조건에 일치하지 않는 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="c5b4e-368">예를 들어 최근 90초 이내에 동일한 브랜드의 차 2대가 연속해서 유료 도로로 진입했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="c5b4e-369">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-369">**Input**:</span></span>

| <span data-ttu-id="c5b4e-370">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-370">Make</span></span> | <span data-ttu-id="c5b4e-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-371">LicensePlate</span></span> | <span data-ttu-id="c5b4e-372">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-373">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-373">Honda</span></span> |<span data-ttu-id="c5b4e-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="c5b4e-374">ABC-123</span></span> |<span data-ttu-id="c5b4e-375">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-376">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-376">Honda</span></span> |<span data-ttu-id="c5b4e-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="c5b4e-377">AAA-999</span></span> |<span data-ttu-id="c5b4e-378">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-379">Toyota</span></span> |<span data-ttu-id="c5b4e-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="c5b4e-380">DEF-987</span></span> |<span data-ttu-id="c5b4e-381">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="c5b4e-382">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-382">Honda</span></span> |<span data-ttu-id="c5b4e-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="c5b4e-383">GHI-345</span></span> |<span data-ttu-id="c5b4e-384">2015-01-01T00:오전 12:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="c5b4e-385">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-385">**Output**:</span></span>

| <span data-ttu-id="c5b4e-386">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-386">Make</span></span> | <span data-ttu-id="c5b4e-387">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-387">Time</span></span> | <span data-ttu-id="c5b4e-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="c5b4e-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="c5b4e-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="c5b4e-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="c5b4e-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c5b4e-391">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-391">Honda</span></span> |<span data-ttu-id="c5b4e-392">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="c5b4e-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="c5b4e-393">AAA-999</span></span> |<span data-ttu-id="c5b4e-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="c5b4e-394">ABC-123</span></span> |<span data-ttu-id="c5b4e-395">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="c5b4e-396">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-396">**Solution**:</span></span>

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

<span data-ttu-id="c5b4e-397">**설명**: **LAG**를 사용하여 지난 이벤트의 입력 스트림을 살펴보고, **Make** 값을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="c5b4e-398">현재 이벤트와 출력 이벤트의 **MAKE** 값이 동일한지 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="c5b4e-399">**LAG**를 사용하여 이전 자동차에 대한 데이터를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="c5b4e-400">쿼리 예제: 이벤트 간 기간 검색</span><span class="sxs-lookup"><span data-stu-id="c5b4e-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="c5b4e-401">**설명**: 제공된 이벤트의 기간을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="c5b4e-402">예를 들어 웹 클릭스트림이 지정된 경우 기능에서 소요된 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="c5b4e-403">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-403">**Input**:</span></span>  

| <span data-ttu-id="c5b4e-404">사용자</span><span class="sxs-lookup"><span data-stu-id="c5b4e-404">User</span></span> | <span data-ttu-id="c5b4e-405">기능</span><span class="sxs-lookup"><span data-stu-id="c5b4e-405">Feature</span></span> | <span data-ttu-id="c5b4e-406">이벤트</span><span class="sxs-lookup"><span data-stu-id="c5b4e-406">Event</span></span> | <span data-ttu-id="c5b4e-407">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="c5b4e-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="c5b4e-408">RightMenu</span></span> |<span data-ttu-id="c5b4e-409">시작</span><span class="sxs-lookup"><span data-stu-id="c5b4e-409">Start</span></span> |<span data-ttu-id="c5b4e-410">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="c5b4e-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="c5b4e-411">RightMenu</span></span> |<span data-ttu-id="c5b4e-412">끝</span><span class="sxs-lookup"><span data-stu-id="c5b4e-412">End</span></span> |<span data-ttu-id="c5b4e-413">2015-01-01T00:오전 12:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="c5b4e-414">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-414">**Output**:</span></span>  

| <span data-ttu-id="c5b4e-415">사용자</span><span class="sxs-lookup"><span data-stu-id="c5b4e-415">User</span></span> | <span data-ttu-id="c5b4e-416">기능</span><span class="sxs-lookup"><span data-stu-id="c5b4e-416">Feature</span></span> | <span data-ttu-id="c5b4e-417">기간</span><span class="sxs-lookup"><span data-stu-id="c5b4e-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="c5b4e-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="c5b4e-418">RightMenu</span></span> |<span data-ttu-id="c5b4e-419">7</span><span class="sxs-lookup"><span data-stu-id="c5b4e-419">7</span></span> |

<span data-ttu-id="c5b4e-420">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="c5b4e-421">**설명**: **LAST** 함수를 사용하여 이벤트 유형이 **Start**였을 때 마지막 **시간** 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="c5b4e-422">**LAST** 함수는 **PARTITION BY [사용자]**를 사용하여 고유한 사용자마다 결과가 계산된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="c5b4e-423">쿼리에 **Start**와 **Stop** 이벤트 간 시간 차이를 위해 최대 1시간의 임계값이 있지만 필요에 따라 구성 가능합니다**(LIMIT DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="c5b4e-424">쿼리 예제: 조건의 기간 감지</span><span class="sxs-lookup"><span data-stu-id="c5b4e-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="c5b4e-425">**설명**: 조건이 발생한 기간을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="c5b4e-426">예를 들어 버그가 생겨서 모든 자동차의 중량이 정확하지 않은 경우(20,000파운드 이상) 를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="c5b4e-427">버그의 기간을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="c5b4e-428">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-428">**Input**:</span></span>

| <span data-ttu-id="c5b4e-429">계정을</span><span class="sxs-lookup"><span data-stu-id="c5b4e-429">Make</span></span> | <span data-ttu-id="c5b4e-430">Time</span><span class="sxs-lookup"><span data-stu-id="c5b4e-430">Time</span></span> | <span data-ttu-id="c5b4e-431">무게</span><span class="sxs-lookup"><span data-stu-id="c5b4e-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-432">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-432">Honda</span></span> |<span data-ttu-id="c5b4e-433">2015-01-01T00:오전 12:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="c5b4e-434">2000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-434">2000</span></span> |
| <span data-ttu-id="c5b4e-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-435">Toyota</span></span> |<span data-ttu-id="c5b4e-436">2015-01-01T00:오전 12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="c5b4e-437">25000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-437">25000</span></span> |
| <span data-ttu-id="c5b4e-438">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-438">Honda</span></span> |<span data-ttu-id="c5b4e-439">2015-01-01T00:오전 12:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="c5b4e-440">26000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-440">26000</span></span> |
| <span data-ttu-id="c5b4e-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-441">Toyota</span></span> |<span data-ttu-id="c5b4e-442">2015-01-01T00:오전 12:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="c5b4e-443">25000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-443">25000</span></span> |
| <span data-ttu-id="c5b4e-444">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-444">Honda</span></span> |<span data-ttu-id="c5b4e-445">2015-01-01T00:오전 12:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="c5b4e-446">26000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-446">26000</span></span> |
| <span data-ttu-id="c5b4e-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-447">Toyota</span></span> |<span data-ttu-id="c5b4e-448">2015-01-01T00:오전 12:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="c5b4e-449">25000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-449">25000</span></span> |
| <span data-ttu-id="c5b4e-450">Honda</span><span class="sxs-lookup"><span data-stu-id="c5b4e-450">Honda</span></span> |<span data-ttu-id="c5b4e-451">2015-01-01T00:오전 12:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="c5b4e-452">26000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-452">26000</span></span> |
| <span data-ttu-id="c5b4e-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="c5b4e-453">Toyota</span></span> |<span data-ttu-id="c5b4e-454">2015-01-01T00:오전 12:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="c5b4e-455">2000</span><span class="sxs-lookup"><span data-stu-id="c5b4e-455">2000</span></span> |

<span data-ttu-id="c5b4e-456">**출력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-456">**Output**:</span></span>

| <span data-ttu-id="c5b4e-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="c5b4e-457">StartFault</span></span> | <span data-ttu-id="c5b4e-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="c5b4e-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-459">2015-01-01T00:오전 12:02.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="c5b4e-460">2015-01-01T00:오전 12:07.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="c5b4e-461">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-461">**Solution**:</span></span>

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

<span data-ttu-id="c5b4e-462">**설명**: **LAG**를 사용하여 24시간 동안 입력 스트림을 보고 **StartFault**와 **StopFault**가 가중치 < 20000인 인스턴스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="c5b4e-463">쿼리 예제: 누락된 값 입력</span><span class="sxs-lookup"><span data-stu-id="c5b4e-463">Query example: Fill missing values</span></span>
<span data-ttu-id="c5b4e-464">**설명**: 누락된 값이 있는 이벤트 스트림의 경우 정기적으로 이벤트 스트림을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="c5b4e-465">예를 들어, 가장 최근 표시된 데이터 지점을 보고하도록 5초마다 이벤트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="c5b4e-466">**입력**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-466">**Input**:</span></span>

| <span data-ttu-id="c5b4e-467">t</span><span class="sxs-lookup"><span data-stu-id="c5b4e-467">t</span></span> | <span data-ttu-id="c5b4e-468">value</span><span class="sxs-lookup"><span data-stu-id="c5b4e-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="c5b4e-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="c5b4e-470">1</span><span class="sxs-lookup"><span data-stu-id="c5b4e-470">1</span></span> |
| <span data-ttu-id="c5b4e-471">"2014-01-01T06:오전 1:05"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="c5b4e-472">2</span><span class="sxs-lookup"><span data-stu-id="c5b4e-472">2</span></span> |
| <span data-ttu-id="c5b4e-473">"2014-01-01T06:오전 1:10"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="c5b4e-474">3</span><span class="sxs-lookup"><span data-stu-id="c5b4e-474">3</span></span> |
| <span data-ttu-id="c5b4e-475">"2014-01-01T06:오전 1:15"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="c5b4e-476">4</span><span class="sxs-lookup"><span data-stu-id="c5b4e-476">4</span></span> |
| <span data-ttu-id="c5b4e-477">"2014-01-01T06:오전 1:30"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="c5b4e-478">5</span><span class="sxs-lookup"><span data-stu-id="c5b4e-478">5</span></span> |
| <span data-ttu-id="c5b4e-479">"2014-01-01T06:오전 1:35"</span><span class="sxs-lookup"><span data-stu-id="c5b4e-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="c5b4e-480">6</span><span class="sxs-lookup"><span data-stu-id="c5b4e-480">6</span></span> |

<span data-ttu-id="c5b4e-481">**출력(처음 10개 행)**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="c5b4e-482">windowend</span><span class="sxs-lookup"><span data-stu-id="c5b4e-482">windowend</span></span> | <span data-ttu-id="c5b4e-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="c5b4e-483">lastevent.t</span></span> | <span data-ttu-id="c5b4e-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="c5b4e-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5b4e-485">2014-01-01T14:오전 1:00.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="c5b4e-486">2014-01-01T14:오전 1:00.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="c5b4e-487">1</span><span class="sxs-lookup"><span data-stu-id="c5b4e-487">1</span></span> |
| <span data-ttu-id="c5b4e-488">2014-01-01T14:오전 1:05.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="c5b4e-489">2014-01-01T14:오전 1:05.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="c5b4e-490">2</span><span class="sxs-lookup"><span data-stu-id="c5b4e-490">2</span></span> |
| <span data-ttu-id="c5b4e-491">2014-01-01T14:오전 1:10.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="c5b4e-492">2014-01-01T14:오전 1:10.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="c5b4e-493">3</span><span class="sxs-lookup"><span data-stu-id="c5b4e-493">3</span></span> |
| <span data-ttu-id="c5b4e-494">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="c5b4e-495">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="c5b4e-496">4</span><span class="sxs-lookup"><span data-stu-id="c5b4e-496">4</span></span> |
| <span data-ttu-id="c5b4e-497">2014-01-01T14:오전 1:20.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="c5b4e-498">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="c5b4e-499">4</span><span class="sxs-lookup"><span data-stu-id="c5b4e-499">4</span></span> |
| <span data-ttu-id="c5b4e-500">2014-01-01T14:오전 1:25.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="c5b4e-501">2014-01-01T14:오전 1:15.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="c5b4e-502">4</span><span class="sxs-lookup"><span data-stu-id="c5b4e-502">4</span></span> |
| <span data-ttu-id="c5b4e-503">2014-01-01T14:오전 1:30.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="c5b4e-504">2014-01-01T14:오전 1:30.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="c5b4e-505">5</span><span class="sxs-lookup"><span data-stu-id="c5b4e-505">5</span></span> |
| <span data-ttu-id="c5b4e-506">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="c5b4e-507">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="c5b4e-508">6</span><span class="sxs-lookup"><span data-stu-id="c5b4e-508">6</span></span> |
| <span data-ttu-id="c5b4e-509">2014-01-01T14:오전 1:40.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="c5b4e-510">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="c5b4e-511">6</span><span class="sxs-lookup"><span data-stu-id="c5b4e-511">6</span></span> |
| <span data-ttu-id="c5b4e-512">2014-01-01T14:오전 1:45.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="c5b4e-513">2014-01-01T14:오전 1:35.000Z</span><span class="sxs-lookup"><span data-stu-id="c5b4e-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="c5b4e-514">6</span><span class="sxs-lookup"><span data-stu-id="c5b4e-514">6</span></span> |

<span data-ttu-id="c5b4e-515">**솔루션**:</span><span class="sxs-lookup"><span data-stu-id="c5b4e-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="c5b4e-516">**설명**: 이 쿼리는 5초마다 이벤트를 생성하고 이전에 수신했던 마지막 이벤트를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="c5b4e-517">[도약 창](https://msdn.microsoft.com/library/dn835041.aspx "도약 창 - Azure Stream Analytics") 기간은 쿼리가 마지막 이벤트를 찾는 데 얼마나 돌아가야 하는지를 결정합니다(이 예에서는 300초).</span><span class="sxs-lookup"><span data-stu-id="c5b4e-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="c5b4e-518">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="c5b4e-518">Get help</span></span>
<span data-ttu-id="c5b4e-519">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5b4e-520">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5b4e-520">Next steps</span></span>
* [<span data-ttu-id="c5b4e-521">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="c5b4e-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c5b4e-522">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="c5b4e-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c5b4e-523">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="c5b4e-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c5b4e-524">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="c5b4e-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c5b4e-525">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c5b4e-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

