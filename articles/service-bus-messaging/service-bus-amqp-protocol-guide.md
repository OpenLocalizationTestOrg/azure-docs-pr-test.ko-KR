---
title: "Azure 서비스 버스 및 이벤트 허브 프로토콜 설명서에서 aaaAMQP 1.0 | Microsoft Docs"
description: "프로토콜 가이드 tooexpressions 및 Azure 서비스 버스 및 이벤트 허브에서 AMQP 1.0의 설명"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure Service Bus 및 이벤트 허브 프로토콜 가이드의 AMQP 1.0

hello 고급 메시지 큐 프로토콜 1.0은 비동기적으로 안전 하 고 안정적으로 두 당사자 간에 메시지를 전송 하는 데 사용 되는 표준화 된 프레이밍 및 전송 프로토콜입니다. Azure 서비스 버스 메시징 및 Azure 이벤트 허브의 hello 기본 프로토콜입니다. 두 서비스 모두 HTTPS를 지원합니다. AMQP를 위해 에서도 지원 되는 hello 소유 SBMP 프로토콜은 더 이상 사용 되지 합니다.

AMQP 1.0은 미들웨어 공급 업체, 예: Microsoft 및 Red Hat hello 금융 서비스 업계 나타내는 JP Morgan Chase 등 많은 메시징 미들웨어 사용자와 연결 하는 광범위 한 산업 공동 작업의 hello 결과입니다. hello AMQP 프로토콜 및 확장 사양에 대 한 hello 기술 표준화 포럼 OASIS, 이며 ISO/IEC 19494로 국제 표준으로 공식 승인에 도달 했습니다.

## 목표

이 문서에서 간단 하 게 hello OASIS AMQP 기술 위원회에서 종료 하 고 현재 초안 확장 사양 중 작은 부분만 함께 hello AMQP 1.0 메시징 사양의 hello 핵심 개념을 요약 하 고 어떻게 Azure 서비스 버스를 설명 합니다. 구현 하 고 이러한 사양을 기반으로 합니다.

hello 목표는 모든 기존 AMQP 1.0 클라이언트 스택에 AMQP 1.0을 통해 Azure 서비스 버스를 통해 모든 플랫폼 toobe 수 toointeract에서 사용 하 여 모든 개발자입니다.

Apache Proton 또는 AMQP.NET Lite와 같은 일반적인 범용 AMQP 1.0 스택은 이미 모든 핵심 AMQP 1.0 제스처를 이미 구현하는 데 사용되고 있습니다. 이러한 기본 제스처 경우에 따라 상위 수준 API; 래핑됩니다. Apache의 Proton 옵션을 제공 두, 명령적 메신저 API hello 및 사후 액 터 API hello 합니다.

Hello 토론 다음에서 것으로 가정 AMQP 연결, 세션 및 링크와 hello 처리 프레임 전송 및 흐름 제어의 hello 관리 hello 해당 스택 (예: Apache Proton-c)에 의해 처리 됩니다 있는 경우에 많은 특정 필요 하지 않습니다. 응용 프로그램 개발자의 주의가 필요 합니다. 추상적 가정 hello 기능 tooconnect toocreate 등 몇 가지 API 기본 형식의 hello 존재 일종의 *보낸 사람* 및 *수신기* 다음 의몇가지셰이프를포함하는추상화개체`send()`및 `receive()` 작업을 각각.

메시지 찾아보기 또는 세션 관리와 같은 Azure Service Bus의 고급 기능을 설명할 때 AMQP 용어로 설명하기도 하지만 이와 같이 가정된 API 추상화를 기반으로 계층화된 의사 구현으로 설명하기도 합니다.

## AMQP란?

AMQP는 프레이밍 및 전송 프로토콜입니다. 프레이밍은 네트워크 연결 방향으로 흐르는 이진 데이터 스트림의 구조를 제공한다는 것을 의미합니다. 데이터의 고유 블록에 대 한 경계를 제공 하는 hello 구조 *프레임*, toobe 연결 hello 파티 간에 교환 합니다. hello 전송 기능 통신 당사자 양쪽 모두가 프레임은 전송 될 때, 및 때 전송 제한 완료에 대 한 공유에 대 한 이해를 설정할 수 있는지 확인 합니다.

만료 된 초안 이전 버전과 달리 hello AMQP 작업 그룹에 의해 생성 된 몇 가지 메시지 브로커에서 사용 중인 hello 작업 그룹의 최종, 하는 표준화 된 AMQP 1.0 프로토콜 메시지 브로커 또는 어떤 특정 토폴로지에의 hello 존재 규정 하지 않습니다. 메시지 브로커 내 엔터티의.

와 Azure 서비스 버스 큐 및 게시/구독 엔터티를 지 원하는 메시지 브로커와의 상호 작용에 대 한 대칭 피어-투-피어 통신에 대 한 hello 프로토콜을 사용할 수 있습니다. 또한 사용할 수 있습니다 메시징 인프라와 상호 작용을 위해 여기서 hello 상호 작용 패턴은 hello 경우 Azure 이벤트 허브와 마찬가지로 일반 큐와에서 다릅니다. 이벤트 허브 이벤트 tooit를 보내면 큐 처럼 작동 하지만 처럼 작동 직렬 저장소 서비스에서 읽는 경우 다소 테이프 드라이브와 유사합니다. hello 클라이언트 hello 사용 가능한 데이터 스트림으로 오프셋을 선택 하 고 해당 오프셋된 toohello 최신 사용 가능한에서 모든 이벤트 광고가 다음.

