---
title: "hello 서비스 패브릭 신뢰할 수 있는 서비스 프로그래밍 모델의 aaaOverview | Microsoft Docs"
description: "서비스 패브릭의 신뢰할 수 있는 서비스 프로그래밍 모델에 대해 알아보고 사용자 고유의 서비스 작성을 시작합니다."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>신뢰할 수 있는 서비스 개요
Azure 서비스 패브릭은 상태 비저장 및 상태 저장 신뢰할 수 있는 서비스의 작성과 관리를 단순화합니다. 이 항목은 다음에 대해 설명합니다.

* hello 상태 비저장 및 상태 저장 서비스에 대 한 프로그래밍 모델을 신뢰할 수 있는 서비스입니다.
* hello 선택할 수 있는 toomake 신뢰할 수 있는 서비스를 작성할 때는 합니다.
* 일부 시나리오와는 경우의 예 toouse 안정성 서비스를 제공 하며 작성 방법입니다.

신뢰할 수 있는 서비스 패브릭 서비스에서 사용할 수 있는 모델을 프로그래밍 하는 hello 중 하나입니다. 다른 hello는 hello Reliable Actor 프로그래밍 모델을 hello 신뢰할 수 있는 서비스 모델 위에 가상 행위자 프로그래밍 모델을 제공 합니다. Hello Reliable Actors 프로그래밍 모델에 대 한 자세한 내용은 참조 하십시오. [소개 tooService 패브릭 Reliable Actors](service-fabric-reliable-actors-introduction.md)합니다.

서비스 패브릭을 통해 프로 비전 하 고 업그레이드 및 삭제를 통해 배포에서 서비스의 hello 수명을 관리 [서비스 패브릭 응용 프로그램 관리](service-fabric-deploy-remove-applications.md)합니다.

## <a name="what-are-reliable-services"></a>신뢰할 수 있는 서비스는 무엇입니까?
신뢰할 수 있는 서비스는 단순 하 고 강력 하 고 중요 한 tooyour 응용 프로그램 이란 express 모델 toohelp 프로그래밍 최상위을 제공 합니다. Hello 신뢰할 수 있는 서비스 프로그래밍 모델에서 가져오기:

* 액세스 toohello rest Api를 프로그래밍 하는 서비스 패브릭 hello 합니다. 서비스 패브릭 서비스도 모델링와 달리 [게스트 실행 파일](service-fabric-deploy-existing-app.md), 신뢰할 수 있는 서비스의 서비스 패브릭 Api hello toouse hello rest를 직접 가져올 합니다. 그러면 서비스에서 다음을 수행할 수 있습니다.
  * 쿼리 hello 시스템
  * hello 클러스터의 엔터티에 대 한 상태 보고
  * 구성 및 코드 변경 내용에 대한 알림 수신
  * 다른 서비스 찾기 및 통신
  * (선택 사항) hello를 사용 하 여 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md)
  * ... 및 쉽게 액세스 toomany 다른 기능, 여러 프로그래밍 언어의 최고 수준의 프로그래밍 모델에서 모두 합니다.
* 기존에 사용하던 프로그래밍 모델과 비슷한 사용자 고유의 코드를 실행하기 위한 간단한 모델. 사용자의 코드에는 잘 정의된 진입점과 쉽게 관리되는 수명 주기가 있습니다.
* 플러그형 통신 모델. HTTP와 같이 선택한 hello 전송을 사용 [웹 API](service-fabric-reliable-services-communication-webapi.md), WebSockets, 사용자 지정 TCP 프로토콜 또는 기타 항목입니다. 신뢰할 수 있는 서비스는 훌륭한 기본 옵션을 제공하거나 직접 만들 수 있게 지원합니다.
* 상태 저장 서비스에 대 한 hello 신뢰할 수 있는 서비스 모델 프로그래밍 tooconsistently 있으며 안전 하 게 사용 하 여 서비스 오른쪽 내부 상태를 저장할 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md)합니다. 신뢰할 수 있는 컬렉션은 간단한 집합이 컬렉션 C# 사용 경험이 친숙 한 tooanyone 수 있는 항상 사용 가능 하 고 신뢰할 수 있는 컬렉션 클래스입니다. 일반적으로 서비스는 신뢰할 수 있는 상태 관리를 위한 외부 시스템이 필요합니다. 신뢰할 수 있는 컬렉션을 사용 하면 상태 다음 tooyour 계산 hello로 저장할 수 있습니다 같은 높은 가용성 및 안정성 돌아와 tooexpect 항상 사용 가능한 외부 저장소에서 저장 했습니다. 또한이 모델 hello 계산 및 toofunction 필요한 상태를 공동 배치는 때문에 대기 시간을 향상 합니다.

