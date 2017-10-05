---
title: "Azure Data Lake Store에 대한 진단 로그 보기 | Microsoft 문서"
description: "Azure Data Lake Store에 대한 진단 로그를 설정하고 액세스하는 방법을 이해합니다  "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="b9513-103">Azure Data Lake Store에 대한 진단 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="b9513-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="b9513-104">Data Lake Store 계정에 대한 진단 로깅을 사용하는 방법 및 계정에 대해 수집된 로그를 보는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="b9513-105">조직에서는 Azure Data Lake Store 계정에 대한 진단 로깅을 사용하도록 설정하여 데이터에 액세스하는 사용자의 목록, 데이터가 액세스되는 빈도, 계정에 저장된 데이터 양과 같은 정보를 제공하는 데이터 액세스 감사 추적을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9513-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9513-106">Prerequisites</span></span>
* <span data-ttu-id="b9513-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b9513-107">**An Azure subscription**.</span></span> <span data-ttu-id="b9513-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9513-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b9513-109">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="b9513-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="b9513-110">[Azure Portal을 사용하여 Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)에 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="b9513-111">Data Lake Store 계정에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="b9513-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="b9513-112">새로운 [Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9513-113">Data Lake Store 계정을 열고 Data Lake Store 계정 블레이드에서 **설정**, **진단 로그**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="b9513-114">**진단 로그** 블레이드에서 **진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="b9513-115">![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "진단 로그 사용")</span><span class="sxs-lookup"><span data-stu-id="b9513-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="b9513-116">**진단** 블레이드에서 진단 로깅을 구성하려면 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="b9513-117">![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "진단 로그 사용")</span><span class="sxs-lookup"><span data-stu-id="b9513-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="b9513-118">진단 로깅을 사용하려면 **상태**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="b9513-119">다양한 방법으로 데이터를 저장/처리하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="b9513-120">Azure Storage 계정에 로그를 저장하려면 **저장소 계정에 보관** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="b9513-121">나중에 배치로 처리할 데이터를 보관하려는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="b9513-122">이 옵션을 선택하는 경우 Azure 저장소 계정을 제공하여 로그를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="b9513-123">Azure Event Hub에 로그 데이터를 스트리밍하려면 **이벤트 허브로 스트리밍** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="b9513-124">들어오는 로그를 실시간으로 분석하는 다운스트림 처리 파이프라인을 사용하는 경우 대개 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="b9513-125">이 옵션을 선택하는 경우 사용하려는 Azure 이벤트 허브에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="b9513-126">Azure Log Analytics 서비스를 사용하여 생성된 로그 데이터를 분석하려면 **Log Analytics으로 전송** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="b9513-127">이 옵션을 선택하는 경우 로그 분석을 수행하는 데 사용하는 Operations Management Suite 작업 영역에 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="b9513-128">감사 로그 또는 요청 로그를 가져올지, 혹은 둘 모두를 가져올지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="b9513-129">데이터를 유지해야 하는 일 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="b9513-130">Azure Storage 계정을 사용하여 로그 데이터를 보관하는 경우에만 보존 기능이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="b9513-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-131">Click **Save**.</span></span>

<span data-ttu-id="b9513-132">진단 설정을 사용하도록 설정했으면 **진단 로그** 탭에서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="b9513-133">Data Lake Store 계정에 대한 진단 로그 보기</span><span class="sxs-lookup"><span data-stu-id="b9513-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="b9513-134">두 가지 방법으로 Data Lake Store 계정에 대한 로그 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="b9513-135">Data Lake Store 계정 설정 보기에서</span><span class="sxs-lookup"><span data-stu-id="b9513-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="b9513-136">데이터가 저장된 Azure 저장소 계정에서</span><span class="sxs-lookup"><span data-stu-id="b9513-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="b9513-137">Data Lake Store 설정 보기 사용</span><span class="sxs-lookup"><span data-stu-id="b9513-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="b9513-138">Data Lake Store 계정 **설정** 블레이드에서 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="b9513-139">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="b9513-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="b9513-140">**진단 로그** 블레이드에서 **감사 로그** 및 **요청 로그**로 분류된 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="b9513-141">요청 로그는 Data Lake Store 계정에 대한 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="b9513-142">감사 로그는 요청 로그와 비슷하지만 Data Lake Store 계정에 수행된 작업의 훨씬 더 세부적인 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="b9513-143">예를 들어, 요청 로그에서 단일 업로드 API 호출은 감사 로그에서 여러 "추가" 작업을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="b9513-144">각 로그 항목에 대한 **다운로드** 링크를 클릭하여 로그를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="b9513-145">로그 데이터를 포함하는 Azure 저장소 계정에서</span><span class="sxs-lookup"><span data-stu-id="b9513-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="b9513-146">로깅을 위한 Data Lake Store와 연결된 Azure 저장소 계정 블레이드를 열고 Blob을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="b9513-147">**Blob 서비스** 블레이드는 두 개의 컨테이너를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="b9513-148">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="b9513-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="b9513-149">**insights-logs-audit** 컨테이너는 감사 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="b9513-150">**insights-logs-requests** 컨테이너는 요청 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="b9513-151">이러한 컨테이너 내에서 로그는 다음 구조로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="b9513-152">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="b9513-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="b9513-153">예를 들어, 감사 로그에 대한 전체 경로는 `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="b9513-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="b9513-154">마찬가지로 요청 로그에 대한 전체 경로는 `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="b9513-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="b9513-155">로그 데이터의 구조 이해</span><span class="sxs-lookup"><span data-stu-id="b9513-155">Understand the structure of the log data</span></span>
<span data-ttu-id="b9513-156">감사 로그 및 요청 로그는 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="b9513-157">이 섹션에서는 요청 로그 및 감사 로그에 대한 JSON의 구조를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="b9513-158">요청 로그</span><span class="sxs-lookup"><span data-stu-id="b9513-158">Request logs</span></span>
<span data-ttu-id="b9513-159">다음은 JSON 형식인 요청 로그의 샘플 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="b9513-160">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="b9513-161">요청 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="b9513-161">Request log schema</span></span>
| <span data-ttu-id="b9513-162">Name</span><span class="sxs-lookup"><span data-stu-id="b9513-162">Name</span></span> | <span data-ttu-id="b9513-163">형식</span><span class="sxs-lookup"><span data-stu-id="b9513-163">Type</span></span> | <span data-ttu-id="b9513-164">설명</span><span class="sxs-lookup"><span data-stu-id="b9513-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9513-165">실시간</span><span class="sxs-lookup"><span data-stu-id="b9513-165">time</span></span> |<span data-ttu-id="b9513-166">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-166">String</span></span> |<span data-ttu-id="b9513-167">로그의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="b9513-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="b9513-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="b9513-168">resourceId</span></span> |<span data-ttu-id="b9513-169">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-169">String</span></span> |<span data-ttu-id="b9513-170">작업이 수행되는 리소스의 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="b9513-171">카테고리</span><span class="sxs-lookup"><span data-stu-id="b9513-171">category</span></span> |<span data-ttu-id="b9513-172">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-172">String</span></span> |<span data-ttu-id="b9513-173">로그 범주</span><span class="sxs-lookup"><span data-stu-id="b9513-173">The log category.</span></span> <span data-ttu-id="b9513-174">예: **Requests**</span><span class="sxs-lookup"><span data-stu-id="b9513-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="b9513-175">operationName</span><span class="sxs-lookup"><span data-stu-id="b9513-175">operationName</span></span> |<span data-ttu-id="b9513-176">String</span><span class="sxs-lookup"><span data-stu-id="b9513-176">String</span></span> |<span data-ttu-id="b9513-177">기록된 작업의 이름</span><span class="sxs-lookup"><span data-stu-id="b9513-177">Name of the operation that is logged.</span></span> <span data-ttu-id="b9513-178">예를 들어 getfilestatus</span><span class="sxs-lookup"><span data-stu-id="b9513-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="b9513-179">resultType</span><span class="sxs-lookup"><span data-stu-id="b9513-179">resultType</span></span> |<span data-ttu-id="b9513-180">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-180">String</span></span> |<span data-ttu-id="b9513-181">작업의 상태, 예를 들어 200</span><span class="sxs-lookup"><span data-stu-id="b9513-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="b9513-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="b9513-182">callerIpAddress</span></span> |<span data-ttu-id="b9513-183">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-183">String</span></span> |<span data-ttu-id="b9513-184">요청한 클라이언트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b9513-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="b9513-185">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="b9513-185">correlationId</span></span> |<span data-ttu-id="b9513-186">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-186">String</span></span> |<span data-ttu-id="b9513-187">관련된 로그 항목의 집합을 그룹화하는 데 사용할 수 있는 로그의 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="b9513-188">ID</span><span class="sxs-lookup"><span data-stu-id="b9513-188">identity</span></span> |<span data-ttu-id="b9513-189">Object</span><span class="sxs-lookup"><span data-stu-id="b9513-189">Object</span></span> |<span data-ttu-id="b9513-190">로그를 생성하는 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-190">The identity that generated the log</span></span> |
| <span data-ttu-id="b9513-191">properties</span><span class="sxs-lookup"><span data-stu-id="b9513-191">properties</span></span> |<span data-ttu-id="b9513-192">JSON</span><span class="sxs-lookup"><span data-stu-id="b9513-192">JSON</span></span> |<span data-ttu-id="b9513-193">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9513-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="b9513-194">요청 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="b9513-194">Request log properties schema</span></span>
| <span data-ttu-id="b9513-195">Name</span><span class="sxs-lookup"><span data-stu-id="b9513-195">Name</span></span> | <span data-ttu-id="b9513-196">형식</span><span class="sxs-lookup"><span data-stu-id="b9513-196">Type</span></span> | <span data-ttu-id="b9513-197">설명</span><span class="sxs-lookup"><span data-stu-id="b9513-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9513-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="b9513-198">HttpMethod</span></span> |<span data-ttu-id="b9513-199">String</span><span class="sxs-lookup"><span data-stu-id="b9513-199">String</span></span> |<span data-ttu-id="b9513-200">작업에 사용된 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="b9513-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="b9513-201">예를 들어 GET</span><span class="sxs-lookup"><span data-stu-id="b9513-201">For example, GET.</span></span> |
| <span data-ttu-id="b9513-202">Path</span><span class="sxs-lookup"><span data-stu-id="b9513-202">Path</span></span> |<span data-ttu-id="b9513-203">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-203">String</span></span> |<span data-ttu-id="b9513-204">작업이 수행된 경로</span><span class="sxs-lookup"><span data-stu-id="b9513-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="b9513-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="b9513-205">RequestContentLength</span></span> |<span data-ttu-id="b9513-206">int</span><span class="sxs-lookup"><span data-stu-id="b9513-206">int</span></span> |<span data-ttu-id="b9513-207">HTTP 요청의 콘텐츠 길이</span><span class="sxs-lookup"><span data-stu-id="b9513-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="b9513-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="b9513-208">ClientRequestId</span></span> |<span data-ttu-id="b9513-209">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-209">String</span></span> |<span data-ttu-id="b9513-210">이 요청을 고유하게 식별하는 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="b9513-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="b9513-211">StartTime</span></span> |<span data-ttu-id="b9513-212">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-212">String</span></span> |<span data-ttu-id="b9513-213">서버가 요청을 받은 시간</span><span class="sxs-lookup"><span data-stu-id="b9513-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="b9513-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="b9513-214">EndTime</span></span> |<span data-ttu-id="b9513-215">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-215">String</span></span> |<span data-ttu-id="b9513-216">서버가 응답을 전송한 시간</span><span class="sxs-lookup"><span data-stu-id="b9513-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="b9513-217">감사 로그</span><span class="sxs-lookup"><span data-stu-id="b9513-217">Audit logs</span></span>
<span data-ttu-id="b9513-218">다음은 JSON 형식인 감사 로그의 샘플 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="b9513-219">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="b9513-220">감사 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="b9513-220">Audit log schema</span></span>
| <span data-ttu-id="b9513-221">Name</span><span class="sxs-lookup"><span data-stu-id="b9513-221">Name</span></span> | <span data-ttu-id="b9513-222">형식</span><span class="sxs-lookup"><span data-stu-id="b9513-222">Type</span></span> | <span data-ttu-id="b9513-223">설명</span><span class="sxs-lookup"><span data-stu-id="b9513-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9513-224">실시간</span><span class="sxs-lookup"><span data-stu-id="b9513-224">time</span></span> |<span data-ttu-id="b9513-225">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-225">String</span></span> |<span data-ttu-id="b9513-226">로그의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="b9513-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="b9513-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="b9513-227">resourceId</span></span> |<span data-ttu-id="b9513-228">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-228">String</span></span> |<span data-ttu-id="b9513-229">작업이 수행되는 리소스의 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="b9513-230">카테고리</span><span class="sxs-lookup"><span data-stu-id="b9513-230">category</span></span> |<span data-ttu-id="b9513-231">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-231">String</span></span> |<span data-ttu-id="b9513-232">로그 범주</span><span class="sxs-lookup"><span data-stu-id="b9513-232">The log category.</span></span> <span data-ttu-id="b9513-233">예: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="b9513-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="b9513-234">operationName</span><span class="sxs-lookup"><span data-stu-id="b9513-234">operationName</span></span> |<span data-ttu-id="b9513-235">String</span><span class="sxs-lookup"><span data-stu-id="b9513-235">String</span></span> |<span data-ttu-id="b9513-236">기록된 작업의 이름</span><span class="sxs-lookup"><span data-stu-id="b9513-236">Name of the operation that is logged.</span></span> <span data-ttu-id="b9513-237">예를 들어 getfilestatus</span><span class="sxs-lookup"><span data-stu-id="b9513-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="b9513-238">resultType</span><span class="sxs-lookup"><span data-stu-id="b9513-238">resultType</span></span> |<span data-ttu-id="b9513-239">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-239">String</span></span> |<span data-ttu-id="b9513-240">작업의 상태, 예를 들어 200</span><span class="sxs-lookup"><span data-stu-id="b9513-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="b9513-241">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="b9513-241">correlationId</span></span> |<span data-ttu-id="b9513-242">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-242">String</span></span> |<span data-ttu-id="b9513-243">관련된 로그 항목의 집합을 그룹화하는 데 사용할 수 있는 로그의 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="b9513-244">ID</span><span class="sxs-lookup"><span data-stu-id="b9513-244">identity</span></span> |<span data-ttu-id="b9513-245">Object</span><span class="sxs-lookup"><span data-stu-id="b9513-245">Object</span></span> |<span data-ttu-id="b9513-246">로그를 생성하는 ID</span><span class="sxs-lookup"><span data-stu-id="b9513-246">The identity that generated the log</span></span> |
| <span data-ttu-id="b9513-247">properties</span><span class="sxs-lookup"><span data-stu-id="b9513-247">properties</span></span> |<span data-ttu-id="b9513-248">JSON</span><span class="sxs-lookup"><span data-stu-id="b9513-248">JSON</span></span> |<span data-ttu-id="b9513-249">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9513-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="b9513-250">감사 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="b9513-250">Audit log properties schema</span></span>
| <span data-ttu-id="b9513-251">Name</span><span class="sxs-lookup"><span data-stu-id="b9513-251">Name</span></span> | <span data-ttu-id="b9513-252">형식</span><span class="sxs-lookup"><span data-stu-id="b9513-252">Type</span></span> | <span data-ttu-id="b9513-253">설명</span><span class="sxs-lookup"><span data-stu-id="b9513-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9513-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="b9513-254">StreamName</span></span> |<span data-ttu-id="b9513-255">문자열</span><span class="sxs-lookup"><span data-stu-id="b9513-255">String</span></span> |<span data-ttu-id="b9513-256">작업이 수행된 경로</span><span class="sxs-lookup"><span data-stu-id="b9513-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="b9513-257">로그 데이터를 처리하는 샘플</span><span class="sxs-lookup"><span data-stu-id="b9513-257">Samples to process the log data</span></span>
<span data-ttu-id="b9513-258">Azure Data Lake Store에서는 로그 데이터를 처리하고 분석하는 방법에 대한 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="b9513-259">[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)에서 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9513-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="b9513-260">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b9513-260">See also</span></span>
* [<span data-ttu-id="b9513-261">Azure 데이터 레이크 저장소 개요</span><span class="sxs-lookup"><span data-stu-id="b9513-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="b9513-262">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="b9513-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