hello AMQP 1.0 프로토콜은 설계 된 toobe 설정 추가 사양을 tooenhance 그 기능을 확장할 수 있습니다. 이 문서에 설명 된 hello 세 확장 사양 이러한 경우를 설명 합니다. Hello 네이티브 AMQP TCP 포트 구성 어려울 수 있는 기존 HTTPS/Websocket 인프라에 대 한 통신을 위해 바인딩 사양의 정의 방법을 toolayer Websocket 통해 AMQP 합니다. Hello 요청/응답 메시징 인프라와 상호 작용 하기 위한 방식으로 관리 목적으로 또는 고급 tooprovide 기능, hello AMQP 관리 사양에 대 한 필요한 hello 기본 상호 작용 기본 형식을 정의 합니다. Hello AMQP 클레임 기반 보안 사양 페더레이션된 권한 부여 모델 통합을 위해 정의 방법을 tooassociate 및 링크와 관련 된 권한 부여 토큰을 갱신 합니다.

## 기본 AMQP 시나리오

이 섹션에서는 hello 연결, 세션 및 링크를 만들고 큐, 항목 및 구독 같은 서비스 버스 엔터티로부터 메시지 tooand 전송를 포함 하는 Azure 서비스 버스 AMQP 1.0의 기본 사용법을 설명 합니다.

AMQP가 작동 하는 방법에 대 한 가장 신뢰할 수 있는 소스 toolearn hello hello AMQP 1.0 사양 이지만 tooprecisely 가이드 구현과 tooteach hello 프로토콜이 아닌 hello 사양을 작성 되었습니다. 이 섹션에서는 Service Bus가 AMQP 1.0을 사용하는 방법을 설명하는 데 필요한 다양한 용어를 중점적으로 소개합니다. 더 포괄적인 소개 tooAMQP와 같은 AMQP 1.0의 광범위 한 토론을 검토할 수 있습니다 [비디오이 코스][this video course]합니다.

### 연결 및 세션

AMQP 호출 hello 프로그램 통신 *컨테이너*이러한; 포함 *노드*이며 hello 엔터티 해당 컨테이너 내에서 통신 합니다. 큐는 이러한 노드가 될 수 있습니다. AMQP; 노드 간에 여러 통신 경로 대 한 단일 연결을 사용할 수 있도록 멀티플렉싱에 대 한 허용 예를 들어 응용 프로그램 클라이언트 받을 수 있습니다 동시에 하나의 큐와 송신 tooanother 큐에서 hello를 통해 동일한 네트워크 연결 합니다.

![][1]

hello 네트워크 연결을 따라서 hello 컨테이너에 고정 합니다. Hello 컨테이너 수신 대기 하 고 인바운드 TCP 연결을 수락 하는 hello 받는 사람 역할의 아웃 바운드 TCP 소켓 연결 tooa 컨테이너를 만드는 hello 클라이언트 역할에 시작 됩니다. 연결 핸드셰이크가 hello hello 프로토콜 버전 협상, 선언 또는 전송 수준 보안 (TLS/SSL) 및 SASL를 기반으로 하는 hello 연결 범위에서 한 인증/권한 부여 핸드셰이크 hello 사용을 협상 포함 되어 있습니다.

Azure 서비스 버스에는 항상 TLS hello 사용을 해야합니다. TCP 연결 hello는 먼저로 중첩 TLS hello AMQP 프로토콜 핸드셰이크로 유입 되기 전에 및 hello 서버의 필수 업그레이드를 즉시 제공 되는 그에 따라 TCP 포트 5672 통해 연결도 지원 되는 연결 TCP 포트 5671 통해 지원 연결 tooTLS hello AMQP 사전 설정 된 모델을 사용 합니다. hello AMQP Websocket 바인딩 다음 동일 tooAMQP 5671 연결 수는 TCP 포트 443 통해 한 터널을 만듭니다.

Hello 연결 및 TLS를 설정한 후 서비스 버스는 두 가지 SASL 메커니즘 옵션을 제공 합니다.

* SASL 일반 자격 증명 tooa 서버 사용자 이름 및 암호를 전달 하기 위해 주로 사용 됩니다. Service Bus에는 계정이 없지만, 권한을 부여하고 키와 연결되어 있는 [공유 액세스 보안 규칙](service-bus-sas.md)이 있습니다. 규칙의 hello 이름이 hello 사용자 이름 및 hello 키로 사용 됩니다 (base 64로 인코딩된 텍스트) 처럼 hello 암호가 사용 됩니다. hello 연결에 허용 되는 hello 작동을 제어 하는 규칙을 선택 하는 hello와 관련 된 hello 권한을 합니다.
* SASL 익명 SASL 권한 부여 바이패스 하 고 hello 클라이언트가 toouse hello 클레임 기반 보안 (CBS) 모델 뒷부분에서 설명 하는 경우에 사용 됩니다. 이 옵션을 사용 클라이언트 연결 수를 설정할 수 익명으로 짧은 시간에 대 한는 hello 하는 동안 클라이언트 수만 상호 작용 hello CBS 끝점과 있으며 hello CBS 핸드셰이크를 완료 해야 합니다.

