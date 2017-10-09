---
title: "aaaAutoscaling 및 앱 서비스 환경 v1"
description: "자동 크기 조정 및 앱 서비스 환경"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="fcffc-103">자동 크기 조정 및 App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="fcffc-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="fcffc-104">앱 서비스 환경 v1 hello에 대 한이 문서는입니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="fcffc-105">최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="fcffc-106">hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="fcffc-107">Azure 앱 서비스 환경은 *자동 크기 조정*을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="fcffc-108">메트릭 또는 일정에 따라 개별 작업자 풀을 자동 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![작업자 풀에 대한 자동 크기 조정 옵션입니다.][intro]

<span data-ttu-id="fcffc-110">자동 크기 조정 최적화 하면 리소스 사용률 자동으로 증가 하 고 앱 서비스 환경 toofit 축소 예산 또는 부하 프로필 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="fcffc-111">작업자 풀 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="fcffc-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="fcffc-112">Hello에서 hello 자동 크기 조정 기능에 액세스할 수 **설정을** hello 작업자 풀의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Hello 작업자 풀의 설정 탭 합니다.][settings-scale]

<span data-ttu-id="fcffc-114">여기에서 hello 인터페이스 이후 매우 친숙 한는 hello 응용 프로그램 서비스를 확장할 때 나타나는 동일한 환경을 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![수동 크기 조정 설정입니다.][scale-manual]

<span data-ttu-id="fcffc-116">또한 자동 크기 조정 프로필을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-116">You can also configure an autoscale profile.</span></span>

![자동 크기 조정 설정입니다.][scale-profile]

<span data-ttu-id="fcffc-118">자동 크기 조정 프로필은 눈금에 대해 유용한 tooset 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="fcffc-119">이렇게 하면 하한 크기 값(1)을 설정하여 일관된 성능 환경을 유지하고 상한(2)을 설정하여 예측 가능한 지출 한도를 정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![프로필의 크기 조정 설정입니다.][scale-profile2]

<span data-ttu-id="fcffc-121">프로필을 정의한 후에 hello 작업자 풀 hello 프로필에 정의 된 hello 범위 내에 있는 인스턴스의 hello 수의 위아래로 자동 크기 조정 규칙 tooscale를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="fcffc-122">자동 크기 조정 규칙은 메트릭을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-122">Autoscale rules are based on metrics.</span></span>

![크기 조정 규칙입니다.][scale-rule]

 <span data-ttu-id="fcffc-124">모든 작업자 풀 또는 프런트 엔드 메트릭을 사용 하는 toodefine 자동 크기 조정 규칙 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="fcffc-125">이러한 메트릭은 hello에 대 한 경고가 동일한 메트릭을 hello 리소스 블레이드 그래프에 모니터링 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="fcffc-126">자동 크기 조정 예제</span><span class="sxs-lookup"><span data-stu-id="fcffc-126">Autoscale example</span></span>
