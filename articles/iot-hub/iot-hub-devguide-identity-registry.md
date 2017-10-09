---
title: "aaaUnderstand hello Azure IoT Hub id 레지스트리에 | Microsoft Docs"
description: "개발자 가이드-hello IoT Hub id 레지스트리에 설명은 방법과 toouse 것 toomanage 장치입니다. 대량에 hello 가져오기 및 내보내기 장치 id에 대 한 정보를 포함합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>IoT hub에 hello id 레지스트리에 이해

모든 IoT hub tooconnect toohello IoT 허브를 허용 하는 hello 장치에 대 한 정보를 저장 하는 id 레지스트리에 있습니다. 장치 tooan IoT 허브에 연결할 수 전에 hello IoT hub id 레지스트리에에서 해당 장치에 대 한 항목이 있어야 합니다. 장치 id 레지스트리에 hello에 저장 된 자격 증명에 따라 hello IoT hub와도 인증 해야 합니다.

hello identity 레지스트리에 저장 된 hello 장치 ID는 대/소문자 구분입니다.

상위 수준 hello id 레지스트리에 장치 identity 리소스는 REST 가능 컬렉션입니다. Hello id 레지스트리에 항목을 추가 하는 경우 IoT 허브는 진행 중인 클라우드-장치 메시지를 포함 하는 hello 큐와 같은 장치 리소스 집합을 만듭니다.

### <a name="when-toouse"></a>때 toouse

Hello id 레지스트리에을 할 때 사용 합니다.

* Tooyour IoT 허브를 연결 하는 장치를 프로 비전 합니다.
* 장치 액세스 tooyour 허브의 장치에 연결 끝점을 제어 합니다.

> [!NOTE]
> hello id 레지스트리에 응용 프로그램별 메타 데이터가 없습니다.

## <a name="identity-registry-operations"></a>ID 레지스트리 작업

IoT Hub id 레지스트리에 hello hello 다음 작업을 노출 합니다.

* 장치 ID 만들기
* 장치 ID 업데이트
* ID로 장치 ID 검색
* 장치 ID 삭제
* Too1000 identities를 나열 합니다.
* 모든 identities tooAzure blob 저장소 내보내기
* Azure Blob Storage에서 ID 가져오기

이러한 모든 작업은 [RFC7232][lnk-rfc7232]에 지정된 낙관적 동시성을 사용할 수 있습니다.

> [!IMPORTANT]
> 방법은 tooretrieve만 hello id 레지스트리에 IoT 허브에서 모든 id는 toouse hello [내보내기] [ lnk-export] 기능입니다.

IoT Hub ID 레지스트리:

* 응용 프로그램 메타 데이터가 없습니다.
* Hello를 사용 하 여 사전 처럼 액세스할 수 **deviceId** hello 키로 합니다.
* 표현 쿼리를 지원하지 않습니다.

IoT 솔루션에는 일반적으로 응용 프로그램 관련 메타데이터가 포함된 별도의 솔루션 관련 저장소가 있습니다. 예를 들어 hello 스마트 건물 솔루션에서 솔루션 별 저장소 기록 온도 센서 배포 된 hello 공간입니다.

> [!IMPORTANT]
> 장치 관리 및 프로비저닝 작업에 대 한 hello id 레지스트리에 사용 합니다. 처리량이 높은 작업 실행 시 hello id 레지스트리에에서 작업을 수행 신뢰 하지 않아야 합니다. 예를 들어 명령을 전송 하기 전에 장치의 hello 연결 상태를 확인 하지 지원 되는 패턴입니다. 있는지 toocheck hello 확인 [제한을] [ lnk-quotas] hello id 레지스트리 및 hello에 대 한 [장치 하트 비트] [ lnk-guidance-heartbeat] 패턴입니다.

## <a name="disable-devices"></a>장치 비활성화

Hello를 업데이트 하 여 장치를 비활성화할 수 **상태** hello identity 레지스트리에 id의 속성입니다. 일반적으로 이 속성은 두 가지 시나리오에 사용합니다.

* 오케스트레이션 과정을 프로비전하는 동안입니다. 자세한 내용은 [장치 프로비전][lnk-guidance-provisioning]을 참조하세요.
* 어떤 이유로든 손상되거나 권한이 없는 장치를 사용하도록 고려합니다.

## <a name="import-and-export-device-identities"></a>장치 ID 가져오기 및 내보내기

Hello에 대 한 비동기 작업을 사용 하 여 IoT 허브의 id 레지스트리에에서 대량에서 장치 id를 내보낼 수 [IoT 허브 리소스 공급자 끝점][lnk-endpoints]합니다. 내보내기는 장기 실행 hello identity 레지스트리에서 고객이 제공한 blob 컨테이너 toosave 장치 id 데이터를 사용 하는 작업을 읽습니다.

