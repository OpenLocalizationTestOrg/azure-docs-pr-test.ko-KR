---
title: "이벤트 허브 aaaAzure 기능 개요 | Microsoft Docs"
description: "Azure Event Hubs 기능에 대한 개요 및 세부 정보"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Event Hubs 기능 개요

Azure Event Hubs는 확장 가능한 처리 서비스로 대량의 이벤트 및 데이터를 수집하여 처리하며, 대기 시간이 낮고 안정성이 우수합니다. 참조 [이벤트 허브는 무엇입니까?](event-hubs-what-is-event-hubs.md) hello 서비스에 대 한 고급 개요에 대 한 합니다.

Hello에 hello 정보를 기반으로 한이 문서 [개요](event-hubs-what-is-event-hubs.md), 이벤트 허브 구성 요소 및 기능에 대 한 기술 및 구현 세부 정보를 제공 합니다.

## <a name="event-publishers"></a>이벤트 게시자

데이터 tooan 이벤트 허브는 이벤트 생산자를 전송 하는 모든 엔터티 또는 *이벤트 게시자*합니다. 이벤트 게시자는 HTTPS 또는 AMQP 1.0을 사용하여 이벤트를 게시할 수 있습니다. 이벤트 게시자 자신을 사용해 서 공유 액세스 서명 (SAS) 토큰 tooidentify tooan 이벤트 허브 및 고유 id가 사용 하거나 공통 SAS 토큰을 사용 하 여 수 있습니다.

### <a name="publishing-an-event"></a>이벤트 게시

