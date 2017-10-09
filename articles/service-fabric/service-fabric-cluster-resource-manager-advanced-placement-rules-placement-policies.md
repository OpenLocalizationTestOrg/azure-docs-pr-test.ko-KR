---
title: "aaaService 패브릭 클러스터 리소스 관리자-배치 정책을 | Microsoft Docs"
description: "서비스 패브릭 서비스에 대한 추가 배치 정책 및 규칙 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>서비스 패브릭 서비스에 대한 배치 정책
배치 정책은 몇 가지 특정, 보다 덜 일반적인 시나리오에 사용 되는 toogovern 서비스 배치 될 수 있는 추가 규칙입니다. 이러한 시나리오의 몇 가지 예는 다음과 같습니다.

- 온-프레미스 데이터 센터 또는 Azure 지역 간에 Service Fabric 클러스터의 지리적 거리가 확대되는 경우
- 지역 또는 법적 컨트롤의 여러 영역이 나 정책 경계가 있는 다른 경우 사용자 환경에 걸쳐 tooenforce 필요
- 기한 toolarge 거리 또는 느린 있거나 덜 안정적인 네트워크 링크의 사용 하 여 통신 성능 또는 대기 시간 고려 사항 사항이
- 다른 워크 로드 또는 근접 toocustomers에서 최상의 노력으로 워크 로드 배치 특정 tookeep 필요

대부분의 이러한 요구 사항이 hello hello hello 클러스터의 장애 도메인으로 표현 되는 hello 클러스터의 실제 레이아웃을 맞춥니다. 

이러한 시나리오는 주소는 데 도움이 되는 배치 정책을 고급 hello:

1. 잘못된 도메인
2. 필수 도메인
3. 기본 설정 도메인
4. 복제본 압축 불가

대부분 hello 다음 컨트롤의 노드 속성 및 배치 제약 조건을 통해 구성할 수 수 있지만 일부는 더 복잡 한. toomake 사항을 간단 hello 서비스 패브릭 클러스터 리소스 관리자는 이러한 추가 배치 정책을 제공합니다. 배치 정책은 명명된 서비스 인스턴스를 기준으로 구성됩니다. 동적으로 업데이트할 수도 있습니다.

## <a name="specifying-invalid-domains"></a>잘못된 도메인 지정
hello **InvalidDomain** 배치 정책을 사용 하면 toospecify 특정 장애 도메인은 특정 서비스에 대해 유효 하지 않습니다. 이 정책을 사용하면 예를 들어 지정학적 또는 회사 정책상의 이유로 특정 영역에서 특정 서비스가 실행되지 않도록 할 수 있습니다. 별도 정책을 통해 잘못된 여러 도메인을 지정할 수 있습니다.

<center>
![잘못된 도메인 예제][Image1]
</center>

코드:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>필수 도메인 지정
hello는 도메인 배치 정책에 따라 hello 서비스는 hello 지정한 도메인에만 필요 합니다. 별도 정책을 통해 여러 필수 도메인을 지정할 수 있습니다.

<center>
![필수 도메인 예제][Image2]
</center>

코드:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>상태 저장 서비스의 hello 주 복제본에 대 한 기본 도메인을 지정
hello 주 도메인 기본 설정 지정 hello 오류 도메인 tooplace Primary in hello 합니다. 정상 상태인 모든 항목 hello 주가이 도메인에서 종료 됩니다. Hello 기본 이동 hello에 이상적으로 다른 위치 toosome hello 도메인 또는 hello 주 복제본에 실패 하거나 종료 되 면 동일한 도메인입니다. 이 새 위치에에서 없는 경우 hello 선호 도메인, hello toohello 선호 도메인을 가능한 한 빨리 다시 클러스터 리소스 관리자 이동 합니다. 이 정책은 Azure 지역 또는 여러 데이터 센터 간에 걸쳐 있는 클러스터에서 가장 유용합니다. 이 정책은 Azure 지역 또는 여러 데이터 센터에 걸쳐 있으나 특정 위치에 배치되는 것을 선호하는 서비스를 포함하는 클러스터에서 가장 유용합니다. 유지 보관 tootheir 사용자 또는 다른 서비스를 사용 하면 기본적으로 기본으로 취급 되는 읽기에 대 한 특히 더 낮은 대기 시간을 제공할 닫습니다.

