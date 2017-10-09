---
title: "서비스 패브릭 재해 복구 aaaAzure | Microsoft Docs"
description: "Azure 서비스 패브릭 hello 모든 재해 유형에 필요한 toodeal 기능을 제공합니다. 이 문서에서는 발생할 수 있는 재해의 hello 유형의 설명와 방법을 사람과 toodeal 합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Azure 서비스 패브릭에서 재해 복구
고가용성 전달의 중요한 부분은 서비스가 다른 모든 유형의 오류를 감당할 수 있는지 확인하는 것입니다. 계획되지 않으며 사용자 통제 하에 있지 않은 오류의 경우 특히 이러한 과정이 중요합니다. 이 문서에서는 올바르게 모델링 및 관리되지 않는 경우 재해가 될 수 있는 몇 가지 일반적인 오류 모드에 대해 설명합니다. 또한 재해 그래도 발생 한 경우 tootake 완화 기능 및 동작을 설명 합니다. hello 목표는 toolimit 또는 계획 된 오류가 발생 하거나 그렇지 않으면 발생할 때 가동 중지 시간 또는 데이터 손실의 hello 위험을 제거 합니다.

## <a name="avoiding-disaster"></a>재해 방지
서비스 패브릭의 기본 목표는 사용자 환경 및 일반적인 오류 유형을 재해 없는 방식으로 서비스를 모두 모델 toohelp입니다. 

일반적으로 다음과 같은 두 가지 유형의 재해/오류 시나리오가 있습니다.

1. 하드웨어 또는 소프트웨어 오류
2. 작동 오류

### <a name="hardware-and-software-faults"></a>하드웨어 및 소프트웨어 오류
하드웨어 및 소프트웨어 오류는 예측할 수 없습니다. 가장 쉬운 방법은 toosurvive 오류 hello 하드웨어 또는 소프트웨어 오류 경계를 넘어 스팬 hello 서비스를 제거할 수 없습니다. 예를 들어 서비스를 하나의 특정 컴퓨터에만 실행 하는 경우 다음 hello 한 해당 컴퓨터의 오류는 해당 서비스에 대 한 재해 합니다. hello 간단한 방법을 tooavoid이이 재해는 hello 서비스가 여러 컴퓨터에서 실행 되 고 실제로 tooensure입니다. 테스트는 또한 필요한 tooensure hello 실패 한 컴퓨터의 서비스를 실행 하는 hello를 방해 하지 않습니다. 용량 계획 하면 다른 곳에서 대체 인스턴스를 만들 수 수 용량이 감소 남아 있는 서비스는 hello 오버 로드 되지는 않습니다. hello 동일한 패턴의 tooavoid hello 실패를 시도 하는 내용에 관계 없이 작동 합니다. 예를 들어 모바일 서비스는 스크립트 실행 간에 상태를 유지하지 않으므로 스크립트 실행 간에 지속되어야 하는 모든 데이터를 테이블에 저장해야 합니다. SAN의 hello 실패에 대 한 확실 하지 않으면 여러 San에서 실행 합니다. 찬 서버 랙과 hello 손실에 대 한 확실 하지 않으면 여러 랙에에서 실행 합니다. 데이터 센터의 hello 손실에 대 한 걱정 인 경우 서비스는 여러 Azure 지역 또는 데이터 센터에서 실행 해야 합니다. 

이러한 유형의 스팬된 모드에서 실행할 때는 넌 아직도 동시 오류 하지만 단일와 특정 유형의 여러 오류를 주체 toosome 유형 (예: 단일 VM 또는 네트워크 연결 실패) 자동으로 처리 됩니다 (및 "재해" 더 이상 이므로). 서비스 패브릭 클러스터 hello 및 실패 한 노드 및 서비스를 다시 상태로 핸들 확장을 위한 여러 메커니즘을 제공 합니다. 서비스 패브릭 서비스의 여러 인스턴스들을에서 실행 순서 tooavoid 이러한 종류의 계획 되지 않은 오류 회전에서 실제 재해에 수도 있습니다.

