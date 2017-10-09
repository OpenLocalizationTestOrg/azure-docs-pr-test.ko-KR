---
title: "aaaScheduler 높은 가용성 및 안정성"
description: "스케줄러 고가용성 및 안정성"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="26773-103">스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="26773-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="26773-104">Azure 스케줄러 고가용성 </span><span class="sxs-lookup"><span data-stu-id="26773-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="26773-105">핵심 Azure 플랫폼 서비스인 Azure 스케줄러는 가용성이 높으며 지역 중복 서비스 배포와 지리적 지역 작업 복제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="26773-106">지리적 중복 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="26773-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="26773-107">Azure 스케줄러는 hello에에서 있는 Azure 오늘날 거의 모든 지역에서 UI 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-107">Azure Scheduler is available via hello UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="26773-108">hello Azure 스케줄러에서 제공 되는 지역 목록은 다음과 같이 [여기에 나열 된](https://azure.microsoft.com/regions/#services)합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-108">hello list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="26773-109">호스트 된 영역에 데이터 센터를 사용할 수 없게 렌더링 하는 경우 다른 데이터 센터에서 hello 서비스를 사용할 수 있도록 Azure 스케줄러의 hello 장애 조치 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-109">If a data center in a hosted region is rendered unavailable, hello failover capabilities of Azure Scheduler are such that hello service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="26773-110">지리적 지역 작업 복제</span><span class="sxs-lookup"><span data-stu-id="26773-110">Geo-regional job replication</span></span>
<span data-ttu-id="26773-111">뿐만 아니라는 hello Azure 스케줄러 프런트 엔드 아니라 자체적인 관리 요청에 사용할 수 있는 이기도 지리적으로 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-111">Not only is hello Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="26773-112">지역에서 가동 중단 되는 경우 Azure 스케줄러는 장애 조치 하 고 해당 hello 작업 hello 쌍 이룬된 지역에 있는 다른 데이터 센터에서 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that hello job is run from another data center in hello paired geographic region.</span></span>

<span data-ttu-id="26773-113">예: 미국 중남부에서 만든 작업을 Azure 스케줄러가 미국 중북부에서 자동으로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="26773-114">미국 중남부에 오류가 있을 때 Azure 스케줄러 미국 중 북부에서에서 해당 hello 작업 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-114">When there’s a failure in South Central US, Azure Scheduler ensures that hello job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="26773-115">결과적으로, Azure 스케줄러 내의 데이터가 유지 되며 Azure 오류가 발생 한 경우 동일한 보다 광범위 한 지리적 지역 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-115">As a result, Azure Scheduler ensures that your data stays within hello same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="26773-116">결과적으로, 작업 뿐 tooadd 높은 가용성을 복제할 필요가 – Azure 스케줄러는 자동으로 작업에 대 한 고가용성 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-116">As a result, you need not duplicate your job just tooadd high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="26773-117">Azure 스케줄러 안정성</span><span class="sxs-lookup"><span data-stu-id="26773-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="26773-118">Azure 스케줄러 자체 고가용성을 보장 하 고는 다른 방식을 toouser 만든 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-118">Azure Scheduler guarantees its own high-availability and takes a different approach toouser-created jobs.</span></span> <span data-ttu-id="26773-119">예를 들어, 사용자 작업에서 사용 불가능한 HTTP 끝점을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="26773-120">Azure 스케줄러 그럼에도 불구 하 고 시도 tooexecute 작업이 성공적으로 오류로 대체 옵션 toodeal 제공 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-120">Azure Scheduler nonetheless tries tooexecute your job successfully, by giving you alternative options toodeal with failure.</span></span> <span data-ttu-id="26773-121">Azure 스케줄러는 두 가지 방법으로 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="26773-122">“retryPolicy”를 통해 구성 가능한 재시도 정책</span><span class="sxs-lookup"><span data-stu-id="26773-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="26773-123">Azure 스케줄러는 다시 시도 정책을 tooconfigure가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-123">Azure Scheduler allows you tooconfigure a retry policy.</span></span> <span data-ttu-id="26773-124">기본적으로 작업이 실패 하면 스케줄러 시도 hello 작업 4 번 더 30 초 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="26773-124">By default, if a job fails, Scheduler tries hello job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="26773-125">이 다시 시도 정책 toobe 보다 적극적으로 (예를 들어 10 번 30 초 간격)를 다시 구성할 수 있습니다 (예: 두 일 간격입니다.) 낮출 또는</span><span class="sxs-lookup"><span data-stu-id="26773-125">You may re-configure this retry policy toobe more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="26773-126">예를 들어, 매주 한 번 실행되고 HTTP 끝점을 호출하는 작업을 만든 경우 이것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="26773-127">작업 실행 하는 경우 몇 시간 동안 hello HTTP 끝점이 다운 된 경우 싶지 않은 toowait 1 주일을 더 hello 작업 toorun 다시 이후 hello 기본 재시도 정책을 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-127">If hello HTTP endpoint is down for a few hours when your job runs, you may not want toowait one more week for hello job toorun again since even hello default retry policy will fail.</span></span> <span data-ttu-id="26773-128">이 경우 다시 구성할 수 있습니다 hello 표준 재시도 정책 tooretry 3 시간 마다 예를 들어 30 초가 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-128">In such cases, you may reconfigure hello standard retry policy tooretry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="26773-129">재시도 정책을 tooconfigure 너무 참조 하는 방법 toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy)합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-129">toolearn how tooconfigure a retry policy, refer too[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="26773-130">“errorAction”을 통한 대체 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="26773-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="26773-131">Azure 스케줄러 작업용 대상 끝점 hello 계속 연결할 수 없으면 Azure 스케줄러 대신 toohello 대체 오류 처리 끝점은 다시 시도 정책을 따른 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-131">If hello target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back toohello alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="26773-132">대체 오류 처리 끝점을 구성한 경우 Azure 스케줄러가 이를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="26773-133">대체 끝점으로 사용자 고유의 작업은 실패의 hello 면에서 항상 사용 가능한입니다.</span><span class="sxs-lookup"><span data-stu-id="26773-133">With an alternate endpoint, your own jobs are highly available in hello face of failure.</span></span>