Hello 전송 연결이 설정 되 면 hello 컨테이너 각각을 선언 hello 최대 프레임 크기 기꺼이 toohandle 하 고, 유휴 시간 후 합니다 일방적으로 연결을 끊을 때 hello 연결에서 활동이 없을 경우.

또한 지원되는 동시 채널 수를 선언합니다. 채널은 단방향, 아웃 바운드, 가상 전송 경로 hello 연결 기반으로 합니다. 세션을 각 hello 상호 연결 된 컨테이너 tooform에서 양방향 통신 경로에서 채널을 사용합니다.

세션, 창 기반 흐름 제어 모델에 포함 되어 각 파티에 기꺼이 tooaccept는 프레임 수가 선언 하는 세션을 만들 때 해당 수신 창. 프레임 창 및 전송을 중지 hello 창이 전체 되 고 hello 창 다시 설정 됩니다. 또는 hello를 사용 하 여 확장 될 때까지 채우기 hello 당사자 exchange 프레임 전송 *흐름 performative* (*performative*프로토콜 수준의 제스처로 hello 두 파티 간에 교환에 대 한 hello AMQP 용어).

이 창 기반 모델은 창 기반 흐름 제어 하지만 hello 소켓 안 hello 세션 수준에서 매우 유사한 toohello TCP 개념입니다. hello 여러 동시 세션 수의 프로토콜의 개념 존재 우선 순위가 높은 트래픽을 수 수 기습 공격 정체 된 일반적인 트래픽이 지난 같은 고속도로 express 레인에 있도록 합니다.

