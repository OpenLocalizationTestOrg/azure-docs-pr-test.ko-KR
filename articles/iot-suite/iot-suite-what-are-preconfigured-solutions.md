---
title: "aaaAzure IoT 솔루션 미리 구성 | Microsoft Docs"
description: "Azure IoT hello에 대 한 설명을 솔루션 및 해당 아키텍처 링크 tooadditional 리소스와 미리 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Hello 미리 구성 된 Azure IoT Suite 솔루션은 무엇입니까?

hello 미리 구성 된 Azure IoT Suite 솔루션은 tooAzure 구독을 사용 하 여 배포할 수 있음을 일반적인 IoT 솔루션 패턴의 구현입니다. Hello 미리 구성 된 솔루션을 사용할 수 있습니다.

* 사용자 고유의 IoT 솔루션에 대한 시작점.
* IoT 솔루션 디자인 및 개발에서 일반적인 패턴에 대 한 toolearn 합니다.

미리 구성 된 각 솔루션에 사용 하 여 장치 toogenerate 원격 분석을 시뮬레이션할 완전 한 종단 간 구현입니다.

Hello 전체 소스 코드 toocustomize 다운로드 하 고 hello 솔루션 toomeet 특정 IoT 요구 사항을 확장할 수 있습니다.

> [!NOTE]
> 솔루션을 미리 구성 된 hello의 toodeploy 하나, 방문 [Microsoft Azure IoT Suite][lnk-azureiotsuite]합니다. hello 문서 [hello 미리 구성 된 IoT 솔루션 시작] [ lnk-getstarted-preconfigured] 방법 중 하나를 실행된 하 고 toodeploy hello 솔루션에 대 한 자세한 정보를 제공 합니다.

hello 다음 표에 나와 hello 솔루션 toospecific IoT 기능:

| 해결 방법 | 데이터 수집 | 장치 ID | 장치 관리 | 명령 및 컨트롤 | 규칙 및 동작 | 예측 분석 |
| --- | --- | --- | --- | --- | --- | --- |
| [원격 모니터링][lnk-getstarted-preconfigured] |예 |예 |예 |예 |예 |- |
| [예측 유지 관리][lnk-predictive-maintenance] |예 |예 |- |예 |예 |예 |
| [연결된 공장][lnk-getstarted-factory] |예 |예 |예 |예 |예 |- |

* *데이터 수집*: toohello 클라우드 눈금에서의 데이터는 수신 합니다.
* *장치 id*: 고유한 장치 id를 관리 하 고 장치 액세스 toohello 솔루션을 제어 합니다.
* *장치 관리*: 장치 메타데이터를 관리하고 장치 재부팅 및 펌웨어 업그레이드 등의 작업을 수행합니다.
* *명령 및 제어*: toocause hello 장치 tootake 있는 동작을 hello 클라우드에서 tooa 장치 메시지를 보냅니다.
* *규칙 및 동작*: tooact hello 솔루션 백 엔드 특정 장치-클라우드 데이터에 규칙을 사용 합니다.
* *예측 분석*: hello 솔루션 백 엔드 특정 작업이 수행 해야 하는 경우 toopredict 장치-클라우드 데이터를 분석 합니다. 예를 들어 엔진 유지 관리 기간이 때 비행기 엔진 원격 분석 toodetermine를 분석 합니다.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>미리 구성된 원격 모니터링 솔루션 개요

Toodiscuss hello 다른 솔루션 공유 하는 많은 일반적인 디자인 요소에 설명 하기 때문에이 문서에서 원격 모니터링 미리 구성 된 솔루션을 hello 했습니다.

hello 다음 다이어그램에서는 hello hello 원격 모니터링 솔루션의 주요 요소입니다. hello 다음 섹션에서는 이러한 요소에 대 한 자세한 정보.

![미리 구성된 원격 모니터링 솔루션 아키텍처][img-remote-monitoring-arch]

## <a name="devices"></a>장치

Hello 원격 모니터링 미리 구성 된 솔루션을 배포 하면 4 개의 시뮬레이션 된 장치는 냉각 장치를 시뮬레이션 하는 hello 솔루션에서 사전 프로 비전 합니다. 이러한 시뮬레이션된 장치에는 원격 분석을 내보내는 기본 제공 온도 및 습도 모델이 있습니다. 이러한 시뮬레이션된 장치에 다음이 포함되어 있습니다.

- Hello 솔루션을 통해 데이터의 hello 종단 간 흐름을 보여 줍니다.
- 원격 분석의 편리한 원본을 제공합니다.
- 시작 지점으로 hello 솔루션을 사용 하 여 사용자 지정 구현에 대 한 백 엔드 개발자의 경우 대상 메서드 또는 명령에 제공 합니다.

hello 솔루션에 hello 시뮬레이션 된 장치는 클라우드-장치 통신 다음 toohello를 응답할 수 있습니다.

