---
title: "aaaAzure 저장소 큐 및 서비스 버스 큐-비교 및 대조 | Microsoft Docs"
description: "Azure에서 제공하는 두 가지 유형의 큐 사이의 차이점과 유사점을 분석합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Azure 큐 및 Service Bus 큐 - 비교 및 대조
이 문서에서는 hello 차이점과 유사점 hello 두 종류의 Microsoft Azure에서 현재 제공 하는 큐: 저장소 큐 및 서비스 버스 큐입니다. 이 정보를 사용 하 여 비교 및 대비 hello 기술의 보다 합리적인된 결정 최상의 솔루션에 대 한 요구 사항에 맞는 수 toomake 수 있습니다.

## <a name="introduction"></a>소개
Azure는 **Storage 큐** 및 **Service Bus 큐**의 두 가지 큐 유형을 지원합니다.

**저장소 큐**, hello 포함 되어 [Azure 저장소](https://azure.microsoft.com/services/storage/) 인프라 간단한 REST 기반 GET/PUT/PEEK 인터페이스 내와 서비스 간에 안정적이 고 지속적인 메시징을 제공 합니다.

**Service Bus 큐**는 더 폭넓은 [Azure 메시징](https://azure.microsoft.com/services/service-bus/) 인프라의 일부이며, 큐뿐 아니라 게시/구독과 여러 고급 통합 패턴도 지원합니다. 서비스 버스 큐/항목/구독에 대 한 자세한 내용은 참조 hello [서비스 버스의 개요](service-bus-messaging-overview.md)합니다.

두 큐 기술이 동시에 존재하고 있지만, Storage 큐가 Azure Storage 서비스를 기반으로 구축된 전용 큐 저장소 메커니즘으로 먼저 소개되었습니다. 서비스 버스 큐는 "메시징" 인프라 설계 toointegrate 응용 프로그램 또는 여러 통신 프로토콜, 데이터 계약, 트러스트 도메인 및 네트워크 환경에 걸쳐 있을 수 있는 응용 프로그램 구성 요소 보다 광범위 한 hello 위에 구축 됩니다.

## <a name="technology-selection-considerations"></a>기술 선택 시 고려 사항
저장소 큐와 서비스 버스 큐는 현재 Microsoft Azure에서 제공 하는 서비스 큐는 hello 메시지의 구현입니다. 각 보안 개체 조금 다른 기능 집합 즉, 하나를 선택 또는 기타 hello 하거나 특정 솔루션 또는 비즈니스/기술 문제를 해결 중인 hello 요구에 따라 둘 다 사용할 수 있습니다.

지정된 된 솔루션에 대 한 hello 목적에 맞는 큐 기술을 결정할 때 솔루션 설계자 및 개발자 hello 다음과 같은 권장 사항을 고려해 야 합니다. 자세한 내용은 hello 다음 섹션을 참조 하세요.

솔루션 설계자/개발자라면 다음과 같은 경우 **Storage 큐의 사용을 고려해야** 합니다.

* 응용 프로그램 여기서 hello 메시지 수명이 7 일 미만인 큐에 80GB의 메시지를 저장 해야 합니다.
* 응용 프로그램 tootrack 진행률을 서빙 직원을 위한 hello 큐 내부의 메시지를 처리 합니다. 메시지를 처리 하는 hello 자가 충돌할 경우 유용 합니다. 이후 작업자는 hello 이전 작업 자가 종료 한 위치에서 해당 정보 toocontinue를 유도할 수 있습니다.
* 서버 쪽 로그가 모든 큐에 대해 실행 하는 hello 트랜잭션이 필요 합니다.

솔루션 설계자/개발자라면 다음과 같은 경우 **Service Bus 큐를 사용하는 것을 고려해야** 합니다.

* 솔루션은 toopoll hello 큐 필요 없이 수 tooreceive 메시지 여야 합니다. 서비스 버스를 통해 hello를 통해 수행할 수 있습니다 hello 긴 폴링의 사용 하 여 hello TCP 기반 프로토콜을 지 원하는 서비스 버스를 사용 하 여 작업을 수신 합니다.
* 솔루션 필요한 hello 큐 tooprovide는 보장 된 첫 번째-에-선입 선출 (FIFO) 순차적 전달 합니다.
* Azure 및 Windows Server(사설 클라우드)에서 대칭 환경을 사용하는 것이 좋습니다. 자세한 내용은 [Windows Server용 Service Bus](https://msdn.microsoft.com/library/dn282144.aspx)를 참조하세요.
* 솔루션에는 자동 중복 검색 수 toosupport 이어야 합니다.
* 원하는 병렬 장기 실행 스트리밍으로으로 응용 프로그램 tooprocess 메시지 (hello를 사용 하 여 스트림을 연결 된 메시지 [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) hello 메시지에 속성). 이 모델에서는 응용 프로그램을 사용 하는 hello 노드마다 스트리밍을 완료 것과 반대로 toomessages로 합니다. 스트림을 tooa 노드 소비를 지정 하는 경우 hello 노드는 트랜잭션을 사용 하 여 hello 응용 프로그램 스트림 상태 hello 상태를 검사할 수 있습니다.
* 큐에서 여러 메시지를 송신 또는 수신할 경우 솔루션에 트랜잭션 동작 및 원자성이 필요합니다.
* hello 응용 프로그램별 작업 부하의 hello 활성 시간 (TTL) 특성 hello 7 일의 기간을 초과할 수 있습니다.
* 응용 프로그램에서 64KB를 초과할 수 있는 메시지를 처리 하지만 희박 접근 방식을 256 KB 제한을 hello 합니다.
* 처리 하는 경우 요구 사항 tooprovide와 역할 기반 액세스 모델 toohello 큐 및 다른 권한/발신자와 수신자에 대 한 권한.
* 큐 크기는 80GB보다 크게 증가하지 않습니다.
* Toouse hello AMQP 1.0 표준 기반 메시징 프로토콜을 사용 하는 것이 좋습니다. AMQP에 대한 자세한 내용은 [Service Bus AMQP 개요](service-bus-amqp-overview.md)를 참조하세요.
* 큐 기반 지점 간 통신 tooa 메시지 교환 패턴을 사용 하면 일부 또는 전체의 독립적인 복사본을 수신 하며 각 추가 받는 사람 (구독자)의 원활한 통합 하는 최종 마이그레이션을 계획할 수 있습니다. 메시지 전송 toohello 큐. 후자의 hello 참조 toohello 게시/구독 기능이 서비스 버스에서 기본적으로 제공 합니다.
* 메시징 솔루션 있습니다 toobuild hello 추가 인프라 구성 요소에 대 한 hello 필요 없이 수 toosupport hello "에서 최대 1 회" 배달 보증 해야 합니다.
* Toobe 수 toopublish 선택한 메시지의 일괄 처리를 사용 합니다.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Storage 큐와 Service Bus 큐 비교
hello hello 다음 섹션에서에서 큐 기능의 논리적으로 그룹화 테이블과 hello 기능 저장소 큐와 서비스 버스 큐에서 사용할 수 있는 한 눈에 비교할 수 있습니다.

## <a name="foundational-capabilities"></a>기본 기능
이 섹션을 비교 하 여 일부 hello 기본 큐 기능 저장소 큐 및 서비스 버스 큐에서 제공 합니다.

| 비교 기준 | Storage 큐 | Service Bus 큐 |
| --- | --- | --- |
| 순서 보장 |**아니요** <br/><br>자세한 내용은 hello "추가 정보" 섹션에서에서 hello 첫 번째 참고를 참조 하세요.</br> |**예 - 선입선출(FIFO)**<br/><br>(hello) 사용 하 여 메시징 세션을 통해 |
| 전달 보장 |**최소 1회(At-Least-Once)** |**최소 1회(At-Least-Once)**<br/><br/>**최대 1회(At-Most-Once)** |
| 원자성 작업 지원 |**아니요** |**예**<br/><br/> |
| 수신 동작 |**비중단**<br/><br/>(새 메시지가 없을 경우 즉시 완료) |**시간 제한 있는/없는 차단**<br/><br/>(긴 폴링 또는 hello ["Comet 기술"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**비중단**<br/><br/>(hello를 통해 사용 하 여.NET 관리형 API만) |
| 푸시 스타일 API |**아니요** |**예**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) 및 **OnMessage** 세션 .NET API |
| 수신 모드 |**보기 및 임대** |**보기 및 잠금**<br/><br/>**수신 및 삭제** |
| 단독 액세스 모드 |**임대 기반** |**잠금 기반** |
| 임대/잠금 기간 |**30초(기본값)**<br/><br/>**7 일 (최대)** (hello를 사용 하 여 메시지 임대를 해제 하거나 갱신할 수 [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API입니다.) |**60초(기본값)**<br/><br/>Hello를 사용 하 여 메시지 잠금을 갱신할 수 [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API입니다. |
| 임대/잠금 정밀도 |**메시지 수준**<br/><br/>(각 메시지에는 다음 hello를 사용 하 여 hello 메시지를 처리 하는 동안 필요에 따라 업데이트할 수 있는 다른 시간 제한 값을 가질 수 있습니다 [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**큐 수준**<br/><br/>(각 큐에 메시지를 잠금 정밀도 적용 tooall 있지만 hello를 사용 하 여 hello 잠금을 갱신할 수 [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API입니다.) |
| 일괄 수신 |**예**<br/><br/>(명시적으로 지정 메시지 수를 tooa 최대 32 메시지의 메시지를 검색할 때) |**예**<br/><br/>(암시적으로 프리페치 속성을 사용 하도록 설정 하거나 명시적으로 hello를 통해 트랜잭션 사용) |
| 일괄 송신 |**아니요** |**예**<br/><br/>(hello) 사용 하 여 트랜잭션 또는 클라이언트 쪽 일괄 처리를 통해 |

### <a name="additional-information"></a>추가 정보
* Storage 큐에 포함된 메시지는 일반적으로 선입선출되지만 예를 들어, 메시지의 가시성 시간 제한 기간이 만료되는 경우(예: 처리 도중 클라이언트 응용 프로그램의 충돌)와 같이 때에 따라 순서가 바뀔 수 있습니다. Hello 메시지에 대 한 다른 작업자 toodequeue hello 큐에 다시 표시 되므로 hello 표시 제한 시간 만료 되 면 것입니다. 해당 시점에 hello 큐에 hello 새로 표시 메시지를 해질 수 있습니다 (toobe 다시 큐) 큐에 배치 된 후 원래 해당 메시지를 합니다.
* hello 보장 서비스 버스 큐의 FIFO 패턴 메시징 세션의 hello 사용 해야 합니다. Hello hello 응용 프로그램 이벤트는 hello에서 받은 메시지를 처리 하는 동안 충돌 **피킹 및 잠금** 모드, hello 다음에 큐 받는 사람이 메시징 세션을 허용 이후 실패 한 메시지 hello로 시작 됩니다 해당 활성 시간 (TTL) 기간이 만료 됩니다.
* 저장소 큐 toosupport 디자인된 표준 큐 시나리오를 응용 프로그램 구성 요소 tooincrease 확장성 및 실패에 대 한 허용 오차를 분리 하는 등, 부하 평준화 및 워크플로 프로세스 빌드와 합니다.
* 서비스 버스 큐 지원 hello *에서-최소 1 회* 배달 보증 합니다. 또한 hello *에서 최대 1 회* 의미 체계 세션 상태 toostore hello 응용 프로그램 상태를 사용 하 여 지원할 수 트랜잭션을 tooatomically를 사용 하 여 메시지를 수신 호스트 인스턴스와 hello 세션 상태를 업데이트 합니다.
* Storage 큐는 개발자와 작업 팀 모두에게 큐, 테이블, BLOB에 걸쳐 균일하고 일관적인 프로그래밍 모델을 제공합니다.
* 서비스 버스 큐는 단일 큐의 hello 컨텍스트에서 로컬 트랜잭션을 지원 합니다.
* hello **수신 및 삭제** 서비스 버스에서 지 원하는 모드 배당 보증 수준은 낮은 대신 메시징 작업 수 (및 연결 된 비용) hello 기능 tooreduce hello를 제공 합니다.
* 저장소 큐 메시지에 대 한 순서 대로 hello 기능 tooextend hello 임대의 임대를 제공합니다. 이렇게 하면 hello 작업자 toomaintain 짧은 임대에 메시지. 따라서 작업 자가 충돌할 경우 hello 메시지 신속 하 게 처리할 수 다시 다른 작업 자가 있습니다. 또한 작업 자가 tooprocess 임대 기간 현재 hello 보다 오래 대기 해야 하는 경우 hello 메시지 임대를 확장할 수 있습니다.
* 저장소 큐 표시 시간 제한을 설정할 수 있는 메시지 큐 하거나 hello 저장 시 설정할를 제공 합니다. 또한 실행 시 서로 다른 임대 값으로 메시지를 업데이트할 수 있습니다 및 hello에 대 한 메시지에 대해 서로 다른 업데이트 값 동일한 큐입니다. 서비스 버스 잠금 시간 제한은 큐 메타 데이터 hello에서는 정의 hello를 호출 하 여 hello 잠금을 갱신할 수 있습니다 [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) 메서드.
* 서비스 버스 큐의 차단 수신 작업에 대 한 최대 제한 시간 hello은 24 일입니다. 하지만 REST 기반 시간 제한의 경우 최대값이 55초입니다.
* 클라이언트 쪽 일괄 처리에서 제공 하면 서비스 버스 큐 클라이언트 toobatch 여러 메시지를 단일 전송 작업으로 합니다. 일괄 처리는 비동기 전송 작업에만 사용 가능합니다.
* Hello 200TB 한계 (계정을 가상화 하면 더 많은) 저장소 큐 및 무제한 큐 등의 기능 있도록 SaaS 공급자에 대 한 이상적인 플랫폼입니다.
* Storage 큐는 유연하고 성능이 위임된 액세스 제어 메커니즘을 제공합니다.

## <a name="advanced-capabilities"></a>고급 기능
이 섹션에서는 Storage 큐와 Service Bus 큐에서 제공하는 고급 기능을 비교합니다.

| 비교 기준 | Storage 큐 | Service Bus 큐 |
| --- | --- | --- |
| 예약 배달 |**예** |**예** |
| 배달 못한 메시지 자동 처리 |**아니요** |**예** |
| 큐 TTL(Time-to-Live) 값 증가 |**예**<br/><br/>(표시 시간 제한의 전체 업데이트를 통해) |**예**<br/><br/>(전용 API 함수를 통해 제공됨) |
| 포이즌 메시지 지원 |**예** |**예** |
| 전체 업데이트 |**예** |**예** |
| 서버 측 트랜잭션 로그 |**예** |**아니요** |
| 저장소 메트릭 |**예**<br/><br/>**순간 메트릭**: 가용성, TPS, API 호출 횟수, 오류 수 등에 대한 실시간 메트릭을 모두 실시간으로 제공합니다(분 단위로 집계되며 프로덕션에서 방금 발생한 일이 몇 분 안에 보고됨). 자세한 내용은 [저장소 분석 메트릭 정보](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics)를 참조하세요. |**예**<br/><br/>([GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)를 호출하여 대량 쿼리) |
| 상태 관리 |**아니요** |**예**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| 메시지 자동 전달 |**아니요** |**예** |
| 큐 삭제 기능 |**예** |**아니요** |
| 메시지 그룹 |**아니요** |**예**<br/><br/>(hello) 사용 하 여 메시징 세션을 통해 |
| 메시지 그룹당 응용 프로그램 상태 |**아니요** |**예** |
| 중복 검색 |**아니요** |**예**<br/><br/>(hello 보낸 사람 쪽에서 구성 가능) |
| 메시지 그룹 찾아보기 |**아니요** |**예** |
| ID별로 메시지 세션 가져오기 |**아니요** |**예** |

### <a name="additional-information"></a>추가 정보
* 두 큐 기술을 나중에 배달 하기 위해 예약할 메시지 toobe 사용 하도록 설정 합니다.
* 큐 자동 전달 hello 메시지를 사용 하는 해당 메시지 tooa 단일 큐는 hello 수신 응용 프로그램에서 큐 tooauto 정방향 수천 수 있습니다. 이 메커니즘 tooachieve 보안, 제어 흐름 및 각 메시지 게시자 간의 격리 저장소를 사용할 수 있습니다.
* Storage 큐는 메시지 콘텐츠의 업데이트를 지원합니다. Hello 마지막으로 알려진된 검사점부터 처음부터 시작 하는 대신 처리할 수 있도록 hello 메시지에 상태 정보를 유지 및 증분 진행률 업데이트에 대 한이 기능을 사용할 수 있습니다. 서비스 버스 큐와 hello를 활성화할 수 있습니다 메시지 세션의 hello 사용을 통해 동일한 시나리오입니다. 세션을 사용 하면 toosave 고 hello 응용 프로그램 처리 상태를 검색 (사용 하 여 [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) 및 [우편 번호](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [메일 데드](service-bus-dead-letter-queues.md), 즉 서비스 버스 큐에서 지 원하는 hello 수신 응용 프로그램에서 성공적으로 처리할 수 없는 메시지를 격리 하기 위해 수행 하거나 tooan 만료 기한 대상에 도달할 수 없는 경우 활성 시간 (TTL) 속성입니다. TTL 값 hello hello 큐에 머무르는 메시지 시간을 지정 합니다. 서비스 버스 hello 메시지 이동된 tooa 특수 큐 $DeadLetterQueue hello TTL 기간이 만료 되 면 호출 됩니다.
* 저장소 큐를 검사 하 여 hello 메시지 hello 응용 프로그램을 제거 하는 경우의 "포이즌" 메시지 toofind  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  hello 메시지의 속성입니다. 경우 **DequeueCount** 지정된 된 임계값 보다 크면 hello 응용 프로그램 hello 메시지 tooan 응용 프로그램 정의 "배달 못한 편지" 큐를 이동 합니다.
* 저장소 큐를 사용 하면 tooobtain 모든 트랜잭션을 hello에 대 한 자세한 로그 hello 큐에 대해 실행으로 메트릭을 집계 합니다. 이 옵션은 모두 디버깅과 응용 프로그램이 Storage 큐를 어떻게 사용하는지 이해하는 데 유용합니다. 또한 응용 프로그램 성능 튜닝 및 큐를 사용 하 여의 hello 비용을 감소 하는 데 유용 합니다.
* 서비스 버스에서 지 원하는 "메시지 세션"의 hello 개념 tooa 속하는 메시지는 메시지와 각 받는 사람 간의 세션 선호도 만들 지정된 된 받는 사람과 연결 된 특정 논리 그룹 toobe를 수 있습니다. 서비스 버스에서이 고급 기능 hello 설정 하 여 설정할 수 있습니다 [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) 메시지 속성을 합니다. 그런 다음 특정 세션 ID에서 수신 대기 하 고 hello 지정을 공유 하는 메시지 수 수신기 세션 식별자입니다.
* hello 자동으로 서비스 버스 큐에서 지 원하는 중복 검색 기능은 제거 전송 된 중복 메시지 tooa 큐 또는 항목의 hello hello 값에 따라 [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) 속성입니다.

## <a name="capacity-and-quotas"></a>용량 및 할당량
이 섹션의 hello 관점에서 서비스 버스 큐 및 저장소 큐 비교 [용량 및 할당량](service-bus-quotas.md) 적용 될 수 있습니다.

| 비교 기준 | Storage 큐 | Service Bus 큐 |
| --- | --- | --- |
| 최대 큐 크기 |**500TB**<br/><br/>(제한 된 tooa [단일 저장소 계정 용량](../storage/common/storage-introduction.md#queue-storage)) |**1GB too80**<br/><br/>(큐를 만들 때 정의 및 [분할 사용](service-bus-partitioning.md) – 참조 hello "추가 정보" 섹션) |
| 최대 메시지 크기 |**64KB**<br/><br/>(**Base64** 인코딩을 사용할 때 48KB)<br/><br/>Azure 큐 및 blob에 too200GB 단일 항목을 큐에 넣을 수 있습니다이 시점을 결합 하 여 큰 메시지를 지원 합니다. |**256KB** 또는 **1MB**<br/><br/>(헤더 및 본문 포함, 최대 헤더 크기: 64KB)<br/><br/>Hello에 따라 달라 집니다 [서비스 계층](service-bus-premium-messaging.md)합니다. |
| 최대 메시지 TTL |**7일** |**`TimeSpan.Max`** |
| 최대 큐 수 |**무제한** |**10,000**<br/><br/>(서비스 네임스페이스당, 확장 가능) |
| 최대 동시 클라이언트 수 |**무제한** |**무제한**<br/><br/>(만 100 동 신 연결 제한은 tooTCP 프로토콜 기반 통신 적용 됨) |

### <a name="additional-information"></a>추가 정보
* Service Bus의 경우 큐 크기 제한이 강제 적용됩니다. hello 최대 큐 크기 hello 큐를 만들 때 지정 되며 1gb와 80gb 사이의 값을 지정할 수 있습니다. Hello 큐를 만들 때 설정한 hello 큐 크기 값에 도달 하면 추가로 들어오는 메시지가 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. Service Bus의 할당량에 대한 자세한 내용은 [Service Bus 할당량](service-bus-quotas.md)을 참조하세요.
* Hello에 [표준 계층](service-bus-premium-messaging.md), 1, 2, 3, 4 또는 5GB 크기로 (hello 기본값은 1GB) 서비스 버스 큐를 만들 수 있습니다. Hello 프리미엄 계층에서는 큐 크기가 too80 GB 만들 수 있습니다. 표준에서 분할 계층 사용 (않는 hello 기본값), 서비스 버스에 대 한 지정한 각 GB 당 16 개의 파티션을 만듭니다. 따라서 크기 5GB 인 큐를 만든 경우 16 개의 파티션이 있는 hello 최대 큐 크기는 (5 * 16) = 80GB입니다. Hello에 항목을 확인 하 여 hello 분할 된 큐 또는 항목의 최대 크기를 볼 수 있습니다 [Azure 포털][Azure portal]합니다. Hello 프리미엄 계층에서 두 파티션은 큐당 생성 됩니다.
* 저장소 큐와 hello hello 메시지의 콘텐츠 하지 XML 안전한 경우 여야 **Base64** 인코딩됩니다. 경우 있습니다 **Base64**-hello 메시지 인코딩, hello 사용자 페이로드 too48 1536KB 64 KB 될 수 있습니다.
* Service Bus 큐의 경우 큐에 저장된 각 메시지가 헤더와 본문의 두 부분으로 구성됩니다. hello 메시지의 전체 크기 hello hello 최대 메시지 hello 서비스 계층에서 지 원하는 크기를 초과할 수 없습니다.
* 클라이언트 hello TCP 프로토콜을 통해 서비스 버스 큐와 통신할 때 hello 최대 동시 연결 tooa 단일 서비스 버스 큐는 too100 제한 합니다. 이 숫자는 보낸 사람과 받는 사람 사이에 공유됩니다. 이 할당량에 도달 하면 추가 연결에 대 한 후속 요청 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. REST 기반 API를 사용 하 여 toohello 큐를 연결 하는 클라이언트에이 제한 됩니다.
* 단일 서비스 버스 네임 스페이스에 10, 000 개 이상의 큐를 필요로 하는 경우 hello Azure 지원 팀에 문의 하 수 증가 요청 합니다. 서비스 버스 큐를 10, 000 이상 tooscale를 만들 수도 있습니다 hello를 사용 하 여 추가 네임 스페이스 [Azure 포털][Azure portal]합니다.

## <a name="management-and-operations"></a>관리 및 운영
이 섹션 저장소 큐 및 서비스 버스 큐에서 제공 하는 hello 관리 기능을 비교 합니다.

| 비교 기준 | Storage 큐 | Service Bus 큐 |
| --- | --- | --- |
| 관리 프로토콜 |**HTTP/HTTPS를 통한 REST** |**HTTPS를 통한 REST** |
| 런타임 프로토콜 |**HTTP/HTTPS를 통한 REST** |**HTTPS를 통한 REST**<br/><br/>**AMQP 1.0 표준(TCP 및 TLS)** |
| .NET API |**예**<br/><br/>(.NET 저장소 클라이언트 API) |**예**<br/><br/>(.NET Service Bus API) |
| 네이티브 C++ |**예** |**예** |
| Java API |**예** |**예** |
| PHP API |**예** |**예** |
| Node.js API |**예** |**예** |
| 임의 메타데이터 지원 |**예** |**아니요** |
| 큐 명명 규칙 |**Too63 자를**<br/><br/>(큐 이름의 문자는 소문자여야 함) |**Too260 자를**<br/><br/>(큐 경로 및 이름은 대/소문자가 구분되지 않음) |
| 큐 길이 가져오기 함수 |**예**<br/><br/>(근사값 메시지가 삭제 되지 않고 hello TTL 이후에 만료 되는 경우.) |**예**<br/><br/>(정확한 지정 시간 값) |
| 엿보기 기능 |**예** |**예** |

### <a name="additional-information"></a>추가 정보
* 저장소 큐 이름/값 쌍의 hello 형식에 적용 된 toohello 큐 설명 될 수 있는 임의의 특성에 대 한 지원을 제공 합니다.
* 두 큐 기술이 제공 하는 hello 기능 toopeek 메시지 toolock 필요 없이 it 큐 탐색기/브라우저 도구를 구현할 때 유용할 수 있습니다.
* 서비스 버스.NET hello 조정 향상 된 성능을 위해 메시징 Api 활용 전이중 TCP 연결 된 경우 HTTP를 통한 tooREST 비교 하 고 hello AMQP 1.0 표준 프로토콜을 지원 합니다.
* Storage 큐 이름은 3 ~ 63자로 지정할 수 있으며, 소문자, 숫자, 하이픈이 포함될 수 있습니다. 자세한 내용은 [큐 및 메타데이터 명명](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata)을 참조하세요.
* 서비스 버스 큐 이름 수를 too260 자와 덜 제한적인 명명 규칙 합니다. Service Bus 큐 이름에는 문자, 숫자, 마침표, 하이픈, 밑줄이 포함될 수 있습니다.

## <a name="authentication-and-authorization"></a>인증 및 권한 부여
이 섹션에서는 저장소 큐 및 서비스 버스 큐에서 지 원하는 hello 인증 및 권한 부여 기능에 설명 합니다.

| 비교 기준 | Storage 큐 | Service Bus 큐 |
| --- | --- | --- |
| 인증 |**대칭 키** |**대칭 키** |
| 보안 모델 |SAS 토큰을 통해 위임된 액세스. |SAS |
| ID 공급자 페더레이션 |**아니요** |**예** |

### <a name="additional-information"></a>추가 정보
* Hello 기술 큐의 모든 요청 tooeither 인증 되어야 합니다. 익명 액세스 가능한 공개 큐는 지원되지 않습니다. [SAS](service-bus-sas.md)를 사용하면 쓰기 전용 SAS, 읽기 전용 SAS 또는 모든 권한 SAS를 게시하여 이러한 시나리오에 대응할 수 있습니다.
* hello 인증 체계 저장소 큐 포함 되는 HMAC 해시 기반 메시지 인증 코드 ()는 대칭 키를 사용 하 여 hello 제공 hello s h A-256 알고리즘으로 계산 된 및로 인코딩된는 **Base64** 문자열입니다. Hello 해당 프로토콜에 대 한 자세한 내용은 참조 [hello Azure 저장소 서비스에 대 한 인증](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services)합니다. Service Bus 큐도 대칭 키를 사용하는 유사한 모델을 지원합니다. 자세한 내용은 [Service Bus에서 공유 액세스 서명 인증](service-bus-sas.md)을 참조하세요.

## <a name="conclusion"></a>결론
Hello 두 기술 더 깊이 이해를 확보 하 여 기반이 보다 합리적인된 결정 큐 기술을 toouse 수 toomake 시점과 됩니다. hello 때 toouse 저장소 큐 또는 Service Bus 큐에 명확 하 게 관련 된 결정 다양 한 요인에 따라 달라 집니다. 이러한 요소는 응용 프로그램 및 해당 아키텍처의 hello 개별 요구 사항에 크게 종속 될 수 있습니다. 응용 프로그램에서 이미 Microsoft Azure의 hello 핵심 기능을 사용 하는 경우 서비스 또는 필요 큐 크기가 80 GB 보다 큰 수 있는 간 기본 통신 및 메시징 해야 하는 경우에 특히 toochoose 저장소 큐를 원할 수 있습니다.

Service Bus 큐의 경우 세션, 트랜잭션, 중복 검색, 배달 못한 메시지 자동 처리, 지속성 높은 게시/구독 기능 등과 같은 다수의 고급 기능을 제공하므로, 하이브리드 응용 프로그램을 개발하는 중이거나 응용 프로그램에서 달리 이러한 기능을 요구할 때 바람직한 선택이 될 수 있습니다.

## <a name="next-steps"></a>다음 단계
다음 문서는 hello 자세한 지침 및 저장소 큐 또는 Service Bus 큐를 사용 하는 방법에 대 한 정보를 제공 합니다.

* [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)
* [어떻게 tooUse hello 큐 저장소 서비스](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Service Bus 조정된 메시징을 사용한 성능 향상의 모범 사례](service-bus-performance-improvements.md)
* [Azure Service Bus의 큐 및 토픽 소개(블로그 게시물)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [개발자 가이드 tooService 버스 hello](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Azure의 hello 큐 서비스를 사용 하 여](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

