---
title: "서비스 패브릭에서 Chaos 클러스터 aaaInduce | Microsoft Docs"
description: "Hello 클러스터의 오류 삽입 및 클러스터 분석 서비스 Api toomanage Chaos를 사용합니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Service Fabric 클러스터에서 제어되는 비정상 상황 유도
클라우드 인프라와 같은 대규모 분산 시스템은 기본적으로 안정적이지 않습니다. Azure 서비스 패브릭 개발자 toowrite 신뢰할 수 있는 배포 된 서비스를 신뢰할 수 없는 인프라를 기반으로 수 있습니다. toowrite 불안정 한 인프라를 기반으로 강력한 분산된 서비스, 개발자 들이 서비스의 toobe 수 tootest hello 안정성 해야 신뢰할 수 없는 인프라 내부 hello 복잡 한 상태 전환 통과 하는 동안 due toofaults 합니다.

hello [오류 삽입 및 클러스터 분석 서비스](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (라고도 hello 오류 Analysis Service)에서는 개발자가 hello 기능 tooinduce 서비스 데 tootest 오류가 발생 합니다. 같은 오류를 시뮬레이션 된 대상으로 이러한 [파티션을 다시 시작](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), hello 가장 일반적인 상태 전환을 실행 하는 데 도움이 됩니다. 그러나 대상 시뮬레이트 오류는 기본적으로 편향되어 있으므로 예측하기 어렵고 오래 진행되는 복잡한 상태 전환 시퀀스로만 나타나는 버그는 놓칠 수 있습니다. 편향되지 않는 테스트를 위해서는 비정상 상황을 사용할 수 있습니다.

Chaos 시간의 오랜된 기간 동안 hello 클러스터 전체에서 정기적으로 인터리브 오류 (정상 및 비정상)을 시뮬레이션합니다. Hello 환율 및 hello 종류의 오류와 함께 Chaos를 구성한 후에 hello 클러스터에서 한 서비스에서 오류를 생성 하는 C# 또는 Powershell API toostart 통해 Chaos를 시작할 수 있습니다. Chaos toorun Chaos 자동으로 중지 되는 지정한 기간 동안 (예: 1 시간)에 대 한 구성 하거나 toostop StopChaos API (C# 또는 Powershell)을 호출할 수 있습니다 언제 든 지 것입니다.

> [!NOTE]
> 현재 형태의 Chaos 적용만 안전 오류 의미 하는 외부 오류 hello 없는 경우 쿼럼 손실, 또는 데이터 손실이 발생 하지 않습니다.
>

Chaos 실행 되는 동안 hello 순간에 실행 하는 hello의 hello 상태를 캡처하는 다양 한 이벤트를 생성 합니다. 예를 들어 한 ExecutingFaultsEvent Chaos가 해당 반복에서 tooexecute를 결정 하는 모든 hello 오류를 포함 합니다. ValidationFailedEvent hello hello 클러스터 유효성 검사 중 발견 된 유효성 검사 실패 (상태 또는 안정성 문제)의 hello 세부 정보를 포함 합니다. Hello Chaos 실행 tooget hello 보고서 GetChaosReport API (C# 또는 Powershell)을 호출할 수 있습니다. 이러한 이벤트는 두 가지 구성 **MaxStoredChaosEventCount**(기본값 25000) 및 **StoredActionCleanupIntervalInSeconds**(기본값 3600)에 따라 잘림 정책이 적용되는 [신뢰할 수 있는 사전](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections)에 유지됩니다. 모든 *StoredActionCleanupIntervalInSeconds* Chaos 검사 및 모든 하지만 hello 가장 최근의 *MaxStoredChaosEventCount* 이벤트 hello 신뢰할 수 있는 사전에서 제거 됩니다.

## <a name="faults-induced-in-chaos"></a>비정상 상황에서 유도되는 오류
Chaos는 hello 전체 서비스 패브릭 클러스터 전체에서 오류를 생성 하 고 몇 시간에 월 또는 년 단위로 표시 되는 오류를 압축 합니다. hello 높은 오류 숙박료가 인터리브 오류의 hello 조합 그렇지 않으면 누락 될 수 있는 코너 케이스를 찾습니다. 이 연습 Chaos의 hello 서비스의 코드 품질 hello에에서 tooa 향상을 안내합니다.

Chaos는 hello 다음 범주에서에서 오류를 적용 합니다.

* 노드 다시 시작
* 배포된 코드 패키지 다시 시작
* 복제본 제거
* 복제본 다시 시작
* 주 복제본 이동(구성 가능)
* 보조 복제본 이동(구성 가능)

비정상 상황에서는 각 반복 오류와 hello에 대 한 클러스터 유효성 검사 기간이 지정 됩니다. Hello 시간 toosucceed 유효성 검사 및 클러스터 toostabilize hello에 대 한 구성할 수 있습니다. 클러스터 유효성 검사에 오류가 있으면 Chaos를 생성 하 고는 ValidationFailedEvent hello UTC 타임 스탬프 및 hello 실패 세부 정보를 유지 합니다. 예를 들어 인스턴스의 Chaos toorun는 3 개의 동시 오류 최대 한 시간에 설정 된 것이 좋습니다. Chaos 세 개의 오류를 적용 한 다음 hello 클러스터 상태에 검증 합니다. 반복 하면서 이전 hello 명시적으로 중지 된 hello StopChaosAsync API 통해 또는 한 시간 될 때까지 단계를 통과 합니다. Hello 클러스터 반복에서 비정상 상태가 되는 경우 (즉, 해당 않습니다 하지 안정화 MaxClusterStabilizationTimeout 전달 기능에 hello 내), Chaos는 ValidationFailedEvent를 생성 합니다. 이 이벤트는 무언가 잘못되었으며 자세한 조사가 필요할 수 있음을 나타냅니다.

Chaos 인 한 오류를 처리 하는 tooget GetChaosReport API (powershell 또는 C#)를 사용할 수 있습니다. hello API hello hello 전달 된 연속 토큰 또는 hello 전달 된 시간 범위에 따라 hello Chaos 보고서의 다음 세그먼트를 가져옵니다. ContinuationToken tooget hello hello Chaos 보고서의 다음 세그먼트 hello 또는 StartTimeUtc 및 EndTimeUtc를 통해 hello 시간 범위를 지정할 수 있지만 hello에 ContinuationToken hello와 hello 시간 범위를 지정할 수 없습니다 지정 하거나 동일한 호출 합니다. 100 개가 넘는 Chaos 이벤트가 없는 hello Chaos 보고서 세그먼트 100 개 이하의 Chaos 이벤트에 포함 된 세그먼트에 반환 됩니다.

## <a name="important-configuration-options"></a>중요 구성 옵션
* **TimeToRun**: 성공적으로 완료될 때까지 비정상 상황이 실행되는 총 시간입니다. Hello TimeToRun 기간에 대 한 hello StopChaos API를 통해 실행 되기 전에 Chaos를 중지할 수 있습니다.

* **MaxClusterStabilizationTimeout**: hello 최대한의 정상는 ValidationFailedEvent 발생 하기 전에 hello 클러스터 toobecome에 대 한 시간 toowait 합니다. 이 대기는 복구 되는 동안 hello 클러스터에서 tooreduce hello load입니다. 수행 되는 hello 검사 됩니다.
  * Hello 클러스터 상태가 양호함 하는 경우
  * Hello 서비스 상태를 확인 하는 경우
  * Hello 대상 복제본 집합 크기는 이루어졌는지 hello 서비스 파티션에 대 한
  * InBuild 복사본이 없음
* **MaxConcurrentFaults**: hello 각 반복에서 발생 하는 동시 오류의 최대 수입니다. hello hello 크면, Chaos 이며 hello 장애 조치 및 hello 상태 전환 하는 조합 hello 클러스터 통과 하는 복잡 한도 보다 적극적으로 hello 합니다. 

> [!NOTE]
> 이와 상관 없이 어떻게 높은 값 *MaxConcurrentFaults* Chaos에 외부 오류-hello 없는 경우에서 쿼럼 손실 또는 데이터 손실 없습니다-보장 합니다.
>

* **EnableMoveReplicaFaults**: hello 기본 또는 보조 복제본 toomove 유발 하는 hello 부재를 사용 하지 않도록 설정 하거나 사용 합니다. 이러한 오류는 기본적으로 해제됩니다.
* **WaitTimeBetweenIterations**: 반복 간 시간 toowait hello 양입니다. 즉, hello Chaos 장애와 hello 클러스터의 hello 상태 hello 해당 유효성 검사를 완료 하지 테스트를 수행 함으로써 후 일시 중지 하는 시간입니다. hello hello 값이 높을수록 더 낮은 hello hello 평균 오류 삽입 속도입니다.
* **WaitTimeBetweenFaults**: hello 양의 시간 toowait 단일 반복에서 두 개의 연속 된 오류 사이입니다. hello 값을 높게 hello의 더 낮은 hello 동시성 hello (또는 겹치지 hello) 오류입니다.
* **ClusterHealthPolicy**: 클러스터 상태 정책이 사용 되는 toovalidate hello 클러스터 상태에 hello Chaos 반복 사이입니다. Hello 클러스터 상태는 오류가 발생 하거나 예기치 않은 예외가 발생 하면 오류 실행 하는 동안 Chaos hello 다음 상태 확인-일부 시간 toorecuperate tooprovide hello 클러스터 30 분 동안 기다립니다.
* **Context**: (string, string) 형식의 키-값 쌍 컬렉션입니다. hello 맵은 실행 Chaos hello에 대 한 정보를 사용 하는 toorecord 될 수 있습니다. 이러한 쌍은 100개 이하로만 존재할 수 있으며 각 문자열(키 또는 값)은 4095자 이하로만 설정할 수 있습니다. 이 맵은 hello 특정 실행에 대 한 hello 실행 Chaos toooptionally 저장소 hello 컨텍스트 hello 시작으로 설정 됩니다.

## <a name="how-toorun-chaos"></a>어떻게 toorun Chaos

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
