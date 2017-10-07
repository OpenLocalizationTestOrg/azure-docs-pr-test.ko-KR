---
title: "비동기 메시징 aaaService 버스 | Microsoft Docs"
description: "Azure Service Bus 비동기 메시지에 대한 설명입니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>비동기 메시징 패턴 및 고가용성

비동기 메시징은 다양한 방식으로 구현할 수 있습니다. 큐, 토픽 및 구독으로 Azure Service Bus는 저장소 및 전달 메커니즘을 통해 비동기를 지원합니다. 일반 (동기) 작업에서 메시지 tooqueues 항목과 보내고 큐와 구독에서 메시지를 수신 합니다. 작성하는 응용 프로그램은 항상 사용 가능한 이러한 엔터티에 따라 다릅니다. Tooa 다양 한 상황 인해 hello 엔터티 상태 변경 방법 tooprovide 대부분의 요구 사항을 충족 시킬 수 있는 제한 된 기능 엔터티가 필요 합니다.

일반적으로 응용 프로그램 비동기 메시징 패턴 tooenable 여러 통신 시나리오를 사용합니다. 클라이언트 전송할 수 있는 메시지 tooservices hello 서비스가 실행 되지 않는 경우에 응용 프로그램을 빌드할 수 있습니다. 통신 버스트 발생 하는 응용 프로그램에 대 한 큐 위치 toobuffer 통신을 제공 하 여 로드 수준 hello를 수 있습니다. 마지막으로 얻을 수 있습니다 단순 하지만 효율적인 부하 분산 장치 toodistribute 메시지 여러 컴퓨터에서.

이러한 엔터티 중 아무 메서드나 순서 toomaintain 가용성의 다양을 한 다른 방법으로 이러한 엔터티 수 지속형 메시징 시스템에 사용할 수 없는 표시 되는 것이 좋습니다. 일반적으로 hello 엔터티는 사용자가 작성 한 가지 방법으로 다음 hello 사용할 수 없는 tooapplications 참조 했습니다.

* 없습니다 toosend 메시지입니다.
* 없습니다 tooreceive 메시지입니다.
* 없습니다 toomanage 엔터티 (만들기, 검색, 업데이트 또는 엔터티를 삭제) 합니다.
* 없습니다 toocontact hello 서비스입니다.

각 이러한 오류에 대 한 다른 오류 모드가 일정 수준의 제한 된 기능에는 응용 프로그램 toocontinue tooperform 작업할 수 있는 있습니다. 예를 들어 메시지를 보낼 수 있지만 받지 않는 시스템은 고객의 주문을 받을 수 있지만 이러한 주문을 처리할 수 없습니다. 이 항목에서는 발생할 수 있는 잠재적인 문제 및 이러한 문제를 줄이는 방법을 설명합니다. 서비스 버스에는 여러을 선택 해야 하는 완화 기능이 도입 되었습니다 및 hello hello 적용 되는 규칙 옵트인 이러한 완화 기능의 사용 절차도 설명 합니다.

## <a name="reliability-in-service-bus"></a>서비스 버스의 안정성
여러 가지 toohandle 메시지 및 엔터티 문제 및 hello 이러한 완화 기능의 적절 한 사용과 관련 된 지침도 있습니다. toounderstand hello 지침 서비스 버스에서 발생 가능한 오류를 먼저 이해 해야 합니다. Azure 시스템의 toohello 디자인 인해 이러한 문제가 모두 경향이 toobe 수명이 짧은 합니다. 상위 수준에서 사용 불가 hello 다른 이유로 다음과 같이 나타납니다.

