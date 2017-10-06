---
title: "hello Azure 포털에서에서 보고서를 aaaFind 활동 | Microsoft Docs"
description: "Azure Active Directory 작업 toofind hello Azure 포털에서에서 보고 하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="dd56d-103">Hello Azure 포털에서에서 작업 보고서를 찾기</span><span class="sxs-lookup"><span data-stu-id="dd56d-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="dd56d-104">Azure 포털에서 Azure 클래식 포털 toohello hello 이동 하는, Azure Active Directory (Azure AD) 활동 로그에서 새로운 모양을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="dd56d-105">최근에서 [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), 활동에서 hello Azure 포털에서 작업 하는 hello 리소스의 hello 컨텍스트에서 로그를 볼 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="dd56d-106">이 문서에서는 toofind 보고 하는 hello hello Azure 포털에서에서 Azure 클래식 포털에서에서 사용 하 여는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="dd56d-107">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="dd56d-107">What's new</span></span>

<span data-ttu-id="dd56d-108">Hello Azure 클래식 포털의에서 보고서 범주로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="dd56d-109">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-109">Security reports</span></span>
2.  <span data-ttu-id="dd56d-110">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-110">Activity reports</span></span>
3.  <span data-ttu-id="dd56d-111">통합 앱 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="dd56d-112">활동 및 통합 앱 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-112">Activity and integrated app reports</span></span>

