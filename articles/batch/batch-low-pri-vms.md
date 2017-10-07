---
title: "aaaRun Azure 일괄 처리 작업에 비용 효율적인 우선 순위가 낮은 Vm (미리 보기) | Microsoft Docs"
description: "Azure 일괄 처리 작업의 tooprovision 우선 순위가 낮은 Vm tooreduce hello 비용 하는 방법에 대해 알아봅니다."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Batch(미리 보기)에서 낮은 우선 순위 VM 사용

Azure 일괄 처리는 일괄 처리 작업의 낮은 우선 순위 가상 컴퓨터 (Vm) tooreduce hello 비용을 제공합니다. 우선 순위가 낮은 VM은 경제적 측면도 있는 대량의 Compute 성능을 제공하여 새로운 유형의 Batch 워크로드를 가능하게 합니다.

우선 순위가 낮은 VM은 Azure에서 남는 용량을 활용합니다. 풀에서 우선 순위가 낮은 VM을 지정하면 Azure Batch는 가능한 경우 이러한 남는 용량을 자동으로 사용할 수 있습니다.

이 경우 Vm 낮은 우선 순위를 사용 하기 위한 hello 단점이 과도 한 용량은 Azure에서 제공 하는 경우에 해당 Vm을 선점 될 수 있습니다. 이러한 이유로 우선 순위가 낮은 VM이 특정 유형의 워크로드에 가장 적절합니다. Vm 낮은 우선 순위를 사용 하 여 일괄 처리 및 비동기 처리 작업은 유연 hello 작업 완료 시간 및 hello 작업 많은 Vm을 분산 됩니다.