<center>
![기본 설정 주 도메인 및 장애 조치(Failover)][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>복제본 배포 요구 및 압축 허용 안 함
복제본은 _정상적으로_ hello 클러스터 상태가 정상이 때 오류 및 업그레이드 도메인에 분산 합니다. 그러나 특정 파티션에 대해 둘 이상의 복제본이 단일 도메인으로 압축될 수 있는 경우가 있습니다. 예를 들어 가정해 해당 hello 클러스터에 세 개의 오류 도메인, fd에 9 개의 노드가: / 0, fd: / 1, 및 fd: / 2입니다. 서비스에 3개의 복제본이 있다고 가정하겠습니다. 해당 hello 경우를 가정해 fd에 해당 복제본에 대 한 사용 되는 노드: / 1 및 fd: / 2이 다운 되었습니다. 일반적으로 hello 클러스터 리소스 관리자는 이러한 동일한 오류 도메인에 있는 다른 노드를 선호 합니다. 이 경우를 가정해 toocapacity 문제 인해 없음 해당 도메인의 다른 노드에의 hello 잘못 되었습니다. Hello 클러스터 리소스 관리자는 해당 복제본에 대 한 대체를 작성 하는 경우 동일 하 게 toochoose 노드의 fd: / 0입니다. 그러나 수행 _하_ hello 장애 도메인 제약 조건 위반 되는 상황을 만듭니다. 전체 복제 세트 hello hello 확률이 복제본 증가 압축 이동 하거나 손실 될 수 없습니다. 

> [!NOTE]
> 제약 조건 및 제약 조건 우선 순위에 대한 자세한 내용은 [이 항목](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities)을 확인하세요.
>

`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`와 같은 상태 메시지가 표시된 경우 이 조건 또는 비슷한 조건에 도달한 것입니다. 일반적으로 한 개나 두 개의 복제본만 일시적으로 함께 압축됩니다. 지정된 도메인에 쿼럼 미만의 복제본이 있는 경우 안전합니다. 압축은 드물게 발생 하지만 발생할 수 있습니다 및 일반적으로 이러한 경우 되므로 일시적인 hello 노드에 다시 시도 합니다. Hello 노드 누워 수행 하며 hello 클러스터 리소스 관리자 toobuild 교체, 일반적으로 많은 경우 다른 노드에 사용할 수 있는 hello 이상적인 오류 도메인에 합니다.

일부 작업은 더 적은 도메인으로 압축 되는 경우에 항상 복제본의 hello 대상 번호를 가진 선호 합니다. 이러한 워크로드는 동시에 발생하는 영구적인 도메인 오류 전체에 대해 안정적이며 일반적으로 로컬 상태를 복구할 수 있습니다. 다른 워크 로드 보다 수행 되는 hello 가동 중지 시간 데이터 손실 위험 정확성 보다 이전입니다. 대부분의 프로덕션 워크로드가 세 개 이상의 복제본, 세 개 이상의 장애 도메인 및 장애 도메인당 여러 개의 유효한 노드에서 실행됩니다. 이 인해 hello 기본 동작은 기본적으로 도메인 압축을 수 있습니다. hello 기본 동작에서는 일반 분산 및 장애 조치 toohandle 극단적인 경우 이러한 경우에 임시 도메인 압축을 의미 합니다.

특정된 작업에 대해 이러한 압축 toodisable 원하는 hello를 지정할 수 있습니다 `RequireDomainDistribution` hello 서비스에는 정책입니다. 이 정책이 설정 된 경우 hello 클러스터 리소스 관리자는 동일한 파티션에 hello 오류 같거나 업그레이드 도메인에서에서 실행 하는 hello에서 두 복제본을 확인 합니다.

코드:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

이제 것은 이러한 구성 된 지리적으로 포함 되는 클러스터에서 서비스에 대 한 가능한 toouse 수 있습니까? 가능하지만 그럴 필요는 없습니다. hello 필수, 유효 하지 않은 및 기본 도메인 필요한 hello 시나리오에만 구성 하면 안 됩니다. 분명히 모든 의미 tootry tooforce 주어진된 작업 toorun 단일 랙에 또는 tooprefer 다른 로컬 클러스터의 일부 세그먼트입니다. 여러 하드웨어 구성을 장애 도메인 간에 분산하고 일반 배치 제약 조건 및 노드 속성을 통해 처리해야 합니다.

## <a name="next-steps"></a>다음 단계
- 서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
