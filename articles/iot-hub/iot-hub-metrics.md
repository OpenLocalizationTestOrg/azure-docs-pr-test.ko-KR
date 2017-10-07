---
title: "Azure IoT Hub aaaUse 메트릭 toomonitor | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 메트릭 tooassess 및 모니터 hello IoT hub의 전반적인 상태입니다."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>IoT Hub 메트릭 이해
IoT Hub 메트릭 Azure 구독에서 hello Azure IoT 리소스의 hello 상태에 대 한 더 나은 데이터를 제공합니다. IoT Hub 메트릭을 사용 하면 tooassess hello hello 장치와 hello IoT 허브 서비스의 전반적인 상태 tooit을 연결 합니다. 사용자 용 통계는 진행 상황 IoT hub 및 도움말 근본 원인 문제 toocontact Azure 지원 필요 없이 참조 수 있기 때문에 중요 합니다.

메트릭은 기본적으로 사용하도록 설정됩니다. Hello Azure 포털에서에서 IoT Hub 메트릭을 볼 수 있습니다.

## <a name="how-tooview-iot-hub-metrics"></a>어떻게 tooview IoT Hub 메트릭
1. IoT Hub를 만듭니다. 방법에 지침을 찾을 수 toocreate hello에서 IoT hub [시작] [ lnk-get-started] 가이드입니다.
2. IoT hub의 hello 블레이드를 엽니다. 여기서 **메트릭**을 클릭합니다.
   
    ![][1]
