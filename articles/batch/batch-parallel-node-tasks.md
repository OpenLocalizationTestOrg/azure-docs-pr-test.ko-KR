---
title: "병렬 toouse의 aaaRun 작업 컴퓨터 리소스를 효율적으로-Azure 일괄 처리 | Microsoft Docs"
description: "Azure 배치 풀의 각 노드에서 동시 작업을 실행하고 더 적은 수의 계산 노드를 사용하여 효율성은 높이고 비용은 낮춥니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>일괄 처리 계산 노드 toomaximize 사용 작업을 동시에 실행 

Azure 배치 풀의 각 계산 노드에서 동시에 둘 이상의 작업을 실행 하 여 hello 풀에 있는 노드의 더 적은 수의 리소스 사용을 최대화할 수 있습니다. 일부 워크로드의 경우, 작업 시간이 짧아지고 비용이 낮아질 수 있습니다.

을 일부 시나리오에서 모든 노드의 리소스 tooa 단일 작업의 전용 제대로 활용 하는 동안 여러 가지 상황에서 여러 작업 tooshare 리소스만 좋습니다.

* **데이터 전송 최소화** 경우 작업은 수 tooshare 데이터입니다. 이 시나리오에서는 크게 절약할 수 있습니다는 데이터 전송 비용이 공유 데이터 tooa 더 적은 수의 노드를 복사 하 여 각 노드에서 동시에 작업을 실행 하 고 있습니다. 특히 hello 데이터 toobe 복사한 tooeach 노드 지리적 지역 간의 전송 해야 하는 경우이 적용 됩니다.
* **메모리 사용 최대화** - 태스크에 많은 양의 메모리가 필요하지만 단기간에만 그리고 실행 중에는 가변 시간에 메모리 사용량을 최대화합니다. 더 큰 하지만 적은 사용, 계산 노드를 더 많은 메모리 tooefficiently 이러한 급증을 처리할 수 있습니다. 이러한 노드는 각 노드에 대해 병렬로 실행 하는 여러 작업이 있을 수 있지만 각 작업은 서로 다른 시간에 hello 노드 매우 많은 메모리를 활용 하기 위해.
* **노드 숫자 제한 완화** . 현재 노드 간 통신을 위해 구성 된 풀 제한 too50 계산 노드는. 이러한 풀의 각 노드는 병렬로 수 tooexecute 작업, 작업 수를 더 동시에 실행할 수 있습니다.
* **온-프레미스 계산 클러스터를 복제**, 먼저 이동 하는 경우 계산 환경 tooAzure 등입니다. Hello 최대 수를 늘릴 수 계산 노드에 당 여러 작업을 실행 하는 현재 온-프레미스 솔루션의 노드 작업 toomore 밀접 하 게 해당 구성을 복사 합니다.

## <a name="example-scenario"></a>예제 시나리오 
예제 tooillustrate로 hello 병렬 작업 실행의 이점, 가정해 작업 응용 프로그램에서 CPU 및 메모리 요구 사항이 되도록 [표준\_D1](../cloud-services/cloud-services-sizes-specs.md) 노드는 충분 합니다. 되지만 이러한 노드 중 1, 000 필요한 hello 시간에서 toofinish hello 작업 순서에서에서 필요 합니다.

1개 CPU 코어가 있는 Standard\_D1 노드를 사용하는 대신 각각 16개 코어가 있는 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 노드를 사용하여 병렬 태스크 실행을 구현할 수 있습니다. 따라서 사용되는 *노드 수가 1/16로 줄기 때문에* 필요한 노드 수는 1000개가 아니라 63개입니다. 또한 대형 응용 프로그램 파일이 나 참조 데이터 각 노드에 대해 필요한 경우 작업 기간 및 효율성은 다시 향상 hello 데이터는 16 개의 노드로 구성 복사한 tooonly 이므로.

