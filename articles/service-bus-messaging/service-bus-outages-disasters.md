---
title: "작동 중단 및 재해 로부터 aaaInsulating Azure 서비스 버스 응용 프로그램 | Microsoft Docs"
description: "잠재적인 서비스 버스 가동 중단에 대해 tooprotect 응용 프로그램을 사용할 수 있습니다 하는 기술을 설명 합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>서비스 버스 가동 중단 및 재해로부터 응용 프로그램을 보호하기 위한 모범 사례
중요 응용 프로그램 계획 되지 않은 가동 중단 또는 재해의 hello 존재 여부에도 계속 작동 해야 합니다. 이 항목에서는 기술을 잠재적 서비스 중단 또는 재해 로부터 tooprotect 서비스 버스 응용 프로그램을 사용할 수 있습니다.

가동 중단은 Azure 서비스 버스의 일시적인 장애가 hello로 정의 됩니다. hello 중단 메시징 저장소 또는 전체 데이터 센터에도 hello와 같은 서비스 버스의 일부 구성 요소에 영향을 줄 수 있습니다. Hello 문제가 해결 된 후 서비스 버스 다시 사용할 수 있습니다. 일반적으로 가동 중단으로 인해 메시지나 기타 데이터는 손실되지는 않습니다. 구성 요소 실패의 예로 hello는 특정 메시징 저장소를 사용할 수 있습니다. 데이터 센터 전체가 가동 중단의 예로 hello 데이터 센터 또는 결함이 있는 데이터 센터 네트워크 스위치의 전원 오류. 가동 중단 며칠에서 몇 분 tooa 지속 될 수 있습니다.

서비스 버스 배율 단위 또는 데이터 센터 hello 영구 손실 재해 정의 되어 있습니다. hello 데이터 센터 하지을 사용할 수 있게 다시 수도 있습니다. 일반적으로 재해가 발생하면 메시지나 기타 데이터의 일부 또는 전체를 잃게 됩니다. 재해의 예로는 화재, 홍수 또는 지진이 있습니다.

## <a name="current-architecture"></a>현재 아키텍처
서비스 버스 여러 메시징 저장소 toostore 전송 된 메시지를 tooqueues 또는 항목을 사용 합니다. 분할 되지 않은 큐 또는 항목 메시지 저장소 tooone를 할당 됩니다. 이 메시지 저장소를 사용할 수 없게 되면 해당 큐 또는 항목의 모든 작업이 실패하게 됩니다.

모든 서비스 버스 메시징 엔터티(큐, 항목, 릴레이)는 데이터센터와 연결된 서비스 네임스페이스에 상주합니다. 서비스 버스의 데이터를 자동 지리적 복제를 사용 하지 않는 될 수 없습니다 네임 스페이스 toospan 여러 데이터 센터.

## <a name="protecting-against-acs-outages"></a>ACS 가동 중단으로부터 보호
ACS 자격 증명을 사용하는 경우 ACS를 사용할 수 없게 되면 클라이언트가 토큰을 가져올 수 없게 됩니다. ACS가 작동 해제 hello 시 한 토큰이 있는 클라이언트 hello 토큰 만료 될 때까지 toouse 서비스 버스를 계속 수 있습니다. hello 기본 토큰 수명은 3 시간입니다.

ACS 가동 중단 으로부터 tooprotect 공유 액세스 서명 (SAS) 토큰을 사용 합니다. 이 경우 hello 클라이언트 비밀 키로 자체 생성 된 토큰을 서명 하 여 서비스 버스에 직접 인증 합니다. 호출 tooACS 더 이상 필요 없는 합니다. SAS 토큰에 대한 자세한 내용은 [Service Bus 인증][Service Bus authentication]을 참조하세요.

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>메시지 저장소 오류로부터 큐와 항목 보호
분할 되지 않은 큐 또는 항목 메시지 저장소 tooone를 할당 됩니다. 이 메시지 저장소를 사용할 수 없게 되면 해당 큐 또는 항목의 모든 작업이 실패하게 됩니다. A 반면 hello에 큐를 분할 여러 조각으로 구성 됩니다. 각 조각은 서로 다른 메시징 저장소에 저장됩니다. 메시지 tooa 분할 된 큐 또는 항목을 보낼 때 서비스 버스 hello 메시지 tooone hello 조각에 할당 합니다. Hello 해당 메시징 저장소를 사용할 수 없는 서비스 버스 hello 메시지 tooa 다른 조각, 가능한 경우 기록 합니다. 분할된 엔터티에 대한 자세한 내용은 [분할된 메시징 엔터티][Partitioned messaging entities]를 참조하세요.

