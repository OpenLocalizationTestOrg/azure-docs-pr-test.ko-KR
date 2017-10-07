---
title: "서비스 패브릭 호스팅 모델 aaaAzure | Microsoft Docs"
description: "배포된 Servic Fabric 서비스 및 서비스 호스트 프로세스 복제본(또는 인스턴스) 간의 관계에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Service Fabric 호스팅 모델
이 문서에서는 서비스 패브릭에서 제공 하는 모델을 호스팅하는 응용 프로그램에 대해 간략하게 설명 하 고 hello hello 차이점에 설명 **공유 프로세스** 및 **단독 프로세스** 모델. 서비스 패브릭 노드와 hello 서비스 및 hello 서비스 호스트 프로세스의 복제본 (또는 인스턴스) 간의 관계에서 배포 된 응용 프로그램의 모양을 설명 합니다.

계속 진행하기 전에 [Service Fabric 응용 프로그램 모델][a1]을 숙지하고 다양한 개념 및 개념 간의 관계를 이해해야 합니다. 

> [!NOTE]
> 간단한 설명을 위해 이 문서에서는 명시적으로 언급되지 않은 경우 다음과 같이 가정합니다.
>
> - 단어의 모든 사용 *복제본* tooboth statless 서비스 인스턴스 또는 상태 저장 서비스의 복제를 의미 합니다.
> - *CodePackage* 취급 같습니다 너무*ServiceHost* 등록 하는 프로세스는 *ServiceType* 및 해당 서비스의 호스트 복제본 *ServiceType*.
>

toounderstand 호스팅 모델 hello, 예를 통해 직접 알려 주세요. *ApplicationType* 'MyAppType'에 있는 *ServiceType* 'MyServiceType'은 *ServicePackage* 'MyServicePackage'에 의해 제공되고, 이 서비스 패키지에 있는 *CodePackage* 'MyCodePackage'는 실행 시 *ServiceType* 'MyServiceType'을 등록한다고 가정합니다.

3 노드 클러스터가 있고, 'MyAppType' 유형의 *응용 프로그램* **fabric:/App1**을 만든다고 가정합니다. 이 *응용 프로그램* **fabric:/App1** 내에 파티션 2개(**P1** & **P2**)와 파티션당 복제본 3개가 있는 'MyServiceType' 유형의 **fabric:/App1/ServiceA** 서비스를 만듭니다. hello 다음 그림에이 응용 프로그램으로의 hello 뷰가 배포 된 노드에 있습니다.

<center>
![배포된 응용 프로그램의 노드 보기][node-view-one]
</center>

서비스 패브릭 활성화 즉, 두 hello 파티션이에서 복제본을 호스팅하는 ' MyCodePackage' 시작 ' MyServicePackage' **P1** & **P2**합니다. 참고 hello 클러스터의 노드 파티션 같은 toonumber 당 복제본 수가 선택 했으므로 hello 클러스터의 모든 hello 노드가 같은 보기를 필요 합니다. **fabric:/App1** 응용 프로그램에 파티션 1개(**P3**)와 파티션당 복제본 3개가 있는 다른 서비스 **fabric:/App1/ServiceB**를 만들어 보겠습니다. 다음 다이어그램에서는 hello hello 노드에서 새 보기를 보여 줍니다.

<center>
![배포된 응용 프로그램의 노드 보기][node-view-two]
</center>

서비스 패브릭 배치 파티션에 대 한 새로운 복제본 hello 볼 수 있듯이 **P3** 서비스의 **패브릭: / App1/ServiceB** hello 'MyServicePackage'의 기존 활성화에서 합니다. 이제 'MyAppType' 유형의 다른 *응용 프로그램* **fabric:/App2**를 만들고, **fabric:/App2** 내부에 파티션 2개(**P4** & **P5**)와 파티션당 복제본 3개가 있는 **fabric:/App2/ServiceA** 서비스를 만들어 보겠습니다. 다음 다이어그램에서는 hello 새 노드 보기를 보여 줍니다.

<center>
![배포된 응용 프로그램의 노드 보기][node-view-three]
</center>

이번에는 Service Fabric이 새로운 'MyCodePackage' 복사본을 시작하는 새로운 'MyServicePackage' 복사본을 활성화했으며, **fabric:/App2/ServiceA** 서비스의 두 파티션(**P4** & **P5**)에 있던 복제본이 이 새로운 복사본 'MyCodePackage'에 배치됩니다.

