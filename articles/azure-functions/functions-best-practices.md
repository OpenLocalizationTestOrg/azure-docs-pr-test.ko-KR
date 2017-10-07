---
title: "Azure 기능에 대 한 aaaBest 사례 | Microsoft Docs"
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
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="2d470-104">함수를 Azure의 hello 성능 및 안정성 최적화</span><span class="sxs-lookup"><span data-stu-id="2d470-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="2d470-105">이 문서에서는 지침 tooimprove hello 성능 및 안정성 기능 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="2d470-106">장기 실행 함수 방지</span><span class="sxs-lookup"><span data-stu-id="2d470-106">Avoid long running functions</span></span>

<span data-ttu-id="2d470-107">큰 장기 실행 함수는 예기치 않은 시간 초과 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="2d470-108">함수는 toomany Node.js 종속성 인해 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="2d470-109">또한 종속성을 가져올 때 로드 시간이 증가하여 예기치 않은 시간 초과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="2d470-110">종속성은 명시적 및 암시적으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="2d470-111">코드를 통해 로드되는 단일 모듈은 자체 추가 모듈을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="2d470-112">큰 함수를 더 작은 함수 집합으로 리팩터링할 때마다 함께 작동하고 빠른 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="2d470-113">예를 들어 webhook 또는 HTTP 트리거 함수 해야 된 승인 응답 시간 제한 내; 것에 대 한 webhook toorequire 즉시 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="2d470-114">큐 트리거 함수에 의해 처리 큐 toobe에 hello HTTP 트리거 페이로드를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="2d470-115">이 방법은 toodefer hello 실제 작업을 허용 하 고 즉각적인 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="2d470-116">함수 통신 교차</span><span class="sxs-lookup"><span data-stu-id="2d470-116">Cross function communication</span></span>

<span data-ttu-id="2d470-117">여러 기능을 통합할 때 일반적으로 모범 사례 toouse 저장소 큐에 대 한 함수 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="2d470-118">hello 주요 이유는 저장소 큐는 비용이 저렴 하 고 훨씬 쉽게 tooprovision 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="2d470-119">저장소 큐에 있는 개별 메시지 크기 too64 제한 됩니다 (kb)입니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="2d470-120">함수 사이 toopass 보다 큰 메시지가 필요한 경우 Azure 서비스 버스 큐 too256 (kb) 사용 하는 toosupport 메시지 크기를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="2d470-121">Service Bus 토픽은 메시지를 처리하기 전에 필터링해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="2d470-122">이벤트 허브는 유용한 toosupport 고용량 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="2d470-123">상태 비저장 함수 toobe 작성</span><span class="sxs-lookup"><span data-stu-id="2d470-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="2d470-124">함수는 가능하면 상태 비저장이며 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="2d470-125">필요한 모든 상태 정보를 사용자 데이터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-125">Associate any required state information with your data.</span></span> <span data-ttu-id="2d470-126">예를 들어 처리할 주문에 연결된 `state` 멤버가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="2d470-127">함수는 hello 함수 자체는 상태 비저장 상태로 유지 하면서 해당 상태에 따라 주문을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="2d470-128">Idempotent 함수는 특히 타이머 트리거 사용이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="2d470-129">예를 들어 절대적으로 하루에 한 번 실행 해야 하는 문제가 있다면 작성 실행할 수 있도록 hello 하루 동안 언제 든 지 hello로 동일한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="2d470-130">특정 날에 대 한 작업이 없는 경우 hello 함수 나갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="2d470-131">또한 이전 실행 toocomplete 실패 한 경우 다음 실행 하는 hello 중단 된 위치를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="2d470-132">방어적 함수 작성</span><span class="sxs-lookup"><span data-stu-id="2d470-132">Write defensive functions</span></span>

<span data-ttu-id="2d470-133">함수에는 언제든지 예외가 발생할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="2d470-134">Hello 다음 실행 하는 동안 hello 기능 toocontinue 이전 장애 지점에서 사용 하 여 함수를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="2d470-135">Hello 동작을 수행 해야 하는 시나리오를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="2d470-136">Db의 10,000개 행에 대해 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="2d470-137">각 hello 줄 아래로 더 행 tooprocess 이러한에 대 한 큐 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="2d470-138">시스템의 복잡성에 따라 잘못 작동되는 관련된 다운스트림 서비스, 네트워킹 작동 중단 또는 할당량 제한 초과 등이 있을 수 있습니다. 이러한 항목은 모두 언제든지 함수에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="2d470-139">것에 대비 하 여 함수 toobe toodesign 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="2d470-140">이러한 항목 중 5,000개를 처리를 위해 큐에 삽입한 후 오류가 발생한다면 코드는 어떻게 반응할까요?</span><span class="sxs-lookup"><span data-stu-id="2d470-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="2d470-141">사용자가 완료한 집합에서 항목을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="2d470-142">다른 방법으로 다음 번에 해당 항목을 삽입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="2d470-143">이는 작업 흐름에 심각한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="2d470-144">큐 항목을 이미 처리 된 함수 toobe no-op를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="2d470-145">Hello 함수 Azure 플랫폼에서 사용 하는 구성 요소에 대해 이미 제공 방어 수단을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="2d470-146">예를 들어 참조 **포이즌 큐 메시지를 처리할** hello 설명서에서 [Azure 저장소 큐 트리거합니다](functions-bindings-storage-queue.md#trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="2d470-147">하지 혼합 테스트 및 프로덕션 코드 hello에 동일 함수 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2d470-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="2d470-148">함수 앱 공유 리소스 내에서 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-148">Functions within a function app share resources.</span></span> <span data-ttu-id="2d470-149">예를 들어 메모리는 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-149">For example, memory is shared.</span></span> <span data-ttu-id="2d470-150">테스트 관련 기능 및 리소스 tooit 함수 응용 프로그램을 프로덕션 환경에서 사용 하는 경우 추가 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2d470-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="2d470-151">프로덕션 코드를 실행하는 동안 예기치 않은 오버 헤드가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="2d470-152">프로덕션 함수 앱에서 로드하는 것에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="2d470-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="2d470-153">각 함수 hello 앱에 메모리는 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="2d470-154">여러.Net 함수에서 참조되는 공유 어셈블리가 있는 경우 일반적인 공유 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="2d470-155">다음 예에서는 문 비슷한 toohello 사용 하 여 hello 어셈블리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="2d470-156">그렇지 않으면 쉽습니다 tooaccidentally 사이 다르게 동작 하는 같은 이진 함수 hello의 여러 테스트 버전을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="2d470-157">프로덕션 코드에 너무 많은 로깅을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2d470-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="2d470-158">부정적인 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="2d470-159">비동기 코드는 사용, 호출 차단 방지</span><span class="sxs-lookup"><span data-stu-id="2d470-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="2d470-160">비동기 프로그래밍은 권장되는 최상의 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="2d470-161">그러나 항상 참조 하지 않을 hello `Result` 속성 또는 호출 `Wait` 에서 메서드는 `Task` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2d470-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="2d470-162">이 방법은 toothread 소모가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="2d470-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d470-163">Next steps</span></span>
<span data-ttu-id="2d470-164">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="2d470-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="2d470-165">Azure Functions에서는 Azure App Service를 사용하므로 App Service 지침도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d470-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="2d470-166">패턴 및 사례 HTTP 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="2d470-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

