---
title: "Microsoft Azure Service Fabric에 대 한 질문 aaaCommon | Microsoft Docs"
description: "다음은 Service Fabric에 대해 자주 묻는 몇 가지 질문과 그에 대한 답변입니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Service Fabric에 대해 자주 묻는 질문

Service Fabric으로 수행할 수 있는 작업 및 사용 방법에 대한 여러 가지 자주 묻는 질문이 있습니다. 이 문서에서는 자주 묻는 질문 및 그에 대한 답변을 설명합니다.

## <a name="cluster-setup-and-management"></a>클러스터 설정 및 관리

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>여러 Azure 지역 또는 나만의 데이터 센터에 걸쳐서 클러스터를 만들 수 있나요?

예. 

네트워크 연결 tooeach 다른 것으로 hello core 서비스 패브릭 클러스터링 기술 hello world에서 요소가 실행 되 고 사용 하는 toocombine 컴퓨터를 수 있습니다. 그러나 이러한 클러스터를 구축하고 실행하는 것은 복잡할 수 있습니다.

이 시나리오에 관심이 있다면 의견을 교환하실 연락처에서 tooget hello 통해 [서비스 패브릭 Github 문제 목록](https://github.com/azure/service-fabric-issues) 또는 순서 tooobtain 추가 설명서에 지원 담당자를 통해. 서비스 패브릭 팀 hello tooprovide 추가 명확성, 지침 및 권장 사항이이 시나리오에 대 한 작동 합니다. 

일부 작업 tooconsider: 

1. hello azure에서 서비스 패브릭 클러스터 리소스는 오늘 지역별, 마찬가지로 해당 hello 클러스터를 설정 하는 hello 가상 컴퓨터 크기는 기반으로 합니다. 이 있음을 의미 국가별 실패의 hello 이벤트에서 있습니다 수 hello Azure 리소스 관리자를 통해 hello 기능 toomanage hello 클러스터 손실 hello Azure 포털입니다. 이 hello 클러스터를 계속 실행 하 고 직접 수 toointeract 함께 있을 수 있습니다 하는 경우에 발생할 수 있습니다. 또한 Azure 오늘날 제공 하지 않습니다 hello 기능 toohave 지역에 걸쳐 사용할 수 있는 단일 가상 네트워크. 즉, Azure의 다중 지역 클러스터 어느 하나라도 필요한 [hello VM 크기 집합의에서 각 VM에 대 한 공용 IP 주소](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) 또는 [Azure VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다. 이러한 네트워킹 선택을 시킬 다른 비용, 성능 및 toosome도 응용 프로그램 디자인 주의 깊은 분석과 계획 순위 이러한 환경 구성 하기 전에 필요 하므로.
2. hello 유지 관리, 관리 및이 시스템의 모니터링 될 수 있습니다, 복잡 한에 확대 하는 경우에 특히 _형식_ 환경 등 다른 클라우드 공급자 또는 온-프레미스 리소스와 Azure 간 . 업그레이드 tooensure, 모니터링, 관리, 주의 해야 하 고 진단은 이러한 환경에서 프로덕션 작업을 실행 하기 전에 hello 클러스터와 hello 응용 프로그램에 대 한 이해 합니다. Azure에서 또는 자체 데이터 센터 내에서 이러한 문제를 여러 번 해결해본 적이 있으면 Service Fabric 클러스터를 구축하거나 실행할 때도 이러한 동일한 해결 방법을 적용할 수 있습니다. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Service Fabric 노드에서 OS 업데이트를 자동으로 수신하나요?

오늘 하지 있지만이 또한 Azure 노드가 toodeliver는 일반적으로 요청 합니다.

중간 hello에 [응용 프로그램 제공](service-fabric-patch-orchestration-application.md) hello 운영 체제 서비스 패브릭 노드 아래 패치가 적용 되 고 toodate를 유지 하 합니다.

hello 챌린지 OS 업데이트를 임시 가용성 손실이 발생 하는 hello 컴퓨터에 대 한 다시 부팅 일반적으로 필요가 없다고입니다. 자체적으로 하지 않으므로 문제가 서비스 패브릭 서비스 tooother 노드에 대 한 트래픽을 자동 리디렉션됩니다. 그러나 OS 업데이트는 hello 클러스터 전체에서 조정 하지 않은, 경우 한 번에 많은 노드 아래로 이동 하는 hello 잠재적인은. 이러한 동시 재부팅은 서비스 또는 적어도 특정 파티션(상태 저장 서비스)에 대한 총체적인 가용성 손실을 유도할 수 있습니다.

Hello 이후에서 계획 toosupport OS 업데이트 정책을 완전히 자동화 하 고 업데이트 도메인에 걸쳐 조정 되는 기타 예기치 않은 실패 및 다시 부팅 가용성 유지 되도록 보장입니다.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>SF 클러스터 내에서 큰 가상 컴퓨터 크기 집합을 사용할 수 있나요? 

**간단한 대답** - 아니요 

**긴 응답** hello 큰 가상 컴퓨터 크기 집합 tooscale 허용 하지만-가상 컴퓨터 크기 집합 최대 1000 VM 인스턴스, hello 배치 그룹 (PGs)를 사용 하 여 작업을 수행 합니다. 오류 도메인 (Fd) 및 업그레이드 도메인 (Ud)은 배치 그룹 서비스 패브릭에서는 Ud와 Fd toomake 배치 결정 서비스 복제본/서비스 인스턴스 내에서 일관 된 수만 있습니다. Hello Fd 및 Ud 비교 가능한 이므로 배치 그룹 내 에서만 SF 사용할 수 없습니다. 예를 들어 p g 1에서 v m 1의 FD 토폴로지 = 0 PG2에 VM9 FD의 토폴로지 있으며 = 4, v m 1과 v m 2는 두 개의 서로 다른 하드웨어 랙에, SF가이 case toomake 배치 결정에 hello FD 값을 사용할 수 없습니다는 따라서 의미 하지 않습니다.

다른 문제가 있습니다 큰 가상 컴퓨터 크기 집합 현재 처럼 수준-4 hello 부족 부하 분산 지원 합니다. Toofor 참조 [큼에 대 한 세부 정보 집합의 크기를 조정](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>서비스 패브릭 클러스터의 최소 크기 hello 이란? 작으면 안되는 이유는 무엇인가요?

프로덕션 작업을 실행 하는 서비스 패브릭 클러스터에 대 한 최소 지원 되는 크기를 hello는 5 개의 노드가 있습니다. 개발/테스트 시나리오에 대해 3개의 노드 클러스터를 지원합니다.

이러한 최소값 hello 서비스 패브릭 클러스터 hello 명명 서비스와 hello 장애 조치 관리자를 포함 하 여 시스템 상태 저장 서비스의 집합을 실행 하기 때문에 존재 합니다. 되었습니다 서비스를 추적 하는 이러한 서비스 toohello 클러스터를 배포 하 고 이러한 서비스는 호스팅되 현재 위치 강력한 일관성에 따라 다릅니다. 강력한 일관성 해당 차례로 hello 기능 tooacquire에 따라 달라 집니다는 *쿼럼* 특정된 업데이트에 대 한 이들의 toohello 상태 서비스, 쿼럼 엄격 하 게 다 수의 지정된 된 서비스에 대 한 hello 복제본 (N/2 + 1)을 나타냅니다.

배경 정보로 몇 가지 가능한 클러스터 구성을 살펴보겠습니다.

**한 노드에서**: 어떤 이유로 든 hello 단일 노드의 hello 손실을 hello 전체 클러스터 hello 손실 의미 하므로이 옵션 고가용성을 제공 하지 않습니다.

**두 개 노드**: 두 노드(N = 2) 간에 배포된 서비스의 쿼럼은 2(2/2 + 1 = 2)입니다. 단일 복제본을 잃어버린 경우 불가능 한 toocreate 쿼럼 있습니다. 서비스 업그레이드를 수행하려면 복제본을 일시적으로 종료해야 하므로 유용한 구성이 아닙니다.

**3 개의 노드가**: 3 개의 노드 (N = 3), hello 요구 사항 toocreate 쿼럼은 여전히 두 노드 (3/2 + 1 = 2). 따라서 개별 노드를 손실하고 쿼럼을 계속 유지할 수 있습니다.

hello 3 개 노드 클러스터 구성 대해서는 개발/테스트 안전 하 게 업그레이드를 수행 하 고 개별 노드 실패 수 있으므로으로 동시에 발생 하지 않습니다. 프로덕션 작업에 대해 5 개의 노드가 필요 하므로 탄력적인 toosuch 동시 실패 이어야 합니다.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>밤/주말 toosave 비용에 클러스터를 해제할 수 있습니까?

일반적으로 그렇지 않습니다. 서비스 패브릭 상태를 저장 임시 로컬 디스크에는 hello 가상 컴퓨터가 다른 호스트로 이동된 tooa 이면 hello 데이터 이동 하지 않습니다 것을 의미 합니다. 정상 작업에서 하는 문제가 되지 않습니다는 hello 새 노드에 다른 노드가 toodate에 가져오는 됩니다. 그러나 모든 노드를 중지 하 고 나중에 다시 시작 하는 경우 대부분의 hello 노드 새 호스트에서 시작한 hello 시스템 없습니다 toorecover 확인 상당한 가능성은.

배포 하기 전에 응용 프로그램을 테스트 하는 것에 대 한 toocreate 클러스터, 원하는 경우 해당 클러스터의 일부로 동적으로 만드는 것이 좋습니다 프로그램 [연속 통합/연속 배포 파이프라인](service-fabric-set-up-continuous-integration.md)합니다.


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>(예: Windows Server 2012 tooWindows 서버 2016)에서 내 운영 체제를 업그레이드 하려면 어떻게 해야 합니까?

오늘날, 개선된 된 환경에서 작업 중 동안 사용자는 hello 업그레이드에 대 한입니다. Hello에 hello OS 이미지를 업그레이드 해야 hello의 가상 컴퓨터를 한 번에 하나의 VM 클러스터입니다. 

## <a name="container-support"></a>컨테이너 지원

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>주소 내 된 컨테이너를 배포 된 tooSF 없습니다 tooresolve DNS 이유는 무엇입니까?

이 문제는 5.6.204.9494 버전의 클러스터에 대해 보고되었습니다. 

**완화** : 따라 [이 문서](service-fabric-dnsservice.md) tooenable hello DNS 서비스 패브릭 클러스터에는 서비스입니다.

**해결** : 지원 되는 업그레이드 tooa 클러스터 버전 사용 가능 해지면 5.6.204.9494, 보다 높은입니다. 클러스터 tooautomatic 업그레이드 설정 되 면 hello 클러스터에는 고정이 문제가 있는 toohello 버전 자동 업그레이드 됩니다.

  
## <a name="application-design"></a>응용 프로그램 설계

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>신뢰할 수 있는 컬렉션의 파티션에서 hello 가장 좋은 방법은 tooquery 데이터 란?

신뢰할 수 있는 컬렉션은 일반적으로 [분할](service-fabric-concepts-partitioning.md) tooenable 큰 성능 및 처리량에 대 한 확장 합니다. 즉, 지정된 된 서비스에 대 한 hello 상태 또는 수 억 컴퓨터의 단위: 100에서 확산 시킬 수 있습니다. 해당 전체 데이터 집합에 대해 tooperform 작업을 몇 가지 옵션은 있습니다.

- 다른 서비스 toopull hello 필요한 데이터에서의 모든 파티션이 쿼리 하는 서비스를 만듭니다.
- 다른 서비스의 모든 파티션에서 데이터를 수신할 수 있는 서비스를 만듭니다.
- 각 서비스 tooan 외부 저장소에서 데이터를 주기적으로 푸시하십시오. 이 방법은 hello 쿼리를 수행 하는 핵심 비즈니스 논리의 일부가 아닌 경우 적절 한만 합니다.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>내 작업자 간에 hello 가장 좋은 방법은 tooquery 데이터 란?

작업자는 상태의 디자인 된 toobe 독립적 단위 및 계산의 경우, 것 이므로 tooperform 런타임에 행위자 상태의 광범위 한 쿼리를 권장 합니다. 행위자 상태의 전체 집합 hello 필요 tooquery를 설정한 경우 중 하나를 고려해 야:

- Hello 요청 수입니다. 네트워크 toogather 모든 데이터 서비스에 있는 파티션의 행위자 toohello 수의 hello 수에서 되도록 행위자 서비스 상태 저장 reliable services 대체 됩니다.
- 행위자 tooperiodically 푸시 쉽게 쿼리를 위한 해당 상태 tooan 외부 저장소를 디자인 합니다. 으로 위에이 방법은 hello 쿼리를 수행 하는 런타임 동작에 대 한 필요 하지 않은 경우에 적합 합니다.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Reliable Collection에 저장할 수 있는 데이터는 얼마나 되나요?

신뢰할 수 있는 서비스는 hello hello 클러스터에 있는 컴퓨터 수와 이러한 컴퓨터에서 사용 가능한 메모리 양에 hello에 의해서만 제한 hello 금액을 저장할 수 있으므로 일반적으로 분할 됩니다.

예를 들어, 평균 1kb 크기의 개체를 저장하는 100개 파티션과 3개 복제본이 있는 서비스에 Reliable Collection이 있다고 가정합니다. 이제 컴퓨터당 16gb의 메모리가 있는 10개의 컴퓨터 클러스터가 있다고 가정합니다. 간소 성 및 toobe 지점에 대 한 hello 운영 체제 및 시스템 서비스, hello 서비스 패브릭 런타임을 서비스 6gb의는 10gb의 사용 가능한 시스템 당 또는 100gb hello 클러스터에 대 한 종료를 사용을 가정 합니다.

각 개체는 세 번(주에서 1번, 복제본에서 2번) 저장되어야 하며 전체 용량으로 작동할 때 컬렉션에서 약 3천 500만 개체에 대해 충분한 메모리를 포함합니다. 그러나 오류 도메인과 업그레이드 도메인 hello 숫자 tooroughly 23 백만 높이면를 용량의 1/3에 대 한 정보를 나타내며의 복원 력이 toohello 동시 손실 되는 것이 좋습니다.

이 계산에서는 다음 사항도 가정합니다.

- Hello 파티션 간에 데이터의 해당 hello 분포는 균일 한 또는 부하 메트릭을 toohello 클러스터 리소스 관리자를 보고 하는 약입니다. 기본적으로 Service Fabric은 복제본 수에 따라 부하 분산을 수행합니다. 위의 예제에서는 hello 클러스터의 각 노드에서 10 개의 주 복제본과 보조 복제본을 20를 추가 하는 됩니다. 부하가 hello 파티션 간에 고르게 분산 되는 잘 작동 합니다. 부하를 없는 경우도 hello 리소스 관리자 및 수 있도록 더 작은 복제본 함께 팩 큰 복제본 tooconsume 더 많은 메모리를 개별 노드에서 부하를 보고 해야 합니다.

- 에 해당 hello 신뢰할 수 있는 서비스는 hello hello 클러스터에 하나의 저장 상태입니다. 여러 서비스 tooa 클러스터를 배포할 수 해야 toobe 각각은 toorun 필요 하 고 관리할 수 있는 상태로 hello 리소스에 주의 합니다.

- 해당 hello 클러스터 자체 증가 하지 않았거나, 축소. 더 많은 컴퓨터를 추가 하면 서비스 패브릭은 균형을 다시 조정할 복제본 tooleverage hello 추가 용량 개별 복제 컴퓨터에 걸쳐 있을 수 있으므로 컴퓨터 수가 hello 회 hello 서비스에는 파티션 수를 초과 될 때까지 합니다. 이와 반대로 컴퓨터를 제거 하 여 hello hello 클러스터 크기를 줄이고 복제본을 더 밀접 하 게 압축할 수 및 전체 용량이 부족 합니다.

### <a name="how-much-data-can-i-store-in-an-actor"></a>행위자에 저장할 수 있는 데이터는 얼마나 되나요?

신뢰할 수 있는 서비스와 마찬가지로 hello 행위자 서비스에 저장할 수 있는 데이터 양은 hello 총 디스크 공간을 사용할 수 있는 메모리도 클러스터의 hello 노드에서 제한만 됩니다. 그러나 개별 배우는 사용 되는 상태 및 연결 된 비즈니스 논리의 양이 tooencapsulate 상태일 때 가장 효과적입니다. 일반적으로 개별 행위자는 킬로바이트 단위로 측정되는 상태를 포함하게 됩니다.

## <a name="other-questions"></a>기타 질문

### <a name="how-does-service-fabric-relate-toocontainers"></a>서비스 패브릭 toocontainers를 연결 하는 방법

컨테이너 환경 모두에서 일관성 있게 실행 및 단일 컴퓨터에서 격리 된 방식으로 작동할 수 있도록 하는 간단한 방법 toopackage 서비스와 해당 종속성을 제공 합니다. 서비스 패브릭 방식으로 toodeploy 제공 및 서비스를 포함 하 여 관리 [서비스 컨테이너에 패키지 된](service-fabric-containers-overview.md)합니다.

### <a name="are-you-planning-tooopen-source-service-fabric"></a>서비스 패브릭 tooopen 소스 계획 입니까?

GitHub에서 tooopen 소스 hello에 대 한 신뢰할 수 있는 서비스 및 신뢰할 수 있는 작업자 프레임 워크를 의도 하 고 커뮤니티 기여 toothose 프로젝트를 수락 합니다. Hello 따라 [서비스 패브릭 블로그](https://blogs.msdn.microsoft.com/azureservicefabric/) 발표 하는 대로 자세한 세부 정보에 대 한 합니다.

hello는 현재 계획 tooopen 소스 hello 서비스 패브릭 런타임을 없습니다.

## <a name="next-steps"></a>다음 단계

- [핵심 Service Fabric 개념 및 모범 사례에 대해 알아보기](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
