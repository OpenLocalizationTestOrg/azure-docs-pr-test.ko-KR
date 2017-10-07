---
title: "서비스 패브릭 서비스의 aaaScalability | Microsoft Docs"
description: "설명 방법을 tooscale 서비스 패브릭 서비스"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Service Fabric에서 크기 조정
Azure 서비스 패브릭 hello 서비스, 파티션 및 복제본에 클러스터의 노드를 hello 관리 하 여 확장 가능한 응용 프로그램을 쉽게 toobuild 있습니다. 많은 작업을 실행 동일한 하드웨어 사용 하면 최대 리소스 사용률 hello 하지만 또한 선택 하는 방법 tooscale 작업 측면에서 유연성을 제공 합니다. 

Service Fabric에서 크기를 조정하는 경우 다음과 같은 여러 가지 방법으로 수행됩니다.

1. 크기 조정: 상태 비저장 서비스 인스턴스 만들기 또는 제거
2. 크기 조정: 명명된 새 서비스 만들기 또는 제거
3. 크기 조정: 명명된 새 응용 프로그램 인스턴스 만들기 또는 제거
4. 크기 조정: 분할된 서비스 사용
5. 추가 하 고 hello 클러스터에서 노드를 제거 하 여 크기 조정 
6. 크기 조정: 클러스터 리소스 관리자 메트릭 사용

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>크기 조정: 상태 비저장 서비스 인스턴스 만들기 또는 제거
서비스 패브릭 내에서 가장 간단한 방법으로 tooscale hello 중 하나는 상태 비저장 서비스와 함께 작동합니다. 기회 toodefine 가져오기 상태 비저장 서비스를 만들 때는 `InstanceCount`합니다. `InstanceCount`hello 서비스가 시작 될 때 해당 서비스 코드의 실행 중인 복사본 수 만들어집니다 정의 합니다. 예를 들어 hello 클러스터에 100 개의 노드가 있다고 이라고 가정해 보겠습니다. `InstanceCount`가 10인 서비스를 만든다고 가정해 보겠습니다. 런타임 중 hello 코드의 10이 실행 중인 사본 모두 될 수 사용량이 또는 충분히 사용 하지 못할 수 있습니다. 한 가지 방법은 tooscale 해당 작업은 인스턴스 toochange hello 수 있습니다. 예를 들어, 모니터링 또는 관리 코드의 몇 가지 인스턴스 too50 또는 too5 hello 기존 수를 변경, hello 작업 또는 축소에 따라 hello tooscale이 필요한 여부에 따라 로드할 수 있습니다. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>동적 인스턴스 수 사용
서비스 패브릭 특별히 상태 비저장 서비스에 자동으로 방법 toochange hello 인스턴스 수를 제공합니다. 이렇게 하면 사용할 수 있는 노드의 hello 수 동적으로 hello 서비스 tooscale가 있습니다. 이 동작을 hello 방식으로 tooopt tooset hello 인스턴스 수는 =-1입니다. InstanceCount =-1은 명령 tooService 패브릭 "모든 노드에서이 상태 비저장 서비스를 실행 합니다." 라는 Hello 노드 수가 변경 되 면 서비스 패브릭 자동으로 변경 hello 인스턴스 개수 toomatch hello 서비스 유효한 모든 노드에서 실행 되 고 있는지 확인 합니다. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>크기 조정: 명명된 새 서비스 만들기 또는 제거
지정 된 서비스 인스턴스가 서비스 유형의 특정 인스턴스가 (참조 [서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)) hello 클러스터의 일부 응용 프로그램 명명 된 인스턴스 내에서. 

서비스가 더 많거나 적게 사용됨에 따라 명명된 새 서비스 인스턴스가 만들어지거나 제거될 수 있습니다. 따라서 요청 toobe를 일반적으로 기존 서비스 toodecrease의 부하를 허용 하는 더 많은 서비스 인스턴스를 분산할 수 있습니다. 서비스를 만들 때 서비스 패브릭 클러스터 리소스 관리자 hello hello 서비스를 분산 방식에서 hello 클러스터에 배치 합니다. hello 정확한 결정 hello에 따라 관리 됩니다 [메트릭](service-fabric-cluster-resource-manager-metrics.md) hello 클러스터 및 기타 배치 규칙의 합니다. 서비스를 여러 가지 방법으로 만들 수 있지만 hello 가장 일반적으로는 호출 하는 등의 관리 작업을 통해 [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), 또는 코드를 호출 하 여 [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet)합니다. `CreateServiceAsync`도 호출할 수 있습니다에서 hello 클러스터에서 실행 되는 다른 서비스 내에서.

