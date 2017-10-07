---
title: "Azure IoT Hub aaaUnderstand 메서드를 직접 | Microsoft Docs"
description: "개발자 가이드-서비스 응용 프로그램에서 사용자 장치에서 사용 가능한 메서드를 직접 tooinvoke 코드입니다."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>IoT Hub의 직접 메서드 호출 및 이해
## <a name="overview"></a>개요
IoT Hub hello 클라우드에서 장치에서 기능 tooinvoke 직접 메서드를 제공합니다. 직접 메서드 HTTP 호출 한다는 점에서 성공 하거나 실패 (직후 사용자가 지정한 시간 제한)은 장치 비슷한 tooan와 요청-회신 상호 작용을 나타냅니다. 즉각적인 동작이 hello 과정은 hello 장치는 장치가 오프 라인 (SMS 되 고 메서드 호출에 비해) 이면 SMS 절전 tooa 장치를 보내는 것과 같은 수 toorespond 했는지 여부에 따라 서로 다른 시나리오에 유용 합니다.

각 장치 메서드는 단일 장치를 대상으로 합니다. [작업] [ lnk-devguide-jobs] 여러 장치에서 방식으로 tooinvoke 직접 메서드를 제공 하 고 연결 되지 않은 장치에 대 한 메서드 호출을 예약 합니다.

IoT Hub에 **서비스 연결** 권한만 있다면 누구든 장치에서 메서드를 호출할 수 있습니다.

### <a name="when-toouse"></a>때 toouse
직접 메서드는 요청-응답 패턴을 따릅니다 하며 해당 결과 팬에 tooturn 예를 들어 hello 장치의 일반적으로 대화형 제어의 즉시 확인 해야 하는 통신을 위해 제공 됩니다.

너무 참조[클라우드-장치 통신 지침] [ lnk-c2d-guidance] 원하는 속성을 사용 하 여 간의 의문이 있는 경우 메서드나 클라우드-장치 메시지를 직접 합니다.

## <a name="method-lifecycle"></a>메서드 수명 주기
직접 메서드 hello 장치에서 구현 되 고 0이 필요할 수 있습니다 또는 hello 메서드 페이로드 toocorrectly에 많은 입력 인스턴스화합니다. 직접 메서드는 서비스 지향 URI를 통해 호출합니다(`{iot hub}/twins/{device id}/methods/`). 장치는 장치별 MQTT 토픽을 통해 직접 메서드를 수신합니다(`$iothub/methods/POST/{method name}/`). Hello 앞에 추가 장치 측 네트워킹 프로토콜에 직접 메서드 지원 될 수 있습니다.

> [!NOTE]
> 장치에서 직접 메서드를 호출 하는 경우 속성 이름 및 값만 포함 될 수 있습니다 US-ASCII 인쇄 가능한 hello 관계 집합에서 제외 하 고 영숫자: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``합니다.
> 
> 

메서드는 동기적 이며 성공 하거나 직접 hello 제한 시간 후에 실패 하거나 (기본값: 30 초 이며 too3600 초를 설정할 수 있음). 직접 메서드는 저장할 장치 tooact hello 장치는 휴대폰에서 빛 설정 등 온라인 상태이 고 받는 명령 하는 경우에 대화형 시나리오에서 유용 합니다. 이러한 시나리오에서 원하는 toosee 즉시 성공 또는 실패 여부는 hello 클라우드 서비스 hello 결과 대해 가능한 한 빨리 작동할 수 있도록 합니다. hello 장치 일부 메시지 본문이 hello 메서드의 결과로 반환할 수 있지만 hello 메서드 toodo에 필요한 하도록 합니다. 메서드 호출의 순서 지정 또는 동시성 의미 체계에 대한 보장은 없습니다.

직접적인 방법 hello 클라우드 측면에서 HTTP 전용 hello 장치 쪽에서 MQTT 전용 되어 있습니다.

메서드 요청 및 응답에 대 한 hello 페이로드는 too8KB JSON 문서입니다.

## <a name="reference-topics"></a>참조 항목:
hello 다음 참조 항목 제공 직접 메서드를 사용 하는 방법에 대 한 자세한 내용은 합니다.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>백 엔드 앱에서 직접 메서드 호출
### <a name="method-invocation"></a>메서드 호출
장치의 직접 메서드 호출은 다음을 포함하는 HTTP 호출입니다.

* hello *URI* 특정 toohello 장치 (`{iot hub}/twins/{device id}/methods/`)
* hello POST *메서드*
* *헤더* hello 권한 부여는, ID, 콘텐츠 형식 및 콘텐츠 인코딩을 요청
* 투명 한 JSON *본문* 형식에 따라 hello에:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

시간 제한은 초 단위입니다. 제한 시간을 설정 하지 않으면 too30 기본값으로 설정 시간 (초)입니다.

### <a name="response"></a>응답
hello 백 엔드 응용 프로그램을 구성을 응답을 수신 합니다.

* *HTTP 상태 코드*, hello IoT 허브에서에서 제공 하는 오류에 사용 되는, 장치에 대 한 404 오류를 포함 하 여 현재 연결 되어 있습니다.
* *헤더* hello ETag를 포함 합니다.는, ID, 콘텐츠 형식 및 콘텐츠 인코딩을 요청
* JSON *본문* 형식에 따라 hello에:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   둘 다 `status` 및 `body` hello 장치에서 제공 되 고 toorespond hello 장치의 상태 코드 및/또는 설명을 사용 합니다.

## <a name="handle-a-direct-method-on-a-device"></a>장치에서 직접 메서드 처리
### <a name="method-invocation"></a>메서드 호출
Hello MQTT 항목에 대 한 직접 메서드 요청을 수신 하는 장치:`$iothub/methods/POST/{method name}/?$rid={request id}`

hello 받는 hello 장치가 고, 형식에 따라 hello:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

메서드 요청은 QoS 0입니다.

### <a name="response"></a>응답
hello 장치 응답을 너무 전송`$iothub/methods/res/{status}/?$rid={request id}`, 여기서:

* hello `status` 속성은 메서드 실행의 hello 장치가 제공한 상태입니다.
* hello `$rid` 속성은 IoT 허브에서 받은 hello 메서드 호출에서 hello 요청 ID입니다.

hello 본문 hello 장치에 의해 설정 되 고 모든 상태의 될 수 있습니다.

## <a name="additional-reference-material"></a>추가 참조 자료
Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* [제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.
* [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.
* [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 합니다.
* [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계
이제 어떻게 toouse 직접 메서드 관심이 있을 수 있습니다 hello IoT 허브 개발자 가이드 항목에 방법을 배웠습니다.

* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.

* [직접 메서드 사용][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