## <a name="shared-process-model"></a>공유 프로세스 모델
Tooas 참조 했으며 그 위에 hello 기본 호스팅 서비스 패브릭에서 제공 하는 모델 이며 **공유 프로세스** 모델입니다. 이 모델에에 대 한는 주어진 *응용 프로그램*하나만의 복사는 주어진 *ServicePackage* 에 활성화 되어는 *노드* (시작 되는 모든 hello *CodePackages* 에 포함 된) 복제본의 모든 서비스의 모든 hello 및는 주어진 *ServiceType* hello에 배치 됩니다 *CodePackage* 등록 하는 *ServiceType*. 복제본의 모든 서비스의 모든 hello 즉, 한 주어진 *ServiceType* 공유 hello 동일한 프로세스입니다.

## <a name="exclusive-process-model"></a>단독 프로세스 모델
hello 서비스 패브릭에서 제공 하는 다른 호스팅 모델은 **단독 프로세스** 모델입니다. 이 모델에 주어진 *노드*, 각 복제본에 거에 대 한 서비스 패브릭 활성화의 새 복사본을 *ServicePackage* (시작 되는 모든 hello *CodePackages* 에 포함 된 ) 복제본 hello에 배치 되 고 *CodePackage* 해당 등록 된 hello *ServiceType* hello 서비스 toowhich의 복제본이 속하는 합니다. 즉, 각 복제본은 해당 전용 프로세스에 상주합니다. 

이 모델은 지원되는 Service Fabric의 시작 버전 5.6입니다. **단독 프로세스** hello hello 서비스를 만들 때 모델을 선택할 수 있습니다 (사용 하 여 [PowerShell][p1], [REST] [ r1]또는 [FabricClient][c1])를 지정 하 여 **ServicePackageActivationMode** 'ExclusiveProcess'으로 합니다.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

응용 프로그램 매니페스트에 기본 서비스가 있는 경우 아래와 같이 **ServicePackageActivationMode** 특성을 지정하여 **단독 프로세스** 모델을 선택할 수 있습니다.

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
위의 예를 계속, 다른 서비스를 만들 수 있습니다 **패브릭: / App1/ServiceC** 응용 프로그램에서 **패브릭: / App1** 파티션 2 개로 (예를 들어 **P6**  &  **P7**)와 파티션당 복제본 3 개가 **ServicePackageActivationMode** too'ExclusiveProcess'를 설정 합니다. 다음 다이어그램에서는 hello 노드에서 새 보기를 보여 줍니다.

<center>
![배포된 응용 프로그램의 노드 보기][node-view-four]
</center>

보시는 것처럼 Service Fabric은 **P6** & **P7** 파티션의 각 복제본에 대해 하나씩 새로운 'MyServicePackage' 복제본 2개를 활성화하고 각 복제본을 전용 *CodePackage* 복사본에 배치했습니다. 다른 것이 toonote은 때 **단독 프로세스** 모델을 사용에 대 한는 주어진 *응용 프로그램*의 복사본을 여러 개는 주어진 *ServicePackage* 는 활성화될수있습니다 *노드*합니다. 위 예제에서는 'MyServicePackage' 복사본 3개가 **fabric:/App1**에 대해 활성화되었습니다. 'MyServicePackage'의 각 활성 복사본에는 *응용 프로그램* **fabric:/App1** 내에서 해당 복사본을 식별하는 **ServicePackageAtivationId**가 연결되어 있습니다.

위 예제의 **fabric:/App2**와 마찬가지로 **공유 프로세스** 모델만 *응용 프로그램*에 사용되는 경우 *노드*에 활성 *ServicePackage* 복사본 하나만 있고, 이 *ServicePackage* 활성화에 대한 **ServicePackageAtivationId**는 '빈 문자열'입니다.

> [!NOTE]
>- **공유 프로세스** 너무 해당 호스팅 모델**ServicePackageAtivationMode** 같은 **SharedProcess**합니다. 이것은 호스팅 모델 hello 기본값 및 **ServicePackageAtivationMode** 필요 hello hello 서비스를 만들 때 지정할 수 없습니다.
>
>- **단독 프로세스** 너무 해당 호스팅 모델**ServicePackageAtivationMode** 같은 **ExclusiveProcess** toobe hello hello를 만들 때 명시적으로 지정 해야 합니다. 서비스입니다. 
>
>- 서비스의 호스팅 모델을 쿼리하여 hello 알 수 [서비스 설명을] [ p2] 값을 살펴보고 **ServicePackageAtivationMode**합니다.
>
>