서비스를 동적으로 만들면 모든 종류의 시나리오에서 사용할 수 있으며 일반적인 패턴입니다. 예를 들어 특정 워크플로를 나타내는 상태 저장 서비스를 고려합니다. 호출 작업을 나타내는 toothis 서비스를 tooshow 숨겨지며이 서비스는 진행 중인 tooexecute hello 단계 toothat 워크플로 및 레코드 진행 합니다. 

이 특정 서비스 규모를 어떻게 수행한 것? hello 서비스 될 수 있습니다 어떤 형태로 다중 테 넌 트 및 호출 수락 고 같은 다양 한 인스턴스의 hello에 대 한 단계를 시작 워크플로 한 번에 모두 있습니다. 그러나를 만들 수는 hello 코드 이후 더 복잡 한 tooworry 다양 한 인스턴스의 hello에 대 한 현재 다양 한 고객에서 및 다양 한 단계에서 모두 동일한 워크플로의 합니다. 또한 눈금 문제 hello hello 해결 되지 않으면 동시에 여러 워크플로 처리 합니다. 즉, 특정 시점에이 서비스는 특정 컴퓨터에서 너무 많은 리소스 toofit 사용 합니다. 또한 hello 첫 번째 위치에서이 패턴에 대 한 기본 제공 되지 않는 많은 서비스 코드 toosome 내재 된 병목 현상 또는 저하 인해 어려움을 겪을 합니다. 이러한 유형의 문제를 추적 하는 동시 워크플로 hello 수를 더 큰 가져오면 hello 서비스 하지 toowork도를 일으킬 있습니다.  

솔루션은 toocreate 인스턴스 tootrack hello 워크플로의 모든 다른 인스턴스에 대해이 서비스의 원하는 합니다. 유용한 패턴 이므로 hello 서비스는 상태 저장 또는 상태 비저장 든 작동 합니다. 이 패턴 toowork에는 일반적으로 다른 서비스 "작업 관리자 서비스" 역할입니다. 이 서비스의 작업을 hello tooreceive 요청과 tooroute 이러한 요청 tooother 서비스입니다. hello 관리자 hello 메시지를 받을 때 hello 작업 서비스의 인스턴스를 동적으로 만들 수 있습니다 및 요청 toothose 서비스에 전달 합니다. 또한 hello 관리자 서비스는 지정 된 워크플로 서비스 작업 완료 되 면 콜백을 받을 수 있습니다. Hello 관리자가 이러한 콜백을 받는 경우 hello 워크플로 서비스의 해당 인스턴스를 삭제 또는 이상의 호출을 예상 되는 경우 사용자에 게 그대로 수 없습니다. 

이러한 유형의 관리자의 고급 버전 관리 하는 hello 서비스의 풀 만들 수 있습니다. hello 풀은 새 요청이 들어올 때 없다는 toowait 서비스 toospin hello에 대 한 확인 하는 데 도움이 됩니다. 대신, hello 관리자 수 방금 hello 풀에서 현재 사용 중 없는 워크플로 서비스를 선택 하거나 임의로 라우팅할 합니다. 사용할 수 있는 서비스 풀을 유지 하면 새 요청을 처리 보다 빠르게 이기는 hello 요청에 생성 되는 새 서비스 toobe에 대 한 toowait 될 가능성이 적기 때문 있습니다. 새 서비스를 만드는 것은 빠르지만 자유롭거나 즉각적이지는 않습니다. hello 풀은 hello hello 요청 서비스를 제공 하기 전에 toowait에 시간을 최소화 하는 데 도움이 됩니다. 응답 시간이 가장 중요 한 문제 hello 때 종종이 관리자 및 풀 패턴을 볼 수 있습니다. 큐 hello 요청 및 hello 백그라운드에서 만드는 hello 서비스 및 _다음_ 에 전달할 이기도 인기 있는 관리자 패턴을 만들고 일부 추적 hello 작업량의 해당 서비스가 현재 기반 서비스를 삭제 하는 대로 보류 중인 합니다. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>크기 조정: 명명된 새 응용 프로그램 인스턴스 만들기 또는 제거
만들기 및 전체 응용 프로그램 인스턴스 삭제는 비슷한 toohello 패턴을 만들고 서비스를 삭제입니다. 이 패턴에 대 한 hello 요청은 표시 된 것에 따라 hello 의사 결정을 수행 하는 몇 가지 관리자 서비스 않으며에서 발생 하는 hello 정보 hello hello 클러스터 내의 다른 서비스입니다. 