Azure Service Bus는 현재 각 연결에 대해 정확히 하나의 세션을 사용합니다. 서비스 버스 최대 프레임 크기 hello는 서비스 버스 표준 및 이벤트 허브에 대 한 262, 144 바이트 (256k 바이트)입니다. Service Bus 프리미엄의 경우는 1,048,576(1MB)입니다. 서비스 버스 된 특정 세션 수준 제한 기간을 따르면 없지만 재설정 hello 창 정기적으로 링크 수준 흐름 제어의 일부로 (참조 [다음 섹션을 hello](#links)).

연결, 채널 및 세션은 사용 후 삭제됩니다. 기본 연결 hello 축소 연결 하는 경우 TLS 터널, SASL 권한 부여 컨텍스트 및 세션 다시 설정 해야 합니다.

### 링크

AMQP는 링크를 통해 메시지를 전송합니다. 링크는 한 방향; 메시지를 전송 하는 세션을 통해 만든 통신 경로 hello 전송 상태 협상 hello 링크와 연결 된 hello 파티 간의 양방향 끝났습니다.

![][2]

언제 든 지 및 AMQP 다 등의 여러 다른 프로토콜, 전송 및 전송 경로 hello 초기화는 hello 파티 만들기의 단독 권한이 MQTT 및 HTTP를에서 사용 하면 기존 세션을 통해 컨테이너 중 하나에서 연결을 만들 수 있습니다. hello 소켓 연결 합니다.

hello 링크 시작 컨테이너 컨테이너 tooaccept 반대 hello 링크 한 후의 발신자 또는 수신자 역할을 선택 합니다. 따라서 컨테이너 단방향 만들기를 시작할 수 있습니다 또는 링크의 쌍으로 양방향 통신 경로 후자 hello로 모델링 합니다.

링크의 이름이 지정되고 노드와 연결됩니다. Hello 시작 부분에서 설명 했 듯이 노드는 엔터티 컨테이너 내부 통신 hello입니다.

서비스 버스에는 노드는 tooa 직접 해당 하는 큐, 항목, 구독 또는 배달 못 한 편지 하위 큐의 큐 또는 구독. hello 노드 이름에 AMQP 사용 hello 엔터티 hello 서비스 버스 네임 스페이스 내부에서 상대적 이름을 hello 되므로 합니다. 큐 이름이 **myqueue**이면 AMQP 노드 이름도 같습니다. 항목 구독에서 "구독" 리소스 컬렉션 및 따라서 구독으로 정렬 하 고 hello HTTP API 규칙을 따릅니다 **sub** 또는 항목 **mytopic** hello AMQP 이름은 되어**mytopic/구독/sub**합니다.

연결 중인 클라이언트 hello 필요한 toouse; 링크를 만들기 위한 로컬 노드 이름을 이기도합니다 서비스 버스 노드 이름에 해당 하는 방법에 대 한 규정 하지 않으며 해석 하지는 않습니다. AMQP 1.0 클라이언트 스택에 hello 클라이언트의 hello 범위에서 이러한 임시 노드 이름이 고유한 지 구성표 tooassure 일반적으로 사용 합니다.

### 전송

링크가 설정되면 해당 링크를 통해 메시지를 전송할 수 있습니다. AMQP를 집합으로 전송 명시적 프로토콜 제스처와 실행 됩니다 (hello *전송* performative) 링크를 통해 메시지를 보낸 사람 tooreceiver에서 이동 하는입니다. 하며 전송이 완료 된 것은 "합의" 때 두 당사자 모두가 해당 전송의 hello 결과 대 한 공유 이해 설정 된 있는 의미 합니다.

![][3]

Hello 가장 간단 하 게 hello 보낸 사람 즉 hello 클라이언트 hello 결과에 관심을 보이지 않이 되 고 hello 수신기 hello 연산의 hello 결과 대 한 피드백을 제공 하지 않습니다 "합의 미리," toosend 메시지를 선택할 수 있습니다. 이 모드는 hello AMQP 프로토콜 수준에서 서비스 버스 지원 하지만 hello 클라이언트 Api에서 노출 되지 않습니다.

hello 일반 대/소문자가 메시지를 보내는 unsettled, 및 hello 수신기 수락 또는 거부 hello를 사용 하 여 다음 나타냅니다 *처리* performative 합니다. 거부는 hello 수신기 어떤 이유로 든 hello 메시지를 수락할 수 없습니다 및 AMQP 정의한 오류 구조는 hello 원인에 대 한 정보를 포함 하는 hello 거부 메시지 하는 경우에 발생 합니다. 서비스 버스 내부 toointernal 오류 인해 메시지는 거부 되 hello 서비스가 제공 하는 데 진단 힌트 toosupport 담당자 지원 요청을 제출 하는 경우 사용할 수 있는 해당 구조 내에서 추가 정보를 반환 합니다. 오류에 대해서는 이후에 좀 더 자세히 살펴보겠습니다.

거부의 특수 한 형태는 hello *출시* 상태 이면 해당 hello 수신기를 나타내는 없습니다 기술 objection toohello 전송 갖지만 끼지에 관심을 두지 않습니다 hello 전송 합니다. 대/소문자 있는지, 예를 들어 메시지의 배달 tooa 서비스 버스 클라이언트 및 클라이언트 hello 너무 "메시지의 버림" hello; hello 메시지 처리에서 발생 하는 hello 작업을 수행할 수 없으므로 선택 hello 메시지 배달 자체는 손상 되지 않았습니다. 해당 상태로의 변형을 hello *수정* 상태 변경 toohello 메시지를 놓을 수 있습니다. 이 상태는 현재 Service Bus에서 사용되지 않습니다.

추가 처리를 정의 하는 hello AMQP 1.0 사양 이라는 상태의 *받은*, 특히 toohandle 링크 복구 해 줍니다. 링크 복구 링크와 새 연결 및 세션을 hello 이전 연결 및 세션 손실 된 경우 위에 배달을 보류 중인의 hello 상태를 다시 구성 수 있습니다.

서비스 버스 연결 복구를 지원 하지 않습니다. hello 클라이언트 hello 연결 tooService 버스 unsettled 발생 하 여 분실 한 경우 보류 중인 전송, 메시지 전송 하 손실 되 고 hello 클라이언트 해야 다시 연결, hello 링크를 다시 설정 및 hello 전송을 다시 시도 하십시오.

따라서 서비스 버스 및 이벤트 허브 "최소 한 번" 전송을 지원 위치 hello 보낸 사람 hello 메시지 저장 및 허용 된 것을 보장할 수 이지만 "정확히 한 번 만" hello hello 시스템 toorecover를 시도해 야 하는 AMQP 수준에서 전송을 지원 하지 않습니다. hello 링크 하 고 hello 메시지를 전송 toonegotiate hello 배달 상태 tooavoid 복제를 계속 합니다.

서비스 버스 큐 및 항목에 선택적 기능으로 중복 검색 지원 가능한 중복에 대 한 toocompensate가 보냅니다. 중복 검색 기록 된 사용자 정의 된 기간 동안 모든 들어오는 메시지의 메시지 Id hello 다음 자동으로 동일한 창에 해당 하는 동안 동일한 메시지 Id hello를 통해 보내는 모든 메시지 삭제 합니다.

### 흐름 제어

또한 toohello 세션 수준 흐름 제어 된 모델을 앞에서 설명한, 각 링크에는 자체 흐름 제어 모델입니다. 세션 수준 흐름 제어 하는 것과 toohandle에 너무 많은 프레임 링크 수준 흐름 제어 수 하는 메시지에서 링크 하려는 toohandle 담당 hello 응용 프로그램을 저장 한 후 시점과 hello 컨테이너를 보호 합니다.

![][4]

링크에서 전송만 때 발생할 수 있습니다 hello 보낸 사람은 충분 *신용 연결*합니다. 링크 신용 hello를 사용 하 여 hello 수신기 넣어 카운터 집합은 *흐름* performative, 즉 tooa 링크 범위입니다. Hello 보낸 사람에 게 할당 하면 링크 신용, 메시지를 전달 하 여 해당 신용을 toouse를 시도 합니다. 1 씩 나머지 링크 신용을 hello 하는 각 메시지 배달 감소 시킵니다. Hello 링크 신용 모두 사용은 배달 중지 합니다.

Hello 받는 사람 역할에 서비스 버스를 즉시 제공 hello 보낸 사람에 게 충분 한 링크 신용와 메시지를 즉시 보낼 수 있도록 합니다. 서비스 버스 보내는 경우에 따라 링크 신용을 사용 하면 한 *흐름* performative toohello 보낸 사람 tooupdate hello 링크 크레딧 잔액입니다.

Hello 보낸 사람 역할에 서비스 버스 메시지 toouse를 모든 미해결 링크 신용을 보냅니다.

Hello API 수준에서 "수신" 호출으로 변환 된 *흐름* performative 보내는 hello 라인으로 전환 하 여 먼저 신용 버스 hello 클라이언트 및 서비스 버스 사용 tooService 사용 가능한 잠금 해제, hello 큐에서 메시지 및 전송 합니다. 즉시 배달할 수 있는 메시지가 없는 경우 모든 링크를 통해 모든 처리 중인 신용와 설정 된 특정 엔터티, 도착 한 순서에에서 기록 된 상태를 유지 및 메시지 잠금이 설정 되 고 있는 뛰어난 크레딧을 제공 될 때, toouse 전송 합니다.

hello 전송 hello 터미널 상태 중 하나로 합의 되 면 hello 메시지 잠금을 해제 *허용*, *거부*, 또는 *출시*합니다. hello 메시지는 hello 터미널 상태는 때 서비스 버스에서 제거 *허용*합니다. 서비스 버스의 상태를 유지 하 고 hello 전송에 도달 하면 hello의 다른 상태에는 toohello 다음 수신기를 배달 됩니다. 서비스 버스 자동 이동 hello 메시지 hello 엔터티의 배달 못한 편지 큐로 기한 toorepeated 거부 또는 릴리스 hello 엔터티에 대 한 허용 hello 최대 배달 횟수에 도달 하면 됩니다.

하위 수준의 AMQP 프로토콜 클라이언트 hello 링크 신용 모델 tooturn hello "풀 스타일" 상호 작용 유형의 각 수신 요청에 대 한 신용의 한 단위를 "밀어넣기 스타일" 모델로 발급 ְ ײ hello 서비스 버스 Api는 이러한 옵션이 오늘, 직접 노출 하지 않는 경우에 실행 하 여 많은 수의 링크 크레딧을 한 다음 메시지 추가 상호 작용 없이 사용 가능 해지면. 푸시 hello를 통해 지원 됩니다 [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) 또는 [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) 속성 설정 합니다. 0이 아닌 경우가 hello AMQP 클라이언트 hello 링크 신용으로 사용 합니다.

이 컨텍스트에서 hello 메시지를 가져옵니다 hello 엔터티에서 hello 메시지는 hello 통신 중에 삽입 했을 때에 하지의 중요 한 toounderstand hello 엔터티 내 hello 메시지에 대 한 hello 잠금 hello 만료에 대 한 클록 hello 하는 시작 됩니다. 클라이언트 hello 링크 신용을 실행 하 여 준비 tooreceive 메시지를 나타내는, 때마다이 따라서 예상된 toobe 적극적으로 풀링 메시지 hello 네트워크를 통해 고 수 준비 toohandle 해당 합니다. 그렇지 않으면 hello 메시지 배달도 되기 전에 hello 메시지 잠금 만료 될 수 있습니다. hello 링크 신용 흐름 제어를 사용 하는 사용 가능한 메시지 발송 toohello 수신기가 포함 된 hello 즉시 준비 toodeal을 반영 직접 해야 합니다.

요약 하자면, hello 다음 단원에서는 개요만 제공 도식 hello performative 흐름의 다른 API 상호 작용 하는 동안. 섹션마다 다른 논리 작업을 설명합니다. 이러한 상호 작용 중 일부는 "지연"될 수 있습니다. 즉, 필요할 때만 수행될 수 있습니다. 메시지 보낸 사람을 만드는 hello 첫 번째 메시지를 보내거나 요청 될 때까지 네트워크 상호 작용 시 키 지 않습니다.

다음 표에 hello에 hello 화살표 hello performative 흐름 방향을 표시 합니다.

#### 메시지 수신자 만들기

| 클라이언트 | Service Bus |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={entity name},<br/>target={client link id}<br/>) |클라이언트 수신기 tooentity 연결 |
| 서비스 버스 회신 hello 링크의 끝에 연결 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={entity name},<br/>target={client link id}<br/>) |