* 서비스 버스가 의존하는 외부 시스템에서 제한합니다. 제한은 계산 및 저장소 리소스와의 상호작용에서 발생합니다.
* 서비스 버스가 의존하는 시스템에서 발생하는 문제입니다. 예를 들어 저장소의 특정 부분에 문제가 발생할 수 있습니다.
* 단일 하위 시스템에서 서비스 버스의 오류입니다. 이 경우 계산 노드 일관성이 없는 상태에 액세스할 수 고 자체적으로 다시 시작 해야에 모든 엔터티가 이것이 tooload 균형 tooother 노드 있습니다. 단기간 동안 차례로 메시지 처리 속도가 느려질 수 있습니다.
* Azure 데이터 센터 내에서 서비스 버스의 오류입니다. hello 시스템 접근할 수 없거나 몇 분에서 길게는 몇 시간에 대 한 "치명적인 오류"입니다.

> [!NOTE]
> hello 용어 **저장소** Azure 저장소와 SQL Azure를 모두 의미할 수 있습니다.
> 
> 

서비스 버스는 이런 문제에 대한 다양한 완화 방법을 포함합니다. 각 문제 및 개별 완화 기능 hello 다음 섹션에 설명 합니다.

### <a name="throttling"></a>제한
서비스 버스로 제한을 사용하면 공동으로 메시지 속도를 관리할 수 있습니다. 각 개별 서비스 버스 노드가 여러 엔터티가 있습니다. 이러한 각 엔터티 CPU, 메모리, 저장소 및 기타 패싯과 기초로 하 여 hello 시스템에서 요구를 하도록 만듭니다. 패싯이 정의된 임계값을 초과하는 사용을 감지하면 서비스 버스는 지정된 요청을 거부할 수 있습니다. hello 호출자가 받을 [ServerBusyException] [ ServerBusyException] 및 10 초 후 다시 시도 합니다.

한 완화 수단으로 hello 코드 읽기 hello 오류 하 고 10 초 이상에 대 한 hello 메시지의 다시 시도 중지 해야 합니다. Hello 오류 hello 고객 응용 프로그램의 여러 부분에서이 오류가 발생할 수 있으므로 각 독립적으로 실행 한다는 하지 hello 재시도 논리 것으로 예상 됩니다. hello 코드 hello 제한 가능성을 분할 된 큐 또는 항목을 사용 하 여 줄일 수 있습니다.

### <a name="issue-for-an-azure-dependency"></a>Azure 종속성에서 발생하는 문제
Azure 내의 다른 구성 요소에는 서비스 문제가 있는 경우도 있습니다. 예를 들어 서비스 버스가 사용하는 시스템이 업그레이드되는 경우 해당 시스템은 일시적으로 기능이 축소될 수 있습니다. 이러한 유형의 문제를 정기적으로 서비스 버스 주위 toowork 조사 하 여 완화 기능을 구현 합니다. 이러한 완화의 부작용도 물론 나타납니다. 예를 들어 toohandle 일시적인 저장소 문제, 서비스 버스 메시지 보내기 작업 toowork를 일관 되 게 허용 하는 시스템을 구현 합니다. Hello 완화에서는 toohello 이기 때문 보낸된 메시지 too15 분 tooappear hello 영향을 받는 큐 또는 구독에서 차지 하 고 수신 작업에 대 한 준비가 수 있습니다. 일반적으로 엔터티에는 대부분 이 문제가 발생하지 않습니다. 그러나 Azure 내에서 서비스 버스에 hello 엔터티 수를 지정 된,이 완화 기능이 필요한 경우도 서비스 버스 고객의 작은 하위 집합에 대 한 합니다.

### <a name="service-bus-failure-on-a-single-subsystem"></a>단일 하위 시스템에서 서비스 버스 오류
모든 응용 프로그램의 경우 일치 하지 않는 서비스 버스 toobecome의 내부 구성이 될 수 있습니다. 서비스 버스에서이 감지한 경우 hello 응용 프로그램 tooaid 무슨 상황이 진단에서 데이터를 수집 합니다. Hello 데이터 수집 되 면 hello 응용 프로그램은 다시 시작 시도가 tooreturn 것 tooa 일관 된 상태입니다. 이 프로세스는 비교적 빠르게 수행 되며 결과 toobe tooa 구성에 사용할 수 없는 몇 분 중단 시간이 일반적인 경우에 나타나는 엔터티의 훨씬 짧기 있습니다.

