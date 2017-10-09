---
title: "서비스 패브릭 서비스에서 데이터 손실이 aaaHow tooInvoke | Microsoft Docs"
description: "Toouse 데이터 손실을 hello 하는 방법에 대해 설명 api"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a>어떻게 tooInvoke 서비스에서 데이터 손실
> [!WARNING]
> 이 문서에 설명 방법을 toocause 데이터 손실의 서비스에 주의 하 여 사용 해야 합니다.
> 
> 

## <a name="introduction"></a>소개
StartPartitionDataLossAsync()를 호출하여 서비스 패브릭 서비스 파티션에서의 데이터 손실을 호출할 수 있습니다.  이 api hello 오류 삽입 및 분석 서비스 tooperform hello 작업 toocause 데이터 손실 조건을 사용합니다.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Hello 오류 삽입 및 분석 서비스를 사용 하 여
hello 오류 삽입 및 분석 서비스는 현재 hello Api hello 차트 아래에 다음을 지원 합니다.  hello 차트의 오른쪽 hello hello 해당 PowerShell cmdlet을 보여 줍니다.  각각에 대 한 자세한 내용은 각 API에 대 한 toohello msdn 설명서를 참조 하십시오.

| C# API | PowerShell Cmdlet |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>명령 실행의 개념적 개요
hello hello를 시작 하는 비동기 모델 하나 api를 명령을이 문서에서는 다음 검사 hello의 진행 상황 터미널에 도달할 때까지 "GetProgress" API를 사용 하 여이 명령 tooas hello "Start" API를 참조 하는 오류 삽입 및 분석 서비스 사용 할 때까지 또는 상태를 취소합니다.
toostart 명령 hello 해당 API에 대 한 hello "시작" API를 호출 합니다.  이 API 오류 삽입 및 분석 서비스에서 hello 요청을 수락 하는 경우 hello에 반환 합니다.  그러나 명령이 얼마나 많이 실행되었는지, 심지어 시작되었는지 자체도 나타내지 않습니다.  명령의 순서 toocheck 진행 hello "GetProgress" toohello "시작" API 호출 이전에 해당 하는 API 호출 합니다.  hello "GetProgress" API의 상태 속성 내 hello 명령의 hello 현재 상태를 나타내는 개체를 반환 합니다.  명령을 다음이 실행될 때까지 무기한 실행됩니다.

1. 성공적으로 완료됩니다.  이 경우 "GetProgress"를 호출 하면 hello 진행률 개체의 상태가 완료 됩니다.
2. 오류가 발생합니다.  Hello 진행률 개체의 상태 오류가 발생 하기에 경우 "GetProgress" 호출 하는 경우
3. Hello를 통해 취소 [CancelTestCommandAsync] [ cancel] API 또는 [중지 ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet.  이 경우 "GetProgress"를 호출 하면 hello 진행률 개체의 상태가 취소 됨 또는 됩니다 ForceCancelled, 인수 toothat API에 따라 합니다.  Hello 설명서를 참조 하십시오 [CancelTestCommandAsync] [ cancel] 내용을 확인 합니다.

## <a name="details-of-running-a-command"></a>명령 실행의 세부 정보
순서 toostart 명령 예상 hello 인수를 갖는 hello 시작 API를 호출 합니다.  모든 Start API에는 operationId라는 GUID 인수가 있습니다.  해야의 추적할 있습니다 hello operationId 인수 사용 되기 때문이 명령의 tootrack 진행 합니다.  이 hello hello 명령의 순서 tootrack 진행 중 "GetProgress" API에 전달 되어야 합니다.  hello operationId 고유 해야 합니다.

Hello 진행 중 반환 될 때까지 루프에서 GetProgress API를 호출 해야 하는 hello hello 시작 API를 성공적으로 호출한 후 개체의 State 속성이 완료 됩니다.  모든 [FabricTransientException][fte] 및 OperationCanceledException이 다시 시도됩니다.
Hello 명령은 종료 상태 (Completed, Faulted, 또는 취소 됨)에 도달 하면 hello 반환 진행률 개체의 Result 속성에 추가 정보가 포함 됩니다.  Hello 상태를 완료 한 경우 Result.SelectedPartition.PartitionId 선택 된 hello 파티션 id를 포함 됩니다.  Result.Exception은 null이 됩니다.  Hello 상태가 Faulted 인 경우 hello 이유 hello 오류 삽입 및 분석 서비스 오류가 발생 한 hello 명령 Result.Exception 해야 합니다.  Result.SelectedPartition.PartitionId 선택 된 hello 파티션 id를 갖습니다.  경우에 따라 hello 명령 수 있습니다는 붙지 않으며 만큼 toochoose 파티션을 합니다.  이 경우 hello PartitionId 0이 됩니다.  Hello 상태가 취소 되 면 Result.Exception null이 됩니다.  Hello Faulted 대/소문자, 같은 Result.SelectedPartition.PartitionId 선택한 hello 파티션 id가 있지만 hello 명령 만큼 toodo를 따라서 붙지 않으며가 면 0이 됩니다.  아래 toohello 샘플도 참조 하십시오.

아래 샘플 코드 hello toostart 특정 파티션에 명령 toocause 데이터 손실에서 진행 한 다음 확인 되는 방법을 보여 줍니다.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

아래 hello 샘플 toouse PartitionSelector toochoose 지정된 된 서비스의 임의 파티션 hello 하는 방법을 보여 줍니다.

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a>기록 및 잘림
명령 종료 상태에 도달 하면 해당 메타 데이터 hello 오류 삽입에에서 남아 있으며 특정 시간 전에 됩니다에 대 한 분석 서비스 toosave 공백을 제거 합니다.  "GetProgress" 명령의 operationId hello를 사용 하 여 제거 된 후 호출 되 면 오류 코드의 KeyNotFound와 FabricException 반환 됩니다.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