#### 메시지 발신자 만들기

| 클라이언트 | Service Bus |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |작업 없음 |
| 작업 없음 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={client link id},<br/>target={entity name}<br/>) |

#### 메시지 발신자 만들기(오류)

| 클라이언트 | Service Bus |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |작업 없음 |
| 작업 없음 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={numeric handle},<br/>closed=**true**,<br/>error={error info}<br/>) |

#### 메시지 수신자/발신자 닫기

| 클라이언트 | Service Bus |
| --- | --- |
| --> detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |작업 없음 |
| 작업 없음 |<-- detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |

#### 전송(성공)

| 클라이언트 | Service Bus |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |작업 없음 |
| 작업 없음 |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### 전송(오류)

| 클라이언트 | Service Bus |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |작업 없음 |
| 작업 없음 |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={error info}<br/>)<br/>) |

#### 수신

| 클라이언트 | Service Bus |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |작업 없음 |
| 작업 없음 |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |작업 없음 |

#### 다중 메시지 수신

| 클라이언트 | Service Bus |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |작업 없음 |
| 작업 없음 |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| 작업 없음 |< transfer(<br/>delivery-id={numeric handle+1},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| 작업 없음 |< transfer(<br/>delivery-id={numeric handle+2},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |작업 없음 |

### 메시지

hello 다음 섹션에서는 설명 hello 표준 AMQP 메시지 섹션에서 서비스 버스에서 사용 되 고 toohello 서비스 버스 API 집합 매핑되는 방식입니다.

#### 머리글

| 필드 이름 | 사용 | API 이름 |
| --- | --- | --- |
| 지속성 |- |- |
| 우선 순위 |- |- |
| ttl |이 메시지에 대 한 toolive 시간 |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| first-acquirer |- |- |
| delivery-count |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| 필드 이름 | 사용 | API 이름 |
| --- | --- | --- |
| message-id |이 메시지에 대한 응용 프로그램 정의 자유 형식 식별자입니다. 중복 검색에 사용됩니다. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |Service Bus에서 해석되지 않는 응용 프로그램 정의 사용자 식별자입니다. |Hello 서비스 버스 API를 통해 액세스할 수 없습니다. |
| 너무|Service Bus에서 해석되지 않는 응용 프로그램 정의 대상 식별자입니다. |[To](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| subject |Service Bus에서 해석되지 않는 응용 프로그램 정의 메시지 용도 식별자입니다. |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| 회신 너무|Service Bus에서 해석되지 않는 응용 프로그램 정의 회산 경로 식별자입니다. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |Service Bus에서 해석되지 않는 응용 프로그램 정의 상관 관계 식별자입니다. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| content-type |서비스 버스에서 해석 되지 hello 본문, 콘텐츠 형식 표시기 응용 프로그램 정의입니다. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |서비스 버스에서 해석 되지 hello 본문, 콘텐츠 인코딩 지표 응용 프로그램 정의 |Hello 서비스 버스 API를 통해 액세스할 수 없습니다. |
| absolute-expiry-time |선언 메시지가 만료 되는 절대 인스턴트 hello 합니다. 입력 중에는 무시되고(헤더 TTL이 확인됨), 출력 중에는 신뢰할 수 있습니다. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |선언 어떤 시간 hello 메시지를 만든 합니다. Service Bus에서 사용되지 않습니다. |Hello 서비스 버스 API를 통해 액세스할 수 없습니다. |
| group-id |관련된 메시지 집합에 대한 응용 프로그램 정의 식별자입니다. Service Bus 세션에 사용됩니다. |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |카운터는 세션 내 hello 메시지의 hello 상대 시퀀스 번호를 식별 합니다. Service Bus에서 무시됩니다. |Hello 서비스 버스 API를 통해 액세스할 수 없습니다. |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## 고급 Service Bus 기능

이 섹션에서는 초안 확장 tooAMQP, 현재 개발 hello 기술 위원회 OASIS AMQP에 대 한 기반으로 하는 Azure 서비스 버스의 고급 기능에 설명 합니다. 서비스 버스 hello 이러한 초안의 최신 버전을 구현 하 고 해당 초안 표준 상태에 도달 도입 된 변경 내용을 적용 합니다.

> [!NOTE]
> Service Bus 메시징 고급 작업은 요청/응답 패턴을 통해 지원됩니다. 이러한 작업의 hello 세부 hello 문서에 설명 되어 [서비스 버스에서 AMQP 1.0: 요청-응답 기반 작업](service-bus-amqp-request-response.md)합니다.
> 
> 

### AMQP 관리

AMQP 관리 사양 hello는 hello 여기서 설명 하는 hello 초안 확장의 첫 번째입니다. 이 사양은 hello AMQP를 통해 메시징 인프라와의 관리 상호 작용을 허용 하는 hello AMQP 프로토콜을 기반으로 계층화 되는 프로토콜 제스처 집합을 정의 합니다. hello 사양에서는 같은 일반 작업 정의 *만들*, *읽을*, *업데이트*, 및 *삭제* 내 엔터티를 관리 하기 위한는 메시징 인프라 및 쿼리 작업의 집합입니다.

이러한 모든 제스처로 hello 클라이언트와 hello 메시징 인프라 요청/응답 상호 작용을 필요 하 고 따라서 hello 사양에 정의 방법을 toomodel 상호 작용을 지는 AMQP 위에 패턴: hello 클라이언트가 연결 toohello 메시징 인프라는 세션을 초기화 한 다음 한 쌍의 링크를 만듭니다. 하나의 링크 hello 클라이언트가 보낸 사람 역할 및 역할을 만들어서 다음 한 쌍의 링크는 양방향 채널을 수행할 수 있는 수신기에 다른 hello 합니다.

| 논리 연산 | 클라이언트 | Service Bus |
| --- | --- | --- |
| 요청 응답 경로 만들기 |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=**null**,<br/>target=”myentity/$management”<br/>) |작업 없음 |
| 요청 응답 경로 만들기 |작업 없음 |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=null,<br/>target=”myentity”<br/>) |
| 요청 응답 경로 만들기 |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=”myentity/$management”,<br/>target=”myclient$id”<br/>) | |
| 요청 응답 경로 만들기 |작업 없음 |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=”myentity”,<br/>target=”myclient$id”<br/>) |