이유 오류를 통해 배포 충분히 큰 toospan 실행 작업이 불가능 이유가 있을 수 있습니다. 예를 들어 소요 하지 예정 보다 많은 하드웨어 리소스 toopay 상대 toohello 오류 발생 가능성에 대 한 합니다. 분산된 응용 프로그램을 처리할 경우 지리적으로 멀리 떨어진 거리로 인해 추가적으로 발생하는 통신 홉 또는 상태 복제 비용 때문에 허용할 수 없는 대기 시간이 초래될 수 있습니다. 이러한 상관 관계는 응용 프로그램마다 다릅니다. 소프트웨어 오류에 대 한 특히 hello 오류 수 hello 서비스 tooscale 하려는 있습니다. 이 경우 모든 hello 인스턴스에서 상관 관계가 있다는 것 hello 실패 조건이 이후 더 많은 복사본 hello 재해가 되어도 합니다.

### <a name="operational-faults"></a>작동 오류
서비스는 많은 중복성 hello 전세계 포함 되는, 경우에 여전히 것은 매우 위험 이벤트를 받을 수 있습니다. 예를 들어 누군가가 실수로 hello 서비스에 대 한 dns 이름을 hello를 다시 구성 하거나 완전 한 삭제 합니다. 한 가지 예로, 상태 저장 Service Fabric 서비스가 있으며 누군가가 해당 서비스를 실수로 삭제한 경우를 가정해 보겠습니다. 해당 서비스와 모든 방문한 hello 상태는 다른 완화 아닌 경우 이제 합니다. 이러한 유형의 작동 재해("oops")를 위해서는 일반적인 계획되지 않은 오류와는 다른 완화 방법 및 복구 단계가 필요합니다. 

가장 좋은 방법으로 tooavoid hello 이러한 유형의 operational 오류입니다.
1. operational 액세스 toohello 환경 제한
2. 위험한 작업을 엄격하게 감사
3. 자동화를 적용, 수동 또는 대역 외 변경 내용 및 해당 시행 하기 전에 hello 실제 환경에 대 한 특정 변경 내용 확인
4. 파괴적 작업이 "일시" 작업인지 확인. 일시 작업은 즉시 영향을 미치지 않으며 일정 기간 내에 실행 취소할 수 있습니다.

서비스 패브릭 몇 가지 메커니즘을 제공 하는 등 tooprevent operational 오류 제공 [역할 기반](service-fabric-cluster-security-roles.md) 액세스 클러스터 작업에 대 한 제어 합니다. 그러나 이러한 작동 오류 대부분을 해결하려면 조직의 노력 및 기타 시스템이 필요합니다. Service Fabric은 작동 오류를 감당하기 위한 일부 메커니즘을 제공합니다. 이중에서 가장 주목할 만한 것이 상태 저장 서비스에 대한 백업 및 복원입니다.

## <a name="managing-failures"></a>오류 관리
서비스 패브릭의 hello 목표는 거의 항상 자동 관리 실패입니다. 그러나에서 주문 toohandle 일부 오류 유형의 서비스는 추가 코드를가지고 있어야 합니다. 다른 유형의 오류는 안전 및 비즈니스 연속성 이유 때문에 자동으로 해결하지 _않아야_ 합니다. 

### <a name="handling-single-failures"></a>단일 오류 처리
단일 컴퓨터는 모든 종류의 이유로 인해 실패할 수 있습니다. 이중 일부는 전원 공급 장치 및 네트워킹 하드웨어 장애와 같은 하드웨어 원인입니다. 다른 오류는 소프트웨어에서 나타납니다. 여기에 hello 실제 운영 체제 및 hello 서비스 자체는 실패 합니다. 서비스 패브릭 이러한 유형의 hello 컴퓨터 toonetwork 문제 때문에 다른 컴퓨터에서 격리 수 없는 경우를 포함 하 여 오류를 자동으로 검색 합니다.

