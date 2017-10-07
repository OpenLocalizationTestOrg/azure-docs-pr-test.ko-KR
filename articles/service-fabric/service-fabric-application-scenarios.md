---
title: "aaaApplication 시나리오 및 디자인 | Microsoft Docs"
description: "서비스 패브릭의 클라우드 응용 프로그램 범주 개요 상태 저장 및 상태 비저장 서비스를 사용하는 응용 프로그램 설계에 대해 논의합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>서비스 패브릭 응용 프로그램 시나리오
Azure 서비스 패브릭 toowrite를 사용 하면 있는 안정적 이며 유연한 플랫폼을 제공 하 고 다양 한 유형의 비즈니스 응용 프로그램 및 서비스를 실행 합니다. 이러한 응용 프로그램과 microservices 수, 상태 저장 또는 상태 비저장 있으며 toomaximize 효율성 가상 컴퓨터 간에 리소스 균형 조정 됩니다. 서비스 패브릭의 고유한 아키텍처 hello tooperform을 거의 실시간 데이터 분석, 메모리에서 계산, 병렬 트랜잭션 및 이벤트 처리 응용 프로그램에 있습니다. 리소스 요구 사항의 변화에 따라 응용 프로그램을 간단하게 확장 또는 축소(실제 내부 또는 외부)할 수 있습니다.

Azure의 hello 서비스 패브릭 플랫폼은 응용 프로그램의 범주를 수행 하는 hello에 대 한 적합 합니다.

* **가용성이 높은 서비스**: 서비스 패브릭 서비스는 여러 보조 서비스 복제본을 만들어 신속한 장애 조치(failover)를 제공합니다. 노드, 프로세스 또는 개별 서비스 toohardware 또는 다른 실패 인해 다운 되 면 서비스 손실이 최소화 승격된 tooa 주 복제본 hello 보조 복제본 중 하나입니다.
* **확장 가능한 서비스**: 개별 서비스를 분할할 수 상태 toobe hello 클러스터 전체로 확장에 대 한 허용 합니다. 또한 개별 서비스를 작성 및 hello 신속 하 게 제거 합니다. 서비스 수를 인스턴스 노드가 여러 개인 경우에 몇 가지 노드 toothousands의 몇 가지 인스턴스와 확장할 신속 하 고 쉽게 있으며 다음 배율에 따라 다시 리소스 요구 사항에 따라. 서비스 패브릭 toobuild 이러한 서비스를 사용 하 고 전체 주기를 관리할 수 있습니다.
* **비정적 데이터에서 계산**: toobuild 데이터, 입/출력 및 계산 집약적인 상태 저장 응용 프로그램 서비스 패브릭 수 있습니다. 서비스 패브릭 응용 프로그램에 hello 배치 (계산)를 처리 및 데이터를 허용 합니다. 일반적으로 응용 프로그램 액세스 toodata를 해야 하는 경우 외부 데이터 캐시 또는 저장소 계층와 연결 된 네트워크 대기 시간이입니다. 대기 시간이 제거된 상태 저장 서비스 패브릭 서비스를 사용하면 읽고 쓰는 기능을 더 사용할 수 있습니다. 예를 들어 100밀리초 보다 적은 왕복 시간을 요구하는 고객에게 실시간 권장 사항을 선택하도록 하는 응용 프로그램이 있다고 가정합니다. 서비스 패브릭 서비스 (여기서 권장 사항 선택의 hello 계산 배치 하는 hello 데이터와 규칙)의 hello 대기 시간 및 성능 특성은 hello 표준 구현에 비해 응답 경험 toohello 사용자 제공 원격 저장소에서 toofetch hello 필요한 데이터의 모델입니다.  
* **세션 기반 대화형 응용 프로그램**: 온라인 게임 또는 인스턴트 메시징 같은 응용 프로그램의 읽기 및 쓰기 대기 시간이 짧아야 하는 경우 서비스 패브릭이 유용합니다. 서비스 패브릭 별도 저장소 또는 상태 비저장 응용 프로그램 필요에 따라 캐시 toocreate 필요 없이 toobuild 있습니다 이러한 대화형, 상태 저장 응용 프로그램이 있습니다. (대기 시간이 증가하고 잠재적으로 일관성 문제가 시작됩니다.)
* **데이터 분석 및 워크플로**: hello 빠른 읽기 및 쓰기 서비스 패브릭의 이벤트 또는 데이터 스트림을 안정적으로 처리 해야 하는 응용 프로그램을 설정 합니다. 서비스 패브릭 해줍니다 결과 안정적이 고 전달 해야 하는 처리 파이프라인에 설명 하는 응용 프로그램 처리 손실 없이 단계 옆에 toohello 합니다. 데이터 일관성 및 계산 보장이 필수적인 트랜잭션 및 재무 시스템을 포함합니다.
* **데이터 수집, 처리 및 IoT**: 이기 때문에 서비스 패브릭 대규모 처리 되었으며 해당 상태 저장 서비스를 통해 낮은 대기 시간, 수백만 개의 장치에 대 한 데이터 처리에 대 한 이상적인 hello 장치 및 hello 계산에 대 한 hello 데이터 있는 배치 됩니다.
[BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) 및 [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/)를 포함한 Service Fabric을 사용하여 IoT 시스템을 구축한 여러 고객을 살펴봤습니다.

