---
title: "Azure Data Lake Analytics에 대한 진단 로그 보기 | Microsoft Docs"
description: "Azure Data Lake Analytics에 대한 진단 로그를 설정하고 액세스하는 방법을 이해합니다. "
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
ms.openlocfilehash: 6c74db1659742aa41306388273bec46800ba7609
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="92da3-103">Azure Data Lake Analytics에 대한 진단 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="92da3-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="92da3-104">진단 로깅을 사용하면 데이터 액세스 감사 내역을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-104">Diagnostic logging allows you to collect data access audit trails.</span></span> <span data-ttu-id="92da3-105">이러한 로그는 다음과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-105">These logs provide information such as:</span></span>

* <span data-ttu-id="92da3-106">데이터에 액세스하는 사용자의 목록.</span><span class="sxs-lookup"><span data-stu-id="92da3-106">A list of users that accessed the data.</span></span>
* <span data-ttu-id="92da3-107">데이터가 액세스되는 빈도.</span><span class="sxs-lookup"><span data-stu-id="92da3-107">How frequently the data is accessed.</span></span>
* <span data-ttu-id="92da3-108">계정에 저장된 데이터의 양.</span><span class="sxs-lookup"><span data-stu-id="92da3-108">How much data is stored in the account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="92da3-109">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="92da3-109">Enable logging</span></span>

