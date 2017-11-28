---
title: "Azure 스트림 분석에 대 한 aaaTroubleshooting 가이드 | Microsoft Docs"
description: "어떻게 tootroubleshoot 스트림 분석 작업"
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
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a><span data-ttu-id="28109-104">Azure Stream Analytics 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="28109-104">Troubleshooting guide for Azure Stream Analytics</span></span>

<span data-ttu-id="28109-105">Azure 스트림 분석 문제 해결 toobe 복잡 한 노력 얼핏 보기에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-105">Azure Stream Analytics troubleshooting can appear toobe a complex effort at first glance.</span></span> <span data-ttu-id="28109-106">여러 사용자가 있는 작업을 한 후이 가이드 toohelp 약식 hello 프로세스 만든 우리 고 입력, 출력, 쿼리 및 함수에 대 한 hello 추측을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-106">After working with many users, we have created this guide toohelp streamline hello process and remove hello guesswork about your inputs, outputs, queries, and functions.</span></span>

## <a name="troubleshoot-your-stream-analytics-job"></a><span data-ttu-id="28109-107">Stream Analytics 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="28109-107">Troubleshoot your Stream Analytics job</span></span>

<span data-ttu-id="28109-108">스트림 분석 작업 문제 해결에 대 한 최상의 결과 지침을 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-108">For best results in troubleshooting your Stream Analytics job, use hello following guidelines:</span></span>

1.  <span data-ttu-id="28109-109">연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-109">Test your connectivity:</span></span>
    - <span data-ttu-id="28109-110">Hello를 사용 하 여 연결 tooinputs 및 출력을 확인 **연결 테스트** 각 입력 및 출력에 대 한 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-110">Verify connectivity tooinputs and outputs by using hello **Test Connection** button for each input and output.</span></span>