## <a name="application-design-case-studies"></a>응용 프로그램 디자인 사례 연구
다양 한 서비스 패브릭 toodesign 사용 되는 응용 프로그램은 하는 방법을 보여 주는 사례 연구 hello에 게시 된 [서비스 패브릭 팀 블로그](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) 및 hello [microservices 솔루션 사이트](https://azure.microsoft.com/solutions/microservice-applications/)합니다.

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>상태 비저장 및 상태 저장 마이크로 서비스로 구성된 응용 프로그램 설계
Azure Cloud Service 작업자 역할이 있는 응용 프로그램을 구축하는 것은 상태 비저장 서비스의 예입니다. 반면, 상태 저장 microservices hello 요청 및 응답 이외의 신뢰할 수 있는 상태를 유지 합니다. 고가용성 및 복제에서 지 원하는 트랜잭션 보장을 제공 하는 단순 Api 통해 hello 상태의 일관성을 제공 합니다. 서비스 패브릭의 상태 저장 서비스 공유할 고가용성을 tooall 종류의 응용 프로그램, 뿐 아니라 데이터베이스와 다른 데이터 저장소 상태로 전환 합니다. 자연적 진행 방향입니다. 응용 프로그램 고가용성 tooNoSQL 데이터베이스에 대 한 순수 관계형 데이터베이스를 사용 하 여 이미 옮겼습니다. 이제 hello 응용 프로그램 자체의 "핫" 상태 및 안정성, 일관성, 또는 가용성을 유지 하면서 추가적인 성능 향상을 위해 내에서 관리 되는 데이터 있을 수 있습니다.

일반적으로 상태 비저장 웹 응용 프로그램 (ASP.NET, Node.js 등)의 조합이 있는 microservices로 구성 된 응용 프로그램을 빌드하는 경우 상태 비저장 및 상태 저장 비즈니스 중간 계층 서비스에 호출을 모두 배포 hello에 동일한 서비스 패브릭 클러스터 hello 서비스 패브릭 배포 명령을 사용 합니다. 이러한 각 서비스는 독립적 큰지에 tooscale, 안정성 및 자원 배정 현황을, 개발 및 수명 주기 관리에 유연성을 크게 향상 시킵니다.

상태 저장 microservices hello 추가 큐에 대 한 hello 요구를 제거 하 고 있는 것은 필수 tooaddress 전통적 캐시 hello 순수 하 게 상태 비저장 응용 프로그램의 가용성 및 대기 시간 요구 사항 때문에 응용 프로그램 디자인을 단순화 합니다. 상태 저장 서비스는 기본적으로 항상 사용 가능 하 고 낮은 대기 시간, 전체적으로 응용 프로그램에서 더 적은 수의 이동 부분 toomanage 됨을 의미 합니다. 아래 hello 다이어그램 디자인 하 고 상태를 저장 하는 상태 비저장 응용 프로그램 간의 hello 차이 보여 줍니다. Hello을 이용 하 여 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) 및 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 프로그래밍 모델, 상태 저장 서비스 응용 프로그램을 간단 하면서 높은 처리량과 낮은 대기 시간을 달성 합니다.

## <a name="an-application-built-using-stateless-services"></a>상태 비저장 서비스를 사용하여 빌드된 응용 프로그램
![상태 비저장 서비스를 사용하는 응용 프로그램][Image1]

## <a name="an-application-built-using-stateful-services"></a>상태 저장 서비스를 사용하여 빌드된 응용 프로그램
![상태 비저장 서비스를 사용하는 응용 프로그램][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계

* 너무 수신[고객 사례 연구](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* [고객 사례 연구](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)에 대해 알아보세요.
* [패턴 및 시나리오](service-fabric-patterns-and-scenarios.md)에 대해 자세히 알아보세요.

* 서비스 패브릭 hello 사용 하 여 상태 비저장 및 상태 저장 서비스를 구축 [신뢰할 수 있는 서비스](service-fabric-reliable-services-quick-start.md) 및 [신뢰할 수 있는 작업자](service-fabric-reliable-actors-get-started.md) 프로그래밍 모델입니다.
* 또한 hello 다음 항목을 참조 하십시오.
  * [마이크로 서비스 정보](service-fabric-overview-microservices.md)
  * [서비스 상태 정의 및 관리](service-fabric-concepts-state.md)
  * [서비스 패브릭 서비스의 가용성](service-fabric-availability-services.md)
  * [서비스 패브릭 서비스 크기 조정](service-fabric-concepts-scalability.md)
  * [서비스 패브릭 서비스 분할](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
