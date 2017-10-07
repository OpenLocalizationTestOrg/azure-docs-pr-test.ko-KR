---
title: "hello Azure Active Directory 포털에서 aaaAudit 활동 보고 | Microsoft Docs"
description: "소개 toohello 감사 hello Azure Active Directory 포털에서 활동 보고서"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="d61d5-103">감사 hello Azure Active Directory 포털에서 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="d61d5-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="d61d5-104">Azure Active Directory (Azure AD)에 보고를 사용 하면 환경의 어떻게 진행 되는 toodetermine 필요한 hello 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="d61d5-105">Azure AD의 보고 아키텍처 hello hello 다음과 같은 구성 요소가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="d61d5-106">**활동**</span><span class="sxs-lookup"><span data-stu-id="d61d5-106">**Activity**</span></span> 
    - <span data-ttu-id="d61d5-107">**로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="d61d5-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="d61d5-108">**감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 작업 정보</span><span class="sxs-lookup"><span data-stu-id="d61d5-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="d61d5-109">**보안**</span><span class="sxs-lookup"><span data-stu-id="d61d5-109">**Security**</span></span> 
    - <span data-ttu-id="d61d5-110">**위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="d61d5-111">자세한 내용은 위험한 로그인을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d61d5-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="d61d5-112">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="d61d5-113">자세한 내용은 위험 플래그가 지정된 사용자를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d61d5-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="d61d5-114">이 항목에서는 hello 감사 작업의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="d61d5-115">Hello 데이터에 액세스할 수 있는 사용자?</span><span class="sxs-lookup"><span data-stu-id="d61d5-115">Who can access hello data?</span></span>
* <span data-ttu-id="d61d5-116">Hello 보안 판독기 또는 보안 관리자 역할의 사용자</span><span class="sxs-lookup"><span data-stu-id="d61d5-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="d61d5-117">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="d61d5-117">Global Admins</span></span>
* <span data-ttu-id="d61d5-118">개별 사용자(비관리자)는 자신의 활동을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="d61d5-119">감사 로그</span><span class="sxs-lookup"><span data-stu-id="d61d5-119">Audit logs</span></span>

