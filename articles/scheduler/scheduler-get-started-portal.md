---
title: "aaaGet Azure 포털에서 Azure 스케줄러를 시작 합니다. | Microsoft Docs"
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
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="d1eba-103">Azure 포털에서 Azure 스케줄러 시작</span><span class="sxs-lookup"><span data-stu-id="d1eba-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="d1eba-104">것은 Azure Scheduler에서 쉽게 toocreate 예약 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="d1eba-105">이 자습서에서는 알아봅니다 어떻게 toocreate 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="d1eba-106">스케줄러의 모니터링 및 관리 기능도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="d1eba-107">작업 만들기</span><span class="sxs-lookup"><span data-stu-id="d1eba-107">Create a job</span></span>
1. <span data-ttu-id="d1eba-108">역시 로그인[Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="d1eba-109">클릭 **+ 새로 만들기** > 형식 *스케줄러* hello 검색 상자에 > 선택 **스케줄러** 결과에서 > 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="d1eba-110">간단히 GET 요청으로 http://www.microsoft.com/을 히트하는 작업을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="d1eba-111">Hello에 **스케줄러 작업** 화면에서 다음 정보는 hello 입력:</span><span class="sxs-lookup"><span data-stu-id="d1eba-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="d1eba-112">**이름:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="d1eba-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="d1eba-113">**구독:** Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="d1eba-114">**작업 컬렉션:** 기존 작업 컬렉션을 선택하거나 **새로 만들기**를 클릭하고 > 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="d1eba-115">다음 **동작 설정**, hello 다음 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="d1eba-116">**작업 유형:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="d1eba-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="d1eba-117">**메서드:** `GET`</span><span class="sxs-lookup"><span data-stu-id="d1eba-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="d1eba-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="d1eba-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="d1eba-119">마지막으로, 일정을 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="d1eba-120">hello 작업 작업은 일회성 작업으로 정의할 수 있지만 되풀이 일정을 선택:</span><span class="sxs-lookup"><span data-stu-id="d1eba-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="d1eba-121">**되풀이**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="d1eba-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="d1eba-122">**시작**: 오늘 날짜</span><span class="sxs-lookup"><span data-stu-id="d1eba-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="d1eba-123">**되풀이 간격**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="d1eba-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="d1eba-124">**종료 날짜**: 오늘 날짜부터 이틀 후</span><span class="sxs-lookup"><span data-stu-id="d1eba-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="d1eba-125">**만들기**</span><span class="sxs-lookup"><span data-stu-id="d1eba-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="d1eba-126">작업 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="d1eba-126">Manage and monitor jobs</span></span>
<span data-ttu-id="d1eba-127">작업을 만든 후 기본 Azure 대시보드 hello에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="d1eba-128">Hello 작업 및 새 클릭 탭 뒤 hello로 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="d1eba-129">properties</span><span class="sxs-lookup"><span data-stu-id="d1eba-129">Properties</span></span>  
2. <span data-ttu-id="d1eba-130">작업 설정</span><span class="sxs-lookup"><span data-stu-id="d1eba-130">Action Settings</span></span>  
3. <span data-ttu-id="d1eba-131">일정</span><span class="sxs-lookup"><span data-stu-id="d1eba-131">Schedule</span></span>  
4. <span data-ttu-id="d1eba-132">기록</span><span class="sxs-lookup"><span data-stu-id="d1eba-132">History</span></span>
5. <span data-ttu-id="d1eba-133">사용자</span><span class="sxs-lookup"><span data-stu-id="d1eba-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="d1eba-134">properties</span><span class="sxs-lookup"><span data-stu-id="d1eba-134">Properties</span></span>
<span data-ttu-id="d1eba-135">이 읽기 전용 속성 hello 스케줄러 작업에 대 한 hello 관리 메타 데이터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="d1eba-136">작업 설정</span><span class="sxs-lookup"><span data-stu-id="d1eba-136">Action settings</span></span>
<span data-ttu-id="d1eba-137">Hello에서 작업을 클릭 하면 **작업** 화면에서는 작업 tooconfigure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="d1eba-138">Hello에 구성 하지 않은 경우 빨리 만들기 마법사, 고급 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="d1eba-139">모든 동작 유형에 대 한 hello 다시 시도 정책 및 hello 오류 시 수행할 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="d1eba-140">HTTP 및 HTTPS 작업 동작 유형에 대 한 HTTP 동사를 허용 하는 hello 메서드 tooany를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="d1eba-141">있습니다 수 또한 추가, 삭제 또는 hello 헤더 및 기본 인증 정보를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="d1eba-142">저장소 큐 동작 유형에 대 한 hello 저장소 계정, 큐 이름, SAS 토큰 및 본문을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="d1eba-143">서비스 버스 동작 유형에 대 한 hello 네임 스페이스, 항목/큐 경로, 인증 설정, 전송 종류, 메시지 속성 및 메시지 본문을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="d1eba-144">일정</span><span class="sxs-lookup"><span data-stu-id="d1eba-144">Schedule</span></span>
<span data-ttu-id="d1eba-145">따라서 hello에서 만든 toochange hello 일정 원하는 경우 빨리 만들기 마법사, hello 일정을 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="d1eba-146">이 영업 기회 toobuild [복잡 한 일정 및 작업에서 고급 되풀이](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="d1eba-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="d1eba-147">종료 날짜 및 시간 (hello 작업이. 되풀이 되) 하는 경우 시간, 되풀이 일정 및 hello 및 hello 시작 날짜를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="d1eba-148">기록</span><span class="sxs-lookup"><span data-stu-id="d1eba-148">History</span></span>
<span data-ttu-id="d1eba-149">hello **기록** 탭에는 hello 선택한 작업에 대 한 hello 시스템의 모든 작업 실행에 대해 선택한 메트릭이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="d1eba-150">이러한 메트릭은 스케줄러의 hello 상태에 대 한 실시간 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="d1eba-151">가동 상태</span><span class="sxs-lookup"><span data-stu-id="d1eba-151">Status</span></span>  
2. <span data-ttu-id="d1eba-152">세부 정보</span><span class="sxs-lookup"><span data-stu-id="d1eba-152">Details</span></span>  
3. <span data-ttu-id="d1eba-153">다시 시도 횟수</span><span class="sxs-lookup"><span data-stu-id="d1eba-153">Retry attempts</span></span>
4. <span data-ttu-id="d1eba-154">발생 빈도: 첫 번째, 두 번째, 세 번째 등</span><span class="sxs-lookup"><span data-stu-id="d1eba-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="d1eba-155">실행 시작 시간</span><span class="sxs-lookup"><span data-stu-id="d1eba-155">Start time of execution</span></span>  
6. <span data-ttu-id="d1eba-156">실행 종료 시간</span><span class="sxs-lookup"><span data-stu-id="d1eba-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="d1eba-157">실행된 tooview 클릭할 수 있습니다 해당 **기록 세부 정보**, 모든 실행에 대 한 hello 전체 응답을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="d1eba-158">이 대화 상자 toocopy hello 응답 toohello 클립보드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="d1eba-159">사용자</span><span class="sxs-lookup"><span data-stu-id="d1eba-159">Users</span></span>
<span data-ttu-id="d1eba-160">Azure RBAC(역할 기반 액세스 제어)를 통해 Azure 스케줄러에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d1eba-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="d1eba-161">사용자 탭 toouse hello 너무 참조 하는 방법 toolearn[신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="d1eba-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="d1eba-162">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d1eba-162">See also</span></span>
 [<span data-ttu-id="d1eba-163">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="d1eba-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="d1eba-164">스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="d1eba-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d1eba-165">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="d1eba-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d1eba-166">일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이</span><span class="sxs-lookup"><span data-stu-id="d1eba-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="d1eba-167">스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="d1eba-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d1eba-168">스케줄러 PowerShell Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="d1eba-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d1eba-169">스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="d1eba-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d1eba-170">스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="d1eba-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="d1eba-171">스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="d1eba-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

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
