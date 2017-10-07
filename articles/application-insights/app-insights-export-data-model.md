---
title: "응용 프로그램 Insights 데이터 모델 aaaAzure | Microsoft Docs"
description: "JSON의 연속 내보내기에서 내보내고 필터로 사용하는 속성을 설명합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="8364e-103">Application Insights 데이터 모델 내보내기</span><span class="sxs-lookup"><span data-stu-id="8364e-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="8364e-104">이 표에 hello에서 전송 하는 원격 분석의 hello 속성 [Application Insights](app-insights-overview.md) Sdk toohello 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-104">This table lists hello properties of telemetry sent from hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span></span>
<span data-ttu-id="8364e-105">이러한 속성이 [연속 내보내기](app-insights-export-telemetry.md)에서 데이터 출력에 표시됩니다</span><span class="sxs-lookup"><span data-stu-id="8364e-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="8364e-106">또한 [메트릭 탐색기](app-insights-metrics-explorer.md) 및 [진단 검색](app-insights-diagnostic-search.md)의 속성 필터에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8364e-107">포인트 toonote:</span><span class="sxs-lookup"><span data-stu-id="8364e-107">Points toonote:</span></span>

* <span data-ttu-id="8364e-108">`[0]`이 표에 있는 tooinsert 인덱스; hello 경로 지정을 나타냅니다. 하지만 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-108">`[0]` in these tables denotes a point in hello path where you have tooinsert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="8364e-109">기간의 단위는 10분의 1 마이크로초이므로 10000000은 1초입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="8364e-110">날짜 및 시간이 UTC 이며 hello ISO 형식으로 지정 됩니다.`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="8364e-110">Dates and times are UTC, and are given in hello ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="8364e-111">예제</span><span class="sxs-lookup"><span data-stu-id="8364e-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="8364e-112">}</span><span class="sxs-lookup"><span data-stu-id="8364e-112">}</span></span>

