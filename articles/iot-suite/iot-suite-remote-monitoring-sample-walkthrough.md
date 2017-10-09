---
title: "aaaRemote 미리 구성 된 모니터링 솔루션 연습 | Microsoft Docs"
description: "Hello 미리 구성 된 Azure IoT 솔루션 원격 모니터링 및 해당 아키텍처의 설명입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>미리 구성된 원격 모니터링 솔루션 연습

원격 모니터링 IoT Suite hello [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 는에 종단 간 구현 원격 위치에서 실행 되는 여러 컴퓨터에 대 한 솔루션을 모니터링 합니다. hello 솔루션 핵심 Azure 서비스 tooprovide hello 비즈니스 시나리오의 제네릭 구현을 결합합니다. 사용자 고유의 구현에 대 한 시작 점으로 hello 솔루션을 사용할 수 있습니다 및 [사용자 지정] [ lnk-customize] 것 toomeet 특정 비즈니스 요구 사항입니다.

이 문서에서는 hello hello 원격 모니터링 솔루션 tooenable의 핵심 요소 중 일부를 통해 toounderstand 작동 방식입니다. 이 정보는 다음 항목을 도울 수 있습니다.

* Hello 솔루션의 문제를 해결 합니다.
* 계획 방법을 toocustomize toohello 솔루션 toomeet 특정 요구 사항입니다. 
* Azure 서비스를 사용하는 고유한 IoT 솔루션을 디자인합니다.

## <a name="logical-architecture"></a>논리 아키텍처

다음 다이어그램 hello hello hello 미리 구성 된 솔루션의 논리적 구성 요소를 설명 합니다.

![논리 아키텍처](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>시뮬레이션된 장치

미리 구성 하는 hello 솔루션 hello 시뮬레이션 된 장치를 냉각 장치를 (예: 건물 공조 장치 또는 시설 공기 처리 장치)를 나타냅니다. 자동으로에서 실행 되는 4 개의 시뮬레이션 된 장치를 프로 비전 hello 미리 구성 된 솔루션을 배포 하는 경우는 [Azure WebJob][lnk-webjobs]합니다. 시뮬레이션 된 hello 장치 쉽게 동작에 대 한 있습니다 tooexplore hello hello 필요 toodeploy 없이 hello 솔루션의 모든 물리적 장치 있습니다. 실제 장치 toodeploy 참조 hello [원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결] [ lnk-connect-rm] 자습서입니다.

### <a name="device-to-cloud-messages"></a>장치-클라우드 메시지

각 시뮬레이션 된 장치는 다음 메시지 유형을 tooIoT 허브 hello를 보낼 수 있습니다.

| Message | 설명 |
| --- | --- |
| 시작 |Hello 장치 시작 될 때 보냅니다는 **장치 정보** toohello 백 엔드 자체에 대 한 정보를 포함 하는 메시지입니다. 이 데이터는 hello 장치 id와 hello 명령 목록을 포함 하 고 메서드 hello 장치 지원 합니다. |
| 현재 상태 |정기적으로 전송 하는 장치는 **존재** hello 장치 센서의 hello 존재를 감지할 수 있는지 여부를 tooreport 메시지입니다. |
| 원격 분석 |정기적으로 전송 하는 장치는 **원격 분석** hello 온도 및 습도 hello 장치에서 수집에 대 한 시뮬레이션 된 값을 보고 하는 메시지의 센서를 시뮬레이션 합니다. |

> [!NOTE]
> hello 솔루션 hello hello 장치로 이중 아니라 Cosmos DB 데이터베이스에 hello 장치에서 지원 되는 명령 목록을 저장 합니다.

### <a name="properties-and-device-twins"></a>속성 및 장치 쌍

hello 시뮬레이션 된 장치 보낼 장치 속성 toohello 다음 hello [로 이중] [ lnk-device-twins] 으로 hello IoT 허브에서 *속성을 보고*합니다. hello 장치 보냅니다 보고 속성 시작 시와 응답 tooa에서 **장치 상태 변경** 명령 또는 메서드.

| 속성 | 목적 |
| --- | --- |
| Config.TelemetryInterval | 원격 분석을 전송 하는 빈도 (초) hello 장치 |
| Config.TemperatureMeanValue | 시뮬레이션 된 hello 온도 원격 분석을 위한 hello 평균 값 지정 |
| Device.DeviceID |제공 되거나 hello 솔루션에 장치를 만들 때 할당 하는 id |
| Device.DeviceState | Hello 장치에서 보고 한 상태 |
| Device.CreatedTime |시간 hello 장치 hello 솔루션에서 만들었을 |
| Device.StartupTime |시작 된 시간 hello 장치 |
| Device.LastDesiredPropertyChange |hello 마지막 원하는 속성의 hello 버전 번호 변경 |
| Device.Location.Latitude |Hello 장치의 위도 위치 |
| Device.Location.Longitude |Hello 장치의 경도 위치 |
| System.Manufacturer |장치 제조업체 |
| System.ModelNumber |Hello 장치의 모델 번호 |
| System.SerialNumber |Hello 장치의 일련 번호 |
| System.FirmwareVersion |현재 버전의 hello 장치에 펌웨어 |
| System.Platform |Hello 장치의 플랫폼 아키텍처 |
| System.Processor |실행 중인 hello 장치 프로세서 |
| System.InstalledRAM |Hello 장치에 설치 된 RAM 크기 |

hello 시뮬레이터 초기값 예제 값을 사용 하 여 시뮬레이션 된 장치에서 이러한 속성을 설정 합니다. 시뮬레이션 된 장치, hello 장치를 초기화 하는 hello 시뮬레이터 때마다 보고 된 속성으로 hello 미리 정의 된 메타 데이터 tooIoT 허브를 보고 합니다. Hello 장치에 의해 보고 된 속성을 업데이트할 수만 있습니다. 보고 속성 toochange 솔루션 포털에서 원하는 속성 설정. hello 장치를 hello 수행 됩니다.

1. 주기적으로 hello IoT 허브에서 원하는 속성을 검색 합니다.
2. 원하는 hello 속성 값으로 구성을 업데이트 합니다.
3. 보고 된 속성으로 새 값 백 toohello 허브를 hello를 보냅니다.

Hello 솔루션 대시보드에서 사용할 수 있습니다 *원하는 속성을* hello를 사용 하 여 장치에서 tooset 속성 [장치로 이중][lnk-device-twins]합니다. 일반적으로 장치는 hello 허브 tooupdate 보고 속성으로 다시 변경의 내부 상태 및 보고서 hello에서에서 원하는 속성 값을 읽습니다.

> [!NOTE]
> hello 시뮬레이션 된 장치 코드만 사용 하 여 hello **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** 원하는 속성이 tooupdate hello 보고 다시 전송 속성 tooIoT 허브입니다. Hello 시뮬레이션 된 장치에 다른 모든 원하는 속성 변경 요청은 무시 됩니다.

### <a name="methods"></a>메서드

hello 시뮬레이션 된 장치 처리할 수 있는 메서드를 다음 hello ([메서드를 직접][lnk-direct-methods]) hello IoT 허브를 통해 hello 솔루션 포털에서 호출 됩니다.

| 메서드 | 설명 |
| --- | --- |
| InitiateFirmwareUpdate |Hello 장치 tooperform 펌웨어 업데이트를 지시합니다. |
| Reboot |Hello 장치 tooreboot을 지시합니다. |
| FactoryReset |공장 기본 설정 hello 장치 tooperform을 지시 합니다. |

일부 메서드는 진행률에 tooreport 보고 속성을 사용합니다. 예를 들어 hello **InitiateFirmwareUpdate** 메서드 시뮬레이션 hello 장치에 비동기적으로 실행 중인 hello 업데이트 합니다. hello 메서드 hello 장치에 즉시 반환 hello 비동기 작업이 계속 toosend 상태 업데이트를 다시 사용 하 여 toohello 솔루션 대시보드 보고 속성.

### <a name="commands"></a>명령

시뮬레이션 된 hello 장치 hello hello IoT 허브를 통해 hello 솔루션 포털에서 전송 되는 명령을 (클라우드-장치 메시지의 경우) 다음 처리할 수 있습니다.

| 명령 | 설명 |
| --- | --- |
| PingDevice |보냅니다는 *ping* toohello 장치 toocheck 자신이 활성 상태임 |
| StartTelemetry |원격 분석 보내기 시작 hello 장치 |
| StopTelemetry |원격 분석 전송에서 중지 hello 장치 |
| ChangeSetPointTemp |난수 데이터 생성 되는 hello 주위 변경 hello 지점 설정 값 |
| DiagnosticTelemetry |트리거 hello 장치 시뮬레이터 toosend 원격 분석 추가 값 (externalTemp) |
| ChangeDeviceState |Hello 장치에 대 한 확장 된 상태 속성을 변경 하 고 hello 장치에서 hello 장치 정보 메시지를 전송 |

> [!NOTE]
> 이러한 명령(클라우드-장치 메시지) 및 메서드(직접 메서드)의 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.

## <a name="iot-hub"></a>IoT 허브

hello [IoT hub] [ lnk-iothub] hello 장치에서 hello 클라우드로 전송 되는 데이터를 수집 하 고 사용할 수 있는 toohello Azure 스트림 분석 ASA () 작업을 만듭니다. 각 스트림 ASA 작업에는 별도 IoT Hub 소비자 그룹 tooread hello 메시지 스트림을 하 여 장치에서 사용합니다.

또한 hello 솔루션에서 IoT hub를 hello:

- Hello id와 tooconnect toohello 포털을 허용 하는 모든 hello 장치 인증 키를 저장 하는 id 레지스트리에 유지 관리 합니다. 사용 및 id 레지스트리에 hello 통해 장치를 비활성화할 수 있습니다.
- Hello 솔루션 포털을 대신 하 여 명령을 tooyour 장치를 보냅니다.
- Hello 솔루션 포털을 대신 하 여 장치에 대 한 메서드를 호출합니다.
- 등록된 모든 장치에 대한 장치 쌍을 유지 관리합니다. 장치로 이중 장치에서 보고 하는 hello 속성 값을 저장 합니다. 또한 장치로 이중 hello 장치 tooretrieve 다음 연결에 대 한 hello 솔루션 포털에서 설정 하는 원하는 속성을 저장 합니다.
- 일정을 여러 장치에 대 한 tooset 속성 작업 또는 여러 장치에서 메서드를 호출 합니다.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Hello 모니터링 솔루션을 원격에 [Azure 스트림 분석] [ lnk-asa] ASA ()는 처리 또는 저장에 대 한 hello IoT 허브 tooother 백 엔드 구성 요소에서 받은 장치 메시지를 디스패치합니다. 다른 ASA 작업 hello 메시지의 hello 내용을 기반으로 하는 특정 기능을 수행 합니다.

**작업 1: 장치 정보** hello 들어오는 메시지 스트림의 장치 정보 메시지를 필터링 하 고 tooan 이벤트 허브 끝점으로 보냅니다. 시작 시와 응답 tooa에는 장치에서 장치 정보 메시지를 전송 **SendDeviceInfo** 명령입니다. 이 작업에 다음 쿼리 정의 tooidentify hello 사용 하 여 **장치 정보** 메시지:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

이 작업은 추가 처리를 위해 해당 출력 tooan 이벤트 허브를 보냅니다.

**작업 2: 규칙** 은 장치 단위 임계값에 대해 들어오는 온도 및 습도 원격 분석 값을 평가합니다. 임계값은 hello 솔루션 포털에서 사용할 수 있는 hello 규칙 편집기에서 설정 됩니다. 각 장치/값 쌍은 **참조 데이터**로서 스트림 분석에서 읽는 Blob의 타임스탬프에 의해 저장됩니다. hello 작업 hello 장치에 대 한 hello 설정한 임계값에 대 한 모든 비어 있지 않은 값을 비교합니다. Hello 초과 하는 경우 ' >' hello 작업에서 출력 조건을 **경보** hello 임계값을 나타내는 이벤트를 초과 하 고 hello 장치, 값 및 타임 스탬프 값을 제공 합니다. 이 작업 경보를 트리거해야 하는 쿼리 정의 tooidentify 원격 분석 메시지 다음 hello를 사용 합니다.

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

hello 작업의 출력 tooan 이벤트 허브 추가 처리를 위해 보내고 hello 솔루션 포털 hello 경고 정보를 읽을 수 있는에서 각 경고 tooblob 저장소의 세부 정보를 저장 합니다.

**작업 3: 원격 분석** 에 두 가지 방법으로 hello 들어오는 장치 원격 분석 스트림에 대해 작동 합니다. 먼저 hello 장기 저장에 대 한 hello 장치 toopersistent blob 저장소에서 모든 원격 분석 메시지를 보냅니다. 두 번째 hello 습도 평균, 최소 및 최대 5 분 슬라이딩 윈도우를 통해 값을이 데이터 tooblob 저장소 보냅니다를 계산 합니다. hello 솔루션 포털 blob 저장소 toopopulate hello 차트에서 hello 원격 분석 데이터를 읽습니다. 이 작업에서는 쿼리 정의 다음 hello를 사용 합니다.

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Event Hubs

hello **장치 정보** 및 **규칙** ASA 작업은 해당 데이터 tooEvent 허브 tooreliably 앞으로 toohello에 출력 **이벤트 프로세서** hello WebJob 실행 합니다.

## <a name="azure-storage"></a>Azure 저장소

hello 솔루션 hello 솔루션에서 Azure blob 저장소 toopersist hello 장치에서 모든 hello 원시 및 요약 된 원격 분석 데이터를 사용 합니다. hello 포털 blob 저장소 toopopulate hello 차트에서 hello 원격 분석 데이터를 읽습니다. toodisplay 경고 hello 솔루션 포털 데이터를 읽습니다 hello blob 저장소에서 기록 하는 원격 분석을 초과 하는 값 hello 임계값을 구성 하는 경우. 또한 hello 솔루션 hello 솔루션 포털에서 설정한 blob 저장소 toorecord hello 임계값 값을 사용 합니다.

## <a name="webjobs"></a>웹 작업

또한 toohosting hello 장치 시뮬레이터 hello WebJobs hello 솔루션에도 호스트 hello **이벤트 프로세서** 명령 응답을 처리 하는 Azure WebJob을 실행 합니다. 명령 응답 메시지 tooupdate hello 장치 명령 기록 (hello Cosmos DB 데이터베이스에 저장)를 사용 합니다.

## <a name="cosmos-db"></a>Cosmos DB

hello 솔루션 hello 장치 연결 된 toohello 솔루션에 대 한 Cosmos DB 데이터베이스 toostore 정보를 사용합니다. 이 정보 hello 솔루션 포털에서 호출 된 메서드 및 toodevices hello 솔루션 포털에서 전송 되는 명령을의 hello 히스토리가 포함 되었습니다.

## <a name="solution-portal"></a>솔루션 포털

hello 솔루션 포털은 hello 미리 구성 된 솔루션의 일부분으로 배포 하는 웹 응용 프로그램입니다. hello 솔루션 포털의 주요 페이지 hello은 hello 대시보드 및 hello 장치 목록입니다.

### <a name="dashboard"></a>대시보드

PowerBI javascript 컨트롤을 사용 하는 hello 웹 응용 프로그램에서이 페이지 (참조 [powerbi-visuals 리포지토리](https://www.github.com/Microsoft/PowerBI-visuals)) hello 장치에서 toovisualize hello 원격 분석 데이터. hello 솔루션 hello ASA 원격 분석 작업 toowrite hello 원격 분석 데이터 tooblob 저장소를 사용합니다.

### <a name="device-list"></a>장치 목록

Hello 솔루션 포털에서이 페이지에서 다음을 수행할 수 있습니다.

* 새 장치를 프로비전합니다. 이 작업 hello 고유한 장치 id를 설정 하 고 hello 인증 키를 생성 합니다. Hello 장치 tooboth hello IoT Hub id 레지스트리에 대 한 정보와 hello 솔루션 별 Cosmos DB 데이터베이스 파일을 씁니다.
* 장치 속성을 관리합니다. 이 작업은 기본 속성 보기 및 새 속성으로 업데이트를 포함합니다.
* 명령을 tooa 장치를 보냅니다.
* 장치에 대 한 hello 명령 기록을 봅니다.
* 장치를 활성화하고 비활성화합니다.

## <a name="next-steps"></a>다음 단계

hello 다음 TechNet 블로그 게시물에 대해 자세히 모니터링 미리 구성 된 솔루션 원격 hello:

* [IoT 속속들이 hello--아래 Suite 원격 모니터링](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT 도구 모음 - 원격 모니터링 - 라이브 및 시뮬레이션된 장치 추가](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Hello 다음 문서를 참조 하 여 IoT Suite를 시작 하기를 진행할 수 있습니다.

* [원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결][lnk-connect-rm]
* [Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
