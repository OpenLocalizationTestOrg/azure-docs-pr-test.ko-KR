---
title: "Azure 데이터 레이크 저장소에 대 한 진단 로그 aaaViewing | Microsoft Docs"
description: "이해 어떻게 Azure 데이터 레이크 저장소에 대 한 진단 로그 toosetup 및 액세스 "
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
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="8646c-103">Azure Data Lake Store에 대한 진단 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="8646c-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="8646c-104">데이터 레이크 저장소 계정과 tooview hello 기록 하는 방법에 대 한 진단 로깅 tooenable 계정에 대해 수집 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-104">Learn about how tooenable diagnostic logging for your Data Lake Store account and how tooview hello logs collected for your account.</span></span>

<span data-ttu-id="8646c-105">조직 계정 toocollect 데이터 액세스 감사 내역은 hello 데이터, hello 데이터를 액세스 하는 빈도, 데이터의 크기를 액세스 하는 사용자의 목록과 같은 정보를 제공 하는 hello에 저장 되는 Azure 데이터 레이크 저장소에 대 한 진단 로깅을 사용 하도록 설정할 수 있습니다. 계정, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account toocollect data access audit trails that provides information such as list of users accessing hello data, how frequently hello data is accessed, how much data is stored in hello account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8646c-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8646c-106">Prerequisites</span></span>
* <span data-ttu-id="8646c-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="8646c-107">**An Azure subscription**.</span></span> <span data-ttu-id="8646c-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8646c-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8646c-109">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="8646c-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="8646c-110">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-110">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="8646c-111">Data Lake Store 계정에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="8646c-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="8646c-112">새 toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-112">Sign on toohello new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8646c-113">Data Lake Store 계정을 열고 Data Lake Store 계정 블레이드에서 **설정**, **진단 로그**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="8646c-114">Hello에 **진단 로그** 블레이드에서 클릭 **진단을 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-114">In hello **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="8646c-115">![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "진단 로그 사용")</span><span class="sxs-lookup"><span data-stu-id="8646c-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="8646c-116">Hello에 **진단** 블레이드에서 다음 변경 내용을 tooconfigure 진단 로깅 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-116">In hello **Diagnostic** blade, make hello following changes tooconfigure diagnostic logging.</span></span>
   
    <span data-ttu-id="8646c-117">![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "진단 로그 사용")</span><span class="sxs-lookup"><span data-stu-id="8646c-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="8646c-118">설정 **상태** 너무**에** tooenable 진단 로깅.</span><span class="sxs-lookup"><span data-stu-id="8646c-118">Set **Status** too**On** tooenable diagnostic logging.</span></span>
   * <span data-ttu-id="8646c-119">다양 한 방식에서 toostore/프로세스 hello 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-119">You can choose toostore/process hello data in different ways.</span></span>
     
        * <span data-ttu-id="8646c-120">너무 hello 옵션을 선택**tooa 저장소 계정 보관** toostore tooan Azure 저장소 계정을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-120">Select hello option too**Archive tooa storage account** toostore logs tooan Azure Storage account.</span></span> <span data-ttu-id="8646c-121">Tooarchive hello 데이터 될 일괄 처리는 나중에이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-121">You use this option if you want tooarchive hello data that will be batch-processed at a later date.</span></span> <span data-ttu-id="8646c-122">이 옵션을 선택 하는 경우 toosave hello 로그를 Azure 저장소 계정을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-122">If you select this option you must provide an Azure Storage account toosave hello logs to.</span></span>
        
        * <span data-ttu-id="8646c-123">Hello 옵션을 너무 선택**스트림 tooan 이벤트 허브** toostream 로그 데이터 tooan Azure 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-123">Select hello option too**Stream tooan event hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="8646c-124">다운스트림 처리 하는 경우이 옵션을 사용 합니다 대개 tooanalyze 들어오는 실시간으로 로그, 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="8646c-124">Most likely you will use this option if you have a downstream processing pipeline tooanalyze incoming logs at real time.</span></span> <span data-ttu-id="8646c-125">이 옵션을 선택 하는 경우에 hello toouse를 원하는 Azure 이벤트 허브에 대 한 hello 세부 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-125">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

        * <span data-ttu-id="8646c-126">Hello 옵션을 너무 선택**tooLog 분석 보내기** toouse hello Azure 로그 분석 서비스 tooanalyze hello 생성 된 로그 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-126">Select hello option too**Send tooLog Analytics** toouse hello Azure Log Analytics service tooanalyze hello generated log data.</span></span> <span data-ttu-id="8646c-127">이 옵션을 선택 하는 경우 hello에 대 한 정보 hello Operations Management Suite 작업 영역을 사용 하 여 hello 로그 분석을 수행 합니다 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-127">If you select this option, you must provide hello details for hello Operations Management Suite workspace that you would use hello perform log analysis.</span></span>
     
   * <span data-ttu-id="8646c-128">Tooget 감사 로그 나 요청 로그 중 하나 또는 둘 다에 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-128">Specify whether you want tooget audit logs or request logs or both.</span></span>
   * <span data-ttu-id="8646c-129">Hello hello 데이터를 유지 해야 하는 일 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-129">Specify hello number of days for which hello data must be retained.</span></span> <span data-ttu-id="8646c-130">보존은 Azure 저장소 계정 tooarchive 로그 데이터를 사용 하는 경우에 적용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-130">Retention is only applicable if you are using Azure storage account tooarchive log data.</span></span>
   * <span data-ttu-id="8646c-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-131">Click **Save**.</span></span>

