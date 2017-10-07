---
title: "aaaUnderstand hello Azure IoT 허브에 대 한 기본 제공 끝점 | Microsoft Docs"
description: "개발자 가이드-toouse 기본 제공, 이벤트 허브 호환 끝점 태그로 장치-클라우드 메시지 hello 하는 방법을 설명 합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Hello 기본 제공 끝점에서 장치-클라우드 메시지 읽기

기본적으로 메시지는 라우트된 toohello 기본 제공 서비스 연결 끝점 (**이벤트 메시지/**), 즉 호환 [이벤트 허브][lnk-event-hubs]합니다. 데이터베이스 미러링이 끝점은 현재 hello를 사용 하 여에 노출 [AMQP] [ lnk-amqp] 포트 5671의 프로토콜입니다. IoT hub hello를 노출 하면 toocontrol 속성 tooenable 다음 기본 제공 이벤트 허브 호환 메시징 끝점을 hello **이벤트메시지/**합니다.

| 속성            | 설명 |
| ------------------- | ----------- |
| **분할 개수** | 생성 toodefine hello 수의이 속성을 설정 [파티션을] [ lnk-event-hub-partitions] 장치-클라우드 이벤트 수집 합니다. |
| **보존 시간**  | 이 속성은 IoT Hub에서 메시지를 보존할 일 수를 지정합니다. hello 기본값은 1 일 이지만 증가 tooseven 일 수 있습니다. |

IoT Hub 사용 하면 수도 toomanage 소비자 그룹에 hello 기본 제공 장치-클라우드 끝점을 수신 합니다.

기본적으로 모든 메시지는 메시지 라우팅 규칙을 명시적으로 일치 하지 않는 기본 제공 끝점 toohello 기록 됩니다. 이 대체 경로를 비활성화하면 메시지 라우팅 규칙과 명시적으로 일치하지 않는 메시지는 삭제됩니다.

Hello를 통해 프로그래밍 방식으로 hello 보존 시간을 수정할 수 있습니다 [IoT 허브 리소스 공급자 REST Api][lnk-resource-provider-apis], 또는 hello를 사용 하 여 [Azure 포털] [ lnk-management-portal].

IoT Hub 노출 hello **이벤트메시지/** 백 엔드에 대 한 기본 제공 끝점 허브에서 수신한 tooread hello 장치-클라우드 메시지를 서비스 합니다. 데이터베이스 미러링이 끝점은 이벤트 허브 호환 toouse 메시지 도착 읽기에 대 한 지원 hello 메커니즘 hello 이벤트 허브 서비스 중 하나를 사용할 수 있는 합니다.

## <a name="read-from-hello-built-in-endpoint"></a>Hello 기본 제공 끝점에서 읽기

Hello를 사용 하는 경우 [.NET 용 Azure 서비스 버스 SDK] [ lnk-servicebus-sdk] 또는 hello [이벤트 허브-이벤트 프로세서 호스트][lnk-eventprocessorhost], 모든 IoT 허브 연결을 사용할 수 있습니다 hello 올바른 사용 권한이 있는 문자열입니다. 다음 사용 하 여 **이벤트메시지/** hello 이벤트 허브 이름으로 합니다.

사용 하는 경우 Sdk (또는 제품 통합) IoT Hub 인식 하지 않습니다, hello의 hello IoT Hub 설정에서 이벤트 허브 호환 끝점 및 이벤트 허브 호환 이름을 검색 해야 [Azure 포털] [ lnk-management-portal]:

1. Hello IoT 허브 블레이드에서 클릭 **끝점**합니다.
1. Hello에 **기본 제공 끝점** 섹션에서 클릭 **이벤트**합니다. hello 블레이드 포함 된 다음 값에는 hello: **호환 이벤트 허브 끝점**, **이벤트 허브와 호환 가능한 이름**, **파티션을**, **보존시간**, 및 **소비자 그룹**합니다.

    ![장치-클라우드 설정][img-eventhubcompatible]

IoT 허브 SDK hello 필요 hello IoT Hub 끝점 이름이 며, **이벤트 메시지/** hello에 나와 있는 것 처럼 **끝점** 블레이드입니다.

SDK를 사용 하는 hello 요구 하는 경우는 **Hostname** 또는 **Namespace** hello에서 hello 구성표 제거, 값 **호환 이벤트 허브 끝점**합니다. 예를 들어 이벤트 허브 호환 끝점 **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** 것  **iothub ns-myiothub 1234.servicebus.windows.net**, 및 hello **Namespace** 것 **ns myiothub 1234 iothub**합니다.

Hello에 있는 공유 액세스 정책을 사용할 수 있습니다 **ServiceConnect** 권한 tooconnect toohello 이벤트 허브를 지정 합니다.

Hello 이전 정보를 사용 하 여 toobuild 이벤트 허브 연결 문자열을 원하는 경우 hello 패턴을 사용 합니다.

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

hello Sdk 및 IoT Hub를 노출 하는 이벤트 허브 호환 끝점으로 사용할 수 있는 통합 hello 목록 다음에 hello 항목을 포함 합니다.

* [Java 이벤트 허브 클라이언트](https://github.com/hdinsight/eventhubs-client)
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Hello를 볼 수 있습니다 [소스 spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) GitHub에서 합니다.
* [Apache Spark 통합](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)

## <a name="next-steps"></a>다음 단계

IoT Hub 끝점에 대한 자세한 내용은 [IoT Hub 끝점][lnk-endpoints]을 참조하세요.

hello [시작] [ lnk-get-started] 보여 주는 자습서 toosend 장치-클라우드 메시지를이 장치를 시뮬레이션 하 고 hello 기본 제공 끝점에서 hello 메시지를 읽은 하는 방법입니다. 자세한 정보를 얻기 위해 hello 참조 [경로 사용 하 여 프로세스 IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.

사용자 장치-클라우드 메시지 toocustom 끝점 tooroute 하려는 경우, 참조 [장치-클라우드 메시지에 대 한 메시지 경로 및 사용자 지정 끝점을 사용 하 여][lnk-custom]합니다.

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