<span data-ttu-id="fcffc-127">앱 서비스 환경의 자동 크기 조정은 시나리오를 살펴보면서 가장 잘 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="fcffc-128">이 문서에서는 자동 크기 조정을 설정할 때 모든 hello 필요한 고려 사항이 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="fcffc-129">hello 문서에서는 앱 서비스 환경에서 호스트 되는 앱 서비스 환경에서 자동 크기 조정 고려 하는 경우에 상호 작용 재생 hello을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="fcffc-130">시나리오 소개</span><span class="sxs-lookup"><span data-stu-id="fcffc-130">Scenario introduction</span></span>
<span data-ttu-id="fcffc-131">Frank가 마이그레이션 tooan 앱 서비스 환경 관리 하는 hello 작업 부하의 일부는 엔터프라이즈에 대 한 sysadmin입니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="fcffc-132">hello 앱 서비스 환경이 toomanual 크기 조정을 구성 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="fcffc-133">**프런트 엔드:** 3</span><span class="sxs-lookup"><span data-stu-id="fcffc-133">**Front ends:** 3</span></span>
* <span data-ttu-id="fcffc-134">**작업자 풀 1**: 10</span><span class="sxs-lookup"><span data-stu-id="fcffc-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="fcffc-135">**작업자 풀 2**: 5</span><span class="sxs-lookup"><span data-stu-id="fcffc-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="fcffc-136">**작업자 풀 3**: 5</span><span class="sxs-lookup"><span data-stu-id="fcffc-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="fcffc-137">작업자 풀 1은 프로덕션 워크로드에, 작업자 풀 2 및 작업자 풀 3은 QA(품질 보증) 및 개발 워크로드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="fcffc-138">hello 앱 서비스 계획에 대 한 QA 및 dev toomanual 크기 조정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="fcffc-139">앱 서비스 계획 hello 프로덕션 부하 및 트래픽 tooautoscale toodeal 변형으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="fcffc-140">Frank가 hello 응용 프로그램에 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="fcffc-141">그 hello office 상태인 직원이 사용 하는 기간 업무 (LOB) 응용 프로그램 이므로 부하에 대 한 hello 사용이 많은 시간별 오전 9시 및 오후 6시 사이 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="fcffc-142">사용자가 퇴근한 후에는 사용량이 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="fcffc-143">사용이 많은 시간 외 여전히 일부 부하는 사용자가 액세스할 수 있으므로 hello 앱 원격으로 자신의 모바일 장치 또는 홈 Pc를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="fcffc-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="fcffc-144">앱 서비스 계획은 이미 hello 프로덕션 tooautoscale 규칙에 따라 hello로 CPU 사용량에 따라 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![LOB 앱에 대한 특정 설정입니다.][asp-scale]

