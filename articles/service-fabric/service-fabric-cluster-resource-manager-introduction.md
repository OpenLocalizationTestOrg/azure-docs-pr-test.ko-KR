---
title: "서비스 패브릭 클러스터 리소스 관리자 aaaIntroducing hello | Microsoft Docs"
description: "소개 toohello 서비스 패브릭 클러스터 리소스 관리자입니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Hello 서비스 패브릭 클러스터 리소스 관리자 소개
일반적으로 IT 시스템 또는 온라인 서비스 관리 전용 특정 물리적 컴퓨터 또는 가상 컴퓨터 toothose 특정 서비스 또는 시스템 제공 됩니다. 서비스는 계층으로 설계되었습니다. “웹” 계층 및 “데이터” 또는 “저장소” 계층이 있었습니다. 응용 프로그램 요청 / 로그 아웃 컴퓨터 전용된 toocaching 집합도 전달 되는 메시징 계층을 것입니다. 각 계층 또는 작업의 형식에 특정 컴퓨터 전용된 tooit: hello 데이터베이스 두 개, 전용된 tooit 컴퓨터, 웹 서버 hello 몇 가지를 가져왔습니다. Hello 컴퓨터에서 부하가 심한 toorun 발생 하는 특정 유형의 작업을 하는 경우 동일한 구성 toothat 계층과 해당 컴퓨터를 더 추가 합니다. 그러나 일부 작업 아웃 쉽게 확장할 수 없습니다-더 큰 컴퓨터를 사용 하 여 컴퓨터 바꾸어 일반적으로 hello 데이터 계층과 특히 합니다. 간편성. 컴퓨터를 실패 한 경우 hello 컴퓨터를 복원할 수 있습니다 때까지 hello 전반적인 응용 프로그램의 해당 부분 낮은 용량으로 실행 합니다. (재미는 없더라도)아직 상당히 쉽습니다.

그러나 이제 서비스의 세계 hello 및 소프트웨어 아키텍처 변경 되었습니다. 응용 프로그램이 확장된 디자인을 채택하는 것이 좀 더 일반적인 것이 되었습니다. 컨테이너 또는 마이크로 서비스(또는 둘 다)로 응용 프로그램을 구축하는 것도 일반적인 것이 되었습니다. 이제 컴퓨터가 몇 대 없어도 단일 워크로드 인스턴스만 실행하지 않습니다. 수도 실행 되 고 있으므로 여러 다른 워크 로드가 hello에서 같은 시간입니다. 이제 다른 유형의 서비스(전체 컴퓨터의 리소스를 사용하지 않음)가 여러 개, 아마도 해당 서비스의 다른 인스턴스가 수백 개나 있을 것입니다. 명명된 인스턴스 각각에는 HA(고가용성)을 위해 하나 이상의 인스턴스 또는 복제본이 있습니다. 이러한 작업 및 빈도의 hello 크기에 따라 수백 또는 수천 대 컴퓨터를 직접 찾을 수 있습니다. 

갑자기 환경을 관리 하는 컴퓨터 전용된 toosingle 종류의 워크 로드 몇 가지 관리 하는 그리 간단 하지 않습니다. 서버는 가상 및 이름이 더 이상 (에서 태도가 전환한 [애완 동물 toocattle](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) 결국). 구성은 hello 서비스 자체에 대 한 hello 컴퓨터 등에 대 한 작은 경우 작업의 전용된 tooa 인스턴스가 하드웨어는 주로 hello 과거의 변화 합니다. 서비스 자체는 더 작은 상용 하드웨어 부분에 걸쳐 있는 작은 분산 시스템이 되었습니다.

앱 일련의 여러 계층 분산 일화 더 이상 이므로와 더 많은 조합 toodeal을 해야 합니다. 어떤 형식의 워크로드가 어떤 하드웨어에서 또는 몇 개의 하드웨어에서 실행될 수 있는지를 누가 결정하나요? 워크 로드는 동일 하 게 작동 hello에서 제대로 하드웨어 및 충돌? 컴퓨터가 가동 중단될 때 해당 컴퓨터에서 어떤 작업이 실행되고 있었는지를 어떻게 알 수 있나요? 워크로드가 다시 실행되기 시작하는지는 누가 확인하나요? (가상)? 컴퓨터 toocome 백 hello에 대 한 대기 하거나 수행 하면 작업 자동으로 장애 조치 tooother 컴퓨터 및 계속 실행? 사람의 개입이 필요하나요? 이러한 환경에서 업그레이드는 어떤가요?

개발자와이 환경에서 처리 하는 연산자 이러한 복잡성을 관리 하는 toowant 도움말을 하겠습니다. A binge 채용 하 고 사용자와 toohide hello 복잡성은 아닐 hello 정답, 따라서 어떻게 하 시겠습니까?

## <a name="introducing-orchestrators"></a>Orchestrator 소개
"Orchestrator"는 관리자가 이러한 유형의 환경 관리 하는 소프트웨어에 대 한 hello 일반 용어입니다. Orchestrators는 "좋을 것 내 환경에서 실행 되는이 서비스의 복사본이 5."와 같은 요청을 사용 하는 hello 구성 요소 Toomake hello 환경 일치 hello 원하는 상태, 수행 되는 작업에 관계 없이 시도 합니다.

