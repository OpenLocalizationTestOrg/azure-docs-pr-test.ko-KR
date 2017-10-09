---
title: "aaaService 패브릭 클러스터 리소스 관리자-응용 프로그램 그룹 | Microsoft Docs"
description: "Hello hello 서비스 패브릭 클러스터 리소스 관리자에서에서 응용 프로그램 그룹 기능 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>소개 tooApplication 그룹
서비스 패브릭 클러스터 리소스 관리자 hello 부하를 분산 함으로써 클러스터 리소스는 일반적으로 관리 (을 통해 나타낼 [메트릭](service-fabric-cluster-resource-manager-metrics.md)) hello 클러스터 전체에서 균등 하 게 합니다. 서비스 패브릭 관리를 통해 전체 hello 클러스터와 hello 클러스터의 hello 노드 hello 용량 [용량](service-fabric-cluster-resource-manager-cluster-description.md)합니다. 메트릭과 용량은 다양한 워크로드에 잘 적용되지만 서로 다른 Service Fabric 응용 프로그램 인스턴스를 과도하게 사용하는 패턴은 때때로 추가 요구 사항을 가져옵니다. 예를 들어 다음을 원할 수 있습니다.

- 예약 일부 응용 프로그램 명명 된 인스턴스 내에서 hello 서비스에 대 한 hello 클러스터의 hello 노드에서 일부 용량
- Hello 총 (hello 전체 클러스터를 통해 확산) 대신 명명 된 응용 프로그램 인스턴스 내에서 hello 서비스가 실행 되는 노드 수를 제한 합니다.
- 정의 용량 hello 명명 된 응용 프로그램 인스턴스 자체에 toolimit hello 수가 내부 hello 서비스의 서비스 또는 전체 리소스 소비량

toomeet 이러한 요구 사항을 hello 서비스 패브릭 클러스터 리소스 관리자는 응용 프로그램 그룹 이라는 기능을 지원 합니다.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Hello 최대 노드 수를 제한합니다.
응용 프로그램 용량에 대 한 가장 간단한 사용 사례 hello 때 응용 프로그램 인스턴스에 필요한 toobe tooa 특정 최대 노드 수를 제한 합니다. 이를 통해 해당 응용 프로그램 인스턴스 내의 모든 서비스가 설정된 수의 컴퓨터에 통합됩니다. 통합은 toopredict 하려는 또는 hello 서비스 해당 응용 프로그램 명명 된 인스턴스 내에서 물리적 리소스 사용을 방지 하는 경우에 유용 합니다. 

hello 다음 이미지 표시와 정의 노드의 최대 수 없는 응용 프로그램 인스턴스:

<center>
![최대 노드 수를 정의하는 응용 프로그램 인스턴스][Image1]
</center>

Hello 왼쪽 예에서 hello 응용 프로그램 정의 노드의 최대 수 없는 경우 인데 % 세 가지 서비스. hello 클러스터 리소스 관리자가 분산 되어 모든 복제본 6 개의 사용 가능한 노드 tooachieve hello 적절 한 hello 클러스터 (hello 기본 동작). Hello hello 오른쪽 예제에 표시 제한 된 toothree 노드가 동일한 응용 프로그램입니다.

이 동작을 제어 하는 hello 매개 변수 MaximumNodes 라고 합니다. 이 매개 변수는 응용 프로그램을 만드는 동안 설정되거나 이미 실행 중인 응용 프로그램 인스턴스에 대해 업데이트될 수 있습니다.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

노드의 hello 집합 내에서 서비스 개체를 함께 배치 하거나 노드를 사용 하는 클러스터 리소스 관리자 hello 보장 하지 않습니다.

## <a name="application-metrics-load-and-capacity"></a>응용 프로그램 메트릭, 부하 및 용량
응용 프로그램 그룹을 특정된 명명 된 응용 프로그램 인스턴스 및 이러한 메트릭에 대 한 해당 응용 프로그램 인스턴스의 용량와 관련 된 toodefine 메트릭을 허용 합니다. 응용 프로그램 메트릭 tootrack, 예약 및 해당 응용 프로그램 인스턴스 내 hello 서비스의 제한 hello 리소스 사용을 허용 합니다.

각 응용 프로그램 메트릭에서 두 개의 값을 다음과 같이 설정할 수 있습니다.