| <span data-ttu-id="fcffc-146">**자동 크기 조정 프로필 - 주중 - 앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="fcffc-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="fcffc-147">**자동 크기 조정 프로필 - 주말 - 앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="fcffc-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="fcffc-148">**이름:** 주중 프로필</span><span class="sxs-lookup"><span data-stu-id="fcffc-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="fcffc-149">**이름:** 주말 프로필</span><span class="sxs-lookup"><span data-stu-id="fcffc-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="fcffc-150">**크기 조정 기준:** 일정 및 성능 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="fcffc-151">**크기 조정 기준:** 일정 및 성능 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fcffc-152">**프로필:** 주중</span><span class="sxs-lookup"><span data-stu-id="fcffc-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="fcffc-153">**프로필:** 주말</span><span class="sxs-lookup"><span data-stu-id="fcffc-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="fcffc-154">**유형:** 반복</span><span class="sxs-lookup"><span data-stu-id="fcffc-154">**Type:** Recurrence</span></span> |<span data-ttu-id="fcffc-155">**유형:** 반복</span><span class="sxs-lookup"><span data-stu-id="fcffc-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fcffc-156">**대상 범위:** 5 too20 인스턴스</span><span class="sxs-lookup"><span data-stu-id="fcffc-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="fcffc-157">**대상 범위:** 3 too10 인스턴스</span><span class="sxs-lookup"><span data-stu-id="fcffc-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="fcffc-158">**요일:** 월요일, 화요일, 수요일, 목요일, 금요일</span><span class="sxs-lookup"><span data-stu-id="fcffc-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="fcffc-159">**요일:** 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="fcffc-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="fcffc-160">**시작 시간:** 오전 9시</span><span class="sxs-lookup"><span data-stu-id="fcffc-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="fcffc-161">**시작 시간:** 오전 9시</span><span class="sxs-lookup"><span data-stu-id="fcffc-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fcffc-162">**표준 시간대:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fcffc-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="fcffc-163">**표준 시간대:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fcffc-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="fcffc-164">**자동 크기 조정 규칙(확장)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="fcffc-165">**자동 크기 조정 규칙(확장)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fcffc-166">**리소스:** 프로덕션(앱 서비스 환경)</span><span class="sxs-lookup"><span data-stu-id="fcffc-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="fcffc-167">**리소스:** 프로덕션(앱 서비스 환경)</span><span class="sxs-lookup"><span data-stu-id="fcffc-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="fcffc-168">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-168">**Metric:** CPU %</span></span> |<span data-ttu-id="fcffc-169">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fcffc-170">**작업:** 60% 초과</span><span class="sxs-lookup"><span data-stu-id="fcffc-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="fcffc-171">**작업:** 80% 초과</span><span class="sxs-lookup"><span data-stu-id="fcffc-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="fcffc-172">**기간:** 5분</span><span class="sxs-lookup"><span data-stu-id="fcffc-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="fcffc-173">**기간:** 10분</span><span class="sxs-lookup"><span data-stu-id="fcffc-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="fcffc-174">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="fcffc-175">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-176">**작업:** 개수 2씩 증가</span><span class="sxs-lookup"><span data-stu-id="fcffc-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="fcffc-177">**작업:** 개수 1씩 증가</span><span class="sxs-lookup"><span data-stu-id="fcffc-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="fcffc-178">**정지(분):** 15</span><span class="sxs-lookup"><span data-stu-id="fcffc-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="fcffc-179">**정지(분):** 20</span><span class="sxs-lookup"><span data-stu-id="fcffc-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="fcffc-180">**자동 크기 조정 규칙(축소)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="fcffc-181">**자동 크기 조정 규칙(축소)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fcffc-182">**리소스:** 프로덕션(앱 서비스 환경)</span><span class="sxs-lookup"><span data-stu-id="fcffc-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="fcffc-183">**리소스:** 프로덕션(앱 서비스 환경)</span><span class="sxs-lookup"><span data-stu-id="fcffc-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="fcffc-184">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-184">**Metric:** CPU %</span></span> |<span data-ttu-id="fcffc-185">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fcffc-186">**작업:** 30% 미만</span><span class="sxs-lookup"><span data-stu-id="fcffc-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="fcffc-187">**작업:** 20% 미만</span><span class="sxs-lookup"><span data-stu-id="fcffc-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="fcffc-188">**기간:** 10분</span><span class="sxs-lookup"><span data-stu-id="fcffc-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="fcffc-189">**기간:** 15분</span><span class="sxs-lookup"><span data-stu-id="fcffc-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="fcffc-190">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="fcffc-191">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-192">**작업:** 개수 1씩 감소</span><span class="sxs-lookup"><span data-stu-id="fcffc-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="fcffc-193">**작업:** 개수 1씩 감소</span><span class="sxs-lookup"><span data-stu-id="fcffc-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="fcffc-194">**정지(분):** 20</span><span class="sxs-lookup"><span data-stu-id="fcffc-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="fcffc-195">**정지(분):** 10</span><span class="sxs-lookup"><span data-stu-id="fcffc-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="fcffc-196">앱 서비스 계획 인플레이션 속도</span><span class="sxs-lookup"><span data-stu-id="fcffc-196">App Service plan inflation rate</span></span>
<span data-ttu-id="fcffc-197">앱 서비스 계획을 구성 된 tooautoscale 있는 시간당 최대 속도로 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="fcffc-198">이 속도 수 수 기반으로 계산 hello hello 자동 크기 조정 규칙에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="fcffc-199">이해 하 고 계산 hello *앱 서비스 계획 인플레이션이 요금* 배율 변경 내용을 tooa 작업자 풀 순간 없기 때문에 앱 서비스 환경 크기 자동 조정에 대 한 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="fcffc-200">앱 서비스 계획 인플레이션이 요금 hello 다음과 같이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![앱 서비스 계획 인플레이션 속도 계산입니다.][ASP-Inflation]

<span data-ttu-id="fcffc-202">Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 요일 프로필에 대 한 크기 확장 규칙 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![자동 크기 조정 - 확장 규칙에 따른 주중의 앱 서비스 계획 인플레이션 속도입니다.][Equation1]

<span data-ttu-id="fcffc-204">Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 주말 프로필에 대 한 크기 확장 규칙의 hello 경우에서 hello 수식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![자동 크기 조정 - 확장 규칙에 따른 주말의 앱 서비스 계획 인플레이션 속도입니다.][Equation2]

<span data-ttu-id="fcffc-206">이 값은 축소 작업에 대해서도 산출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="fcffc-207">Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 요일 프로필에 대 한 아래쪽 크기 조정 규칙에 따라이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![자동 크기 조정 - 축소 규칙에 따른 주중의 앱 서비스 계획 인플레이션 속도입니다.][Equation3]

