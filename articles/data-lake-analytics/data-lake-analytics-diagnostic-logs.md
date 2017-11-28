---
title: "Azure Data Lake 분석에 대 한 진단 로그 aaaViewing | Microsoft Docs"
description: "Toosetup 및 진단 액세스 기록 하는 방법에 대 한 Azure 데이터 레이크 분석 이해 "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="dc50f-103">Azure Data Lake Analytics에 대한 진단 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="dc50f-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="dc50f-104">진단 로깅 toocollect 데이터 액세스 감사 내역은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="dc50f-105">이러한 로그는 다음과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-105">These logs provide information such as:</span></span>

* <span data-ttu-id="dc50f-106">Hello 데이터에 액세스 하는 사용자의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="dc50f-107">얼마나 자주 hello 데이터 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="dc50f-108">데이터의 양을 hello 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="dc50f-109">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="dc50f-109">Enable logging</span></span>

1. <span data-ttu-id="dc50f-110">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="dc50f-111">Data Lake 분석 계정을 열고 선택 **진단 로그** hello에서 __모니터__ 섹션.</span><span class="sxs-lookup"><span data-stu-id="dc50f-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="dc50f-112">다음으로, __진단 상태 켜기__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-112">Next, select __Turn on diagnostics__.</span></span>

    ![진단 toocollect 감사를 켜고 요청 로그](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="dc50f-114">__진단 설정을__hello 상태 too__On__를 설정 하 고 로깅 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="dc50f-115">![요청 로그 및 진단 toocollect 감사 설정](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "진단 로그를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="dc50f-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="dc50f-116">설정 **상태** 너무**에** tooenable 진단 로깅.</span><span class="sxs-lookup"><span data-stu-id="dc50f-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="dc50f-117">세 가지 방법으로 toostore/프로세스 hello 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="dc50f-118">선택 __tooa 저장소 계정 보관__ toostore가 Azure 저장소 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="dc50f-119">Tooarchive hello 데이터를 원하는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="dc50f-120">이 옵션을 선택 하는 경우에 Azure 저장소 계정 toosave hello 로그를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="dc50f-121">선택 **tooan 이벤트 허브를 Stream** toostream 로그 데이터 tooan Azure 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="dc50f-122">들어오는 로그를 실시간으로 분석하는 다운스트림 처리 파이프라인을 사용하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="dc50f-123">이 옵션을 선택 하는 경우에 hello toouse를 원하는 Azure 이벤트 허브에 대 한 hello 세부 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="dc50f-124">선택 __tooLog 분석 보내기__ toosend hello 데이터 toohello 로그 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="dc50f-125">로그 분석 toogather toouse 원하는 로그를 분석 하는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="dc50f-126">Tooget 감사 로그 나 요청 로그 중 하나 또는 둘 다에 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="dc50f-127">요청 로그는 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-127">A request log captures every API request.</span></span> <span data-ttu-id="dc50f-128">감사 로그는 해당 API 요청에 의해 트리거되는 모든 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="dc50f-129">에 대 한 __tooa 저장소 계정 보관__, hello tooretain hello 데이터 일 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="dc50f-130">__저장__을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dc50f-131">하나를 선택 해야 __tooa 저장소 계정 보관__, __tooan 이벤트 허브를 Stream__ 또는 __tooLog 분석 보내기__ hello 클릭 하기 전에 __저장__단추입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="dc50f-132">진단 설정을 사용 하도록 설정한 후 toohello 반환할 수 있습니다 __진단 로그__ 블레이드 tooview hello 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="dc50f-133">로그 보기</span><span class="sxs-lookup"><span data-stu-id="dc50f-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="dc50f-134">Hello Data Lake 분석 보기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="dc50f-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="dc50f-135">Data Lake 분석에서 블레이드에서 아래에서 계정 **모니터링**선택, **진단 로그** 및 항목 toodisplay 로그를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="dc50f-136">![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="dc50f-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="dc50f-137">hello 로그는로 분류 되어 **감사 로그** 및 **요청 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![로그 항목](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="dc50f-139">요청 로그 hello Data Lake 분석 계정에 수행 된 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="dc50f-140">감사 로그는 유사한 toorequest 로그 되지만 더욱 세부적인된 분석 hello 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="dc50f-141">예를 들어, 요청 로그에서 단일 업로드 API 호출은 감사 로그에서 여러 "추가" 작업을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="dc50f-142">Hello 클릭 **다운로드** 로그 하는 로그 항목 toodownload에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="dc50f-143">로그 데이터를 포함 하는 hello Azure 저장소 계정 사용</span><span class="sxs-lookup"><span data-stu-id="dc50f-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="dc50f-144">로깅에 대 한 연결 된 데이터 레이크 분석 hello Azure 저장소 계정 블레이드를 열고 클릭 __Blob__합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="dc50f-145">hello **Blob 서비스** 블레이드에 두 개의 컨테이너를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="dc50f-146">![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="dc50f-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="dc50f-147">hello 컨테이너 **insights 로그 감사** hello 감사 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="dc50f-148">hello 컨테이너 **insights 로그 요청이** hello 요청 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="dc50f-149">이러한 컨테이너 내에서 hello 로그 hello 구조를 다음으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="dc50f-150">hello `##` hello 경로에 항목이 hello 연도, 월, 일 및 어떤 hello 로그가 만들어진 시간을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="dc50f-151">Data Lake Analytics는 1시간마다 하나의 파일을 만들므로 `m=`은(는) 항상 `00`의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="dc50f-152">예를 들어 hello 전체 경로 tooan 감사 로그 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="dc50f-153">마찬가지로, hello 전체 경로 tooa 요청 로그 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="dc50f-154">로그 구조</span><span class="sxs-lookup"><span data-stu-id="dc50f-154">Log structure</span></span>

<span data-ttu-id="dc50f-155">hello 감사 및 요청 로그는 구조화 된 JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="dc50f-156">요청 로그</span><span class="sxs-lookup"><span data-stu-id="dc50f-156">Request logs</span></span>

<span data-ttu-id="dc50f-157">Hello JSON 형식의 요청 로그에서 샘플 항목 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="dc50f-158">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="dc50f-159">요청 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="dc50f-159">Request log schema</span></span>

| <span data-ttu-id="dc50f-160">Name</span><span class="sxs-lookup"><span data-stu-id="dc50f-160">Name</span></span> | <span data-ttu-id="dc50f-161">형식</span><span class="sxs-lookup"><span data-stu-id="dc50f-161">Type</span></span> | <span data-ttu-id="dc50f-162">설명</span><span class="sxs-lookup"><span data-stu-id="dc50f-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc50f-163">실시간</span><span class="sxs-lookup"><span data-stu-id="dc50f-163">time</span></span> |<span data-ttu-id="dc50f-164">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-164">String</span></span> |<span data-ttu-id="dc50f-165">hello 타임 스탬프 (UTC) hello 로그</span><span class="sxs-lookup"><span data-stu-id="dc50f-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="dc50f-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc50f-166">resourceId</span></span> |<span data-ttu-id="dc50f-167">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-167">String</span></span> |<span data-ttu-id="dc50f-168">작업에서 걸리는 hello 리소스의 hello 식별자에 배치</span><span class="sxs-lookup"><span data-stu-id="dc50f-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="dc50f-169">카테고리</span><span class="sxs-lookup"><span data-stu-id="dc50f-169">category</span></span> |<span data-ttu-id="dc50f-170">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-170">String</span></span> |<span data-ttu-id="dc50f-171">hello 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-171">hello log category.</span></span> <span data-ttu-id="dc50f-172">예: **Requests**</span><span class="sxs-lookup"><span data-stu-id="dc50f-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="dc50f-173">operationName</span><span class="sxs-lookup"><span data-stu-id="dc50f-173">operationName</span></span> |<span data-ttu-id="dc50f-174">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-174">String</span></span> |<span data-ttu-id="dc50f-175">기록 된 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="dc50f-176">예를 들어 GetAggregatedJobHistory</span><span class="sxs-lookup"><span data-stu-id="dc50f-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="dc50f-177">resultType</span><span class="sxs-lookup"><span data-stu-id="dc50f-177">resultType</span></span> |<span data-ttu-id="dc50f-178">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-178">String</span></span> |<span data-ttu-id="dc50f-179">예를 들어 200 hello 연산의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="dc50f-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="dc50f-180">callerIpAddress</span></span> |<span data-ttu-id="dc50f-181">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-181">String</span></span> |<span data-ttu-id="dc50f-182">hello 요청을 만드는 hello 클라이언트의 hello IP 주소</span><span class="sxs-lookup"><span data-stu-id="dc50f-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="dc50f-183">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="dc50f-183">correlationId</span></span> |<span data-ttu-id="dc50f-184">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-184">String</span></span> |<span data-ttu-id="dc50f-185">hello 로그의 hello 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-185">hello identifier of hello log.</span></span> <span data-ttu-id="dc50f-186">이 값에 사용 되는 toogroup는 관련된 로그 항목 집합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="dc50f-187">ID</span><span class="sxs-lookup"><span data-stu-id="dc50f-187">identity</span></span> |<span data-ttu-id="dc50f-188">Object</span><span class="sxs-lookup"><span data-stu-id="dc50f-188">Object</span></span> |<span data-ttu-id="dc50f-189">hello 로그를 생성 하는 hello id</span><span class="sxs-lookup"><span data-stu-id="dc50f-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="dc50f-190">properties</span><span class="sxs-lookup"><span data-stu-id="dc50f-190">properties</span></span> |<span data-ttu-id="dc50f-191">JSON</span><span class="sxs-lookup"><span data-stu-id="dc50f-191">JSON</span></span> |<span data-ttu-id="dc50f-192">자세한 내용은 hello 다음 섹션 (요청 로그 속성 스키마)를 참조 하십시오</span><span class="sxs-lookup"><span data-stu-id="dc50f-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="dc50f-193">요청 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="dc50f-193">Request log properties schema</span></span>

| <span data-ttu-id="dc50f-194">Name</span><span class="sxs-lookup"><span data-stu-id="dc50f-194">Name</span></span> | <span data-ttu-id="dc50f-195">형식</span><span class="sxs-lookup"><span data-stu-id="dc50f-195">Type</span></span> | <span data-ttu-id="dc50f-196">설명</span><span class="sxs-lookup"><span data-stu-id="dc50f-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc50f-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="dc50f-197">HttpMethod</span></span> |<span data-ttu-id="dc50f-198">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-198">String</span></span> |<span data-ttu-id="dc50f-199">hello HTTP 메서드가 사용 hello 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="dc50f-200">예를 들어 GET</span><span class="sxs-lookup"><span data-stu-id="dc50f-200">For example, GET.</span></span> |
| <span data-ttu-id="dc50f-201">Path</span><span class="sxs-lookup"><span data-stu-id="dc50f-201">Path</span></span> |<span data-ttu-id="dc50f-202">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-202">String</span></span> |<span data-ttu-id="dc50f-203">hello 경로 hello 작업에 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="dc50f-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="dc50f-204">RequestContentLength</span></span> |<span data-ttu-id="dc50f-205">int</span><span class="sxs-lookup"><span data-stu-id="dc50f-205">int</span></span> |<span data-ttu-id="dc50f-206">hello hello HTTP 요청의 콘텐츠 길이</span><span class="sxs-lookup"><span data-stu-id="dc50f-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="dc50f-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="dc50f-207">ClientRequestId</span></span> |<span data-ttu-id="dc50f-208">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-208">String</span></span> |<span data-ttu-id="dc50f-209">이 요청을 고유 하 게 식별 하는 hello 식별자</span><span class="sxs-lookup"><span data-stu-id="dc50f-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="dc50f-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-210">StartTime</span></span> |<span data-ttu-id="dc50f-211">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-211">String</span></span> |<span data-ttu-id="dc50f-212">hello는 hello 받은 서버 hello 요청 시간</span><span class="sxs-lookup"><span data-stu-id="dc50f-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="dc50f-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-213">EndTime</span></span> |<span data-ttu-id="dc50f-214">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-214">String</span></span> |<span data-ttu-id="dc50f-215">hello 시간은 hello 서버 응답 전송</span><span class="sxs-lookup"><span data-stu-id="dc50f-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="dc50f-216">감사 로그</span><span class="sxs-lookup"><span data-stu-id="dc50f-216">Audit logs</span></span>

<span data-ttu-id="dc50f-217">Hello JSON 형식 감사 로그에 샘플 항목 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="dc50f-218">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="dc50f-219">감사 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="dc50f-219">Audit log schema</span></span>

| <span data-ttu-id="dc50f-220">Name</span><span class="sxs-lookup"><span data-stu-id="dc50f-220">Name</span></span> | <span data-ttu-id="dc50f-221">형식</span><span class="sxs-lookup"><span data-stu-id="dc50f-221">Type</span></span> | <span data-ttu-id="dc50f-222">설명</span><span class="sxs-lookup"><span data-stu-id="dc50f-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc50f-223">실시간</span><span class="sxs-lookup"><span data-stu-id="dc50f-223">time</span></span> |<span data-ttu-id="dc50f-224">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-224">String</span></span> |<span data-ttu-id="dc50f-225">hello 타임 스탬프 (UTC) hello 로그</span><span class="sxs-lookup"><span data-stu-id="dc50f-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="dc50f-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc50f-226">resourceId</span></span> |<span data-ttu-id="dc50f-227">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-227">String</span></span> |<span data-ttu-id="dc50f-228">작업에서 걸리는 hello 리소스의 hello 식별자에 배치</span><span class="sxs-lookup"><span data-stu-id="dc50f-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="dc50f-229">카테고리</span><span class="sxs-lookup"><span data-stu-id="dc50f-229">category</span></span> |<span data-ttu-id="dc50f-230">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-230">String</span></span> |<span data-ttu-id="dc50f-231">hello 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-231">hello log category.</span></span> <span data-ttu-id="dc50f-232">예: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="dc50f-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="dc50f-233">operationName</span><span class="sxs-lookup"><span data-stu-id="dc50f-233">operationName</span></span> |<span data-ttu-id="dc50f-234">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-234">String</span></span> |<span data-ttu-id="dc50f-235">기록 된 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="dc50f-236">예를 들어 JobSubmitted</span><span class="sxs-lookup"><span data-stu-id="dc50f-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="dc50f-237">resultType</span><span class="sxs-lookup"><span data-stu-id="dc50f-237">resultType</span></span> |<span data-ttu-id="dc50f-238">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-238">String</span></span> |<span data-ttu-id="dc50f-239">Hello 작업 상태 (operationName)에 대 한 하위 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="dc50f-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="dc50f-240">resultSignature</span></span> |<span data-ttu-id="dc50f-241">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-241">String</span></span> |<span data-ttu-id="dc50f-242">Hello에 대 한 자세한 내용은 작업 상태 (operationName).</span><span class="sxs-lookup"><span data-stu-id="dc50f-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="dc50f-243">ID</span><span class="sxs-lookup"><span data-stu-id="dc50f-243">identity</span></span> |<span data-ttu-id="dc50f-244">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-244">String</span></span> |<span data-ttu-id="dc50f-245">hello 작업을 요청한 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-245">hello user that requested hello operation.</span></span> <span data-ttu-id="dc50f-246">예: susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="dc50f-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="dc50f-247">properties</span><span class="sxs-lookup"><span data-stu-id="dc50f-247">properties</span></span> |<span data-ttu-id="dc50f-248">JSON</span><span class="sxs-lookup"><span data-stu-id="dc50f-248">JSON</span></span> |<span data-ttu-id="dc50f-249">자세한 내용은 hello 다음 섹션 (감사 로그 속성 스키마)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc50f-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="dc50f-250">**resultType** 및 **resultSignature** hello 결과 작업의 정보를 제공 하 고 작업을 완료 하는 경우에 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="dc50f-251">예를 들어 **operationName**이 **JobStarted** 또는 **JobEnded**의 값을 포함할 때 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="dc50f-252">감사 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="dc50f-252">Audit log properties schema</span></span>

| <span data-ttu-id="dc50f-253">Name</span><span class="sxs-lookup"><span data-stu-id="dc50f-253">Name</span></span> | <span data-ttu-id="dc50f-254">형식</span><span class="sxs-lookup"><span data-stu-id="dc50f-254">Type</span></span> | <span data-ttu-id="dc50f-255">설명</span><span class="sxs-lookup"><span data-stu-id="dc50f-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc50f-256">JobId</span><span class="sxs-lookup"><span data-stu-id="dc50f-256">JobId</span></span> |<span data-ttu-id="dc50f-257">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-257">String</span></span> |<span data-ttu-id="dc50f-258">hello ID 할당된 toohello 작업</span><span class="sxs-lookup"><span data-stu-id="dc50f-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="dc50f-259">JobName</span><span class="sxs-lookup"><span data-stu-id="dc50f-259">JobName</span></span> |<span data-ttu-id="dc50f-260">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-260">String</span></span> |<span data-ttu-id="dc50f-261">hello 작업에 대해 제공 된 hello 이름</span><span class="sxs-lookup"><span data-stu-id="dc50f-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="dc50f-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-262">JobRunTime</span></span> |<span data-ttu-id="dc50f-263">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-263">String</span></span> |<span data-ttu-id="dc50f-264">hello 런타임 tooprocess hello 작업 사용</span><span class="sxs-lookup"><span data-stu-id="dc50f-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="dc50f-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-265">SubmitTime</span></span> |<span data-ttu-id="dc50f-266">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-266">String</span></span> |<span data-ttu-id="dc50f-267">hello 시간 (UTC)에 해당 hello 작업이 제출 된</span><span class="sxs-lookup"><span data-stu-id="dc50f-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="dc50f-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-268">StartTime</span></span> |<span data-ttu-id="dc50f-269">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-269">String</span></span> |<span data-ttu-id="dc50f-270">hello 시간 hello 작업 제출 (UTC)에서 실행이 시작</span><span class="sxs-lookup"><span data-stu-id="dc50f-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="dc50f-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="dc50f-271">EndTime</span></span> |<span data-ttu-id="dc50f-272">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-272">String</span></span> |<span data-ttu-id="dc50f-273">hello 시간 hello 작업 종료</span><span class="sxs-lookup"><span data-stu-id="dc50f-273">hello time hello job ended</span></span> |
| <span data-ttu-id="dc50f-274">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="dc50f-274">Parallelism</span></span> |<span data-ttu-id="dc50f-275">문자열</span><span class="sxs-lookup"><span data-stu-id="dc50f-275">String</span></span> |<span data-ttu-id="dc50f-276">데이터 레이크 분석 단위 제출 하는 동안이 작업에 대해 요청 된 hello 수</span><span class="sxs-lookup"><span data-stu-id="dc50f-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="dc50f-277">**SubmitTime**, **StartTime**, **EndTime** 및 **Parallelism**은 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="dc50f-278">해당 작업이 시작 또는 완료되는 경우 이러한 항목만 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="dc50f-279">예를 들어 **SubmitTime** 만 후 값이 포함 된 **operationName** hello 값 **JobSubmitted**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="dc50f-280">프로세스 hello 로그 데이터</span><span class="sxs-lookup"><span data-stu-id="dc50f-280">Process hello log data</span></span>

<span data-ttu-id="dc50f-281">Azure Data Lake 분석 방법에 대 한 샘플을 제공 tooprocess hello 로그 데이터를 분석 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="dc50f-282">Hello에 있는 샘플을 찾을 수 있습니다 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc50f-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc50f-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc50f-283">Next steps</span></span>
* [<span data-ttu-id="dc50f-284">Azure Data Lake Analytics 개요</span><span class="sxs-lookup"><span data-stu-id="dc50f-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
