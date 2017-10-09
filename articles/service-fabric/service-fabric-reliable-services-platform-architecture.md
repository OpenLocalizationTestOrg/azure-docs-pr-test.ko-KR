---
title: "서비스 아키텍처 aaaReliable | Microsoft Docs"
description: "상태 저장 및 상태 비저장 서비스에 대 한 hello 신뢰할 수 있는 서비스 아키텍처의 개요"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>상태 비저장 Reliable Services를 위한 아키텍처
Azure 서비스 패브릭 Reliable Service는 상태 저장이거나 상태 비저장일 수 있습니다. 각 서비스 유형은 특정 아키텍처 내에서 실행됩니다. 이러한 아키텍처는 이 문서에 설명되어 있습니다.
Hello 참조 [신뢰할 수 있는 서비스 개요](service-fabric-reliable-services-introduction.md) hello 차이점 상태 저장 및 상태 비저장 서비스에 대 한 자세한 내용은 합니다.

## <a name="stateful-reliable-services"></a>상태 저장 신뢰할 수 있는 서비스
### <a name="architecture-of-a-stateful-service"></a>상태 저장 서비스의 아키텍처
![상태 저장 서비스의 아키텍처 다이어그램](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>상태 저장 신뢰할 수 있는 서비스
신뢰할 수 있는 상태 저장 서비스는 hello StatefulService 또는 StatefulServiceBase 클래스 중 하나에서 파생 될 수 있습니다. 이러한 기본 클래스는 모두 서비스 패브릭에서 제공하며, 다양 한 수준의 지원과 hello 서비스 패브릭 클러스터 내에서 서비스로 서비스 패브릭-tooparticipate와 상태 저장 서비스 toointerface hello에 대 한 추상화를 제공합니다.

StatefulService는 StatefulServiceBase에서 파생됩니다. StatefulServiceBase 더 큰 유연성, 서비스를 제공 하지만 더 많은 서비스 패브릭의 hello 내부 이해 해야 합니다.
Hello 참조 [신뢰할 수 있는 서비스 개요](service-fabric-reliable-services-introduction.md) 및 [고급 사용 하는 신뢰할 수 있는 서비스](service-fabric-reliable-services-advanced-usage.md) 쓰기 hello StatefulService 및 StatefulServiceBase 클래스를 사용 하 여 서비스의 hello 사항에 대 한 자세한 내용은 .

기본 클래스를 모두 hello 수명 및 hello 서비스 구현의 역할을 관리합니다. hello 서비스 구현에서 hello 서비스 구현 수명 주기-이 시점에 작업 toodo에 있는 경우 또는 toocreate 통신 수신기 개체를 읽으려는 경우 hello 서비스 구현에서 기본 클래스의 가상 메서드를 재정의 될 수 있습니다. 참고는 서비스 구현에서 위의 hello 다이어그램 ICommunicationListener, 노출 자체 통신 수신기 개체를 구현할 수 있습니다 하지만 hello 통신 수신기를 구현 하는 서비스 패브릭으로-hello 서비스 구현으로 사용 하는 서비스 패브릭에서 구현 되는 통신 수신기 수 있습니다.

상태 저장 서비스의 신뢰할 수 있는 신뢰할 수 있는 컬렉션의 신뢰할 수 있는 상태 관리자 tootake 이점은 hello를 사용합니다. 신뢰할 수 있는 컬렉션은 로컬 데이터 구조를 항상 사용 가능한 toohello 서비스--는, 서비스 장애 조치에 관계 없이 사용할 수 있는 경우가 있습니다. 신뢰할 수 있는 컬렉션의 각 유형은 신뢰할 수 있는 상태 제공자에 의해 구현됩니다.
신뢰할 수 있는 컬렉션에 대 한 자세한 내용은 참조 hello [신뢰할 수 있는 컬렉션 개요](service-fabric-reliable-services-reliable-collections.md)합니다.

### <a name="reliable-state-manager-and-state-providers"></a>신뢰할 수 있는 상태 관리자와 제공자
hello 신뢰할 수 있는 상태 관리자는 신뢰할 수 있는 상태 공급자를 관리 하는 hello 개체입니다. Hello 기능 toocreate, 삭제, 열거 및 hello 신뢰할 수 있는 상태 공급자가 유지 되 고 항상 사용 가능한 확인 된이 있습니다. 신뢰할 수 있는 상태 제공자 인스턴스는 사전이나 큐와 같은 지속적이고 항상 사용 가능한 데이터 구조체의 인스턴스를 나타냅니다.

각 신뢰할 수 있는 상태 공급자는 상태 저장 서비스 toointeract hello 신뢰할 수 있는 상태 공급자와 함께 사용 되는 인터페이스를 노출 합니다. 예를 들어 IReliableDictionary 있고 hello 신뢰할 수 있는 사전으로 사용 되는 toointerface IReliableQueue hello 신뢰할 수 있는 큐와 toointerface를 사용된 합니다. 모든 신뢰할 수 있는 상태 공급자 hello IReliableState 인터페이스를 구현합니다.

hello 신뢰할 수 있는 상태 관리자 이라는 IReliableStateManager 상태 저장 서비스에서 액세스 tooit 수 있는 인터페이스를 있습니다. 인터페이스 tooreliable 상태 공급자 IReliableStateManager 통해 반환 됩니다.

hello 신뢰할 수 있는 상태 관리자는 새로운 유형의 신뢰할 수 있는 컬렉션 동적으로 연결 될 수 있도록 플러그 인 아키텍처를 사용 합니다.

신뢰할 수 있는 사전 hello 및 신뢰할 수 있는 큐는 고성능, 버전 관리 된 차등 저장소의 hello 구현 시 작성 됩니다.

### <a name="transactional-replicator"></a>트랜잭션 복제자
hello 트랜잭션 복제기 구성 요소는 hello 서비스를 실행 하는 모든 복제본 hello 상태 서비스 (즉, 신뢰할 수 있는 상태 관리자 hello 및 hello 신뢰할 수 있는 컬렉션 내에서 hello 상태)이 일치 하는지 확인 해야 합니다. 또한 hello 로그 hello 상태가 유지 되도록 보장 합니다. hello 개인 메커니즘을 통해 트랜잭션 복제기 hello와 관리자 인터페이스를 신뢰할 수 있는 상태입니다.

hello 트랜잭션 복제기 최신 상태 정보를 포함 하는 모든 복제 되도록 hello 서비스 인스턴스의 다른 복제본과 네트워크 프로토콜 toocommunicate 상태를 사용 합니다.

hello 트랜잭션 복제기 hello 상태 정보 프로세스 후에 유지 하거나 노드 충돌 로그 toopersist 상태 정보를 사용 합니다. 개인 메커니즘을 통해 hello 인터페이스 toohello 로그가입니다.

### <a name="log"></a>로그
hello 로그 구성 toospinning 또는 반도체 디스크를 쓰기 위한 최적화할 수 있는 고성능 영구 저장소를 제공 합니다.  hello 로그의 hello 디자인 hello 상태 저장 서비스를 실행 하는 toobe 로컬 toohello 노드가 hello 영구 저장소 (예: 하드 디스크)입니다. 따라서 낮은 대기 시간과 높은 처리량, 로컬 toohello 노드 하지 않는 비교 tooremote 영구 저장소로 있습니다.

hello 로그 구성 요소는 여러 로그 파일을 사용 합니다. 상태 데이터를 저장 하기 위한 hello 가장 낮은 대기 시간과 높은 처리량 제공할 수 있습니다 하는 대로 모든 복제본에서 사용 하는 노드 수준 공유 로그 파일이 있습니다. 기본적으로 hello 공유 로그는 hello 서비스 패브릭 노드 작업 디렉터리에 위치 하 하지만 hello 공유 로그에 대 한 예약 된 디스크에 이상적으로 다른 위치에 배치 하는 구성 된 toobe 수도 있습니다. 또한 각 복제본 hello 서비스에 대 한 전용된 로그 파일을 개이고 hello 전용된 로그 hello 서비스의 작업 디렉터리 내에 배치 됩니다. 다른 위치에 배치 되지 메커니즘 tooconfigure 전용 hello 로그 toobe 있습니다.

hello 공유 로그는 hello 복제본의 상태 정보에 대 한 전환 영역, hello 동안 전용된 로그 파일은 hello 최종 대상 유지 됩니다. 이 설계에 hello 상태 정보는 첫 번째 서 면된 toohello 공유 로그 파일 및 다음 지연 hello 백그라운드에서 toohello 전용된 로그 파일을 이동 합니다. 이러한 방식으로 hello 쓰기 toohello 공유 로그는 hello 가장 낮은 대기 시간 및 hello 서비스 toomake 진행 상황을 더 빠르게 수 있는 가장 높은 처리량 합니다.

읽기 및 쓰기 toohello 공유 로그 hello 공유 하는 로그 파일에 대 한 hello 디스크에 직접 IO toopreallocated 공간을 통해 수행 됩니다. 전용된 로그와 hello 드라이브에서 디스크 공간 사용을 최적화 하는 tooallow, hello 전용된 로그 파일에 NTFS 스파스 파일로 생성 됩니다. 이 사용할 수 있음을 3tb의 디스크 공간 및 hello 운영 체제는 실제로 사용 보다 훨씬 더 많은 디스크 공간을 사용 하 여 hello 전용 로그 파일에 표시 됩니다.

최소한의 사용자 모드 인터페이스 toohello 로그 외에도 hello 로그는 커널 모드 드라이버로 기록 됩니다. 커널 모드 드라이버를 실행 하 여 tooall 서비스를 사용 하는 hello 로그 hello 최고의 성능을 제공할 수 있습니다.

Hello 로그를 구성 하는 방법에 대 한 자세한 내용은 참조 [신뢰할 수 있는 상태 저장 서비스 구성](service-fabric-reliable-services-configuration.md)합니다.

## <a name="stateless-reliable-service"></a>상태 비저장 신뢰할 수 있는 서비스
### <a name="architecture-of-a-stateless-service"></a>상태 저장 서비스의 아키텍처
![상태 비저장 서비스의 아키텍처 다이어그램](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>상태 비저장 신뢰할 수 있는 서비스
상태 비저장 서비스 구현을 StatelessService hello 또는 StatelessServiceBase 클래스에서 파생 됩니다. hello StatelessServiceBase 클래스 hello StatelessService 클래스 보다 더 높은 유연성을 허용 합니다.
기본 클래스를 모두 hello 수명 및 서비스의 역할을 관리합니다.

hello 서비스에서 hello 서비스 수명 주기-이 시점에 작업 toodo에 또는 toocreate 통신 수신기 개체를 읽으려는 경우 hello 서비스 구현에서 기본 클래스의 가상 메서드를 재정의 될 수 있습니다. Hello 서비스 위의 hello 다이어그램에서 ICommunicationListener를 노출 하는 자체 통신 수신기 개체를 구현할 수 있지만 hello 통신 수신기를 구현 하는 서비스 패브릭에서 서비스 구현에는 통신을 사용 하는 참고 서비스 패브릭에서 구현 되는 수신기 수 있습니다.

Hello 참조 [신뢰할 수 있는 서비스 개요](service-fabric-reliable-services-introduction.md) 및 [고급 사용 하는 신뢰할 수 있는 서비스](service-fabric-reliable-services-advanced-usage.md) hello StatelessService 및 StatelessServiceBase 클래스를 사용 하 여 서비스를 작성의 hello 사항에 대 한 자세한 내용은 .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
서비스 패브릭에 대한 자세한 내용은 다음을 참조하세요.

[Reliable Services 개요](service-fabric-reliable-services-introduction.md)

[빠른 시작](service-fabric-reliable-services-quick-start.md)

[신뢰할 수 있는 컬렉션 개요](service-fabric-reliable-services-reliable-collections.md)

[Reliable Services 고급 사용법](service-fabric-reliable-services-advanced-usage.md)

[Reliable Services 구성](service-fabric-reliable-services-configuration.md)  