AMQP 1.0 또는 HTTPS를 통해 이벤트를 게시할 수 있습니다. 이벤트 허브 제공 [클라이언트 라이브러리와 클래스](event-hubs-dotnet-framework-api-overview.md) 이벤트 tooan 이벤트 허브.NET 클라이언트에서 게시에 대 한 합니다. 다른 런타임 및 플랫폼의 경우, [Apache Qpid](http://qpid.apache.org/)와 같은 모든 AMQP 1.0 클라이언트를 사용할 수 있습니다. 이벤트를 개별적으로 게시하거나 일괄처리할 수 있습니다. 단일 게시(이벤트 데이터 인스턴스)는 단일 이벤트 또는 일괄 처리인지에 관계 없이 256KB로 제한됩니다. 이 임계값보다 큰 이벤트를 게시하면 오류가 발생합니다. 게시자 toobe hello 이벤트 허브 내의 파티션을 인식 하지 못하는 대 한 가장 좋은 방법은 및 tooonly 지정는 *파티션 키* (hello 다음 섹션에서 도입) 또는 SAS 토큰을 통해 id입니다.

AMQP 나 HTTPS hello 선택 toouse 특정 toohello 사용 시나리오입니다. AMQP은 SSL/TLS 또는 더하기 tootransport 수준 보안 (TLS)에 영구 양방향 소켓으로 hello 구축이 필요합니다. AMQP에 더 높은 네트워크 비용 hello 세션에 초기화할 때 HTTPS 추가 SSL 오버 헤드가 필요 모든 요청에 대해 있지만 있습니다. AMQP는 빈번한 게시자에게 더 높은 성능을 제공합니다.

![Event Hubs](./media/event-hubs-features/partition_keys.png)

이벤트 허브를 사용 하는 파티션 키 값을 공유 하는 모든 이벤트로 전달 되는 순서 및 toohello 동일한 파티션 합니다. 게시자 정책과 함께 파티션 키를 사용 하면 다음 hello 게시자의 id를 hello 및 hello hello 파티션 키 값과 일치 해야 합니다. 그렇지 않은 경우 오류가 발생합니다.

### <a name="publisher-policy"></a>게시자 정책

이벤트 허브는 *게시자 정책*을 통한 이벤트 게시자에 대한 세부적 제어를 사용합니다. 게시자 정책은 런타임에 기능인 toofacilitate 많은 수의 독립 이벤트 게시자는입니다. 게시자 정책을 사용 하 여 각 게시자 사용 하 여 고유한 자체 식별자 이벤트 tooan 이벤트 허브를 게시 하는 경우 다음 메커니즘 hello를 사용 하 여:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Toocreate 게시자 이름을 미리 필요는 없지만 hello SAS 토큰 순서 tooensure 게시자 id의 독립성에 이벤트를 게시할 때 사용 되는 일치 해야 합니다. 게시자 정책을 사용 하는 경우 hello **PartitionKey** toohello 게시자 이름이 설정 됩니다. toowork 적절 하 게 이러한 값 일치 해야 합니다.

## <a name="capture"></a>캡처

[이벤트 허브 캡처](event-hubs-capture-overview.md) tooautomatically 캡처 hello 스트리밍 데이터 이벤트 허브에 있고 tooyour 다양 한 Blob 저장소 계정 또는 Azure 데이터 레이크 서비스 계정을 저장 합니다. Hello Azure 포털에서에서 캡처를 활성화 하 고 최소 크기 및 시간 창 tooperform hello 캡처 지정 수 있습니다. 직접 Azure Blob 저장소 계정 및 컨테이너에 지정 이벤트 허브 캡처를 사용 하거나 사용 되는 toostore hello Azure 데이터 레이크 서비스 계정에 데이터를 캡처한 합니다. 캡처된 데이터는 hello Apache Avro 형식으로 기록 됩니다.

## <a name="partitions"></a>파티션

이벤트 허브는 각 소비자를 읽을 수만 특정 하위 집합 또는 hello 메시지 스트림의 파티션을 분할 된 소비자 패턴을 통해 메시지 스트리밍를 제공 합니다. 이 패턴은 이벤트 처리를 위한 가로 눈금을 사용하며 큐 및 항목에 사용할 수 없는 기타 스트림 중심 기능을 제공합니다.

파티션은 Event Hub에서 보유하는 순서가 지정된 이벤트 시퀀스입니다. 도착 한 이벤트,이 시퀀스의 끝 toohello 추가 됩니다. 파티션을 "커밋 로그"로 생각할 수 있습니다.

![Event Hubs](./media/event-hubs-features/partition.png)

이벤트 허브는 hello 이벤트 허브의 모든 파티션에 적용 되는 구성 된 보존 시간에 대 한 데이터를 유지 합니다. 시간 단위로 이벤트가 만료됩니다. 명시적으로 삭제할 수 없습니다. 파티션은 독립적이며 자체 데이터 시퀀스를 포함하기 때문에 종종 다른 속도로 증가합니다.

![Event Hubs](./media/event-hubs-features/multiple_partitions.png)

hello 파티션 수가 생성 시 지정 하 고 2에서 32 사이 여야 합니다. hello 파티션 수를 변경할 수 하지 않으므로 파티션 수를 설정할 때 장기 눈금을 고려해 야 합니다. 파티션은은 데이터 구성 메커니즘이 소비형 응용 프로그램에 필요한 toohello 다운스트림 병렬 처리를 연결 하는입니다. hello 이벤트 허브의 파티션 수가 직접 toohello 수 연결 toohave 동시 독자의 예상 합니다. Hello 이벤트 허브 팀에 문의 하 여 hello 수가 32 초과 하는 파티션을 늘릴 수 있습니다.

파티션은 식별 가능 하며 toodirectly 보낼 수, 하는 동안 보내기 직접 tooa 파티션 권장 되지 않습니다. 대신 hello에 도입 된 더 높은 수준의 구문을 사용할 수 있습니다 [이벤트 게시자](#event-publishers) 및 [용량](#capacity) 섹션. 

파티션은는 hello 이벤트의 hello 본문, 사용자 정의 속성 모음 및 hello 파티션에 오프셋과 hello 스트림 시퀀스의 해당 번호로 등의 메타 데이터를 포함 하는 이벤트 데이터 시퀀스가 채워집니다.

파티션 및 사용 가능성 및 안정성이 사이의 절충 값 hello에 대 한 자세한 내용은 참조 hello [이벤트 허브 프로그래밍 가이드](event-hubs-programming-guide.md#partition-key) 및 hello [가용성 및 이벤트 허브의 일관성](event-hubs-availability-and-consistency.md) 문서 .

### <a name="partition-key"></a>파티션 키

사용할 수는 [파티션 키](event-hubs-programming-guide.md#partition-key) 데이터 구성의 hello 용도 대 한 특정 파티션으로 toomap 들어오는 이벤트 데이터입니다. hello 파티션 키는 이벤트 허브로 전달 되는 발신자가 제공한 값입니다. Hello 파티션 할당을 만드는 정적 해시 기능을 통해 처리 됩니다. 이벤트를 게시할 때 파티션 키를 지정하지 않으면 라운드 로빈 할당이 사용됩니다.

hello 이벤트 게시자는 파티션 키를 인식만 하지 hello 파티션 toowhich hello 이벤트 게시 됩니다. Hello 다운스트림 처리에 대해 자세히 tooknow 않아도 hello 보낸 같은 파티션 키와 키의이 분리로 인해 합니다. 관련 이벤트를 단일 파티션으로-장치 또는 사용자 고유 identity 파티션 키 하지만 지리 등의 다른 특성에 사용 되는 toogroup 수도 있습니다.

## <a name="sas-tokens"></a>SAS 토큰

이벤트 허브를 사용 하 여 *공유 액세스 서명*는 hello 네임 스페이스 및 이벤트 허브 수준에서 사용할 수 있는 합니다. SAS 토큰은 SAS 키에서 생성되고 특정 형식으로 인코딩된 URL의 SHA 해시입니다. 이벤트 허브 수 hello 키 (정책)와 hello 토큰의 hello 이름을 사용 하 여 hello 해시를 다시 생성 한 있으므로 hello 보낸 사람 인증. 일반적으로 이벤트 게시자에 대한 SAS 토큰은 특정 Event Hub에 대한 **전송** 권한만으로 작성됩니다. 이 SAS 토큰 URL 메커니즘은 게시자 정책 hello에에서 도입 된 게시자 id에 대 한 hello 기준이 됩니다. SAS 작업에 대한 자세한 내용은 [Service Bus를 사용한 공유 액세스 서명 인증](../service-bus-messaging/service-bus-sas.md)을 참조하세요.

## <a name="event-consumers"></a>이벤트 소비자

Event Hubs에서 이벤트 데이터를 읽는 모든 엔터티는 *이벤트 소비자*입니다. 모든 이벤트 허브 소비자 hello AMQP 1.0 세션을 통해 연결 하 고 제공 되 면 이벤트가 hello 세션을 통해 전달 됩니다. 클라이언트 hello 데이터 가용성에 대 한 toopoll이 필요 하지 않습니다.

### <a name="consumer-groups"></a>소비자 그룹

이벤트 허브의 hello 게시/구독 메커니즘을 통해 사용 됩니다 *소비자 그룹*합니다. 소비자 그룹은 전체 Event Hub의 보기(상태, 위치, 또는 오프셋)입니다. 소비자 그룹에는 여러 응용 프로그램이 tooeach hello 이벤트 스트림, 및 상황에 맞게에서 독립적으로 tooread hello 스트림에 대 한 별도 뷰 및 자체와 오프셋을 사용 합니다.

스트림 처리 아키텍처에서는 각 다운스트림 응용 프로그램에는 tooa 소비자 그룹을 같습니다. Toowrite 이벤트 데이터 toolong 장기 저장소를 사용 하도록 하려는 경우 해당 저장소 작성기 응용 프로그램은 소비자 그룹입니다. 복합 이벤트 처리는 별도의 다른 소비자 그룹에서 수행될 수 있습니다. 소비자 그룹을 통해서만 파티션을 액세스할 수 있습니다. 소비자 그룹당 파티션에는 최대 5개의 동시 판독기가 있을 수 있습니다. 하지만 **소비자 그룹당 파티션에는 활성 수신기를 하나만 포함하는 것이 좋습니다.** 항상 기본 소비자 그룹에 이벤트 허브에 있고 표준 계층 이벤트 허브에 대 한 too20 소비자 그룹을 만들 수 있습니다.

hello 다음은 hello 소비자 그룹 URI 규칙의 예입니다.

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

hello 다음 그림은 hello 이벤트 허브 스트림 처리 아키텍처:

![Event Hubs](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>스트림 오프셋

*오프셋* 파티션 내에서 이벤트의 hello 위치입니다. 오프셋을 클라이언트 쪽 커서로 생각할 수 있습니다. hello 오프셋은 바이트 hello 이벤트의 번호를 지정 합니다. 이 오프셋 이벤트 소비자 (독자) toospecify를 hello 이벤트 스트림에서 이벤트를 읽는 toobegin 보고자 지점 수 있습니다. Hello 오프셋을 타임 스탬프 또는 오프셋된 값으로 지정할 수 있습니다. 소비자는 hello 이벤트 허브 서비스 외부의 자체 오프셋된 값을 저장 해야 합니다. 파티션 내에서 각 이벤트는 오프셋을 포함합니다.

![Event Hubs](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>검사점 설정

*검사점* 은 판독기가 파티션 이벤트 시퀀스 내에서 위치를 표시하거나 커밋하는 프로세스입니다. 검사점은 hello hello 소비자 작업에서 수행 하 고 소비자 그룹 내에서 파티션 단위로에 발생 합니다. 이러한 책임 있음을 나타내고 각 소비자 그룹에 대 한 각 파티션 독자 해야 한 추적의 현재 위치에서 hello 이벤트 스트림, 되었다고 간주 hello 데이터 스트림이 완료 되 면 hello 서비스에 알릴 수 있습니다.

게 다시 연결 하는 경우 판독기는 파티션에서 끊어집니다가 해당 소비자 그룹 내에서 해당 파티션의 hello 마지막 독자가 이전에 제출한 hello 검사점에서 읽기를 시작 합니다. Hello 판독기에 연결 되 면이 오프셋된 toohello 이벤트 허브 toospecify hello 위치는 toostart 읽기에 전달 합니다. 이러한 방식으로 다운스트림 응용 프로그램에 의해 "완료"로 검사점 tooboth 표시 이벤트를 사용할 수 있습니다 및 tooprovide 복원 력 서로 다른 컴퓨터에서 실행 되는 독자 간의 장애 조치 하는 경우 발생 합니다. 이 검사점 설정 프로세스에서 더 낮은 오프셋을 지정 하 여 가능한 tooreturn tooolder 데이터를입니다. 이 메커니즘을 통해 검사점을 지정하면 장애 조치 복원력 및 제어된 이벤트 스트림 재생 모두를 사용할 수 있습니다.

### <a name="common-consumer-tasks"></a>일반 소비자 작업

모든 Event Hubs 소비자는 상태 인식 양방향 통신 채널인 AMQP 1.0 세션을 통해 연결됩니다. 각 파티션에 파티션별로 분리 된 이벤트의 hello 전송을 용이 하 게 하는 AMQP 1.0 세션입니다.

#### <a name="connect-tooa-partition"></a>Tooa 파티션에 연결 합니다.

Toopartitions를 연결할 경우에 임대는 일반적인 방법은 toouse 메커니즘 toocoordinate 판독기 연결 toospecific 파티션을 합니다. 이러한 방식으로 있기는 소비자 그룹 toohave 하나만 활성 독자의 모든 파티션에 대 한. 검사점 설정, 임대 및 관리 판독기 hello를 사용 하 여 간결 [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) .NET 클라이언트에 대 한 클래스입니다. 이벤트 프로세서 호스트 hello 지능형 소비자 에이전트인입니다.

#### <a name="read-events"></a>읽기 이벤트

특정 파티션에 대해 AMQP 1.0 세션 및 링크를 열면 이벤트가 toohello AMQP 1.0 클라이언트에서 이벤트 허브 서비스 hello에 전달 됩니다. 이 배달 메커니즘은 HTTP GET과 같은 풀 기반 메커니즘보다 더 낮은 대기 시간 및 더 높은 처리량을 사용합니다. 이벤트 toohello 클라이언트 전송 되므로, 각 이벤트 데이터 인스턴스 hello 이벤트 시퀀스에 사용 되는 toofacilitate 검사점을 설정 하는 hello 오프셋, 시퀀스 번호 같은 중요 한 메타 데이터를 포함 합니다.

이벤트 데이터:
* Offset
* 시퀀스 번호
* body
* 사용자 속성
* 시스템 속성

이 프로그램 책임 toomanage hello 오프셋입니다.

## <a name="capacity"></a>용량

이벤트 허브는 확장성이 높은 병렬 인프라를 갖추고 이며 몇 가지 주요 요인을 tooconsider 크기 조정을 하 고 크기를 조정할 수 있습니다.

### <a name="throughput-units"></a>처리량 단위

이벤트 허브의 처리 용량은 hello에 의해 제어 됩니다 *처리량 단위*합니다. 처리량 단위는 미리 구입한 용량의 단위입니다. 단일 처리량 단위는 다음 용량 hello를 포함 되어 있습니다.

* 수신: too1 초당 1MB 또는 두 번째 이벤트 / 초 (중 먼저)를
* 초당 too2 MB를 송신:

수신 스로틀 되는 처리량 단위 구입 hello의 hello 용량을 초과 및 [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) 반환 됩니다. 송신 제한 예외가 발생 하지는 않지만 여전히 제한 toohello 용량 hello 구입한 처리량 단위입니다. 게시 속도 예외가 받거나 toosee 송신을 예상할 수 있는지 toocheck hello 네임 스페이스에 대해 구입한 처리량 단위 수입니다. 처리량 단위 hello 관리할 수 있습니다 **배율** hello에 hello 네임 스페이스의 블레이드에서 [Azure 포털](https://portal.azure.com)합니다. 처리량 단위 hello를 사용 하 여 프로그래밍 방식으로 관리할 수도 있습니다 [이벤트 허브 Api](event-hubs-api-overview.md)합니다.

처리량 단위는 시간당 요금이 청구되며 미리 구입됩니다. 구입하면, 처리량 단위는 최소 한시간으로 청구됩니다. Too20 위로 처리량 단위는 이벤트 허브 네임 스페이스에 대 한 구입할 수 있습니다 및 hello 네임 스페이스의 모든 이벤트 허브에서 공유 됩니다.

Azure 지원에 문의 하 여 too100 처리량 단위를 20 개에서 더 많은 처리량 단위를 구입할 수 있습니다. 이보다 많은 경우, 100개의 처리량 단위 블록도 구입할 수 있습니다.

처리량 단위와 파티션 tooachieve 최적의 눈금 균형을 조정 하는 것이 좋습니다. 단일 파티션에는 처리량 단위 하나의 최대 크기가 있습니다. hello 처리량 단위 수를 보다 작거나 같은 toohello 이벤트 허브의 파티션 수가 있습니다.

Event Hubs 가격에 대한 자세한 내용은 [Event Hubs 가격](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.

## <a name="next-steps"></a>다음 단계

이벤트 허브에 대 한 자세한 내용은 다음 링크는 hello 방문.

* [Event Hubs 자습서][Event Hubs tutorial] 시작
* [Event Hubs 프로그래밍 가이드](event-hubs-programming-guide.md)
* [Event Hubs의 가용성 및 일관성](event-hubs-availability-and-consistency.md)
* [Event Hubs FAQ](event-hubs-faq.md)
* [Event Hubs 샘플][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Event Hubs 샘플]: https://github.com/Azure/azure-event-hubs/tree/master/samples
