---
title: "Azure Stream Analytics 문제 해결 가이드 | Microsoft Docs"
description: "Stream Analytics 작업 문제를 해결하는 방법"
keywords: "문제 해결 가이드"
documentationcenter: 
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 8ecf279047f06691cef1bc0db06888974405a9f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a><span data-ttu-id="db610-104">Azure Stream Analytics 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="db610-104">Troubleshooting guide for Azure Stream Analytics</span></span>

<span data-ttu-id="db610-105">Azure Stream Analytics 문제 해결은 언뜻 보기에 복잡한 노력이 필요한 것처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-105">Azure Stream Analytics troubleshooting can appear to be a complex effort at first glance.</span></span> <span data-ttu-id="db610-106">여러 사용자가 작업을 한 후에 프로세스를 간소화하고 입력, 출력, 쿼리 및 함수에 대한 추측을 제거하는 데 도움이 되도록 이 가이드를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-106">After working with many users, we have created this guide to help streamline the process and remove the guesswork about your inputs, outputs, queries, and functions.</span></span>

## <a name="troubleshoot-your-stream-analytics-job"></a><span data-ttu-id="db610-107">Stream Analytics 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="db610-107">Troubleshoot your Stream Analytics job</span></span>

<span data-ttu-id="db610-108">Stream Analytics 작업 문제 해결에서 최상의 결과를 얻으려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="db610-108">For best results in troubleshooting your Stream Analytics job, use the following guidelines:</span></span>

1.  <span data-ttu-id="db610-109">연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-109">Test your connectivity:</span></span>
    - <span data-ttu-id="db610-110">각 입력 및 출력에 대해 **테스트 연결** 단추를 사용하여 입력 및 출력에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-110">Verify connectivity to inputs and outputs by using the **Test Connection** button for each input and output.</span></span>