3. Hello 메트릭 블레이드에서 IoT 허브에 대 한 hello 메트릭을 볼 하 고 메트릭을 사용자 지정 보기를 만들 수 있습니다. 메트릭 데이터 tooan 이벤트 허브 끝점 또는 Azure 저장소 계정을 클릭 하 여 toosend을 선택할 수 **진단 설정을**합니다.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>IoT Hub 메트릭 및 방법을 toouse에
IoT Hub에는 여러 가지 메트릭을 제공 합니다. 연결 된 장치 toogive 있습니다 허브 및 hello hello 상태에 대해 간략하게 총 수입니다. 여러 메트릭 toopaint hello IoT 허브 hello 상태의 큰 그림에서에서 정보를 결합할 수 있습니다. 상태 IoT hub hello 각 메트릭에 toohello 전체 연결 하는 방법 및 다음 표에 hello hello 메트릭을 추적 하는 각 IoT 허브를 설명 합니다.

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|원격 분석 메시지 보내기 시도|개수|합계|Tooyour IoT 허브를 전송 하는 원격 분석 장치-클라우드 메시지 시도한 toobe의 수|
|d2c.telemetry.ingress.success|보낸 원격 분석 메시지|개수|합계|원격 분석 장치-클라우드 메시지 수가 성공적으로 보낸 tooyour IoT 허브|
|c2d.commands.egress.complete.success|완료된 명령|개수|합계|클라우드-장치 명령 hello 장치에 의해 완료 수입니다.|
|c2d.commands.egress.abandon.success|중단된 명령|개수|합계|Hello 장치에 의해 중단 된 클라우드-장치 명령 수입니다.|
|c2d.commands.egress.reject.success|거부된 명령|개수|합계|Hello 장치에 의해 거부 클라우드-장치 명령 수입니다.|
|devices.totalDevices|총 장치|개수|합계|Tooyour IoT 허브 등록 된 장치 수|
|devices.connectedDevices.allProtocol|연결된 장치|개수|합계|Tooyour IoT 허브를 연결 된 장치 수|
|d2c.telemetry.egress.success|배달된 원격 분석 메시지|개수|합계|메시지 tooendpoints (합계)을 성공적으로 작성 된 횟수|
|d2c.telemetry.egress.dropped|삭제된 메시지|개수|합계|모든 경로 일치 하지 않아 및 hello 대체 경로 사용할 수 있으므로 삭제 된 메시지 수|
|d2c.telemetry.egress.orphaned|분리된 메시지|개수|합계|hello 메시지의 수 hello 대체 경로 포함 하 여 모든 경로 일치 하지 않습니다|
|d2c.telemetry.egress.invalid|잘못된 메시지|개수|합계|hello 메시지의 수 배달 되지 인해 tooincompatibility hello 끝점과|
|d2c.telemetry.egress.fallback|대체(fallback) 조건과 일치하는 메시지|개수|합계|대체 끝점 toohello 작성 된 메시지 수|
|d2c.endpoints.egress.eventHubs|메시지가 배달 tooEvent 허브 끝점|개수|합계|메시지가 성공적으로 작성 된 tooEvent 허브 끝점 된 횟수|
|d2c.endpoints.latency.eventHubs|이벤트 허브 끝점에 대한 메시지 대기 시간|밀리초|평균|밀리초에서의 이벤트 허브 끝점으로 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.serviceBusQueues|메시지가 배달 tooService 버스 큐 끝점|개수|합계|메시지 버스 큐 끝점 tooService 성공적으로 작성된 된 횟수|
|d2c.endpoints.latency.serviceBusQueues|Service Bus 큐 끝점에 대한 메시지 대기 시간|밀리초|평균|시간 (밀리초)에 있는 서비스 버스 큐 끝점에 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.serviceBusTopics|메시지가 배달 tooService 버스 항목 끝점|개수|합계|메시지 버스 항목 끝점 성공적으로 작성 된 tooService 된 횟수|
|d2c.endpoints.latency.serviceBusTopics|Service Bus 항목 끝점에 대한 메시지 대기 시간|밀리초|평균|시간 (밀리초)에 있는 서비스 버스 주제 끝점에 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.builtIn.events|메시지가 배달 toohello 기본 제공 끝점 (메시지/이벤트)|개수|합계|메시지가 성공적으로 작성 된 toohello 기본 제공 끝점 (메시지/이벤트) 된 횟수|
|d2c.endpoints.latency.builtIn.events|Hello 기본 제공 끝점 (메시지/이벤트)에 대 한 메시지 대기 시간|밀리초|평균|hello 평균 대기 시간 메시지 수신 toohello IoT hub 및 메시지 수신 사이의 밀리초에서 hello 기본 제공 끝점 (메시지/이벤트) |
|d2c.twin.read.success|장치에서의 성공한 쌍 읽기|개수|합계|성공한 모든 장치에서 시작한로 이중 hello 수를 읽습니다.|
|d2c.twin.read.failure|장치에서의 실패한 쌍 읽기|개수|합계|모든의 hello 개수 장치 시작로 이중 읽기 실패 했습니다.|
|d2c.twin.read.size|장치에서의 쌍 읽기 응답 크기|바이트|평균|hello average, min, 및 최대 성공한 모든 장치에서 시작한로 이중 읽습니다.|
|d2c.twin.update.success|장치에서의 성공한 쌍 업데이트|개수|합계|성공한 모든 장치에서 시작한로 이중 업데이트 hello 수입니다.|
|d2c.twin.update.failure|장치에서의 실패한 쌍 업데이트|개수|합계|hello 수가 모두로 이중 장치에서 시작 된 업데이트에 실패 했습니다.|
|d2c.twin.update.size|장치에서의 쌍 업데이트 크기|바이트|평균|hello 평균, 최소값, 및 성공한 모든의 최대 크기 장치 시작로 이중 업데이트 합니다.|
|c2d.methods.success|성공한 직접 메서드 호출|개수|합계|성공한 모든 직접 메서드 호출의 hello 수입니다.|
|c2d.methods.failure|실패한 직접 메서드 호출|개수|합계|모든의 hello 개수 직접 메서드 호출에 실패 했습니다.|
|c2d.methods.requestSize|직접 메서드 호출의 요청 크기|바이트|평균|hello 평균, 최소 및 최대 성공한 모든 메서드가 요청에 전달 합니다.|
|c2d.methods.responseSize|직접 메서드 호출의 응답 크기|바이트|평균|hello average, min, 및 성공적인 직접적인 방법에 대 한 모든 응답의 최대값입니다.|
|c2d.twin.read.success|백 엔드에서의 성공한 쌍 읽기|개수|합계|성공한 모든 백 엔드 시작로 이중 hello 수를 읽습니다.|
|c2d.twin.read.failure|백 엔드에서의 실패한 쌍 읽기|개수|합계|모든의 hello 개수 읽기로 이중 백 엔드 시작 실패 했습니다.|
|c2d.twin.read.size|백 엔드에서의 쌍 읽기 응답 크기|바이트|평균|hello average, min, 및 최대 성공한 모든 백 엔드 시작로 이중 읽습니다.|
|c2d.twin.update.success|백 엔드에서의 성공한 쌍 업데이트|개수|합계|성공한 모든로 이중 백 엔드 시작 업데이트의 hello 수입니다.|
|c2d.twin.update.failure|백 엔드에서의 실패한 쌍 업데이트|개수|합계|모든의 hello 개수로 이중 백 엔드 시작 된 업데이트에 실패 했습니다.|
|c2d.twin.update.size|백 엔드에서의 쌍 업데이트 크기|바이트|평균|hello average, min, 및 성공한 모든의 최대 크기 백 엔드 시작로 이중 업데이트 합니다.|
|twinQueries.success|성공한 쌍 쿼리|개수|합계|모든 성공적인로 이중 쿼리의 hello 수입니다.|
|twinQueries.failure|실패한 쌍 쿼리|개수|합계|모든 실패 한로 이중 쿼리의 hello 수입니다.|
|twinQueries.resultSize|쌍 쿼리 결과 크기|바이트|평균|hello average, min, 및 모든 성공적인로 이중 쿼리의 hello 결과 크기의 최대값입니다.|
|jobs.createTwinUpdateJob.success|쌍 업데이트 작업에 대한 성공한 만들기|개수|합계|hello 모든 성공적으로 만드는 이중 업데이트 작업의 수입니다.|
|jobs.createTwinUpdateJob.failure|쌍 업데이트 작업에 대한 실패한 만들기|개수|합계|실패 한 모두로 이중 업데이트 작업 만들기의 hello 수입니다.|
|jobs.createDirectMethodJob.success|메서드 호출 작업에 대한 성공한 만들기|개수|합계|직접 메서드 호출 작업의 모든 성공적으로 만드는 hello 수입니다.|
|jobs.createDirectMethodJob.failure|실패한 메서드 호출 작업 만들기|개수|합계|직접 메서드 호출 작업의 모든 실패 한 만들기의 hello 수입니다.|
|jobs.listJobs.success|성공한 호출 toolist 작업|개수|합계|모든 호출이 성공 toolist 작업의 hello 수입니다.|
|jobs.listJobs.failure|실패 한 호출 toolist 작업|개수|합계|모든 실패 한 호출 toolist 작업의 hello 수입니다.|
|jobs.cancelJob.success|성공한 작업 취소|개수|합계|성공한 모든 hello 수 toocancel 작업을 호출합니다.|
|jobs.cancelJob.failure|실패한 작업 취소|개수|합계|모든 실패 한 호출 toocancel 작업의 hello 수입니다.|
|jobs.queryJobs.success|성공한 작업 쿼리|개수|합계|모든 호출이 성공 tooquery 작업의 hello 수입니다.|
|jobs.queryJobs.failure|실패한 작업 쿼리|개수|합계|모든 실패 한 호출 tooquery 작업의 hello 수입니다.|
|jobs.completed|완료된 작업|개수|합계|모든 완료 된 작업의 hello 수입니다.|
|jobs.failed|실패한 작업|개수|합계|모든 실패 한 작업의 hello 수입니다.|

## <a name="next-steps"></a>다음 단계
IoT Hub 메트릭에 대 한 개요를 살펴보았으므로 이제 Azure IoT Hub를 관리 하는 방법에 대 한 자세한 링크 toolearn이를 수행 합니다.

* [작업 모니터링][lnk-monitor]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