<span data-ttu-id="8646c-132">진단 설정을 사용 하도록 설정한 후 hello hello에 로그를 볼 수 있습니다 **진단 로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-132">Once you have enabled diagnostic settings, you can watch hello logs in hello **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="8646c-133">Data Lake Store 계정에 대한 진단 로그 보기</span><span class="sxs-lookup"><span data-stu-id="8646c-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="8646c-134">데이터 레이크 저장소 계정에 대 한 tooview hello 로그 데이터는 두 가지가.</span><span class="sxs-lookup"><span data-stu-id="8646c-134">There are two ways tooview hello log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="8646c-135">Hello Data Lake 저장소 계정에서 설정을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="8646c-135">From hello Data Lake Store account settings view</span></span>
* <span data-ttu-id="8646c-136">Hello 데이터가 저장 되는 hello Azure 저장소 계정에서</span><span class="sxs-lookup"><span data-stu-id="8646c-136">From hello Azure Storage account where hello data is stored</span></span>

### <a name="using-hello-data-lake-store-settings-view"></a><span data-ttu-id="8646c-137">Hello를 사용 하 여 데이터 레이크 저장소 설정 보기</span><span class="sxs-lookup"><span data-stu-id="8646c-137">Using hello Data Lake Store Settings view</span></span>
1. <span data-ttu-id="8646c-138">Data Lake Store 계정 **설정** 블레이드에서 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="8646c-139">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="8646c-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="8646c-140">Hello에 **진단 로그** 블레이드를 표시 되어야 hello 로그에 의해 분류 **감사 로그** 및 **요청 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-140">In hello **Diagnostic Logs** blade, you should see hello logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="8646c-141">요청 로그 hello Data Lake 저장소 계정에서 수행 된 모든 API 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-141">Request logs capture every API request made on hello Data Lake Store account.</span></span>
   * <span data-ttu-id="8646c-142">감사 로그는 유사한 toorequest 로그 되지만 더욱 세부적인된 분석 hello Data Lake 저장소 계정에서 수행 되는 hello 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-142">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations being performed on hello Data Lake Store account.</span></span> <span data-ttu-id="8646c-143">예를 들어 hello 감사 로그에서 "추가" 작업을 여러 개 요청 로그에서 단일 업로드 API 호출이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-143">For example, a single upload API call in request logs might result in multiple "Append" operations in hello audit logs.</span></span>
