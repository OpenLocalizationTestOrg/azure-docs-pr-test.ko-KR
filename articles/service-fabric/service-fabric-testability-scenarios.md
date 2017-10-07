---
title: "Azure microservices에 대 한 aaaCreate chaos 및 장애 조치 테스트 | Microsoft Docs"
description: "서비스 패브릭 hello를 사용 하 여 chaos 테스트 및 장애 조치 tooinduce 오류 시나리오를 테스트 하 고 서비스의 hello 신뢰성을 확인 합니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>테스트 용이성 시나리오
클라우드 인프라 같은 대규모 분산 시스템은 본질적으로 불안정합니다. Azure 서비스 패브릭 제공 개발자 hello 기능 toowrite 서비스 toorun 신뢰할 수 없는 인프라를 기반으로 합니다. 순서 toowrite 고품질 서비스에서는 개발자 들이 서비스의 신뢰할 수 없는 인프라 tootest hello 안정성 이러한 toobe 수 tooinduce을 해야합니다.

hello 오류 분석 서비스 오류의 hello 존재의 개발자 hello 기능 tooinduce 오류 동작 tootest 서비스를 제공 합니다. 그러나 특정 대상을 통한 오류 시뮬레이션으로는 한계가 있습니다. 또한 테스트 tootake hello hello 테스트 시나리오를 사용 하 여 서비스 패브릭에서: chaos 테스트 및 장애 조치 테스트 합니다. 이러한 시나리오는 정상 및 비정상 시간의 오랜된 기간 동안 hello 클러스터 전체에서 인터리빙된 연속 오류를 시뮬레이션합니다. 테스트 hello 환율 및 종류의 오류와 함께 구성 되 면 C# Api 또는 PowerShell, hello 클러스터에서 toogenerate 오류 및 서비스를 통해 시작할 수 있습니다.

> [!WARNING]
> ChaosTestScenario는 회복력이 뛰어난 서비스 기반 비정상 상황으로 바뀝니다. Toohello 새 문서를 참조 하십시오 [Chaos 제어](service-fabric-controlled-chaos.md) 내용을 확인 합니다.
> 
> 

## <a name="chaos-test"></a>비정상 상황 테스트
hello chaos 시나리오 hello 전체 서비스 패브릭 클러스터 전체에서 오류를 생성 합니다. hello 시나리오는 일반적으로 볼 수 개월 또는 수 년 tooa에서 몇 시간 오류를 압축 합니다. hello 높은 오류 숙박료가 인터리브 오류의 hello 조합 그렇지 않으면 누락 코너 케이스를 찾습니다. 이 hello 서비스 hello 코드 품질에서 향상을 tooa 이어집니다.

### <a name="faults-simulated-in-hello-chaos-test"></a>Hello chaos 테스트에서 시뮬레이션 된 오류
* 노드 다시 시작
* 배포된 코드 패키지 다시 시작
* 복제본 제거
* 복제본 다시 시작
* 주 복제본 이동(선택 사항)
* 보조 복제본 이동(선택 사항)

hello chaos 테스트 오류를 여러 차례 반복 실행 하 고 hello에 대 한 클러스터 유효성 검사 일정 기간을 지정 합니다. hello 시간 toosucceed 유효성 검사 및 클러스터 toostabilize hello에 대 한 구성 가능한 이기도 합니다. hello 시나리오에는 단일 클러스터 유효성 검사 실패에 도달 하면 실패 합니다.

예를 들어 테스트는 3 개의 동시 오류 최대 1 시간 동안 toorun를 설정 하는 것이 좋습니다. hello 테스트 유도 세 개의 오류를 한 다음 hello 클러스터 상태를 확인 합니다. hello 테스트 hello 클러스터 비정상 또는 1 시간까지 hello 이전 단계를 반복 됩니다. Hello 클러스터는 반복에서 비정상 상태가 되 면, 즉 구성 된 시간 내 안정화 하지 않는 면 hello 테스트 예외와 함께 실패 합니다. 이 예외는 뭔가가 잘못되었으며 자세한 조사가 필요함을 나타냅니다.

현재 형태의 hello 오류 생성 엔진 hello chaos 테스트에만 안전 오류를 적용 합니다. 이 hello 없는 경우 외부 오류, 쿼럼 또는 데이터 손실이 발생 하지 것을 의미 합니다.