## <a name="working-with-deployed-service-package"></a>배포된 서비스 패키지 작업
노드의 활성 *ServicePackage* 복사본을 [배포된 서비스 패키지][p3]라고 합니다. 앞서 설명한 것 처럼 위에서 때 **단독 프로세스** 모델에 대 한 서비스를 만드는 데 사용 되는 주어진 *응용 프로그램*, 동일 hello에 대 한 여러 배포 된 서비스 패키지 될 수  *ServicePackage*합니다. 특정 toodeployed 서비스 패키지와 같은 작업을 수행 하는 동안 [배포 된 서비스 패키지의 상태를 보고] [ p4] 또는 [배포된서비스패키지의코드패키지를다시시작] [ p5] 등에 **ServicePackageActivationId** 요구 toobe tooidentify 특정 배포 된 서비스 패키지를 제공 합니다.

 **ServicePackageActivationId** 배포 된 서비스의 패키지 목록이 hello를 쿼리하여 얻을 수 [배포 된 서비스 패키지] [ p3] 노드에 있습니다. 쿼리할 때 [서비스 유형을 배포][p6], [복제본 배포] [ p7] 및 [배포 된 코드 패키지] [ p8] 노드에 hello 쿼리 결과 스페이스도 hello **ServicePackageActivationId** 부모 배포 된 서비스 패키지의 합니다.

> [!NOTE]
>- **공유 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나만 활성화됩니다. 있기 **ServicePackageActivationId** 너무 같은*빈 문자열* 관련 작업을 수행 하는 배포 된 서비스 패키지 하는 동안 지정할 수 있어야 합니다. 
>
> - **단독 프로세스** 호스팅 모델 아래의 지정된 *노드*에서 지정된 *응용 프로그램*에 대해 *ServicePackage* 복사본 하나 이상이 활성화될 수 있습니다. 각 활성화에는 *비어 있지 않은* **ServicePackageActivationId** toobe 관련 작업을 수행 하는 배포 된 서비스 패키지를 나타내고 필요 합니다. 
>
> - 경우 **ServicePackageActivationId** ommited too'empty 문자열 기본값은 '. 배포 된 서비스를 패키지 하는 경우 아래에서 활성화 된 **공유 프로세스** 모델이 있는 경우 다음 작업이 수행 되도록, 그렇지 않으면 hello 작업이 실패 합니다.
>
> - 한 번 tooquery 및 캐시 좋습니다 **ServicePackageActivationId** 동적으로 생성 하 고 다양 한 이유로 변경할 수 있습니다. 에 필요한 작업을 수행 하기 전에 **ServicePackageActivationId**, hello 목록을 쿼리하여 먼저 [배포 된 서비스 패키지] [ p3] 노드와 다음 사용 하 여 에 *ServicePackageActivationId** 쿼리 결과 tooperform hello 원래 작업에서 합니다.
>
>

## <a name="guest-executable-and-container-applications"></a>게스트 실행 파일 및 컨테이너 응용 프로그램
Service Fabric은 [게스트 실행 파일][a2] 및 [컨테이너][a3] 응용프로그램을 자체 포함된 상태 비저장 서비스로 처리합니다. 즉, *ServiceHost*(프로세스 또는 컨테이너)에 Service Fabric 런타임이 없습니다. 자체 포함된 이러한 서비스에는 *ServiceHost*당 복제본 수가 적용되지 않습니다. hello 이러한 서비스와 함께 사용 되는 가장 일반적인 구성을 단일 파티션와 [InstanceCount] [ c2] 너무-1 (즉, 클러스터의 각 노드에서 실행 되는 hello 서비스 코드의 한 복사). 

기본 hello **ServicePackageActivationMode** 이러한 서비스는 **SharedProcess** 서비스 패브릭의 복사본이 두 개만 활성화 되는 경우 *ServicePackage* 에 *노드* 에 대 한는 주어진 *응용 프로그램* 즉, 서비스 코드의 복사본을 하나만 실행 됩니다는 *노드*합니다. 서비스 코드 toorun의 여러 복사본을 원하는 한 *노드* 여러 서비스를 만들 때 (*Service1* 너무*서비스가*)의 *ServiceType* (에 지정 된 *ServiceManifest*)을 지정 하십시오 다중 분할 서비스가 있으면 **ServicePackageActivationMode** 으로 **ExclusiveProcess**hello hello 서비스를 만들 때.