1. <span data-ttu-id="92da3-110">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-110">Sign on to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="92da3-111">Data Lake Analytics 계정을 열고 __모니터링__ 섹션에서 **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-111">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitor__ section.</span></span> <span data-ttu-id="92da3-112">다음으로, __진단 상태 켜기__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-112">Next, select __Turn on diagnostics__.</span></span>

    ![진단을 켜서 감사 및 요청 로그 수집](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="92da3-114">__진단 설정__에서 상태를 __켜기__로 설정하고 로깅 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-114">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="92da3-115">![진단을 켜서 감사 및 요청 로그 수집](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "진단 로그 활성화")</span><span class="sxs-lookup"><span data-stu-id="92da3-115">![Turn on diagnostics to collect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="92da3-116">진단 로깅을 사용하려면 **상태**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-116">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="92da3-117">세 가지 방법으로 데이터를 저장/처리하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-117">You can choose to store/process the data in three different ways.</span></span>

     * <span data-ttu-id="92da3-118">Azure Storage 계정에 로그를 저장하려면 __저장소 계정에 보관__을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-118">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="92da3-119">데이터를 보관하려는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-119">Use this option if you want to archive the data.</span></span> <span data-ttu-id="92da3-120">이 옵션을 선택하는 경우 Azure Storage 계정을 제공하여 로그를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-120">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="92da3-121">Azure Event Hub에 로그 데이터를 스트리밍하려면 **이벤트 허브로 스트리밍**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-121">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="92da3-122">들어오는 로그를 실시간으로 분석하는 다운스트림 처리 파이프라인을 사용하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="92da3-123">이 옵션을 선택하는 경우 사용하려는 Azure 이벤트 허브에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-123">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="92da3-124">__Log Analytics로 보내기__를 선택하여 데이터를 Log Analytics 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-124">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="92da3-125">Log Analytics를 사용하여 로그를 수집하고 분석하려는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-125">Use this option if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="92da3-126">감사 로그 또는 요청 로그를 가져올지, 혹은 둘 모두를 가져올지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-126">Specify whether you want to get audit logs or request logs or both.</span></span>  <span data-ttu-id="92da3-127">요청 로그는 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-127">A request log captures every API request.</span></span> <span data-ttu-id="92da3-128">감사 로그는 해당 API 요청에 의해 트리거되는 모든 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="92da3-129">__저장소 계정에 보관__의 경우 데이터를 보관할 일 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-129">For __Archive to a storage account__, specify the number of days to retain the data.</span></span>

   * <span data-ttu-id="92da3-130">__저장__을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="92da3-131">__저장__ 단추를 클릭하기 전에 __저장소 계정에 보관__, __이벤트 허브로 스트리밍__ 또는 __Log Analytics로 보내기__를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-131">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before clicking the __Save__ button.</span></span>

<span data-ttu-id="92da3-132">진단 설정을 사용하도록 설정했으면 __진단 로그__ 블레이드로 돌아가서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-132">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view the logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="92da3-133">로그 보기</span><span class="sxs-lookup"><span data-stu-id="92da3-133">View logs</span></span>

### <a name="use-the-data-lake-analytics-view"></a><span data-ttu-id="92da3-134">Data Lake Analytics 보기 사용</span><span class="sxs-lookup"><span data-stu-id="92da3-134">Use the Data Lake Analytics view</span></span>

1. <span data-ttu-id="92da3-135">Data Lake Analytics 계정 블레이드의 **모니터링** 아래에서 **진단 로그**를 선택한 다음 로그를 표시할 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry to display logs for.</span></span>

    <span data-ttu-id="92da3-136">![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="92da3-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="92da3-137">로그는 **감사 로그**와 **요청 로그**로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-137">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![로그 항목](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="92da3-139">요청 로그는 Data Lake Analytics 계정에 대한 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-139">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="92da3-140">감사 로그는 요청 로그와 비슷하지만 작업의 훨씬 더 세부적인 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-140">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations.</span></span> <span data-ttu-id="92da3-141">예를 들어, 요청 로그에서 단일 업로드 API 호출은 감사 로그에서 여러 "추가" 작업을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="92da3-142">로그 항목에 대한 **다운로드** 링크를 클릭하여 해당 로그를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-142">Click the **Download** link for a log entry to download that log.</span></span>

### <a name="use-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="92da3-143">로그 데이터를 포함하는 Azure Storage 계정 사용</span><span class="sxs-lookup"><span data-stu-id="92da3-143">Use the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="92da3-144">로깅을 위한 Data Lake Analytics와 연결된 Azure Storage 계정 블레이드를 열고 __Blob__을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-144">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="92da3-145">**Blob service** 블레이드는 두 개의 컨테이너를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-145">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="92da3-146">![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="92da3-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="92da3-147">**insights-logs-audit** 컨테이너는 감사 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-147">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="92da3-148">**insights-logs-requests** 컨테이너는 요청 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-148">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="92da3-149">이러한 컨테이너 내에서 로그는 다음 구조로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-149">Within these containers, the logs are stored under the following structure:</span></span>

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
   > <span data-ttu-id="92da3-150">`##` 항목은 로그가 생성된 연도, 월, 일 및 시간을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-150">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="92da3-151">Data Lake Analytics는 1시간마다 하나의 파일을 만들므로 `m=`은(는) 항상 `00`의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="92da3-152">예를 들어, 감사 로그에 대한 전체 경로는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-152">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="92da3-153">마찬가지로 요청 로그에 대한 전체 경로는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-153">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="92da3-154">로그 구조</span><span class="sxs-lookup"><span data-stu-id="92da3-154">Log structure</span></span>

<span data-ttu-id="92da3-155">감사 로그 및 요청 로그는 구조화된 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-155">The audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="92da3-156">요청 로그</span><span class="sxs-lookup"><span data-stu-id="92da3-156">Request logs</span></span>

<span data-ttu-id="92da3-157">다음은 JSON 형식인 요청 로그의 샘플 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-157">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="92da3-158">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="92da3-159">요청 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="92da3-159">Request log schema</span></span>

| <span data-ttu-id="92da3-160">Name</span><span class="sxs-lookup"><span data-stu-id="92da3-160">Name</span></span> | <span data-ttu-id="92da3-161">형식</span><span class="sxs-lookup"><span data-stu-id="92da3-161">Type</span></span> | <span data-ttu-id="92da3-162">설명</span><span class="sxs-lookup"><span data-stu-id="92da3-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da3-163">실시간</span><span class="sxs-lookup"><span data-stu-id="92da3-163">time</span></span> |<span data-ttu-id="92da3-164">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-164">String</span></span> |<span data-ttu-id="92da3-165">로그의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="92da3-165">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="92da3-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="92da3-166">resourceId</span></span> |<span data-ttu-id="92da3-167">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-167">String</span></span> |<span data-ttu-id="92da3-168">작업이 수행되는 리소스의 식별자</span><span class="sxs-lookup"><span data-stu-id="92da3-168">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="92da3-169">카테고리</span><span class="sxs-lookup"><span data-stu-id="92da3-169">category</span></span> |<span data-ttu-id="92da3-170">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-170">String</span></span> |<span data-ttu-id="92da3-171">로그 범주</span><span class="sxs-lookup"><span data-stu-id="92da3-171">The log category.</span></span> <span data-ttu-id="92da3-172">예: **Requests**</span><span class="sxs-lookup"><span data-stu-id="92da3-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="92da3-173">operationName</span><span class="sxs-lookup"><span data-stu-id="92da3-173">operationName</span></span> |<span data-ttu-id="92da3-174">String</span><span class="sxs-lookup"><span data-stu-id="92da3-174">String</span></span> |<span data-ttu-id="92da3-175">기록된 작업의 이름</span><span class="sxs-lookup"><span data-stu-id="92da3-175">Name of the operation that is logged.</span></span> <span data-ttu-id="92da3-176">예를 들어 GetAggregatedJobHistory</span><span class="sxs-lookup"><span data-stu-id="92da3-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="92da3-177">resultType</span><span class="sxs-lookup"><span data-stu-id="92da3-177">resultType</span></span> |<span data-ttu-id="92da3-178">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-178">String</span></span> |<span data-ttu-id="92da3-179">작업의 상태, 예를 들어 200</span><span class="sxs-lookup"><span data-stu-id="92da3-179">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="92da3-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="92da3-180">callerIpAddress</span></span> |<span data-ttu-id="92da3-181">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-181">String</span></span> |<span data-ttu-id="92da3-182">요청한 클라이언트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="92da3-182">The IP address of the client making the request</span></span> |
| <span data-ttu-id="92da3-183">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="92da3-183">correlationId</span></span> |<span data-ttu-id="92da3-184">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-184">String</span></span> |<span data-ttu-id="92da3-185">로그의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-185">The identifier of the log.</span></span> <span data-ttu-id="92da3-186">이 값을 사용하여 관련된 로그 항목의 집합을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-186">This value can be used to group a set of related log entries.</span></span> |
| <span data-ttu-id="92da3-187">ID</span><span class="sxs-lookup"><span data-stu-id="92da3-187">identity</span></span> |<span data-ttu-id="92da3-188">Object</span><span class="sxs-lookup"><span data-stu-id="92da3-188">Object</span></span> |<span data-ttu-id="92da3-189">로그를 생성하는 ID</span><span class="sxs-lookup"><span data-stu-id="92da3-189">The identity that generated the log</span></span> |
| <span data-ttu-id="92da3-190">properties</span><span class="sxs-lookup"><span data-stu-id="92da3-190">properties</span></span> |<span data-ttu-id="92da3-191">JSON</span><span class="sxs-lookup"><span data-stu-id="92da3-191">JSON</span></span> |<span data-ttu-id="92da3-192">자세한 내용은 다음 섹션(요청 로그 속성 스키마)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92da3-192">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="92da3-193">요청 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="92da3-193">Request log properties schema</span></span>

| <span data-ttu-id="92da3-194">Name</span><span class="sxs-lookup"><span data-stu-id="92da3-194">Name</span></span> | <span data-ttu-id="92da3-195">형식</span><span class="sxs-lookup"><span data-stu-id="92da3-195">Type</span></span> | <span data-ttu-id="92da3-196">설명</span><span class="sxs-lookup"><span data-stu-id="92da3-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da3-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="92da3-197">HttpMethod</span></span> |<span data-ttu-id="92da3-198">String</span><span class="sxs-lookup"><span data-stu-id="92da3-198">String</span></span> |<span data-ttu-id="92da3-199">작업에 사용된 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="92da3-199">The HTTP Method used for the operation.</span></span> <span data-ttu-id="92da3-200">예를 들어 GET</span><span class="sxs-lookup"><span data-stu-id="92da3-200">For example, GET.</span></span> |
| <span data-ttu-id="92da3-201">Path</span><span class="sxs-lookup"><span data-stu-id="92da3-201">Path</span></span> |<span data-ttu-id="92da3-202">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-202">String</span></span> |<span data-ttu-id="92da3-203">작업이 수행된 경로</span><span class="sxs-lookup"><span data-stu-id="92da3-203">The path the operation was performed on</span></span> |
| <span data-ttu-id="92da3-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="92da3-204">RequestContentLength</span></span> |<span data-ttu-id="92da3-205">int</span><span class="sxs-lookup"><span data-stu-id="92da3-205">int</span></span> |<span data-ttu-id="92da3-206">HTTP 요청의 콘텐츠 길이</span><span class="sxs-lookup"><span data-stu-id="92da3-206">The content length of the HTTP request</span></span> |
| <span data-ttu-id="92da3-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="92da3-207">ClientRequestId</span></span> |<span data-ttu-id="92da3-208">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-208">String</span></span> |<span data-ttu-id="92da3-209">이 요청을 고유하게 식별하는 식별자</span><span class="sxs-lookup"><span data-stu-id="92da3-209">The identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="92da3-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="92da3-210">StartTime</span></span> |<span data-ttu-id="92da3-211">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-211">String</span></span> |<span data-ttu-id="92da3-212">서버가 요청을 받은 시간</span><span class="sxs-lookup"><span data-stu-id="92da3-212">The time at which the server received the request</span></span> |
| <span data-ttu-id="92da3-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="92da3-213">EndTime</span></span> |<span data-ttu-id="92da3-214">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-214">String</span></span> |<span data-ttu-id="92da3-215">서버가 응답을 전송한 시간</span><span class="sxs-lookup"><span data-stu-id="92da3-215">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="92da3-216">감사 로그</span><span class="sxs-lookup"><span data-stu-id="92da3-216">Audit logs</span></span>

<span data-ttu-id="92da3-217">다음은 JSON 형식인 감사 로그의 샘플 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-217">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="92da3-218">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="92da3-219">감사 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="92da3-219">Audit log schema</span></span>

| <span data-ttu-id="92da3-220">Name</span><span class="sxs-lookup"><span data-stu-id="92da3-220">Name</span></span> | <span data-ttu-id="92da3-221">형식</span><span class="sxs-lookup"><span data-stu-id="92da3-221">Type</span></span> | <span data-ttu-id="92da3-222">설명</span><span class="sxs-lookup"><span data-stu-id="92da3-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da3-223">실시간</span><span class="sxs-lookup"><span data-stu-id="92da3-223">time</span></span> |<span data-ttu-id="92da3-224">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-224">String</span></span> |<span data-ttu-id="92da3-225">로그의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="92da3-225">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="92da3-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="92da3-226">resourceId</span></span> |<span data-ttu-id="92da3-227">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-227">String</span></span> |<span data-ttu-id="92da3-228">작업이 수행되는 리소스의 식별자</span><span class="sxs-lookup"><span data-stu-id="92da3-228">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="92da3-229">카테고리</span><span class="sxs-lookup"><span data-stu-id="92da3-229">category</span></span> |<span data-ttu-id="92da3-230">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-230">String</span></span> |<span data-ttu-id="92da3-231">로그 범주</span><span class="sxs-lookup"><span data-stu-id="92da3-231">The log category.</span></span> <span data-ttu-id="92da3-232">예: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="92da3-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="92da3-233">operationName</span><span class="sxs-lookup"><span data-stu-id="92da3-233">operationName</span></span> |<span data-ttu-id="92da3-234">String</span><span class="sxs-lookup"><span data-stu-id="92da3-234">String</span></span> |<span data-ttu-id="92da3-235">기록된 작업의 이름</span><span class="sxs-lookup"><span data-stu-id="92da3-235">Name of the operation that is logged.</span></span> <span data-ttu-id="92da3-236">예를 들어 JobSubmitted</span><span class="sxs-lookup"><span data-stu-id="92da3-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="92da3-237">resultType</span><span class="sxs-lookup"><span data-stu-id="92da3-237">resultType</span></span> |<span data-ttu-id="92da3-238">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-238">String</span></span> |<span data-ttu-id="92da3-239">작업 상태(operationName)에 대한 하위 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-239">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="92da3-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="92da3-240">resultSignature</span></span> |<span data-ttu-id="92da3-241">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-241">String</span></span> |<span data-ttu-id="92da3-242">작업 상태(operationName)에 추가 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-242">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="92da3-243">ID</span><span class="sxs-lookup"><span data-stu-id="92da3-243">identity</span></span> |<span data-ttu-id="92da3-244">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-244">String</span></span> |<span data-ttu-id="92da3-245">작업을 요청한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-245">The user that requested the operation.</span></span> <span data-ttu-id="92da3-246">예: susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="92da3-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="92da3-247">properties</span><span class="sxs-lookup"><span data-stu-id="92da3-247">properties</span></span> |<span data-ttu-id="92da3-248">JSON</span><span class="sxs-lookup"><span data-stu-id="92da3-248">JSON</span></span> |<span data-ttu-id="92da3-249">자세한 내용은 다음 섹션(감사 로그 속성 스키마)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92da3-249">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="92da3-250">**resultType** 및 **resultSignature**는 작업의 결과에 대한 정보를 제공하고 작업이 완료되었을 경우에 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-250">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="92da3-251">예를 들어 **operationName**이 **JobStarted** 또는 **JobEnded**의 값을 포함할 때 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="92da3-252">감사 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="92da3-252">Audit log properties schema</span></span>

| <span data-ttu-id="92da3-253">Name</span><span class="sxs-lookup"><span data-stu-id="92da3-253">Name</span></span> | <span data-ttu-id="92da3-254">형식</span><span class="sxs-lookup"><span data-stu-id="92da3-254">Type</span></span> | <span data-ttu-id="92da3-255">설명</span><span class="sxs-lookup"><span data-stu-id="92da3-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da3-256">JobId</span><span class="sxs-lookup"><span data-stu-id="92da3-256">JobId</span></span> |<span data-ttu-id="92da3-257">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-257">String</span></span> |<span data-ttu-id="92da3-258">작업에 할당된 ID</span><span class="sxs-lookup"><span data-stu-id="92da3-258">The ID assigned to the job</span></span> |
| <span data-ttu-id="92da3-259">JobName</span><span class="sxs-lookup"><span data-stu-id="92da3-259">JobName</span></span> |<span data-ttu-id="92da3-260">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-260">String</span></span> |<span data-ttu-id="92da3-261">작업에 대해 제공된 이름</span><span class="sxs-lookup"><span data-stu-id="92da3-261">The name that was provided for the job</span></span> |
| <span data-ttu-id="92da3-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="92da3-262">JobRunTime</span></span> |<span data-ttu-id="92da3-263">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-263">String</span></span> |<span data-ttu-id="92da3-264">작업을 처리하는 데 사용된 런타임</span><span class="sxs-lookup"><span data-stu-id="92da3-264">The runtime used to process the job</span></span> |
| <span data-ttu-id="92da3-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="92da3-265">SubmitTime</span></span> |<span data-ttu-id="92da3-266">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-266">String</span></span> |<span data-ttu-id="92da3-267">작업이 제출된 시간(UTC)</span><span class="sxs-lookup"><span data-stu-id="92da3-267">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="92da3-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="92da3-268">StartTime</span></span> |<span data-ttu-id="92da3-269">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-269">String</span></span> |<span data-ttu-id="92da3-270">제출 후(UTC) 작업이 실행을 시작한 시간</span><span class="sxs-lookup"><span data-stu-id="92da3-270">The time the job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="92da3-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="92da3-271">EndTime</span></span> |<span data-ttu-id="92da3-272">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-272">String</span></span> |<span data-ttu-id="92da3-273">작업이 종료된 시간</span><span class="sxs-lookup"><span data-stu-id="92da3-273">The time the job ended</span></span> |
| <span data-ttu-id="92da3-274">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="92da3-274">Parallelism</span></span> |<span data-ttu-id="92da3-275">문자열</span><span class="sxs-lookup"><span data-stu-id="92da3-275">String</span></span> |<span data-ttu-id="92da3-276">제출하는 동안 이 작업에 대해 요청된 Data Lake Analytics 단위의 수</span><span class="sxs-lookup"><span data-stu-id="92da3-276">The number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="92da3-277">**SubmitTime**, **StartTime**, **EndTime** 및 **Parallelism**은 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="92da3-278">해당 작업이 시작 또는 완료되는 경우 이러한 항목만 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="92da3-279">예를 들어 **operationName**이 **JobSubmitted** 값을 가진 후 **SubmitTime**은 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-279">For example, **SubmitTime** only contains a value after **operationName** has the value **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="92da3-280">로그 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="92da3-280">Process the log data</span></span>

<span data-ttu-id="92da3-281">Azure Data Lake Analytics에서는 로그 데이터를 처리하고 분석하는 방법에 대한 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-281">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="92da3-282">[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)에서 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92da3-282">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92da3-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92da3-283">Next steps</span></span>
* [<span data-ttu-id="92da3-284">Azure Data Lake Analytics 개요</span><span class="sxs-lookup"><span data-stu-id="92da3-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
