---
title: "진단 로그로 Azure 스트림 분석 aaaTroubleshoot | Microsoft Docs"
description: "어떻게 tooanalyze 진단에서에서 로그 스트림 분석 작업에서 Microsoft Azure에 알아봅니다."
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a><span data-ttu-id="6eb92-103">진단 로그를 사용하여 Azure Stream Analytics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6eb92-103">Troubleshoot Azure Stream Analytics by using diagnostics logs</span></span>

<span data-ttu-id="6eb92-104">경우에 따라 Azure Stream Analytics 작업이 예기치 않게 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-104">Occasionally, an Azure Stream Analytics job unexpectedly stops processing.</span></span> <span data-ttu-id="6eb92-105">중요 한 toobe 수 tootroubleshoot이 이벤트의 종류는</span><span class="sxs-lookup"><span data-stu-id="6eb92-105">It's important toobe able tootroubleshoot this kind of event.</span></span> <span data-ttu-id="6eb92-106">hello 이벤트는 예기치 않은 쿼리 결과, 연결 toodevices 또는 예기치 않은 서비스 중단으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-106">hello event might be caused by an unexpected query result, by connectivity toodevices, or by an unexpected service outage.</span></span> <span data-ttu-id="6eb92-107">hello 스트림 분석에서 진단 로그의 활용 발생 하 고 복구 시간을 줄일 때 문제의 원인을 hello를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-107">hello diagnostics logs in Stream Analytics can help you identify hello cause of issues when they occur, and reduce recovery time.</span></span>

## <a name="log-types"></a><span data-ttu-id="6eb92-108">로그 형식</span><span class="sxs-lookup"><span data-stu-id="6eb92-108">Log types</span></span>

<span data-ttu-id="6eb92-109">Stream Analytics에서는 다음과 같은 두 가지 형식의 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-109">Stream Analytics offers two types of logs:</span></span> 
* <span data-ttu-id="6eb92-110">[활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)(항상 켜짐).</span><span class="sxs-lookup"><span data-stu-id="6eb92-110">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (always on).</span></span> <span data-ttu-id="6eb92-111">활동 로그는 작업을 수행하는 작업에 대한 통찰력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-111">Activity logs give insights into operations performed on jobs.</span></span>
* <span data-ttu-id="6eb92-112">[진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)(구성 가능).</span><span class="sxs-lookup"><span data-stu-id="6eb92-112">[Diagnostics logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurable).</span></span> <span data-ttu-id="6eb92-113">진단 로그는 작업과 관련하여 발생하는 모든 항목에 대해 더 다양한 통찰력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-113">Diagnostics logs provide richer insights into everything that happens with a job.</span></span> <span data-ttu-id="6eb92-114">진단 로그에 hello 작업이 만들어질 때 시작 및 종료 시간도 hello 작업이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-114">Diagnostics logs start when hello job is created, and end when hello job is deleted.</span></span> <span data-ttu-id="6eb92-115">Hello 작업이 업데이트 되 고 실행 하는 동안 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-115">They cover events when hello job is updated and while it’s running.</span></span>

> [!NOTE]
> <span data-ttu-id="6eb92-116">Azure 저장소, Azure 이벤트 허브 및 Azure 로그 분석 tooanalyze 일치 하지 않는 데이터와 같은 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-116">You can use services like Azure Storage, Azure Event Hubs, and Azure Log Analytics tooanalyze nonconforming data.</span></span> <span data-ttu-id="6eb92-117">가격 책정 모델 해당 서비스에 대 한 hello에 따라 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-117">You are charged based on hello pricing model for those services.</span></span>
>

## <a name="turn-on-diagnostics-logs"></a><span data-ttu-id="6eb92-118">진단 로그 켜기</span><span class="sxs-lookup"><span data-stu-id="6eb92-118">Turn on diagnostics logs</span></span>

<span data-ttu-id="6eb92-119">진단 로그는 기본적으로 **해제**되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-119">Diagnostics logs are **off** by default.</span></span> <span data-ttu-id="6eb92-120">tooturn 진단 로그에 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-120">tooturn on diagnostics logs, complete these steps:</span></span>