어떤 기존 응용 프로그램에서 명명된 새 서비스 인스턴스를 만드는 대신 명명된 새 응용 프로그램 인스턴스를 만들어야 하나요? 여기에는 다음 몇 가지 경우가 있습니다.

  * hello 새 응용 프로그램 인스턴스가 해당 코드 toorun 일부 특정 id 또는 보안 설정에 필요한 고객에 대 한 합니다.
    * 서비스 패브릭 서로 다른 코드 패키지 toorun 특정 id를 정의할 수 있습니다. 순서 toolaunch hello hello 정품 인증 하는 서로 다른 id로 동일한 코드 패키지 해야 toooccur 서로 다른 응용 프로그램의 경우. 기존 고객의 워크로드가 배포되는 경우를 고려합니다. 이러한 모니터링 하 고 원격 데이터베이스 또는 다른 시스템 등 액세스 tooother 리소스가 제어할 수 있도록 특정 id를 서비스가 실행 될 수 있습니다. 이 경우 새 고객 등록 하는 경우 원하지 않을 것 tooactivate hello의 코드 동일한 컨텍스트 (프로세스 공간)입니다. 할 수 하는 동안 것이 어려워집니다 특정 id의 hello 컨텍스트 내에서 서비스 코드 tooact 프로그램에 대 한 합니다. 일반적으로 더 많은 보안, 격리 및 ID 관리 코드가 있어야 합니다. 사용 하는 대신 다른 서비스의 명명 된 인스턴스 내 같은 응용 프로그램 인스턴스에 hello 및 동일한 프로세스 공간 따라서 hello, 서로 다른 명명 된 서비스 패브릭 응용 프로그램 인스턴스를 사용할 수 있습니다. 이렇게 하면 보다 쉽게 toodefine 서로 다른 id 컨텍스트.
  * 새 응용 프로그램 인스턴스 hello 구성 하는 방법으로도 사용
    * 기본적으로 모든 응용 프로그램 인스턴스 내에서 특정 서비스 유형의 서비스 인스턴스를 명명 된 hello hello 지정 된 노드에서 동일한 프로세스에서 실행 됩니다. 즉 각 서비스 인스턴스마다 다르게 구성할 수 있지만 이 방법은 복잡합니다. 서비스는 toolook 구성 패키지 내에서 해당 구성을 사용 하는 몇 가지 토큰이 있어야 합니다. 일반적으로 바로 hello 서비스의 이름입니다. 이 정상적으로 작동 하지만 해당 응용 프로그램 인스턴스 내 hello 개별 명명 된 서비스 인스턴스의 hello 구성 toohello 이름을 결합 합니다. 이 혼동 될 수 있으며 구성 이후 하드 toomanage는 일반적으로 응용 프로그램 인스턴스 특정 값으로 디자인 타임 아티팩트입니다. 더 많은 서비스를 항상 만들기 의미 더 많은 응용 프로그램 업그레이드 hello 구성 패키지 또는 toodeploy 새로 내 toochange hello 정보 hello 새 서비스의 특정 정보를 볼 수 있도록 합니다. 것이 더 쉽게 toocreate 완전히 새로운 응용 프로그램 명명 된 인스턴스입니다. 그런 다음 모든 구성은 hello 서비스에 대 한 필요 hello 응용 프로그램 매개 변수 tooset 사용할 수 있습니다. 이러한 방식으로 hello 서비스 내에 만들어진 모든 응용 프로그램 인스턴스는 명명 된 특정 구성 설정을 상속할 수 있습니다. 예를 들어 hello 설정 및 암호와 같은 또는 고객 리소스 제한 당 모든 고객에 대 한 사용자 지정 된 단일 구성 파일 대신 대신 해야 다른 응용 프로그램 인스턴스를 이러한 설정 사용 하 여 각 고객에 대 한 재정의 합니다. 
  * 업그레이드 한계로 hello 새 응용 프로그램 역
    * Service Fabric 내에서 명명된 다른 응용 프로그램 인스턴스는 업그레이드를 위한 경계 역할을 합니다. 단일 명명 된 응용 프로그램 인스턴스를 업그레이드 하는 다른 명명 된 응용 프로그램 인스턴스가 실행 되는 hello 코드를 영향을 주지 않습니다. hello 서로 다른 응용 프로그램은 실행 될 서로 다른 버전의 코드 hello의 hello에 같은 노드. 또는 not으로 다른 서비스를 업그레이드 동일 hello 새 코드 hello 따라야 하는지 여부를 선택할 수 있으므로 toomake 크기 조정 의사 결정을 할 때이 비율을 수 있습니다. 예를 들어, 특정 고객의 작업을 만들고 서비스를 동적으로 삭제 하 여 크기 조정 작업을 담당 하는 hello 관리자 서비스 도착 호출 합니다. 그러나이 경우 hello 호출은 연결 된 작업에는 _새_ 고객 합니다. 대부분의 고객 뿐 아니라 이유로 hello 보안 및 구성 이전에 표시 된를 서로 격리 된 비슷하지만 특정 버전의 hello 소프트웨어 선택 및 실행 측면에서 더 많은 유연성을 제공 하기 때문에 이러한 가져오기 업그레이드할 때. 또한 새 응용 프로그램 인스턴스를 만들고 및 hello 서비스를 만들 수 있습니다 있습니다 toofurther 파티션 단순히 hello 업그레이드를 한 번 닿는 서비스입니다. 별도의 응용 프로그램 인스턴스에서 응용 프로그램 업그레이드를 수행할 때 더 자세한 세분성을 제공하며, A/B 테스트 및 파랑/녹색 배포도 가능하게 합니다. 
  * 기존 응용 프로그램 인스턴스가 hello 꽉
    * 서비스 패브릭에서 [응용 프로그램 용량](service-fabric-cluster-resource-manager-application-groups.md) 는 특정 응용 프로그램 인스턴스에 대해 toocontrol hello 양을 사용 가능한 리소스를 사용할 수 있는 개념입니다. 예를 들어, 주어진된 서비스가 필요한 순서 tooscale에서 만든 다른 인스턴스 toohave 있는지 결정할 수 있습니다. 그러나 이 응용 프로그램 인스턴스에는 특정 메트릭에 대한 용량이 부족합니다. 이 특정 고객 또는 워크 로드 해야 계속 부여할 수 있으면 더 많은 리소스, 있습니다 수 hello 해당 응용 프로그램에 대 한 기존 용량을 늘릴 하거나 새 응용 프로그램을 만듭니다. 