Hello에 대 한 비동기 작업을 사용 하 여 대량 tooan IoT hub id 레지스트리에에서 장치 id를 가져올 수 있습니다 [IoT 허브 리소스 공급자 끝점][lnk-endpoints]합니다. 가져오기는 hello identity 레지스트리에 고객이 제공한 blob 컨테이너 toowrite 장치 id 데이터에서 데이터를 사용 하는 장기 실행 작업입니다.

* Hello 가져오기 및 내보내기 Api에 대 한 자세한 내용은 참조 [IoT 허브 리소스 공급자 REST Api][lnk-resource-provider-apis]합니다.
* toolearn 실행에 대 한 자세한 가져오기 및 내보내기 작업을 참조 하십시오 [IoT Hub 장치 id 관리 대량][lnk-bulk-identity]합니다.

## <a name="device-provisioning"></a>장치 프로비전

지정된 된 IoT 솔루션을 저장 하는 hello 장치 데이터 hello 해당 솔루션의 특정 요구 사항에 따라 달라 집니다. 하지만 어떤 솔루션이든 최소한 장치 ID와 인증 키를 저장해야 합니다. Azure IoT Hub는 ID, 인증 키 및 상태 코드와 같은 각 장치에 대한 값을 저장할 수 있는 ID 레지스트리를 포함합니다. 솔루션 추가 장치 데이터 Cosmos DB toostore 테이블 저장소, blob 저장소 등 다른 Azure 서비스를 사용할 수 있습니다.

*장치 프로 비전* hello 프로세스 솔루션의 hello 초기 장치 데이터 toohello 매장을 추가 하는입니다. 새 장치 tooconnect tooyour 허브 tooenable 장치 ID와 키 toohello IoT Hub id 레지스트리에 추가 해야 합니다. Hello 프로 비전 프로세스의 일환으로, 다른 솔루션 저장소에 tooinitialize 장치 관련 데이터를 할 수 있습니다.

## <a name="device-heartbeat"></a>장치 하트비트

hello IoT Hub id 레지스트리에 필드가 들어 **connectionState**합니다. 만 hello를 사용 하 여 **connectionState** 개발 및 디버깅 하는 동안 필드입니다. IoT 솔루션에서 런타임에 hello 필드를 쿼리할 해야 합니다. 예를 들어 hello 쿼리하지 않는 **connectionState** 필드 toocheck 클라우드-장치 메시지 또는 SMS 보내기 전에 장치가 연결 된 경우.

Hello를 구현 해야 하면 IoT 솔루션을 필요한 경우 tooknow 장치가 연결 된 경우 *하트 비트 패턴*합니다.

Hello 하트 비트 패턴을 한 번 이상 (예: 매 시간 마다 적어도 한 번) 시간의 모든 고정 된 숫자일 hello 장치 장치-클라우드 메시지를 보냅니다. 따라서 장치에 모든 데이터 toosend 없는 경우에 여전히 일반적으로 (하트 비트도 식별 하는 속성)를 사용 하는 빈 장치-클라우드 메시지를 보냅니다. Hello 솔루션 hello 서비스 쪽에서는 각 장치에 대 한 수신 hello 마지막 하트 비트와 지도 유지 관리 합니다. Hello 솔루션 hello 장치에서 hello 예상 시간 안에 하트 비트 메시지를 받지 않을 경우 hello 장치 문제 임을 가정 합니다.

더 복잡 한 구현에서 hello 정보를 포함할 수 [작업 모니터링] [ lnk-devguide-opmon] tooidentify 장치 tooconnect 또는 통신에 실패 하지만 합니다. Hello 하트 비트 패턴을 구현 하는 경우 확인 되었는지 toocheck [IoT 허브 할당량 및 제한을][lnk-quotas]합니다.

> [!NOTE]
> IoT 솔루션 사용 하 여 hello 연결 상태만 toodetermine 여부 경우 toosend 클라우드-장치 메시지, 메시지는 하지 장치 집합이 toolarge 브로드캐스트, 간단 hello를 사용 하는 것이 좋습니다 *짧은 만료 시간* 패턴입니다. 이 패턴 hello hello 하트 비트 패턴을 사용 하 여 보다 효율적인를 사용 하는 장치 연결 상태 레지스트리를 유지 관리와 같은 결과 얻을 수 있습니다. 메시지 승인이 요청 하는 경우 IoT Hub 있는 장치 수 tooreceive 메시지 이며 하지 않은 알릴 수 있음.

## <a name="device-lifecycle-notifications"></a>장치 수명 주기 알림

장치 ID가 생성 또는 삭제되면 IoT Hub에서 장치 수명 주기 알림을 전송하여 IoT 솔루션에 알릴 수 있습니다. toodo, 하면 IoT 솔루션 필요한 등 toocreate 경로 및 tooset hello 데이터 소스 같음 너무*DeviceLifecycleEvents*합니다. 기본적으로 수명 주기 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다. hello 알림 메시지에 속성 및 본문에 포함 됩니다.

