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
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="a9efa-103">어떻게 tooInvoke 서비스에서 데이터 손실</span><span class="sxs-lookup"><span data-stu-id="a9efa-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="a9efa-104">이 문서에 설명 방법을 toocause 데이터 손실의 서비스에 주의 하 여 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a9efa-105">소개</span><span class="sxs-lookup"><span data-stu-id="a9efa-105">Introduction</span></span>
<span data-ttu-id="a9efa-106">StartPartitionDataLossAsync()를 호출하여 서비스 패브릭 서비스 파티션에서의 데이터 손실을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="a9efa-107">이 api hello 오류 삽입 및 분석 서비스 tooperform hello 작업 toocause 데이터 손실 조건을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="a9efa-108">Hello 오류 삽입 및 분석 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a9efa-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="a9efa-109">hello 오류 삽입 및 분석 서비스는 현재 hello Api hello 차트 아래에 다음을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="a9efa-110">hello 차트의 오른쪽 hello hello 해당 PowerShell cmdlet을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="a9efa-111">각각에 대 한 자세한 내용은 각 API에 대 한 toohello msdn 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a9efa-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="a9efa-112">C# API</span><span class="sxs-lookup"><span data-stu-id="a9efa-112">C# API</span></span> | <span data-ttu-id="a9efa-113">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a9efa-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="a9efa-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="a9efa-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="a9efa-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="a9efa-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="a9efa-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="a9efa-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="a9efa-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="a9efa-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="a9efa-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="a9efa-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="a9efa-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="a9efa-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="a9efa-120">명령 실행의 개념적 개요</span><span class="sxs-lookup"><span data-stu-id="a9efa-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="a9efa-121">hello hello를 시작 하는 비동기 모델 하나 api를 명령을이 문서에서는 다음 검사 hello의 진행 상황 터미널에 도달할 때까지 "GetProgress" API를 사용 하 여이 명령 tooas hello "Start" API를 참조 하는 오류 삽입 및 분석 서비스 사용 할 때까지 또는 상태를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="a9efa-122">toostart 명령 hello 해당 API에 대 한 hello "시작" API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="a9efa-123">이 API 오류 삽입 및 분석 서비스에서 hello 요청을 수락 하는 경우 hello에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="a9efa-124">그러나 명령이 얼마나 많이 실행되었는지, 심지어 시작되었는지 자체도 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="a9efa-125">명령의 순서 toocheck 진행 hello "GetProgress" toohello "시작" API 호출 이전에 해당 하는 API 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="a9efa-126">hello "GetProgress" API의 상태 속성 내 hello 명령의 hello 현재 상태를 나타내는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="a9efa-127">명령을 다음이 실행될 때까지 무기한 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="a9efa-128">성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-128">It completes successfully.</span></span>  <span data-ttu-id="a9efa-129">이 경우 "GetProgress"를 호출 하면 hello 진행률 개체의 상태가 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="a9efa-130">오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-130">It encounters a fatal error.</span></span>  <span data-ttu-id="a9efa-131">Hello 진행률 개체의 상태 오류가 발생 하기에 경우 "GetProgress" 호출 하는 경우</span><span class="sxs-lookup"><span data-stu-id="a9efa-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="a9efa-132">Hello를 통해 취소 [CancelTestCommandAsync] [ cancel] API 또는 [중지 ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9efa-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="a9efa-133">이 경우 "GetProgress"를 호출 하면 hello 진행률 개체의 상태가 취소 됨 또는 됩니다 ForceCancelled, 인수 toothat API에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="a9efa-134">Hello 설명서를 참조 하십시오 [CancelTestCommandAsync] [ cancel] 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="a9efa-135">명령 실행의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a9efa-135">Details of Running a Command</span></span>
<span data-ttu-id="a9efa-136">순서 toostart 명령 예상 hello 인수를 갖는 hello 시작 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="a9efa-137">모든 Start API에는 operationId라는 GUID 인수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="a9efa-138">해야의 추적할 있습니다 hello operationId 인수 사용 되기 때문이 명령의 tootrack 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="a9efa-139">이 hello hello 명령의 순서 tootrack 진행 중 "GetProgress" API에 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="a9efa-140">hello operationId 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-140">hello operationId must be unique.</span></span>

<span data-ttu-id="a9efa-141">Hello 진행 중 반환 될 때까지 루프에서 GetProgress API를 호출 해야 하는 hello hello 시작 API를 성공적으로 호출한 후 개체의 State 속성이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="a9efa-142">모든 [FabricTransientException][fte] 및 OperationCanceledException이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="a9efa-143">Hello 명령은 종료 상태 (Completed, Faulted, 또는 취소 됨)에 도달 하면 hello 반환 진행률 개체의 Result 속성에 추가 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="a9efa-144">Hello 상태를 완료 한 경우 Result.SelectedPartition.PartitionId 선택 된 hello 파티션 id를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="a9efa-145">Result.Exception은 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-145">Result.Exception will be null.</span></span>  <span data-ttu-id="a9efa-146">Hello 상태가 Faulted 인 경우 hello 이유 hello 오류 삽입 및 분석 서비스 오류가 발생 한 hello 명령 Result.Exception 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="a9efa-147">Result.SelectedPartition.PartitionId 선택 된 hello 파티션 id를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="a9efa-148">경우에 따라 hello 명령 수 있습니다는 붙지 않으며 만큼 toochoose 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="a9efa-149">이 경우 hello PartitionId 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="a9efa-150">Hello 상태가 취소 되 면 Result.Exception null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="a9efa-151">Hello Faulted 대/소문자, 같은 Result.SelectedPartition.PartitionId 선택한 hello 파티션 id가 있지만 hello 명령 만큼 toodo를 따라서 붙지 않으며가 면 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="a9efa-152">아래 toohello 샘플도 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a9efa-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="a9efa-153">아래 샘플 코드 hello toostart 특정 파티션에 명령 toocause 데이터 손실에서 진행 한 다음 확인 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

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

<span data-ttu-id="a9efa-154">아래 hello 샘플 toouse PartitionSelector toochoose 지정된 된 서비스의 임의 파티션 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="a9efa-155">기록 및 잘림</span><span class="sxs-lookup"><span data-stu-id="a9efa-155">History and Truncation</span></span>
<span data-ttu-id="a9efa-156">명령 종료 상태에 도달 하면 해당 메타 데이터 hello 오류 삽입에에서 남아 있으며 특정 시간 전에 됩니다에 대 한 분석 서비스 toosave 공백을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="a9efa-157">"GetProgress" 명령의 operationId hello를 사용 하 여 제거 된 후 호출 되 면 오류 코드의 KeyNotFound와 FabricException 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9efa-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
