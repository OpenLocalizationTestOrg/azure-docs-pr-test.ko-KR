---
title: "Azure microservices의 aaaSimulate 오류 | Microsoft Docs"
description: "이 문서는 Microsoft Azure 서비스 패브릭에서 찾을 수 hello 테스트 용이성 동작에 대 한 설명입니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>테스트 용이성 작업
순서 toosimulate 신뢰할 수 없는 인프라에서에서 Azure 서비스 패브릭 제공 hello 개발자 toosimulate 방법 사용 하면 다양 한 실제 오류 및 상태 전환 합니다. 이러한 작업을 테스트 용이성 작업이라고 합니다. hello 작업에는 특정 오류 삽입, 상태 전환을 또는 유효성 검사 발생 하는 낮은 수준의 Api hello 됩니다. 이러한 작업을 결합하여 서비스에 대한 포괄적인 테스트 시나리오를 작성할 수 있습니다.

서비스 패브릭은 이러한 작업으로 구성된 몇 가지 일반 테스트 시나리오를 제공합니다. Tootest 일반적인 상태 전환 및 실패의 경우 신중 하 게 선택 되는 이러한 기본 제공 시나리오를 활용 하는 것이 좋습니다. 그러나 동작 하는 포함 되지 않은 기본 제공 시나리오 hello 아직 또는 사용자 지정 응용 프로그램에 맞게 조정 된 시나리오에 대 한 tooadd 검사 하려는 경우 toocreate 사용 되는 사용자 지정 테스트 시나리오를 수 있습니다.

C# hello 동작의 구현은 hello System.Fabric.dll 어셈블리에에서 있습니다. hello 시스템 패브릭 PowerShell 모듈은 hello Microsoft.ServiceFabric.Powershell.dll 어셈블리에에서 있습니다. 런타임 설치의 일환으로, hello ServiceFabric PowerShell 모듈 사용 편의성에 대 한 설치 된 tooallow 됩니다.

## <a name="graceful-vs-ungraceful-fault-actions"></a>정상적인 오류 작업과 비정상적인 오류 작업 비교
테스트 용이성 작업은 두 주요 버킷으로 분류됩니다.

* 비정상적 오류: 이러한 오류는 컴퓨터 재시작, 프로세스 충돌 같은 실패를 시뮬레이션합니다. 이러한 오류의 경우 프로세스의 실행 컨텍스트 hello 갑자기 중지합니다. 즉, hello 응용 프로그램 다시 시작 하기 전에 hello 상태의 정리를 실행할 수 있습니다.
* 정상적인 오류: 이러한 오류는 부하 분산에 의해 트리거되는 복제본 이동 또는 삭제 등의 정상적인 작업을 시뮬레이션합니다. 이러한 경우 hello 서비스 hello에 대 한 알림을 닫기 가져오고 종료 하기 전에 hello 상태를 정리할 수 있습니다.

더 나은 품질 유효성 검사에 대 한 hello 서비스를 실행 및 다양 한 오류 정상 및 비정상을 유도 하는 동안 비즈니스 작업 합니다. 비정상적 오류 hello 서비스 프로세스가 갑자기 일부 워크플로의 hello 중간에 종료 되는 시나리오를 실행 합니다. 이 서비스 복제본 hello 서비스 패브릭에서 복원 되 면 hello 복구 경로 테스트 합니다. 데이터의 일관성과 hello 서비스 상태가 실패 후 올바르게 유지 되는지 여부를 테스트 하는 데 도움이 됩니다. hello 다른 집합이 실패 (hello 정상적인 실패) 테스트 hello 서비스에 올바르게 tooreplicas 서비스 패브릭에 의해 이동 되 고 반응 합니다. 이 hello RunAsync 메서드에서 취소의 처리를 테스트합니다. hello 서비스는 hello 취소 토큰 중에 설정 하 고, 올바르게 해당 상태를 저장 하 고, hello RunAsync 메서드 종료 toocheck이 필요 합니다.