이러한 경우 hello 클라이언트 응용 프로그램에서는 오류가 발생 하는 [System.TimeoutException] [ System.TimeoutException] 또는 [MessagingException] [ MessagingException] 예외입니다. 서비스 버스에 자동화 된 클라이언트 다시 시도 논리의 hello 형태로이 문제에 대 한 완화 기능이 포함 되어 있습니다. Hello 다시 시도 기간이 지 났 고 hello 메시지가 배달 되지 않은와 같은 다른 기능을 사용 하 여 탐색할 수 있습니다 [네임 스페이스 쌍이][paired namespaces]합니다. 쌍을 이루는 네임스페이스에는 이 문서에서 설명하는 다른 주의 사항이 있습니다.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Azure 데이터 센터 내에서 서비스 버스의 오류
Azure 데이터 센터에서 실패에 대 한 hello 가장 큰 이유는 서비스 버스 또는 종속 시스템의 업그레이드 배포 실패 합니다. Hello 플랫폼은 성숙 되어 이러한 유형의 오류 hello 가능성 감소 했습니다. 데이터 센터 오류가 hello 다음을 포함 하는 이유로 발생할 수 있습니다.

* 전기 중단(전력 공급 및 전력 생산 불가).
* 연결.(클라이언트와 Azure 간에 인터넷 끊김)

두 경우 모두 자연 또는 인위적 재해 hello 문제를 발생합니다. 이 toowork 계속 메시지를 보낼 수, 사용할 수 있는지 확인 하 고 [네임 스페이스 쌍이] [ paired namespaces] tooenable 메시지 전송 toobe tooa 두 번째 위치 중 hello 기본 위치는 정상 다시 합니다. 자세한 정보는 [Service Bus 중단 및 재해로부터 응용 프로그램을 보호하는 모범 사례][Best practices for insulating applications against Service Bus outages and disasters]를 참조하세요.

## <a name="paired-namespaces"></a>쌍을 이루는 네임스페이스
hello [네임 스페이스 쌍이] [ paired namespaces] 기능은 있는 시나리오를 지원 합니다. 서비스 버스 엔터티 또는 데이터 센터 내에서 배포 수 없게 합니다. 이 이벤트는 자주 발생 하는 동안 분산된 시스템도 준비 해야 toohandle 최악의 시나리오입니다. 일반적으로 이 이벤트는 서비스 버스가 의존 하는 일부 요소가 수명이 짧기 때문에 발생합니다. 응용 프로그램 가용성 toomaintain 중단이 발생 하는 동안 서비스 버스를 사용할 수 있습니다 toohost 별도 데이터 센터에 두 개의 별도 네임 스페이스는 메시징 엔터티. 이 섹션의 나머지 부분은 hello hello 다음 용어를 사용 합니다.

* 기본 네임 스페이스: hello 네임 스페이스는 응용 프로그램 상호 작용, 송신 및 수신 작업입니다.
* 보조 네임 스페이스: hello 백업 toohello 기본 네임 스페이스 역할을 하는 네임 스페이스입니다. 응용 프로그램 논리는 이 네임스페이스 상호작용하지 않습니다.
* 장애 조치 간격: hello 양의 시간 tooaccept hello 응용 프로그램 하기 전에 일반적인 오류가 hello 기본 네임 스페이스 toohello 보조 네임 스페이스에서 전환 합니다.

쌍을 이루는 네임스페이스는 *가용성 보내기*를 지원합니다. 가용성 유지 능력 toosend hello 메시지를 보냅니다. toouse 보내기 가용성 응용 프로그램 요구 사항을 준수 하는 hello를 충족 해야 합니다.

