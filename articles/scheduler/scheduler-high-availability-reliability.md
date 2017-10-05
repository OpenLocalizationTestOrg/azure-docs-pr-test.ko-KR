---
title: "스케줄러 고가용성 및 안정성"
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
ms.openlocfilehash: 7e7fe49de7814b6058468d630f8638720e5864f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="7a98b-103">스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="7a98b-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="7a98b-104">Azure 스케줄러 고가용성 </span><span class="sxs-lookup"><span data-stu-id="7a98b-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="7a98b-105">핵심 Azure 플랫폼 서비스인 Azure 스케줄러는 가용성이 높으며 지역 중복 서비스 배포와 지리적 지역 작업 복제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="7a98b-106">지리적 중복 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="7a98b-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="7a98b-107">Azure 스케줄러는 현재 Azure에 있는 거의 모든 지리적 지역에서 UI를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="7a98b-108">Azure 스케줄러에서 사용할 수 있는 지역 목록은 [여기에 있습니다](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="7a98b-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="7a98b-109">호스팅되는 지역의 데이터 센터가 사용할 수 없게 렌더링될 경우 Azure 스케줄러의 장애 조치 기능을 통해 다른 데이터 센터에서 해당 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="7a98b-110">지리적 지역 작업 복제</span><span class="sxs-lookup"><span data-stu-id="7a98b-110">Geo-regional job replication</span></span>
<span data-ttu-id="7a98b-111">관리 요청에 대해 Azure 스케줄러 프론트엔드 외에 자체 작업도 지리적으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="7a98b-112">한 지역에서 정전이 발생할 경우 Azure 스케줄러가 장애 조치를 통해 해당 작업이 쌍을 이루는 지리적 지역에 있는 다른 데이터 센터에서 실행될 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span></span>

<span data-ttu-id="7a98b-113">예: 미국 중남부에서 만든 작업을 Azure 스케줄러가 미국 중북부에서 자동으로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="7a98b-114">미국 중남부에 장애가 발생하면 Azure 스케줄러가 이 작업을 미국 중북부에서 실행되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="7a98b-115">결과적으로, Azure 스케줄러는 Azure에서 오류가 발생할 경우 데이터가 동일한 광범위 지역 안에 유지되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="7a98b-116">즉 Azure 스케줄러가 작업에 대해 자동으로 고가용성 기능을 제공하므로 단지 고가용성을 목적으로 작업을 복제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="7a98b-117">Azure 스케줄러 안정성</span><span class="sxs-lookup"><span data-stu-id="7a98b-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="7a98b-118">Azure 스케줄러는 자체 고가용성을 보장하며 사용자가 생성한 작업에 대해서 다른 방식을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span></span> <span data-ttu-id="7a98b-119">예를 들어, 사용자 작업에서 사용 불가능한 HTTP 끝점을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="7a98b-120">어쨌든 Azure 스케줄러는 장애 처리를 위한 대안을 제시하여 작업을 성공적으로 실행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span></span> <span data-ttu-id="7a98b-121">Azure 스케줄러는 두 가지 방법으로 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="7a98b-122">“retryPolicy”를 통해 구성 가능한 재시도 정책</span><span class="sxs-lookup"><span data-stu-id="7a98b-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="7a98b-123">Azure 스케줄러에서는 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-123">Azure Scheduler allows you to configure a retry policy.</span></span> <span data-ttu-id="7a98b-124">기본적으로, 작업이 실패하면 스케줄러는 30초 간격으로 4회 더 작업을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="7a98b-125">더 적극적이거나(예: 30초 간격 10회) 더  소극적인(예: 매일 2회) 재시도 정책을 재구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="7a98b-126">예를 들어, 매주 한 번 실행되고 HTTP 끝점을 호출하는 작업을 만든 경우 이것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="7a98b-127">작업을 실행하는데 HTTP 끝점이 몇 시간 동안 다운된 경우, 기본 재시도 정책이 실패할 것이므로 작업을 다시 실행하기 위해 1주일을 더 기다리고 싶지는 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span></span> <span data-ttu-id="7a98b-128">이러한 경우 30초 간격 대신 3시간(예) 간격으로 표준 재시도 정책을 재구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="7a98b-129">재시도 정책을 구성하는 방법은 [retryPolicy](scheduler-concepts-terms.md#retrypolicy)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7a98b-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="7a98b-130">“errorAction”을 통한 대체 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="7a98b-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="7a98b-131">Azure 스케줄러 작업에 대한 대상 끝점이 연결 불가 상태로 있을 경우 Azure 스케줄러는 재시도 정책을 따른 후 대체 오류 처리 끝점으로 장애 전환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="7a98b-132">대체 오류 처리 끝점을 구성한 경우 Azure 스케줄러가 이를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="7a98b-133">대체 끝점을 지정하면 장애를 고려했을 때 자체 작업의 가용성이 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span></span>

<span data-ttu-id="7a98b-134">한 예로 아래 표에서는 Azure 스케줄러가 재시도 정책에 따라 뉴욕 웹 서비스를 히트합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span></span> <span data-ttu-id="7a98b-135">재시도 실패 후에는 대체 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-135">After the retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="7a98b-136">그런 다음 진행하여 동일한 재시도 정책으로 대체 항목에 대한 요청을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span></span>

![][2]

<span data-ttu-id="7a98b-137">원래 동작과 대체 오류 동작 모두에 동일한 재시도 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-137">Note that the same retry policy applies to both the original action and the alternate error action.</span></span> <span data-ttu-id="7a98b-138">또한 대체 오류 동작의 동작 유형이 주 동작의 동작 유형과 다를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span></span> <span data-ttu-id="7a98b-139">예를 들어 주 동작은 HTTP 끝점을 호출하는 것이면서 오류 동작은 오류 로깅을 수행하는 저장소 큐, 서비스 버스 큐 또는 서비스 버스 토픽 동작이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a98b-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="7a98b-140">대체 끝점을 구성하는 방법은 [errorAction](scheduler-concepts-terms.md#action-and-erroraction)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a98b-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a98b-141">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a98b-141">See Also</span></span>
 [<span data-ttu-id="7a98b-142">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="7a98b-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="7a98b-143">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="7a98b-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="7a98b-144">Azure 포털에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="7a98b-144">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7a98b-145">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="7a98b-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7a98b-146">Azure 스케줄러를 사용하여 복잡한 일정 및 고급 되풀이를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7a98b-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="7a98b-147">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="7a98b-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7a98b-148">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="7a98b-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="7a98b-149">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="7a98b-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="7a98b-150">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="7a98b-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