서비스의 hello 유형에 관계 없이 단일 인스턴스를 실행 결과 해당 서비스에 대 한 가동 중지 시간에 어떤 이유로 든 실패 하면 hello 코드의 단일 복사본입니다. 

순서 toohandle에서 모든 단일 오류 hello 가장 간단한 할 수 있는 점은 tooensure 기본적으로 둘 이상의 노드에서 서비스를 실행 하는입니다. 상태 비저장 서비스의 경우 `InstanceCount`를 1보다 큰 값으로 지정하여 이렇게 할 수 있습니다. 상태 저장 서비스에 대 한 hello 최소 권장은 항상 한 `TargetReplicaSetSize` 및 `MinReplicaSetSize` 3 이상. 서비스 코드의 복사본을 더 많이 실행하면 서비스가 모든 단일 오류를 자동으로 처리할 수 있습니다. 

### <a name="handling-coordinated-failures"></a>조정된 오류 처리
클러스터 tooeither 계획 된 또는 계획 되지 않은 인프라 오류가 및 변경 내용 또는 계획 된 소프트웨어 변경 내용 때문에 조정 실패할 수 있습니다. Service Fabric은 조정된 오류가 발생하는 인프라 영역을 장애 도메인으로 모델링합니다. 조정된 소프트웨어 변경이 발생하는 영역은 업그레이드 도메인으로 모델링됩니다. 장애 및 업그레이드 도메인에 대한 자세한 내용은 클러스터 토폴로지 및 정의를 설명하는 [이 문서](service-fabric-cluster-resource-manager-cluster-description.md)에 나와 있습니다.

기본적으로 Service Fabric은 서비스 실행 위치를 계획할 때 장애 및 업그레이드 도메인을 고려합니다. 기본적으로 서비스 패브릭 tooensure 계획 되거나 계획 되지 않은 변경이 발생 하는 경우 서비스에 계속 사용할 수 있도록 여러 오류 및 업그레이드 도메인 간 서비스를 실행 하는 시도 합니다. 

예를 들어 전원이 공급 실패 컴퓨터 toofail 랙과 동시에 처리가 가정해 보겠습니다. 장애 도메인 오류에서 hello 손실 많은 컴퓨터를 실행 하는 hello 서비스의 여러 복사본과 함께 지정된 된 서비스에 대 한 단일 실패의 또 다른 예도 바뀝니다. 이 때문에 중요 한 tooensuring 서비스의 고가용성은 장애 도메인을 관리 합니다. Azure에서 Service Fabric을 실행하는 경우 장애 도메인은 자동으로 관리됩니다. 다른 환경에서는 그렇지 않을 수 있습니다. 온-프레미스 사용자 고유의 클러스터를 작성 하는 경우 있는지 toomap 수 및 오류 도메인 레이아웃을 올바르게 계획 합니다.

업그레이드 도메인은 여기서 소프트웨어 동일 hello 시 toobe 업그레이드 진행 되는 영역을 모델링 하는 데 유용 시간입니다. 이 인해 업그레이드 도메인 역시 hello 경계 계획 된 업그레이드 하는 동안 소프트웨어가 다운 되는 위치를 정의 합니다. 서비스 패브릭와 서비스 모두의 업그레이드 hello에 따라 동일한 모델입니다. 롤링 업그레이드, 업그레이드 도메인 및 hello 클러스터와 서비스에 영향을 주는 변경 내용을 적용 하지 않도록 하는 hello 서비스 패브릭 상태 모델에 대 한 자세한에 대 한 이러한 문서를 참조 합니다.

 - [응용 프로그램 업그레이드](service-fabric-application-upgrade.md)
 - [응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md)
 - [Service Fabric 상태 모델](service-fabric-health-introduction.md)

제공 된 hello 클러스터 맵을 사용 하 여 클러스터의 hello 레이아웃을 시각화할 수 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md):