<span data-ttu-id="fcffc-209">자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 주말 프로필에 대 한 배율 아래로 규칙 hello hello 경우에서 hello 수식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![자동 크기 조정 - 축소 규칙에 따른 주말의 앱 서비스 계획 인플레이션 속도입니다.][Equation4]

<span data-ttu-id="fcffc-211">hello 프로덕션 앱 서비스 계획에서 최대 속도는 hello 주 인스턴스/시간 및 주말 hello 4 개의 인스턴스/시간 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="fcffc-212">Hello 주간에 4 개의 인스턴스/시간에서 최대 속도로 인스턴스 및 주말 중 6 개 인스턴스/시간을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="fcffc-213">앱 서비스 계획을 여러 작업자 풀에서 호스트 되는, 있으면 toocalculate hello *인플레이션이 초 당 총* 앱 서비스 계획을 만들고 있는 모든 hello에 대 한 hello 인플레이션이 비율의 hello 합계로 작업자 풀의 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![작업자 풀에서 호스팅되는 여러 앱 서비스 계획에 대한 총 인플레이션 속도 계산입니다.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="fcffc-215">사용 하 여 hello 앱 서비스 계획 인플레이션이 속도 toodefine 작업자 풀 자동 크기 조정 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="fcffc-216">작업자는 tooautoscale 구성된 되어 있는 앱 서비스 계획의 용량 버퍼 할당 해야 합니다. 해당 호스트를 풀링합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="fcffc-217">hello 버퍼 hello 자동 크기 조정 작업 toogrow 허용 하며 필요에 따라 앱 서비스 계획을 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="fcffc-218">hello 앱 서비스 계획 인플레이션이 초 당 총 계산 hello 최소 버퍼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="fcffc-219">앱 서비스 환경 크기 조정 작업이 몇 시간 tooapply 걸리므로 모든 변경 내용이 추가 크기 조정 작업이 진행 중인 동안이 오류가 발생할 수 있는 요청 변경을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="fcffc-220">tooaccommodate 이러한 대기 시간은 권장를 사용 하는 hello hello 최소 각 자동 크기 조정 작업에 대해 추가 된 인스턴스 수로 전체 앱 서비스 계획 인플레이션이 비율을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="fcffc-221">이 정보를 사용 하 여 Frank hello 정의할 수 자동 크기 조정 프로필 및 규칙:</span><span class="sxs-lookup"><span data-stu-id="fcffc-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![LOB 예제에 대한 자동 크기 조정 프로필 규칙입니다.][Worker-Pool-Scale]

| <span data-ttu-id="fcffc-223">**자동 크기 조정 프로필 – 주중**</span><span class="sxs-lookup"><span data-stu-id="fcffc-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="fcffc-224">**자동 크기 조정 프로필 – 주말**</span><span class="sxs-lookup"><span data-stu-id="fcffc-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="fcffc-225">**이름:** 주중 프로필</span><span class="sxs-lookup"><span data-stu-id="fcffc-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="fcffc-226">**이름:** 주말 프로필</span><span class="sxs-lookup"><span data-stu-id="fcffc-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="fcffc-227">**크기 조정 기준:** 일정 및 성능 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="fcffc-228">**크기 조정 기준:** 일정 및 성능 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fcffc-229">**프로필:** 주중</span><span class="sxs-lookup"><span data-stu-id="fcffc-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="fcffc-230">**프로필:** 주말</span><span class="sxs-lookup"><span data-stu-id="fcffc-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="fcffc-231">**유형:** 반복</span><span class="sxs-lookup"><span data-stu-id="fcffc-231">**Type:** Recurrence</span></span> |<span data-ttu-id="fcffc-232">**유형:** 반복</span><span class="sxs-lookup"><span data-stu-id="fcffc-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fcffc-233">**대상 범위:** 13 too25 인스턴스</span><span class="sxs-lookup"><span data-stu-id="fcffc-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="fcffc-234">**대상 범위:** 6 too15 인스턴스</span><span class="sxs-lookup"><span data-stu-id="fcffc-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="fcffc-235">**요일:** 월요일, 화요일, 수요일, 목요일, 금요일</span><span class="sxs-lookup"><span data-stu-id="fcffc-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="fcffc-236">**요일:** 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="fcffc-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="fcffc-237">**시작 시간:** 오전 7시</span><span class="sxs-lookup"><span data-stu-id="fcffc-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="fcffc-238">**시작 시간:** 오전 9시</span><span class="sxs-lookup"><span data-stu-id="fcffc-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fcffc-239">**표준 시간대:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fcffc-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="fcffc-240">**표준 시간대:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fcffc-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="fcffc-241">**자동 크기 조정 규칙(확장)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="fcffc-242">**자동 크기 조정 규칙(확장)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fcffc-243">**리소스:** 작업자 풀 1</span><span class="sxs-lookup"><span data-stu-id="fcffc-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="fcffc-244">**리소스:** 작업자 풀 1</span><span class="sxs-lookup"><span data-stu-id="fcffc-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fcffc-245">**메트릭:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fcffc-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="fcffc-246">**메트릭:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fcffc-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="fcffc-247">**작업:** 8 미만</span><span class="sxs-lookup"><span data-stu-id="fcffc-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="fcffc-248">**작업:** 3 미만</span><span class="sxs-lookup"><span data-stu-id="fcffc-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="fcffc-249">**기간:** 20분</span><span class="sxs-lookup"><span data-stu-id="fcffc-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="fcffc-250">**기간:** 30분</span><span class="sxs-lookup"><span data-stu-id="fcffc-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="fcffc-251">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="fcffc-252">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-253">**작업:** 개수 8씩 증가</span><span class="sxs-lookup"><span data-stu-id="fcffc-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="fcffc-254">**작업:** 개수 3씩 증가</span><span class="sxs-lookup"><span data-stu-id="fcffc-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="fcffc-255">**정지(분):** 180</span><span class="sxs-lookup"><span data-stu-id="fcffc-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="fcffc-256">**정지(분):** 180</span><span class="sxs-lookup"><span data-stu-id="fcffc-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="fcffc-257">**자동 크기 조정 규칙(축소)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="fcffc-258">**자동 크기 조정 규칙(축소)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fcffc-259">**리소스:** 작업자 풀 1</span><span class="sxs-lookup"><span data-stu-id="fcffc-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="fcffc-260">**리소스:** 작업자 풀 1</span><span class="sxs-lookup"><span data-stu-id="fcffc-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fcffc-261">**메트릭:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fcffc-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="fcffc-262">**메트릭:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fcffc-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="fcffc-263">**작업:** 8 초과</span><span class="sxs-lookup"><span data-stu-id="fcffc-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="fcffc-264">**작업:** 3 초과</span><span class="sxs-lookup"><span data-stu-id="fcffc-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="fcffc-265">**기간:** 20분</span><span class="sxs-lookup"><span data-stu-id="fcffc-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="fcffc-266">**기간:** 15분</span><span class="sxs-lookup"><span data-stu-id="fcffc-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="fcffc-267">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="fcffc-268">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-269">**작업:** 개수 2씩 감소</span><span class="sxs-lookup"><span data-stu-id="fcffc-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="fcffc-270">**작업:** 개수 3씩 감소</span><span class="sxs-lookup"><span data-stu-id="fcffc-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="fcffc-271">**정지(분):** 120</span><span class="sxs-lookup"><span data-stu-id="fcffc-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="fcffc-272">**정지(분):** 120</span><span class="sxs-lookup"><span data-stu-id="fcffc-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="fcffc-273">hello hello 프로필에 정의 된 대상 범위는 hello 앱 서비스 계획에 대 한 프로필 + 버퍼에 정의 된 hello 최소 인스턴스 여 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="fcffc-274">hello 최대 범위 hello 합계 hello 작업자 풀에서 호스팅되는 모든 앱 서비스 계획에 대 한 모든 hello 최대 범위를 가진 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="fcffc-275">hello hello 수직 확장 규칙에 대 한 증가 수를 눈금에 대 한 앱 서비스 계획 인플레이션이 요금 X 집합 tooat 최소 1 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="fcffc-276">1 X 아래로 눈금에 대 한 앱 서비스 계획 인플레이션이 속도 hello 또는 감소 수 조정된 toosomething X 1/2 사이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="fcffc-277">프런트 엔드 풀에 대한 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fcffc-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="fcffc-278">프런트 엔드 자동 크기 조정에 대한 규칙은 작업자 풀에 대한 것보다 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="fcffc-279">기본적으로</span><span class="sxs-lookup"><span data-stu-id="fcffc-279">Primarily, you should</span></span>  
<span data-ttu-id="fcffc-280">앱 서비스 계획에서 크기 조정 작업 순간 없는 hello 측정 및 hello 쿨 다운 타이머의 기간을 고려 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="fcffc-281">이 시나리오에서는 Frank 알고 해당 hello 오류율 프런트 엔드 CPU 사용률이 80%에 도달 하는 후 늘어나고 hello 자동 크기 조정 규칙 tooincrease 인스턴스 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcffc-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![프런트 엔드 풀에 대한 자동 크기 조정 설정입니다.][Front-End-Scale]

| <span data-ttu-id="fcffc-283">**자동 크기 조정 프로필 – 프런트 엔드**</span><span class="sxs-lookup"><span data-stu-id="fcffc-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="fcffc-284">**이름:** 자동 크기 조정 - 프런트 엔드</span><span class="sxs-lookup"><span data-stu-id="fcffc-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="fcffc-285">**크기 조정 기준:** 일정 및 성능 규칙</span><span class="sxs-lookup"><span data-stu-id="fcffc-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fcffc-286">**프로필:** 매일</span><span class="sxs-lookup"><span data-stu-id="fcffc-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="fcffc-287">**유형:** 반복</span><span class="sxs-lookup"><span data-stu-id="fcffc-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fcffc-288">**대상 범위:** 3 too10 인스턴스</span><span class="sxs-lookup"><span data-stu-id="fcffc-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="fcffc-289">**요일:** 매일</span><span class="sxs-lookup"><span data-stu-id="fcffc-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="fcffc-290">**시작 시간:** 오전 9시</span><span class="sxs-lookup"><span data-stu-id="fcffc-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fcffc-291">**표준 시간대:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fcffc-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="fcffc-292">**자동 크기 조정 규칙(확장)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fcffc-293">**리소스:** 프런트 엔드 풀</span><span class="sxs-lookup"><span data-stu-id="fcffc-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="fcffc-294">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fcffc-295">**작업:** 60% 초과</span><span class="sxs-lookup"><span data-stu-id="fcffc-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="fcffc-296">**기간:** 20분</span><span class="sxs-lookup"><span data-stu-id="fcffc-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="fcffc-297">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-298">**작업:** 개수 3씩 증가</span><span class="sxs-lookup"><span data-stu-id="fcffc-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="fcffc-299">**정지(분):** 120</span><span class="sxs-lookup"><span data-stu-id="fcffc-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="fcffc-300">**자동 크기 조정 규칙(축소)**</span><span class="sxs-lookup"><span data-stu-id="fcffc-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fcffc-301">**리소스:** 작업자 풀 1</span><span class="sxs-lookup"><span data-stu-id="fcffc-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fcffc-302">**메트릭:** CPU %</span><span class="sxs-lookup"><span data-stu-id="fcffc-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fcffc-303">**작업:** 30% 미만</span><span class="sxs-lookup"><span data-stu-id="fcffc-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="fcffc-304">**기간:** 20분</span><span class="sxs-lookup"><span data-stu-id="fcffc-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="fcffc-305">**집계 시간:** 평균</span><span class="sxs-lookup"><span data-stu-id="fcffc-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fcffc-306">**작업:** 개수 3씩 감소</span><span class="sxs-lookup"><span data-stu-id="fcffc-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="fcffc-307">**정지(분):** 120</span><span class="sxs-lookup"><span data-stu-id="fcffc-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