Orchestrator(사람 아님)는 컴퓨터가 실패하거나 예기치 않은 이유로 워크로드를 종료하는 경우 조치를 취합니다. 대부분의 Orchestrator는 오류 처리 이상의 작업을 수행합니다. 다른 기능으로는 새 배포를 관리하고 업그레이드를 처리하며 리소스 사용 및 거버넌스를 처리하는 작업이 있습니다. 모든 orchestrators은 hello 환경에서 구성의 일부 원하는 상태를 유지 하는 방법에 대 한 기본적입니다. Toobe 수 tootell는 orchestrator 원하는 고 원하는 하 게 작업을 대신 hello지 않습니다. Mesos, Docker Datacenter/Docker Swarm, Kubernetes 및 Service Fabric에 기반하는 Aurora는 모두 Orchestrator의 예입니다. 이러한 orchestrators 프로덕션 환경에서 실제 작업 부하의 적극적으로 개발 된 toomeet hello 요구 되는 합니다. 

## <a name="orchestration-as-a-service"></a>서비스인 Orchestration
hello 클러스터 리소스 관리자는 서비스 패브릭에서 오케스트레이션을 처리 하는 hello 시스템 구성 요소입니다. hello 클러스터 리소스 관리자 작업은 세 부분으로 나누어집니다.

1. 규칙 적용
2. 환경 최적화
3. 다른 프로세스 지원

toosee hello 클러스터 리소스 관리자의 작동 방식, Microsoft Virtual Academy 비디오 다음 조사식 hello:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>잘못된 정의
일반적인 N 계층 응용 프로그램에는 항상 [Load Balancer](https://en.wikipedia.org/wiki/Load_balancing_(computing))가 있습니다. 일반적으로이 네트워크 부하 분산 (NLB) 또는 응용 프로그램 부하 분산 장치 (ALB) hello 네트워킹 스택에 채도 위치에 따라 이었습니다. 일부 부하 분산 장치는 F5의 BigIP 제품과 같은 하드웨어 기반이며 나머지는 Microsoft의 NLB와 같은 소프트웨어 기반입니다. 다른 환경에서는 이 역할에서 HAProxy, nginx, Istio 또는 Envoy와 같은 항목을 확인할 수 있습니다. 이러한 아키텍처에서 로드 균형 조정의 hello 작업은 tooensure 상태 비저장 워크 로드 수신 hello 개략적인 작업 시간 동일 합니다. 부하를 분산하는 전략은 다양합니다. 일부 분산 각 다른 호출 tooa 다른 서버로를 보내집니다. 다른 기능은 세션 고정/인력을 제공했습니다. 더 많은 고급 분산 실제 부하 예측 또는 보고 tooroute 예상된 비용 및 현재 시스템 로드에 따라 호출을 사용 합니다.

웹/작업자 계층 hello 네트워크 분산 장치 또는 메시지 라우터 시도 tooensure 대략 균형 유지 합니다. 데이터 계층 hello를 분산 하기 위한 전략에는 다른 및 hello 데이터 저장소 메커니즘에 종속 했습니다. 데이터 분할, 캐싱, 관리 되는 뷰, 저장된 프로시저 및 기타 저장소별 메커니즘에 의존 hello 데이터 계층을 분산 합니다.

흥미로운 다음이 전략 중 일부가 동안 hello 서비스 패브릭 클러스터 리소스 관리자가 되지 네트워크 부하 분산 장치 또는 캐시 됩니다. 네트워크 Load Balancer는 여러 프런트 엔드에 트래픽을 분산하여 프런트 엔드에서 부하를 분산합니다. 서비스 패브릭 클러스터 리소스 관리자 hello 다른 전략을 있습니다. 서비스 패브릭 이동 근본적으로 *서비스* toowhere 트래픽 예상 하는 가장 좋은 hello 또는 toofollow 로드 구성 합니다. 예를 들어 홥 hello 서비스 많은 작업을 수행 하지 않습니다 하므로 현재 콜드 있는 서비스 toonodes를 이동 될 수 있습니다. 이후 hello 서비스를 삭제 또는 다른 곳에서 이동 된 hello 노드 콜드 수 있습니다. 또 다른 예로, hello 클러스터 리소스 관리자는 컴퓨터에서 서비스를 이동할 수도 있습니다. 아마도 hello 컴퓨터 toobe 업그레이드에 대 한 과부화 된 소비에서 tooa 급증 때문에 실행 하는 hello 서비스에 의해 합니다. Alernatively, hello 서비스의 리소스 요구 사항을 커졌을 수 있습니다. 따라서 실행 하는이 컴퓨터 toocontinue에 충분 한 리소스가 없습니다. 

Hello 클러스터 리소스 관리자 서비스 주위 이동 이기 때문에 네트워크 부하 분산 장치에서 볼 수는 서로 다른 기능 집합 비교 toowhat 포함 되어 있습니다. 이 네트워크 부하 분산 장치는 해당 위치는 hello 서비스 자체를 실행 하는 데 적절 하지 하는 경우에 서비스는 이미, 네트워크 트래픽 toowhere 제공 하기 때문에 있습니다. 서비스 패브릭 클러스터 리소스 관리자 hello hello hello 클러스터 리소스는 효율적으로 활용을 위한 기본값과 다른 전략을 사용 합니다.

## <a name="next-steps"></a>다음 단계
- 에 대 한 내용은 hello 클러스터 리소스 관리자 내에서 hello 아키텍처 및 정보 흐름을 체크 아웃 [이 문서](service-fabric-cluster-resource-manager-architecture.md)
- 클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다. toofind 메트릭에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)
- 서비스 구성에 대한 자세한 내용은 [서비스 구성](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.
- 메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다. 메트릭 및 어떻게 tooconfigure로 체크 아웃 하는 방법에 대 한 자세한 toolearn [이 문서](service-fabric-cluster-resource-manager-metrics.md)
- hello 클러스터 리소스 관리자 서비스 패브릭 관리 기능을 사용 합니다. 해당 통합에 대 한 자세한 내용을 toofind 읽을 [이 문서](service-fabric-cluster-resource-manager-management-integration.md)
- toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)