- **전체 응용 프로그램 용량** –이 설정은 특정 메트릭에 대 한 hello 응용 프로그램의 총 용량 hello를 나타냅니다. 클러스터 리소스 관리자 hello hello 생성을 해야 하는 총 부하 tooexceed이이 값이 응용 프로그램 인스턴스 내에서 새로운 서비스의 허용 하지 않습니다. 예를 들어 hello 응용 프로그램 인스턴스가 10의 용량 치인 이미 5 개의 부하 가정해 봅니다. 10의 총 기본 부하로 서비스의 hello 만들기가 허용 되지 것입니다.
- **최대 노드 용량** –이 설정은 단일 노드에서 hello hello 응용 프로그램에 대 한 최대 총 부하를 지정 합니다. 이 용량을 통해 로드 되 면 클러스터 리소스 관리자 hello hello 부하가 감소 있도록 복제본 tooother 노드를 이동 합니다.


Powershell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>용량 예약
응용 프로그램 그룹에 대 한 또 다른 일반적인 용도 tooensure 내의 리소스 클러스터 hello는 특정된 응용 프로그램 인스턴스에 대해 예약 된입니다. hello 공간 hello 응용 프로그램 인스턴스를 만들 때 항상 예약 됩니다.

경우에 hello 응용 프로그램을 즉시 전파에 대 한 hello 클러스터에는 공간을 예약 합니다.
- hello 응용 프로그램 인스턴스는 만들어지지만 그 안에 서비스가 아직 없습니다
- hello 응용 프로그램 인스턴스 내에서 서비스의 hello 번호가 변경 될 때마다 
- hello 서비스 존재 하지만 hello 리소스 사용 되지 않습니다. 

응용 프로그램 인스턴스에 대해 리소스를 예약하려면 2개의 추가 매개 변수 *MinimumNodes* 및 *NodeReservationCapacity*를 지정해야 합니다.

- **MinimumNodes** -hello 최소 수를 정의 hello 응용 프로그램 노드의 인스턴스에서 실행 해야 합니다.  
- **NodeReservationCapacity** -이 설정은 hello 응용 프로그램에 대 한 메트릭을 별로 표시 됩니다. hello 값이 있는 hello 실행 해당 응용 프로그램의 서비스는 모든 노드에 hello 응용 프로그램에 대 한 예약 된 해당 메트릭이 hello 용량입니다.

결합 **MinimumNodes** 및 **NodeReservationCapacity** hello 클러스터 내에서 hello 응용 프로그램에 대 한 최소 부하 예약을 보장 합니다. Hello에 대 한 용량 보다 필요한 hello 총 예약 클러스터을 적게 남은 선택한 경우 hello 응용 프로그램을 만들 수 없습니다. 

용량 예약의 예를 살펴보겠습니다.

<center>
![예약된 용량을 정의하는 응용 프로그램 인스턴스][Image2]
</center>

Hello 왼쪽 예제에서 응용 프로그램 정의 하는 응용 프로그램 기능이 갖지 않습니다. 클러스터 리소스 관리자 hello toonormal 규칙에 따라 모든 균형을 조정 합니다.

Hello 오른쪽에 hello 예에서 응용 프로그램 1 설정을 다음 hello로 만들어 졌 음 가정해 보겠습니다.

- MinimumNodes tootwo 설정
- 다음으로 정의된 응용 프로그램 메트릭
  - 20인 NodeReservationCapacity

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

서비스 패브릭 응용 프로그램 1에 대 한 두 개의 노드가에서 용량을 예약 하 고 서비스 응용 프로그램 2 tooconsume에서 부하가 hello 시 응용 프로그램 1 내 hello 서비스에서 사용 되는 경우에 이러한 능력을 허용 하지 않습니다. 이 예약 된 응용 프로그램 용량 사용 하 고 용량 및 hello 클러스터 내에서 해당 노드에 남아 있는 hello에 반해 서 집계 것으로 간주 됩니다.  즉시 클러스터 용량 남은 hello에서 하 게 차감 된 hello 예약, hello 예약 되어 있지만 소비 하 게 차감 된 특정 노드의 hello 용량에서 하나 이상의 서비스에 개체 갖추어야 하는 경우에 합니다. 이후 예약을 사용하면 리소스가 노드에서 필요할 때만 예약되므로 유연성과 리소스 사용률을 개선할 수 있습니다.

## <a name="obtaining-hello-application-load-information"></a>Hello 응용 프로그램 부하 정보 얻기
메트릭을 하나 이상에 대해 정의 된 응용 프로그램 용량이 있는 각 응용 프로그램에 대 한 서비스 복제본에서 보고 하는 hello 집계 부하에 대 한 hello 정보를 얻을 수 있습니다.