3. <span data-ttu-id="8646c-144">Hello 클릭 **다운로드** 링크 각각에 대해 항목 toodownload hello 로그를 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-144">Click hello **Download** link against each log entry toodownload hello logs.</span></span>

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="8646c-145">로그 데이터를 포함 하는 hello Azure 저장소 계정에서</span><span class="sxs-lookup"><span data-stu-id="8646c-145">From hello Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="8646c-146">로깅에 대 한 데이터 레이크 저장소와 관련 된 hello Azure 저장소 계정 블레이드 열고 Blob을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-146">Open hello Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="8646c-147">hello **Blob 서비스** 블레이드에 두 개의 컨테이너를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-147">hello **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="8646c-148">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="8646c-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="8646c-149">hello 컨테이너 **insights 로그 감사** hello 감사 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-149">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="8646c-150">hello 컨테이너 **insights 로그 요청이** hello 요청 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-150">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="8646c-151">이러한 컨테이너 내에서 hello 로그 hello 구조를 다음으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-151">Within these containers, hello logs are stored under hello following structure.</span></span>
   
    <span data-ttu-id="8646c-152">![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "진단 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="8646c-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="8646c-153">예를 들어 hello 전체 경로 tooan 감사 로그 수 있습니다.`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="8646c-153">As an example, hello complete path tooan audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="8646c-154">마찬가지로, hello 전체 경로 tooa 요청 로그 수 있습니다.`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="8646c-154">Similary, hello complete path tooa request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-hello-structure-of-hello-log-data"></a><span data-ttu-id="8646c-155">Hello 로그 데이터의 hello 구조 이해</span><span class="sxs-lookup"><span data-stu-id="8646c-155">Understand hello structure of hello log data</span></span>
<span data-ttu-id="8646c-156">hello 감사 및 요청 로그는 JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-156">hello audit and request logs are in a JSON format.</span></span> <span data-ttu-id="8646c-157">이 섹션에서는 요청에 대 한 JSON의 hello 구조를 확인 하 고 감사 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-157">In this section, we look at hello structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="8646c-158">요청 로그</span><span class="sxs-lookup"><span data-stu-id="8646c-158">Request logs</span></span>
<span data-ttu-id="8646c-159">Hello JSON 형식의 요청 로그에서 샘플 항목 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-159">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="8646c-160">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="8646c-161">요청 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="8646c-161">Request log schema</span></span>
| <span data-ttu-id="8646c-162">Name</span><span class="sxs-lookup"><span data-stu-id="8646c-162">Name</span></span> | <span data-ttu-id="8646c-163">형식</span><span class="sxs-lookup"><span data-stu-id="8646c-163">Type</span></span> | <span data-ttu-id="8646c-164">설명</span><span class="sxs-lookup"><span data-stu-id="8646c-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8646c-165">실시간</span><span class="sxs-lookup"><span data-stu-id="8646c-165">time</span></span> |<span data-ttu-id="8646c-166">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-166">String</span></span> |<span data-ttu-id="8646c-167">hello 타임 스탬프 (UTC) hello 로그</span><span class="sxs-lookup"><span data-stu-id="8646c-167">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="8646c-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="8646c-168">resourceId</span></span> |<span data-ttu-id="8646c-169">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-169">String</span></span> |<span data-ttu-id="8646c-170">에 배치 되는 작업에 걸린 hello 리소스의 hello ID</span><span class="sxs-lookup"><span data-stu-id="8646c-170">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="8646c-171">카테고리</span><span class="sxs-lookup"><span data-stu-id="8646c-171">category</span></span> |<span data-ttu-id="8646c-172">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-172">String</span></span> |<span data-ttu-id="8646c-173">hello 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-173">hello log category.</span></span> <span data-ttu-id="8646c-174">예: **Requests**</span><span class="sxs-lookup"><span data-stu-id="8646c-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="8646c-175">operationName</span><span class="sxs-lookup"><span data-stu-id="8646c-175">operationName</span></span> |<span data-ttu-id="8646c-176">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-176">String</span></span> |<span data-ttu-id="8646c-177">기록 된 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-177">Name of hello operation that is logged.</span></span> <span data-ttu-id="8646c-178">예를 들어 getfilestatus</span><span class="sxs-lookup"><span data-stu-id="8646c-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="8646c-179">resultType</span><span class="sxs-lookup"><span data-stu-id="8646c-179">resultType</span></span> |<span data-ttu-id="8646c-180">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-180">String</span></span> |<span data-ttu-id="8646c-181">예를 들어 200 hello 연산의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-181">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="8646c-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="8646c-182">callerIpAddress</span></span> |<span data-ttu-id="8646c-183">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-183">String</span></span> |<span data-ttu-id="8646c-184">hello 요청을 만드는 hello 클라이언트의 hello IP 주소</span><span class="sxs-lookup"><span data-stu-id="8646c-184">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="8646c-185">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="8646c-185">correlationId</span></span> |<span data-ttu-id="8646c-186">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-186">String</span></span> |<span data-ttu-id="8646c-187">hello 로그 수 함께 사용 되는 toogroup는 관련된 로그 항목 집합의 hello id</span><span class="sxs-lookup"><span data-stu-id="8646c-187">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="8646c-188">ID</span><span class="sxs-lookup"><span data-stu-id="8646c-188">identity</span></span> |<span data-ttu-id="8646c-189">Object</span><span class="sxs-lookup"><span data-stu-id="8646c-189">Object</span></span> |<span data-ttu-id="8646c-190">hello 로그를 생성 하는 hello id</span><span class="sxs-lookup"><span data-stu-id="8646c-190">hello identity that generated hello log</span></span> |
| <span data-ttu-id="8646c-191">properties</span><span class="sxs-lookup"><span data-stu-id="8646c-191">properties</span></span> |<span data-ttu-id="8646c-192">JSON</span><span class="sxs-lookup"><span data-stu-id="8646c-192">JSON</span></span> |<span data-ttu-id="8646c-193">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8646c-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="8646c-194">요청 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="8646c-194">Request log properties schema</span></span>
| <span data-ttu-id="8646c-195">Name</span><span class="sxs-lookup"><span data-stu-id="8646c-195">Name</span></span> | <span data-ttu-id="8646c-196">형식</span><span class="sxs-lookup"><span data-stu-id="8646c-196">Type</span></span> | <span data-ttu-id="8646c-197">설명</span><span class="sxs-lookup"><span data-stu-id="8646c-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8646c-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="8646c-198">HttpMethod</span></span> |<span data-ttu-id="8646c-199">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-199">String</span></span> |<span data-ttu-id="8646c-200">hello HTTP 메서드가 사용 hello 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-200">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="8646c-201">예를 들어 GET</span><span class="sxs-lookup"><span data-stu-id="8646c-201">For example, GET.</span></span> |
| <span data-ttu-id="8646c-202">Path</span><span class="sxs-lookup"><span data-stu-id="8646c-202">Path</span></span> |<span data-ttu-id="8646c-203">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-203">String</span></span> |<span data-ttu-id="8646c-204">hello 경로 hello 작업에 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-204">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="8646c-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="8646c-205">RequestContentLength</span></span> |<span data-ttu-id="8646c-206">int</span><span class="sxs-lookup"><span data-stu-id="8646c-206">int</span></span> |<span data-ttu-id="8646c-207">hello hello HTTP 요청의 콘텐츠 길이</span><span class="sxs-lookup"><span data-stu-id="8646c-207">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="8646c-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="8646c-208">ClientRequestId</span></span> |<span data-ttu-id="8646c-209">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-209">String</span></span> |<span data-ttu-id="8646c-210">이 요청을 고유 하 게 식별 하는 Id hello</span><span class="sxs-lookup"><span data-stu-id="8646c-210">hello Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="8646c-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="8646c-211">StartTime</span></span> |<span data-ttu-id="8646c-212">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-212">String</span></span> |<span data-ttu-id="8646c-213">hello는 hello 받은 서버 hello 요청 시간</span><span class="sxs-lookup"><span data-stu-id="8646c-213">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="8646c-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="8646c-214">EndTime</span></span> |<span data-ttu-id="8646c-215">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-215">String</span></span> |<span data-ttu-id="8646c-216">hello 시간은 hello 서버 응답 전송</span><span class="sxs-lookup"><span data-stu-id="8646c-216">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="8646c-217">감사 로그</span><span class="sxs-lookup"><span data-stu-id="8646c-217">Audit logs</span></span>
<span data-ttu-id="8646c-218">Hello JSON 형식 감사 로그에 샘플 항목 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-218">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="8646c-219">각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="8646c-220">감사 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="8646c-220">Audit log schema</span></span>
| <span data-ttu-id="8646c-221">Name</span><span class="sxs-lookup"><span data-stu-id="8646c-221">Name</span></span> | <span data-ttu-id="8646c-222">형식</span><span class="sxs-lookup"><span data-stu-id="8646c-222">Type</span></span> | <span data-ttu-id="8646c-223">설명</span><span class="sxs-lookup"><span data-stu-id="8646c-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8646c-224">실시간</span><span class="sxs-lookup"><span data-stu-id="8646c-224">time</span></span> |<span data-ttu-id="8646c-225">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-225">String</span></span> |<span data-ttu-id="8646c-226">hello 타임 스탬프 (UTC) hello 로그</span><span class="sxs-lookup"><span data-stu-id="8646c-226">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="8646c-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="8646c-227">resourceId</span></span> |<span data-ttu-id="8646c-228">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-228">String</span></span> |<span data-ttu-id="8646c-229">에 배치 되는 작업에 걸린 hello 리소스의 hello ID</span><span class="sxs-lookup"><span data-stu-id="8646c-229">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="8646c-230">카테고리</span><span class="sxs-lookup"><span data-stu-id="8646c-230">category</span></span> |<span data-ttu-id="8646c-231">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-231">String</span></span> |<span data-ttu-id="8646c-232">hello 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-232">hello log category.</span></span> <span data-ttu-id="8646c-233">예: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="8646c-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="8646c-234">operationName</span><span class="sxs-lookup"><span data-stu-id="8646c-234">operationName</span></span> |<span data-ttu-id="8646c-235">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-235">String</span></span> |<span data-ttu-id="8646c-236">기록 된 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-236">Name of hello operation that is logged.</span></span> <span data-ttu-id="8646c-237">예를 들어 getfilestatus</span><span class="sxs-lookup"><span data-stu-id="8646c-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="8646c-238">resultType</span><span class="sxs-lookup"><span data-stu-id="8646c-238">resultType</span></span> |<span data-ttu-id="8646c-239">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-239">String</span></span> |<span data-ttu-id="8646c-240">예를 들어 200 hello 연산의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-240">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="8646c-241">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="8646c-241">correlationId</span></span> |<span data-ttu-id="8646c-242">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-242">String</span></span> |<span data-ttu-id="8646c-243">hello 로그 수 함께 사용 되는 toogroup는 관련된 로그 항목 집합의 hello id</span><span class="sxs-lookup"><span data-stu-id="8646c-243">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="8646c-244">ID</span><span class="sxs-lookup"><span data-stu-id="8646c-244">identity</span></span> |<span data-ttu-id="8646c-245">Object</span><span class="sxs-lookup"><span data-stu-id="8646c-245">Object</span></span> |<span data-ttu-id="8646c-246">hello 로그를 생성 하는 hello id</span><span class="sxs-lookup"><span data-stu-id="8646c-246">hello identity that generated hello log</span></span> |
| <span data-ttu-id="8646c-247">properties</span><span class="sxs-lookup"><span data-stu-id="8646c-247">properties</span></span> |<span data-ttu-id="8646c-248">JSON</span><span class="sxs-lookup"><span data-stu-id="8646c-248">JSON</span></span> |<span data-ttu-id="8646c-249">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8646c-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="8646c-250">감사 로그 속성 스키마</span><span class="sxs-lookup"><span data-stu-id="8646c-250">Audit log properties schema</span></span>
| <span data-ttu-id="8646c-251">Name</span><span class="sxs-lookup"><span data-stu-id="8646c-251">Name</span></span> | <span data-ttu-id="8646c-252">형식</span><span class="sxs-lookup"><span data-stu-id="8646c-252">Type</span></span> | <span data-ttu-id="8646c-253">설명</span><span class="sxs-lookup"><span data-stu-id="8646c-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8646c-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="8646c-254">StreamName</span></span> |<span data-ttu-id="8646c-255">문자열</span><span class="sxs-lookup"><span data-stu-id="8646c-255">String</span></span> |<span data-ttu-id="8646c-256">hello 경로 hello 작업에 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-256">hello path hello operation was performed on</span></span> |

## <a name="samples-tooprocess-hello-log-data"></a><span data-ttu-id="8646c-257">샘플 tooprocess hello 로그 데이터</span><span class="sxs-lookup"><span data-stu-id="8646c-257">Samples tooprocess hello log data</span></span>
<span data-ttu-id="8646c-258">Azure 데이터 레이크 저장소 방법에 대 한 샘플을 제공 tooprocess hello 로그 데이터를 분석 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-258">Azure Data Lake Store provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="8646c-259">Hello에 있는 샘플을 찾을 수 있습니다 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)합니다.</span><span class="sxs-lookup"><span data-stu-id="8646c-259">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="8646c-260">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8646c-260">See also</span></span>
* [<span data-ttu-id="8646c-261">Azure 데이터 레이크 저장소 개요</span><span class="sxs-lookup"><span data-stu-id="8646c-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="8646c-262">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="8646c-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