## <a name="changing-hosting-model-of-an-existing-service"></a>기존 서비스의 호스팅 모델 변경
기존 서비스에서의 호스팅 모델을 변경 **공유 프로세스** 너무**단독 프로세스** 반대의 통해 업그레이드 또는 업데이트 메커니즘 (또는 기본 서비스 응용 프로그램에서 사양 매니페스트) 현재 지원 되지 않습니다. 이 기능에 대한 지원은 이후 버전에서 제공될 예정입니다.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>공유 프로세스 및 단독 프로세스 모델 중에서 선택
호스팅 모델은 해당 장점 및 단점 및 사용자에 게 필요한 해당 요구 사항에 가장 적합 한 tooevaluate 모두 있습니다. **공유 프로세스** 모델 적은 프로세스가 생성 됩니다 때문에 운영 체제 리소스를 더 효율적으로 사용을 통해, 여러 복제본에서 동일한 hello 포트 등 프로세스를 공유할 수 있습니다. 그러나 hello 복제본 중 하나에 도달 toobring hello 서비스 호스트를이 필요한 경우에 오류를 같은 프로세스에서 다른 모든 복제본 영향 됩니다.

 **단독 프로세스** 모델은 해당 프로세스의 모든 복제본에 대해 격리를 개선하므로 오동작하는 복제본이 다른 복제본에 영향을 주지 않습니다. 처리 하는 여기서 포트 공유에서 지원 하지 않는 hello 통신 프로토콜의 경우에 편리 합니다. 복제본 수준에서 hello 기능 tooapply 리소스 관리를 지원합니다. 반면에 hello **단독 프로세스** hello 노드의 각 복제본에 대 한 프로세스를 생성 하는 대로 많은 수의 운영 체제 리소스를 소비 합니다.

## <a name="exclusive-process-model-and-application-model-considerations"></a>단독 프로세스 모델 및 응용 프로그램 모델 고려 사항
hello 권장 방법은 toomodel 서비스 패브릭에서 응용 프로그램은 하나 tookeep *ServiceType* 당 *ServicePackage* 이 모델은 대부분의 hello 응용 프로그램에 적합 하 고 합니다. 

그러나 tooenable 특별 한 시나리오 하나 있는 *ServiceType* 당 *ServicePackage* 되지 않을 수 있습니다, 기능적으로 서비스 패브릭 허용 파일이 둘 이상 toohave *ServiceType* 당 *ServicePackage* (하나의 *CodePackage* 개 이상 등록할 수 *ServiceType*). 다음은 일부의 hello 시나리오 이러한 구성은 유용할 수 있습니다.

- Toooptimize OS 리소스 사용률을 원하는 프로세스당 높은 복제본 밀도 여 더 적은 프로세스를 생성 합니다.
- 다른 servicetype은에서 복제본 tooshare 높은 초기화 또는 메모리 비용에 몇 가지 일반 데이터를 필요 합니다.
- 무료 서비스를 제공 해야 하 고 tooput 리소스 사용률에도 동일한 프로세스에서 hello 서비스의 모든 복제본을 배치 하 여 원하는 합니다.

**단독 프로세스** 호스팅 모델은 *ServicePackage*당 여러 *ServiceTypes*가 있는 응용 프로그램 모델과 일치하지 않습니다. 즉, 여러 *servicetype은* 당 *ServicePackage* 디자인 된 tooachieve 더 높은 리소스 복제본 간에 공유 되며 프로세스당 높은 복제본 밀도 사용 하도록 설정 합니다. 이 반대 toowhat **단독 프로세스** 모델은 설계 된 tooachieve 합니다.

여러 hello 경우 *servicetype은* 당 *ServicePackage* 서로 다른 *CodePackage* 각 등록 *ServiceType*. 가령, *CodePackages* 2개가 있는 *ServicePackage* 'MultiTypeServicePackge'가 있다고 가정합니다.

- 'MyCodePackageA'는 *ServiceType* 'MyServiceTypeA'를 등록합니다.
- 'MyCodePackageB'는 *ServiceType* 'MyServiceTypeB'를 등록합니다.

