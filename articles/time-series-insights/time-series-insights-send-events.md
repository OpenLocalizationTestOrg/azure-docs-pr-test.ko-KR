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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>이벤트 허브를 사용 하 여 이벤트 tooa 시간 계열 Insights 환경 보내기

이 자습서에 설명 어떻게 toocreate 이벤트 허브를 구성 하 고 샘플 응용 프로그램 toopush 이벤트를 실행 합니다. JSON 형식의 이벤트가 있는 기존 이벤트 허브가 있는 경우 이 자습서를 건너뛰고 [시계열 정보](https://insights.timeseries.azure.com)에서 환경을 봅니다.

## <a name="configure-an-event-hub"></a>이벤트 허브 구성
1. 이벤트 허브 toocreate hello 이벤트 허브에서에서 지침에 따라 [설명서](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)합니다.

2. Time Series Insights 이벤트 원본에서 단독으로 사용하는 소비자 그룹을 만들어야 합니다.

  > [!IMPORTANT]
  > 이 소비자 그룹을 다른 서비스(예: Stream Analytics 작업 또는 다른 Time Series Insights 환경)에서 사용하지 못하게 합니다. 소비자 그룹은 다른 서비스에서 사용 되 면 작업은이 환경에 대 한 부정적인 영향을 읽고 다른 서비스 hello 합니다. "$Default" hello 소비자 그룹을 사용 하는 경우 toopotential 다시 사용할 수 있도록 다른 판독기에서 발생할 수 있습니다.

  ![이벤트 허브 소비자 그룹 선택](media/send-events/consumer-group.png)

3. Hello 이벤트 허브에서 만들 "MySendPolicy" hello csharp 샘플에서 toosend 사용 되는 이벤트입니다.

  ![공유 액세스 정책을 선택하고 추가 단추 클릭](media/send-events/shared-access-policy.png)  

  ![새 공유 액세스 정책 추가](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Time Series Insights 이벤트 원본 만들기
1. 이벤트 소스를 만들지 않은 경우에 따라 [이러한 지침](time-series-insights-add-event-source.md) toocreate 이벤트 소스입니다.

2. "DeviceTimestamp" hello 타임 스탬프 속성 이름으로 지정-hello csharp 샘플에서 실제 timestamp 안녕으로이 속성을 사용 합니다. hello 타임 스탬프 속성 이름은 대/소문자 구분이 고 값 hello 형식을 따라야 합니다. __yyyy-m M-ddTHH:mm:ss 합니다. FFFFFFFK__ JSON tooevent 허브로 전송 합니다. Hello 속성이 hello 이벤트에 존재 하지 않을 경우 다음 hello 이벤트 허브 큐에 대기 된 시간이 사용 됩니다.

  ![이벤트 원본 만들기](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>샘플 코드 toopush 이벤트
1. Toohello 이벤트 허브 정책 "MySendPolicy" 이동한 다음 hello 정책 키를 사용 하 여 hello 연결 문자열을 복사 합니다.

  ![MySendPolicy 연결 문자열 복사](media/send-events/sample-code-connection-string.png)

2. Hello 코드 다음 각각의 세 hello 장치 당 해당 toosend 600 이벤트를 실행 합니다. 연결 문자열로 `eventHubConnectionString`을 업데이트합니다.

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
## <a name="supported-json-shapes"></a>지원되는 JSON 셰이프
### <a name="sample-1"></a>샘플 1

#### <a name="input"></a>입력

간단한 JSON 개체입니다.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>출력 - 1개 이벤트

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>샘플 2

#### <a name="input"></a>입력
두 JSON 개체가 포함된 JSON 배열입니다. 각 JSON 개체에는 변환 된 tooan 이벤트 수 있습니다.
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
#### <a name="output---2-events"></a>출력 - 2개 이벤트

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>샘플 3

#### <a name="input"></a>입력

두 JSON 개체가 들어 있는 중첩된 JSON 배열이 포함된 JSON 개체입니다.
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
#### <a name="output---2-events"></a>출력 - 2개 이벤트
참고 해당 hello 속성 "위치" hello 이벤트의 tooeach 복사 됩니다.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>샘플 4

#### <a name="input"></a>입력

두 JSON 개체가 들어 있는 중첩된 JSON 배열이 포함된 JSON 개체입니다. 이 입력 hello 전역 속성 hello 복합 JSON 개체에 의해 표시 될 수 있습니다 하는 방법을 보여 줍니다.

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
#### <a name="output---2-events"></a>출력 - 2개 이벤트

|위치|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.type|events.data.type|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>다음 단계

* [Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기