<center>
![노드는 Service Fabric Explorer에서 장애 도메인에 분산됩니다.][sfx-cluster-map]
</center>

> [!NOTE]
> 오류의 롤링 업그레이드, 서비스 코드 및 상태를 여러 인스턴스를 실행 하는 영역을 모델링 오류 및 업그레이드 도메인에 걸쳐 배치 규칙 tooensure 서비스 실행 되며 기본 제공 상태 모니터링만 **일부** hello의 서비스 패브릭 순서 tookeep 일반 운영 문제 및 오류가 재해에 대 한 변환에서 제공 하는 기능입니다. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>동시에 발생하는 하드웨어 또는 소프트웨어 오류 처리
위에서는 단일 오류에 대해 살펴보았습니다. 볼 수 있듯이 장애 도메인과 업그레이드 도메인에서 실행 hello 코드 (및 상태)의 더 많은 복사본을 유지 하 여 상태 비저장 및 상태 저장 서비스에 대 한 쉬운 toohandle가 됩니다. 여러 임의 오류가 동시에 발생할 수도 있습니다. 이들은 toolead tooan 실제 재해 가능성이 높습니다.


### <a name="random-failures-leading-tooservice-failures"></a>임의 오류가 선행 tooservice 실패
Hello 서비스에는 경우를 가정해는 `InstanceCount` 해당 인스턴스를 실행 하는 5 일 및 여러 노드의 모든 실패 한 hello에서 동일한 시간입니다. Service Fabric은 다른 노드에 대체 인스턴스를 자동으로 만들어 응답합니다. Hello 서비스를 다시 tooits 인스턴스 수를 원하는 때까지 교체 만드는 계속 됩니다. 또 다른 예로, 가정해 사용 하 여 상태 비저장 서비스 했습니다는 `InstanceCount`hello 클러스터의 모든 유효한 노드에서 실행 즉-1입니다. 이러한 인스턴스 중 일부 toofail 되었는지 경우를 가정해 봅니다. 이 경우 서비스 패브릭 정보 hello 서비스의 원하는 상태에 있지 않은 및는 누락 된 hello 노드에서 toocreate hello 인스턴스를 시도 합니다. 

상태 저장 서비스에 대 한 hello 상황 여부 hello 서비스에 영구적인 상태가 여부에 따라 달라 집니다. 또한 복제본 hello 서비스 수 있고 실패 한에 따라 달라 집니다. 상태 저장 서비스에 대해 재해가 발생했는지 여부를 확인하고 관리하는 작업은 다음 3단계로 진행됩니다.

1. 쿼럼 손실 여부 확인
 - 쿼럼 손실은 다 수의 상태 저장 서비스 복제본 hello hello에 다운 되 든 지 hello 주를 포함 하 여 동시 합니다.
