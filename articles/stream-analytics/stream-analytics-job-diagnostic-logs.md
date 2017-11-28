---
title: "진단 로그로 Azure Stream Analytics 문제 해결 | Microsoft Docs"
description: "Microsoft Azure에서 Stream Analytics 작업의 진단 로그를 분석하는 방법을 알아봅니다."
keywords: 
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
ms.openlocfilehash: ea90a62ffee9c766985f76e1c0abc1585bebc69b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a><span data-ttu-id="4b2a9-103">진단 로그를 사용하여 Azure Stream Analytics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4b2a9-103">Troubleshoot Azure Stream Analytics by using diagnostics logs</span></span>

<span data-ttu-id="4b2a9-104">경우에 따라 Azure Stream Analytics 작업이 예기치 않게 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-104">Occasionally, an Azure Stream Analytics job unexpectedly stops processing.</span></span> <span data-ttu-id="4b2a9-105">이 이벤트 종류의 문제를 해결하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-105">It's important to be able to troubleshoot this kind of event.</span></span> <span data-ttu-id="4b2a9-106">이벤트는 예기치 않은 쿼리 결과, 장치에 대한 연결 또는 예기치 않은 서비스 중단으로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-106">The event might be caused by an unexpected query result, by connectivity to devices, or by an unexpected service outage.</span></span> <span data-ttu-id="4b2a9-107">Stream Analytics에서 진단 로그를 사용하면 이와 같은 이벤트가 발생했을 때 문제 원인을 파악하고 복구 시간을 단축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-107">The diagnostics logs in Stream Analytics can help you identify the cause of issues when they occur, and reduce recovery time.</span></span>

## <a name="log-types"></a><span data-ttu-id="4b2a9-108">로그 형식</span><span class="sxs-lookup"><span data-stu-id="4b2a9-108">Log types</span></span>

<span data-ttu-id="4b2a9-109">Stream Analytics에서는 다음과 같은 두 가지 형식의 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-109">Stream Analytics offers two types of logs:</span></span> 
* <span data-ttu-id="4b2a9-110">[활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)(항상 켜짐).</span><span class="sxs-lookup"><span data-stu-id="4b2a9-110">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (always on).</span></span> <span data-ttu-id="4b2a9-111">활동 로그는 작업을 수행하는 작업에 대한 통찰력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-111">Activity logs give insights into operations performed on jobs.</span></span>
* <span data-ttu-id="4b2a9-112">[진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)(구성 가능).</span><span class="sxs-lookup"><span data-stu-id="4b2a9-112">[Diagnostics logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurable).</span></span> <span data-ttu-id="4b2a9-113">진단 로그는 작업과 관련하여 발생하는 모든 항목에 대해 더 다양한 통찰력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-113">Diagnostics logs provide richer insights into everything that happens with a job.</span></span> <span data-ttu-id="4b2a9-114">진단 작업은 작업을 생성할 때 시작되고, 작업을 삭제할 때 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-114">Diagnostics logs start when the job is created, and end when the job is deleted.</span></span> <span data-ttu-id="4b2a9-115">작업이 업데이트되고 실행되는 동안 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-115">They cover events when the job is updated and while it’s running.</span></span>

> [!NOTE]
> <span data-ttu-id="4b2a9-116">Azure Storage, Azure Event Hubs 및 Azure Log Analytics와 같은 서비스를 사용하여 맞지 않는 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-116">You can use services like Azure Storage, Azure Event Hubs, and Azure Log Analytics to analyze nonconforming data.</span></span> <span data-ttu-id="4b2a9-117">그러한 서비스에 대한 가격 책정 모델에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-117">You are charged based on the pricing model for those services.</span></span>
>

## <a name="turn-on-diagnostics-logs"></a><span data-ttu-id="4b2a9-118">진단 로그 켜기</span><span class="sxs-lookup"><span data-stu-id="4b2a9-118">Turn on diagnostics logs</span></span>