1.  <span data-ttu-id="6eb92-121">Toohello Azure 포털에에서 로그인 하 고 toohello 스트리밍 작업 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-121">Sign in toohello Azure portal, and go toohello streaming job blade.</span></span> <span data-ttu-id="6eb92-122">**모니터링** 아래에서 **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-122">Under **Monitoring**, select **Diagnostics logs**.</span></span>

    ![블레이드 탐색 toodiagnostics 로그](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  <span data-ttu-id="6eb92-124">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-124">Select **Turn on diagnostics**.</span></span>

    ![진단 로그 켜기](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  <span data-ttu-id="6eb92-126">Hello에 **진단 설정을** 페이지에 대 한 **상태**선택, **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-126">On hello **Diagnostics settings** page, for **Status**, select **On**.</span></span>

    ![진단 로그에 대한 상태 변경](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  <span data-ttu-id="6eb92-128">원하는 hello 보관 대상 (저장소 계정, 이벤트 허브, 로그 분석)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-128">Set up hello archival target (storage account, event hub, Log Analytics) that you want.</span></span> <span data-ttu-id="6eb92-129">그런 다음 (실행, 작성) toocollect 로그의 hello 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-129">Then, select hello categories of logs that you want toocollect (Execution, Authoring).</span></span> 

5.  <span data-ttu-id="6eb92-130">Hello 새 진단 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-130">Save hello new diagnostics configuration.</span></span>

<span data-ttu-id="6eb92-131">hello 진단 구성에는 약 10 분 tootake 적용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-131">hello diagnostics configuration takes about 10 minutes tootake effect.</span></span> <span data-ttu-id="6eb92-132">그 후 hello 로그 보관 hello 구성 대상에 나타나는 시작 (hello에서이 확인할 수 있습니다 **진단 로그** 페이지):</span><span class="sxs-lookup"><span data-stu-id="6eb92-132">After that, hello logs start appearing in hello configured archival target (you can see these on hello **Diagnostics logs** page):</span></span>

![블레이드 탐색 toodiagnostics 로그-보관 대상](./media/stream-analytics-job-diagnostic-logs/image4.png)

<span data-ttu-id="6eb92-134">진단을 구성하는 방법에 대한 자세한 내용은 [Azure 리소스의 진단 데이터 수집 및 사용](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb92-134">For more information about configuring diagnostics, see [Collect and consume diagnostics data from your Azure resources](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span></span>

## <a name="diagnostics-log-categories"></a><span data-ttu-id="6eb92-135">진단 로그 범주</span><span class="sxs-lookup"><span data-stu-id="6eb92-135">Diagnostics log categories</span></span>

<span data-ttu-id="6eb92-136">현재 두 가지 진단 로그 범주를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-136">Currently, we capture two categories of diagnostics logs:</span></span>

* <span data-ttu-id="6eb92-137">**작성**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-137">**Authoring**.</span></span> <span data-ttu-id="6eb92-138">캡처 작업을 제작 하는 관련된 toojob 된 이벤트 로그: 작업 만들기를 추가 하 고 입력 및 출력을 추가 하 고 hello 쿼리, 시작 및 중지 hello 작업 업데이트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-138">Captures log events that are related toojob authoring operations: job creation, adding and deleting inputs and outputs, adding and updating hello query, starting and stopping hello job.</span></span>
* <span data-ttu-id="6eb92-139">**실행**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-139">**Execution**.</span></span> <span data-ttu-id="6eb92-140">작업 실행 중 발생하는 이벤트를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-140">Captures events that occur during job execution:</span></span>
    * <span data-ttu-id="6eb92-141">연결 오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-141">Connectivity errors</span></span>
    * <span data-ttu-id="6eb92-142">다음을 포함하는 데이터 처리 오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-142">Data processing errors, including:</span></span>
        * <span data-ttu-id="6eb92-143">Toohello 따르지 않는 이벤트 쿼리 정의 (일치 하지 않는 필드 형식, 누락 된 필드 및 값 등)</span><span class="sxs-lookup"><span data-stu-id="6eb92-143">Events that don’t conform toohello query definition (mismatched field types and values, missing fields, and so on)</span></span>
        * <span data-ttu-id="6eb92-144">식 평가 오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-144">Expression evaluation errors</span></span>
    * <span data-ttu-id="6eb92-145">다른 이벤트 및 오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-145">Other events and errors</span></span>

## <a name="diagnostics-logs-schema"></a><span data-ttu-id="6eb92-146">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="6eb92-146">Diagnostics logs schema</span></span>

<span data-ttu-id="6eb92-147">모든 로그는 JSON 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-147">All logs are stored in JSON format.</span></span> <span data-ttu-id="6eb92-148">각 항목에 공통 문자열 필드에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="6eb92-148">Each entry has hello following common string fields:</span></span>

<span data-ttu-id="6eb92-149">이름</span><span class="sxs-lookup"><span data-stu-id="6eb92-149">Name</span></span> | <span data-ttu-id="6eb92-150">설명</span><span class="sxs-lookup"><span data-stu-id="6eb92-150">Description</span></span>
------- | -------
<span data-ttu-id="6eb92-151">실시간</span><span class="sxs-lookup"><span data-stu-id="6eb92-151">time</span></span> | <span data-ttu-id="6eb92-152">타임 스탬프 (UTC) hello 로그의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-152">Timestamp (in UTC) of hello log.</span></span>
<span data-ttu-id="6eb92-153">resourceId</span><span class="sxs-lookup"><span data-stu-id="6eb92-153">resourceId</span></span> | <span data-ttu-id="6eb92-154">작업 hello hello 리소스의 ID에 발생, 대문자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-154">ID of hello resource that hello operation took place on, in upper case.</span></span> <span data-ttu-id="6eb92-155">Hello 구독 ID, hello 리소스 그룹 및 hello 작업 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-155">It includes hello subscription ID, hello resource group, and hello job name.</span></span> <span data-ttu-id="6eb92-156">예: **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-156">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span></span>
<span data-ttu-id="6eb92-157">카테고리</span><span class="sxs-lookup"><span data-stu-id="6eb92-157">category</span></span> | <span data-ttu-id="6eb92-158">로그 범주로, **실행** 또는 **작성** 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-158">Log category, either **Execution** or **Authoring**.</span></span>
<span data-ttu-id="6eb92-159">operationName</span><span class="sxs-lookup"><span data-stu-id="6eb92-159">operationName</span></span> | <span data-ttu-id="6eb92-160">기록 된 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-160">Name of hello operation that is logged.</span></span> <span data-ttu-id="6eb92-161">예를 들어 **이벤트 보내기: SQL 출력 쓰기 실패 toomysqloutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-161">For example, **Send Events: SQL Output write failure toomysqloutput**.</span></span>
<span data-ttu-id="6eb92-162">status</span><span class="sxs-lookup"><span data-stu-id="6eb92-162">status</span></span> | <span data-ttu-id="6eb92-163">Hello 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-163">Status of hello operation.</span></span> <span data-ttu-id="6eb92-164">예: **실패** 또는 **성공**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-164">For example, **Failed** or **Succeeded**.</span></span>
<span data-ttu-id="6eb92-165">최소 수준</span><span class="sxs-lookup"><span data-stu-id="6eb92-165">level</span></span> | <span data-ttu-id="6eb92-166">로그 수준.</span><span class="sxs-lookup"><span data-stu-id="6eb92-166">Log level.</span></span> <span data-ttu-id="6eb92-167">예: **오류**, **경고** 또는 **정보**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-167">For example, **Error**, **Warning**, or **Informational**.</span></span>
<span data-ttu-id="6eb92-168">properties</span><span class="sxs-lookup"><span data-stu-id="6eb92-168">properties</span></span> | <span data-ttu-id="6eb92-169">로그 항목별 세부 정보로, JSON 문자열로 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-169">Log entry-specific detail, serialized as a JSON string.</span></span> <span data-ttu-id="6eb92-170">자세한 내용은 hello 다음 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb92-170">For more information, see hello following sections.</span></span>

### <a name="execution-log-properties-schema"></a><span data-ttu-id="6eb92-171">실행 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="6eb92-171">Execution log properties schema</span></span>

<span data-ttu-id="6eb92-172">실행 로그에는 Stream Analytics 작업 실행 중에 발생한 이벤트에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-172">Execution logs have information about events that happened during Stream Analytics job execution.</span></span> <span data-ttu-id="6eb92-173">속성의 hello 스키마 이벤트의 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-173">hello schema of properties varies, depending on hello type of event.</span></span> <span data-ttu-id="6eb92-174">현재 실행 로그의 유형만 hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-174">Currently, we have hello following types of execution logs:</span></span>

### <a name="data-errors"></a><span data-ttu-id="6eb92-175">데이터 오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-175">Data errors</span></span>

<span data-ttu-id="6eb92-176">이 범주의 로그 hello 작업은 데이터를 처리 하는 동안 발생 하는 모든 오류가입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-176">Any error that occurs while hello job is processing data is in this category of logs.</span></span> <span data-ttu-id="6eb92-177">이러한 로그는 데이터 읽기, serialization 및 쓰기 작업 도중에 가장 자주 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-177">These logs most often are created during data read, serialization, and write operations.</span></span> <span data-ttu-id="6eb92-178">이러한 로그는 연결 오류를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-178">These logs do not include connectivity errors.</span></span> <span data-ttu-id="6eb92-179">연결 오류는 일반 이벤트로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-179">Connectivity errors are treated as generic events.</span></span>

<span data-ttu-id="6eb92-180">이름</span><span class="sxs-lookup"><span data-stu-id="6eb92-180">Name</span></span> | <span data-ttu-id="6eb92-181">설명</span><span class="sxs-lookup"><span data-stu-id="6eb92-181">Description</span></span>
------- | -------
<span data-ttu-id="6eb92-182">원본</span><span class="sxs-lookup"><span data-stu-id="6eb92-182">Source</span></span> | <span data-ttu-id="6eb92-183">Hello 작업의 이름 입력 또는 출력 hello 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-183">Name of hello job input or output where hello error occurred.</span></span>
<span data-ttu-id="6eb92-184">Message</span><span class="sxs-lookup"><span data-stu-id="6eb92-184">Message</span></span> | <span data-ttu-id="6eb92-185">Hello 오류와 관련 된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-185">Message associated with hello error.</span></span>
<span data-ttu-id="6eb92-186">형식</span><span class="sxs-lookup"><span data-stu-id="6eb92-186">Type</span></span> | <span data-ttu-id="6eb92-187">오류의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-187">Type of error.</span></span> <span data-ttu-id="6eb92-188">예: **DataConversionError**, **CsvParserError** 또는 **ServiceBusPropertyColumnMissingError**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-188">For example, **DataConversionError**, **CsvParserError**, or **ServiceBusPropertyColumnMissingError**.</span></span>
<span data-ttu-id="6eb92-189">Data</span><span class="sxs-lookup"><span data-stu-id="6eb92-189">Data</span></span> | <span data-ttu-id="6eb92-190">유용한 데이터를 포함 tooaccurately hello hello 오류 소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-190">Contains data that is useful tooaccurately locate hello source of hello error.</span></span> <span data-ttu-id="6eb92-191">크기에 따라 제목 tootruncation 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-191">Subject tootruncation, depending on size.</span></span>

<span data-ttu-id="6eb92-192">Hello에 따라 **operationName** 값, 데이터 오류의 경우 스키마를 따르는 hello:</span><span class="sxs-lookup"><span data-stu-id="6eb92-192">Depending on hello **operationName** value, data errors have hello following schema:</span></span>
* <span data-ttu-id="6eb92-193">**직렬화 이벤트**입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-193">**Serialize events**.</span></span> <span data-ttu-id="6eb92-194">직렬화 이벤트는 이벤트 읽기 작업 중에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-194">Serialize events occur during event read operations.</span></span> <span data-ttu-id="6eb92-195">Hello hello 입력 데이터에 맞지 않는 hello 쿼리 스키마 다음이 이유 중 하나에 대 한 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-195">They occur when hello data at hello input does not satisfy hello query schema for one of these reasons:</span></span>
    * <span data-ttu-id="6eb92-196">*이벤트 (de) 하는 동안 형식 불일치 serialize*: hello 오류가 발생 하는 hello 필드를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-196">*Type mismatch during event (de)serialize*: Identifies hello field that's causing hello error.</span></span>
    * <span data-ttu-id="6eb92-197">*이벤트, 잘못 된 직렬화를 읽을 수 없습니다*: hello 오류가 발생 hello 입력된 데이터에 hello 위치에 대 한 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-197">*Cannot read an event, invalid serialization*: Lists information about hello location in hello input data where hello error occurred.</span></span> <span data-ttu-id="6eb92-198">Blob 이름이 blob 입력, 오프셋 및 hello 데이터의 샘플에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-198">Includes blob name for blob input, offset, and a sample of hello data.</span></span>
* <span data-ttu-id="6eb92-199">**전송 이벤트**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-199">**Send events**.</span></span> <span data-ttu-id="6eb92-200">전송 이벤트는 쓰기 작업 중에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-200">Send events occur during write operations.</span></span> <span data-ttu-id="6eb92-201">Hello 스트리밍 hello 오류를 발생 시킨 이벤트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-201">They identify hello streaming event that caused hello error.</span></span>

### <a name="generic-events"></a><span data-ttu-id="6eb92-202">일반 이벤트</span><span class="sxs-lookup"><span data-stu-id="6eb92-202">Generic events</span></span>

<span data-ttu-id="6eb92-203">일반 이벤트는 다른 모든 항목을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-203">Generic events cover everything else.</span></span>

<span data-ttu-id="6eb92-204">이름</span><span class="sxs-lookup"><span data-stu-id="6eb92-204">Name</span></span> | <span data-ttu-id="6eb92-205">설명</span><span class="sxs-lookup"><span data-stu-id="6eb92-205">Description</span></span>
-------- | --------
<span data-ttu-id="6eb92-206">오류</span><span class="sxs-lookup"><span data-stu-id="6eb92-206">Error</span></span> | <span data-ttu-id="6eb92-207">(선택 사항) 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-207">(optional) Error information.</span></span> <span data-ttu-id="6eb92-208">일반적으로 사용 가능한 경우 예외 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-208">Usually, this is exception information, if it's available.</span></span>
<span data-ttu-id="6eb92-209">Message</span><span class="sxs-lookup"><span data-stu-id="6eb92-209">Message</span></span>| <span data-ttu-id="6eb92-210">로그 메시지</span><span class="sxs-lookup"><span data-stu-id="6eb92-210">Log message.</span></span>
<span data-ttu-id="6eb92-211">형식</span><span class="sxs-lookup"><span data-stu-id="6eb92-211">Type</span></span> | <span data-ttu-id="6eb92-212">메시지 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-212">Type of message.</span></span> <span data-ttu-id="6eb92-213">오류의 toointernal 분류를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-213">Maps toointernal categorization of errors.</span></span> <span data-ttu-id="6eb92-214">예: **JobValidationError** 또는 **BlobOutputAdapterInitializationFailure**.</span><span class="sxs-lookup"><span data-stu-id="6eb92-214">For example, **JobValidationError** or **BlobOutputAdapterInitializationFailure**.</span></span>
<span data-ttu-id="6eb92-215">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="6eb92-215">Correlation ID</span></span> | <span data-ttu-id="6eb92-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) hello 작업이 실행을 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies hello job execution.</span></span> <span data-ttu-id="6eb92-217">동일한 hello 작업 중지 hello 있을 때까지 hello 시간 hello에서 모든 실행 로그 항목에 시작 작업 **상관 관계 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb92-217">All execution log entries from hello time hello job starts until hello job stops have hello same **Correlation ID** value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eb92-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6eb92-218">Next steps</span></span>

* [<span data-ttu-id="6eb92-219">소개 tooStream 분석</span><span class="sxs-lookup"><span data-stu-id="6eb92-219">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6eb92-220">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="6eb92-220">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6eb92-221">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6eb92-221">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6eb92-222">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="6eb92-222">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6eb92-223">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="6eb92-223">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