2. Hello 쿼럼 손실 영구 인지 인지 확인
 - 대부분의 hello 시간 오류는 일시적입니다. 프로세스가 다시 시작되고, 노드가 다시 시작되고, VM이 다시 시작되고, 네트워크 파티션이 회복됩니다. 그러나 경우에 따라 오류가 영구적일 수 있습니다. 
    - 영구 상태가 아닌 서비스의 경우 쿼럼 이상의 복제본에 오류가 발생하면 _즉시_ 영구 쿼럼 손실이 발생합니다. 서비스 패브릭을 발견 하면 쿼럼 손실 상태 저장 비 영구적인 서비스에서 (가능성)를 선언 하 여 3 toostep dataloss 바로 진행 됩니다. 계속 toodataloss 서비스 패브릭은 hello 복제본 toocome 백 기다리는 의미가 없습니다 다르기 때문에 복구 된 경우에 빈 알기 때문에 의미가 있습니다.
    - 영구 상태 저장 서비스의 경우 쿼럼 이상의 복제본이 실패 하면 서비스 패브릭 toostart hello 복제본 toocome 백업 및 복원 쿼럼에 대 한 대기 합니다. 이 인해 서비스 중단에 대 한 _씁니다_ 영향을 받는 toohello hello 서비스의 파티션 (또는 "복제 세트"). 그러나 일관성은 감소하지만 읽기는 계속 진행될 수 있습니다. 서비스 패브릭 쿼럼 toobe 복원에 대 한 대기 시간을 hello 기본 공간이 계속 (잠재적) dataloss 이벤트가 고 다른 위험 수행 되므로 한정있지 않습니다. Hello 기본값 무시 `QuorumLossWaitDuration` 값 수 있지만 권장 되지 않습니다. 대신이 때 모든 활동 이루어져야 toorestore hello 복제본 다운 합니다. 그러려면, 백 다운 된 hello 노드도 전환 하 고 hello 로컬 영구 상태 저장 위치의 hello 드라이브 다시 탑재할 수 있습니다. Hello 쿼럼 손실 프로세스 오류로 인해 발생 하는 경우 서비스 패브릭 자동으로 toorecreate hello 프로세스를 시도 하 고 그 안에 hello 복제본 다시 시작 합니다. 이 작업이 실패하면 Service Fabric은 상태 오류를 보고합니다. 확인 될 수 없으면 다음 hello 복제본 일반적으로 돌아옵니다. 경우에 따라 하지만 hello 복제본 상태로 만들 수 없습니다 다시 합니다. 예를 들어 hello 드라이브 모두 실패 하거나 hello 컴퓨터는 물리적으로 인해 제거 합니다. 이러한 경우 영구 쿼럼 손실 이벤트가 발생하게 됩니다. tootell 서비스 패브릭 toostop 복제본 toocome에 다시 사용 클러스터 관리자가 다운 hello에 대 한 대기 중인 각 파티션에는 서비스는 영향을 및 hello 호출을 결정 해야 `Repair-ServiceFabricPartition -PartitionId` 또는 ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API입니다.  이 API는 hello 파티션 toomove QuorumLoss를 잠재적인 dataloss의 hello ID를 지정할 수 있습니다.

> [!NOTE]
> _되지_ 안전 toouse 이외의 특정 파티션에 대해 대상으로 지정 된 방식으로이 API입니다. 
>

