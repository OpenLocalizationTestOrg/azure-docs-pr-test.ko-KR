---
title: "Azure Functions 소비 및 App Service 계획 | Microsoft Docs"
description: "Azure Functions에서 이벤트 기반 워크로드의 수요를 충족하도록 규모를 조정하는 방식을 이해합니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a><span data-ttu-id="60938-104">Azure Functions 소비 및 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="60938-104">Azure Functions Consumption and App Service plans</span></span> 

## <a name="introduction"></a><span data-ttu-id="60938-105">소개</span><span class="sxs-lookup"><span data-stu-id="60938-105">Introduction</span></span>

<span data-ttu-id="60938-106">Azure Functions는 소비 계획 및 Azure App Service 계획 두 가지 모드로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-106">You can run Azure Functions in two different modes: Consumption plan and Azure App Service plan.</span></span> <span data-ttu-id="60938-107">소비 계획은 코드가 실행 중일 때 계산 용량을 자동으로 할당하고, 로드를 처리하는 데 필요한 만큼 확장한 다음 코드가 실행되지 않을 때 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-107">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="60938-108">따라서 유휴 VM에 대한 요금을 지불하고 용량을 미리 예약할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-108">So, you don't have to pay for idle VMs and don't have to reserve capacity in advance.</span></span> <span data-ttu-id="60938-109">이 문서에서는 소비 계획을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="60938-109">This article focuses on the Consumption plan.</span></span> <span data-ttu-id="60938-110">App Service 계획의 작동 원리에 대한 자세한 내용은 [Azure App Service 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-110">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="60938-111">Azure Functions에 익숙하지 않으면 [Azure Functions 개요](functions-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-111">If you aren't familiar with Azure Functions, see the [Azure Functions overview](functions-overview.md).</span></span>

<span data-ttu-id="60938-112">함수 앱을 만들 때 앱에 포함된 함수에 대한 호스팅 계획을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-112">When you create a function app, you must configure a hosting plan for functions that the app contains.</span></span> <span data-ttu-id="60938-113">두 모드에서 *Azure Functions 호스트* 인스턴스는 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-113">In either mode, an instance of the *Azure Functions host* executes the functions.</span></span> <span data-ttu-id="60938-114">계획 형식은 다음을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-114">The type of plan controls:</span></span>

* <span data-ttu-id="60938-115">호스트 인스턴스 확장 방법</span><span class="sxs-lookup"><span data-stu-id="60938-115">How host instances are scaled out.</span></span>
* <span data-ttu-id="60938-116">각 호스트에 사용할 수 있는 리소스</span><span class="sxs-lookup"><span data-stu-id="60938-116">The resources that are available to each host.</span></span>

<span data-ttu-id="60938-117">현재는 함수 앱을 만드는 중에 계획 형식을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-117">Currently, you must choose the plan type during the creation of the function app.</span></span> <span data-ttu-id="60938-118">나중에 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-118">You can't change it afterward.</span></span> 

<span data-ttu-id="60938-119">App Service 계획에서는 계층 간에 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-119">You can scale between tiers on the App Service plan.</span></span> <span data-ttu-id="60938-120">소비 계획에서 Azure Functions는 모든 리소스 할당을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-120">On the Consumption plan, Azure Functions automatically handles all resource allocation.</span></span>

## <a name="consumption-plan"></a><span data-ttu-id="60938-121">소비 계획</span><span class="sxs-lookup"><span data-stu-id="60938-121">Consumption plan</span></span>

<span data-ttu-id="60938-122">소비 계획을 사용하는 경우 Azure Functions 호스트의 인스턴스는 들어오는 이벤트의 수에 따라 동적으로 추가되고 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-122">When you're using a Consumption plan, instances of the Azure Functions host are dynamically added and removed based on the number of incoming events.</span></span> <span data-ttu-id="60938-123">이 계획은 자동으로 규모를 조정하며, 함수를 실행하는 경우에만 계산 리소스에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-123">This plan scales automatically, and you are charged for compute resources only when your functions are running.</span></span> <span data-ttu-id="60938-124">소비 계획에서 함수는 최대 10분 동안 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-124">On a Consumption plan, a function can run for a maximum of 10 minutes.</span></span> 

> [!NOTE]
> <span data-ttu-id="60938-125">소비 계획에서 함수에 대한 기본 시간 제한은 5분입니다.</span><span class="sxs-lookup"><span data-stu-id="60938-125">The default timeout for functions on a Consumption plan is 5 minutes.</span></span> <span data-ttu-id="60938-126">[host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)에서 `functionTimeout` 속성을 변경하여 함수 앱에 대한 이 값을 10분으로 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-126">The value can be increased to 10 minutes for the Function App by changing the property `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

<span data-ttu-id="60938-127">대금 청구는 실행 시간 및 사용되는 메모리를 기반으로 하며 함수 앱 내에서 모든 함수에 대해 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-127">Billing is based on execution time and memory used, and it's aggregated across all functions within a function app.</span></span> <span data-ttu-id="60938-128">자세한 내용은 [Azure Functions 가격 책정 페이지]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-128">For more information, see the [Azure Functions pricing page].</span></span>

<span data-ttu-id="60938-129">소비 계획은 기본값이며 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-129">The Consumption plan is the default and offers the following benefits:</span></span>
- <span data-ttu-id="60938-130">함수를 실행 중인 경우에만 지불</span><span class="sxs-lookup"><span data-stu-id="60938-130">Pay only when your functions are running.</span></span>
- <span data-ttu-id="60938-131">높은 부하 기간 동안에도 자동으로 규모 확장</span><span class="sxs-lookup"><span data-stu-id="60938-131">Scale out automatically, even during periods of high load.</span></span>

## <a name="app-service-plan"></a><span data-ttu-id="60938-132">앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="60938-132">App Service plan</span></span>

<span data-ttu-id="60938-133">App Service 계획에서 함수 앱은 Web Apps와 유사하게 기본, 표준, 프리미엄 SKU의 전용 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-133">In the App Service plan, your function apps run on dedicated VMs on Basic, Standard, and Premium SKUs, similar to Web Apps.</span></span> <span data-ttu-id="60938-134">전용 VM은 App Service 앱에 할당됩니다. 즉, 함수 호스트는 항상 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-134">Dedicated VMs are allocated to your App Service apps, which means the functions host is always running.</span></span>

<span data-ttu-id="60938-135">다음과 같은 경우에 App Service 계획을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-135">Consider an App Service plan in the following cases:</span></span>
- <span data-ttu-id="60938-136">이미 다른 App Service 인스턴스를 실행하고 있는 기존의 활용도가 낮은 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-136">You have existing, underutilized VMs that are already running other App Service instances.</span></span>
- <span data-ttu-id="60938-137">함수 앱을 계속해서 또는 거의 끊임없이 실행할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="60938-137">You expect your function apps to run continuously, or nearly continuously.</span></span>
- <span data-ttu-id="60938-138">소비 계획에서 제공하는 것보다 많은 CPU 또는 메모리 옵션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-138">You need more CPU or memory options than what is provided on the Consumption plan.</span></span>
- <span data-ttu-id="60938-139">소비 계획에 허용된 최대 실행 시간보다 오래 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-139">You need to run longer than the maximum execution time allowed on the Consumption plan.</span></span>

<span data-ttu-id="60938-140">VM은 런타임 및 메모리에서 비용을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-140">A VM decouples cost from both runtime and memory size.</span></span> <span data-ttu-id="60938-141">결과적으로, 할당하는 VM 인스턴스의 비용보다 더 지불하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-141">As a result, you won't pay more than the cost of the VM instance that you allocate.</span></span> <span data-ttu-id="60938-142">App Service 계획의 작동 원리에 대한 자세한 내용은 [Azure App Service 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-142">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="60938-143">App Service 계획을 사용하면 더 많은 VM 인스턴스를 추가하여 수동으로 확장하거나 자동 조정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-143">With an App Service plan, you can manually scale out by adding more VM instances, or you can enable autoscale.</span></span> <span data-ttu-id="60938-144">자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-144">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span> <span data-ttu-id="60938-145">다른 App Service 계획을 선택하여 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-145">You can also scale up by choosing a different App Service plan.</span></span> <span data-ttu-id="60938-146">자세한 내용은 [Azure에서 앱 확장](../app-service-web/web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-146">For more information, see [Scale up an app in Azure](../app-service-web/web-sites-scale.md).</span></span> <span data-ttu-id="60938-147">App Service 계획에서 JavaScript 함수를 실행하려는 경우 코어 수가 더 작은 계획을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-147">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan that has fewer cores.</span></span> <span data-ttu-id="60938-148">자세한 내용은 [함수에 대한 JavaScript 참조](functions-reference-node.md#choose-single-core-app-service-plans)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-148">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>  

<span data-ttu-id="60938-149"><!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### 무중단</span><span class="sxs-lookup"><span data-stu-id="60938-149"><!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On</span></span>

<span data-ttu-id="60938-150">App Service 계획에서 실행하는 경우 함수 앱이 올바르게 실행되도록 **무중단** 설정을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-150">If you run on an App Service plan, you should enable the **Always On** setting so that your function app  runs correctly.</span></span> <span data-ttu-id="60938-151">App Service 계획에서 함수 런타임은 비활성화되고 몇 분 후 유휴 상태가 되므로 HTTP 트리거만 함수를 "다시 시작"합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-151">On an App Service plan, the functions runtime will go idle after a few minutes of inactivity, so only HTTP triggers will "wake up" your functions.</span></span> <span data-ttu-id="60938-152">이는 WebJobs에서 무중단을 활성화해야 하는 방식과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-152">This is similar to how WebJobs must have Always On enabled.</span></span> 

<span data-ttu-id="60938-153">무중단은 App Service 계획에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-153">Always On is available only on an App Service plan.</span></span> <span data-ttu-id="60938-154">소비 계획에서 플랫폼은 함수 앱을 자동으로 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-154">On a Consumption plan, the platform activates function apps automatically.</span></span>

## <a name="storage-account-requirements"></a><span data-ttu-id="60938-155">저장소 계정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="60938-155">Storage account requirements</span></span>

<span data-ttu-id="60938-156">소비 계획 또는 App Service 계획에서 함수 앱에는 Azure Blob, Queue 및 Table storage를 지원하는 Azure Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-156">On either a Consumption plan or an App Service plan, a function app requires an Azure Storage account that supports Azure Blob, Queue, and Table storage.</span></span> <span data-ttu-id="60938-157">내부적으로 Azure Functions는 트리거 관리 및 함수 실행 로깅 등의 작업을 위해 Azure Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-157">Internally, Azure Functions uses Azure Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="60938-158">Blob 전용 저장소 계정(Premium Storage 포함) 및 영역 중복 저장소 복제가 사용되는 범용 저장소 계정 같은 일부 저장소 계정은 큐 및 테이블을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-158">Some storage accounts do not support queues and tables, such as blob-only storage accounts (including premium storage) and general-purpose storage accounts with zone-redundant storage replication.</span></span> <span data-ttu-id="60938-159">이러한 계정은 함수 앱을 만들 때 **저장소 계정** 블레이드에서 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-159">These accounts are filtered from the **Storage Account** blade when you're creating a function app.</span></span>

<span data-ttu-id="60938-160">저장소 계정 유형에 대해 자세히 알아보려면 [Azure Storage 서비스 소개](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-160">To learn more about storage account types, see [Introducing the Azure Storage services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span>

## <a name="how-the-consumption-plan-works"></a><span data-ttu-id="60938-161">소비 계획의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="60938-161">How the Consumption plan works</span></span>

<span data-ttu-id="60938-162">소비 계획은 해당 함수가 트리거되는 이벤트의 수에 따라 함수 호스트의 추가 인스턴스를 추가하여 CPU 및 메모리 리소스를 자동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-162">The Consumption plan automatically scales CPU and memory resources by adding additional instances of the Functions host, based on the number of events that its functions are triggered on.</span></span> <span data-ttu-id="60938-163">함수 호스트의 각 인스턴스는 1.5GB의 메모리로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-163">Each instance of the Functions host is limited to 1.5 GB of memory.</span></span>

<span data-ttu-id="60938-164">소비 호스팅 계획을 사용하는 경우 함수 코드 파일은 주 저장소 계정의 Azure Files 공유에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-164">When you use the Consumption hosting plan, function code files are stored on Azure Files shares on the main storage account.</span></span> <span data-ttu-id="60938-165">기본 저장소 계정을 삭제하면 이 콘텐츠는 삭제되고 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-165">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

> [!NOTE]
> <span data-ttu-id="60938-166">소비 계획에서 Blob 트리거를 사용하는 경우 함수 앱이 유휴 상태가 되면 새 Blob 처리에 하루 최대 10분이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-166">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.</span></span> <span data-ttu-id="60938-167">함수 앱이 실행된 후 Blob이 즉시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-167">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="60938-168">이 초기 지연을 방지하려면 다음 옵션 중 하나를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-168">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="60938-169">무중단이 사용되는 App Service 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-169">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="60938-170">Blob 이름을 포함하는 큐 메시지와 같은 다른 메커니즘을 사용하여 Blob 처리를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-170">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="60938-171">예를 들어 [Blob 입력 바인딩을 사용하여 큐 트리거](functions-bindings-storage-blob.md#input-sample)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60938-171">For an example, see [Queue trigger with blob input binding](functions-bindings-storage-blob.md#input-sample).</span></span>

### <a name="runtime-scaling"></a><span data-ttu-id="60938-172">런타임 크기 조정</span><span class="sxs-lookup"><span data-stu-id="60938-172">Runtime scaling</span></span>

<span data-ttu-id="60938-173">Azure Functions는 *크기 조정 컨트롤러*라는 구성 요소를 사용하여 이벤트의 비율을 모니터링하고 규모를 확장하거나 축소할 것인지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-173">Azure Functions uses a component called the *scale controller* to monitor the rate of events and determine whether to scale out or scale down.</span></span> <span data-ttu-id="60938-174">크기 조정 컨트롤러는 각 트리거 유형에 대해 추론을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-174">The scale controller uses heuristics for each trigger type.</span></span> <span data-ttu-id="60938-175">예를 들어 Azure Queue Storage 트리거를 사용하는 경우 큐 길이 및 가장 오래된 큐 메시지의 기간에 따라 트리거가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-175">For example, when you're using an Azure Queue storage trigger, it scales based on the queue length and the age of the oldest queue message.</span></span>

<span data-ttu-id="60938-176">크기 조정 단위는 함수 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="60938-176">The unit of scale is the function app.</span></span> <span data-ttu-id="60938-177">함수 앱을 확장하는 경우 Azure Functions 호스트의 여러 인스턴스를 실행하기 위해 더 많은 리소스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-177">When the function app is scaled out, more resources are allocated to run multiple instances of the Azure Functions host.</span></span> <span data-ttu-id="60938-178">반대로, 계산 수요가 감소하면 크기 조정 컨트롤러에서 함수 호스트 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="60938-178">Conversely, as compute demand is reduced, the scale controller removes function host instances.</span></span> <span data-ttu-id="60938-179">함수 앱 내에서 실행 중인 함수가 없으면 인스턴스 수가 결국 0으로 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-179">The number of instances is eventually scaled down to zero when no functions are running within a function app.</span></span>

![이벤트를 모니터링하고 인스턴스를 만드는 크기 조정 컨트롤러](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a><span data-ttu-id="60938-181">청구 모델</span><span class="sxs-lookup"><span data-stu-id="60938-181">Billing model</span></span>

<span data-ttu-id="60938-182">소비 계획의 요금 청구는 [Azure Functions 가격 책정 페이지]에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60938-182">Billing for the Consumption plan is described in detail on the [Azure Functions pricing page].</span></span> <span data-ttu-id="60938-183">사용량은 함수 앱 수준에서 집계되며 함수 코드가 실행될 때만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-183">Usage is aggregated at the function app level and counts only the time that function code is running.</span></span> <span data-ttu-id="60938-184">다음은 요금 청구 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="60938-184">The following are units for billing:</span></span> 
* <span data-ttu-id="60938-185">**기가바이트-초 단위의 리소스 소비(GB-s)**.</span><span class="sxs-lookup"><span data-stu-id="60938-185">**Resource consumption in gigabyte-seconds (GB-s)**.</span></span> <span data-ttu-id="60938-186">함수 앱 내 모든 함수의 메모리 크기와 실행 시간 조합으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-186">Computed as a combination of memory size and execution time for all functions within a function app.</span></span> 
* <span data-ttu-id="60938-187">**실행 횟수**.</span><span class="sxs-lookup"><span data-stu-id="60938-187">**Executions**.</span></span> <span data-ttu-id="60938-188">바인딩으로 트리거된 이벤트에 대한 응답으로 함수가 실행될 때마다 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="60938-188">Counted each time a function is executed in response to an event, triggered by a binding.</span></span>

[Azure Functions 가격 책정 페이지]: https://azure.microsoft.com/pricing/details/functions