## <a name="protecting-against-datacenter-outages-or-disasters"></a>데이터센터 가동 중단 또는 재해로부터 보호
두 데이터 센터 사이의 장애 조치에 대 한 tooallow, 각 데이터 센터에서 서비스 버스 서비스 네임 스페이스를 만들 수 있습니다. 예를 들어 서비스 버스 서비스 네임 스페이스를 hello **contosoPrimary.servicebus.windows.net** hello 미국 북부/중부 지역에 있을 수 있습니다 및 **contosoSecondary.servicebus.windows.net**hello 미국 남부/중부 지역에 있을 수 있습니다. 서비스 버스 메시징 엔터티의 데이터 센터 가동 중단의 hello 존재에 액세스할 수 없으므로 유지 해야 하는 경우에 네임 스페이스 모두에 해당 엔터티를 만들 수 있습니다.

자세한 내용은 hello "Azure 데이터 센터 내에서 서비스 버스 실패" 섹션을 참조 하십시오. [비동기 메시징 패턴 및 고가용성][Asynchronous messaging patterns and high availability]합니다.

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>데이터센터 가동 중단 또는 재해로부터 릴레이 끝점 보호
릴레이 끝점의 지역 간 복제에는 서비스 버스 가동 중단의 hello 존재에 연결할 수 있는 릴레이 끝점 toobe 노출 하는 서비스 수 있습니다. tooachieve 지리적 복제 hello 서비스 다른 네임 스페이스에 두 릴레이 끝점을 만들 해야 합니다. hello 네임 스페이스는 서로 다른 데이터 센터에 있어야 합니다 및 hello 두 개의 끝점 이름과 달라 야 합니다. 예를 들어, 기본 끝점은 **contosoPrimary.servicebus.windows.net/myPrimaryService**에서 연결할 수 있고 이에 상응하는 보조 끝점은 **contosoSecondary.servicebus.windows.net/mySecondaryService**에서 연결할 수 있습니다.

hello 서비스는 다음 두 끝점에서 수신 대기 하 고는 클라이언트 hello 서비스 중 하나를 호출할 수 있습니다. 클라이언트 응용 프로그램은 임의로 hello 기본 끝점으로 hello 릴레이 중 하나를 선택 하 고 요청 toohello 활성 끝점을 보냅니다. Hello 작업이 오류 코드와 함께 실패 하면 해당 hello 릴레이 끝점을 사용할 수 없으면이 오류가 나타냅니다. hello 응용 프로그램 채널 toohello 백업 끝점 열리고 hello 요청을 다시 실행 합니다. 활성 hello 및 hello 백업 끝점 역할을 전환 시점: hello 클라이언트 응용 프로그램에서는 hello 이전 활성 끝점이 toobe 새 백업 끝점이 hello와 hello 이전 백업 끝점 toobe hello 새 활성 끝점이 간주 합니다. 전송 작업이 모두 실패, hello 두 엔터티의 역할 hello 그대로 유지 하 고 오류가 반환 됩니다.

hello [헤더 블록이 릴레이 서비스 버스를 사용 하 여 지역 복제 메시지] [ Geo-replication with Service Bus relayed Messages] 샘플 tooreplicate 릴레이 하는 방법을 보여 줍니다.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>데이터센터 가동 중단 또는 재해로부터 큐 또는 항목 보호
복원 력 tooachieve 조정 된 메시징을 사용할 경우 데이터 센터 가동 중단 으로부터 서비스 버스에서는 두 방법: *활성* 및 *수동* 복제 합니다. 각 접근 방식에 대 한 지정 된 큐 또는 항목을 데이터 센터 중단의 hello 존재에 액세스할 수 있어야 하는 경우에 두 네임 스페이스에서 만들 수 있습니다. 두 엔터티 hello 점이 동일한 이름입니다. 예를 들어, 기본 큐는 **contosoPrimary.servicebus.windows.net/myQueue**에서 연결할 수 있고 이에 상응하는 보조 큐는 **contosoSecondary.servicebus.windows.net/myQueue**에서 연결할 수 있습니다.

Hello 응용 프로그램 영구 발신자-수신자 통신에 필요 하지 않으면 hello 응용 프로그램 내구성이 우수한 클라이언트 쪽 큐 tooprevent 메시지 손실 및 tooshield hello 보낸 모든 일시적인 서비스 버스 오류에서를 구현할 수 있습니다.

## <a name="active-replication"></a>능동 복제
능동 복제는 모든 작업에서 양쪽 네임스페이스의 엔터티를 사용합니다. 메시지를 보내는 모든 클라이언트가 보내는 hello의 두 복사본이 동일한 메시지입니다. 첫 번째 복사는 hello toohello 주 엔터티가 전송 됩니다 (예를 들어 **contosoPrimary.servicebus.windows.net/sales**), hello 메시지의 두 번째 복사본 hello toohello 보조 엔터티에 전송 됩니다 (예를 들어  **contosoSecondary.servicebus.windows.net/sales**).