3. 실제 데이터 손실이 있었는지 확인 및 백업에서 복원
  - 서비스 패브릭 hello를 호출 하는 경우 `OnDataLossAsync` 때문에 항상 메서드 _의심_ dataloss 합니다. 서비스 패브릭 하면이 호출은 toohello 배달는 _최상의_ 나머지 복제본입니다. 이 어느 복제본 hello 대부분 진행 될입니다. 항상 말 이유 hello _의심_ dataloss 가능한 hello 주가 다운 되었습니다 때와 마찬가지로 실제로 hello 나머지 데이터베이스 모두 동일한 상태에 있다는 것입니다. 그러나 해당 상태 toocompare 없이 것, 좋은 방법이 있으면 tooknow 서비스 패브릭 또는 연산자에 대 한 확실히 합니다. 이 시점에서 서비스 패브릭도 알고 hello 다른 복제본은 다시 전달 되지 않습니다. 그건 hello 결정할 때 hello 쿼럼 손실 tooresolve 자체에 대 한 대기를 중지 하는 것입니다. hello 서비스에 대 한 동작의 hello 최상의 조치는 일반적으로 toofreeze 및 특정 관리 작업을 수행에 대 한 대기 합니다. 따라서 hello 구현 하는 일반적인 용도 `OnDataLossAsync` 메서드에서 수행할?
  - 먼저 `OnDataLossAsync`가 트리거되었음을 로깅하고 필요한 모든 관리 경고를 발생합니다.
   - 일반적으로 시점에서 toopause 및 추가 의사 결정을 수행 하는 수동 작업 toobe 합니다. 즉, 백업을 사용할 수 있는 경우에 toobe 준비를 할 수 있습니다. 예를 들어 두 개의 서비스 정보를 정리 하는 경우 이러한 백업 toobe는 hello 정보 두 서비스만 중요 한 발생 하는 hello 복원 되 면 일치 하는 순서 tooensure에서 수정 해야 합니다. 
  - 종종 이기도 다른 원격 분석 또는 hello 서비스에서 배기 합니다. 이 메타데이터는 다른 서비스 또는 로그에 포함될 수 있습니다. 이 정보는 hello 백업이 나 복제 된 toothis 특정 복제본에 있던 것 호출 수신 및 처리 hello 주에 있는 경우 사용 되는 필요한 toodetermine 수 있습니다. 이러한 해야 toobe 재생 또는 추가 된 toohello 백업을 복원 하기 전에 합니다.  
   - 사용할 수 있는 모든 백업에 포함 된 복제 데이터베이스의 상태 toothat 남은 hello 비교 합니다. 에 설명 된 조건이 hello 서비스 패브릭 신뢰할 수 있는 컬렉션을 사용 하 여 도구를 작업에 사용할 수 있는 처리 [이 여기서](service-fabric-reliable-services-backup-restore.md)합니다. hello ´ ֲ toosee hello 복제본 내의 hello 상태는 부족 한 경우도 hello 백업 누락 될 수 있습니다.
  - 한 번 hello 비교 수행 하 고 hello 서비스 코드 상태 변경 작업을 수행 하는 경우 true를 반환 해야 하는 경우 필요한 hello 복원이 완료 합니다. Hello 복제본 hello 가장 사용 가능한의 복사본이 hello 상태 변경 내용이 확인할 경우 false를 반환 합니다. True는 나머지 _다른_ 복제본이 현재 이 상태와 일치하지 않을 수 있음을 나타냅니다. 이러한 상태는 삭제되며 이 복제본에서 다시 작성됩니다. False 이면 hello 하므로 상태 변경 적용 된 다른 복제 해야 하는 상태로 유지할 수 있습니다. 

서비스가 프로덕션에 배포되기 전에 서비스 작성자가 잠재적인 데이터 손실 및 오류 시나리오를 연습해보는 것이 매우 중요합니다. dataloss hello 가능성에 대해 tooprotect, 것이 중요 tooperiodically [hello 상태를 다시](service-fabric-reliable-services-backup-restore.md) 상태 저장 서비스 tooa 지역 중복 저장소 중 하나입니다. Hello 기능 toorestore 있는지 확인 해야 것입니다. 서로 다른 시간에 여러 서비스의 백업 된 이후 tooensure 복원 후 서비스는 서로 볼 수 있게 해야 합니다. 예를 들어 하나의 서비스를는 숫자를 생성 하 고 저장 한 다음 보냅니다 tooanother 서비스도 저장 하는 위치는 상황입니다. 복원 후의 백업 하지 않은 해당 작업을 포함 하기 때문에 hello 두 번째 서비스에 hello 수 있지만 hello 그렇지 않으면 처음 발견할 수 있습니다.

백업의 hello 빈도 결정 하면 최상의 가능한 복구 지점 목표 (RPO)를 찾을 경우 해당 hello 남은 아웃 복제본은 dataloss 시나리오에서에서 부족 toocontinue 및 원격 분석 배기에서 서비스 상태를 다시 만들 수 없습니다. . Service Fabric은 백업에서 복원해야 하는 영구 쿼럼 및 데이터 손실을 비롯한 다양한 오류 시나리오를 테스트하기 위한 여러 가지 도구를 제공합니다. 이러한 시나리오 hello 오류 분석 서비스에서 관리 하는 서비스 패브릭의 테스트 용이성 도구의 일부로 포함 됩니다. 이러한 도구와 패턴에 대한 자세한 내용은 [여기](service-fabric-testability-overview.md)에서 사용할 수 있습니다. 