위치에 해당 쌍의 링크를 having, hello 요청/응답 구현이 간단 하 게 되었습니다.: 요청에는이 패턴을 이해 하는 hello 메시징 인프라 내부 tooan 엔터티를 보낸 메시지입니다. 해당 요청 메시지에서 hello *회신* 필드 hello에 *속성* 섹션 toohello 설정 되어 *대상* toodeliver hello 응답으로 hello 링크에 대 한 식별자입니다. 엔터티를 처리 하는 hello hello 요청을 처리 한 다음 hello 통해 제공 hello 회신 연결 인 *대상* 표시 된 hello 식별자가와 일치 *회신* 식별자입니다.

hello 패턴은 분명 hello 클라이언트 컨테이너와 hello 회신 대상에 대 한 hello 클라이언트에서 생성 된 식별자는 고유 모든 클라이언트에서 주고 보안상의 이유로 어려울 toopredict 하기 위해 필요 합니다.

hello 메시지 교환을 사용 hello 관리 프로토콜에 대 한 다른 모든 프로토콜에 대 한 동일한 패턴 발생할 hello 응용 프로그램 수준;에서 해당 사용 하 여 hello 새 AMQP 프로토콜 수준의 제스처를 정의 하지 않습니다. 이러한 방식은 응용 프로그램이 호환 AMQP 1.0 스택에서 이러한 확장을 즉시 활용할 수 있도록 하기 위해 의도된 것입니다.