## <a name="enable-parallel-task-execution"></a>병렬 작업 실행 사용
Hello 풀 수준에서 병렬 작업 실행에 대 한 계산 노드를 구성합니다. Hello 일괄 처리.NET 라이브러리를 사용 하 여 hello 설정할 [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 풀을 만들 때 속성입니다. Hello 배치 REST API를 사용 하는 경우 설정 hello [maxTasksPerNode] [ rest_addpool] 풀을 만드는 동안 hello 요청 본문의 요소입니다.

Azure 배치 tooset toofour 배 (4 x) hello 노드 코어 수가를 노드당 최대 작업 수 있습니다. 예를 들어 경우 hello으로 풀이 구성 되어 (4 코어), "Large" 크기의 노드 다음 `maxTasksPerNode` too16 설정 될 수 있습니다. Hello hello 노드 크기를 각 코어 수에 대 한 세부 정보를 참조 하십시오. [클라우드 서비스에 대 한 크기](../cloud-services/cloud-services-sizes-specs.md)합니다. 서비스 제한에 대 한 자세한 내용은 참조 하십시오. [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다.

> [!TIP]
> 계정 hello에 있는지 tootake 수 `maxTasksPerNode` 를 생성할 때 값는 [자동 크기 조정 수식을] [ enable_autoscaling] 풀에 있습니다. 예를 들어, `$RunningTasks` 를 평가하는 수식은 노드당 작업 수 증가에 크게 영향을 받을 수 있습니다. 자세한 내용은 [Azure Batch 풀에서 자동으로 계산 노드 크기 조정](batch-automatic-scaling.md) 을 참조하세요.
>
>

## <a name="distribution-of-tasks"></a>작업 배분
Hello 계산 노드는 풀의 작업을 동시에 실행할 수 때 중요 한 toospecify 원하는 hello 작업 toobe hello 풀의 hello 노드에 분산 됩니다.

Hello를 사용 하 여 [CloudPool.TaskSchedulingPolicy] [ task_schedule] 속성 ("확산") hello 풀의 모든 노드에서 태스크를 균등 하 게 할당할 수 있도록을 지정할 수 있습니다. 또는 가능한 한 많은 작업 할당 해야 tooeach 노드 작업 tooanother 노드 ("패키지") hello 풀에 할당 되기 전에 지정할 수 있습니다.

이 기능은 유용 방법의 예를 들어 hello 풀 고려 [표준\_D14](../cloud-services/cloud-services-sizes-specs.md) (위의 hello 예제)에 구성 된 노드는 [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 16의 값입니다. 경우 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] 구성 된 한 [ComputeNodeFillType] [ fill_type] 의 *팩*, 각 노드의 모든 16 개 코어의 사용을 최대화 하 고 허용 합니다는 [자동 크기 조정 풀](batch-automatic-scaling.md) tooprune hello 풀 (할당 된 작업 없이 노드)에서 사용 되지 않는 노드. 리소스 사용량을 최소화하고 비용을 절감합니다.

## <a name="batch-net-example"></a>Batch .NET 예
이 [일괄 처리.NET] [ api_net] API 코드 조각을 요청 toocreate 노드당 4 개 작업의 최대 4 개의 큰 노드를 포함 하는 그룹을 표시 합니다. 예약 작업 이전 tooassigning 작업 tooanother 노드 hello 풀의 각 노드에 채울 정책 작업을 지정 합니다. 풀 hello 일괄 처리.NET API를 사용 하 여 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [BatchClient.PoolOperations.CreatePool][poolcreate_net]합니다.

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Batch REST 예
이 [배치 REST] [ api_rest] API 조각 요청 toocreate 노드당 4 개 작업의 최대 두 개의 큰 노드를 포함 하는 그룹을 표시 합니다. 풀 hello REST API를 사용 하 여 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [풀 tooan 계정 추가][rest_addpool]합니다.

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Hello를 설정할 수 있습니다 `maxTasksPerNode` 요소 및 [MaxTasksPerComputeNode] [ maxtasks_net] 풀 만들 때에만 속성입니다. 풀이 이미 만들어진 후에는 수정될 수 없습니다.
>
>

## <a name="code-sample"></a>코드 샘플
hello [ParallelNodeTasks] [ parallel_tasks_sample] GitHub에서 프로젝트 hello hello 사용을 보여 줍니다. [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 속성입니다.

이 C# 콘솔 응용 프로그램 사용 hello [일괄 처리.NET] [ api_net] 라이브러리 toocreate 하나 이상의 풀 계산 노드. 이러한 노드 toosimulate 가변 부하에서 구성 가능한 다양 한 태스크를 실행합니다. 출력 hello 응용 프로그램에서 각 작업을 실행 하는 노드를 지정 합니다. 또한 hello 응용 프로그램 hello 작업 매개 변수 및 기간에 대 한 요약을 제공합니다. hello 샘플 응용 프로그램의 두 가지 다른 실행에서 hello 출력의 hello 요약 부분 아래에 나타납니다.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

hello 샘플 응용 프로그램의 첫 번째 실행 hello 표시 하는 hello 그룹 및 hello 기본 설정인 노드당 한 작업의 단일 노드와 상호 hello 작업 기간 (30 분) 합니다.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

hello 실행 hello 샘플 프로그램의 중요 한 작업 기간을 감소 합니다. 즉, hello 풀 거의 hello 시간의 사분기에 병렬 작업 실행 toocomplete hello 작업에 대 한 허용 노드당 4 개 작업으로 구성 되었습니다.

> [!NOTE]
> 위의 hello 요약에서 작업 기간 hello 풀 생성 시간을 포함 하지 마십시오. 계산 노드를 모두 hello에 제출 된 toopreviously 만든 풀이 위의 hello 작업의 각 *Idle* 제출 시 상태입니다.
>
>

## <a name="next-steps"></a>다음 단계
### <a name="batch-explorer-heat-map"></a>배치 탐색기 열 지도
hello [Azure 일괄 처리 탐색기][batch_explorer], hello Azure 일괄 처리 중 하나 [샘플 응용 프로그램][github_samples]를 포함 한 *열지도* 태스크 실행의 시각화를 제공 하는 기능입니다. Hello를 실행 하는 경우 [ParallelTasks] [ parallel_tasks_sample] 샘플 응용 프로그램에서는 hello 열 지도 기능 tooeasily hello 각 노드에서 병렬 작업 실행을 시각화 합니다.

![배치 탐색기 열 지도][1]

*현재 4가지 작업을 실행하는 각 노드와 4개 노드의 풀을 보여 주는 배치 탐색기 열 지도*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
