---
title: "aaaUnderstand Azure IoT 허브 작업 | Microsoft Docs"
description: "개발자 가이드-여러 장치에서 작업 toorun 예약 tooyour IoT 허브를 연결 합니다. 작업은 태그와 원하는 속성을 업데이트하고 여러 장치에서 직접 메서드를 호출할 수 있습니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>여러 장치에서 작업 예약
## <a name="overview"></a>개요
이전 문서에 설명된 대로, Azure IoT Hub를 통해 다양한 구성 요소([장치 쌍 속성 및 태그][lnk-twin-devguide] 및 [직접 메서드][lnk-dev-methods])를 사용할 수 있습니다.  일반적으로 백 엔드 응용 프로그램 장치 관리자 및 운영자 tooupdate를 사용 하도록 설정 하 고 IoT 장치를 대량 및 예약된 된 시간에 상호 작용 합니다.  작업 일정 시간에는 장치로 이중 업데이트 및 일련의 장치에 대해 직접 메서드 hello 실행을 캡슐화합니다.  예를 들어 운영자는 시작 및 작업 tooreboot 43 및 3 층 hello 건물의 중단 toohello 작업 되지 않은 한 번에 빌드 장치 집합을 추적 하는 백 엔드 응용 프로그램을 사용 합니다.

### <a name="when-toouse"></a>때 toouse
고려 될 경우 작업을 사용 하 여: 솔루션 백 엔드 요구 tooschedule 및 추적 진행 hello 활동 장치 집합에서 다음 중 하나:

* desired 속성 업데이트
* tags 업데이트
* 직접 메서드 호출

## <a name="job-lifecycle"></a>작업 수명 주기
작업은 hello 솔루션 백 엔드에 의해 시작 되 고 IoT 허브에 의해 유지 관리 합니다.  서비스 지향 URI(`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`)를 통해 작업을 시작하고 서비스 지향 URI(`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`)를 통해 작업 실행 진행 상태를 쿼리할 수 있습니다.  작업이 시작 되 면 작업에 대 한 쿼리 실행 중인 작업의 hello 백 엔드 앱 toorefresh hello 상태를 있습니다.

> [!NOTE]
> 작업을 시작 하면 속성 이름 및 값만 포함 될 수 있습니다 US-ASCII 인쇄 가능한 hello 관계 집합에서 제외 하 고 영숫자: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``합니다.
> 
> 

## <a name="reference-topics"></a>참조 항목:
다음 참조 항목 hello 작업을 사용 하는 방법에 대 한 자세한 정보를 제공 합니다.

## <a name="jobs-tooexecute-direct-methods"></a>작업 tooexecute 직접 메서드
hello 다음은를 실행 하기 위한 HTTP 1.1 hello 요청 세부 정보는 [직접적인 방법] [ lnk-dev-methods] 일련의 작업을 사용 하는 장치에서:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
hello 쿼리 조건이 수도 있습니다는 단일 장치 Id 또는 장치 Id 목록에서 아래와 같이

**예**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IoT Hub 쿼리 언어][lnk-query]는 추가 세부 정보에서 IoT Hub 쿼리 언어를 설명합니다.

## <a name="jobs-tooupdate-device-twin-properties"></a>작업 tooupdate 장치로 이중 속성
hello 다음은 작업을 사용 하는 장치로 이중 속성을 업데이트 하기 위한 HTTP 1.1 hello 요청 세부 정보:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>작업 진행 상태 쿼리
hello 다음은 hello에 대 한 HTTP 1.1 요청 정보 [작업에 대 한 쿼리][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

hello continuationToken hello 응답에서 제공 됩니다.  

## <a name="jobs-properties"></a>작업 속성
hello 다음은 속성 및 작업 또는 작업 결과 쿼리할 때 사용할 수 있는 해당 설명의 목록입니다.

| 속성 | 설명 |
| --- | --- |
| **jobId** |Hello 작업에 대 한 ID를 제공 하는 응용 프로그램. |
| **startTime** |Hello 작업에 대 한 제공 된 응용 프로그램 시작 시간 (ISO 8601)입니다. |
| **endTime** |IoT Hub hello 작업 완료에 대 한 날짜 (ISO 8601)을 제공 합니다. Hello 작업에는 '완료' hello 상태에 도달한 후에 유효 합니다. |
| **type** |작업 형식: |
| **scheduledUpdateTwin**: 사용 작업 tooupdate 원하는 속성 또는 태그의 집합입니다. | |
| **scheduledDeviceMethod**: 사용 작업 tooinvoke 장치 트윈스 집합이 장치 메서드. | |
| **상태** |Hello 작업의 현재 상태입니다. 가능한 상태 값: |
| **보류 중인** : 예약 하 고 대기 toobe hello 작업 서비스에 의해 선택 합니다. | |
| **예약 된** : 시간 보다 이후 hello에 예약 합니다. | |
| **실행 중** : 현재 활성 상태의 작업입니다. | |
| **취소됨** : 작업이 취소되었습니다. | |
| **실패함** : 작업이 실패했습니다. | |
| **완료됨** : 작업이 완료되었습니다. | |
| **deviceJobStatistics** |Hello 작업의 실행에 대 한 통계입니다. |

**deviceJobStatistics** 속성입니다.

| 속성 | 설명 |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Hello 작업에는 장치 수입니다. |
| **deviceJobStatistics.failedCount** |Hello 작업에 실패 하는 장치 수입니다. |
| **deviceJobStatistics.succeededCount** |여기서 hello 작업이 성공적으로 수행 하는 장치 수입니다. |
| **deviceJobStatistics.runningCount** |Hello 작업이 현재 실행 중인 장치 수입니다. |
| **deviceJobStatistics.pendingCount** |Toorun hello 작업이 보류 중인 장치 수입니다. |

### <a name="additional-reference-material"></a>추가 참조 자료
Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* [제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.
* [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록에는 다양 한 언어 Sdk hello IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용 합니다.
* [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 합니다.
* [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.

* [작업 예약 및 브로드캐스트][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
