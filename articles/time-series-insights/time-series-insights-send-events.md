---
title: "aaaSend 이벤트 tooAzure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 hello 단계 toopush 이벤트 tooyour 시간 계열 Insights 환경"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="770b1-103">이벤트 허브를 사용 하 여 이벤트 tooa 시간 계열 Insights 환경 보내기</span><span class="sxs-lookup"><span data-stu-id="770b1-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="770b1-104">이 자습서에 설명 어떻게 toocreate 이벤트 허브를 구성 하 고 샘플 응용 프로그램 toopush 이벤트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="770b1-105">JSON 형식의 이벤트가 있는 기존 이벤트 허브가 있는 경우 이 자습서를 건너뛰고 [시계열 정보](https://insights.timeseries.azure.com)에서 환경을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="770b1-106">이벤트 허브 구성</span><span class="sxs-lookup"><span data-stu-id="770b1-106">Configure an event hub</span></span>
1. <span data-ttu-id="770b1-107">이벤트 허브 toocreate hello 이벤트 허브에서에서 지침에 따라 [설명서](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="770b1-108">Time Series Insights 이벤트 원본에서 단독으로 사용하는 소비자 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="770b1-109">이 소비자 그룹을 다른 서비스(예: Stream Analytics 작업 또는 다른 Time Series Insights 환경)에서 사용하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="770b1-110">소비자 그룹은 다른 서비스에서 사용 되 면 작업은이 환경에 대 한 부정적인 영향을 읽고 다른 서비스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="770b1-111">"$Default" hello 소비자 그룹을 사용 하는 경우 toopotential 다시 사용할 수 있도록 다른 판독기에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![이벤트 허브 소비자 그룹 선택](media/send-events/consumer-group.png)

3. <span data-ttu-id="770b1-113">Hello 이벤트 허브에서 만들 "MySendPolicy" hello csharp 샘플에서 toosend 사용 되는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![공유 액세스 정책을 선택하고 추가 단추 클릭](media/send-events/shared-access-policy.png)  

  ![새 공유 액세스 정책 추가](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="770b1-116">Time Series Insights 이벤트 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="770b1-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="770b1-117">이벤트 소스를 만들지 않은 경우에 따라 [이러한 지침](time-series-insights-add-event-source.md) toocreate 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="770b1-118">"DeviceTimestamp" hello 타임 스탬프 속성 이름으로 지정-hello csharp 샘플에서 실제 timestamp 안녕으로이 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="770b1-119">hello 타임 스탬프 속성 이름은 대/소문자 구분이 고 값 hello 형식을 따라야 합니다. __yyyy-m M-ddTHH:mm:ss 합니다. FFFFFFFK__ JSON tooevent 허브로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="770b1-120">Hello 속성이 hello 이벤트에 존재 하지 않을 경우 다음 hello 이벤트 허브 큐에 대기 된 시간이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![이벤트 원본 만들기](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="770b1-122">샘플 코드 toopush 이벤트</span><span class="sxs-lookup"><span data-stu-id="770b1-122">Sample code toopush events</span></span>
1. <span data-ttu-id="770b1-123">Toohello 이벤트 허브 정책 "MySendPolicy" 이동한 다음 hello 정책 키를 사용 하 여 hello 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![MySendPolicy 연결 문자열 복사](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="770b1-125">Hello 코드 다음 각각의 세 hello 장치 당 해당 toosend 600 이벤트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="770b1-126">연결 문자열로 `eventHubConnectionString`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="770b1-127">지원되는 JSON 셰이프</span><span class="sxs-lookup"><span data-stu-id="770b1-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="770b1-128">샘플 1</span><span class="sxs-lookup"><span data-stu-id="770b1-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="770b1-129">입력</span><span class="sxs-lookup"><span data-stu-id="770b1-129">Input</span></span>

<span data-ttu-id="770b1-130">간단한 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="770b1-131">출력 - 1개 이벤트</span><span class="sxs-lookup"><span data-stu-id="770b1-131">Output - 1 event</span></span>

|<span data-ttu-id="770b1-132">id</span><span class="sxs-lookup"><span data-stu-id="770b1-132">id</span></span>|<span data-ttu-id="770b1-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="770b1-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="770b1-134">device1</span><span class="sxs-lookup"><span data-stu-id="770b1-134">device1</span></span>|<span data-ttu-id="770b1-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="770b1-136">샘플 2</span><span class="sxs-lookup"><span data-stu-id="770b1-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="770b1-137">입력</span><span class="sxs-lookup"><span data-stu-id="770b1-137">Input</span></span>
<span data-ttu-id="770b1-138">두 JSON 개체가 포함된 JSON 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="770b1-139">각 JSON 개체에는 변환 된 tooan 이벤트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-139">Each JSON object will be converted tooan event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="770b1-140">출력 - 2개 이벤트</span><span class="sxs-lookup"><span data-stu-id="770b1-140">Output - 2 Events</span></span>

|<span data-ttu-id="770b1-141">id</span><span class="sxs-lookup"><span data-stu-id="770b1-141">id</span></span>|<span data-ttu-id="770b1-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="770b1-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="770b1-143">device1</span><span class="sxs-lookup"><span data-stu-id="770b1-143">device1</span></span>|<span data-ttu-id="770b1-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="770b1-145">device2</span><span class="sxs-lookup"><span data-stu-id="770b1-145">device2</span></span>|<span data-ttu-id="770b1-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="770b1-147">샘플 3</span><span class="sxs-lookup"><span data-stu-id="770b1-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="770b1-148">입력</span><span class="sxs-lookup"><span data-stu-id="770b1-148">Input</span></span>

<span data-ttu-id="770b1-149">두 JSON 개체가 들어 있는 중첩된 JSON 배열이 포함된 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="770b1-150">출력 - 2개 이벤트</span><span class="sxs-lookup"><span data-stu-id="770b1-150">Output - 2 Events</span></span>
<span data-ttu-id="770b1-151">참고 해당 hello 속성 "위치" hello 이벤트의 tooeach 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="770b1-152">location</span><span class="sxs-lookup"><span data-stu-id="770b1-152">location</span></span>|<span data-ttu-id="770b1-153">events.id</span><span class="sxs-lookup"><span data-stu-id="770b1-153">events.id</span></span>|<span data-ttu-id="770b1-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="770b1-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="770b1-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="770b1-155">WestUs</span></span>|<span data-ttu-id="770b1-156">device1</span><span class="sxs-lookup"><span data-stu-id="770b1-156">device1</span></span>|<span data-ttu-id="770b1-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="770b1-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="770b1-158">WestUs</span></span>|<span data-ttu-id="770b1-159">device2</span><span class="sxs-lookup"><span data-stu-id="770b1-159">device2</span></span>|<span data-ttu-id="770b1-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="770b1-161">샘플 4</span><span class="sxs-lookup"><span data-stu-id="770b1-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="770b1-162">입력</span><span class="sxs-lookup"><span data-stu-id="770b1-162">Input</span></span>

<span data-ttu-id="770b1-163">두 JSON 개체가 들어 있는 중첩된 JSON 배열이 포함된 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="770b1-164">이 입력 hello 전역 속성 hello 복합 JSON 개체에 의해 표시 될 수 있습니다 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="770b1-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="770b1-165">출력 - 2개 이벤트</span><span class="sxs-lookup"><span data-stu-id="770b1-165">Output - 2 Events</span></span>

|<span data-ttu-id="770b1-166">위치</span><span class="sxs-lookup"><span data-stu-id="770b1-166">location</span></span>|<span data-ttu-id="770b1-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="770b1-167">manufacturer.name</span></span>|<span data-ttu-id="770b1-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="770b1-168">manufacturer.location</span></span>|<span data-ttu-id="770b1-169">events.id</span><span class="sxs-lookup"><span data-stu-id="770b1-169">events.id</span></span>|<span data-ttu-id="770b1-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="770b1-170">events.timestamp</span></span>|<span data-ttu-id="770b1-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="770b1-171">events.data.type</span></span>|<span data-ttu-id="770b1-172">events.data.type</span><span class="sxs-lookup"><span data-stu-id="770b1-172">events.data.units</span></span>|<span data-ttu-id="770b1-173">events.data.type</span><span class="sxs-lookup"><span data-stu-id="770b1-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="770b1-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="770b1-174">WestUs</span></span>|<span data-ttu-id="770b1-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="770b1-175">manufacturer1</span></span>|<span data-ttu-id="770b1-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="770b1-176">EastUs</span></span>|<span data-ttu-id="770b1-177">device1</span><span class="sxs-lookup"><span data-stu-id="770b1-177">device1</span></span>|<span data-ttu-id="770b1-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="770b1-179">pressure</span><span class="sxs-lookup"><span data-stu-id="770b1-179">pressure</span></span>|<span data-ttu-id="770b1-180">psi</span><span class="sxs-lookup"><span data-stu-id="770b1-180">psi</span></span>|<span data-ttu-id="770b1-181">108.09</span><span class="sxs-lookup"><span data-stu-id="770b1-181">108.09</span></span>|
|<span data-ttu-id="770b1-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="770b1-182">WestUs</span></span>|<span data-ttu-id="770b1-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="770b1-183">manufacturer1</span></span>|<span data-ttu-id="770b1-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="770b1-184">EastUs</span></span>|<span data-ttu-id="770b1-185">device2</span><span class="sxs-lookup"><span data-stu-id="770b1-185">device2</span></span>|<span data-ttu-id="770b1-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="770b1-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="770b1-187">vibration</span><span class="sxs-lookup"><span data-stu-id="770b1-187">vibration</span></span>|<span data-ttu-id="770b1-188">abs G</span><span class="sxs-lookup"><span data-stu-id="770b1-188">abs G</span></span>|<span data-ttu-id="770b1-189">217.09</span><span class="sxs-lookup"><span data-stu-id="770b1-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="770b1-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="770b1-190">Next steps</span></span>

* <span data-ttu-id="770b1-191">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기</span><span class="sxs-lookup"><span data-stu-id="770b1-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