### <a name="important-configuration-options"></a>중요 구성 옵션
* **TimeToRun**: 총 시간 해당 hello 테스트가 성공적으로 완료 하기 전에 실행 됩니다. hello 테스트 유효성 검사 실패 하는 대신 이전 마칠 수 있습니다.
* **MaxClusterStabilizationTimeout**: 시간 toowait hello 클러스터 toobecome hello 테스트 실패 전에 정상 상태에 대 한 최대 크기입니다. hello 수행 되는 검사 클러스터 상태가 양호함 여부, 서비스 상태를 확인, hello 대상 복제 세트 크기 이루어집니다 hello 서비스 파티션에 대 한 않으며 InBuild 복제본이 없는 존재 합니다.
* **MaxConcurrentFaults**: 각 반복에서 유도되는 동시 오류의 최대 수입니다. hello 값이 클수록 hello, 따라서 그 결과 더 복잡 한 장애 조치를 수행 하 고 전환 조합 보다 적극적으로 hello 테스트 hello 합니다. hello 테스트 없는 경우 외부 오류 없습니다 것은 어떻습니까이 구성에 관계 없이 쿼럼 또는 데이터 손실 보장 합니다.
* **EnableMoveReplicaFaults**: 사용 하거나 기본 또는 보조 복제본의 hello hello 이동을 유발 하는 오류를 hello를 사용 하지 않도록 설정 합니다. 이러한 오류는 기본적으로 해제됩니다.
* **WaitTimeBetweenIterations**: 즉, 오류 및 해당 유효성 검사의 라운드 후의 반복 간 시간 toowait입니다.

### <a name="how-toorun-hello-chaos-test"></a>Toorun hello chaos 테스트 하는 방법
C# 샘플

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>장애 조치(failover) 테스트
hello 장애 조치 테스트 시나리오에는 특정 서비스 파티션을 대상으로 하는 hello chaos 테스트 시나리오의 버전입니다. Hello 다른 서비스 영향을 받지 않고 그대로 유지 하면서 장애 조치의 특정 서비스 파티션에 hello 효과 테스트 합니다. Hello 대상 파티션 정보 및 다른 매개 변수와 함께 구성 되 면 서비스 파티션에 대 한 C# Api 또는 PowerShell toogenerate 오류를 사용 하는 클라이언트 쪽 도구도 실행 됩니다. 비즈니스 논리 실행 hello 쪽 tooprovide에서 작업 하는 동안 hello 시나리오는 일련의 시뮬레이션 된 오류와 서비스 유효성 검사를 반복 합니다. 서비스 유효성 검사에서 오류가 발생하면 추가 조사가 필요한 문제가 있다는 의미입니다.

### <a name="faults-simulated-in-hello-failover-test"></a>Hello 장애 조치 테스트에서 시뮬레이션 된 오류
* Hello 파티션 호스팅되는 배포 된 코드 패키지를 다시 시작
* 주/보조 복제본 또는 상태 비저장 인스턴스 제거
* 주/보조 복제본 다시 시작(서비스가 지속되는 경우)
* 주 복제본 이동
* 보조 복제본 이동
* Hello 파티션 다시 시작

선택한 오류를 적용 하 고 hello 서비스 tooensure에서 유효성 검사를의 안정성 실행 하는 hello 장애 조치 테스트 합니다. hello 장애 조치 테스트 hello chaos 테스트에서 여러 오류 시간, 달리 toopossible에서 오류 하나에 적용 합니다. Hello 서비스 파티션 hello 구성 된 제한 시간 내 각 오류 후 안정화 하지 않는 hello 테스트가 실패 합니다. hello 테스트를 안전 하 게 보호 오류만 적용 합니다. 다시 말해서 외부 오류가 없으면 쿼럼 또는 데이터 손실이 발생하지 않습니다.

### <a name="important-configuration-options"></a>중요 구성 옵션
* **PartitionSelector**: toobe 대상으로 해야 하는 hello 파티션을 지정 하는 선택기 개체입니다.
* **TimeToRun**: 총 시간 hello 테스트를 완료 하기 전에 실행 됩니다.
* **MaxServiceStabilizationTimeout**: 시간 toowait hello 클러스터 toobecome hello 테스트 실패 전에 정상 상태에 대 한 최대 크기입니다. hello 수행 되는 검사는 서비스 상태 인지 확인 하 고 hello 대상 복제 세트 크기 이루어집니다 모든 파티션에 대 한 InBuild 복제본이 없는 존재 합니다.
* **WaitTimeBetweenFaults**: 모든 오류 및 유효성 검사 주기 사이의 시간 toowait입니다.

### <a name="how-toorun-hello-failover-test"></a>Toorun hello 장애 조치 테스트 하는 방법
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