## <a name="scaling-at-hello-partition-level"></a>Hello 파티션 수준에서 크기 조정
Service Fabric은 파티션을 지원합니다. 분할은 서비스를 여러 논리적 및 물리적 섹션으로 나누며, 각 섹션은 독립적으로 작동합니다. 이 상태 저장 서비스에 유용을 아무도 복제본의 설정 때문에 toohandle hello에 대 한 모든 호출에 한 번에 모든 hello 상태를 조작 합니다. hello [개요 분할](service-fabric-concepts-partitioning.md) hello 유형의 지원 되는 파티션 구성표에 대해 설명 합니다. 각 파티션의 hello 복제본 클러스터에서 해당 서비스의 부하를 분산 하 고, 두 hello 서비스 전체 또는 파티션의 단일 실패 지점이 있음을 보장 hello 노드에 분산 됩니다. 

서비스가 0개의 하위 키, 99개의 상위 키 및 4개의 파티션 개수를 가진 범위 지정 파티션 구성표를 사용한다고 가정합니다. 3 노드 클러스터에서 hello 서비스 다음과 같이 각 노드에서 hello 리소스를 공유 하는 4 개의 복제본으로 배치할지 수 있습니다.:

<center>
![3개의 노드가 있는 파티션 레이아웃](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Hello 노드 수를 늘리면 서비스 패브릭 옮겨집니다 hello 기존 복제본의 일부 있습니다. 예를 들어 hello 노드 수가 증가 toofour 빌드하고 hello 복제본 가져오기 가정해 봅니다. Toodifferent 파티션에 속하는 각 이제 hello 서비스는 각 노드에서 실행 하는 3 개의 복제본, 이제 합니다. 이렇게 하면 hello 새 노드가 콜드 되지 않으면 이후 보다 우수한 리소스 사용률과가 있습니다. 일반적으로 성능이 향상 됩니다 각 서비스에 더 많은 리소스가 사용 가능한 tooit 합니다.

<center>
![4개의 노드가 있는 파티션 레이아웃](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>서비스 패브릭 클러스터 리소스 관리자 hello 및 메트릭을 사용 하 여 크기 조정
[메트릭](service-fabric-cluster-resource-manager-metrics.md) 서비스 패브릭의 리소스 소비 tooService를 표현 하는 방법이 됩니다. 메트릭을 사용 하 여 기회 tooreorganize hello 클러스터 리소스 관리자를 제공 하 고 hello 클러스터의 hello 레이아웃을 최적화 합니다. 예를 들어 hello 클러스터에 리소스를 많이 있을 수 있지만 있습니다 수를 할당할 수 toohello 서비스를 현재 작업을 수행 합니다. 메트릭을 사용 하면 클러스터 리소스 관리자 tooreorganize hello 액세스할 수 있는 서비스는 hello 클러스터 tooensure toohello 사용 가능한 리소스입니다. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>추가 하 고 hello 클러스터에서 노드를 제거 하 여 크기 조정 
서비스 패브릭 크기 조정에 대 한 또 다른 옵션에는 hello 클러스터의 toochange hello 크기입니다. 노드 추가 또는 제거 하나 이상의 hello 노드 형식에 대 한 hello 클러스터의 의미 hello hello 클러스터 크기를 변경 합니다. 예를 들어 들어 hello 클러스터에서 hello 노드의 모든는 핫 하는 경우. 즉, hello 클러스터의 리소스를 거의 모두 사용 됩니다. 클러스터에 가장 좋은 방법은 tooscale hello는이 경우 더 많은 노드 toohello 추가 합니다. Hello 새 노드 가입 hello 클러스터 hello 서비스 패브릭 클러스터 리소스 관리자 이동 서비스 toothem hello 기존 노드에 대 한 전체 부하를 생성 합니다. 인스턴스 수가 -1인 상태 비저장 서비스의 경우 더 많은 서비스 인스턴스가 자동으로 만들어집니다. 따라서 일부 호출 toomove를 hello 기존 노드 toohello 새 노드를 수 있습니다. 

추가 및 제거 노드 toohello 클러스터 hello 서비스 패브릭 Azure 리소스 관리자 PowerShell 모듈을 통해 수행할 수 있습니다.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>모든 항목 요약
여기에 설명 된 하 고 예를 통해 통신 하는 모든 hello 아이디어 보겠습니다. 서비스는 hello 고려: 고치려는 toobuild 주소록을 역할을 하는 서비스 toonames 및 연락처 정보를 보유 합니다. 

다양 한 질문 관련된 tooscale 있는 들겠지만 오른쪽: 사용자 수는 진행 중인 toohave? 각 사용자가 연락처를 얼마나 많이 저장하나요? 시도 toofigure이 모두 때 하면 대기 중입니다. hello에 대 한 서비스를 처음으로 어렵습니다. 특정 파티션 수와 단일 정적 서비스 toogo 휴가가 경우를 가정해 봅니다. hello 파티션 수 문제가 발생할 수 있습니다 toohave 배율 나중에 잘못 된 선택의 hello 결과가 발생 합니다. 마찬가지로, 모든 hello 정보 hello 오른쪽 수 없을 수도 있습니다를 선택 하는 경우에 필요. 예를 들어 갖게 hello 클러스터 들겠지만, toodecide hello 크기 hello 노드 수 및 크기 측면에서 모두 됩니다. 일반적으로 하드 toopredict 서비스 리소스의 수는 수명 주기 동안 tooconsume 것입니다. 실제로 hello 서비스에 게 표시 되는 시간 hello 트래픽 패턴 보다 먼저 하드 tooknow 수도 있습니다. 예를 들어 maybe 사람에서에서 추가 및 제거의 연락처 것만 hello 아침 또는 미정 배포 균등 하 게 hello 하루의 hello 과정입니다. 바탕 tooscale에 및를 동적으로 할 수 있습니다. 이전에, 및 tooneed tooscale 거 하지만 어느 쪽 야 tooneed tooreact toochanging 리소스 사용 서비스에 의해 toopredict을 배울 수 있습니다. 이 될 수 있습니다 순서 tooprovide hello 클러스터의 hello 크기 변경 더 많은 리소스가 충분 하지 않을 기존 리소스의 사용을 다시 구성 하는 경우. 

하지만 이유 toopick 모든 사용자에 대해 아웃 단일 파티션 구성표도 시도? 만 tooone 서비스와 하나의 정적 클러스터? 실제 상황 hello 일반적으로 보다 동적입니다. 

눈금을 개발할 때는 hello를 동적 패턴을 따르는 것이 좋습니다. Tooadapt 해야 것 tooyour 상황.

1. 들겠지만 모두를 위한 toopick 파티션 구성표를 시도 하는 대신 빌드 "관리자 서비스"입니다.
2. hello 작업이 hello 관리자 서비스의 서비스에 등록할 때 toolook 고객 정보를입니다. 그런 다음 해당 정보에 따라 hello 관리자 서비스의 인스턴스를 만듭니다 프로그램 _실제_ 연락처 저장소 서비스 _해당 고객에 대 한_합니다. 특정 구성, 격리, 또는 업그레이드를 필요로 할 경우이 고객에 대 한 toospin 응용 프로그램 인스턴스를 결정할 수도 있습니다. 

이 동적 만들기 패턴은 다음과 같은 많은 이점을 제공합니다.

  - 모든 사용자에 게 들겠지만 tooguess hello 올바른 파티션 수를 시도 하는 또는 빌드 무한히 단독으로 확장 가능한 단일 서비스입니다. 
  - 다른 사용자가 동일한 파티션 수, 복제본 수, 배치 제약 조건, 메트릭, 기본 로드, 서비스 이름, dns 설정 또는 hello hello 서비스에서 지정한 다른 속성과 toohave hello 없는 또는 응용 프로그램 수준입니다. 
  - 추가 데이터 조각화를 구성할 수 있습니다. 각 고객에 게 hello 서비스의 자체 복사본
    - 각 고객 서비스마다 예상되는 규모에 따라 필요한 만큼 더 많거나 적은 파티션 또는 복제본으로 다르게 구성되어 더 많거나 적은 리소스가 허용될 수 있습니다.
      - 예를 들어 "Gold" 계층 hello에 대 한 지불 hello 고객-복제본 수를 늘리거나 큰 파티션 수를 가져올 수 있습니다 및 잠재적으로 리소스 용량 메트릭 및 응용 프로그램을 통해 tootheir 서비스입니다.
      - 또는 이러한 제공 hello 연락처 필요할 수 있음을 나타내는 정보는 "작음" 되었습니다-몇 가지 파티션만 대기줄 또는 다른 고객을 사용 하 여 공유 서비스 풀에도 배치 될 수 있습니다.
  - 고객 tooshow를 기다리는 동안 다양 한 서비스 인스턴스 또는 복제본을 실행 하지 하는
  - 고객 떠나고 하는 경우 해당 서비스 또는 응용 프로그램 카탈로그 생성을 삭제 하는 hello 관리자 것 만큼 간단는 다음 서비스에서 해당 정보를 제거 합니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 개념에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [서비스 패브릭 서비스의 가용성](service-fabric-availability-services.md)
* [서비스 패브릭 서비스 분할](service-fabric-concepts-partitioning.md)