> [!NOTE]
> 또한 시스템 서비스 특정 toohello 서비스 문제가 되 고 hello 영향으로 쿼럼 손실을 떨어질 수 있습니다. 예를 들어 hello 명명 서비스에 대 한 쿼럼 손실 영향 쿼럼 손실 hello failover manager 서비스에서 새 서비스 만들기 및 장애 조치를 차단 하는 반면 이름 확인 합니다. Hello 서비스 패브릭 시스템 서비스 hello에 대 한 상태 관리 서비스와 같은 패턴을 수행 하는 동안 좋습니다 toomove 시도할지 잠재적인 dataloss를 쿼럼 손실 합니다. hello 좋습니다 대신 너무[지원을](service-fabric-support.md) toodetermine 한 솔루션을 tooyour 특정 상황을 대상으로 합니다.  일반적으로 hello 복제본 반환 다운 될 때까지 것이 좋습니다 toosimply 대기입니다.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Hello 서비스 패브릭 클러스터의 가용성
일반적으로 자체 hello 서비스 패브릭 클러스터는 단일 실패 지점이 있는 고도로 분산 된 환경입니다. 한 노드에서 오류가 발생 하지 것입니다 가용성 또는 hello 클러스터에 대 한 안정성 문제 hello 윗부분 동일한 지침을 준수 하는 hello 서비스 패브릭 시스템 서비스 때문에 주로: 항상 넘어가는 3 개 이상의 복제 데이터베이스와 기본적으로 하는 것 시스템 서비스는 상태 비저장에 모든 노드에서 실행 됩니다. 기본 서비스 패브릭 네트워킹 hello 및 실패 감지 레이어 완벽 하 게 배포 됩니다. 대부분의 시스템 서비스는 hello 클러스터에 대 한 메타 데이터에서 다시 작성할 수 있습니다 또는 알고 어떻게 tooresynchronize 상태를 다른 곳에서 합니다. 시스템 서비스에 빠지지 쿼럼 손실 하는 경우 설명 된 위의 경우에 hello 클러스터의 가용성을 hello 손상 될 수 있습니다. 이러한 경우 특정 hello 클러스터에 대 한 작업 처럼 업그레이드를 시작 하거나 새 서비스를 배포 하지만 hello 클러스터 자체를 여전히 수 tooperform 아닐 수 있습니다. 서비스를 이미 실행 되 고 쓰기 toohello 시스템 서비스 toocontinue 작동 필요로 하지 않는 한 이러한 조건에서 실행 중인 유지 됩니다. 예를 들어 hello Failover Manager 쿼럼 손실에는 모든 서비스는 toorun, 계속 있지만 hello 장애 조치 관리자의 hello 참여 되므로 실패 하는 모든 서비스 수 tooautomatically 다시 시작 되지 않습니다. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>데이터 센터 또는 Azure 지역 오류
드문 경우 이지만 실제 데이터 센터 인해 일시적으로 사용할 수 없게 될 수 있습니다 전원 또는 네트워크 연결의 tooloss 합니다. 이 경우 해당 데이터 센터 또는 Azure 지역의 Service Fabric 클러스터 및 서비스를 사용할 수 없게 됩니다. 그러나 _사용자 데이터는 보존_됩니다. Azure에서 실행 하는 클러스터에 대 한 hello에 장애가 발생에서 업데이트를 볼 수 있습니다 [Azure 상태 페이지][azure-status-dashboard]합니다. Hello 가능성 이벤트는 물리적 데이터 센터 또는 부분적으로 파괴 있습니다 호스팅되는 서비스 패브릭 클러스터 또는 그 안에 hello 서비스 손실 될 수 있습니다. 여기에는 해당 데이터 센터 또는 지역 외부에서 백업되지 않은 상태가 모두 포함됩니다.

정상 작동 하는 대 한 두 가지 전략은 hello 단일 데이터 센터 또는 지역 영구 또는 지속적인 실패 합니다. 