Reliable Services의 개요는 다음 Microsoft Virtual Academy 비디오를 시청하세요. <center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>신뢰할 수 있는 서비스가 다른 서비스와 다른 점은 무엇입니까?
서비스 패브릭의 신뢰할 수 있는 서비스는 이전에 작성하던 서비스와 다릅니다. 서비스 패브릭은 안정성, 가용성, 일관성 및 확장성을 제공합니다.

* **안정성** 프로그램-컴퓨터 실패 하거나 네트워크 문제를 적중 위치 신뢰할 수 없는 환경에서 조차 위로 유지 되며 서비스 또는 오류 및 충돌이 발생할 경우 hello 서비스 자체에 실패 합니다. 상태 저장 서비스에 대 한 상태는 네트워크 또는 기타 실패로 인해 hello 있는지에도 유지 됩니다.
* **가용성** - 연결 가능하고 응답성이 뛰어난 서비스입니다. Service Fabric은 실행 중인 복사본 수를 유지 관리합니다.
* **확장성** -서비스는 특정 하드웨어에서 분리 되 고 늘리거나 하드웨어 또는 기타 리소스의 hello 추가 또는 제거를 통해 필요에 따라 줄일 수 있습니다. 서비스는 hello 서비스 확장할 수 있습니다 (특히 hello 안정 된 경우)에서 분할 된 쉽게 tooensure 및 핸들 부분 실패 합니다. 서비스를 만들 수 있으며 응답 toocustomer 요청에 올린 코드를 필요에 따라 생성 되는 더 많은 인스턴스 toobe 통해 동적으로 삭제 합니다. 마지막으로, 서비스 패브릭 서비스 toobe lightweight을 권장합니다. 서비스 패브릭 서비스 toobe 단일 프로세스 내에서 사용자를 프로 비전 하지 않고 요구 하거나 전체 OS 인스턴스 또는 서비스의 프로세스 tooa 단일 인스턴스 전용 수천 수 있습니다.
* **일관성** -이 서비스에 저장 된 모든 정보 보장할 수 toobe 일치 합니다. 서비스 내에서 여러 신뢰할 수 있는 컬렉션 간에도 적용됩니다. 서비스 내의 컬렉션을 트랜잭션 원자 방식으로 변경할 수 있습니다.

## <a name="service-lifecycle"></a>서비스 수명 주기
서비스가 상태 저장 서비스이든, 상태 비저장 서비스이든, 신뢰할 수 있는 서비스는 신속하게 코드를 연결하고 시작할 수 있는 간단한 수명 주기를 제공합니다.  된다고 tooimplement tooget 서비스 시작 및 실행 하는 하나 또는 두 개의 메서드가 있습니다.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -이 메서드는 hello 서비스는 hello 통신 stack(s) toouse 브로드캐스트하며를 정의 합니다. 와 같은 통신 스택을 hello [웹 API](service-fabric-reliable-services-communication-webapi.md), 수신 대기 끝점 hello 정의 또는 대 한 끝점 hello (방법: 클라이언트 hello 서비스 연결할) 서비스입니다. 또한 표시 되는 hello 메시지 hello 서비스 코드의 나머지 부분 hello 상호 작용 하는 방법을 정의 합니다.
* **RunAsync** -이 방법은 서비스는 비즈니스 논리 실행 되 고 작업이 있는 hello 서비스의 수명과 hello에 대 한 실행 해야 하는 모든 백그라운드 작업 시작 되어 합니다. hello, 취소 토큰을 제공 되는 해당 작업을 중지 하는 것에 대 한 신호입니다. 예를 들어 hello 서비스 신뢰할 수 있는 큐에서 메시지 toopull 필요 하 고 처리 하는 경우이 작동 하는 상황이 발생 합니다.

처음으로 hello에 대 한 신뢰할 수 있는 서비스에 대 한 학습 하는, 경우 기대해 주세요! 신뢰할 수 있는 서비스의 수명 주기 hello의 자세한 연습 과정을 찾고 있는 경우 수을 향해 위로 너무[이 여기서](service-fabric-reliable-services-lifecycle.md)합니다.

## <a name="example-services"></a>예제 서비스
이 프로그래밍 모델을 알고 있으면 하면 이러한 개념이 서로 어떻게 연결 하는 두 개의 서로 다른 서비스 toosee 개요를 보겠습니다.