- *메서드 ([메서드를 직접][lnk-direct-methods])*: 여기서 연결된 된 장치는 예상된 toorespond 즉시 양방향 통신 방법입니다.
- *명령 (클라우드-장치 메시지)*: 장치에서 지 속성 큐 hello 명령을 검색 하는 단방향 통신 메서드.

서로 다른 방법에 대한 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.

장치에서 먼저 hello 미리 구성 된 솔루션의 tooIoT 허브를 연결 된 장치 정보 메시지 toohello 허브를 보냅니다. 이 메시지에 hello 장치에 응답할 수 hello 메서드를 열거 합니다. Hello 원격 미리 구성 된 솔루션 모니터링, 시뮬레이션 된 장치는 이러한 메서드를 지원 합니다.

* *펌웨어 업데이트 시작*:이 메서드는 hello 장치 tooperform 펌웨어 업데이트에는 비동기 작업을 시작 합니다. hello 비동기 작업 보고 속성 toodeliver 상태 업데이트 toohello 솔루션 대시보드를 사용합니다.
* *다시 부팅*:이 메서드를 사용 하면 장치 tooreboot hello 시뮬레이션 합니다.
* *FactoryReset*:이 메서드는 hello 시뮬레이션 된 장치에서 공장 재설정을 트리거합니다.

장치에서 먼저 hello 미리 구성 된 솔루션의 tooIoT 허브를 연결 된 장치 정보 메시지 toohello 허브를 보냅니다. 이 메시지 hello 장치에 응답할 수 hello 명령을 열거 합니다. Hello 원격 미리 구성 된 솔루션 모니터링, 시뮬레이션 된 장치는 이러한 명령을 지원 합니다.

* *Ping 장치*: hello 장치 승인을 toothis 명령에 응답 합니다. 이 명령은 해당 hello 장치는 여전히 활성 상태이 고 수신 대기를 검사 하는 것에 대 한 유용 합니다.
* *원격 분석을 시작*: hello 장치 toostart 원격 분석을 전송 하도록 지시 합니다.
* *원격 분석을 중지*: hello 장치 toostop 원격 분석을 전송 하도록 지시 합니다.
* *변경 집합 지점 온도*: 컨트롤 hello 시뮬레이션된 온도 값 hello 장치 원격 분석을 보냅니다. 이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.
* *진단 원격 분석*: hello 장치 원격 분석으로 hello 외부 온도 보내야 하는 경우를 제어 합니다.
* *장치 상태 변경*: 장치 보고서 hello 하 hello 장치 상태 메타 데이터 속성을 설정 합니다. 이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.

Hello를 생성 하는 시뮬레이션 된 장치 toohello 솔루션을 더 추가할 수 있습니다는 동일한 원격 분석 및 응답 toohello 동일한 메서드 및 명령.

또한 tooresponding toocommands 및 메서드 hello 솔루션에서는 [장치 트윈스][lnk-device-twin]합니다. 장치는 장치 트윈스 tooreport 속성 값 toohello 솔루션 백 엔드를 사용합니다. hello 솔루션 대시보드는 장치에서 장치 트윈스 tooset 원하는 toonew 속성 값을 사용합니다. 예를 들어 hello 펌웨어 업데이트 프로세스를 시뮬레이션 하는 hello 장치 보고서 중 hello의 hello 상태 업데이트 보고 속성을 사용 합니다.

## <a name="iot-hub"></a>IoT 허브

이 미리 구성 된 솔루션에서는 hello IoT Hub 인스턴스에 해당 toohello *클라우드 게이트웨이* 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.

IoT hub는 단일 끝점에서 hello 장치에서 원격 분석을 받습니다. IoT hub에 장치 관련 끝점 각 장치 tooit 전송 하는 hello 명령을 검색할 수 있는 유지 관리 합니다.

hello IoT 허브를 사용 하면 수신 hello 원격 분석 끝점 읽을 hello 서비스 측 원격 분석을 통해 사용할 수 있습니다.

IoT Hub의 hello 장치 관리 기능이 있습니다 toomanage hello 솔루션 포털 및 일정 작업에서 작업을 수행 하 여 장치 속성을 사용 하면:

- 장치 재부팅
- 장치 상태 변경
- 펌웨어 업데이트

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

hello 미리 구성 된 솔루션 사용 하 여 세 개의 [Azure 스트림 분석] [ lnk-asa] (ASA) 작업 toofilter hello 원격 분석 스트림 hello 장치에서:

* *DeviceInfo 작업* -장치 등록 별 메시지 toohello 솔루션 장치 레지스트리 경로 조정 하는 출력 데이터 tooan 이벤트 허브입니다. 이 장치 레지스트리는 Azure Cosmos DB 데이터베이스입니다. 이러한 메시지는 장치를 처음으로 연결할 때 또는 응답 tooa **장치 상태 변경** 명령입니다.
* *원격 분석 작업* -콜드 저장소에 대 한 모든 원시 원격 분석 tooAzure blob 저장소를 전송 하 고 hello 솔루션 대시보드를 표시 하는 원격 분석 집계를 계산 합니다.
* *규칙 작업* -필터 규칙 임계값을 초과 하는 값에 대 한 원격 분석 스트림을 hello 및 출력 hello 데이터 tooan 이벤트 허브입니다. 규칙을 발생 시키면 hello 솔루션 포털 대시보드 보기 hello 경보 기록 테이블에 새 행으로이 이벤트를 표시 합니다. 이러한 규칙 hello에 정의 된 hello 설정을 기반으로 작업을 트리거할 수도 **규칙** 및 **동작** hello 솔루션 포털에서 보기.

이 미리 구성 된 솔루션에서는 hello ASA 작업 toohello의 일부가 **IoT 솔루션 백 엔드** 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.

## <a name="event-processor"></a>이벤트 프로세서

이 미리 구성 된 솔루션에서는 hello 이벤트 프로세서 hello의 일부를 형성 **IoT 솔루션 백 엔드** 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.

hello **DeviceInfo** 및 **규칙** ASA 작업 보낼 배달에 대 한 해당 출력 tooEvent 허브 tooother 백 엔드 서비스입니다. hello 솔루션에서 사용 하는 [EventProcessorHost] [ lnk-event-processor] 에서 실행 중인 인스턴스는 [WebJob][lnk-web-job], 이러한 이벤트 허브에서 tooread hello 메시지입니다. hello **EventProcessorHost** 사용:
- hello **DeviceInfo** hello Cosmos DB 데이터베이스의 데이터 tooupdate hello 장치 데이터입니다.
- hello **규칙** 데이터 tooinvoke hello 논리 앱 및 업데이트 hello 경고 hello 솔루션 포털에 표시 합니다.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>장치 ID 레지스트리, 장치 쌍 및 Cosmos DB

모든 IoT Hub는 장치 키를 저장하는 [장치 ID 레지스트리][lnk-identity-registry]를 포함합니다. IoT Hub이이 정보를 사용 하 여 장치 인증-장치를 등록 해야 하 고 toohello 허브에 연결할 수 있으려면 유효한 키를 보유 합니다.

A [장치로 이중] [ lnk-device-twin] hello IoT 허브에서 관리 하는 JSON 문서입니다. 장치에 대한 장치 쌍은 다음을 포함합니다.

- Hello 장치 toohello 허브에서 보낸 보고 된 속성입니다. Hello 솔루션 포털에서 이러한 속성을 볼 수 있습니다.
- 원하는 속성을 원하는 toosend toohello 장치입니다. Hello 솔루션 포털에서 이러한 속성을 설정할 수 있습니다.
- Hello 장치에 없는 hello 장치로 이중에만 존재 하는 태그입니다. Hello 솔루션 포털에서 이러한 태그 toofilter 목록 장치를 사용할 수 있습니다.

이 솔루션에서는 장치 트윈스 toomanage 장치 메타 데이터를 사용 합니다. 또한 hello 솔루션 각 장치와 hello 명령 기록에서 지 원하는 hello 명령 같은 Cosmos DB 데이터베이스 toostore 추가 솔루션 별 장치 데이터를 사용 합니다.

또한 hello 솔루션 hello Cosmos DB 데이터베이스의 내용을 hello와 동기화 하는 hello 장치 id 레지스트리에서의 hello 정보를 유지 해야 합니다. hello **EventProcessorHost** 사용 하 여 데이터를 hello **DeviceInfo** stream analytics 작업 toomanage hello 동기화 합니다.

## <a name="solution-portal"></a>솔루션 포털

![솔루션 포털][img-dashboard]

hello 솔루션 포털은 웹 기반 UI를 hello 미리 구성 된 솔루션의 일부로 배포 된 모든 toohello 클라우드입니다. 다음을 수행할 수 있습니다.

* 대시보드에서 원격 분석 및 경보 기록을 봅니다.
* 새 장치를 프로비전합니다.
* 장치를 관리 및 모니터링합니다.
* Toospecific 장치는 명령을 보냅니다.
* 특정 장치에서 메서드를 호출합니다.
* 규칙 및 작업을 관리합니다.
* 하나 이상의 장치에서 작업 toorun를 예약 합니다.

이 미리 구성 된 솔루션에서는 hello 솔루션 포털 hello의 일부를 형성 **IoT 솔루션 백 엔드** hello의 일부인 **처리 및 비즈니스 연결** 일반적인 hello에 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.

## <a name="next-steps"></a>다음 단계

IoT 솔루션 아키텍처에 대한 자세한 내용은 [Microsoft Azure IoT 서비스: 참조 아키텍처][lnk-refarch]를 참조하세요.

이제 미리 구성 된 솔루션은 hello를 배포 하 여 시작할 수 있습니다 *원격 모니터링* 솔루션 미리 구성 된: [hello 미리 구성 된 솔루션 시작] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