우선 순위가 낮은 VM은 전용 VM보다 훨씬 덜 비쌉니다. 가격 책정 세부 정보에 대해서는 [Batch 가격 책정](https://azure.microsoft.com/pricing/details/batch/)을 참조하세요.

Vm 낮은 우선 순위는 추가 논의 알려면 hello 블로그 게시물 공지: [hello 가격의 일부분에 컴퓨팅 일괄 처리](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)합니다.

> [!IMPORTANT]
> 우선 순위가 낮은 VM은 현재 미리 보기 상태이며 Batch에서 실행되는 워크로드에만 사용할 수 있습니다. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>우선 순위가 낮은 VM에 대한 사용 사례

우선 순위가 낮은 Vm의 hello 특성, 어떤 작업 수와으로 사용할 수 없습니다. 작업이 여러 병렬 태스크로 분할되거나, 많은 VM에서 확장 및 분산되는 많은 작업이 있으므로 일반적으로는 Batch 처리 워크로드가 적합합니다.

-   Azure, 적합 한 작업에 과도 한 용량 toomaximize 사용 확장할 수 있습니다.

-   경우에 따라 Vm 사용 하지 못할 또는 있는 작업에 대 한 용량을 감소 되 고 tootask 중단 및 트리거하는지 않을 선점 될 것입니다. 따라서 작업 유연한 toorun 많이 hello 시간 이어야 합니다.

-   좀 더 긴 태스크를 포함하는 작업은 중단될 경우 더 많은 영향을 받을 수 있습니다. 장기 실행 작업 실행 검사점 toosave 진행 상황을 구현 하는 경우 다음 중단의 영향 것 훨씬 적습니다. 실행 시간이 짧은 작업 간격과 toowork 가장 우선 순위가 낮은 Vm과 중단의 hello 영향은 훨씬 적습니다.

-   여러 Vm을 활용 하는 MPI 작업에 가장 적합된 toouse 없는 장기 실행 선점된 하나의 VM으로 우선 순위가 낮은 Vm 가능성이 높은 잠재 고객 toohello 전체 작업을 다시 실행 toobe 필요 합니다.

일괄 처리의 몇 가지 예의 경우에 가장 적합된 toouse vm 낮은 우선 순위를 사용 합니다.

-   **개발 및 테스트**: 특히 대규모 솔루션을 개발 중인 경우 상당한 비용 절감을 실현할 수 있습니다. 모든 유형의 테스트가 혜택을 볼 수 있지만 대규모 부하 테스트 및 회귀 테스트에 사용하면 아주 좋습니다.

-   **요청 시 용량 보완**: regular 전용된 Vm-보완 하기 위해 Vm 낮은 우선 순위를 사용할 수 작업의 크기를 조정 하 고 따라서 저렴 한 비용에 대 한 훨씬 더 빠르게 완료 수, 사용 가능한 경우; 때의 전용을 사용할 수 없는 hello 초기 Vm을 사용할 수 있습니다.

-   **유연한 작업 실행 시간**: hello 타이머 작업이 더 유연성을 제공 하는 경우 toocomplete, 한 다음 잠재적인 용량 감소 허용 될 수 있으며 단, hello로 우선 순위가 낮은 Vm 작업의 추가 자주 실행 빠르고 저렴 한 비용에 대 한 합니다.

일괄 처리 풀의 hello 유연성에 따라 몇 가지 방법으로 우선 순위가 낮은 Vm 작업 실행 시간이 구성 된 toouse 될 수 있습니다.

-   풀에서 우선 순위가 낮은 VM만 사용될 수 있고 Batch 기능은 사용 가능한 경우 선점된 용량을 복구합니다. 이 hello 가장 저렴 한 방식으로 tooexecute 작업만 우선 순위가 낮은 Vm에 사용 됩니다.

-   우선 순위가 낮은 VM을 고정된 전용 VM과 함께 사용할 수 있습니다. hello 전용된 Vm의 고정 된 수 있는지 확인할 일부 용량 tookeep 항상 작업 진행 합니다.

-   사용 가능한 경우 더 저렴 우선 순위가 낮은 Vm 전적으로 사용 되지만 필요한 경우 tookeep 용량 사용 가능한 tookeep hello 작업의 최소 크기를 확장 하는 전용 전체 가격이 책정 hello Vm 수 있도록 동적 조합의 전용 및 우선 순위가 낮은 Vm 수 있습니다. 진행 합니다.

## <a name="batch-support-for-low-priority-vms"></a>우선 순위가 낮은 VM에 대한 Batch 지원

Azure 배치 쉽게 tooconsume 확인 하 고 우선 순위가 낮은 Vm에서 활용 하는 몇 가지 기능을 제공 합니다.

-   Batch 풀은 전용 VM 및 우선 순위가 낮은 VM을 모두 포함할 수 있습니다. 풀을 생성 하거나 언제 든 지 자동 크기 조정 또는 안녕하세요 명시적 크기 조정 작업을 사용 하 여 기존 풀에 대 한 변경할 hello 각 유형의 VM 수를 지정할 수 있습니다. 작업 및 태스크 전송 변경 되지 않고 남아 있을 수 및 hello 풀의 hello VM 유형에 신경 쓸 필요가 없습니다. 풀을 완전히 우선 순위가 낮은 Vm toorun 작업 사용 가능 하지만 Vm 전용된 회전 저렴 hello 용량 실행 중인 작업을 유지 하는 최소 임계값 아래로 떨어지는 경우 가능한 toohave 이기도 합니다.

-   일괄 처리 풀 Vm 낮은 우선 순위 toohello 대상 수를 자동으로 검색 합니다. Vm 선점 된 경우 일괄 처리 용량 및 반환 toohello 대상 손실 tooreplace hello를 시도 합니다.

-   Hello 중단 되 고 작업의 경우에서 일괄 처리에서는 검색 하 고 자동으로 다시 실행 작업 toobe 내용을 알리게 됩니다.

-   우선 순위가 낮은 VM의 코어 할당량은 전용 VM과는 다릅니다. 
    우선 순위가 낮은 Vm에 대 한 인용 hello 우선 순위가 낮은 Vm 비용을 줄일 때문에 전용된 Vm의 보다 최신입니다. 자세한 내용은 [Batch 서비스 할당량 및 제한](batch-quota-limit.md#resource-quotas)을 참조하세요.    

> [!NOTE]
> 우선 순위가 낮은 Vm 너무 hello 풀 할당 모드가 설정 되어 있는 일괄 처리 계정에 대 한 현재 지원 되지 않는[사용자 구독](batch-account-create-portal.md#user-subscription-mode)합니다.
>
>

## <a name="create-and-update-pools"></a>풀 만들기 및 업데이트

일괄 처리 풀 전용 및 우선 순위가 낮은 Vm (또한 참조 tooas 계산 노드)를 포함할 수 있습니다. 전용 및 우선 순위가 낮은 Vm에 대 한 계산 노드의 hello 대상 수를 설정할 수 있습니다. hello 노드 수가 대상 수를 지정 hello toohave hello 풀에서 원하는 Vm의 합니다.

예를 들어 5의 대상을 사용 하 여 Azure 클라우드 서비스 Vm을 사용 하 여 풀 a toocreate Vm과 20 대의 우선 순위가 낮은 Vm 전용:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

5의 대상을 사용 하 여 (이 경우 Linux Vm)에서 Azure 가상 컴퓨터를 사용 하 여 풀 a toocreate Vm과 20 대의 우선 순위가 낮은 Vm 전용:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

전용 및 우선 순위가 낮은 Vm에 대 한 hello 현재 노드 수를 얻을 수 있습니다.

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

풀 노드 속성 tooindicate 있으면 hello 노드는 전용 또는 우선 순위가 낮은 VM:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

선점 된 풀에서 하나 이상의 노드, 풀에는 목록 노드 작업은 해당 노드의 반환 여전히, hello 현재 우선 순위가 낮은 노드 수가 동일할 것 있지만 이러한 노드는 상태로 설정 toothe **프로그램 바뀜**상태입니다. 일괄 처리는 Vm toofind 대체를 시도 하 고 hello 노드를 통과 성공 하면 **만들기** 차례로 **시작** 상태 작업 실행을 위해 사용할 수 있게 되기 전에 새 노드에서 동일 하 게 합니다.

## <a name="scale-a-pool-containing-low-priority-vms"></a>우선 순위가 낮은 VM을 포함하는 풀 크기 조정

전적으로 전용된 Vm으로 구성 된 풀에서와 마찬가지로 hello 크기 조정 메서드를 호출 하 여 또는 자동 크기 조정에 사용 하 여 가능한 tooscale는 풀 포함 우선 순위가 낮은 Vm 않습니다.

hello 풀 크기 조정 작업 두 번째 선택적 매개 변수 값을 업데이트 하는 **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

hello 풀 자동 크기 조정 수식을 다음과 같이 Vm 낮은 우선 순위를 지원합니다.

-   가져오거나 hello hello 서비스 정의 된 변수 값을 설정할 수 **$TargetLowPriorityNodes**합니다.

-   Hello 서비스 정의 변수의 hello 값을 얻을 수 **$CurrentLowPriorityNodes**합니다.

-   Hello 서비스 정의 변수의 hello 값을 얻을 수 **$PreemptedNodeCount**합니다. 
    이 변수는 hello hello의 노드 수가 선점 상태 및 사용할 수 없는 선점된 노드 hello 수에 따라 전용 노드의 hello 수의 위아래로 조정할 수 있습니다를 반환 합니다.

## <a name="jobs-and-tasks"></a>작업 및 태스크

작업 및 작업에 대 한 우선 순위가 낮은 노드; 거의 지원이 필요 hello 지원만는 다음과 같습니다.

-   hello JobManagerTask 속성 작업의 새 속성이 **AllowLowPriorityNode**합니다. 
    이 속성이 true 이면 전용 또는 우선 순위가 낮은 노드에 hello 작업 관리자 태스크를 예약할 수 있습니다. 이 속성이 false 이면 hello 작업 관리자 태스크 예약된 tooa 전용된 노드에서만 됩니다.

-   [환경 변수](batch-compute-node-environment-variables.md) 는 사용할 수 있는 tooa 작업 응용 프로그램 우선 순위가 낮은 또는 전용 노드에서 실행 되 고 있는지 여부를 결정할 수 있도록 합니다. hello 환경 변수가 AZ_BATCH_NODE_IS_DEDICATED 합니다.

## <a name="handling-preemption"></a>선점 처리

Vm 수 선점 될 경우에 따라; 이 경우 일괄 처리는 다음 hello:

-   hello 선점된 Vm 상태에 있는 해당 업데이트**프로그램 바뀜**합니다.
-   작업에서 실행 되 던 작업은 다시 대기 하 고 다시 실행 hello 노드 Vm을 선점.
-   hello VM 효과적으로 삭제 됩니다 업계 최고의 tooany 데이터 hello 손실 되는 VM에 로컬로 저장 합니다.
-   hello 풀 지속적으로 사용할 수 있는 우선 순위가 낮은 노드 tooreach hello 대상 수를 시도합니다. 대체 용량이 발견되면 노드는 해당 ID를 유지하지만 다시 초기화되며, 작업 예약에 사용되기 전에 먼저 **만드는 중** 및 **시작 중** 상태를 거치게 됩니다.
-   선점 수는 hello Azure 포털에서에서를 기준으로 사용할 수 있습니다.

## <a name="metrics"></a>메트릭

Hello에 사용할 수 있는 새 메트릭이 [Azure 포털](https://portal.azure.com) 우선 순위가 낮은 노드에 대 한 합니다. 이러한 메트릭은 다음과 같습니다.

- 우선 순위가 낮은 노드 수
- 우선 순위가 낮은 코어 수 
- 선점된 노드 수

hello Azure 포털에서에서 tooview 메트릭:

1. Hello 포털에서 일괄 처리 계정 tooyour를 탐색 하 고 일괄 처리 계정에 대 한 hello 설정을 확인 합니다.
2. 선택 **메트릭** hello에서 **모니터링** 섹션.
3. Hello에서 원하는 hello 메트릭을 선택 **사용 가능한 메트릭** 목록입니다.

![우선 순위가 낮은 노드의 메트릭](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>다음 단계

* 읽기 hello [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), toouse 일괄 처리를 준비 하 고 모든 사용자에 대 한 필수 정보입니다. hello 문서 풀, 노드, 작업 및 작업, 및 hello와 같은 일괄 처리 서비스 리소스에 대 한 자세한 내용은 일괄 처리 응용 프로그램을 작성 하는 동안 사용할 수 있는 많은 API 기능을 포함 합니다.
* Hello에 대 한 자세한 내용은 [일괄 처리 Api와 도구](batch-apis-tools.md) 일괄 처리 솔루션을 만드는 데 사용할 수 있습니다.