<span data-ttu-id="d61d5-120">Azure Active Directory에 hello 감사 로그는 규정 준수에 대 한 시스템 활동의 레코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="d61d5-121">데이터 감사 하 여 첫 번째 항목 지점 tooall는 **감사 로그** hello에 **활동** 섹션 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="d61d5-122">![감사 로그](./media/active-directory-reporting-activity-audit-logs/61.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="d61d5-123">감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="d61d5-124">hello 발생의 hello 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="d61d5-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="d61d5-125">초기자 hello / 행위자 (*가*) 활동</span><span class="sxs-lookup"><span data-stu-id="d61d5-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="d61d5-126">활동 hello (*어떤*)</span><span class="sxs-lookup"><span data-stu-id="d61d5-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="d61d5-127">hello 대상</span><span class="sxs-lookup"><span data-stu-id="d61d5-127">hello target</span></span>

<span data-ttu-id="d61d5-128">![감사 로그](./media/active-directory-reporting-activity-audit-logs/18.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="d61d5-129">클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="d61d5-130">![감사 로그](./media/active-directory-reporting-activity-audit-logs/19.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="d61d5-131">이 toodisplay 추가 필드를 사용 하면 하거나 이미 표시 되는 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="d61d5-132">![감사 로그](./media/active-directory-reporting-activity-audit-logs/21.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="d61d5-133">Hello 목록 뷰에서 항목을 클릭 하 여 항목에 대 한 모든 사용 가능한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="d61d5-134">![감사 로그](./media/active-directory-reporting-activity-audit-logs/22.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="d61d5-135">감사 로그 필터링</span><span class="sxs-lookup"><span data-stu-id="d61d5-135">Filtering audit logs</span></span>

<span data-ttu-id="d61d5-136">hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 감사 데이터를 보고.</span><span class="sxs-lookup"><span data-stu-id="d61d5-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="d61d5-137">날짜 범위</span><span class="sxs-lookup"><span data-stu-id="d61d5-137">Date range</span></span>
- <span data-ttu-id="d61d5-138">초기자(작업자)</span><span class="sxs-lookup"><span data-stu-id="d61d5-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="d61d5-139">Category</span><span class="sxs-lookup"><span data-stu-id="d61d5-139">Category</span></span>
- <span data-ttu-id="d61d5-140">활동 리소스 종류</span><span class="sxs-lookup"><span data-stu-id="d61d5-140">Activity resource type</span></span>
- <span data-ttu-id="d61d5-141">작업</span><span class="sxs-lookup"><span data-stu-id="d61d5-141">Activity</span></span>

<span data-ttu-id="d61d5-142">![감사 로그](./media/active-directory-reporting-activity-audit-logs/23.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="d61d5-143">hello **날짜 범위** 필터 사용 tooyou toodefine hello에 대 한 시간 범위는 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="d61d5-144">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-144">Possible values are:</span></span>

- <span data-ttu-id="d61d5-145">1개월</span><span class="sxs-lookup"><span data-stu-id="d61d5-145">1 month</span></span>
- <span data-ttu-id="d61d5-146">7 일</span><span class="sxs-lookup"><span data-stu-id="d61d5-146">7 days</span></span>
- <span data-ttu-id="d61d5-147">24시간</span><span class="sxs-lookup"><span data-stu-id="d61d5-147">24 hours</span></span>
- <span data-ttu-id="d61d5-148">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d61d5-148">Custom</span></span>

<span data-ttu-id="d61d5-149">사용자 지정 시간 범위를 선택하면 시작 시간과 종료 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="d61d5-150">hello **에 의해 시작** 필터를 사용 하면 있습니다 toodefine 행위자의 이름 또는 유니버설 보안 주체 이름 (UPN)입니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="d61d5-151">hello **범주** 필터를 사용 하면 다음 필터는 hello의 tooselect 하나:</span><span class="sxs-lookup"><span data-stu-id="d61d5-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="d61d5-152">모두</span><span class="sxs-lookup"><span data-stu-id="d61d5-152">All</span></span>
- <span data-ttu-id="d61d5-153">핵심 범주</span><span class="sxs-lookup"><span data-stu-id="d61d5-153">Core category</span></span>
- <span data-ttu-id="d61d5-154">핵심 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d61d5-154">Core directory</span></span>
- <span data-ttu-id="d61d5-155">셀프 서비스 암호 관리</span><span class="sxs-lookup"><span data-stu-id="d61d5-155">Self-service password management</span></span>
- <span data-ttu-id="d61d5-156">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="d61d5-156">Self-service group management</span></span>
- <span data-ttu-id="d61d5-157">계정 프로비전 - 자동화된 암호 롤오버</span><span class="sxs-lookup"><span data-stu-id="d61d5-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="d61d5-158">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="d61d5-158">Invited users</span></span>
- <span data-ttu-id="d61d5-159">MIM 서비스</span><span class="sxs-lookup"><span data-stu-id="d61d5-159">MIM service</span></span>
- <span data-ttu-id="d61d5-160">ID 보호</span><span class="sxs-lookup"><span data-stu-id="d61d5-160">Identity Protection</span></span>
- <span data-ttu-id="d61d5-161">B2C</span><span class="sxs-lookup"><span data-stu-id="d61d5-161">B2C</span></span>

<span data-ttu-id="d61d5-162">hello **활동 리소스 종류** 필터를 사용 하면 tooselect hello 다음 중 하나를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="d61d5-163">모두</span><span class="sxs-lookup"><span data-stu-id="d61d5-163">All</span></span> 
- <span data-ttu-id="d61d5-164">그룹</span><span class="sxs-lookup"><span data-stu-id="d61d5-164">Group</span></span>
- <span data-ttu-id="d61d5-165">디렉터리</span><span class="sxs-lookup"><span data-stu-id="d61d5-165">Directory</span></span>
- <span data-ttu-id="d61d5-166">사용자</span><span class="sxs-lookup"><span data-stu-id="d61d5-166">User</span></span>
- <span data-ttu-id="d61d5-167">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d61d5-167">Application</span></span>
- <span data-ttu-id="d61d5-168">정책</span><span class="sxs-lookup"><span data-stu-id="d61d5-168">Policy</span></span>
- <span data-ttu-id="d61d5-169">장치</span><span class="sxs-lookup"><span data-stu-id="d61d5-169">Device</span></span>
- <span data-ttu-id="d61d5-170">기타</span><span class="sxs-lookup"><span data-stu-id="d61d5-170">Other</span></span>

<span data-ttu-id="d61d5-171">선택 하는 경우 **그룹** 으로 **활동 리소스 종류**, 수 있는 추가 필터 범주 tooalso를 얻게 제공는 **소스**:</span><span class="sxs-lookup"><span data-stu-id="d61d5-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="d61d5-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="d61d5-172">Azure AD</span></span>
- <span data-ttu-id="d61d5-173">O365</span><span class="sxs-lookup"><span data-stu-id="d61d5-173">O365</span></span>


<span data-ttu-id="d61d5-174">hello **활동** 필터 hello 범주 및 작업 리소스 유형 선택한 내용에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="d61d5-175">Toosee 모두 선택 하거나 특정 활동을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="d61d5-176">Graph API https://graph.windows.net/$ hello tenantdomain/활동/auditActivityTypes를 사용 하 여 모든 감사 활동의 hello 목록을 가져올 수 있습니까? api 버전 = beta, 여기서 $tenantdomain = 도메인 이름 또는 toohello 문서를 참조 [감사 보고서 이벤트](active-directory-reporting-audit-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="d61d5-177">감사 로그 바로 가기</span><span class="sxs-lookup"><span data-stu-id="d61d5-177">Audit logs shortcuts</span></span>

<span data-ttu-id="d61d5-178">또한 너무**Azure Active Directory**, hello Azure 포털을 제공 두 개의 추가 진입점 tooaudit 데이터:</span><span class="sxs-lookup"><span data-stu-id="d61d5-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="d61d5-179">개요</span><span class="sxs-lookup"><span data-stu-id="d61d5-179">Users and groups</span></span>
- <span data-ttu-id="d61d5-180">Enterprise 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d61d5-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="d61d5-181">사용자 및 그룹 감사 로그</span><span class="sxs-lookup"><span data-stu-id="d61d5-181">Users and groups audit logs</span></span>

<span data-ttu-id="d61d5-182">사용자와 그룹 기반 감사 보고서를 같은 tooquestions 답변을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="d61d5-183">어떤 종류의 업데이트 된 사용자가 적용 된 hello?</span><span class="sxs-lookup"><span data-stu-id="d61d5-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="d61d5-184">얼마나 많은 사용자가 변경되었나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-184">How many users were changed?</span></span>

- <span data-ttu-id="d61d5-185">얼마나 많은 암호가 변경되었나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-185">How many passwords were changed?</span></span>

- <span data-ttu-id="d61d5-186">관리자가 디렉터리에서 무엇을 수행했나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="d61d5-187">추가 된 hello 그룹 이란?</span><span class="sxs-lookup"><span data-stu-id="d61d5-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="d61d5-188">멤버 자격이 변경된 그룹이 있나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="d61d5-189">변경 된 그룹의 소유자 hello?</span><span class="sxs-lookup"><span data-stu-id="d61d5-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="d61d5-190">어떤 라이선스 tooa 그룹 또는 사용자 지정 된?</span><span class="sxs-lookup"><span data-stu-id="d61d5-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="d61d5-191">아래에 있는 필터링 된 보기를 찾을 수 tooreview 감사 관련된 toousers 및 그룹 데이터를 원하는 경우 **감사 로그** hello에 **활동** hello의 섹션 **사용자 및 그룹**.</span><span class="sxs-lookup"><span data-stu-id="d61d5-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="d61d5-192">이 진입점에는 미리 선택된 **활동 리소스 종류**로 **사용자 및 그룹**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="d61d5-193">![감사 로그](./media/active-directory-reporting-activity-audit-logs/93.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="d61d5-194">Enterprise 응용 프로그램 감사 로그</span><span class="sxs-lookup"><span data-stu-id="d61d5-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="d61d5-195">응용 프로그램을 기반으로 감사 보고서를 같은 tooquestions 답변을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="d61d5-196">추가 되거나 업데이트 된 하는 hello 응용 프로그램은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d61d5-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="d61d5-197">제거 된 hello 응용 프로그램은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d61d5-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="d61d5-198">응용 프로그램에 대한 서비스 원칙이 변경되었나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="d61d5-199">응용 프로그램의 hello 이름은 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="d61d5-200">누가 동의 tooan 응용 프로그램을 줬?</span><span class="sxs-lookup"><span data-stu-id="d61d5-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="d61d5-201">아래에 있는 필터링 된 보기를 찾을 수 tooreview 관련된 tooyour 응용 프로그램은 데이터 감사를 원하는 경우 **감사 로그** hello에 **활동** hello의 섹션 **엔터프라이즈 응용 프로그램**  블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="d61d5-202">이 진입점에는 미리 선택된 **활동 리소스 종류**인 **엔터프라이즈 응용 프로그램**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="d61d5-203">![감사 로그](./media/active-directory-reporting-activity-audit-logs/134.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="d61d5-204">Toojust 아래로 더 이상이 보기를 필터링 할 수 있습니다 **그룹** 또는 그냥 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="d61d5-205">![감사 로그](./media/active-directory-reporting-activity-audit-logs/25.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="d61d5-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="d61d5-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d61d5-206">Next steps</span></span>

<span data-ttu-id="d61d5-207">Reporting의 개요를 참조 hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