속성: 메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.

| 이름 | 값 |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  Hello 알림을 전송 시간 |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** 또는 **deleteDeviceIdentity** |
hubName | IoT Hub의 이름 |
deviceId | Hello 장치의 ID |
operationTimestamp | 작업의 ISO8601 타임스탬프 |
iothub-message-schema | deviceLifecycleNotification |

본문:이 섹션 JSON 형식으로는 고 장치 id를 생성 하는 hello의 hello로 이중을 나타냅니다. 예를 들면 다음과 같습니다.

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>참조 항목:

hello 다음 참조 항목 제공 hello id 레지스트리에 대 한 자세한 내용은 합니다.

## <a name="device-identity-properties"></a>장치 ID 속성

장치 id가 다음과 같은 속성 hello로 JSON 문서가 표시 됩니다.

| 속성 | 옵션 | 설명 |
| --- | --- | --- |
| deviceId |필요한 경우 업데이트에서 읽기 전용입니다. |ASCII 7 비트 영숫자 문자 (위쪽 too128 자)는 대/소문자 구분 문자열 + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`합니다. |
| generationId |필요한 경우 읽기 전용 |IoT 허브에서 생성 된, 대/소문자 구분 문자열을 too128 자입니다. 이 값은 hello로 사용 되는 toodistinguish 장치 동일한 **deviceId**삭제 및 다시 생성 하는 경우. |
| etag |필요한 경우 읽기 전용 |기준으로 hello 장치 id에 대 한 약한 ETag를 나타내는 문자열 [RFC7232][lnk-rfc7232]합니다. |
| auth |선택 사항 |인증 정보 및 보안 자료를 포함하는 복합 개체입니다. |
| auth.symkey |선택 사항 |base64 형식으로 저장된 기본 및 보조 키를 포함하는 복합 개체입니다. |
| status |필수 |액세스 표시기입니다. **사용** 또는 **사용 안 함**으로 설정할 수 있습니다. 경우 **Enabled**, hello 장치 tooconnect ï ´ ù. **사용 안 함**이면 이 장치는 장치 연결 끝점에 액세스할 수 없습니다. |
| statusReason |선택 사항 |128 문자 길이의 문자열 hello 장치 id 상태에 대 한 해당 저장소 hello 이유입니다. UTF-8 문자를 모두 허용합니다. |
| statusUpdateTime |읽기 전용 |상태 업데이트를 마지막 hello의 hello 날짜 및 시간을 보여 주는 임시 표시기입니다. |
| connectionState |읽기 전용 |연결 상태를 나타내는 필드: **연결됨** 또는 **연결 끊김**. 이 필드는 hello를 IoT Hub 보기의 hello 장치 연결 상태를 나타냅니다. **중요**: 이 필드는 개발/디버깅 용도로만 사용해야 합니다. hello 연결 상태가 MQTT 또는 AMQP를 사용 하 여 장치에 대해서만 업데이트 됩니다. 또한 이는 프로토콜 수준의 ping(MQTT ping 또는 AMQP ping)을 기반으로 하고 있으며 최대 5분 동안만 지연이 될 수 있습니다. 이러한 이유로, 연결되었지만 연결이 끊긴 것으로 보고된 장치와 같이 거짓 긍정이 있을 수 있습니다. |
| connectionStateUpdatedTime |읽기 전용 |Hello 날짜 및 마지막 시간 hello 연결 상태와 함께 임시 표시기가 업데이트 되었습니다. |
| lastActivityTime |읽기 전용 |Hello 날짜 및 마지막 시간 hello 장치 연결 받거나 보낸 메시지와 함께 임시 표시기입니다. |

> [!NOTE]
> 연결 상태 hello hello 연결의 hello 상태에 대 한 IoT Hub 보기 나타낼 수 있습니다. 네트워크 상태 및 구성에 따라 업데이트 toothis 상태 지연 될 수 있습니다.

## <a name="additional-reference-material"></a>추가 참조 자료

Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* [제한 및 할당량] [ lnk-quotas] hello 할당량을 설명 하 고 toohello IoT 허브 서비스에 적용 되는 동작을 조정 합니다.
* [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.
* [IoT Hub 쿼리 언어] [ lnk-query] 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용할 수는 hello 쿼리 언어에 설명 합니다.
* [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계

이제 어떻게 toouse hello IoT Hub id 레지스트리에 관심이 있을 수 있습니다 hello 다음 IoT 허브 개발자 가이드 항목에에서는 방법을 배웠습니다.

* [컨트롤 액세스 tooIoT 허브][lnk-devguide-security]
* [장치 트윈스 toosynchronize 상태 및 구성 사용][lnk-devguide-device-twins]
* [장치에서 직접 메서드 호출][lnk-devguide-directmethods]
* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.

* [Azure IoT Hub 시작][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
