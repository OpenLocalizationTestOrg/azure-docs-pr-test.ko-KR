---
title: "Azure Functions에 대한 모범 사례 | Microsoft Docs"
description: "Azure Functions에 대한 모범 사례 및 패턴에 알아봅니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 패턴, 모범 사례, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="cb6f7-104">Azure Functions의 성능 및 안정성 최적화</span><span class="sxs-lookup"><span data-stu-id="cb6f7-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="cb6f7-105">이 문서에서는 함수 앱의 성능 및 안정성을 개선하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="cb6f7-106">장기 실행 함수 방지</span><span class="sxs-lookup"><span data-stu-id="cb6f7-106">Avoid long running functions</span></span>

<span data-ttu-id="cb6f7-107">큰 장기 실행 함수는 예기치 않은 시간 초과 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="cb6f7-108">함수는 많은 Node.js 종속성으로 인해 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="cb6f7-109">또한 종속성을 가져올 때 로드 시간이 증가하여 예기치 않은 시간 초과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="cb6f7-110">종속성은 명시적 및 암시적으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="cb6f7-111">코드를 통해 로드되는 단일 모듈은 자체 추가 모듈을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="cb6f7-112">큰 함수를 더 작은 함수 집합으로 리팩터링할 때마다 함께 작동하고 빠른 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="cb6f7-113">예를 들어 webhook 또는 HTTP 트리거 함수는 특정 시간 제한 내의 승인 응답이 필요할 수 있습니다. webhook의 경우 즉각적인 응답을 요구하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="cb6f7-114">HTTP 트리거 페이로드를 큐 트리거 함수에 의해 처리되도록 큐에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="cb6f7-115">이 방법은 실제 작업을 연기하고 즉각적인 응답을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="cb6f7-116">함수 통신 교차</span><span class="sxs-lookup"><span data-stu-id="cb6f7-116">Cross function communication</span></span>

<span data-ttu-id="cb6f7-117">여러 기능을 통합할 때 함수 통신 교차를 위해 저장소 큐를 사용하는 것이 일반적으로 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="cb6f7-118">주요 이유는 저장소 큐는 더 저렴하고 프로비전하는 것이 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="cb6f7-119">저장소 큐에 있는 개별 메시지 크기는 64KB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="cb6f7-120">함수 간에 더 큰 메시지를 전달해야 하는 경우 Azure Service Bus 큐를 사용하여 최대 256KB의 메시지 크기를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="cb6f7-121">Service Bus 토픽은 메시지를 처리하기 전에 필터링해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="cb6f7-122">이벤트 허브는 고용량 통신을 지원하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="cb6f7-123">상태 비저장 함수 작성</span><span class="sxs-lookup"><span data-stu-id="cb6f7-123">Write functions to be stateless</span></span> 

<span data-ttu-id="cb6f7-124">함수는 가능하면 상태 비저장이며 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="cb6f7-125">필요한 모든 상태 정보를 사용자 데이터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-125">Associate any required state information with your data.</span></span> <span data-ttu-id="cb6f7-126">예를 들어 처리할 주문에 연결된 `state` 멤버가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="cb6f7-127">함수는 주문을 해당 상태에 따라 처리하며 함수 자체는 비저장 상태로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="cb6f7-128">Idempotent 함수는 특히 타이머 트리거 사용이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="cb6f7-129">예를 들어 반드시 하루에 한 번 실행해야 하는 내용이 있는 경우 하루 동안 언제든지 같은 결과로 실행할 수 있도록 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="cb6f7-130">함수는 특정 날짜에 대한 작업이 없는 경우 종료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="cb6f7-131">또한 이전 실행이 완료되지 못한 경우 다음 실행은 중단되었던 부분으로 돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="cb6f7-132">방어적 함수 작성</span><span class="sxs-lookup"><span data-stu-id="cb6f7-132">Write defensive functions</span></span>

<span data-ttu-id="cb6f7-133">함수에는 언제든지 예외가 발생할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="cb6f7-134">다음 실행 동안 이전 실패 지점에서 계속할 수 있는 기능을 넣어 함수를 설계합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="cb6f7-135">다음과 같은 작업이 필요한 시나리오를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="cb6f7-136">Db의 10,000개 행에 대해 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="cb6f7-137">앞으로 처리할 각 행에 대한 큐 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="cb6f7-138">시스템의 복잡성에 따라 잘못 작동되는 관련된 다운스트림 서비스, 네트워킹 작동 중단 또는 할당량 제한 초과 등이 있을 수 있습니다. 이러한 항목은 모두 언제든지 함수에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="cb6f7-139">함수가 이에 대비할 수 있도록 설계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="cb6f7-140">이러한 항목 중 5,000개를 처리를 위해 큐에 삽입한 후 오류가 발생한다면 코드는 어떻게 반응할까요?</span><span class="sxs-lookup"><span data-stu-id="cb6f7-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="cb6f7-141">사용자가 완료한 집합에서 항목을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="cb6f7-142">다른 방법으로 다음 번에 해당 항목을 삽입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="cb6f7-143">이는 작업 흐름에 심각한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="cb6f7-144">큐 항목을 이미 처리한 경우 함수는 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="cb6f7-145">Azure Functions 플랫폼에서 사용하는 구성 요소를 위해 이미 제공된 방어 수단을 활용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="cb6f7-146">예를 들어 [Azure Storage 큐 트리거](functions-bindings-storage-queue.md#trigger)를 위한 설명서에서 **포이즌 큐 메시지 처리**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="cb6f7-147">동일한 함수 앱에서 테스트와 프로덕션 코드의 혼합 금지</span><span class="sxs-lookup"><span data-stu-id="cb6f7-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="cb6f7-148">함수 앱 공유 리소스 내에서 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-148">Functions within a function app share resources.</span></span> <span data-ttu-id="cb6f7-149">예를 들어 메모리는 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-149">For example, memory is shared.</span></span> <span data-ttu-id="cb6f7-150">프로덕션 환경에서 함수 앱을 사용하는 경우 테스트 관련 함수 및 리소스를 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="cb6f7-151">프로덕션 코드를 실행하는 동안 예기치 않은 오버 헤드가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="cb6f7-152">프로덕션 함수 앱에서 로드하는 것에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="cb6f7-153">메모리는 앱에서 각 함수가 사용하는 것의 평균으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="cb6f7-154">여러.Net 함수에서 참조되는 공유 어셈블리가 있는 경우 일반적인 공유 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="cb6f7-155">다음 예제와 비슷한 문을 사용하여 어셈블리를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="cb6f7-156">그렇지 않으면 함수 간 다르게 작동하는 동일한 바이너리의 여러 테스트 버전이 실수로 배포되기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="cb6f7-157">프로덕션 코드에 너무 많은 로깅을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="cb6f7-158">부정적인 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="cb6f7-159">비동기 코드는 사용, 호출 차단 방지</span><span class="sxs-lookup"><span data-stu-id="cb6f7-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="cb6f7-160">비동기 프로그래밍은 권장되는 최상의 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="cb6f7-161">그러나 `Task` 인스턴스의 `Result` 속성을 참조하거나 `Wait` 메서드를 호출하는 것은 항상 피하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="cb6f7-162">이 방법은 스레드를 소진시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="cb6f7-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb6f7-163">Next steps</span></span>
<span data-ttu-id="cb6f7-164">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-164">For more information, see the following resources:</span></span>

<span data-ttu-id="cb6f7-165">Azure Functions에서는 Azure App Service를 사용하므로 App Service 지침도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6f7-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="cb6f7-166">패턴 및 사례 HTTP 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="cb6f7-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

