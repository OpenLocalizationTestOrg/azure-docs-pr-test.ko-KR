---
title: ".NET 및 AMQP 1.0을 사용 하 여 버스 aaaService | Microsoft Docs"
description: "AMQP를 사용하여 .NET에서 Azure Service Bus 사용"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>AMQP 1.0을 사용하여 .NET에서 서비스 버스 사용

## <a name="downloading-hello-service-bus-sdk"></a>Hello 서비스 버스 SDK 다운로드

AMQP 1.0 지원이 hello 서비스 버스 SDK 2.1 이상 버전에서에서 제공 됩니다. 있도록 hello 최신 버전의 hello 서비스 버스 비트를 다운로드 하 여 할 수 있습니다 [NuGet][NuGet]합니다.

## <a name="configuring-net-applications-toouse-amqp-10"></a>.NET 응용 프로그램 toouse AMQP 1.0 구성

Hello 서비스 버스.NET 클라이언트 라이브러리는 기본적으로 서비스 버스 서비스는 전용된 SOAP 기반 프로토콜을 사용 하 여 hello와 통신 합니다. hello 기본 프로토콜 대신 AMQP 1.0 toouse hello 다음 섹션에 설명 된 대로 hello 서비스 버스 연결 문자열에서 명시적 구성이 필요 합니다. AMQP 1.0을 사용하는 경우 이러한 변경 사항 외에는 응용 프로그램 코드가 변경되지 않습니다.