클라이언트는 두 큐에서 모두 메시지를 받습니다. hello 수신기 프로세스는 메시지의 첫 번째 사본을 hello 및 hello 두 번째 사본은 표시 되지 않습니다. toosuppress 중복 메시지 hello 보낸 고유 식별자를 가진 각 메시지를 태그 지정 해야 합니다. Hello 메시지의 두 복사본 hello로 태그가 지정 되어야 동일한 식별자입니다. Hello를 사용할 수 있습니다 [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] 또는 [BrokeredMessage.Label] [ BrokeredMessage.Label] 속성 또는 사용자 지정 속성 tootag hello 메시지. hello 수신기 이미 수신 된 메시지의 목록을 유지 관리 해야 합니다.

hello [서비스 버스 조정 메시지를 사용 하 여 지역 복제] [ Geo-replication with Service Bus Brokered Messages] 샘플에서는 메시징 엔터티의 능동 복제를 보여 줍니다.

> [!NOTE]
> hello 능동 복제 접근 방식을 hello 작업 수가 두 배로 설정, 따라서이 방법은 toohigher 비용 될 수 있습니다.
> 
> 

## <a name="passive-replication"></a>수동 복제
Hello 오류가 없는 경우 수동 복제 hello 두 메시징 엔터티 중 하나만 사용합니다. 클라이언트는 hello 메시지 toohello 활성 엔터티를 보냅니다. Hello 연산을 hello 활성 엔터티 hello 데이터 센터 호스트 hello 활성 엔터티를 사용할 수 있는지를 나타내는 오류 코드와 함께 실패 하면 hello 클라이언트 hello 메시지 toohello 백업 엔터티의의 복사본을 보냅니다. 이때 hello 활성 및 백업 엔터티 hello 역할 전환: hello 보내는 클라이언트 hello 이전 활성 엔터티 toobe hello 새 백업 엔터티로 간주 되며 이전 백업 엔터티 hello hello 새 활성 엔터티로 합니다. 전송 작업이 모두 실패, hello 두 엔터티의 역할 hello 그대로 유지 하 고 오류가 반환 됩니다.

클라이언트는 두 큐에서 모두 메시지를 받습니다. 해당 hello 수신기 동일 메시지, hello hello의 두 복사본을 받을 가능성이 있기 때문에 수신기 중복 메시지를 표시 하지 않아야 합니다. 표시 하지 않을 수 hello 마찬가지 능동 복제에 대해 설명 하는 방식으로 복제 합니다.

일반적으로 대부분의 경우 하나의 작업만 수행되기 때문에 수동 복제가 능동 복제보다 더 경제적입니다. 대기 시간, 처리량 및 금전적 비용은 동일한 toohello 복제 되지 않은 시나리오 됩니다.

수동 복제를 사용할 때는 hello에 다음과 같은 시나리오 메시지 수 손실 또는 수신 될 두 번:

* **메시지 지연 또는 손실**: hello 보낸 메시지 m1 toohello 기본 큐를 성공적으로 전송 하 고 다음 hello 큐가 hello 수신기 m 1에서 수신 하기 전에 사용할 수 없는 것으로 가정 합니다. hello 보낸 사람 이어서 나타나는 메시지 m2 toohello 보조 큐를 보냅니다. Hello 기본 큐를 일시적으로 사용할 수 없는 경우 hello 수신기 hello 큐를 다시 사용할 수 있게 m 1을 받습니다. 재해 발생 시 hello 수신기 m 1을 받지 못할 수 있습니다.
* **중복 수신**: 해당 hello 보내는 메시지 m toohello 기본 큐를 가정 합니다. 서비스 버스 m 처리 되었지만 toosend 응답 실패 합니다. 보내기 작업의 제한 시간에 hello, hello 보낸 사람 m toohello 보조 큐의 동일한 복사본을 보냅니다. Hello 약 hello에는 m의 두 사본을 모두 받습니다 이면 hello 수신기 수 tooreceive hello m의 첫 번째 복사본 hello 기본 큐를 사용할 수 없게 되기 전에 동시 합니다. 이면 hello 수신기 수 tooreceive hello m의 첫 번째 복사본 hello 기본 큐를 사용할 수 없게 되기 전에 hello 수신기 처음 m의 두 번째 복사본 hello만를 수신 하지만 기본 큐 hello 사용 가능 해지면 m의 두 번째 복사본을 받습니다.

hello [서비스 버스를 사용 하 여 지역 복제 브로커 메시지] [ Geo-replication with Service Bus Brokered Messages] 샘플에서는 메시징 엔터티의 수동 복제를 보여 줍니다.

## <a name="next-steps"></a>다음 단계
다음이 문서를 참조 하는 toolearn 재해 복구에 대 한 자세한 정보:

* [Azure SQL Database 비즈니스 연속성][Azure SQL Database Business Continuity]
* [Azure용 복원 응용 프로그램 디자인][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