1. 별도의 Service Fabric 클러스터를 이러한 여러 하위 지역에서 실행하고 이러한 환경 사이에서 장애 조치(failover) 및 장애 복구(Failback) 메커니즘을 활용합니다. 이러한 종류의 다중 클러스터 활성-활성 또는 활성-수동 모델은 추가적인 관리 및 작동 코드를 요구합니다. 그러려면, 하나의 데이터 센터 또는 지역에 hello 서비스에서 백업 조정 다른 데이터 센터 또는 지역 하나에 사용할 수 있도록 실패 합니다. 
2. 여러 데이터 센터 또는 하위 지역에 걸쳐 있는 단일 Service Fabric 클러스터를 실행합니다. hello 최소 지원 되는이 구성은 세 가지 데이터 센터 또는 지역 합니다. hello 권장 되는 영역의 수 또는 데이터 센터는 5 개입니다. 이를 위해서는 좀 더 복잡한 클러스터 토폴로지가 필요합니다. 그러나 hello이 모델의 장점은 실패 한 데이터 센터 또는 지역 있는 일반 오류도 재해에서 변환 됩니다. 단일 지역 내에서 클러스터에 대 한 작동 하는 hello 메커니즘에 의해 이러한 오류를 처리할 수 있습니다. 장애 도메인, 업그레이드 도메인 및 Service Fabric의 배치 규칙은 일반 오류를 허용할 수 있게 워크로드를 분산시킵니다. 이 유형의 클러스터에서 서비스를 작동하는 데 도움이 되는 정책에 대한 자세한 내용은 [배치 정책](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)을 참조하세요.

### <a name="random-failures-leading-toocluster-failures"></a>임의 오류가 선행 toocluster 실패
서비스 패브릭 시드 노드 hello 개념을 있습니다. 이들은 hello 기반이 되는 클러스터의 hello 가용성을 유지 하는 노드입니다. 이러한 노드 도움이 tooensure hello 클러스터 남아 다른 노드와 임대를 설정 하 고 우선 순위 특정 종류의 네트워크 오류 하는 동안 역할을 수행 합니다. 임의 오류가 hello 클러스터의 대부분의 hello 시드 노드를 제거 하는 경우 다시 상태가 되지 hello 클러스터를 자동으로 종료 합니다. 시드 노드에 자동으로 Azure에서 관리: hello 사용할 수 있는 장애 도메인과 업그레이드 도메인을 통해 배포 되 고 다른 단일 시드 노드 hello 클러스터에서 제거 되 면 그 위치에 생성 됩니다. 

독립 실행형 서비스 패브릭 클러스터와 Azure 모두에서 "주 노드 유형" hello는 hello 시드가 실행 되는 hello입니다. 주 노드 종류를 정의할 때 서비스 패브릭 자동으로 활용 합니다 hello too9 시드 노드 및 각 hello 시스템 서비스의 9 복제본을 만들어 제공 하는 노드 수입니다. 임의 오류가 집합이 다 수의 해당 시스템 서비스 복제본을 동시에 사용 하는 경우 위에서 설명한 것 처럼 hello 시스템 서비스 쿼럼 손실를 입력 합니다. 대부분의 hello 시드 노드 손실 되 면 hello 클러스터 직후 종료 됩니다.

## <a name="next-steps"></a>다음 단계
- 자세한 내용은 방법 toosimulate hello를 사용 하 여 다양 한 오류 [테스트 가능성 프레임 워크](service-fabric-testability-overview.md)
- 다른 재해 복구 및 고가용성 리소스를 참고합니다. Microsoft는 이 항목에 많은 양의 지침을 게시했습니다. Toospecific 기술을 다른 제품에서 사용 하기 위해 참조 이러한 문서 중 일부가 동안 많은 일반적인 최선의 구현 방법 hello 서비스 패브릭 컨텍스트에 적용할 수 포함:
  - [가용성 검사 목록](../best-practices-availability-checklist.md)
  - [재해 복구 훈련 수행](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Azure 응용 프로그램에 대한 재해 복구 및 고가용성][dr-ha-guide]
- [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
