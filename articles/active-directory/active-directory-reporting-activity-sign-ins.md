---
title: "hello Azure Active Directory 포털에서 aaaSign 기능 작업 보고서 | Microsoft Docs"
description: "Hello Azure Active Directory 포털에서 소개 toosign 기능 작업 보고서"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="bea8f-103">Hello Azure Active Directory 포털의 로그인 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="bea8f-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="bea8f-104">Azure Active Directory (Azure AD) hello에 보고 [Azure 포털](https://portal.azure.com), 환경을 어떻게 진행 되는 toodetermine 필요한 hello 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="bea8f-105">Azure Active Directory의 보고 아키텍처 hello hello 다음과 같은 구성 요소가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="bea8f-106">**활동**</span><span class="sxs-lookup"><span data-stu-id="bea8f-106">**Activity**</span></span> 
    - <span data-ttu-id="bea8f-107">**로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="bea8f-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="bea8f-108">**감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 작업 정보</span><span class="sxs-lookup"><span data-stu-id="bea8f-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="bea8f-109">**보안**</span><span class="sxs-lookup"><span data-stu-id="bea8f-109">**Security**</span></span> 
    - <span data-ttu-id="bea8f-110">**위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="bea8f-111">자세한 내용은 위험한 로그인을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bea8f-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="bea8f-112">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="bea8f-113">자세한 내용은 위험 플래그가 지정된 사용자를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bea8f-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="bea8f-114">이 항목에서는 hello 로그인 작업의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="bea8f-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="bea8f-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="bea8f-116">Hello 데이터에 액세스할 수 있는 사용자?</span><span class="sxs-lookup"><span data-stu-id="bea8f-116">Who can access hello data?</span></span>
* <span data-ttu-id="bea8f-117">Hello 보안 판독기 또는 보안 관리자 역할의 사용자</span><span class="sxs-lookup"><span data-stu-id="bea8f-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="bea8f-118">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="bea8f-118">Global Admins</span></span>
* <span data-ttu-id="bea8f-119">모든 사용자(비관리자)가 자신의 로그인에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="bea8f-120">어떤 Azure AD 라이선스가 tooaccess 로그인 활동이 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="bea8f-121">테 넌 트에 연결 된 Azure AD Premium 라이선스가 있어야 합니다. toosee hello 모두에 대 한 로그인 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="bea8f-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="bea8f-122">로그인 활동</span><span class="sxs-lookup"><span data-stu-id="bea8f-122">Signs-in activities</span></span>

<span data-ttu-id="bea8f-123">Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="bea8f-124">사용자의 hello 로그인 패턴 이란?</span><span class="sxs-lookup"><span data-stu-id="bea8f-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="bea8f-125">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="bea8f-126">이러한 로그인의 hello 상태는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bea8f-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="bea8f-127">첫 번째 항목 지점 tooall 로그인 활동 데이터는 **로그인** 의 hello 활동 섹션에서 **Azure Active**합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="bea8f-128">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/61.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="bea8f-129">감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="bea8f-130">hello 관련된 사용자</span><span class="sxs-lookup"><span data-stu-id="bea8f-130">hello related user</span></span>
- <span data-ttu-id="bea8f-131">hello 응용 프로그램 hello 사용자가 로그인 하려면</span><span class="sxs-lookup"><span data-stu-id="bea8f-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="bea8f-132">hello 로그인 상태</span><span class="sxs-lookup"><span data-stu-id="bea8f-132">hello sign-in status</span></span>
- <span data-ttu-id="bea8f-133">hello 로그인 시간</span><span class="sxs-lookup"><span data-stu-id="bea8f-133">hello sign-in time</span></span>

<span data-ttu-id="bea8f-134">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-135">클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="bea8f-136">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/19.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-137">이 toodisplay 추가 필드를 사용 하면 하거나 이미 표시 되는 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="bea8f-138">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/42.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-139">Hello 목록 뷰에서 항목을 클릭 하 여 항목에 대 한 모든 사용 가능한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="bea8f-140">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/43.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="bea8f-141">로그인 활동 필터링</span><span class="sxs-lookup"><span data-stu-id="bea8f-141">Filtering sign-in activities</span></span>

<span data-ttu-id="bea8f-142">hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 로그인 데이터를 보고.</span><span class="sxs-lookup"><span data-stu-id="bea8f-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="bea8f-143">시간 간격</span><span class="sxs-lookup"><span data-stu-id="bea8f-143">Time interval</span></span>
- <span data-ttu-id="bea8f-144">사용자</span><span class="sxs-lookup"><span data-stu-id="bea8f-144">User</span></span>
- <span data-ttu-id="bea8f-145">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bea8f-145">Application</span></span>
- <span data-ttu-id="bea8f-146">클라이언트</span><span class="sxs-lookup"><span data-stu-id="bea8f-146">Client</span></span>
- <span data-ttu-id="bea8f-147">로그인 상태</span><span class="sxs-lookup"><span data-stu-id="bea8f-147">Sign-in status</span></span>

<span data-ttu-id="bea8f-148">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/44.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="bea8f-149">hello **시간 간격** 필터 사용 tooyou toodefine hello에 대 한 시간 범위는 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="bea8f-150">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-150">Possible values are:</span></span>

- <span data-ttu-id="bea8f-151">1개월</span><span class="sxs-lookup"><span data-stu-id="bea8f-151">1 month</span></span>
- <span data-ttu-id="bea8f-152">7 일</span><span class="sxs-lookup"><span data-stu-id="bea8f-152">7 days</span></span>
- <span data-ttu-id="bea8f-153">24시간</span><span class="sxs-lookup"><span data-stu-id="bea8f-153">24 hours</span></span>
- <span data-ttu-id="bea8f-154">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bea8f-154">Custom</span></span>