2.  <span data-ttu-id="28109-111">입력된 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-111">Examine your input data:</span></span>
    - <span data-ttu-id="28109-112">입력 데이터 tooverify 이벤트 허브로 전달 되는지, 사용 하 여 [서비스 버스 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure (이벤트 허브 입력이 사용 됨) 하는 경우 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-112">tooverify that input data is flowing into Event Hub, use [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Event Hub (if Event Hub input is used).</span></span>  
    - <span data-ttu-id="28109-113">사용 하 여 hello [ **예제 데이터** ](stream-analytics-sample-data-input.md) 각 입력에 대 한 단추 및 hello 입력된 샘플 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-113">Use hello [**Sample Data**](stream-analytics-sample-data-input.md) button for each input, and download hello input sample data.</span></span>
    - <span data-ttu-id="28109-114">Hello 데이터 hello 샘플 데이터 toounderstand hello 형식 검사: 스키마와 hello hello [데이터 형식](https://msdn.microsoft.com/library/azure/dn835065.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-114">Inspect hello sample data toounderstand hello shape of hello data: hello schema and hello [data types](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

3.  <span data-ttu-id="28109-115">쿼리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-115">Test your query:</span></span>
    - <span data-ttu-id="28109-116">Hello에 **쿼리** 탭에서 hello를 사용 하 여 **테스트** tootest hello 쿼리 단추를 선택한 너무 hello 다운로드 한 샘플 데이터를 사용 하 여[hello 쿼리 테스트](stream-analytics-test-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-116">On hello **Query** tab, use hello **Test** button tootest hello query, and use hello downloaded sample data too[test hello query](stream-analytics-test-query.md).</span></span> <span data-ttu-id="28109-117">모든 오류를 검토 하 고 toocorrect 시도 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-117">Examine any errors and attempt toocorrect them.</span></span>
    - <span data-ttu-id="28109-118">사용 하는 경우 [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), hello 이벤트 hello 보다 큰 타임 스탬프가 있는지 확인 해야 [작업 시작 시간](stream-analytics-out-of-order-and-late-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-118">If you use [**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verify that hello events have timestamps greater than hello [job start time](stream-analytics-out-of-order-and-late-events.md).</span></span>

4.  <span data-ttu-id="28109-119">쿼리를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-119">Debug your query:</span></span>
    - <span data-ttu-id="28109-120">단순 select 문 toomore 복잡 한 집계에서 점진적으로 hello 쿼리 단계를 사용 하 여 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-120">Rebuild hello query progressively from simple select statement toomore complex aggregates by using steps.</span></span> <span data-ttu-id="28109-121">toobuild 단계별로 hello 쿼리 논리를 사용 하 여 [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) 절.</span><span class="sxs-lookup"><span data-stu-id="28109-121">toobuild up hello query logic step by step, use [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clauses.</span></span>
    - <span data-ttu-id="28109-122">사용 하 여 [SELECT INTO](stream-analytics-select-into.md) toodebug 쿼리 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-122">Use [SELECT INTO](stream-analytics-select-into.md) toodebug query steps.</span></span>

5.  <span data-ttu-id="28109-123">다음과 같은 공통 문제를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-123">Eliminate common pitfalls, such as:</span></span>
    - <span data-ttu-id="28109-124">A [ **여기서** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) hello 쿼리 절 어떠한 출력도 생성 되지 방지 하는 모든 이벤트를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-124">A [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) clause in hello query filtered out all events, preventing any output from being generated.</span></span>
    - <span data-ttu-id="28109-125">창 함수를 사용할 때까지 기다린 hello 창의 전체 기간 toosee hello 쿼리에서 출력.</span><span class="sxs-lookup"><span data-stu-id="28109-125">When you use window functions, wait for hello entire window duration toosee an output from hello query.</span></span>
    - <span data-ttu-id="28109-126">이벤트에 대 한 타임 스탬프 hello hello 작업 시작 시간을 앞에 오고, 따라서 이벤트 손실 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-126">hello timestamp for events precedes hello job start time and, therefore, events are being dropped.</span></span>

6.  <span data-ttu-id="28109-127">이벤트 순서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-127">Use event ordering:</span></span>
    - <span data-ttu-id="28109-128">모든 이전 단계는 작동 hello, toohello 이동 **설정** 블레이드에 대 한 선택 [ **이벤트 순서가**](stream-analytics-out-of-order-and-late-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-128">If all hello previous steps worked fine, go toohello **Settings** blade and select [**Event Ordering**](stream-analytics-out-of-order-and-late-events.md).</span></span> <span data-ttu-id="28109-129">이 정책이 사용자 시나리오에 적합하게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-129">Verify that this policy is configured for what makes sense in your scenario.</span></span> <span data-ttu-id="28109-130">hello 정책이 *하지* hello를 사용할 때 적용 **테스트** 단추 tootest hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-130">hello policy is *not* applied when you use hello **Test** button tootest hello query.</span></span> <span data-ttu-id="28109-131">이 결과 프로덕션 환경에서 hello 작업을 실행 하는 비교는 브라우저에서 테스트 간의 차이점 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-131">This result is one difference between testing in-browser versus running hello job in production.</span></span>

7.  <span data-ttu-id="28109-132">메트릭을 사용하여 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-132">Debug by using metrics:</span></span>
    - <span data-ttu-id="28109-133">Hello 예상 기간 (쿼리를 기반으로 hello) 후 없는 출력을 가져올 경우 hello 다음을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="28109-133">If you obtain no output after hello expected duration (based on hello query), try hello following:</span></span>
        - <span data-ttu-id="28109-134">살펴보고 [ **모니터링 메트릭에** ](stream-analytics-monitoring.md) hello에 **모니터** 탭 합니다. Hello 값이 집계 되기 때문에 hello 메트릭 몇 분 정도 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28109-134">Look at [**Monitoring Metrics**](stream-analytics-monitoring.md) on hello **Monitor** tab. Because hello values are aggregated, hello metrics are delayed by a few minutes.</span></span>
            - <span data-ttu-id="28109-135">하는 경우 입력 이벤트 > 0 hello 작업은 수 tooread 입력된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-135">If Input Events > 0, hello job is able tooread input data.</span></span> <span data-ttu-id="28109-136">입력 이벤트가 0보다 크지 않으면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-136">If Input Events is not > 0, then:</span></span>
                - <span data-ttu-id="28109-137">toosee hello 데이터 원본에 유효한 데이터가 있는지 여부를 확인 하기를 사용 하 여 [서비스 버스 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-137">toosee whether hello data source has valid data, check it by using [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a).</span></span> <span data-ttu-id="28109-138">이 검사는 hello 작업 입력으로 이벤트 허브를 사용 하는 경우 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28109-138">This check applies if hello job is using Event Hub as input.</span></span>
                - <span data-ttu-id="28109-139">Toosee를 예상 대로 hello 데이터 serialization 형식 및 데이터 인코딩 되는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-139">Check toosee whether hello data serialization format and data encoding are as expected.</span></span>
                - <span data-ttu-id="28109-140">Hello 메시지의 본문 hello 인지 hello 작업 이벤트 허브를 사용 하는 경우 확인 toosee *Null*합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-140">If hello job is using an Event Hub, check toosee whether hello body of hello message is *Null*.</span></span>
            - <span data-ttu-id="28109-141">하는 경우 데이터 변환 오류 > 0 및 오르기 hello 다음 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-141">If Data Conversion Errors > 0 and climbing, hello following might be true:</span></span>
                - <span data-ttu-id="28109-142">hello 작업 수 있습니다 수 toode-hello 이벤트를 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-142">hello job might not be able toode-serialize hello events.</span></span>
                - <span data-ttu-id="28109-143">hello 이벤트 스키마와 일치 하지 않는 hello 정의 된 또는 hello 쿼리에서 hello 이벤트 스키마 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-143">hello event schema might not match hello defined or expected schema of hello events in hello query.</span></span>
                - <span data-ttu-id="28109-144">일부 hello 이벤트의 hello 필드의 데이터 형식이 hello 기대와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="28109-144">hello datatypes of some of hello fields in hello event might not match expectations.</span></span>
            - <span data-ttu-id="28109-145">경우 런타임 오류가 해당 hello 작업 hello 데이터를 받을 수는 있지만 hello 쿼리를 처리 하는 동안 오류를 생성 하는 의미 > 0입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-145">If Runtime Errors > 0, it means that hello job can receive hello data but is generating errors while processing hello query.</span></span>
                - <span data-ttu-id="28109-146">toofind hello 오류 이동 toohello [감사 로그](../azure-resource-manager/resource-group-audit.md) 찾아서 활성 *실패* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-146">toofind hello errors, go toohello [Audit Logs](../azure-resource-manager/resource-group-audit.md) and filter on *Failed* status.</span></span>
            - <span data-ttu-id="28109-147">경우 InputEvents > 0과 OutputEvents = 0, hello 다음 중 하나가 충족 될 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-147">If InputEvents > 0 and OutputEvents = 0, it means that one of hello following is true:</span></span>
                - <span data-ttu-id="28109-148">쿼리 처리로 제로 출력 이벤트가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-148">Query processing resulted in zero output events.</span></span>
                - <span data-ttu-id="28109-149">이벤트 또는 그 필드가 잘못되어 쿼리 처리 후 제로 출력이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-149">Events or its fields might be malformed, resulting in zero output after query processing.</span></span>
                - <span data-ttu-id="28109-150">hello 작업은 없습니다 toopush 데이터 toohello [출력 싱크](stream-analytics-select-into.md) 연결 또는 인증 이유로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-150">hello job was unable toopush data toohello [output sink](stream-analytics-select-into.md) for connectivity or authentication reasons.</span></span>
        - <span data-ttu-id="28109-151">모든 hello에 앞서 언급 한 작업 (발생 하는 작업 포함)에 추가 세부 정보를 설명 하는 로그 메시지의 오류 경우 hello 쿼리 논리 모든 이벤트를 필터링 하는 경우에서를 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-151">In all hello previously mentioned error cases, operations log messages explain additional details (including what is happening), except in cases where hello query logic filtered out all events.</span></span> <span data-ttu-id="28109-152">여러 이벤트의 hello 처리에서 오류가 발생 하면 스트림 분석 로그 hello tooOperations 10 분 내에서 동일한 형식 hello의 처음 세 개의 오류 메시지를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-152">If hello processing of multiple events generates errors, Stream Analytics logs hello first three error messages of hello same type within 10 minutes tooOperations logs.</span></span> <span data-ttu-id="28109-153">그런 다음 “오류가 너무 빠르게 발생하고 억제되고 있습니다”라는 메시지로 동일한 추가 오류를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28109-153">It then suppresses additional identical errors with a message that reads “Errors are happening too rapidly, these are being suppressed.”</span></span>

8. <span data-ttu-id="28109-154">감사 및 진단 로그를 사용하여 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-154">Debug by using audit and diagnostic logs:</span></span>
    - <span data-ttu-id="28109-155">사용 하 여 [감사 로그](../azure-resource-manager/resource-group-audit.md), 필터 tooidentify 및 디버그 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="28109-155">Use [Audit Logs](../azure-resource-manager/resource-group-audit.md), and filter tooidentify and debug errors.</span></span>
    - <span data-ttu-id="28109-156">사용 하 여 [작업 진단 로그](stream-analytics-job-diagnostic-logs.md) 오류 tooidentify 및 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-156">Use [job diagnostic logs](stream-analytics-job-diagnostic-logs.md) tooidentify and debug errors.</span></span>

9. <span data-ttu-id="28109-157">Hello 출력을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-157">Examine hello outputs:</span></span>
    - <span data-ttu-id="28109-158">Hello 작업 상태는 때 *실행*hello 싱크 데이터 원본에 대 한 hello 출력을 볼 수 있습니다 hello 쿼리에서 명시한는 hello 기간에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-158">When hello job status is *Running*, depending on hello duration that's stipulated in hello query, you can see hello output in hello sink data source.</span></span>
    - <span data-ttu-id="28109-159">출력 tooa 특정 출력 형식이는 표시 되지 않는 경우 Azure Blob와 같은 덜 복잡 한 않은 tooan 출력 형식이 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="28109-159">If you cannot see outputs that are going tooa specific output type, redirect them tooan output type that is less complex, such as an Azure Blob.</span></span> <span data-ttu-id="28109-160">저장소 탐색기를 사용 하 여 toosee hello 출력을 볼 수 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-160">By using Storage Explorer, check toosee whether hello output can be seen.</span></span> <span data-ttu-id="28109-161">또한 스로틀 한계 hello 출력에서 데이터를 수신 하지 못합니다 방지는 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-161">Additionally, verify whether throttling limits at hello output are preventing data from being received.</span></span>

10. <span data-ttu-id="28109-162">작업 다이어그램 메트릭을 통해 데이터 흐름 분석을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-162">Use data-flow analysis with job diagram metrics:</span></span>
    - <span data-ttu-id="28109-163">tooanalyze 데이터 흐름 및 문제를 사용 하 여 hello 식별 [메트릭 사용 하 여 작업 다이어그램](stream-analytics-job-diagram-with-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28109-163">tooanalyze data flow and identify issues, use hello [job diagram with metrics](stream-analytics-job-diagram-with-metrics.md).</span></span>

11. <span data-ttu-id="28109-164">지원 사례를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28109-164">Open a support case:</span></span>
    - <span data-ttu-id="28109-165">마지막으로, 모든 작업이 실패 하면 작업을 포함 하는 SubscriptionID hello를 사용 하 여 Microsoft 지원 케이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28109-165">Finally, if all else fails, open a Microsoft support case by using hello SubscriptionID that contains your job.</span></span>

## <a name="get-help"></a><span data-ttu-id="28109-166">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="28109-166">Get help</span></span>

<span data-ttu-id="28109-167">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28109-167">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="28109-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28109-168">Next steps</span></span>

* [<span data-ttu-id="28109-169">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="28109-169">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="28109-170">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="28109-170">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="28109-171">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="28109-171">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="28109-172">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="28109-172">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="28109-173">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="28109-173">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