서비스 버스 구현 하지 않는 현재 hello 관리 사양의 hello 코어 기능 하지만 hello 관리 사양에 정의 된 hello 요청/응답 패턴은 hello 클레임 기반 보안 기능 및 모든 거의 기본 hello 고급 hello 다음 섹션에서에서 설명 하는 기능입니다.

### 클레임 기반 권한 부여

hello AMQP 클레임 기반 인증 (CBS) 사양 초안 hello 관리 사양 요청/응답 패턴을 바탕으로 하며 toouse AMQP 가진 보안 토큰을 페더레이션 하는 방법에 대 한 일반화 된 모델에 설명 합니다.

AMQP hello 소개에서 설명한 hello 기본 보안 모델 SASL 기반 및 AMQP 연결 핸드셰이크 hello와 통합 합니다. SASL를 사용 하는 메커니즘의 집합에서 모든 프로토콜 SASL에 공식적으로 leans을 얻을 수 정의 된를 확장 가능 모델을 제공 하는 hello 장점이 있습니다. 사용자 이름 및 암호, "외부" toobind tooTLS 수준 보안, 명시적 인증/권한 부여 및 추가 메커니즘 허용 하는 광범위 한 "ANONYMOUS" tooexpress hello 없으면 전송에 대 한 "일반"는 이러한 메커니즘 중 인증 및/또는 권한 부여 자격 증명 또는 토큰을 전달 합니다.

AMQP의 SASL 통합에는 다음과 같은 두 가지 단점이 있습니다.

* 모든 자격 증명 및 토큰 범위 지정 된 toohello 연결 됩니다. 메시징 인프라 엔터티별 기준 differentiated tooprovide 액세스 제어를 사용할 수 있습니다. 예를 들어 hello 전달자 토큰 toosend tooqueue A 하지만 tooqueue B. 하지 허용 Hello 권한 부여 컨텍스트 hello 연결에서 앵커를 사용 불가능 toouse 단일 연결 되며 큐 A 및 2. 큐에 대 한 서로 다른 액세스 토큰을 아직 사용
* 액세스 토큰은 일반적으로 제한된 시간 동안만 유효합니다. 이 유효성 hello 사용자 tooperiodically 다시 가져오기 토큰이 필요 하 고 hello 사용자의 액세스 권한을 변경 된 경우 새로 고침 토큰을 발급 하는 기회 toohello 토큰 발급자 toorefuse를 제공 합니다. AMQP 연결은 매우 긴 시간 동안 지속될 수 있습니다. hello SASL 모델만 기회 tooset 한 토큰을 제공 하거나 메시징 인프라 hello을 의미 하는 hello 토큰 만료 될 때와 계속된 통신을 허용할 때의 tooaccept hello 위험은 필요한 toodisconnect hello 클라이언트에 연결 시는 클라이언트 사용자가 hello 중간에 대 한 액세스 권한을 취소 합니다.

hello AMQP CBS 사양 서비스 버스에 의해 구현 이러한 문제를 모두에 대 한 적절 한 해결 방법을 통해: tooassociate 액세스 토큰을 각 노드와 tooupdate hello 메시지 흐름을 중단 하지 않고 만료 되기 전까지 이러한 토큰을 사용 하 여 클라이언트가 있습니다.

CBS 라는 가상 관리 노드가 정의 *$cbs*, toobe hello 메시징 인프라에서 제공 합니다. hello 관리 노드 hello 메시징 인프라의에서 다른 노드에 대신 하 여 토큰을 수락 합니다.

hello 프로토콜 제스처는 hello 관리 사양에 정의 된 대로 요청/회신 교환 합니다. 한 쌍의 hello로 링크 설정 의미 클라이언트 hello는 *$cbs* 노드를 선택한 다음에 요청에 아웃 바운드 링크 및 hello 응답 대기 hello 전달 hello 인바운드 링크 합니다.