### <a name="stateless-reliable-services"></a>상태 비저장 신뢰할 수 있는 서비스
상태 비저장 서비스에는 하나의 호출 간에 hello 서비스 내에서 유지 관리 하는 상태가 되지 않았습니다. 표시된 상태는 완전히 삭제 가능하며 동기화, 복제, 지속성 또는 고가용성이 필요하지 않습니다.

예를 들어 메모리가 없습니다. 수신 하는 모든 조건 및 작업 tooperform 한 번에 하는 계산기를 것이 좋습니다.

이 경우 hello `RunAsync()` (C#) 또는 `runAsync()` (Java)의 hello 서비스 비어 있을 수 있습니다, 태스크 처리 해당 hello 서비스 toodo 필요 없는 백그라운드 있기 때문입니다. 반환 hello 계산기 서비스를 만드는 경우는 `ICommunicationListener` (C#) 또는 `CommunicationListener` (Java) (예를 들어 [웹 API](service-fabric-reliable-services-communication-webapi.md)) 하는 일부 포트에서 수신 대기 끝점을 엽니다. 이 수신 대기 끝점 연결 하는 toohello 다른 계산 방법 (예: "Add (n1, n2)") hello 계산기 공용 API를 정의 하는 합니다.

클라이언트에서 호출 되 면 hello 적절 한 메서드를 호출 하 고 hello 계산기 서비스 데이터 제공 되 고 hello 결과 반환 하는 hello에 hello 작업을 수행 합니다. 상태를 저장하지 않습니다.

모든 내부 상태를 저장하지 않으므로 이 계산기 예제는 간단해집니다. 하지만 대부분의 서비스는 상태 비저장이 아닙니다. 해당 상태 toosome 다른 저장소 외부화 하는 대신. (예를 들어 세션 상태를 백업 저장소 또는 캐시에 유지하는 모든 웹앱은 상태 비저장이 아닙니다.)

어떻게 상태 비저장 서비스의 일반적인 예로 서비스 패브릭에서 사용 되는 프런트 엔드로 hello 웹 응용 프로그램에 대 한 공용 API를 노출 하 합니다. hello 프런트 엔드 서비스는 다음 toostateful 서비스 toocomplete 사용자 요청을 설명 합니다. 이 경우 클라이언트의 호출에는 방향이 지정 된 tooa 알려진 같은 포트 80, hello 상태 비저장 서비스 수신 대기 됩니다. 이 상태 비저장 서비스 hello 전화를 받 및 hello 호출에서 신뢰할 수 있는 당사자 인지 여부와 어떤가 서비스에 대 한 대상입니다.  그런 다음 hello 상태 비저장 서비스 hello 호출 toohello hello 상태 저장 서비스의 올바른 파티션을 전달 하 고 응답을 받기 위해 대기 합니다. Hello 상태 비저장 서비스 응답을 받으면 toohello 원래 클라이언트를 회신 합니다. 이러한 서비스의 예제는 [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService) 샘플에 있습니다. 이 hello 샘플에서이 패턴의 한 예도 다른 샘플에도 키워드가, 합니다.

### <a name="stateful-reliable-services"></a>상태 저장 신뢰할 수 있는 서비스
상태 저장 서비스는 일관 되 고 hello 서비스 toofunction 하기 위해 존재 유지 상태의 일부 있어야입니다. 수신하는 업데이트에 따라 일부 값의 이동 평균을 지속적으로 계산하는 서비스를 고려할 수 있습니다. toodo이를 현재 평균 hello 및 tooprocess 필요한 들어오는 요청의 hello 현재 설정 되어 있어야 합니다. 정보를 검색, 처리하고 외부 저장소(예: Azure Blob 또는 현재 테이블 저장소)에 저장하는 모든 서비스는 상태 저장입니다. 방금 hello 외부 상태 저장소에 해당 상태를 유지합니다.

대부분의 서비스는 hello 외부 저장소는 해당 상태에 대 한 안정성, 가용성, 확장성 및 일관성 제공 하므로 오늘 외부적으로 상태를 저장 합니다. 서비스 패브릭에서 서비스 필요한 toostore 자신의 상태를 외부적으로 되지 않습니다. 서비스 패브릭 서비스 코드 hello와 hello 서비스 상태에 대 한 이러한 요구 사항을 처리합니다.

> [!NOTE]
> 아직 Linux에서는 상태 저장 Reliable Services가 지원되지 않습니다(C# 또는 Java의 경우).
>

이미지를 처리 하는 서비스 toowrite 원하는 경우를 가정해 봅니다. toodo이 변환 tooperform 해당 이미지에는 이미지와 hello 계열의에서 hello 서비스 사용 합니다. 이 서비스는 `ConvertImage(Image i, IList<Conversion> conversions)`와 같은 API를 노출하는 통신 수신기(WebAPI라고 가정함)를 반환합니다. 요청을 받으면 hello 서비스에 저장 한 `IReliableQueue`, hello 요청을 추적할 수 있도록 일부 id toohello 클라이언트를 반환 합니다.

이 서비스에서는 `RunAsync()`가 더 복잡해질 수 있습니다. hello 서비스 내부 루프에 해당 `RunAsync()` 의 요청을 끌어오는 `IReliableQueue` 요청 hello 변환을 수행 하 고 있습니다. hello 결과에 저장 된 가져오기는 `IReliableDictionary` hello 클라이언트 다시 시작 하는 경우 있도록가 변환 된 이미지를 가져올 수 있습니다. tooensure hello 이미지 오류가 있으면 즉도 손실 되지 않습니다, 그리고 신뢰할 수 있는이 서비스는 hello 큐에서 꺼냅니다, hello 변환을 수행 및 단일 트랜잭션 내에서 모든 hello 결과 저장 합니다. 이 경우 hello 메시지 hello 큐에서 제거 되 고 hello 변환 작업이 완료 된 경우에 hello 결과 hello 결과 사전에 저장 됩니다. 또는 hello 서비스는 hello 이미지 hello 큐에서 끌어오도록 하 고 즉시 원격 저장소에 저장 수 없습니다. 이렇게 하면 줄어듭니다 hello 상태 hello 서비스 양을 toomanage를 갖지만 hello 서비스 tookeep hello 필요한 메타 데이터가 toomanage hello 원격 저장소에 있기 때문에 복잡성을 증가 합니다. 각 접근 방법에 작업에 실패 한 경우 hello 중간 hello 요청 처리 hello 큐 대기 toobe에 남아 있습니다.

이 서비스에 대 한 한 가지 toonote 일반.NET 서비스 말 하는! hello 유일한 차이점은 hello 데이터를 사용 하 고 구조는 (`IReliableQueue` 및 `IReliableDictionary`) 서비스 패브릭에서 제공 되 고 매우 안정적이 고, 사용할 수 있는 일관 됩니다.

## <a name="when-toouse-reliable-services-apis"></a>때 toouse 신뢰할 수 있는 서비스 Api
응용 프로그램 서비스에 필요한 특징을 결정 hello 다음 신뢰할 수 있는 서비스 Api 고려해 야 합니다.

* 서비스의 코드 (및 필요에 따라 상태) 항상 사용 가능 하 고 신뢰할 수 있는 toobe
* 여러 상태 단위(예: 주문 및 주문 품목)에 걸쳐 트랜잭션 보장이 필요합니다.
* 응용 프로그램의 상태를 신뢰할 수 있는 사전 및 큐로 자연스럽게 모델링할 수 있습니다.
* 응용 프로그램 코드 또는 상태로 대기 시간이 짧은 읽기 및 쓰기를 항상 사용 가능한 toobe가 필요합니다.
* 응용 프로그램 하나 이상의 신뢰할 수 있는 컬렉션에서 toocontrol hello 동시성 또는 트랜잭션 처리 작업의 세분성에 필요 합니다.
* Toomanage hello 통신 또는 파티션 구성표 서비스에 대 한 제어 hello 원합니다.
* 코드에 자유 스레드된 런타임 환경이 필요합니다.
* 응용 프로그램에 필요한 toodynamically 만들거나 신뢰할 수 있는 사전 또는 큐 또는 런타임 시 전체 서비스를 삭제 합니다.
* Tooprogrammatically 제어 서비스 패브릭 제공 백업 및 복원 기능이 필요한 서비스의 상태에 대 한 합니다.
* 응용 프로그램 상태의 해당 장치에 대 한 toomaintain 변경 내용에 필요 합니다.
* 원하는 toodevelop 또는 파티 개발, 사용자 지정 상태 공급자를 사용 합니다.

## <a name="next-steps"></a>다음 단계
* [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
* [신뢰할 수 있는 서비스 고급 사용법](service-fabric-reliable-services-advanced-usage.md)
* [hello Reliable Actors 프로그래밍 모델](service-fabric-reliable-actors-introduction.md)