## <a name="testability-actions-list"></a>테스트 용이성 작업 목록
| 작업 | 설명 | 관리 API | PowerShell cmdlet | 정상/비정상 오류 |
| --- | --- | --- | --- | --- |
| CleanTestState |Hello 테스트 드라이버의 잘못 된 시스템 종료 시 hello 클러스터에서 모든 hello 테스트 상태를 제거합니다. |CleanTestStateAsync |Remove-ServiceFabricTestState |해당 없음 |
| InvokeDataLoss |서비스 파티션으로 데이터 손실을 유도합니다. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |정상 |
| InvokeQuorumLoss |지정된 상태 저장 서비스 파티션을 쿼럼 손실에 배치합니다. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |정상 |
| Move Primary |이동 hello toohello 지정한 클러스터 노드 상태 저장 서비스의 주 복제본을 지정 합니다. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |정상 |
| Move Secondary |상태 저장 서비스 tooa 다른 클러스터 노드에의 hello 현재 보조 복제본으로 이동합니다. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |정상 |
| RemoveReplica |클러스터에서 복제본을 제거하여 복제 오류를 시뮬레이션합니다. 이렇게 하면 hello 복제본 및 toorole 전환 되 'None', hello 클러스터에서 모든 해당 상태를 제거 합니다. |RemoveReplicaAsync |Remove-ServiceFabricReplica |정상 |
| RestartDeployedCodePackage |클러스터의 노드에 배포된 코드 패키지를 다시 시작하여 코드 패키지 프로세스 오류를 시뮬레이션합니다. 해당 프로세스에 호스팅되는 모든 hello 사용자 서비스 복제본 다시 시작 하는 hello 코드 패키지 프로세스를 중단 합니다. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |비정상 |
| RestartNode |노드를 다시 시작하여 서비스 패브릭 클러스터 노드 오류를 시뮬레이션합니다. |RestartNodeAsync |Restart-ServiceFabricNode |비정상 |
| RestartPartition |파티션의 일부 또는 모든 복제본을 다시 시작하여 데이터 센터 블랙아웃 또는 클러스터 블랙아웃 시나리오를 시뮬레이션합니다. |RestartPartitionAsync |Restart-ServiceFabricPartition |정상 |
| RestartReplica |클러스터에서 영구 복제본을 다시 시작, hello 복제본 닫은 후이 복제본 오류를 시뮬레이트합니다. |RestartReplicaAsync |Restart-ServiceFabricReplica |정상 |
| StartNode |클러스터에서 이미 중지된 노드를 시작합니다. |StartNodeAsync |Start-ServiceFabricNode |해당 없음 |
| StopNode |클러스터의 노드를 중지하여 노드 오류를 시뮬레이션합니다. hello 노드 StartNode를 호출할 때까지 아래로 유지 됩니다. |StopNodeAsync |Stop-ServiceFabricNode |비정상 |
| ValidateApplication |Hello 가용성 및 hello 시스템에 일부 오류를 발생 시켜 후 일반적으로 응용 프로그램 내에서 모든 서비스 패브릭 서비스의 상태를 확인 합니다. |ValidateApplicationAsync |Test-ServiceFabricApplication |해당 없음 |
| ValidateService |일반적으로 hello 시스템에 일부 오류를 발생 시켜 후 hello 가용성 및 서비스 패브릭 서비스의 상태를 확인 합니다. |ValidateServiceAsync |Test-ServiceFabricService |해당 없음 |

## <a name="running-a-testability-action-using-powershell"></a>PowerShell을 사용하여 테스트 용이성 작업 실행
이 자습서에서는 어떻게 toorun PowerShell을 사용 하 여 테스트 용이성 동작 합니다. 에 대해 설명 합니다 방법을 toorun 로컬 (1-상자) 클러스터 또는 Azure 클러스터에 대해 테스트 용이성 동작 합니다. Microsoft.Fabric.Powershell.dll-hello 서비스 패브릭 PowerShell 모듈-자동으로 설치 됩니다 hello Microsoft 서비스 패브릭 MSI를 설치 합니다. hello 모듈은 PowerShell 프롬프트를 열 때 자동으로 로드 됩니다.

자습서 세그먼트:

* [one-box 클러스터에 대해 작업 실행](#run-an-action-against-a-one-box-cluster)
* [Azure 클러스터에 대해 작업 실행](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>one-box 클러스터에 대해 작업 실행
로컬 클러스터에 대 한 테스트 용이성 동작 toorun toohello 클러스터와 관리자 모드에서 열린 hello PowerShell 프롬프트에 먼저 연결 합니다. Hello에 알아보겠습니다 **다시 시작 ServiceFabricNode** 동작 합니다.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

작업을 여기 hello **ServiceFabricNode 다시 시작** "Node1" 이라는 노드를 실행 합니다. hello 완성 모드 하지 hello 노드 다시 시작 작업 실제로 성공 했는지 여부를 확인 해야 것을 지정 합니다. "확인"으로 hello 완성 모드를 지정 하면 tooverify 실제로 hello를 다시 시작 동작의 성공 여부. Hello 노드 이름을 사용 하 여를 직접 지정 하지 않고 지정할 수 있습니다는 파티션 키와 hello 종류의 복제본을 통해 다음과 같습니다.

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**다시 시작 ServiceFabricNode** 서비스 패브릭 노드 클러스터에서 사용 되는 toorestart 있어야 합니다. 모든 hello 시스템 서비스 및 사용자 서비스에서 호스팅되는 복제본 해당 노드는 다시 시작 하는 hello Fabric.exe 프로세스를 중지 합니다. 이 API tootest를 사용 하 여 서비스 hello 장애 복구 경로 따라 버그를 확인할 수 있습니다. Hello 클러스터의 노드 오류를 시뮬레이션할 수 있습니다.

hello 다음 스크린샷은 hello **다시 시작 ServiceFabricNode** 테스트 용이성 명령 활용 합니다.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

먼저의 hello 출력 hello **Get ServiceFabricNode** 해당 hello 로컬 클러스터에는 5 개의 노드가 있는 (hello 서비스 패브릭 PowerShell 모듈의 cmdlet)를 보여 줍니다: Node.1 tooNode.5 합니다. Hello 테스트 용이성 동작 (cmdlet) 후 **다시 시작 ServiceFabricNode** hello 노드에서 실행 Node.4 명명 된, 보면 해당 hello 노드 가동 시간을 다시 설정 되었습니다.

### <a name="run-an-action-against-an-azure-cluster"></a>Azure 클러스터에 대해 작업 실행
Azure 클러스터에 대해 테스트 용이성 작업 (PowerShell 사용)에서 실행 하는 것은 로컬 클러스터에 대해 비슷한 toorunning hello 작업입니다. hello 차이점은 연결 toohello 로컬 클러스터 대신 hello 동작을 실행 하기 전에 필요한 tooconnect toohello Azure 먼저 클러스터 합니다.

## <a name="running-a-testability-action-using-c35"></a>C&#35;을 사용하여 테스트 용이성 작업 실행
C#을 사용 하 여 테스트 용이성 작업 toorun 먼저 tooconnect toohello 클러스터 FabricClient를 사용 하 여 합니다. 다음 hello 필요한 매개 변수 toorun hello 동작을 확인 합니다. 다른 매개 변수를 사용할 수 있습니다 toorun hello 동일한 동작입니다.
Hello 클러스터의 hello hello 노드 정보 (노드 이름과 노드 인스턴스 ID)을 사용 하 여 한 가지 방법은 toorun RestartServiceFabricNode 동작을 찾습니다.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

매개 변수 설명:

* **CompleteMode** 지정 hello 모드를 사용 하는 hello 다시 시작 동작 실제로 성공 했는지 여부를 확인 하지 않아야 합니다. "확인"으로 hello 완성 모드를 지정 하면 tooverify 실제로 hello를 다시 시작 동작의 성공 여부.  
* **OperationTimeout** TimeoutException 예외는 throw 되기 전에 집합 hello 작업 toofinish hello에 대 한 시간입니다.
* **CancellationToken** 취소는 보류 중인 호출 toobe 수 있도록 합니다.

Hello 노드 이름을 사용 하 여를 직접 지정 하지 않고 복제 데이터베이스의 파티션 키와 hello 종류를 통해 지정할 수 있습니다.

자세한 내용은 [PartitionSelector 및 ReplicaSelector](#partition_replica_selector)를 참조하세요.

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector 및 ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector 테스트 가능성에 노출 하는 도우미 이며가 사용 되는 tooselect 특정 분할 작업을 어떤 tooperform hello 테스트 용이성 동작 중 하나입니다. Hello 파티션 ID가 미리 알려진 경우 사용 되는 특정 파티션에 tooselect 수 있습니다. 또는 hello 파티션 키를 제공할 수 있습니다를 hello 작업 hello 파티션 ID를 내부적으로 해결 됩니다. 임의의 파티션을 선택한 hello 옵션이 있습니다.

toouse이이 도우미 hello PartitionSelector 개체를 만들고 hello Select * 방법 중 하나를 사용 하 여 hello 파티션을 선택 합니다. Hello PartitionSelector 개체 toohello에서 필요로 하는 API에 전달 합니다. 없음 옵션을 선택 하는 경우 tooa 임의 파티션을 기본값으로 사용 합니다.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector 테스트 가능성에 노출 하는 도우미 인데은 사용 되는 toohelp 선택 복제본 어떤 tooperform에 hello 테스트 용이성 동작 중 하나입니다. Hello 복제본 ID가 미리 알려진 경우 사용 되는 tooselect 특정 복제본 수 있습니다. 또한 주 복제본 또는 임의의 보조 데이터베이스를 선택 하면 hello 옵션도가 있습니다. ReplicaSelector PartitionSelector에서 파생 되, 둘 다 hello tooperform hello 테스트 용이성 작업을 원하는 복제 하 고 hello 파티션이 있으므로 tooselect 필요 합니다.

toouse이이 도우미 ReplicaSelector 개체를 만들고 원하는 hello 방식으로 tooselect hello 복제본과 hello 파티션을 설정 합니다. API에서 필요로 하는 hello에 전달할 수 있습니다. 없음 옵션을 선택 하면 tooa 임의의 복제본 및 임의 파티션 기본값입니다.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>다음 단계
* [테스트 용이성 시나리오](service-fabric-testability-scenarios.md)
* 어떻게 tootest 서비스
  * [서비스 작업 중 오류 시뮬레이션](service-fabric-testability-workload-tests.md)
  * [서비스 대 서비스 통신 오류](service-fabric-testability-scenarios-service-communication.md)

