---
title: "Service Fabric 서비스에 대해 데이터 손실을 호출하는 방법 | Microsoft Docs"
description: "데이터 손실 API를 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="e70c0-103">서비스에 대해 데이터 손실을 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="e70c0-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="e70c0-104">이 문서에서는 서비스에서 데이터 손실을 유발하는 방법을 설명합니다. 이 문서는 주의해서 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="e70c0-105">소개</span><span class="sxs-lookup"><span data-stu-id="e70c0-105">Introduction</span></span>
<span data-ttu-id="e70c0-106">StartPartitionDataLossAsync()를 호출하여 서비스 패브릭 서비스 파티션에서의 데이터 손실을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="e70c0-107">이 API는 오류 주입 및 분석 서비스를 사용하여 데이터 손실 조건을 일으키는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="e70c0-108">오류 주입 및 분석 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="e70c0-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="e70c0-109">오류 주입 및 분석 서비스는 현재 아래 차트에 나오는 다음과 같은 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="e70c0-110">차트 오른쪽에는 각각에 해당하는 PowerShell cmdlet이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="e70c0-111">각 API에 대한 자세한 내용은 각 API에 대한 MSDN 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e70c0-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="e70c0-112">C# API</span><span class="sxs-lookup"><span data-stu-id="e70c0-112">C# API</span></span> | <span data-ttu-id="e70c0-113">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e70c0-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="e70c0-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="e70c0-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="e70c0-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="e70c0-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="e70c0-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="e70c0-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="e70c0-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="e70c0-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="e70c0-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="e70c0-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="e70c0-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="e70c0-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="e70c0-120">명령 실행의 개념적 개요</span><span class="sxs-lookup"><span data-stu-id="e70c0-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="e70c0-121">오류 주입 및 분석 서비스에서는 하나의 API(이 문서에서는 “Start" API)로 명령을 시작해서 최종 상태에 도달하거나 사용자가 취소할 때까지 "GetProgress" API를 통해 해당 명령의 진행 상황을 확인하는 비동기 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="e70c0-122">명령을 시작하려면 해당 API에 대해 "Start" API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="e70c0-123">이 API는 오류 주입 및 분석 서비스가 요청을 수락할 때 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="e70c0-124">그러나 명령이 얼마나 많이 실행되었는지, 심지어 시작되었는지 자체도 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="e70c0-125">명령의 진행 상태를 확인하려면 이전에 호출한 “Start” API에 해당하는 "GetProgress" API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="e70c0-126">"GetProgress" API는 State 속성 내에서 명령의 현재 상태를 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="e70c0-127">명령을 다음이 실행될 때까지 무기한 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="e70c0-128">성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-128">It completes successfully.</span></span>  <span data-ttu-id="e70c0-129">이 경우 "GetProgress"를 호출하면 진행 중인 개체의 State는 Completed가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="e70c0-130">오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-130">It encounters a fatal error.</span></span>  <span data-ttu-id="e70c0-131">이 경우 "GetProgress"를 호출하면 진행 중인 개체의 State는 Faulted가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="e70c0-132">[CancelTestCommandAsync][cancel] API 또는 [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet을 통해 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="e70c0-133">이 경우 "GetProgress"를 호출하면 진행 중인 개체의 State는 해당 API의 인수에 따라 Cancelled 또는 ForceCancelled가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="e70c0-134">자세한 내용은 [CancelTestCommandAsync][cancel]에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e70c0-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="e70c0-135">명령 실행의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e70c0-135">Details of Running a Command</span></span>
<span data-ttu-id="e70c0-136">명령을 시작하려면 예상되는 인수를 사용하여 Start API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="e70c0-137">모든 Start API에는 operationId라는 GUID 인수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="e70c0-138">operationId 인수는 이 명령의 진행률을 추적하는 데 사용되므로 추적해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="e70c0-139">그런 후 명령의 진행률을 추적하기 위해 "GetProgress" API에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="e70c0-140">operationId는 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-140">The operationId must be unique.</span></span>

<span data-ttu-id="e70c0-141">Start API를 성공적으로 호출하면 반환된 진행 중인 개체의 State 속성이 Completed가 될 때까지 GetProgress API가 반복해서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="e70c0-142">모든 [FabricTransientException][fte] 및 OperationCanceledException이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="e70c0-143">이 명령이 최종 상태(Completed, Faulted 또는 Cancelled)에 도달하면 반환된 진행 중인 개체의 Result 속성은 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="e70c0-144">상태가 Completed이면 Result.SelectedPartition.PartitionId는 선택한 파티션 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="e70c0-145">Result.Exception은 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-145">Result.Exception will be null.</span></span>  <span data-ttu-id="e70c0-146">상태가 Faulted인 경우 Result.Exception에는 오류 주입 및 분석 서비스 기능에서 해당 명령이 실패한 이유가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="e70c0-147">Result.SelectedPartition.PartitionId는 선택한 파티션 ID가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="e70c0-148">상황에 따라 파티션을 선택할 만큼 명령이 충분히 진행되지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="e70c0-149">그런 경우에 PartitionId는 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="e70c0-150">상태가 Cancelled인 경우 Result.Exception은 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="e70c0-151">Faulted 사례와 같이, Result.SelectedPartition.PartitionId는 선택된 파티션 ID를 가지고 있지만 명령이 그럴 수 있을 정도로 충분히 진행되지 않은 경우 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="e70c0-152">아래 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e70c0-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="e70c0-153">아래 샘플 코드에서는 명령을 시작한 후 진행 상태를 확인하고 특정 파티션에서 데이터 손실을 일으키는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

<span data-ttu-id="e70c0-154">아래 샘플은 PartitionSelector를 사용하여 지정된 서비스의 임의 파티션을 선택하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="e70c0-155">기록 및 잘림</span><span class="sxs-lookup"><span data-stu-id="e70c0-155">History and Truncation</span></span>
<span data-ttu-id="e70c0-156">명령이 최종 상태에 도달하면 해당 메타데이터는 특정 시간 동안 오류 주입 및 분석 서비스에 남아 있다가 공간 절약을 위해 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="e70c0-157">명령이 제거된 후 명령의 operationId를 사용하여 "GetProgress"가 호출되면 ErrorCode인 KeyNotFound를 사용하여 FabricException을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e70c0-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