<span data-ttu-id="dd56d-113">컨텍스트 기반 hello Azure 포털에서에서 보고를 위해 기존 보고서는 단일 보기에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="dd56d-114">단일, 기본 API hello 데이터 toohello 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="dd56d-115">hello에이 보기는 toosee **Azure Active Directory** 블레이드 아래에서 **활동**선택, **감사 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="dd56d-116">![감사 로그](./media/active-directory-reporting-migration/482.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="dd56d-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="dd56d-117">이 보기에서 보고서를 다음 hello 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="dd56d-118">감사 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-118">Audit report</span></span>
-   <span data-ttu-id="dd56d-119">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-119">Password reset activity</span></span>
-   <span data-ttu-id="dd56d-120">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-120">Password reset registration activity</span></span>
-   <span data-ttu-id="dd56d-121">셀프 서비스 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="dd56d-121">Self-service groups activity</span></span>
-   <span data-ttu-id="dd56d-122">Office 365 그룹 이름 변경</span><span class="sxs-lookup"><span data-stu-id="dd56d-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="dd56d-123">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-123">Account provisioning activity</span></span>
-   <span data-ttu-id="dd56d-124">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="dd56d-124">Password rollover status</span></span>
-   <span data-ttu-id="dd56d-125">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="dd56d-125">Account provisioning errors</span></span>


<span data-ttu-id="dd56d-126">hello 응용 프로그램 사용 현황 보고서가 향상 되었으며 및 hello에 포함 된 **로그인** 보기.</span><span class="sxs-lookup"><span data-stu-id="dd56d-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="dd56d-127">hello에이 보기는 toosee **Azure Active Directory** 블레이드 아래에서 **활동**선택, **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="dd56d-128">![로그인 보기](./media/active-directory-reporting-migration/483.png "로그인 보기")</span><span class="sxs-lookup"><span data-stu-id="dd56d-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="dd56d-129">hello **로그인** 뷰에 모든 사용자 로그인이 포함 됩니다. 이 정보 tooget 응용 프로그램 사용 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="dd56d-130">또한 hello에 응용 프로그램 사용 정보를 볼 수 있습니다 **엔터프라이즈 응용 프로그램** hello에 개요 **관리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="dd56d-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="dd56d-131">![Enterprise 응용 프로그램](./media/active-directory-reporting-migration/484.png "Enterprise 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="dd56d-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="dd56d-132">특정 보고서에 액세스</span><span class="sxs-lookup"><span data-stu-id="dd56d-132">Access a specific report</span></span>

<span data-ttu-id="dd56d-133">Hello Azure 포털에서는 단일 보기를 제공 하지만 또한 살펴보면 특정 보고서.</span><span class="sxs-lookup"><span data-stu-id="dd56d-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="dd56d-134">감사 로그</span><span class="sxs-lookup"><span data-stu-id="dd56d-134">Audit logs</span></span>

<span data-ttu-id="dd56d-135">Hello Azure 포털에서에서 응답 toocustomer 피드백에 고급 필터링 tooaccess hello 원하는 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="dd56d-136">하나의 필터를 사용할 수는 *활동 범주*, Azure AD 로그인 hello 다양 한 유형의 작업을 나열 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="dd56d-137">toonarrow 결과 대 한 원하는 toowhat, 범주를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="dd56d-138">예를 들어 활동 관련된 tooself 서비스 암호 재설정에만 관심이 경우 선택할 수 있습니다 hello **셀프 서비스 암호 관리** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="dd56d-139">표시 되는 hello 범주에서 작업 하는 hello 리소스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="dd56d-140">![Hello 필터 감사 로그 페이지의 옵션 범주](./media/active-directory-reporting-migration/06.png "hello 필터 감사 로그 페이지의 옵션 범주")</span><span class="sxs-lookup"><span data-stu-id="dd56d-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="dd56d-141">작업 범주에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-141">Activity categories include:</span></span>

- <span data-ttu-id="dd56d-142">핵심 디렉터리</span><span class="sxs-lookup"><span data-stu-id="dd56d-142">Core Directory</span></span>
- <span data-ttu-id="dd56d-143">셀프 서비스 암호 관리</span><span class="sxs-lookup"><span data-stu-id="dd56d-143">Self-service Password Management</span></span>
- <span data-ttu-id="dd56d-144">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="dd56d-144">Self-service Group Management</span></span>
- <span data-ttu-id="dd56d-145">계정 프로비전</span><span class="sxs-lookup"><span data-stu-id="dd56d-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="dd56d-146">응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="dd56d-146">Application usage</span></span>

<span data-ttu-id="dd56d-147">tooview 아래에서 모든 앱에 대 한 또는 단일 앱에 대 한 응용 프로그램 사용에 대 한 세부 정보 **활동**선택, **로그인**. toonarrow hello 결과 사용자 이름 또는 응용 프로그램 이름을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="dd56d-148">![로그인 이벤트 필터링 페이지](./media/active-directory-reporting-migration/07.png "로그인 이벤트 필터링 페이지")</span><span class="sxs-lookup"><span data-stu-id="dd56d-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="dd56d-149">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="dd56d-150">Azure AD 비정상 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="dd56d-151">Azure AD의 비정상적인 활동 보안 통합된 tooprovide 된 hello Azure 클래식 포털에서에서 보고서 하나, 중앙 뷰부터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="dd56d-152">이 보기에는 Azure AD가 감지하여 보고할 수 있는 모든 보안 관련 위험 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="dd56d-153">다음 표에서 hello hello Azure AD의 비정상적인 활동 보안 보고서 및 hello Azure 포털에서에서 해당 위험 이벤트 유형을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="dd56d-154">Azure AD 비정상 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="dd56d-155">ID 보호 위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="dd56d-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="dd56d-156">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="dd56d-156">Users with leaked credentials</span></span> | <span data-ttu-id="dd56d-157">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="dd56d-157">Leaked credentials</span></span> |
| <span data-ttu-id="dd56d-158">비정상적인 로그인 작업</span><span class="sxs-lookup"><span data-stu-id="dd56d-158">Irregular sign-in activity</span></span> | <span data-ttu-id="dd56d-159">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="dd56d-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="dd56d-160">감염 가능성이 있는 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="dd56d-161">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="dd56d-162">알 수 없는 원본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="dd56d-163">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="dd56d-164">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="dd56d-165">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="dd56d-166">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="dd56d-167">Azure AD의 비정상적인 활동 보안 다음 hello 보고 hello Azure 포털의에서 위험 이벤트로 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="dd56d-168">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="dd56d-169">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="dd56d-170">이러한 보고서는 hello Azure 클래식 포털에서에서 계속 제공 하지만 향후 hello에 중단 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="dd56d-171">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd56d-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="dd56d-172">검색된 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="dd56d-172">Detected risk events</span></span>

<span data-ttu-id="dd56d-173">Hello에 검색 된 위험 이벤트에 대 한 보고서에 액세스할 수 hello Azure 포털에서에서 **Azure Active Directory** 블레이드 아래 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="dd56d-174">Hello 다음 보고서에서에서 검색 된 위험 이벤트가 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="dd56d-175">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="dd56d-175">Users at Risk</span></span>
- <span data-ttu-id="dd56d-176">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="dd56d-176">Risky Sign-ins</span></span>

<span data-ttu-id="dd56d-177">![보안 보고서](./media/active-directory-reporting-migration/04.png "보안 보고서")</span><span class="sxs-lookup"><span data-stu-id="dd56d-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="dd56d-178">보안 보고서에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd56d-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="dd56d-179">Hello Azure Active Directory 포털에서 위험 보안 보고서에 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="dd56d-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="dd56d-180">Hello Azure Active Directory 포털에서 위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="dd56d-181">Hello hello Azure 포털 및 Azure 클래식 포털에서에서 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="dd56d-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="dd56d-182">이 섹션의 표 hello hello Azure 클래식 포털에서에서 기존 보고서를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="dd56d-183">또한를 가져오는 방법을 설명 hello hello Azure 포털에서에서 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="dd56d-184">모든 tooview hello에 데이터 감사 **Azure Active Directory** 블레이드 아래 **활동**, 너무 이동**감사 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="dd56d-185">![감사 로그](./media/active-directory-reporting-migration/61.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="dd56d-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="dd56d-186">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="dd56d-186">Azure classic portal</span></span>                 | <span data-ttu-id="dd56d-187">toofind hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="dd56d-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="dd56d-188">감사 로그</span><span class="sxs-lookup"><span data-stu-id="dd56d-188">Audit logs</span></span>                           | <span data-ttu-id="dd56d-189">**작업 범주**로 **핵심 디렉터리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="dd56d-190">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-190">Password reset activity</span></span>              | <span data-ttu-id="dd56d-191">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="dd56d-192">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-192">Password reset registration activity</span></span> | <span data-ttu-id="dd56d-193">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="dd56d-194">셀프 서비스 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="dd56d-194">Self-service groups activity</span></span>         | <span data-ttu-id="dd56d-195">**작업 범주**로 **셀프 서비스 그룹 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="dd56d-196">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="dd56d-196">Account provisioning activity</span></span>        | <span data-ttu-id="dd56d-197">**작업 범주**로 **계정 사용자 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="dd56d-198">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="dd56d-198">Password rollover status</span></span>             | <span data-ttu-id="dd56d-199">**작업 범주**로 **자동 앱 암호 롤오버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="dd56d-200">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="dd56d-200">Account provisioning errors</span></span>          | <span data-ttu-id="dd56d-201">**작업 범주**로 **계정 사용자 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="dd56d-202">Office 365 그룹 이름 변경</span><span class="sxs-lookup"><span data-stu-id="dd56d-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="dd56d-203">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="dd56d-204">**작업 리소스 유형**으로 **그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="dd56d-205">**작업 원본**으로 **O365 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="dd56d-206">tooview hello **응용 프로그램 사용** hello에 보고서 **Azure Active Directory** 블레이드 아래 **관리**선택, **엔터프라이즈 응용 프로그램**를 선택한 후 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="dd56d-207">![Enterprise 응용 프로그램 로그인 보고서](./media/active-directory-reporting-migration/199.png "Enterprise 응용 프로그램 로그인 보고서")</span><span class="sxs-lookup"><span data-stu-id="dd56d-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd56d-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd56d-208">Next steps</span></span>

<span data-ttu-id="dd56d-209">Reporting의 개요를 참조 hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd56d-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