## <a name="context"></a><span data-ttu-id="8364e-113">Context</span><span class="sxs-lookup"><span data-stu-id="8364e-113">Context</span></span>
<span data-ttu-id="8364e-114">모든 유형의 원격 분석에는 컨텍스트 섹션이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="8364e-115">이러한 모든 필드가 모든 데이터 요소와 함께 전송되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="8364e-116">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-116">Path</span></span> | <span data-ttu-id="8364e-117">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-117">Type</span></span> | <span data-ttu-id="8364e-118">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="8364e-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="8364e-120">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8364e-120">object [ ]</span></span> |<span data-ttu-id="8364e-121">사용자 지정 속성 매개 변수에 의해 설정되는 키-값 문자열 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="8364e-122">키 최대 길이가 100이고, 값 최대 길이가 1024입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="8364e-123">100 개 이상의 고유 값 hello 속성 검색할 수 있지만 분할에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-123">More than 100 unique values, hello property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="8364e-124">ikey당 최대 키는 200개입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="8364e-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="8364e-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="8364e-126">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8364e-126">object [ ]</span></span> |<span data-ttu-id="8364e-127">사용자 지정 측정 매개 변수 및 TrackMetrics에 의해 설정된 키-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="8364e-128">키 최대 길이가 100이고, 값은 숫자가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="8364e-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="8364e-129">context.data.eventTime</span></span> |<span data-ttu-id="8364e-130">string</span><span class="sxs-lookup"><span data-stu-id="8364e-130">string</span></span> |<span data-ttu-id="8364e-131">UTC</span><span class="sxs-lookup"><span data-stu-id="8364e-131">UTC</span></span> |
| <span data-ttu-id="8364e-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="8364e-132">context.data.isSynthetic</span></span> |<span data-ttu-id="8364e-133">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-133">boolean</span></span> |<span data-ttu-id="8364e-134">요청 된 봇 또는 웹 테스트에서 toocome 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-134">Request appears toocome from a bot or web test.</span></span> |
| <span data-ttu-id="8364e-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="8364e-135">context.data.samplingRate</span></span> |<span data-ttu-id="8364e-136">number</span><span class="sxs-lookup"><span data-stu-id="8364e-136">number</span></span> |<span data-ttu-id="8364e-137">Hello tooportal 보내집니다 SDK에 의해 생성 된 원격 분석의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-137">Percentage of telemetry generated by hello SDK that is sent tooportal.</span></span> <span data-ttu-id="8364e-138">범위는 0.0-100.0입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="8364e-139">context.device</span><span class="sxs-lookup"><span data-stu-id="8364e-139">context.device</span></span> |<span data-ttu-id="8364e-140">object</span><span class="sxs-lookup"><span data-stu-id="8364e-140">object</span></span> |<span data-ttu-id="8364e-141">클라이언트 장치</span><span class="sxs-lookup"><span data-stu-id="8364e-141">Client device</span></span> |
| <span data-ttu-id="8364e-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="8364e-142">context.device.browser</span></span> |<span data-ttu-id="8364e-143">string</span><span class="sxs-lookup"><span data-stu-id="8364e-143">string</span></span> |<span data-ttu-id="8364e-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="8364e-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="8364e-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="8364e-145">context.device.browserVersion</span></span> |<span data-ttu-id="8364e-146">string</span><span class="sxs-lookup"><span data-stu-id="8364e-146">string</span></span> |<span data-ttu-id="8364e-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="8364e-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="8364e-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="8364e-148">context.device.deviceModel</span></span> |<span data-ttu-id="8364e-149">string</span><span class="sxs-lookup"><span data-stu-id="8364e-149">string</span></span> | |
| <span data-ttu-id="8364e-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="8364e-150">context.device.deviceName</span></span> |<span data-ttu-id="8364e-151">string</span><span class="sxs-lookup"><span data-stu-id="8364e-151">string</span></span> | |
| <span data-ttu-id="8364e-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="8364e-152">context.device.id</span></span> |<span data-ttu-id="8364e-153">string</span><span class="sxs-lookup"><span data-stu-id="8364e-153">string</span></span> | |
| <span data-ttu-id="8364e-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="8364e-154">context.device.locale</span></span> |<span data-ttu-id="8364e-155">string</span><span class="sxs-lookup"><span data-stu-id="8364e-155">string</span></span> |<span data-ttu-id="8364e-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="8364e-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="8364e-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="8364e-157">context.device.network</span></span> |<span data-ttu-id="8364e-158">string</span><span class="sxs-lookup"><span data-stu-id="8364e-158">string</span></span> | |
| <span data-ttu-id="8364e-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="8364e-159">context.device.oemName</span></span> |<span data-ttu-id="8364e-160">string</span><span class="sxs-lookup"><span data-stu-id="8364e-160">string</span></span> | |
| <span data-ttu-id="8364e-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="8364e-161">context.device.osVersion</span></span> |<span data-ttu-id="8364e-162">string</span><span class="sxs-lookup"><span data-stu-id="8364e-162">string</span></span> |<span data-ttu-id="8364e-163">호스트 OS</span><span class="sxs-lookup"><span data-stu-id="8364e-163">Host OS</span></span> |
| <span data-ttu-id="8364e-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="8364e-164">context.device.roleInstance</span></span> |<span data-ttu-id="8364e-165">string</span><span class="sxs-lookup"><span data-stu-id="8364e-165">string</span></span> |<span data-ttu-id="8364e-166">서버 호스트의 ID</span><span class="sxs-lookup"><span data-stu-id="8364e-166">ID of server host</span></span> |
| <span data-ttu-id="8364e-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="8364e-167">context.device.roleName</span></span> |<span data-ttu-id="8364e-168">string</span><span class="sxs-lookup"><span data-stu-id="8364e-168">string</span></span> | |
| <span data-ttu-id="8364e-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="8364e-169">context.device.type</span></span> |<span data-ttu-id="8364e-170">string</span><span class="sxs-lookup"><span data-stu-id="8364e-170">string</span></span> |<span data-ttu-id="8364e-171">PC, 브라우저...</span><span class="sxs-lookup"><span data-stu-id="8364e-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="8364e-172">context.location</span><span class="sxs-lookup"><span data-stu-id="8364e-172">context.location</span></span> |<span data-ttu-id="8364e-173">object</span><span class="sxs-lookup"><span data-stu-id="8364e-173">object</span></span> |<span data-ttu-id="8364e-174">clientip에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-174">Derived from clientip.</span></span> |
| <span data-ttu-id="8364e-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="8364e-175">context.location.city</span></span> |<span data-ttu-id="8364e-176">string</span><span class="sxs-lookup"><span data-stu-id="8364e-176">string</span></span> |<span data-ttu-id="8364e-177">알 수 있는 경우 clientip에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="8364e-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="8364e-178">context.location.clientip</span></span> |<span data-ttu-id="8364e-179">string</span><span class="sxs-lookup"><span data-stu-id="8364e-179">string</span></span> |<span data-ttu-id="8364e-180">마지막 팔각형 익명화 된 too0입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-180">Last octagon is anonymized too0.</span></span> |
| <span data-ttu-id="8364e-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="8364e-181">context.location.continent</span></span> |<span data-ttu-id="8364e-182">string</span><span class="sxs-lookup"><span data-stu-id="8364e-182">string</span></span> | |
| <span data-ttu-id="8364e-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="8364e-183">context.location.country</span></span> |<span data-ttu-id="8364e-184">string</span><span class="sxs-lookup"><span data-stu-id="8364e-184">string</span></span> | |
| <span data-ttu-id="8364e-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="8364e-185">context.location.province</span></span> |<span data-ttu-id="8364e-186">string</span><span class="sxs-lookup"><span data-stu-id="8364e-186">string</span></span> |<span data-ttu-id="8364e-187">시/도</span><span class="sxs-lookup"><span data-stu-id="8364e-187">State or province</span></span> |
| <span data-ttu-id="8364e-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="8364e-188">context.operation.id</span></span> |<span data-ttu-id="8364e-189">string</span><span class="sxs-lookup"><span data-stu-id="8364e-189">string</span></span> |<span data-ttu-id="8364e-190">항목 hello hello 포털에서 동일한 작업 id 관련 항목으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-190">Items that have hello same operation id are shown as Related Items in hello portal.</span></span> <span data-ttu-id="8364e-191">일반적으로 hello 요청 id입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-191">Usually hello request id.</span></span> |
| <span data-ttu-id="8364e-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="8364e-192">context.operation.name</span></span> |<span data-ttu-id="8364e-193">string</span><span class="sxs-lookup"><span data-stu-id="8364e-193">string</span></span> |<span data-ttu-id="8364e-194">URL 또는 요청 이름</span><span class="sxs-lookup"><span data-stu-id="8364e-194">url or request name</span></span> |
| <span data-ttu-id="8364e-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="8364e-195">context.operation.parentId</span></span> |<span data-ttu-id="8364e-196">string</span><span class="sxs-lookup"><span data-stu-id="8364e-196">string</span></span> |<span data-ttu-id="8364e-197">중첩된 관련 항목을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-197">Allows nested related items.</span></span> |
| <span data-ttu-id="8364e-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="8364e-198">context.session.id</span></span> |<span data-ttu-id="8364e-199">string</span><span class="sxs-lookup"><span data-stu-id="8364e-199">string</span></span> |<span data-ttu-id="8364e-200">Hello에서 작업 그룹의 id 동일한 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-200">Id of a group of operations from hello same source.</span></span> <span data-ttu-id="8364e-201">작업 없이 30 분 동안 신호를 세션의 hello 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-201">A period of 30 minutes without an operation signals hello end of a session.</span></span> |
| <span data-ttu-id="8364e-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="8364e-202">context.session.isFirst</span></span> |<span data-ttu-id="8364e-203">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-203">boolean</span></span> | |
| <span data-ttu-id="8364e-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8364e-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="8364e-205">string</span><span class="sxs-lookup"><span data-stu-id="8364e-205">string</span></span> | |
| <span data-ttu-id="8364e-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8364e-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="8364e-207">string</span><span class="sxs-lookup"><span data-stu-id="8364e-207">string</span></span> | |
| <span data-ttu-id="8364e-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="8364e-208">context.user.anonId</span></span> |<span data-ttu-id="8364e-209">string</span><span class="sxs-lookup"><span data-stu-id="8364e-209">string</span></span> | |
| <span data-ttu-id="8364e-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8364e-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="8364e-211">string</span><span class="sxs-lookup"><span data-stu-id="8364e-211">string</span></span> |[<span data-ttu-id="8364e-212">인증된 사용자</span><span class="sxs-lookup"><span data-stu-id="8364e-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="8364e-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="8364e-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="8364e-214">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-214">boolean</span></span> | |
| <span data-ttu-id="8364e-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="8364e-215">internal.data.documentVersion</span></span> |<span data-ttu-id="8364e-216">string</span><span class="sxs-lookup"><span data-stu-id="8364e-216">string</span></span> | |
| <span data-ttu-id="8364e-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="8364e-217">internal.data.id</span></span> |<span data-ttu-id="8364e-218">string</span><span class="sxs-lookup"><span data-stu-id="8364e-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="8364e-219">이벤트</span><span class="sxs-lookup"><span data-stu-id="8364e-219">Events</span></span>
<span data-ttu-id="8364e-220">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)에 의해 생성된 사용자 지정 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="8364e-221">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-221">Path</span></span> | <span data-ttu-id="8364e-222">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-222">Type</span></span> | <span data-ttu-id="8364e-223">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-224">event [0] count</span></span> |<span data-ttu-id="8364e-225">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-225">integer</span></span> |<span data-ttu-id="8364e-226">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-227">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="8364e-228">event [0] name</span></span> |<span data-ttu-id="8364e-229">string</span><span class="sxs-lookup"><span data-stu-id="8364e-229">string</span></span> |<span data-ttu-id="8364e-230">이벤트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-230">Event name.</span></span>  <span data-ttu-id="8364e-231">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="8364e-231">Max length 250.</span></span> |
| <span data-ttu-id="8364e-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="8364e-232">event [0] url</span></span> |<span data-ttu-id="8364e-233">string</span><span class="sxs-lookup"><span data-stu-id="8364e-233">string</span></span> | |
| <span data-ttu-id="8364e-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8364e-234">event [0] urlData.base</span></span> |<span data-ttu-id="8364e-235">string</span><span class="sxs-lookup"><span data-stu-id="8364e-235">string</span></span> | |
| <span data-ttu-id="8364e-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8364e-236">event [0] urlData.host</span></span> |<span data-ttu-id="8364e-237">string</span><span class="sxs-lookup"><span data-stu-id="8364e-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="8364e-238">예외</span><span class="sxs-lookup"><span data-stu-id="8364e-238">Exceptions</span></span>
<span data-ttu-id="8364e-239">보고서 [예외](app-insights-asp-net-exceptions.md) hello 서버 및 hello 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in hello server and in hello browser.</span></span>