<span data-ttu-id="4b2a9-119">진단 로그는 기본적으로 **해제**되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-119">Diagnostics logs are **off** by default.</span></span> <span data-ttu-id="4b2a9-120">진단 로그를 켜려면 다음과 같은 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-120">To turn on diagnostics logs, complete these steps:</span></span>

1.  <span data-ttu-id="4b2a9-121">Azure Portal에 로그인하고 스트리밍 작업 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-121">Sign in to the Azure portal, and go to the streaming job blade.</span></span> <span data-ttu-id="4b2a9-122">**모니터링** 아래에서 **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-122">Under **Monitoring**, select **Diagnostics logs**.</span></span>

    ![진단 로그에 대한 블레이드 탐색](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  <span data-ttu-id="4b2a9-124">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-124">Select **Turn on diagnostics**.</span></span>

    ![진단 로그 켜기](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  <span data-ttu-id="4b2a9-126">**진단 설정** 페이지의 **상태**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-126">On the **Diagnostics settings** page, for **Status**, select **On**.</span></span>

    ![진단 로그에 대한 상태 변경](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  <span data-ttu-id="4b2a9-128">원하는 보관 대상(저장소 계정, 이벤트 허브, Log Analytics)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-128">Set up the archival target (storage account, event hub, Log Analytics) that you want.</span></span> <span data-ttu-id="4b2a9-129">그런 다음, 수집할 로그의 범주를 선택합니다(실행, 작성).</span><span class="sxs-lookup"><span data-stu-id="4b2a9-129">Then, select the categories of logs that you want to collect (Execution, Authoring).</span></span> 

5.  <span data-ttu-id="4b2a9-130">새 진단 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-130">Save the new diagnostics configuration.</span></span>

<span data-ttu-id="4b2a9-131">진단 구성이 적용되는 데 약 10분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-131">The diagnostics configuration takes about 10 minutes to take effect.</span></span> <span data-ttu-id="4b2a9-132">그 후 구성된 보관 대상에 로그가 나타나기 시작합니다(**진단 로그** 페이지에서 볼 수 있음).</span><span class="sxs-lookup"><span data-stu-id="4b2a9-132">After that, the logs start appearing in the configured archival target (you can see these on the **Diagnostics logs** page):</span></span>

![진단 로그에 대한 블레이드 탐색 - 보관 대상](./media/stream-analytics-job-diagnostic-logs/image4.png)

<span data-ttu-id="4b2a9-134">진단을 구성하는 방법에 대한 자세한 내용은 [Azure 리소스의 진단 데이터 수집 및 사용](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-134">For more information about configuring diagnostics, see [Collect and consume diagnostics data from your Azure resources](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span></span>

## <a name="diagnostics-log-categories"></a><span data-ttu-id="4b2a9-135">진단 로그 범주</span><span class="sxs-lookup"><span data-stu-id="4b2a9-135">Diagnostics log categories</span></span>

<span data-ttu-id="4b2a9-136">현재 두 가지 진단 로그 범주를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-136">Currently, we capture two categories of diagnostics logs:</span></span>

* <span data-ttu-id="4b2a9-137">**작성**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-137">**Authoring**.</span></span> <span data-ttu-id="4b2a9-138">작업 생성, 입력 및 출력 추가 및 삭제, 쿼리 추가 및 업데이트, 작업 시작 및 중지 등 작업 작성 작업과 관련된 로그 이벤트를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-138">Captures log events that are related to job authoring operations: job creation, adding and deleting inputs and outputs, adding and updating the query, starting and stopping the job.</span></span>
* <span data-ttu-id="4b2a9-139">**실행**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-139">**Execution**.</span></span> <span data-ttu-id="4b2a9-140">작업 실행 중 발생하는 이벤트를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-140">Captures events that occur during job execution:</span></span>
    * <span data-ttu-id="4b2a9-141">연결 오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-141">Connectivity errors</span></span>
    * <span data-ttu-id="4b2a9-142">다음을 포함하는 데이터 처리 오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-142">Data processing errors, including:</span></span>
        * <span data-ttu-id="4b2a9-143">쿼리 정의를 따르지 않는 이벤트(필드 형식 및 값 불일치, 필드 누락 등)</span><span class="sxs-lookup"><span data-stu-id="4b2a9-143">Events that don’t conform to the query definition (mismatched field types and values, missing fields, and so on)</span></span>
        * <span data-ttu-id="4b2a9-144">식 평가 오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-144">Expression evaluation errors</span></span>
    * <span data-ttu-id="4b2a9-145">다른 이벤트 및 오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-145">Other events and errors</span></span>

## <a name="diagnostics-logs-schema"></a><span data-ttu-id="4b2a9-146">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="4b2a9-146">Diagnostics logs schema</span></span>

<span data-ttu-id="4b2a9-147">모든 로그는 JSON 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-147">All logs are stored in JSON format.</span></span> <span data-ttu-id="4b2a9-148">각 항목에는 다음과 같은 일반적인 문자열 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-148">Each entry has the following common string fields:</span></span>

<span data-ttu-id="4b2a9-149">이름</span><span class="sxs-lookup"><span data-stu-id="4b2a9-149">Name</span></span> | <span data-ttu-id="4b2a9-150">설명</span><span class="sxs-lookup"><span data-stu-id="4b2a9-150">Description</span></span>
------- | -------
<span data-ttu-id="4b2a9-151">실시간</span><span class="sxs-lookup"><span data-stu-id="4b2a9-151">time</span></span> | <span data-ttu-id="4b2a9-152">로그의 타임스탬프(UTC)입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-152">Timestamp (in UTC) of the log.</span></span>
<span data-ttu-id="4b2a9-153">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b2a9-153">resourceId</span></span> | <span data-ttu-id="4b2a9-154">작업이 수행되는 리소스의 ID(대문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-154">ID of the resource that the operation took place on, in upper case.</span></span> <span data-ttu-id="4b2a9-155">여기에는 구독 ID, 리소스 그룹 및 작업 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-155">It includes the subscription ID, the resource group, and the job name.</span></span> <span data-ttu-id="4b2a9-156">예: **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-156">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span></span>
<span data-ttu-id="4b2a9-157">카테고리</span><span class="sxs-lookup"><span data-stu-id="4b2a9-157">category</span></span> | <span data-ttu-id="4b2a9-158">로그 범주로, **실행** 또는 **작성** 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-158">Log category, either **Execution** or **Authoring**.</span></span>
<span data-ttu-id="4b2a9-159">operationName</span><span class="sxs-lookup"><span data-stu-id="4b2a9-159">operationName</span></span> | <span data-ttu-id="4b2a9-160">기록된 작업의 이름</span><span class="sxs-lookup"><span data-stu-id="4b2a9-160">Name of the operation that is logged.</span></span> <span data-ttu-id="4b2a9-161">예: **이벤트 전송: mysqloutput에 대한 SQL 출력 쓰기 실패**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-161">For example, **Send Events: SQL Output write failure to mysqloutput**.</span></span>
<span data-ttu-id="4b2a9-162">status</span><span class="sxs-lookup"><span data-stu-id="4b2a9-162">status</span></span> | <span data-ttu-id="4b2a9-163">작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-163">Status of the operation.</span></span> <span data-ttu-id="4b2a9-164">예: **실패** 또는 **성공**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-164">For example, **Failed** or **Succeeded**.</span></span>
<span data-ttu-id="4b2a9-165">최소 수준</span><span class="sxs-lookup"><span data-stu-id="4b2a9-165">level</span></span> | <span data-ttu-id="4b2a9-166">로그 수준.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-166">Log level.</span></span> <span data-ttu-id="4b2a9-167">예: **오류**, **경고** 또는 **정보**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-167">For example, **Error**, **Warning**, or **Informational**.</span></span>
<span data-ttu-id="4b2a9-168">properties</span><span class="sxs-lookup"><span data-stu-id="4b2a9-168">properties</span></span> | <span data-ttu-id="4b2a9-169">로그 항목별 세부 정보로, JSON 문자열로 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-169">Log entry-specific detail, serialized as a JSON string.</span></span> <span data-ttu-id="4b2a9-170">자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-170">For more information, see the following sections.</span></span>

### <a name="execution-log-properties-schema"></a><span data-ttu-id="4b2a9-171">실행 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="4b2a9-171">Execution log properties schema</span></span>

<span data-ttu-id="4b2a9-172">실행 로그에는 Stream Analytics 작업 실행 중에 발생한 이벤트에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-172">Execution logs have information about events that happened during Stream Analytics job execution.</span></span> <span data-ttu-id="4b2a9-173">속성의 스키마는 이벤트의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-173">The schema of properties varies, depending on the type of event.</span></span> <span data-ttu-id="4b2a9-174">현재 실행 로그의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-174">Currently, we have the following types of execution logs:</span></span>

### <a name="data-errors"></a><span data-ttu-id="4b2a9-175">데이터 오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-175">Data errors</span></span>

<span data-ttu-id="4b2a9-176">작업이 데이터를 처리하는 동안 발생한 오류는 이 로그 범주에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-176">Any error that occurs while the job is processing data is in this category of logs.</span></span> <span data-ttu-id="4b2a9-177">이러한 로그는 데이터 읽기, serialization 및 쓰기 작업 도중에 가장 자주 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-177">These logs most often are created during data read, serialization, and write operations.</span></span> <span data-ttu-id="4b2a9-178">이러한 로그는 연결 오류를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-178">These logs do not include connectivity errors.</span></span> <span data-ttu-id="4b2a9-179">연결 오류는 일반 이벤트로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-179">Connectivity errors are treated as generic events.</span></span>

<span data-ttu-id="4b2a9-180">이름</span><span class="sxs-lookup"><span data-stu-id="4b2a9-180">Name</span></span> | <span data-ttu-id="4b2a9-181">설명</span><span class="sxs-lookup"><span data-stu-id="4b2a9-181">Description</span></span>
------- | -------
<span data-ttu-id="4b2a9-182">원본</span><span class="sxs-lookup"><span data-stu-id="4b2a9-182">Source</span></span> | <span data-ttu-id="4b2a9-183">오류가 발생한 작업 입력 또는 출력의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-183">Name of the job input or output where the error occurred.</span></span>
<span data-ttu-id="4b2a9-184">Message</span><span class="sxs-lookup"><span data-stu-id="4b2a9-184">Message</span></span> | <span data-ttu-id="4b2a9-185">오류와 연결된 메시지</span><span class="sxs-lookup"><span data-stu-id="4b2a9-185">Message associated with the error.</span></span>
<span data-ttu-id="4b2a9-186">형식</span><span class="sxs-lookup"><span data-stu-id="4b2a9-186">Type</span></span> | <span data-ttu-id="4b2a9-187">오류의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-187">Type of error.</span></span> <span data-ttu-id="4b2a9-188">예: **DataConversionError**, **CsvParserError** 또는 **ServiceBusPropertyColumnMissingError**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-188">For example, **DataConversionError**, **CsvParserError**, or **ServiceBusPropertyColumnMissingError**.</span></span>
<span data-ttu-id="4b2a9-189">Data</span><span class="sxs-lookup"><span data-stu-id="4b2a9-189">Data</span></span> | <span data-ttu-id="4b2a9-190">오류 출처를 정확히 찾는 데 도움이 되는 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-190">Contains data that is useful to accurately locate the source of the error.</span></span> <span data-ttu-id="4b2a9-191">크기에 따라 잘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-191">Subject to truncation, depending on size.</span></span>

<span data-ttu-id="4b2a9-192">**operationName** 값에 따라 데이터 오류의 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-192">Depending on the **operationName** value, data errors have the following schema:</span></span>
* <span data-ttu-id="4b2a9-193">**직렬화 이벤트**입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-193">**Serialize events**.</span></span> <span data-ttu-id="4b2a9-194">직렬화 이벤트는 이벤트 읽기 작업 중에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-194">Serialize events occur during event read operations.</span></span> <span data-ttu-id="4b2a9-195">이는 데이터 입력 시 쿼리 스키마를 충족하지 않을 때 다음과 같은 이유 중 하나로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-195">They occur when the data at the input does not satisfy the query schema for one of these reasons:</span></span>
    * <span data-ttu-id="4b2a9-196">*이벤트 (역)직렬화 도중 형식 불일치*: 오류를 발생시키는 필드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-196">*Type mismatch during event (de)serialize*: Identifies the field that's causing the error.</span></span>
    * <span data-ttu-id="4b2a9-197">*이벤트를 읽을 수 없음, 잘못된 serialization*: 입력 데이터에서 오류가 발생하는 위치에 대한 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-197">*Cannot read an event, invalid serialization*: Lists information about the location in the input data where the error occurred.</span></span> <span data-ttu-id="4b2a9-198">Blob 입력에 대한 Blob 이름, 오프셋 및 데이터 샘플이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-198">Includes blob name for blob input, offset, and a sample of the data.</span></span>
* <span data-ttu-id="4b2a9-199">**전송 이벤트**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-199">**Send events**.</span></span> <span data-ttu-id="4b2a9-200">전송 이벤트는 쓰기 작업 중에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-200">Send events occur during write operations.</span></span> <span data-ttu-id="4b2a9-201">오류를 발생시키는 스트리밍 이벤트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-201">They identify the streaming event that caused the error.</span></span>

### <a name="generic-events"></a><span data-ttu-id="4b2a9-202">일반 이벤트</span><span class="sxs-lookup"><span data-stu-id="4b2a9-202">Generic events</span></span>

<span data-ttu-id="4b2a9-203">일반 이벤트는 다른 모든 항목을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-203">Generic events cover everything else.</span></span>

<span data-ttu-id="4b2a9-204">이름</span><span class="sxs-lookup"><span data-stu-id="4b2a9-204">Name</span></span> | <span data-ttu-id="4b2a9-205">설명</span><span class="sxs-lookup"><span data-stu-id="4b2a9-205">Description</span></span>
-------- | --------
<span data-ttu-id="4b2a9-206">오류</span><span class="sxs-lookup"><span data-stu-id="4b2a9-206">Error</span></span> | <span data-ttu-id="4b2a9-207">(선택 사항) 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-207">(optional) Error information.</span></span> <span data-ttu-id="4b2a9-208">일반적으로 사용 가능한 경우 예외 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-208">Usually, this is exception information, if it's available.</span></span>
<span data-ttu-id="4b2a9-209">Message</span><span class="sxs-lookup"><span data-stu-id="4b2a9-209">Message</span></span>| <span data-ttu-id="4b2a9-210">로그 메시지</span><span class="sxs-lookup"><span data-stu-id="4b2a9-210">Log message.</span></span>
<span data-ttu-id="4b2a9-211">형식</span><span class="sxs-lookup"><span data-stu-id="4b2a9-211">Type</span></span> | <span data-ttu-id="4b2a9-212">메시지 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-212">Type of message.</span></span> <span data-ttu-id="4b2a9-213">내부 오류 분류에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-213">Maps to internal categorization of errors.</span></span> <span data-ttu-id="4b2a9-214">예: **JobValidationError** 또는 **BlobOutputAdapterInitializationFailure**.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-214">For example, **JobValidationError** or **BlobOutputAdapterInitializationFailure**.</span></span>
<span data-ttu-id="4b2a9-215">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="4b2a9-215">Correlation ID</span></span> | <span data-ttu-id="4b2a9-216">작업 실행을 고유하게 식별하는 [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier).</span><span class="sxs-lookup"><span data-stu-id="4b2a9-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies the job execution.</span></span> <span data-ttu-id="4b2a9-217">작업 시작 시간부터 작업이 중지될 때까지 모든 실행 로그 항목에는 동일한 **상관 관계 ID** 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b2a9-217">All execution log entries from the time the job starts until the job stops have the same **Correlation ID** value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b2a9-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b2a9-218">Next steps</span></span>

* [<span data-ttu-id="4b2a9-219">Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="4b2a9-219">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4b2a9-220">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="4b2a9-220">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4b2a9-221">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4b2a9-221">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4b2a9-222">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="4b2a9-222">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4b2a9-223">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="4b2a9-223">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
