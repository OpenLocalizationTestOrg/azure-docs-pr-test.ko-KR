---
title: "Azure 서비스 패브릭 상태를 확인 하 고 aaaReport | Microsoft Docs"
description: "서비스 코드에서 toosend 상태 보고 하는 방법 및 toocheck hello 상태는 Azure 서비스 패브릭 hello 상태 모니터링 도구를 사용 하 여 서비스를 제공 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>서비스 상태 보고 및 확인
서비스에서 문제가 발생할 때 기능 toorespond tooand 수정 인시던트 및 작동 중단 문제에 종속 프로그램 기능 toodetect hello 신속 하 게 합니다. 서비스 코드에서 문제 및 오류 toohello Azure 서비스 패브릭 상태 관리자를 보고 하는 경우 표준 상태 모니터링 서비스 패브릭 toocheck hello 상태를 제공 하는 도구를 사용할 수 있습니다.

세 가지 방법으로 hello 서비스에서 상태를 보고할 수 있습니다.

* [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 또는 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 개체를 사용합니다.  
  Hello를 사용할 수 있습니다 `Partition` 및 `CodePackageActivationContext` hello 현재 컨텍스트에 포함 되는 요소 tooreport hello 상태 개체입니다. 예를 들어 복제본의 일부로 실행 되는 코드는 해당 복제본는 자신이 속한 hello 파티션 및 hello 응용 프로그램의 일부인 하에 상태를 보고할 수 있습니다.
* `FabricClient`를 사용합니다.   
  사용할 수 있습니다 `FabricClient` hello 클러스터 없으면 hello 서비스 코드에서 tooreport 상태 [보안](service-fabric-cluster-security.md) 아니면 관리자 권한으로 hello 서비스가 실행 되 고 있습니다. 대부분의 실제 시나리오에서는 보안되지 않은 클러스터를 사용하거나 관리자 권한을 제공하지 않습니다. 와 `FabricClient`, hello 클러스터의 일부인 모든 엔터티의 상태를 보고할 수 있습니다. 그러나 이상적으로 서비스 코드만 보내야 관련된 tooits 자체 상태에 있는 보고서를 합니다.
* Hello 클러스터, 응용 프로그램, 배포 된 응용 프로그램, 서비스, 서비스 패키지, 파티션, 복제본 또는 노드 수준에서 hello REST Api를 사용 합니다. 이 컨테이너 내에서 사용 되는 tooreport 상태 수 있습니다.

이 문서에서는 hello 서비스 코드에서 상태를 보고 하는 예제를 안내 합니다. hello 예제에는 서비스 패브릭에서 제공 하는 hello 도구 사용된 toocheck hello 상태를 수 있는 방법을 보여 줍니다. 이 문서는 의도 한 toobe 간략 한 소개 toohello 상태 서비스 패브릭의 기능을 모니터링 합니다. 자세한 내용을 보려면 hello 일련의 hello 끝이 문서에 링크 hello로 시작 하는 상태에 대 한 심도 있는 문서를 읽을 수 있습니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음이 설치 되어 있어야 합니다.

* Visual Studio 2015 또는 Visual Studio 2017
* 서비스 패브릭 SDK

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate 안전한 로컬 개발 클러스터
* 관리자 권한으로 PowerShell을 열고 hello 다음 명령을 실행 합니다.

![방법을 보여 주는 명령 toocreate 보안 개발 클러스터](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy 응용 프로그램의 상태를 확인 합니다.
1. 관리자 권한으로 Visual Studio를 엽니다.
2. Hello를 사용 하 여 프로젝트를 만들 **상태 저장 서비스** 템플릿.
   
    ![상태 저장 서비스를 사용하여 서비스 패브릭 응용 프로그램 만들기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. 키를 눌러 **F5** 디버그 모드에서 toorun hello 응용 프로그램입니다. hello 응용 프로그램은 배포 된 toohello 로컬 클러스터 있습니다.
4. Hello 응용 프로그램을 실행 한 후 hello 알림 영역에서 hello 로컬 클러스터 관리자 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **로컬 클러스터 관리** hello 바로 가기 메뉴 tooopen 서비스 패브릭 탐색기에서에서 합니다.
   
    ![알림 영역에서 서비스 패브릭 탐색기 열기](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. 이 이미지와 같이 hello 응용 프로그램 상태를 표시 합니다. 이때 hello 응용 프로그램 오류 없이 정상 이어야 합니다.
   
    ![서비스 패브릭 탐색기에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. 또한 PowerShell을 사용 하 여 hello 상태를 확인할 수 있습니다. 사용할 수 있습니다 ```Get-ServiceFabricApplicationHealth``` 응용 프로그램의 상태 및 있습니다 사용할 수 toocheck ```Get-ServiceFabricServiceHealth``` toocheck 서비스의 상태입니다. PowerShell에서 동일한 응용 프로그램은이 이미지에 hello에 대 한 상태 보고서를 hello 합니다.
   
    ![PowerShell에서 정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>tooadd 사용자 지정 상태 이벤트 tooyour 서비스 코드
Visual Studio에서 hello 서비스 패브릭 프로젝트 템플릿은 샘플 코드를 포함합니다. hello 다음 단계 표시 방법을 서비스 코드에서 사용자 지정 상태 이벤트를 보고할 수 있습니다. 이런 종류의 보고서 자동으로 도구에 표시 hello 표준 서비스 패브릭 제공 하는지, PowerShell, 서비스 패브릭 탐색기 및 Azure 포털 상태 보기 등을 모니터링 하는 상태에 대 한 합니다.

1. Visual Studio에서 이전에 만든 hello 응용 프로그램을 닫았다가 다시 열거나 hello를 사용 하 여 새 응용 프로그램을 만들 **상태 저장 서비스** Visual Studio 템플릿이 있습니다.
2. Hello Stateful1.cs 파일을 열고 hello `myDictionary.TryGetValueAsync` hello에서 호출 `RunAsync` 메서드. 이 메서드가 반환 하는지 확인할 수 있습니다는 `result` 보류 hello 카운터의 현재 값을이 응용 프로그램에서 키 논리 hello tookeep 개수 실행 중 이므로 hello 하 합니다. 실제 응용 프로그램의 경우 및 결과의 hello 부족 오류를 표시 하는 경우 해당 이벤트 tooflag를 사용할 수 있습니다.
3. 결과의 hello 부족 오류를 나타내는 경우 상태 이벤트 tooreport hello 다음 단계를 추가 합니다.
   
    a. Hello 추가 `System.Fabric.Health` 네임 스페이스 toohello Stateful1.cs 파일입니다.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Hello hello 후 코드를 다음 추가 `myDictionary.TryGetValueAsync` 호출
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    이 복제본 상태는 상태 저장 서비스에서 보고되므로 해당 상태를 보고합니다. hello `HealthInformation` 보고 하는 hello 상태 문제에 대 한 정보를 저장 하는 매개 변수입니다.
   
    코드 다음 hello를 사용 하 여 상태 비저장 서비스를 만들 때
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. 서비스 관리자 권한으로 실행 되거나 hello 클러스터 없으면 경우 [보안](service-fabric-cluster-security.md), 사용할 수도 있습니다 `FabricClient` hello 다음 단계에에서 표시 된 대로 tooreport 상태입니다.  
   
    a. Hello 만들기 `FabricClient` hello 후 인스턴스 `var myDictionary` 선언 합니다.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Hello hello 후 코드를 다음 추가 `myDictionary.TryGetValueAsync` 호출 합니다.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. 이 오류를 시뮬레이션 하 고 hello 상태 모니터링 도구에서 표시 살펴보겠습니다. 이전에 추가한 코드를 보고 하는 hello 상태에서 hello 첫 번째 줄의 주석 toosimulate hello 실패 합니다. Hello 첫 번째 줄을 주석 후 hello 코드는 다음 예제는 hello와 같습니다.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   이 코드 hello 상태 보고서를 될 때마다 발생 `RunAsync` 실행 합니다. 키를 눌러 변경 hello를 변경한 후 **F5** toorun hello 응용 프로그램입니다.
6. Hello 응용 프로그램을 실행 한 후에 hello 응용 프로그램의 서비스 패브릭 탐색기 toocheck hello 상태를 엽니다. 이 시간 서비스 패브릭 탐색기 hello 응용 프로그램 상태가 표시 됩니다. 이전에 추가한 hello 코드에서 보고 된 hello 오류 때문에 이것이입니다.
   
    ![서비스 패브릭 탐색기에서 비정상적인 응용 프로그램](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. 서비스 패브릭 탐색기의 hello 트리 보기에서 hello 주 복제본을 선택 하면 확인 하 게 **상태** 너무 오류를 나타냅니다. 서비스 패브릭 탐색기에 내용 추가 toohello hello 상태 보고서도 표시 됩니다 `HealthInformation` hello 코드의 매개 변수입니다. 나타나면 PowerShell에서 동일한 상태 보고서 hello 및 Azure 포털 hello 합니다.
   
    ![서비스 패브릭 탐색기 내 복제본 상태](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

이 보고서는 다른 보고서 또는이 복제본이 삭제 될 때까지 교체 될 때까지 hello 상태 관리자에서 유지 됩니다. 여백을 설정 하지 않았으므로 때문에 `TimeToLive` hello에서이 상태 보고서에 대 한 `HealthInformation` 개체 hello 보고서 만료 되지 않습니다.

Hello 가장 세분화 된 수준에는 예에서 hello 복제 데이터베이스 상태를 보고 해야 하는 것이 좋습니다. `Partition`에 대해 상태를 보고할 수도 있습니다.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

tooreport 상태 `Application`, `DeployedApplication`, 및 `DeployedServicePackage`를 사용 하 여 `CodePackageActivationContext`합니다.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>다음 단계
* [서비스 패브릭 상태 심층 분석](service-fabric-health-introduction.md)
* [서비스 상태를 보고하기 위한 REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [응용 프로그램 상태를 보고하기 위한 REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