Hello 현재 릴리스에서 가지 AMQP를 사용할 때 지원 되지 않는 몇 가지 API 기능이 있습니다. 이러한 지원 되지 않는 기능은 뒷부분 hello 섹션에 나열 됩니다 [기능, 제한 사항 및 동작의 차이 지원 하지 않는](#unsupported-features-restrictions-and-behavioral-differences)합니다. Hello 고급 구성 설정 중 일부는 또한 AMQP를 사용할 때 서로 다른 의미를 갖습니다.

### <a name="configuration-using-appconfig"></a>App.config를 사용한 구성

응용 프로그램 toouse hello App.config 구성 파일 toostore 설정에 대 한 것이 좋습니다. 서비스 버스 응용 프로그램에 대 한 App.config toostore hello 서비스 버스 연결 문자열을 사용할 수 있습니다. 샘플 App.config 파일은 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

값의 hello hello `Microsoft.ServiceBus.ConnectionString` 설정은 hello 서비스 버스 연결 문자열을 사용 하는 tooconfigure hello 연결 tooService 버스입니다. hello 형식은 다음과 같습니다.

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

여기서 `[namespace]` 및 `SharedAccessKey` hello에서 가져온 [Azure 포털] [ Azure portal] 서비스 버스 네임 스페이스를 만들 때. 자세한 내용은 참조 [hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스 만들기][Create a Service Bus namespace using hello Azure portal]합니다.

AMQP를 사용할 때는 추가 된 연결 문자열 hello `;TransportType=Amqp`합니다. 이 표기는 해당 연결 tooService 버스 AMQP 1.0을 사용 하 여 hello 클라이언트 라이브러리 toomake를 지시 합니다.

## <a name="message-serialization"></a>메시지 직렬화

Hello.NET 클라이언트 라이브러리의 hello 기본 serialization 동작은 toouse hello hello 기본 프로토콜을 사용할 경우 [DataContractSerializer] [ DataContractSerializer] tooserialize 입력 한 [BrokeredMessage ] [ BrokeredMessage] hello 클라이언트 라이브러리와 hello 서비스 버스 서비스 간 전송에 대 한 인스턴스. Hello 클라이언트 라이브러리의 hello serialization에 대 한 hello AMQP 형식 시스템 hello AMQP 전송 모드를 사용 하면 사용 [조정 된 메시지] [ BrokeredMessage] 를 AMQP 메시지로 합니다. 이 serialization hello 메시지 toobe를 받아서 hello JMS API tooaccess 서비스 버스를 사용 하는 Java 응용 예를 들어, 다른 플랫폼에서 실행 중일 수 있는 수신 응용 프로그램에서 해석할 수 있습니다.

생성할 때는 [BrokeredMessage] [ BrokeredMessage] 인스턴스에 hello hello 메시지 본문으로 매개 변수 toohello 생성자 tooserve로.NET 개체를 제공할 수 있습니다. 매핑된 tooAMQP 기본 형식 수 있는 개체에 대 한 hello 본문은 AMQP 데이터 형식으로 serialize 됩니다. Hello 개체를 AMQP 기본 형식;에 직접 매핑할 수 없는 경우 즉, hello 응용 프로그램 다음 hello 개체에 정의 된 사용자 지정 형식을 hello를 사용 하 여 serialize 되 [DataContractSerializer][DataContractSerializer], 직렬화 hello 바이트는 AMQP 데이터 메시지의 전송 됩니다.

.NET 이외의 클라이언트의 상호 운용성 toofacilitate hello 메시지의 본문 hello에 대 한 AMQP 형식으로 직접 serialize 할 수 있는.NET 형식만 사용 합니다. 다음 표에 hello 해당 형식과 hello 해당 매핑 toohello AMQP 형식 시스템을 자세히 설명 합니다.

| .NET 본문 개체 형식 | 매핑된 AMQP 형식 | AMQP 본문 섹션 형식 |
| --- | --- | --- |
| bool |부울 |AMQP 값 |
| byte |ubyte |AMQP 값 |
| ushort |ushort |AMQP 값 |
| uint |uint |AMQP 값 |
| ulong |ulong |AMQP 값 |
| sbyte |byte |AMQP 값 |
| short |short |AMQP 값 |
| int |int |AMQP 값 |
| long |long |AMQP 값 |
| float |float |AMQP 값 |
| double |double |AMQP 값 |
| decimal |decimal128 |AMQP 값 |
| char |char |AMQP 값 |
| DateTime |timestamp |AMQP 값 |
| Guid |uuid |AMQP 값 |
| byte[] |binary |AMQP 값 |
| string |string |AMQP 값 |
| System.Collections.IList |list |AMQP 값: hello 컬렉션에 포함 된 항목으로 가능이 테이블에 정의 된 것입니다. |
| System.Array |array |AMQP 값: hello 컬렉션에 포함 된 항목으로 가능이 테이블에 정의 된 것입니다. |
| System.Collections.IDictionary |map |AMQP 값: hello 컬렉션에 포함 된 항목으로 가능이 테이블에 정의 된 것입니다. 참고: String 키만 지원 됩니다. |
| Uri |설명 문자열 (hello 다음 표 참조) |AMQP 값 |
| Datetimeoffset |긴 설명 (hello 다음 표 참조) |AMQP 값 |
| TimeSpan |긴 설명 (hello 다음 참조) |AMQP 값 |
| Stream |binary |AMQP 데이터(여러 개가 있을 수 있음). hello 데이터 섹션 hello 스트림 개체에서 읽은 hello 원시 바이트를 포함 합니다. |
| 다른 개체 |binary |AMQP 데이터(여러 개가 있을 수 있음). Hello 응용 프로그램에서 제공 하는 직렬 변환기 또는 DataContractSerializer hello를 사용 하는 hello 개체의 직렬화 된 hello 이진을 포함 합니다. |

| .NET 형식 | 매핑된 AMQP 설명된 형식 | 참고 사항 |
| --- | --- | --- |
| Uri |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>지원되지 않는 기능, 제한 및 동작 차이

hello 서비스 버스.NET API의 기능을 수행 하는 hello AMQP를 사용 하는 경우 현재 지원 되지 않습니다.

* 트랜잭션
* 전송 대상을 통해 보내기

또한 작은 차이가 있습니다 hello 동작 hello 서비스 버스.NET API의 AMQP, 비교 toohello 기본 프로토콜을 사용 하는 경우:

* hello [OperationTimeout] [ OperationTimeout] 속성은 무시 됩니다.
* `MessageReceiver.Receive(TimeSpan.Zero)`은(는) `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`(으)로 구현됩니다.
* 메시지 잠금 토큰에 의해 완료 처음 hello 메시지를 받은 hello 메시지 수신기만 수행할 수 있습니다.

## <a name="controlling-amqp-protocol-settings"></a>AMQP 프로토콜 설정 제어

hello [.NET Api](/dotnet/api/) hello AMQP 프로토콜의 몇 가지 설정을 toocontrol hello 동작을 노출 합니다.

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: 컨트롤에 적용 하는 초기 신용도 tooa 링크 hello 합니다. hello 기본값은 0입니다.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: 열린 연결 시 hello 협상 하는 동안 컨트롤 hello 최대 AMQP 프레임 크기를 제공 합니다. hello 기본값은 65, 536 바이트입니다.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: 전송 인 따라 발신이 값 hello 최대 지연 처리를 결정 합니다. 기본적으로 발신자/수신자를 상속합니다. 개별 발신자/수신자 hello 기본값인 20 밀리초를 재정의할 수 있습니다.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: AMQP 연결이 SSL 연결을 통해 설정되는지 여부를 제어합니다. hello 기본값은 **true**합니다.

## <a name="next-steps"></a>다음 단계

더 많은 toolearn 준비? Hello 다음 링크를 방문.

* [Service Bus AMQP 개요]
* [Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]
* [Windows Server용 Service Bus의 AMQP]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Service Bus AMQP 개요]: service-bus-amqp-overview.md
[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