<span data-ttu-id="bea8f-155">사용자 지정 시간 범위를 선택하면 시작 시간과 종료 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="bea8f-156">hello **사용자** toospecify hello 이름이 나 hello 사용자 계정 이름 (UPN) hello 사용자에 대 한 관심의 필터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="bea8f-157">hello **응용 프로그램** 필터 하면 중요 한 hello 응용 프로그램의 toospecify hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="bea8f-158">hello **클라이언트** 필터 사용 하면 중요 한 hello 장치에 대 한 toospecify 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="bea8f-159">hello **로그인 상태** 필터를 사용 하면 다음 필터는 hello의 tooselect 하나:</span><span class="sxs-lookup"><span data-stu-id="bea8f-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="bea8f-160">모두</span><span class="sxs-lookup"><span data-stu-id="bea8f-160">All</span></span>
- <span data-ttu-id="bea8f-161">성공</span><span class="sxs-lookup"><span data-stu-id="bea8f-161">Success</span></span>
- <span data-ttu-id="bea8f-162">실패</span><span class="sxs-lookup"><span data-stu-id="bea8f-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="bea8f-163">로그인 활동 바로 가기</span><span class="sxs-lookup"><span data-stu-id="bea8f-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="bea8f-164">또한 Active Directory tooAzure hello Azure 포털 하면 두 개의 추가 항목 지점 toosign 기능 작업 데이터:</span><span class="sxs-lookup"><span data-stu-id="bea8f-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="bea8f-165">개요</span><span class="sxs-lookup"><span data-stu-id="bea8f-165">Users and groups</span></span>
- <span data-ttu-id="bea8f-166">Enterprise 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bea8f-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="bea8f-167">사용자 및 그룹 로그인 활동</span><span class="sxs-lookup"><span data-stu-id="bea8f-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="bea8f-168">Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="bea8f-169">사용자의 hello 로그인 패턴 이란?</span><span class="sxs-lookup"><span data-stu-id="bea8f-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="bea8f-170">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="bea8f-171">이러한 로그인의 hello 상태는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bea8f-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="bea8f-172">항목 지점 toothis 데이터는 hello 사용자 로그인에서 그래프 hello **개요** 섹션 아래 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="bea8f-173">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/45.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-174">부호 주간 집계를 표시 하는 hello 사용자 로그인 그래프의 지정된 된 기간 동안 모든 사용자에 대 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="bea8f-175">hello에 대 한 hello 기본 기간 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="bea8f-176">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/46.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-177">Hello 로그인 그래프에서 날짜를 클릭 하는 경우이 날짜에 대 한 hello 로그인 활동의 자세한 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="bea8f-178">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-179">각 행에 선택한 hello 로그인과 같은 대 한 자세한 내용은 hello hello 로그인 활동 목록 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="bea8f-180">누가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-180">Who has signed in?</span></span>
* <span data-ttu-id="bea8f-181">UPN을 관련 hello 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="bea8f-181">What was hello related UPN?</span></span>
* <span data-ttu-id="bea8f-182">어떤 응용 프로그램을 hello에 대 한 로그인의 대상 hello?</span><span class="sxs-lookup"><span data-stu-id="bea8f-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="bea8f-183">Hello에 대 한 로그인의 hello IP 주소는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bea8f-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="bea8f-184">Hello에 대 한 로그인의 hello 상태는 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="bea8f-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="bea8f-185">hello **로그인** 옵션 모든 사용자 로그인의 전체적인 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="bea8f-186">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/51.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="bea8f-187">관리되는 응용 프로그램의 사용량</span><span class="sxs-lookup"><span data-stu-id="bea8f-187">Usage of managed applications</span></span>

<span data-ttu-id="bea8f-188">로그인 데이터의 응용 프로그램 중심 보기를 사용하여 다음과 같은 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="bea8f-189">누가 내 응용 프로그램을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-189">Who is using my applications?</span></span>
* <span data-ttu-id="bea8f-190">Hello 상위 3 개의 응용 프로그램에서 조직 이란?</span><span class="sxs-lookup"><span data-stu-id="bea8f-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="bea8f-191">최근에 응용 프로그램을 롤아웃했습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-191">I have recently rolled out an application.</span></span> <span data-ttu-id="bea8f-192">어떻게 작동하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="bea8f-192">How is it doing?</span></span>

<span data-ttu-id="bea8f-193">항목 지점 toothis 데이터는 hello 상위 3 개의 응용 프로그램에 hello hello 마지막 30 일 보고서 내에서 조직의 **개요** 섹션 아래 **엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="bea8f-194">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/64.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-195">상위 3 응용 프로그램에 대 한 기능 지정된 된 기간 동안에 로그인 하는 hello 응용 프로그램 사용 현황 그래프 주간 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="bea8f-196">hello에 대 한 hello 기본 기간 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="bea8f-197">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/47.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="bea8f-198">원하는 경우에 특정 응용 프로그램에 hello 포커스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="bea8f-199">![보고](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="bea8f-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="bea8f-200">하루에 hello 앱 사용량 그래프를 클릭할 때 hello 로그인 활동의 자세한 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="bea8f-201">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/48.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="bea8f-202">hello **로그인** 옵션 모든 로그인 이벤트 tooyour 응용 프로그램의 전체적인 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="bea8f-203">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/49.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="bea8f-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="bea8f-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bea8f-204">Next steps</span></span>

<span data-ttu-id="bea8f-205">로그인 활동이 오류 코드에 대 한 자세한 tooknow hello를 참조 하십시오 [로그인 활동 보고서의에서 오류 코드 hello Azure Active Directory 포털](active-directory-reporting-activity-sign-ins-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea8f-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

