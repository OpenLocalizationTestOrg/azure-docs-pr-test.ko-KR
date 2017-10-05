---
title: "Azure 포털에서 Azure 스케줄러 시작 | Microsoft Docs"
description: "Azure 포털에서 Azure 스케줄러 시작"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 3861ee121ed1c4d086ea81640e84d924d7d17ea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="ce37c-103">Azure 포털에서 Azure 스케줄러 시작</span><span class="sxs-lookup"><span data-stu-id="ce37c-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="ce37c-104">Azure 스케줄러에서 예약된 작업을 만드는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="ce37c-105">이 자습서에서는 작업을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="ce37c-106">스케줄러의 모니터링 및 관리 기능도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="ce37c-107">작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ce37c-107">Create a job</span></span>
1. <span data-ttu-id="ce37c-108">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="ce37c-109">**+새로 만들기**를 클릭하고 > 검색 상자에 *스케줄러*를 입력하고 > 결과에서 **스케줄러**를 선택하고 > **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="ce37c-110">간단히 GET 요청으로 http://www.microsoft.com/을 히트하는 작업을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="ce37c-111">**스케줄러 작업** 화면에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="ce37c-112">**이름:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="ce37c-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="ce37c-113">**구독:** Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="ce37c-114">**작업 컬렉션:** 기존 작업 컬렉션을 선택하거나 **새로 만들기**를 클릭하고 > 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="ce37c-115">다음으로 **작업 설정**에서 다음 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="ce37c-116">**작업 유형:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="ce37c-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="ce37c-117">**메서드:** `GET`</span><span class="sxs-lookup"><span data-stu-id="ce37c-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="ce37c-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="ce37c-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="ce37c-119">마지막으로, 일정을 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="ce37c-120">작업은 일회성 작업으로 정의할 수 있지만 되풀이 일정을 선택해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="ce37c-121">**되풀이**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="ce37c-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="ce37c-122">**시작**: 오늘 날짜</span><span class="sxs-lookup"><span data-stu-id="ce37c-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="ce37c-123">**되풀이 간격**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="ce37c-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="ce37c-124">**종료 날짜**: 오늘 날짜부터 이틀 후</span><span class="sxs-lookup"><span data-stu-id="ce37c-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="ce37c-125">**만들기**</span><span class="sxs-lookup"><span data-stu-id="ce37c-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="ce37c-126">작업 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="ce37c-126">Manage and monitor jobs</span></span>
<span data-ttu-id="ce37c-127">작업이 만들어지면 기본 Azure 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="ce37c-128">작업을 클릭하면 다음 탭을 제공하는 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="ce37c-129">속성</span><span class="sxs-lookup"><span data-stu-id="ce37c-129">Properties</span></span>  
2. <span data-ttu-id="ce37c-130">작업 설정</span><span class="sxs-lookup"><span data-stu-id="ce37c-130">Action Settings</span></span>  
3. <span data-ttu-id="ce37c-131">일정</span><span class="sxs-lookup"><span data-stu-id="ce37c-131">Schedule</span></span>  
4. <span data-ttu-id="ce37c-132">기록</span><span class="sxs-lookup"><span data-stu-id="ce37c-132">History</span></span>
5. <span data-ttu-id="ce37c-133">사용자</span><span class="sxs-lookup"><span data-stu-id="ce37c-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="ce37c-134">속성</span><span class="sxs-lookup"><span data-stu-id="ce37c-134">Properties</span></span>
<span data-ttu-id="ce37c-135">이러한 읽기 전용 속성은 스케줄러 작업에 대한 관리 메타데이터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="ce37c-136">작업 설정</span><span class="sxs-lookup"><span data-stu-id="ce37c-136">Action settings</span></span>
<span data-ttu-id="ce37c-137">**작업** 화면에서 작업을 클릭하면 해당 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="ce37c-138">이렇게 하면 빠른 만들기 마법사에서 구성하지 않은 경우 고급 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="ce37c-139">모든 동작 유형의 경우 다시 시도 정책 및 오류 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="ce37c-140">HTTP 및 HTTPS 작업 동작 유형에서, 메서드를 허용되는 HTTP 동사로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="ce37c-141">헤더와 기본 인증 정보를 추가, 삭제 또는 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="ce37c-142">저장소 큐 동작 유형의 경우 저장소 계정, 큐 이름, SAS 토큰 및 본문을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="ce37c-143">서비스 버스 동작 유형의 네임스페이스, 토픽/큐 경로, 인증 설정, 전송 유형, 메시지 속성 및 메시지 본문을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="ce37c-144">일정</span><span class="sxs-lookup"><span data-stu-id="ce37c-144">Schedule</span></span>
<span data-ttu-id="ce37c-145">이렇게 하면 빠른 만들기 마법사에서 만든 일정을 변경하지 않으려는 경우 일정을 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="ce37c-146">[작업에서 복잡한 일정 및 고급 되풀이](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="ce37c-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="ce37c-147">시작 날짜와 시간, 되풀이 일정 및 종료 날짜와 시간(작업이 되풀이될 경우)을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="ce37c-148">기록</span><span class="sxs-lookup"><span data-stu-id="ce37c-148">History</span></span>
<span data-ttu-id="ce37c-149">**기록** 탭은 선택한 작업에 대해 시스템의 모든 작업 실행에 선택한 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="ce37c-150">이러한 메트릭은 스케줄러 상태와 관련된 실시간 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="ce37c-151">가동 상태</span><span class="sxs-lookup"><span data-stu-id="ce37c-151">Status</span></span>  
2. <span data-ttu-id="ce37c-152">세부 정보</span><span class="sxs-lookup"><span data-stu-id="ce37c-152">Details</span></span>  
3. <span data-ttu-id="ce37c-153">다시 시도 횟수</span><span class="sxs-lookup"><span data-stu-id="ce37c-153">Retry attempts</span></span>
4. <span data-ttu-id="ce37c-154">발생 빈도: 첫 번째, 두 번째, 세 번째 등</span><span class="sxs-lookup"><span data-stu-id="ce37c-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="ce37c-155">실행 시작 시간</span><span class="sxs-lookup"><span data-stu-id="ce37c-155">Start time of execution</span></span>  
6. <span data-ttu-id="ce37c-156">실행 종료 시간</span><span class="sxs-lookup"><span data-stu-id="ce37c-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="ce37c-157">**기록 세부 정보**보기 실행을 클릭하여 각 실행의 전체 응답을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="ce37c-158">이 대화 상자에서는 응답을 클립보드에 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="ce37c-159">사용자</span><span class="sxs-lookup"><span data-stu-id="ce37c-159">Users</span></span>
<span data-ttu-id="ce37c-160">Azure RBAC(역할 기반 액세스 제어)를 통해 Azure 스케줄러에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ce37c-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="ce37c-161">사용자 탭을 사용하는 방법을 알아보려면 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ce37c-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="ce37c-162">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ce37c-162">See also</span></span>
 [<span data-ttu-id="ce37c-163">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="ce37c-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="ce37c-164">스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="ce37c-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="ce37c-165">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="ce37c-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="ce37c-166">Azure 스케줄러를 사용하여 복잡한 일정 및 고급 되풀이를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ce37c-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="ce37c-167">스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="ce37c-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="ce37c-168">스케줄러 PowerShell Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="ce37c-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="ce37c-169">스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="ce37c-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="ce37c-170">스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="ce37c-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="ce37c-171">스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="ce37c-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