| <span data-ttu-id="8364e-240">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-240">Path</span></span> | <span data-ttu-id="8364e-241">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-241">Type</span></span> | <span data-ttu-id="8364e-242">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8364e-243">basicException [0] assembly</span></span> |<span data-ttu-id="8364e-244">string</span><span class="sxs-lookup"><span data-stu-id="8364e-244">string</span></span> | |
| <span data-ttu-id="8364e-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-245">basicException [0] count</span></span> |<span data-ttu-id="8364e-246">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-246">integer</span></span> |<span data-ttu-id="8364e-247">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-248">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="8364e-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="8364e-250">string</span><span class="sxs-lookup"><span data-stu-id="8364e-250">string</span></span> | |
| <span data-ttu-id="8364e-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="8364e-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="8364e-252">string</span><span class="sxs-lookup"><span data-stu-id="8364e-252">string</span></span> | |
| <span data-ttu-id="8364e-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="8364e-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="8364e-254">string</span><span class="sxs-lookup"><span data-stu-id="8364e-254">string</span></span> | |
| <span data-ttu-id="8364e-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="8364e-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="8364e-256">string</span><span class="sxs-lookup"><span data-stu-id="8364e-256">string</span></span> | |
| <span data-ttu-id="8364e-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="8364e-257">basicException [0] handledAt</span></span> |<span data-ttu-id="8364e-258">string</span><span class="sxs-lookup"><span data-stu-id="8364e-258">string</span></span> | |
| <span data-ttu-id="8364e-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="8364e-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="8364e-260">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-260">boolean</span></span> | |
| <span data-ttu-id="8364e-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="8364e-261">basicException [0] id</span></span> |<span data-ttu-id="8364e-262">string</span><span class="sxs-lookup"><span data-stu-id="8364e-262">string</span></span> | |
| <span data-ttu-id="8364e-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="8364e-263">basicException [0] method</span></span> |<span data-ttu-id="8364e-264">string</span><span class="sxs-lookup"><span data-stu-id="8364e-264">string</span></span> | |
| <span data-ttu-id="8364e-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="8364e-265">basicException [0] message</span></span> |<span data-ttu-id="8364e-266">string</span><span class="sxs-lookup"><span data-stu-id="8364e-266">string</span></span> |<span data-ttu-id="8364e-267">예외 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-267">Exception message.</span></span> <span data-ttu-id="8364e-268">최대 길이 10000</span><span class="sxs-lookup"><span data-stu-id="8364e-268">Max length 10k.</span></span> |
| <span data-ttu-id="8364e-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="8364e-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="8364e-270">string</span><span class="sxs-lookup"><span data-stu-id="8364e-270">string</span></span> | |
| <span data-ttu-id="8364e-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="8364e-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="8364e-272">string</span><span class="sxs-lookup"><span data-stu-id="8364e-272">string</span></span> | |
| <span data-ttu-id="8364e-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="8364e-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="8364e-274">string</span><span class="sxs-lookup"><span data-stu-id="8364e-274">string</span></span> | |
| <span data-ttu-id="8364e-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="8364e-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="8364e-276">string</span><span class="sxs-lookup"><span data-stu-id="8364e-276">string</span></span> | |
| <span data-ttu-id="8364e-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="8364e-277">basicException [0] outerId</span></span> |<span data-ttu-id="8364e-278">string</span><span class="sxs-lookup"><span data-stu-id="8364e-278">string</span></span> | |
| <span data-ttu-id="8364e-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8364e-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="8364e-280">string</span><span class="sxs-lookup"><span data-stu-id="8364e-280">string</span></span> | |
| <span data-ttu-id="8364e-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="8364e-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="8364e-282">string</span><span class="sxs-lookup"><span data-stu-id="8364e-282">string</span></span> | |
| <span data-ttu-id="8364e-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="8364e-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="8364e-284">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-284">integer</span></span> | |
| <span data-ttu-id="8364e-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="8364e-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="8364e-286">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-286">integer</span></span> | |
| <span data-ttu-id="8364e-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="8364e-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="8364e-288">string</span><span class="sxs-lookup"><span data-stu-id="8364e-288">string</span></span> | |
| <span data-ttu-id="8364e-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="8364e-289">basicException [0] stack</span></span> |<span data-ttu-id="8364e-290">string</span><span class="sxs-lookup"><span data-stu-id="8364e-290">string</span></span> |<span data-ttu-id="8364e-291">최대 길이 10000</span><span class="sxs-lookup"><span data-stu-id="8364e-291">Max length 10k</span></span> |
| <span data-ttu-id="8364e-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="8364e-292">basicException [0] typeName</span></span> |<span data-ttu-id="8364e-293">string</span><span class="sxs-lookup"><span data-stu-id="8364e-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="8364e-294">추적 메시지</span><span class="sxs-lookup"><span data-stu-id="8364e-294">Trace Messages</span></span>
<span data-ttu-id="8364e-295">보낸 [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), hello 여 [로깅 어댑터](app-insights-asp-net-trace-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by hello [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="8364e-296">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-296">Path</span></span> | <span data-ttu-id="8364e-297">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-297">Type</span></span> | <span data-ttu-id="8364e-298">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="8364e-299">message [0] loggerName</span></span> |<span data-ttu-id="8364e-300">string</span><span class="sxs-lookup"><span data-stu-id="8364e-300">string</span></span> | |
| <span data-ttu-id="8364e-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="8364e-301">message [0] parameters</span></span> |<span data-ttu-id="8364e-302">string</span><span class="sxs-lookup"><span data-stu-id="8364e-302">string</span></span> | |
| <span data-ttu-id="8364e-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="8364e-303">message [0] raw</span></span> |<span data-ttu-id="8364e-304">string</span><span class="sxs-lookup"><span data-stu-id="8364e-304">string</span></span> |<span data-ttu-id="8364e-305">최대 길이가 10 k hello 로그 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-305">hello log message, max length 10k.</span></span> |
| <span data-ttu-id="8364e-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="8364e-306">message [0] severityLevel</span></span> |<span data-ttu-id="8364e-307">string</span><span class="sxs-lookup"><span data-stu-id="8364e-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="8364e-308">원격 종속성</span><span class="sxs-lookup"><span data-stu-id="8364e-308">Remote dependency</span></span>
<span data-ttu-id="8364e-309">TrackDependency에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-309">Sent by TrackDependency.</span></span> <span data-ttu-id="8364e-310">Tooreport 성능 및 사용 현황의 사용 [toodependencies 호출](app-insights-asp-net-dependencies.md) hello 서버 및 hello 브라우저에서 AJAX 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-310">Used tooreport performance and usage of [calls toodependencies](app-insights-asp-net-dependencies.md) in hello server, and AJAX calls in hello browser.</span></span>

| <span data-ttu-id="8364e-311">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-311">Path</span></span> | <span data-ttu-id="8364e-312">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-312">Type</span></span> | <span data-ttu-id="8364e-313">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="8364e-314">remoteDependency [0] async</span></span> |<span data-ttu-id="8364e-315">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-315">boolean</span></span> | |
| <span data-ttu-id="8364e-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="8364e-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="8364e-317">string</span><span class="sxs-lookup"><span data-stu-id="8364e-317">string</span></span> | |
| <span data-ttu-id="8364e-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="8364e-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="8364e-319">string</span><span class="sxs-lookup"><span data-stu-id="8364e-319">string</span></span> |<span data-ttu-id="8364e-320">예를 들어 "홈/인덱스"</span><span class="sxs-lookup"><span data-stu-id="8364e-320">For example "home/index"</span></span> |
| <span data-ttu-id="8364e-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-321">remoteDependency [0] count</span></span> |<span data-ttu-id="8364e-322">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-322">integer</span></span> |<span data-ttu-id="8364e-323">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-324">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="8364e-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="8364e-326">string</span><span class="sxs-lookup"><span data-stu-id="8364e-326">string</span></span> |<span data-ttu-id="8364e-327">HTTP, SQL, ...</span><span class="sxs-lookup"><span data-stu-id="8364e-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="8364e-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="8364e-329">number</span><span class="sxs-lookup"><span data-stu-id="8364e-329">number</span></span> |<span data-ttu-id="8364e-330">종속성에 의해 응답의 호출 toocompletion에서 시간</span><span class="sxs-lookup"><span data-stu-id="8364e-330">Time from call toocompletion of response by dependency</span></span> |
| <span data-ttu-id="8364e-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="8364e-331">remoteDependency [0] id</span></span> |<span data-ttu-id="8364e-332">string</span><span class="sxs-lookup"><span data-stu-id="8364e-332">string</span></span> | |
| <span data-ttu-id="8364e-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="8364e-333">remoteDependency [0] name</span></span> |<span data-ttu-id="8364e-334">string</span><span class="sxs-lookup"><span data-stu-id="8364e-334">string</span></span> |<span data-ttu-id="8364e-335">Url.</span><span class="sxs-lookup"><span data-stu-id="8364e-335">Url.</span></span> <span data-ttu-id="8364e-336">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="8364e-336">Max length 250.</span></span> |
| <span data-ttu-id="8364e-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="8364e-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="8364e-338">string</span><span class="sxs-lookup"><span data-stu-id="8364e-338">string</span></span> |<span data-ttu-id="8364e-339">HTTP 종속성에서</span><span class="sxs-lookup"><span data-stu-id="8364e-339">from HTTP dependency</span></span> |
| <span data-ttu-id="8364e-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="8364e-340">remoteDependency [0] success</span></span> |<span data-ttu-id="8364e-341">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-341">boolean</span></span> | |
| <span data-ttu-id="8364e-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="8364e-342">remoteDependency [0] type</span></span> |<span data-ttu-id="8364e-343">string</span><span class="sxs-lookup"><span data-stu-id="8364e-343">string</span></span> |<span data-ttu-id="8364e-344">Http, Sql,...</span><span class="sxs-lookup"><span data-stu-id="8364e-344">Http, Sql,...</span></span> |
| <span data-ttu-id="8364e-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="8364e-345">remoteDependency [0] url</span></span> |<span data-ttu-id="8364e-346">string</span><span class="sxs-lookup"><span data-stu-id="8364e-346">string</span></span> |<span data-ttu-id="8364e-347">최대 길이 2000</span><span class="sxs-lookup"><span data-stu-id="8364e-347">Max length 2000</span></span> |
| <span data-ttu-id="8364e-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8364e-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="8364e-349">string</span><span class="sxs-lookup"><span data-stu-id="8364e-349">string</span></span> |<span data-ttu-id="8364e-350">최대 길이 2000</span><span class="sxs-lookup"><span data-stu-id="8364e-350">Max length 2000</span></span> |
| <span data-ttu-id="8364e-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8364e-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="8364e-352">string</span><span class="sxs-lookup"><span data-stu-id="8364e-352">string</span></span> | |
| <span data-ttu-id="8364e-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8364e-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="8364e-354">string</span><span class="sxs-lookup"><span data-stu-id="8364e-354">string</span></span> |<span data-ttu-id="8364e-355">최대 길이 200</span><span class="sxs-lookup"><span data-stu-id="8364e-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="8364e-356">요청</span><span class="sxs-lookup"><span data-stu-id="8364e-356">Requests</span></span>
<span data-ttu-id="8364e-357">[TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest)에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="8364e-358">hello 표준 모듈 측정 한 hello 서버에서이 tooreports 서버 응답 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-358">hello standard modules use this tooreports server response time, measured at hello server.</span></span>

| <span data-ttu-id="8364e-359">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-359">Path</span></span> | <span data-ttu-id="8364e-360">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-360">Type</span></span> | <span data-ttu-id="8364e-361">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-362">request [0] count</span></span> |<span data-ttu-id="8364e-363">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-363">integer</span></span> |<span data-ttu-id="8364e-364">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-365">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="8364e-367">number</span><span class="sxs-lookup"><span data-stu-id="8364e-367">number</span></span> |<span data-ttu-id="8364e-368">요청이 도착 tooresponse 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-368">Time from request arriving tooresponse.</span></span> <span data-ttu-id="8364e-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="8364e-369">1e7 == 1s</span></span> |
| <span data-ttu-id="8364e-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="8364e-370">request [0] id</span></span> |<span data-ttu-id="8364e-371">string</span><span class="sxs-lookup"><span data-stu-id="8364e-371">string</span></span> |<span data-ttu-id="8364e-372">작업 ID</span><span class="sxs-lookup"><span data-stu-id="8364e-372">Operation id</span></span> |
| <span data-ttu-id="8364e-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="8364e-373">request [0] name</span></span> |<span data-ttu-id="8364e-374">string</span><span class="sxs-lookup"><span data-stu-id="8364e-374">string</span></span> |<span data-ttu-id="8364e-375">GET/POST + url 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-375">GET/POST + url base.</span></span>  <span data-ttu-id="8364e-376">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="8364e-376">Max length 250</span></span> |
| <span data-ttu-id="8364e-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="8364e-377">request [0] responseCode</span></span> |<span data-ttu-id="8364e-378">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-378">integer</span></span> |<span data-ttu-id="8364e-379">HTTP 응답 전송 tooclient</span><span class="sxs-lookup"><span data-stu-id="8364e-379">HTTP response sent tooclient</span></span> |
| <span data-ttu-id="8364e-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="8364e-380">request [0] success</span></span> |<span data-ttu-id="8364e-381">부울</span><span class="sxs-lookup"><span data-stu-id="8364e-381">boolean</span></span> |<span data-ttu-id="8364e-382">기본값 == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="8364e-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="8364e-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="8364e-383">request [0] url</span></span> |<span data-ttu-id="8364e-384">string</span><span class="sxs-lookup"><span data-stu-id="8364e-384">string</span></span> |<span data-ttu-id="8364e-385">호스트를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="8364e-385">Not including host</span></span> |
| <span data-ttu-id="8364e-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8364e-386">request [0] urlData.base</span></span> |<span data-ttu-id="8364e-387">string</span><span class="sxs-lookup"><span data-stu-id="8364e-387">string</span></span> | |
| <span data-ttu-id="8364e-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8364e-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="8364e-389">string</span><span class="sxs-lookup"><span data-stu-id="8364e-389">string</span></span> | |
| <span data-ttu-id="8364e-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8364e-390">request [0] urlData.host</span></span> |<span data-ttu-id="8364e-391">string</span><span class="sxs-lookup"><span data-stu-id="8364e-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="8364e-392">페이지 보기 성능</span><span class="sxs-lookup"><span data-stu-id="8364e-392">Page View Performance</span></span>
<span data-ttu-id="8364e-393">Hello 브라우저에서 보낸 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-393">Sent by hello browser.</span></span> <span data-ttu-id="8364e-394">측정값 hello 시간 tooprocess는 페이지에서 사용자 시작 hello 요청 toodisplay (비동기 AJAX 호출 제외)를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-394">Measures hello time tooprocess a page, from user initiating hello request toodisplay complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="8364e-395">컨텍스트 값은 클라이언트 OS 및 브라우저 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="8364e-396">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-396">Path</span></span> | <span data-ttu-id="8364e-397">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-397">Type</span></span> | <span data-ttu-id="8364e-398">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="8364e-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="8364e-400">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-400">integer</span></span> |<span data-ttu-id="8364e-401">받는 hello HTML toodisplaying hello 페이지 끝 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-401">Time from end of receiving hello HTML toodisplaying hello page.</span></span> |
| <span data-ttu-id="8364e-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="8364e-402">clientPerformance [0] name</span></span> |<span data-ttu-id="8364e-403">string</span><span class="sxs-lookup"><span data-stu-id="8364e-403">string</span></span> | |
| <span data-ttu-id="8364e-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="8364e-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="8364e-405">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-405">integer</span></span> |<span data-ttu-id="8364e-406">걸린 시간 tooestablish 네트워크에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-406">Time taken tooestablish a network connection.</span></span> |
| <span data-ttu-id="8364e-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="8364e-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="8364e-408">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-408">integer</span></span> |<span data-ttu-id="8364e-409">끝 hello 요청 tooreceiving hello HTML 회신이 전송 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-409">Time from end of sending hello request tooreceiving hello HTML in reply.</span></span> |
| <span data-ttu-id="8364e-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="8364e-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="8364e-411">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-411">integer</span></span> |<span data-ttu-id="8364e-412">가져왔으면된 toosend hello HTTP 요청 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-412">Time from taken toosend hello HTTP request.</span></span> |
| <span data-ttu-id="8364e-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="8364e-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="8364e-414">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-414">integer</span></span> |<span data-ttu-id="8364e-415">Toosend hello 요청 toodisplaying hello 페이지 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-415">Time from starting toosend hello request toodisplaying hello page.</span></span> |
| <span data-ttu-id="8364e-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="8364e-416">clientPerformance [0] url</span></span> |<span data-ttu-id="8364e-417">string</span><span class="sxs-lookup"><span data-stu-id="8364e-417">string</span></span> |<span data-ttu-id="8364e-418">이 요청의 URL</span><span class="sxs-lookup"><span data-stu-id="8364e-418">URL of this request</span></span> |
| <span data-ttu-id="8364e-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8364e-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="8364e-420">string</span><span class="sxs-lookup"><span data-stu-id="8364e-420">string</span></span> | |
| <span data-ttu-id="8364e-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8364e-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="8364e-422">string</span><span class="sxs-lookup"><span data-stu-id="8364e-422">string</span></span> | |
| <span data-ttu-id="8364e-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8364e-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="8364e-424">string</span><span class="sxs-lookup"><span data-stu-id="8364e-424">string</span></span> | |
| <span data-ttu-id="8364e-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="8364e-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="8364e-426">string</span><span class="sxs-lookup"><span data-stu-id="8364e-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="8364e-427">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="8364e-427">Page Views</span></span>
<span data-ttu-id="8364e-428">trackPageView() 또는 [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)에서 전송</span><span class="sxs-lookup"><span data-stu-id="8364e-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="8364e-429">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-429">Path</span></span> | <span data-ttu-id="8364e-430">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-430">Type</span></span> | <span data-ttu-id="8364e-431">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-432">view [0] count</span></span> |<span data-ttu-id="8364e-433">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-433">integer</span></span> |<span data-ttu-id="8364e-434">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-435">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="8364e-437">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-437">integer</span></span> |<span data-ttu-id="8364e-438">필요에 따라 trackPageView()에서 또는 startTrackPage() - stopTrackPage()에 의해 설정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="8364e-439">ClientPerformance 값으로 동일한 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-439">Not hello same as clientPerformance values.</span></span> |
| <span data-ttu-id="8364e-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="8364e-440">view [0] name</span></span> |<span data-ttu-id="8364e-441">string</span><span class="sxs-lookup"><span data-stu-id="8364e-441">string</span></span> |<span data-ttu-id="8364e-442">페이지 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-442">Page title.</span></span>  <span data-ttu-id="8364e-443">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="8364e-443">Max length 250</span></span> |
| <span data-ttu-id="8364e-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="8364e-444">view [0] url</span></span> |<span data-ttu-id="8364e-445">string</span><span class="sxs-lookup"><span data-stu-id="8364e-445">string</span></span> | |
| <span data-ttu-id="8364e-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8364e-446">view [0] urlData.base</span></span> |<span data-ttu-id="8364e-447">string</span><span class="sxs-lookup"><span data-stu-id="8364e-447">string</span></span> | |
| <span data-ttu-id="8364e-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8364e-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="8364e-449">string</span><span class="sxs-lookup"><span data-stu-id="8364e-449">string</span></span> | |
| <span data-ttu-id="8364e-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8364e-450">view [0] urlData.host</span></span> |<span data-ttu-id="8364e-451">string</span><span class="sxs-lookup"><span data-stu-id="8364e-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="8364e-452">Availability</span><span class="sxs-lookup"><span data-stu-id="8364e-452">Availability</span></span>
<span data-ttu-id="8364e-453">[가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="8364e-454">Path</span><span class="sxs-lookup"><span data-stu-id="8364e-454">Path</span></span> | <span data-ttu-id="8364e-455">형식</span><span class="sxs-lookup"><span data-stu-id="8364e-455">Type</span></span> | <span data-ttu-id="8364e-456">참고</span><span class="sxs-lookup"><span data-stu-id="8364e-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8364e-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="8364e-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="8364e-458">string</span><span class="sxs-lookup"><span data-stu-id="8364e-458">string</span></span> |<span data-ttu-id="8364e-459">Availability</span><span class="sxs-lookup"><span data-stu-id="8364e-459">availability</span></span> |
| <span data-ttu-id="8364e-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="8364e-461">number</span><span class="sxs-lookup"><span data-stu-id="8364e-461">number</span></span> |<span data-ttu-id="8364e-462">1.0 또는 0.0</span><span class="sxs-lookup"><span data-stu-id="8364e-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="8364e-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="8364e-463">availability [0] count</span></span> |<span data-ttu-id="8364e-464">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-464">integer</span></span> |<span data-ttu-id="8364e-465">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="8364e-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8364e-466">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8364e-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8364e-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="8364e-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="8364e-468">string</span><span class="sxs-lookup"><span data-stu-id="8364e-468">string</span></span> | |
| <span data-ttu-id="8364e-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="8364e-470">정수</span><span class="sxs-lookup"><span data-stu-id="8364e-470">integer</span></span> | |
| <span data-ttu-id="8364e-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="8364e-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="8364e-472">string</span><span class="sxs-lookup"><span data-stu-id="8364e-472">string</span></span> | |
| <span data-ttu-id="8364e-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8364e-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="8364e-474">number</span><span class="sxs-lookup"><span data-stu-id="8364e-474">number</span></span> |<span data-ttu-id="8364e-475">테스트 기간</span><span class="sxs-lookup"><span data-stu-id="8364e-475">Duration of test.</span></span> <span data-ttu-id="8364e-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="8364e-476">1e7==1s</span></span> |
| <span data-ttu-id="8364e-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="8364e-477">availability [0] message</span></span> |<span data-ttu-id="8364e-478">string</span><span class="sxs-lookup"><span data-stu-id="8364e-478">string</span></span> |<span data-ttu-id="8364e-479">오류 진단</span><span class="sxs-lookup"><span data-stu-id="8364e-479">Failure diagnostic</span></span> |
| <span data-ttu-id="8364e-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="8364e-480">availability [0] result</span></span> |<span data-ttu-id="8364e-481">string</span><span class="sxs-lookup"><span data-stu-id="8364e-481">string</span></span> |<span data-ttu-id="8364e-482">성공/실패</span><span class="sxs-lookup"><span data-stu-id="8364e-482">Pass/Fail</span></span> |
| <span data-ttu-id="8364e-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="8364e-483">availability [0] runLocation</span></span> |<span data-ttu-id="8364e-484">string</span><span class="sxs-lookup"><span data-stu-id="8364e-484">string</span></span> |<span data-ttu-id="8364e-485">Http 요청의 지역 소스</span><span class="sxs-lookup"><span data-stu-id="8364e-485">Geo source of http req</span></span> |
| <span data-ttu-id="8364e-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="8364e-486">availability [0] testName</span></span> |<span data-ttu-id="8364e-487">string</span><span class="sxs-lookup"><span data-stu-id="8364e-487">string</span></span> | |
| <span data-ttu-id="8364e-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="8364e-488">availability [0] testRunId</span></span> |<span data-ttu-id="8364e-489">string</span><span class="sxs-lookup"><span data-stu-id="8364e-489">string</span></span> | |
| <span data-ttu-id="8364e-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="8364e-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="8364e-491">string</span><span class="sxs-lookup"><span data-stu-id="8364e-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="8364e-492">메트릭</span><span class="sxs-lookup"><span data-stu-id="8364e-492">Metrics</span></span>
<span data-ttu-id="8364e-493">TrackMetric()에서 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="8364e-494">context.custom.metrics[0 hello 메트릭 값을 찾을 수]</span><span class="sxs-lookup"><span data-stu-id="8364e-494">hello metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="8364e-495">예:</span><span class="sxs-lookup"><span data-stu-id="8364e-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="8364e-496">메트릭 값 정보</span><span class="sxs-lookup"><span data-stu-id="8364e-496">About metric values</span></span>
<span data-ttu-id="8364e-497">메트릭 보고서 및 기타 다른 곳의 메트릭 값은 모두 표준 개체 구조를 사용하여 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="8364e-498">예:</span><span class="sxs-lookup"><span data-stu-id="8364e-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="8364e-499">Hello 이후-hello 표준 SDK 모듈에서 보고 하는 모든 값에에서 변경 될 수 있습니다이 하지만 현재- `count==1` 만 hello 및 `name` 및 `value` 필드는 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-499">Currently - though this might change in hello future - in all values reported from hello standard SDK modules, `count==1` and only hello `name` and `value` fields are useful.</span></span> <span data-ttu-id="8364e-500">hello만 될 수 없는 다른 되는 경우가 TrackMetric 호출을 작성 하는 경우 설정 하는 hello 다른 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-500">hello only case where they would be different would be if you write your own TrackMetric calls in which you set hello other parameters.</span></span>

<span data-ttu-id="8364e-501">용도 hello hello의 다른 필드는 tooallow 메트릭 toobe hello SDK, tooreduce 트래픽 toohello 포털에에서 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-501">hello purpose of hello other fields is tooallow metrics toobe aggregated in hello SDK, tooreduce traffic toohello portal.</span></span> <span data-ttu-id="8364e-502">예를 들어 각 메트릭 보고서를 보내기 전에 여러 연속 판독값의 평균을 낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="8364e-503">그런 다음 hello min, max, 표준 편차 및 집계 값 (합계 또는 평균)을 계산 하는 hello 보고서가 나타내는 판독값 count toohello 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-503">Then you would calculate hello min, max, standard deviation and aggregate value (sum or average) and set count toohello number of readings represented by hello report.</span></span>

<span data-ttu-id="8364e-504">위 hello 표에서 hello 거의 사용 되지 않는 필드 count, min, max, stdDev 및 sampledValue를 생략 했습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-504">In hello tables above, we have omitted hello rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="8364e-505">사전 집계 메트릭을 대신 사용할 수 있습니다 [샘플링](app-insights-sampling.md) tooreduce hello 양의 원격 분석 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need tooreduce hello volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="8364e-506">기간</span><span class="sxs-lookup"><span data-stu-id="8364e-506">Durations</span></span>
<span data-ttu-id="8364e-507">달리 명시된 경우를 제외하고, 기간은 10분의 1 마이크로초로 표현되므로 10000000.0은 1초를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8364e-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="8364e-508">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8364e-508">See also</span></span>
* [<span data-ttu-id="8364e-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8364e-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="8364e-510">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="8364e-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="8364e-511">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="8364e-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