Powershell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

hello ApplicationLoad 쿼리 hello hello 응용 프로그램에 대해 지정 된 응용 프로그램 성능에 대 한 기본 정보를 반환 합니다. 이 정보는 hello 노드 최소 및 최대 노드 정보 및 hello 응용 프로그램 현재 차지 하는 hello 번호 포함 됩니다. 다음을 비롯한 각 응용 프로그램 부하 메트릭에 대한 정보도 포함합니다.

* Hello 메트릭의 메트릭 이름: 이름입니다.
* 예약 용량:이 응용 프로그램에 대 한 hello 클러스터에서 예약 된 용량을 클러스터 합니다.
* 응용 프로그램 부하: 이 응용 프로그램 자식 복제본의 총 부하.
* 응용 프로그램 용량: 응용 프로그램 부하의 허용되는 최대값.

## <a name="removing-application-capacity"></a>응용 프로그램 용량 삭제
응용 프로그램에 대 한 hello 응용 프로그램 용량 매개 변수 설정 되 면 제거할 수도 업데이트 응용 프로그램 Api 또는 PowerShell cmdlet을 사용 합니다. 예:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

이 명령은 hello 응용 프로그램 인스턴스에서 모든 응용 프로그램 용량 관리 매개 변수를 제거합니다. 있는 경우 MinimumNodes, MaximumNodes, 및 hello 응용 프로그램의 메트릭을 포함 합니다. 즉시 hello hello 명령의 영향을 주지가 않습니다. 이 명령이 완료 되 면 후 hello 클러스터 리소스 관리자 hello 기본 동작을 사용 하 여 응용 프로그램을 관리 합니다. `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`을 통해 응용 프로그램 용량 매개 변수를 다시 지정할 수 있습니다.

### <a name="restrictions-on-application-capacity"></a>응용 프로그램 용량에 대한 제한 사항
고려해야 할 응용 프로그램 용량 매개 변수에 대한 몇 가지 제한 사항이 있습니다. 유효성 검사 오류가 있는 경우 아무 것도 변경되지 않습니다.

- 모든 정수 매개 변수는 음수가 아닌 숫자여야 합니다.
- MinimumNodes는 MaximumNodes보다 클 수 없습니다.
- 부하 메트릭의 용량을 정의한 경우 다음 규칙을 따라야 합니다.
  - 노드 예약 용량은 최대 노드 용량보다 크지 않아야 합니다. 예를 들어 hello 메트릭에 "CPU" hello 노드 tootwo 단위에 대 한 hello 용량 제한 수 없으며 각 노드에서 tooreserve 세 단위를 시도 하십시오.
  - MaximumNodes를 지정 하는 경우 다음 MaximumNodes 및 최대 노드 용량 hello 제품 하지 보다 커야 합니다 응용 프로그램의 총 용량입니다. 예를 들어 hello 부하 메트릭 "CPU" tooeight 설정에 대 한 최대 노드 용량 가정해 봅니다. 또한 경우를 가정해 최대 노드 too10 hello를 설정 합니다. 이 경우 이 부하 메트릭에 대해 응용 프로그램 총 용량은 80보다 커야 합니다.

응용 프로그램을 만들고 업데이트 하는 동안 둘 다 hello 제한이 적용 됩니다.

## <a name="how-not-toouse-application-capacity"></a>방법 toouse 응용 프로그램 용량 하지
- Toouse hello 응용 프로그램 그룹 기능 tooconstrain hello 응용 프로그램 tooa 마십시오 _특정_ 노드의 하위 집합입니다. 즉, 지정할 수 있습니다에서 최대 5 개의 노드가 hello 응용 프로그램을 실행 하지만 hello 클러스터의 특정 5 노드 하지 않습니다. 응용 프로그램 toospecific 제한 노드 가능 배치 제약 조건을 사용 하 여 서비스에 대 한 합니다.
- 두 서비스에서 동일한 응용 프로그램에 대 한 사항은 hello hello 같은 노드는 toouse hello 응용 프로그램 용량 tooensure를 하지 마십시오. 대신 [선호도](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) 또는 [배치 제약 조건](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)을 사용합니다.

## <a name="next-steps"></a>다음 단계
- 서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.
- toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)
- Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)
- 메트릭이 일반적으로 작동하는 방식에 대한 자세한 내용은 [서비스 패브릭 부하 메트릭](service-fabric-cluster-resource-manager-metrics.md)
- 클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다. toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