<span data-ttu-id="26773-134">예를 들어, 아래 hello 다이어그램에서 Azure 스케줄러는 다시 시도 정책 toohit 뉴욕 웹 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-134">As an example, in hello diagram below, Azure Scheduler follows its retry policy toohit a New York web service.</span></span> <span data-ttu-id="26773-135">Hello 실패 다시 시도 시간 후 대체 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-135">After hello retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="26773-136">그런 다음 끝점 하 고 시작 동일 hello로 toohello 대체 하는 요청을 다시 시도 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="26773-136">It then goes ahead and starts making requests toohello alternate with hello same retry policy.</span></span>

![][2]

<span data-ttu-id="26773-137">같은 다시 시도 정책을 hello 참고 tooboth hello 원래 작업과 대체 오류 동작 hello 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26773-137">Note that hello same retry policy applies tooboth hello original action and hello alternate error action.</span></span> <span data-ttu-id="26773-138">도 가능한 toohave hello 대체 오류 동작의 동작 유형을 수 hello 기본 작업의 동작 유형과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="26773-138">It’s also possible toohave hello alternate error action’s action type be different from hello main action’s action type.</span></span> <span data-ttu-id="26773-139">예를 들어 hello 기본 동작과 수 HTTP 끝점을 호출 하는 동안 저장소 큐, 서비스 버스 큐 또는 오류 로깅을 수행 하는 서비스 버스 항목 동작이 hello 오류 동작 수 대신 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26773-139">For example, while hello main action may be invoking an HTTP endpoint, hello error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="26773-140">대체 끝점을 tooconfigure 너무 참조 하는 방법 toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction)합니다.</span><span class="sxs-lookup"><span data-stu-id="26773-140">toolearn how tooconfigure an alternate endpoint, refer too[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="26773-141">참고 항목</span><span class="sxs-lookup"><span data-stu-id="26773-141">See Also</span></span>
 [<span data-ttu-id="26773-142">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="26773-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="26773-143">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="26773-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="26773-144">Hello Azure 포털에서에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="26773-144">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="26773-145">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="26773-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="26773-146">일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이</span><span class="sxs-lookup"><span data-stu-id="26773-146">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="26773-147">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="26773-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="26773-148">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="26773-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="26773-149">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="26773-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="26773-150">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="26773-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