1. Hello 기본 네임 스페이스에서 메시지 수신만 됩니다.
2. 지정 된 큐 또는 항목으로 전송 된 메시지 tooa 잘못 된 순서로 도착할 수 있습니다.
3. 세션 내의 메시지가 잘못된 순서로 도착할 수 있습니다. 세션의 정상적인 기능에 문제가 생겼습니다. 이 응용 프로그램이 세션 toologically 그룹 메시지를 사용 하는 것을 의미 합니다.
4. 세션 상태 hello 기본 네임 스페이스에만 유지 됩니다.
5. hello 기본 큐는 온라인 상태로 전환 하 고 hello 보조 큐 hello 기본 큐에 모든 메시지를 전달 하기 전에 메시지 수락을 시작할 수 있습니다.

hello Api, hello Api 구현 되는 방식 및 hello 기능을 사용 하는 샘플 코드를 보여 줍니다 hello 다음 섹션에 설명 합니다. 이 기능과 관련된 비용이 청구될 수 있습니다.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>hello MessagingFactory.PairNamespaceAsync API
hello 쌍 이룬된 네임 스페이스 기능에는 hello 포함 [PairNamespaceAsync] [ PairNamespaceAsync] 메서드 hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] 클래스:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Hello 작업이 완료 되 면 hello 네임 스페이스 쌍 이기도 대 한 시 완성 되었으며 tooact [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], 또는 [TopicClient] [ TopicClient] hello를 사용 하 여 만든 [MessagingFactory] [ MessagingFactory] 인스턴스. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] hello hello에 대 한 기본 클래스를 여러 쌍 유형의에 사용할 수 있는는 [MessagingFactory] [ MessagingFactory] 개체입니다. 현재 hello만 파생 클래스는 이름이 하나 [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], hello 보내기 가용성 요구 사항을 구현 하는 합니다. [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions]에는 서로 간에 빌드한 생성자의 집합이 있습니다. Hello 생성자 hello로 대부분의 매개 변수를 살펴보면 이해할 수 hello의 hello 동작 다른 생성자입니다.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

이러한 매개 변수에 있는 의미 다음 hello:

* *secondaryNamespaceManager*: 초기화 된 [NamespaceManager] [ NamespaceManager] 인스턴스 hello 보조 네임 스페이스에 대 한 해당 hello [PairNamespaceAsync] [ PairNamespaceAsync] 메서드도 tooset hello 보조 네임 스페이스를 사용할 수 있습니다. hello 네임 스페이스 관리자는 사용 되는 tooobtain hello 목록 hello 네임 스페이스와 toomake 존재 hello 필요한 백로그 큐에서 큐입니다. 이러한 큐가 존재하지 않는 경우 만들어집니다. [NamespaceManager] [ NamespaceManager] hello 기능 toocreate hello로 토큰 필요 **관리** 클레임입니다.
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] hello 보조 네임 스페이스에 대 한 인스턴스. hello [MessagingFactory] [ MessagingFactory] 개체는 사용 되는 toosend 경우 hello [EnableSyphon] [ EnableSyphon] 너무 속성이**true** , hello 백로그 큐에서 메시지를 수신 합니다.
* *backlogQueueCount*: hello 백로그 수가 toocreate 큐 대기 합니다. 이 값은 적어도 1이어야 합니다. 메시지 toohello 백로그를 보낼 때 이러한 큐 중 하나가 임의로 선택 됩니다. Hello 값 too1를 설정한 경우 하나의 큐 수 있습니다 사용할 적이 있습니다. 이런 경우가 발생 하 고 오류를 생성 하는 hello 백로그 큐 하나를 hello 클라이언트 수 tootry 다른 백로그 큐 아니며 toosend 메시지 실패할 수 있습니다. 이 값 toosome 더 큰 값 및 기본 hello 값 too10를 설정 하는 것이 좋습니다. 이 tooa 더 높은 바꾸거나 데이터 크기에 따라 값이 낮을수록 매일 보내는 응용 프로그램. 각 백로그 큐는 메시지의 too5 GB를 보유할 수 있습니다.
* *failoverInterval*:는 toohello 보조 네임 스페이스를 통해 모든 단일 엔터티를 전환 하기 전에 hello 기본 네임 스페이스에서 실패에 허용 되는 시간의 hello 크기입니다. 장애 조치는 엔터티 단위로 발생합니다. 단일 네임스페이스의 엔터티는 주로 서비스 버스 내의 다른 노드에 있습니다. 한 엔터티의 오류가 다른 오류를 의미하지는 않습니다. 이 값을 너무 설정할 수[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello 첫 번째, 일시적이 지 않은 오류 직후 보조 합니다. 하며 hello 장애 조치 타이머를 트리거하는 오류는 변수가 [MessagingException] [ MessagingException] 어떤 hello에 [IsTransient] [ IsTransient] 속성은 false, 또는 [System.TimeoutException][System.TimeoutException]합니다. 다른 예외와 같은 [UnauthorizedAccessException] [ UnauthorizedAccessException] hello 클라이언트를 올바르게 구성 되어를 나타내기 때문에 장애를 일으키지 않습니다. A [ServerBusyException] [ ServerBusyException] 않는 원인 장애 조치 되지 hello 올바른 패턴은 toowait 10 초이지만 시간 때문에 다음 hello 메시지를 다시 보냅니다.
* *enableSyphon*:는 특정 쌍이 되어야 또한 사이 펀 hello 보조 네임 스페이스 백 toohello 기본 네임 스페이스에서 메시지를 나타냅니다. 일반적으로 메시지를 보내는 응용 프로그램을 설정 해야이 값이 너무**false**; 메시지를 수신 하는 응용 프로그램 너무이 값을 설정 해야**true**합니다. hello 이유는 있는지 자주 적은 메시지 발신자 보다 수신자입니다. 수신자의 hello 수에 따라 toohave 단일 응용 프로그램 인스턴스 핸들 hello 사이 펀 의무를 선택할 수 있습니다. 여러 수신자를 사용하면 각 백로그 큐에 비용 청구의 영향을 미칩니다.

toouse 코드 hello, 기본 만들 [MessagingFactory] [ MessagingFactory] 인스턴스, 보조 [MessagingFactory] [ MessagingFactory] 인스턴스, 보조 [NamespaceManager] [ NamespaceManager] 인스턴스 및 [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] 인스턴스. hello 호출 hello 다음과 같이 간단할 수 있습니다.

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Hello에서 반환 된 작업을 hello 때 [PairNamespaceAsync] [ PairNamespaceAsync] 메서드가 완료 되 면 모든 항목이 설치 되 고 toouse 준비 합니다. Hello 작업이 반환 되기 전에 있습니다 완료 하지 않았을 수도 hello toowork 오른쪽 쌍으로 연결 하는 데 필요한 hello 백그라운드 작업을 모두 합니다. 결과적으로 시작 하지 않아야 hello 작업 반환 될 때까지 메시지를 송신 합니다. 잘못 된 자격 증명 또는 오류 toocreate hello 백로그 큐와 같은 오류가 발생 한 hello 작업이 완료 되 면이 예외가 throw 됩니다. Hello 큐 발견 되거나 hello를 검사 하 여 생성 된 hello 작업 반환 되 면 확인 [BacklogQueueCount] [ BacklogQueueCount] 속성에 사용자 [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] 인스턴스. 코드 앞에 오는 hello에 대 한 작업을 다음과 같이 나타납니다.

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>다음 단계
서비스 버스의 비동기 메시징 hello 기본 사항 학습 한, 했으므로 대 한 자세한 내용을 보려면 [네임 스페이스 쌍이][paired namespaces]합니다.

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