hello 요청 메시지에 hello 다음과 같은 응용 프로그램 속성:

| 키 | 옵션 | 값 형식 | 값 내용 |
| --- | --- | --- | --- |
| operation |아니요 |string |**put-token** |
| type |아니요 |string |put 중인 hello 토큰의 hello 형식입니다. |
| name |아니요 |string |hello "audience" toowhich hello 토큰에는 다음이 적용 됩니다. |
| expiration |예 |timestamp |hello hello 토큰의 만료 시간입니다. |

hello *이름* 토큰을 관련 여야 하는 hello로 hello 엔터티 속성을 식별 합니다. 서비스 버스의 hello 경로 toohello 큐 또는 항목/구독의 합니다. hello *형식* 속성 hello 토큰 유형을 식별 합니다.

| 토큰 형식 | 토큰 설명 | 본문 형식 | 참고 사항 |
| --- | --- | --- | --- |
| amqp:jwt |JWT(JSON 웹 토큰) |AMQP 값(문자열) |아직 사용할 수 없습니다. |
| amqp:swt |SWT(단순 웹 토큰) |AMQP 값(문자열) |AAD/ACS에서 발급한 SWT 토큰에 대해서만 지원됩니다. |
| servicebus.windows.net:sastoken |Service Bus SAS 토큰 |AMQP 값(문자열) |- |

토큰은 권한을 부여합니다. Service Bus는 다음 세 가지 기본 권한을 알고 있습니다. "전송"은 전송을 가능하게 하고, "수신"은 수신을 가능하게 하고, "메시지"는 엔터티 조작을 가능하게 합니다. 명시적으로 AAD/ACS에서 발급한 SWT 토큰에는 이러한 권한이 클레임으로 포함되어 있습니다. 서비스 버스 SAS 토큰 hello 네임 스페이스 또는 엔터티에에 구성 된 toorules을 권한으로 이러한 규칙이 구성 됩니다. 따라서 해당 규칙와 연결 된 hello 키로 서명 hello 토큰 hello 토큰 express hello 해당 권리를 만듭니다. 엔터티를 사용 하 여 연관 된 hello 토큰 *put 토큰* 허용 hello hello 토큰 권한 당 hello 엔터티와 toointeract 클라이언트를 연결 합니다. Hello 클라이언트 hello에 사용 되는 링크 *보낸 사람* 역할을 사용 하려면 오른쪽; hello "Send" hello에 대 *수신기* 역할을 사용 하려면 hello "수신" 권한이 필요 합니다.

hello 회신 메시지에 hello 다음 *응용 프로그램 속성* 값

| 키 | 옵션 | 값 형식 | 값 내용 |
| --- | --- | --- | --- |
| status-code |아니요 |int |HTTP 응답 코드 **[RFC2616]** |
| status-description |예 |string |Hello 상태에 대 한 설명입니다. |

hello 클라이언트가 호출할 수 있는 *put 토큰* 반복적 이며 hello 메시징 인프라에서 모든 엔터티에 대 한 합니다. hello 토큰은 범위 지정 된 toohello 현재 클라이언트 놓습니다 hello 현재 연결을 고정 의미 hello 서버 보관 된 모든 토큰 hello 연결을 삭제 하는 경우.

현재 서비스 버스 구현 hello hello SASL 방법 "ANONYMOUS"와 함께에서 CBS 허용 SSL/TLS 연결에는 이전 toohello SASL 핸드셰이크 항상 존재 해야 합니다.

AMQP 1.0 클라이언트를 선택 하는 hello 따라서 hello 익명 메커니즘을 지원 합니다. Hello 초기 세션 만들기를 포함 하 여 초기 연결 핸드셰이크 hello 익명 액세스 의미 hello 연결 작성자나 알면 서비스 버스 없이 발생 합니다.

Hello 연결 및 세션 설정 되 면 toohello 링크 hello 연결 *$cbs* 노드와 hello 보내는 *put 토큰* 요청은 hello 허용 된 작업입니다. 유효한 토큰을 사용 하 여 성공적으로 설정 해야 합니다는 *put 토큰* 요청 일부 엔터티 노드 20 초 내에 대 한 hello 연결이 설정 된 후 그렇지 않으면 hello 연결을 일방적으로 삭제할지 서비스 버스입니다.

hello 클라이언트는 토큰 만료는 추적에 대 한 이후에 해야 합니다. 토큰이 만료 되 면 서비스 버스 hello 연결 toohello 해당 엔터티의 모든 링크를 신속 하 게 삭제 합니다. tooprevent이,이 hello 클라이언트가 hello 노드에 대 한 hello 토큰 언제 든 지 가상 hello 통해 새 항목으로 대체할 수 *$cbs* 관리 노드를 동일한 hello *put 토큰* , 제스처 및 없이 hello에 가져오기 hello 페이로드의 방법은 트래픽 서로 다른 연결에서 해당 흐름.

## 다음 단계

AMQP, 링크를 따라 방문 hello에 대 한 자세한 toolearn:

* [Service Bus AMQP 개요]
* [Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]
* [Windows Server용 Service Bus의 AMQP]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Service Bus AMQP 개요]: service-bus-amqp-overview.md
[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
