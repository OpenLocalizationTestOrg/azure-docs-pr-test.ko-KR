---
title: "Azure Application Insights 데이터 모델 | Microsoft Docs"
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
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="10eb6-103">Application Insights 데이터 모델 내보내기</span><span class="sxs-lookup"><span data-stu-id="10eb6-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="10eb6-104">이 테이블은 [Application Insights](app-insights-overview.md) SDK에서 포털로 전송된 원격 분석의 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="10eb6-105">이러한 속성이 [연속 내보내기](app-insights-export-telemetry.md)에서 데이터 출력에 표시됩니다</span><span class="sxs-lookup"><span data-stu-id="10eb6-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="10eb6-106">또한 [메트릭 탐색기](app-insights-metrics-explorer.md) 및 [진단 검색](app-insights-diagnostic-search.md)의 속성 필터에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="10eb6-107">주의할 사항:</span><span class="sxs-lookup"><span data-stu-id="10eb6-107">Points to note:</span></span>

* <span data-ttu-id="10eb6-108">`[0]` 은 인덱스를 삽입해야 하는 경로의 지점을 나타내지만 항상 0은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="10eb6-109">기간의 단위는 10분의 1 마이크로초이므로 10000000은 1초입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="10eb6-110">날짜와 시간은 UTC이며 ISO 형식 `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="10eb6-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="10eb6-111">예제</span><span class="sxs-lookup"><span data-stu-id="10eb6-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
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
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
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
  <span data-ttu-id="10eb6-112">}</span><span class="sxs-lookup"><span data-stu-id="10eb6-112">}</span></span>

## <a name="context"></a><span data-ttu-id="10eb6-113">Context</span><span class="sxs-lookup"><span data-stu-id="10eb6-113">Context</span></span>
<span data-ttu-id="10eb6-114">모든 유형의 원격 분석에는 컨텍스트 섹션이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="10eb6-115">이러한 모든 필드가 모든 데이터 요소와 함께 전송되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="10eb6-116">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-116">Path</span></span> | <span data-ttu-id="10eb6-117">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-117">Type</span></span> | <span data-ttu-id="10eb6-118">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="10eb6-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="10eb6-120">object [ ]</span><span class="sxs-lookup"><span data-stu-id="10eb6-120">object [ ]</span></span> |<span data-ttu-id="10eb6-121">사용자 지정 속성 매개 변수에 의해 설정되는 키-값 문자열 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="10eb6-122">키 최대 길이가 100이고, 값 최대 길이가 1024입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="10eb6-123">100개 이상의 고유 값, 속성을 검색할 수 있지만 구분에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="10eb6-124">ikey당 최대 키는 200개입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="10eb6-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="10eb6-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="10eb6-126">object [ ]</span><span class="sxs-lookup"><span data-stu-id="10eb6-126">object [ ]</span></span> |<span data-ttu-id="10eb6-127">사용자 지정 측정 매개 변수 및 TrackMetrics에 의해 설정된 키-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="10eb6-128">키 최대 길이가 100이고, 값은 숫자가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="10eb6-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="10eb6-129">context.data.eventTime</span></span> |<span data-ttu-id="10eb6-130">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-130">string</span></span> |<span data-ttu-id="10eb6-131">UTC</span><span class="sxs-lookup"><span data-stu-id="10eb6-131">UTC</span></span> |
| <span data-ttu-id="10eb6-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="10eb6-132">context.data.isSynthetic</span></span> |<span data-ttu-id="10eb6-133">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-133">boolean</span></span> |<span data-ttu-id="10eb6-134">요청이 봇 또는 웹 테스트에서 들어오는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="10eb6-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="10eb6-135">context.data.samplingRate</span></span> |<span data-ttu-id="10eb6-136">number</span><span class="sxs-lookup"><span data-stu-id="10eb6-136">number</span></span> |<span data-ttu-id="10eb6-137">포털에 전송되는 SDK에 의해 생성된 원격 분석의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="10eb6-138">범위는 0.0-100.0입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="10eb6-139">context.device</span><span class="sxs-lookup"><span data-stu-id="10eb6-139">context.device</span></span> |<span data-ttu-id="10eb6-140">object</span><span class="sxs-lookup"><span data-stu-id="10eb6-140">object</span></span> |<span data-ttu-id="10eb6-141">클라이언트 장치</span><span class="sxs-lookup"><span data-stu-id="10eb6-141">Client device</span></span> |
| <span data-ttu-id="10eb6-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="10eb6-142">context.device.browser</span></span> |<span data-ttu-id="10eb6-143">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-143">string</span></span> |<span data-ttu-id="10eb6-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="10eb6-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="10eb6-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="10eb6-145">context.device.browserVersion</span></span> |<span data-ttu-id="10eb6-146">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-146">string</span></span> |<span data-ttu-id="10eb6-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="10eb6-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="10eb6-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="10eb6-148">context.device.deviceModel</span></span> |<span data-ttu-id="10eb6-149">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-149">string</span></span> | |
| <span data-ttu-id="10eb6-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="10eb6-150">context.device.deviceName</span></span> |<span data-ttu-id="10eb6-151">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-151">string</span></span> | |
| <span data-ttu-id="10eb6-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="10eb6-152">context.device.id</span></span> |<span data-ttu-id="10eb6-153">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-153">string</span></span> | |
| <span data-ttu-id="10eb6-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="10eb6-154">context.device.locale</span></span> |<span data-ttu-id="10eb6-155">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-155">string</span></span> |<span data-ttu-id="10eb6-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="10eb6-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="10eb6-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="10eb6-157">context.device.network</span></span> |<span data-ttu-id="10eb6-158">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-158">string</span></span> | |
| <span data-ttu-id="10eb6-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="10eb6-159">context.device.oemName</span></span> |<span data-ttu-id="10eb6-160">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-160">string</span></span> | |
| <span data-ttu-id="10eb6-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="10eb6-161">context.device.osVersion</span></span> |<span data-ttu-id="10eb6-162">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-162">string</span></span> |<span data-ttu-id="10eb6-163">호스트 OS</span><span class="sxs-lookup"><span data-stu-id="10eb6-163">Host OS</span></span> |
| <span data-ttu-id="10eb6-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="10eb6-164">context.device.roleInstance</span></span> |<span data-ttu-id="10eb6-165">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-165">string</span></span> |<span data-ttu-id="10eb6-166">서버 호스트의 ID</span><span class="sxs-lookup"><span data-stu-id="10eb6-166">ID of server host</span></span> |
| <span data-ttu-id="10eb6-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="10eb6-167">context.device.roleName</span></span> |<span data-ttu-id="10eb6-168">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-168">string</span></span> | |
| <span data-ttu-id="10eb6-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="10eb6-169">context.device.type</span></span> |<span data-ttu-id="10eb6-170">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-170">string</span></span> |<span data-ttu-id="10eb6-171">PC, 브라우저...</span><span class="sxs-lookup"><span data-stu-id="10eb6-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="10eb6-172">context.location</span><span class="sxs-lookup"><span data-stu-id="10eb6-172">context.location</span></span> |<span data-ttu-id="10eb6-173">object</span><span class="sxs-lookup"><span data-stu-id="10eb6-173">object</span></span> |<span data-ttu-id="10eb6-174">clientip에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-174">Derived from clientip.</span></span> |
| <span data-ttu-id="10eb6-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="10eb6-175">context.location.city</span></span> |<span data-ttu-id="10eb6-176">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-176">string</span></span> |<span data-ttu-id="10eb6-177">알 수 있는 경우 clientip에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="10eb6-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="10eb6-178">context.location.clientip</span></span> |<span data-ttu-id="10eb6-179">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-179">string</span></span> |<span data-ttu-id="10eb6-180">마지막 팔각형이 0으로 익명 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="10eb6-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="10eb6-181">context.location.continent</span></span> |<span data-ttu-id="10eb6-182">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-182">string</span></span> | |
| <span data-ttu-id="10eb6-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="10eb6-183">context.location.country</span></span> |<span data-ttu-id="10eb6-184">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-184">string</span></span> | |
| <span data-ttu-id="10eb6-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="10eb6-185">context.location.province</span></span> |<span data-ttu-id="10eb6-186">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-186">string</span></span> |<span data-ttu-id="10eb6-187">시/도</span><span class="sxs-lookup"><span data-stu-id="10eb6-187">State or province</span></span> |
| <span data-ttu-id="10eb6-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="10eb6-188">context.operation.id</span></span> |<span data-ttu-id="10eb6-189">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-189">string</span></span> |<span data-ttu-id="10eb6-190">작업 ID가 동일한 항목은 포털에서 관련 항목으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="10eb6-191">일반적으로 요청 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-191">Usually the request id.</span></span> |
| <span data-ttu-id="10eb6-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="10eb6-192">context.operation.name</span></span> |<span data-ttu-id="10eb6-193">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-193">string</span></span> |<span data-ttu-id="10eb6-194">URL 또는 요청 이름</span><span class="sxs-lookup"><span data-stu-id="10eb6-194">url or request name</span></span> |
| <span data-ttu-id="10eb6-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="10eb6-195">context.operation.parentId</span></span> |<span data-ttu-id="10eb6-196">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-196">string</span></span> |<span data-ttu-id="10eb6-197">중첩된 관련 항목을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-197">Allows nested related items.</span></span> |
| <span data-ttu-id="10eb6-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="10eb6-198">context.session.id</span></span> |<span data-ttu-id="10eb6-199">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-199">string</span></span> |<span data-ttu-id="10eb6-200">동일한 소스의 작업 그룹 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="10eb6-201">30분 동안 작업이 없으면 세션이 끝난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="10eb6-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="10eb6-202">context.session.isFirst</span></span> |<span data-ttu-id="10eb6-203">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-203">boolean</span></span> | |
| <span data-ttu-id="10eb6-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="10eb6-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="10eb6-205">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-205">string</span></span> | |
| <span data-ttu-id="10eb6-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="10eb6-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="10eb6-207">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-207">string</span></span> | |
| <span data-ttu-id="10eb6-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="10eb6-208">context.user.anonId</span></span> |<span data-ttu-id="10eb6-209">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-209">string</span></span> | |
| <span data-ttu-id="10eb6-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="10eb6-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="10eb6-211">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-211">string</span></span> |[<span data-ttu-id="10eb6-212">인증된 사용자</span><span class="sxs-lookup"><span data-stu-id="10eb6-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="10eb6-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="10eb6-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="10eb6-214">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-214">boolean</span></span> | |
| <span data-ttu-id="10eb6-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="10eb6-215">internal.data.documentVersion</span></span> |<span data-ttu-id="10eb6-216">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-216">string</span></span> | |
| <span data-ttu-id="10eb6-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="10eb6-217">internal.data.id</span></span> |<span data-ttu-id="10eb6-218">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="10eb6-219">이벤트</span><span class="sxs-lookup"><span data-stu-id="10eb6-219">Events</span></span>
<span data-ttu-id="10eb6-220">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)에 의해 생성된 사용자 지정 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="10eb6-221">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-221">Path</span></span> | <span data-ttu-id="10eb6-222">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-222">Type</span></span> | <span data-ttu-id="10eb6-223">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-224">event [0] count</span></span> |<span data-ttu-id="10eb6-225">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-225">integer</span></span> |<span data-ttu-id="10eb6-226">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-227">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="10eb6-228">event [0] name</span></span> |<span data-ttu-id="10eb6-229">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-229">string</span></span> |<span data-ttu-id="10eb6-230">이벤트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-230">Event name.</span></span>  <span data-ttu-id="10eb6-231">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="10eb6-231">Max length 250.</span></span> |
| <span data-ttu-id="10eb6-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="10eb6-232">event [0] url</span></span> |<span data-ttu-id="10eb6-233">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-233">string</span></span> | |
| <span data-ttu-id="10eb6-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="10eb6-234">event [0] urlData.base</span></span> |<span data-ttu-id="10eb6-235">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-235">string</span></span> | |
| <span data-ttu-id="10eb6-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="10eb6-236">event [0] urlData.host</span></span> |<span data-ttu-id="10eb6-237">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="10eb6-238">예외</span><span class="sxs-lookup"><span data-stu-id="10eb6-238">Exceptions</span></span>
<span data-ttu-id="10eb6-239">서버 및 브라우저의 [예외](app-insights-asp-net-exceptions.md) 를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="10eb6-240">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-240">Path</span></span> | <span data-ttu-id="10eb6-241">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-241">Type</span></span> | <span data-ttu-id="10eb6-242">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="10eb6-243">basicException [0] assembly</span></span> |<span data-ttu-id="10eb6-244">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-244">string</span></span> | |
| <span data-ttu-id="10eb6-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-245">basicException [0] count</span></span> |<span data-ttu-id="10eb6-246">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-246">integer</span></span> |<span data-ttu-id="10eb6-247">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-248">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="10eb6-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="10eb6-250">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-250">string</span></span> | |
| <span data-ttu-id="10eb6-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="10eb6-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="10eb6-252">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-252">string</span></span> | |
| <span data-ttu-id="10eb6-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="10eb6-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="10eb6-254">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-254">string</span></span> | |
| <span data-ttu-id="10eb6-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="10eb6-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="10eb6-256">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-256">string</span></span> | |
| <span data-ttu-id="10eb6-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="10eb6-257">basicException [0] handledAt</span></span> |<span data-ttu-id="10eb6-258">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-258">string</span></span> | |
| <span data-ttu-id="10eb6-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="10eb6-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="10eb6-260">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-260">boolean</span></span> | |
| <span data-ttu-id="10eb6-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="10eb6-261">basicException [0] id</span></span> |<span data-ttu-id="10eb6-262">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-262">string</span></span> | |
| <span data-ttu-id="10eb6-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="10eb6-263">basicException [0] method</span></span> |<span data-ttu-id="10eb6-264">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-264">string</span></span> | |
| <span data-ttu-id="10eb6-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="10eb6-265">basicException [0] message</span></span> |<span data-ttu-id="10eb6-266">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-266">string</span></span> |<span data-ttu-id="10eb6-267">예외 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-267">Exception message.</span></span> <span data-ttu-id="10eb6-268">최대 길이 10000</span><span class="sxs-lookup"><span data-stu-id="10eb6-268">Max length 10k.</span></span> |
| <span data-ttu-id="10eb6-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="10eb6-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="10eb6-270">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-270">string</span></span> | |
| <span data-ttu-id="10eb6-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="10eb6-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="10eb6-272">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-272">string</span></span> | |
| <span data-ttu-id="10eb6-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="10eb6-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="10eb6-274">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-274">string</span></span> | |
| <span data-ttu-id="10eb6-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="10eb6-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="10eb6-276">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-276">string</span></span> | |
| <span data-ttu-id="10eb6-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="10eb6-277">basicException [0] outerId</span></span> |<span data-ttu-id="10eb6-278">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-278">string</span></span> | |
| <span data-ttu-id="10eb6-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="10eb6-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="10eb6-280">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-280">string</span></span> | |
| <span data-ttu-id="10eb6-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="10eb6-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="10eb6-282">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-282">string</span></span> | |
| <span data-ttu-id="10eb6-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="10eb6-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="10eb6-284">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-284">integer</span></span> | |
| <span data-ttu-id="10eb6-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="10eb6-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="10eb6-286">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-286">integer</span></span> | |
| <span data-ttu-id="10eb6-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="10eb6-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="10eb6-288">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-288">string</span></span> | |
| <span data-ttu-id="10eb6-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="10eb6-289">basicException [0] stack</span></span> |<span data-ttu-id="10eb6-290">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-290">string</span></span> |<span data-ttu-id="10eb6-291">최대 길이 10000</span><span class="sxs-lookup"><span data-stu-id="10eb6-291">Max length 10k</span></span> |
| <span data-ttu-id="10eb6-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="10eb6-292">basicException [0] typeName</span></span> |<span data-ttu-id="10eb6-293">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="10eb6-294">추적 메시지</span><span class="sxs-lookup"><span data-stu-id="10eb6-294">Trace Messages</span></span>
<span data-ttu-id="10eb6-295">[TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace) 및 [로깅 어댑터](app-insights-asp-net-trace-logs.md)에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="10eb6-296">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-296">Path</span></span> | <span data-ttu-id="10eb6-297">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-297">Type</span></span> | <span data-ttu-id="10eb6-298">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="10eb6-299">message [0] loggerName</span></span> |<span data-ttu-id="10eb6-300">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-300">string</span></span> | |
| <span data-ttu-id="10eb6-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="10eb6-301">message [0] parameters</span></span> |<span data-ttu-id="10eb6-302">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-302">string</span></span> | |
| <span data-ttu-id="10eb6-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="10eb6-303">message [0] raw</span></span> |<span data-ttu-id="10eb6-304">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-304">string</span></span> |<span data-ttu-id="10eb6-305">로그 메시지입니다(최대 길이 10k).</span><span class="sxs-lookup"><span data-stu-id="10eb6-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="10eb6-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="10eb6-306">message [0] severityLevel</span></span> |<span data-ttu-id="10eb6-307">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="10eb6-308">원격 종속성</span><span class="sxs-lookup"><span data-stu-id="10eb6-308">Remote dependency</span></span>
<span data-ttu-id="10eb6-309">TrackDependency에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-309">Sent by TrackDependency.</span></span> <span data-ttu-id="10eb6-310">서버의 [종속성에 대한 호출](app-insights-asp-net-dependencies.md) 과 브라우저의 AJAX 호출 성능 및 사용을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="10eb6-311">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-311">Path</span></span> | <span data-ttu-id="10eb6-312">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-312">Type</span></span> | <span data-ttu-id="10eb6-313">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="10eb6-314">remoteDependency [0] async</span></span> |<span data-ttu-id="10eb6-315">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-315">boolean</span></span> | |
| <span data-ttu-id="10eb6-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="10eb6-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="10eb6-317">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-317">string</span></span> | |
| <span data-ttu-id="10eb6-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="10eb6-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="10eb6-319">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-319">string</span></span> |<span data-ttu-id="10eb6-320">예를 들어 "홈/인덱스"</span><span class="sxs-lookup"><span data-stu-id="10eb6-320">For example "home/index"</span></span> |
| <span data-ttu-id="10eb6-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-321">remoteDependency [0] count</span></span> |<span data-ttu-id="10eb6-322">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-322">integer</span></span> |<span data-ttu-id="10eb6-323">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-324">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="10eb6-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="10eb6-326">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-326">string</span></span> |<span data-ttu-id="10eb6-327">HTTP, SQL, ...</span><span class="sxs-lookup"><span data-stu-id="10eb6-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="10eb6-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="10eb6-329">number</span><span class="sxs-lookup"><span data-stu-id="10eb6-329">number</span></span> |<span data-ttu-id="10eb6-330">호출부터 종속성의 응답 완료까지 걸리는 시간</span><span class="sxs-lookup"><span data-stu-id="10eb6-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="10eb6-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="10eb6-331">remoteDependency [0] id</span></span> |<span data-ttu-id="10eb6-332">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-332">string</span></span> | |
| <span data-ttu-id="10eb6-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="10eb6-333">remoteDependency [0] name</span></span> |<span data-ttu-id="10eb6-334">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-334">string</span></span> |<span data-ttu-id="10eb6-335">Url.</span><span class="sxs-lookup"><span data-stu-id="10eb6-335">Url.</span></span> <span data-ttu-id="10eb6-336">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="10eb6-336">Max length 250.</span></span> |
| <span data-ttu-id="10eb6-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="10eb6-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="10eb6-338">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-338">string</span></span> |<span data-ttu-id="10eb6-339">HTTP 종속성에서</span><span class="sxs-lookup"><span data-stu-id="10eb6-339">from HTTP dependency</span></span> |
| <span data-ttu-id="10eb6-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="10eb6-340">remoteDependency [0] success</span></span> |<span data-ttu-id="10eb6-341">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-341">boolean</span></span> | |
| <span data-ttu-id="10eb6-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="10eb6-342">remoteDependency [0] type</span></span> |<span data-ttu-id="10eb6-343">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-343">string</span></span> |<span data-ttu-id="10eb6-344">Http, Sql,...</span><span class="sxs-lookup"><span data-stu-id="10eb6-344">Http, Sql,...</span></span> |
| <span data-ttu-id="10eb6-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="10eb6-345">remoteDependency [0] url</span></span> |<span data-ttu-id="10eb6-346">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-346">string</span></span> |<span data-ttu-id="10eb6-347">최대 길이 2000</span><span class="sxs-lookup"><span data-stu-id="10eb6-347">Max length 2000</span></span> |
| <span data-ttu-id="10eb6-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="10eb6-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="10eb6-349">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-349">string</span></span> |<span data-ttu-id="10eb6-350">최대 길이 2000</span><span class="sxs-lookup"><span data-stu-id="10eb6-350">Max length 2000</span></span> |
| <span data-ttu-id="10eb6-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="10eb6-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="10eb6-352">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-352">string</span></span> | |
| <span data-ttu-id="10eb6-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="10eb6-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="10eb6-354">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-354">string</span></span> |<span data-ttu-id="10eb6-355">최대 길이 200</span><span class="sxs-lookup"><span data-stu-id="10eb6-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="10eb6-356">요청</span><span class="sxs-lookup"><span data-stu-id="10eb6-356">Requests</span></span>
<span data-ttu-id="10eb6-357">[TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest)에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="10eb6-358">표준 모듈이 서버에서 측정된 서버 응답 시간을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="10eb6-359">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-359">Path</span></span> | <span data-ttu-id="10eb6-360">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-360">Type</span></span> | <span data-ttu-id="10eb6-361">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-362">request [0] count</span></span> |<span data-ttu-id="10eb6-363">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-363">integer</span></span> |<span data-ttu-id="10eb6-364">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-365">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="10eb6-367">number</span><span class="sxs-lookup"><span data-stu-id="10eb6-367">number</span></span> |<span data-ttu-id="10eb6-368">요청부터 응답까지 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-368">Time from request arriving to response.</span></span> <span data-ttu-id="10eb6-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="10eb6-369">1e7 == 1s</span></span> |
| <span data-ttu-id="10eb6-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="10eb6-370">request [0] id</span></span> |<span data-ttu-id="10eb6-371">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-371">string</span></span> |<span data-ttu-id="10eb6-372">작업 ID</span><span class="sxs-lookup"><span data-stu-id="10eb6-372">Operation id</span></span> |
| <span data-ttu-id="10eb6-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="10eb6-373">request [0] name</span></span> |<span data-ttu-id="10eb6-374">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-374">string</span></span> |<span data-ttu-id="10eb6-375">GET/POST + url 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-375">GET/POST + url base.</span></span>  <span data-ttu-id="10eb6-376">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="10eb6-376">Max length 250</span></span> |
| <span data-ttu-id="10eb6-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="10eb6-377">request [0] responseCode</span></span> |<span data-ttu-id="10eb6-378">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-378">integer</span></span> |<span data-ttu-id="10eb6-379">클라이언트에 보낸 HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="10eb6-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="10eb6-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="10eb6-380">request [0] success</span></span> |<span data-ttu-id="10eb6-381">부울</span><span class="sxs-lookup"><span data-stu-id="10eb6-381">boolean</span></span> |<span data-ttu-id="10eb6-382">기본값 == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="10eb6-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="10eb6-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="10eb6-383">request [0] url</span></span> |<span data-ttu-id="10eb6-384">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-384">string</span></span> |<span data-ttu-id="10eb6-385">호스트를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="10eb6-385">Not including host</span></span> |
| <span data-ttu-id="10eb6-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="10eb6-386">request [0] urlData.base</span></span> |<span data-ttu-id="10eb6-387">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-387">string</span></span> | |
| <span data-ttu-id="10eb6-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="10eb6-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="10eb6-389">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-389">string</span></span> | |
| <span data-ttu-id="10eb6-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="10eb6-390">request [0] urlData.host</span></span> |<span data-ttu-id="10eb6-391">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="10eb6-392">페이지 보기 성능</span><span class="sxs-lookup"><span data-stu-id="10eb6-392">Page View Performance</span></span>
<span data-ttu-id="10eb6-393">브라우저에서 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-393">Sent by the browser.</span></span> <span data-ttu-id="10eb6-394">사용자가 요청을 시작할 때부터 표시가 완료될 때까지 페이지 처리 시간을 측정합니다(비동기 AJAX 호출 제외).</span><span class="sxs-lookup"><span data-stu-id="10eb6-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="10eb6-395">컨텍스트 값은 클라이언트 OS 및 브라우저 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="10eb6-396">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-396">Path</span></span> | <span data-ttu-id="10eb6-397">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-397">Type</span></span> | <span data-ttu-id="10eb6-398">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="10eb6-400">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-400">integer</span></span> |<span data-ttu-id="10eb6-401">HTML 수신 완료부터 페이지 표시까지 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="10eb6-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="10eb6-402">clientPerformance [0] name</span></span> |<span data-ttu-id="10eb6-403">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-403">string</span></span> | |
| <span data-ttu-id="10eb6-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="10eb6-405">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-405">integer</span></span> |<span data-ttu-id="10eb6-406">네트워크 연결을 설정하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="10eb6-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="10eb6-408">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-408">integer</span></span> |<span data-ttu-id="10eb6-409">요청 전송 완료부터 HTML 응답 수신까지 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="10eb6-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="10eb6-411">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-411">integer</span></span> |<span data-ttu-id="10eb6-412">HTTP 요청을 전송하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="10eb6-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="10eb6-414">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-414">integer</span></span> |<span data-ttu-id="10eb6-415">요청 전송 시작부터 페이지 표시까지 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="10eb6-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="10eb6-416">clientPerformance [0] url</span></span> |<span data-ttu-id="10eb6-417">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-417">string</span></span> |<span data-ttu-id="10eb6-418">이 요청의 URL</span><span class="sxs-lookup"><span data-stu-id="10eb6-418">URL of this request</span></span> |
| <span data-ttu-id="10eb6-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="10eb6-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="10eb6-420">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-420">string</span></span> | |
| <span data-ttu-id="10eb6-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="10eb6-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="10eb6-422">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-422">string</span></span> | |
| <span data-ttu-id="10eb6-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="10eb6-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="10eb6-424">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-424">string</span></span> | |
| <span data-ttu-id="10eb6-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="10eb6-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="10eb6-426">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="10eb6-427">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="10eb6-427">Page Views</span></span>
<span data-ttu-id="10eb6-428">trackPageView() 또는 [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)에서 전송</span><span class="sxs-lookup"><span data-stu-id="10eb6-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="10eb6-429">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-429">Path</span></span> | <span data-ttu-id="10eb6-430">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-430">Type</span></span> | <span data-ttu-id="10eb6-431">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-432">view [0] count</span></span> |<span data-ttu-id="10eb6-433">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-433">integer</span></span> |<span data-ttu-id="10eb6-434">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-435">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="10eb6-437">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-437">integer</span></span> |<span data-ttu-id="10eb6-438">필요에 따라 trackPageView()에서 또는 startTrackPage() - stopTrackPage()에 의해 설정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="10eb6-439">clientPerformance 값과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="10eb6-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="10eb6-440">view [0] name</span></span> |<span data-ttu-id="10eb6-441">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-441">string</span></span> |<span data-ttu-id="10eb6-442">페이지 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-442">Page title.</span></span>  <span data-ttu-id="10eb6-443">최대 길이 250</span><span class="sxs-lookup"><span data-stu-id="10eb6-443">Max length 250</span></span> |
| <span data-ttu-id="10eb6-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="10eb6-444">view [0] url</span></span> |<span data-ttu-id="10eb6-445">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-445">string</span></span> | |
| <span data-ttu-id="10eb6-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="10eb6-446">view [0] urlData.base</span></span> |<span data-ttu-id="10eb6-447">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-447">string</span></span> | |
| <span data-ttu-id="10eb6-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="10eb6-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="10eb6-449">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-449">string</span></span> | |
| <span data-ttu-id="10eb6-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="10eb6-450">view [0] urlData.host</span></span> |<span data-ttu-id="10eb6-451">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="10eb6-452">Availability</span><span class="sxs-lookup"><span data-stu-id="10eb6-452">Availability</span></span>
<span data-ttu-id="10eb6-453">[가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="10eb6-454">Path</span><span class="sxs-lookup"><span data-stu-id="10eb6-454">Path</span></span> | <span data-ttu-id="10eb6-455">형식</span><span class="sxs-lookup"><span data-stu-id="10eb6-455">Type</span></span> | <span data-ttu-id="10eb6-456">참고</span><span class="sxs-lookup"><span data-stu-id="10eb6-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10eb6-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="10eb6-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="10eb6-458">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-458">string</span></span> |<span data-ttu-id="10eb6-459">Availability</span><span class="sxs-lookup"><span data-stu-id="10eb6-459">availability</span></span> |
| <span data-ttu-id="10eb6-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="10eb6-461">number</span><span class="sxs-lookup"><span data-stu-id="10eb6-461">number</span></span> |<span data-ttu-id="10eb6-462">1.0 또는 0.0</span><span class="sxs-lookup"><span data-stu-id="10eb6-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="10eb6-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="10eb6-463">availability [0] count</span></span> |<span data-ttu-id="10eb6-464">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-464">integer</span></span> |<span data-ttu-id="10eb6-465">100/([샘플링](app-insights-sampling.md) 속도)</span><span class="sxs-lookup"><span data-stu-id="10eb6-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="10eb6-466">예: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="10eb6-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="10eb6-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="10eb6-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="10eb6-468">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-468">string</span></span> | |
| <span data-ttu-id="10eb6-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="10eb6-470">정수</span><span class="sxs-lookup"><span data-stu-id="10eb6-470">integer</span></span> | |
| <span data-ttu-id="10eb6-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="10eb6-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="10eb6-472">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-472">string</span></span> | |
| <span data-ttu-id="10eb6-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="10eb6-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="10eb6-474">number</span><span class="sxs-lookup"><span data-stu-id="10eb6-474">number</span></span> |<span data-ttu-id="10eb6-475">테스트 기간</span><span class="sxs-lookup"><span data-stu-id="10eb6-475">Duration of test.</span></span> <span data-ttu-id="10eb6-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="10eb6-476">1e7==1s</span></span> |
| <span data-ttu-id="10eb6-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="10eb6-477">availability [0] message</span></span> |<span data-ttu-id="10eb6-478">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-478">string</span></span> |<span data-ttu-id="10eb6-479">오류 진단</span><span class="sxs-lookup"><span data-stu-id="10eb6-479">Failure diagnostic</span></span> |
| <span data-ttu-id="10eb6-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="10eb6-480">availability [0] result</span></span> |<span data-ttu-id="10eb6-481">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-481">string</span></span> |<span data-ttu-id="10eb6-482">성공/실패</span><span class="sxs-lookup"><span data-stu-id="10eb6-482">Pass/Fail</span></span> |
| <span data-ttu-id="10eb6-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="10eb6-483">availability [0] runLocation</span></span> |<span data-ttu-id="10eb6-484">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-484">string</span></span> |<span data-ttu-id="10eb6-485">Http 요청의 지역 소스</span><span class="sxs-lookup"><span data-stu-id="10eb6-485">Geo source of http req</span></span> |
| <span data-ttu-id="10eb6-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="10eb6-486">availability [0] testName</span></span> |<span data-ttu-id="10eb6-487">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-487">string</span></span> | |
| <span data-ttu-id="10eb6-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="10eb6-488">availability [0] testRunId</span></span> |<span data-ttu-id="10eb6-489">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-489">string</span></span> | |
| <span data-ttu-id="10eb6-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="10eb6-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="10eb6-491">string</span><span class="sxs-lookup"><span data-stu-id="10eb6-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="10eb6-492">메트릭</span><span class="sxs-lookup"><span data-stu-id="10eb6-492">Metrics</span></span>
<span data-ttu-id="10eb6-493">TrackMetric()에서 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="10eb6-494">메트릭 값은 context.custom.metrics[0]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="10eb6-495">예:</span><span class="sxs-lookup"><span data-stu-id="10eb6-495">For example:</span></span>

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

## <a name="about-metric-values"></a><span data-ttu-id="10eb6-496">메트릭 값 정보</span><span class="sxs-lookup"><span data-stu-id="10eb6-496">About metric values</span></span>
<span data-ttu-id="10eb6-497">메트릭 보고서 및 기타 다른 곳의 메트릭 값은 모두 표준 개체 구조를 사용하여 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="10eb6-498">예:</span><span class="sxs-lookup"><span data-stu-id="10eb6-498">For example:</span></span>

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

<span data-ttu-id="10eb6-499">현재는 표준 SDK 모듈에서 보고되는 모든 값 중에서 `count==1`과 `name` 및 `value` 필드만 유용합니다(향후 변경될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="10eb6-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="10eb6-500">이러한 값이 달라지는 유일한 경우는 TrackMetric 호출을 직접 작성하고 다른 매개 변수를 설정하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="10eb6-501">다른 필드의 목적은 포털로 가는 트래픽을 줄이기 위해 SDK에 메트릭이 집계되도록 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="10eb6-502">예를 들어 각 메트릭 보고서를 보내기 전에 여러 연속 판독값의 평균을 낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="10eb6-503">그런 다음 최소값, 최대값, 표준 편차 및 집계 값(합계 또는 평균)을 계산하고 개수를 보고서에서 표시한 판독값 수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="10eb6-504">위의 테이블에서는 거의 사용되지 않는 필드인 count, min, max, stdDev 및 sampledValue가 생략되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="10eb6-505">원격 분석의 양을 줄여야 하는 경우 사전 집계 메트릭 대신 [샘플링](app-insights-sampling.md) 을 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="10eb6-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="10eb6-506">기간</span><span class="sxs-lookup"><span data-stu-id="10eb6-506">Durations</span></span>
<span data-ttu-id="10eb6-507">달리 명시된 경우를 제외하고, 기간은 10분의 1 마이크로초로 표현되므로 10000000.0은 1초를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb6-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="10eb6-508">참고 항목</span><span class="sxs-lookup"><span data-stu-id="10eb6-508">See also</span></span>
* [<span data-ttu-id="10eb6-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="10eb6-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="10eb6-510">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="10eb6-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="10eb6-511">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="10eb6-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