2.  <span data-ttu-id="db610-111">입력된 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-111">Examine your input data:</span></span>
    - <span data-ttu-id="db610-112">해당 입력 데이터가 이벤트 허브로 전달되고 있는지 확인하려면 [Service Bus 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)를 사용하여 Azure Event Hub(이벤트 허브 입력이 사용되는 경우)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-112">To verify that input data is flowing into Event Hub, use [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) to connect to Azure Event Hub (if Event Hub input is used).</span></span>  
    - <span data-ttu-id="db610-113">각 입력에 대해 [**샘플 데이터**](stream-analytics-sample-data-input.md) 단추를 사용하고 입력된 샘플 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-113">Use the [**Sample Data**](stream-analytics-sample-data-input.md) button for each input, and download the input sample data.</span></span>
    - <span data-ttu-id="db610-114">샘플 데이터를 검사하여 데이터의 셰이프(스키마 및 [데이터 형식](https://msdn.microsoft.com/library/azure/dn835065.aspx))를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-114">Inspect the sample data to understand the shape of the data: the schema and the [data types](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

3.  <span data-ttu-id="db610-115">쿼리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-115">Test your query:</span></span>
    - <span data-ttu-id="db610-116">**쿼리** 탭에서 **테스트** 단추를 사용하여 쿼리를 테스트하고 다운로드한 샘플 데이터를 사용하여 [쿼리를 테스트](stream-analytics-test-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-116">On the **Query** tab, use the **Test** button to test the query, and use the downloaded sample data to [test the query](stream-analytics-test-query.md).</span></span> <span data-ttu-id="db610-117">모든 오류를 검사하고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-117">Examine any errors and attempt to correct them.</span></span>
    - <span data-ttu-id="db610-118">[**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx)를 사용하는 경우 이벤트에 [작업 시작 시간](stream-analytics-out-of-order-and-late-events.md)보다 큰 타임스탬프가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-118">If you use [**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verify that the events have timestamps greater than the [job start time](stream-analytics-out-of-order-and-late-events.md).</span></span>

4.  <span data-ttu-id="db610-119">쿼리를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-119">Debug your query:</span></span>
    - <span data-ttu-id="db610-120">단계를 통해 간단한 select 문에서 좀 더 복잡한 집계까지 점진적으로 쿼리를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db610-120">Rebuild the query progressively from simple select statement to more complex aggregates by using steps.</span></span> <span data-ttu-id="db610-121">단계별로 쿼리 논리를 작성하려면 [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-121">To build up the query logic step by step, use [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clauses.</span></span>
    - <span data-ttu-id="db610-122">[SELECT INTO](stream-analytics-select-into.md)를 사용하여 쿼리 단계를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-122">Use [SELECT INTO](stream-analytics-select-into.md) to debug query steps.</span></span>

5.  <span data-ttu-id="db610-123">다음과 같은 공통 문제를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-123">Eliminate common pitfalls, such as:</span></span>
    - <span data-ttu-id="db610-124">쿼리의 [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) 절은 출력이 생성되지 않도록 방지하는 모든 이벤트를 필터링했습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-124">A [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) clause in the query filtered out all events, preventing any output from being generated.</span></span>
    - <span data-ttu-id="db610-125">창 함수를 사용하는 경우 전체 창 기간을 기다려서 쿼리의 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-125">When you use window functions, wait for the entire window duration to see an output from the query.</span></span>
    - <span data-ttu-id="db610-126">작업 시작 시간 전에 이벤트에 대한 타임스탬프가 있으므로 이벤트가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="db610-126">The timestamp for events precedes the job start time and, therefore, events are being dropped.</span></span>

6.  <span data-ttu-id="db610-127">이벤트 순서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-127">Use event ordering:</span></span>
    - <span data-ttu-id="db610-128">이전 단계가 모두 정상적으로 작동하는 경우 **설정** 블레이드로 이동하여 [**이벤트 순서**](stream-analytics-out-of-order-and-late-events.md)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-128">If all the previous steps worked fine, go to the **Settings** blade and select [**Event Ordering**](stream-analytics-out-of-order-and-late-events.md).</span></span> <span data-ttu-id="db610-129">이 정책이 사용자 시나리오에 적합하게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-129">Verify that this policy is configured for what makes sense in your scenario.</span></span> <span data-ttu-id="db610-130">정책은 **테스트** 단추를 사용하여 쿼리를 테스트하는 경우 적용되지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="db610-130">The policy is *not* applied when you use the **Test** button to test the query.</span></span> <span data-ttu-id="db610-131">이것이 브라우저에서 테스트할 때와 프로덕션의 작업을 실행할 때의 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="db610-131">This result is one difference between testing in-browser versus running the job in production.</span></span>

7.  <span data-ttu-id="db610-132">메트릭을 사용하여 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-132">Debug by using metrics:</span></span>
    - <span data-ttu-id="db610-133">예상된 기간(쿼리 기준) 후 획득된 출력이 없는 경우 다음을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-133">If you obtain no output after the expected duration (based on the query), try the following:</span></span>
        - <span data-ttu-id="db610-134">**모니터** 탭에서 [**모니터링 메트릭**](stream-analytics-monitoring.md)을 확인합니다. 값을 집계하기 때문에 메트릭이 몇 분 동안 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="db610-134">Look at [**Monitoring Metrics**](stream-analytics-monitoring.md) on the **Monitor** tab. Because the values are aggregated, the metrics are delayed by a few minutes.</span></span>
            - <span data-ttu-id="db610-135">입력 이벤트가 0보다 큰 경우, 작업은 입력 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-135">If Input Events > 0, the job is able to read input data.</span></span> <span data-ttu-id="db610-136">입력 이벤트가 0보다 크지 않으면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-136">If Input Events is not > 0, then:</span></span>
                - <span data-ttu-id="db610-137">데이터 원본에 유효한 데이터가 있는지 확인하려면 [Service Bus 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)를 사용하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-137">To see whether the data source has valid data, check it by using [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a).</span></span> <span data-ttu-id="db610-138">이 확인은 작업이 입력으로 이벤트 허브를 사용하는 경우 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db610-138">This check applies if the job is using Event Hub as input.</span></span>
                - <span data-ttu-id="db610-139">데이터 serialization 형식과 데이터 인코딩이 예상대로인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-139">Check to see whether the data serialization format and data encoding are as expected.</span></span>
                - <span data-ttu-id="db610-140">작업이 이벤트 허브를 사용하는 경우 메시지의 본문이 *Null*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-140">If the job is using an Event Hub, check to see whether the body of the message is *Null*.</span></span>
            - <span data-ttu-id="db610-141">데이터 변환 오류가 0보다 크며 증가하는 경우 다음을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-141">If Data Conversion Errors > 0 and climbing, the following might be true:</span></span>
                - <span data-ttu-id="db610-142">작업이 이벤트를 역직렬화하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-142">The job might not be able to de-serialize the events.</span></span>
                - <span data-ttu-id="db610-143">이벤트 스키마가 쿼리에서 이벤트의 정의 또는 예상 스키마와 일치하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-143">The event schema might not match the defined or expected schema of the events in the query.</span></span>
                - <span data-ttu-id="db610-144">이벤트에서 일부 필드의 데이터 형식이 예상과 일치하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-144">The datatypes of some of the fields in the event might not match expectations.</span></span>
            - <span data-ttu-id="db610-145">런타임 오류가 0보다 큰 경우 작업이 데이터를 수신할 수 있지만 쿼리를 처리하는 동안 오류가 발생함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-145">If Runtime Errors > 0, it means that the job can receive the data but is generating errors while processing the query.</span></span>
                - <span data-ttu-id="db610-146">오류를 찾으려면 [감사 로그](../azure-resource-manager/resource-group-audit.md)로 이동하여 *실패* 상태를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-146">To find the errors, go to the [Audit Logs](../azure-resource-manager/resource-group-audit.md) and filter on *Failed* status.</span></span>
            - <span data-ttu-id="db610-147">InputEvents가 0보다 크고 OutputEvents가 0인 경우 다음 중 하나를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-147">If InputEvents > 0 and OutputEvents = 0, it means that one of the following is true:</span></span>
                - <span data-ttu-id="db610-148">쿼리 처리로 제로 출력 이벤트가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-148">Query processing resulted in zero output events.</span></span>
                - <span data-ttu-id="db610-149">이벤트 또는 그 필드가 잘못되어 쿼리 처리 후 제로 출력이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-149">Events or its fields might be malformed, resulting in zero output after query processing.</span></span>
                - <span data-ttu-id="db610-150">작업이 연결 또는 인증 이유로 데이터를 [출력 싱크](stream-analytics-select-into.md)에 푸시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-150">The job was unable to push data to the [output sink](stream-analytics-select-into.md) for connectivity or authentication reasons.</span></span>
        - <span data-ttu-id="db610-151">이전에 언급한 모든 오류 사례에서 작업 로그 메시지는 쿼리 논리가 모든 이벤트를 필터링하는 경우 외에 추가 정보(발생하는 상황 포함)를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-151">In all the previously mentioned error cases, operations log messages explain additional details (including what is happening), except in cases where the query logic filtered out all events.</span></span> <span data-ttu-id="db610-152">여러 이벤트 처리에서 오류가 발생하면 Stream Analytics는 작업 로그에 10분 이내 동일한 형식의 첫 세 개의 오류 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-152">If the processing of multiple events generates errors, Stream Analytics logs the first three error messages of the same type within 10 minutes to Operations logs.</span></span> <span data-ttu-id="db610-153">그런 다음 “오류가 너무 빠르게 발생하고 억제되고 있습니다”라는 메시지로 동일한 추가 오류를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-153">It then suppresses additional identical errors with a message that reads “Errors are happening too rapidly, these are being suppressed.”</span></span>

8. <span data-ttu-id="db610-154">감사 및 진단 로그를 사용하여 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-154">Debug by using audit and diagnostic logs:</span></span>
    - <span data-ttu-id="db610-155">[감사 로그](../azure-resource-manager/resource-group-audit.md)를 사용하고 필터링하여 오류를 식별하고 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-155">Use [Audit Logs](../azure-resource-manager/resource-group-audit.md), and filter to identify and debug errors.</span></span>
    - <span data-ttu-id="db610-156">[작업 진단 로그](stream-analytics-job-diagnostic-logs.md)를 사용하여 오류를 식별하고 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-156">Use [job diagnostic logs](stream-analytics-job-diagnostic-logs.md) to identify and debug errors.</span></span>

9. <span data-ttu-id="db610-157">출력을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-157">Examine the outputs:</span></span>
    - <span data-ttu-id="db610-158">쿼리에 지정한 기간에 따라 작업 상태가 *실행 중*이면 출력은 싱크 데이터 원본에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db610-158">When the job status is *Running*, depending on the duration that's stipulated in the query, you can see the output in the sink data source.</span></span>
    - <span data-ttu-id="db610-159">특정 출력 형식으로 된 출력을 볼 수 없는 경우 Azure Blob과 같이 덜 복잡한 출력 형식으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-159">If you cannot see outputs that are going to a specific output type, redirect them to an output type that is less complex, such as an Azure Blob.</span></span> <span data-ttu-id="db610-160">Storage Explorer를 사용하여 출력을 볼 수 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-160">By using Storage Explorer, check to see whether the output can be seen.</span></span> <span data-ttu-id="db610-161">또한 출력 시 제한 한도가 데이터를 수신하지 못하게 하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-161">Additionally, verify whether throttling limits at the output are preventing data from being received.</span></span>

10. <span data-ttu-id="db610-162">작업 다이어그램 메트릭을 통해 데이터 흐름 분석을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-162">Use data-flow analysis with job diagram metrics:</span></span>
    - <span data-ttu-id="db610-163">데이터 흐름을 분석하고 문제를 식별하려면 [메트릭을 사용한 작업 다이어그램](stream-analytics-job-diagram-with-metrics.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db610-163">To analyze data flow and identify issues, use the [job diagram with metrics](stream-analytics-job-diagram-with-metrics.md).</span></span>

11. <span data-ttu-id="db610-164">지원 사례를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db610-164">Open a support case:</span></span>
    - <span data-ttu-id="db610-165">마지막으로, 모든 작업이 실패하면 작업을 포함하는 SubscriptionID를 사용하여 Microsoft 지원 사례를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db610-165">Finally, if all else fails, open a Microsoft support case by using the SubscriptionID that contains your job.</span></span>

## <a name="get-help"></a><span data-ttu-id="db610-166">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="db610-166">Get help</span></span>

<span data-ttu-id="db610-167">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db610-167">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db610-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db610-168">Next steps</span></span>

* [<span data-ttu-id="db610-169">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="db610-169">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="db610-170">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="db610-170">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="db610-171">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="db610-171">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="db610-172">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="db610-172">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="db610-173">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="db610-173">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