이제 *응용 프로그램* **fabric:/SpecialApp**을 만들고, **단독 프로세스** 모델을 사용하여 **fabric:/SpecialApp** 내부에 다음 두 개의 서비스를 만듭니다.

- 파티션 2개(**P1** 및 **P2**)와 파티션당 복제본 3개가 있는 'MyServiceTypeA' 유형의 **fabric:/SpecialApp/ServiceA** 서비스
- 파티션 2개(**P3** 및 **P4**)와 파티션당 복제본 3개가 있는 'MyServiceTypeB' 유형의 **fabric:/SpecialApp/ServiceB** 서비스

지정 된 노드에서 두 hello 서비스 각 복제본 두 개가 됩니다. 사용 하므로 **단독 프로세스** 모델 toocreate hello 서비스, 서비스 패브릭 각 복제본에 대 한 'MyServicePackge'의 새 복사본을 활성화 합니다. 'MultiTypeServicePackge'를 활성화할 때마다 'MyCodePackageA' 및 'MyCodePackageB'의 복사본이 시작됩니다. 그러나를 'MultiTypeServicePackge' 활성화 된 hello 복제본을 호스트 'MyCodePackageA' 또는 'MyCodePackageB' 중 하나만 있습니다. 다음 다이어그램에서는 hello 노드 보기를 보여 줍니다.

<center>
![배포된 응용 프로그램의 노드 보기][node-view-five]
</center>

 볼 수 있듯이, 파티션의 복제본에 대 한 'MultiTypeServicePackge' hello 활성화에 **P1** 서비스의 **패브릭: / SpecialApp/ServiceA**, 'MyCodePackageA' hello 복제본을 호스팅 중인 및 ' MyCodePackageB' 바로 실행 되 고 있습니다. 마찬가지로, 파티션의 복제본에 대 한 'MultiTypeServicePackge'의 활성화에 **P3** 서비스의 **패브릭: / SpecialApp/ServiceB**'MyCodePackageB' hello 복제본을 호스팅하는, 및 'MyCodePackageA'가 방금 실행 되 고 기타 등등 따라서 수가 더 hello *CodePackages* (서로 다른 등록 *servicetype은*) 당 *ServicePackage*, 더 높은 됩니다 중복 리소스 사용 합니다. 
 
 서비스를 만들면 다른 손에 hello **패브릭: / SpecialApp/ServiceA** 및 **패브릭: / SpecialApp/ServiceB** 와 **공유 프로세스** 모델 서비스 패브릭 됩니다 에 대 한 'MultiTypeServicePackge' 인스턴스의 복사본이 하나만 활성화 *응용 프로그램* **패브릭: / SpecialApp** (보았듯이 이전에). 'MyCodePackageA' 서비스에 대 한 모든 복제본을 호스팅할 **패브릭: / SpecialApp/ServiceA** (또는 보다 정확 하 게 'MyServiceTypeA' toobe 유형의 모든 서비스의) 'MyCodePackageB' 서비스에 대 한 모든 복제본을 호스트 하 고 **패브릭: / SpecialApp/ServiceB** (또는 보다 정확 하 게 'MyServiceTypeB' toobe 유형의 모든 서비스의). 다음 다이어그램에서는이 설정에 hello 노드 보기를 보여 줍니다. 

<center>
![배포된 응용 프로그램의 노드 보기][node-view-six]
</center>

위 예제는 hello에서 'MyCodePackageA' 등록 'MyServiceTypeA'와 'MyServiceTypeB' 없음 'MyCodePackageB' 없을 경우 있을 더 중복으로 생각할 수 있습니다 *CodePackage* 실행 합니다. 이 가정은 맞지만, 앞에서 설명한 대로 이 응용 프로그램 모델은 **단독 프로세스** 호스팅 모델과 일치하지 않습니다. Tooput ´ ֲ 자체에서 각 복제본 둘 다를 등록 하는 프로세스 전용 전용 *servicetype은* 동일한 *CodePackage* 는 필요 하지 않으며 각 배치 *ServiceType* 에서 자체 *ServicePacakge* 더 자연 스러운 선택 됩니다.

## <a name="next-steps"></a>다음 단계
[응용 프로그램 패키지] [ a4] 준비 toodeploy 가져오기 및 합니다.

[배포 및 응용 프로그램을 제거할] [ a5] 설명 방법을 toouse PowerShell toomanage 응용 프로그램 인스턴스.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage