---
title: "Azure Portal에서 작업 보고서 찾기 | Microsoft Docs"
description: "Azure Portal에서 Azure Active Directory 작업 보고서를 찾는 방법을 알아봅니다."
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
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="af136-103">Azure Portal에서 작업 보고서 찾기</span><span class="sxs-lookup"><span data-stu-id="af136-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="af136-104">Azure 클래식 포털에서 Azure Portal로 전환하면 새로운 Azure AD(Azure Active Directory) 작업 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="af136-105">최근에 [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/)을 통해 Azure Portal에서 작업 중인 리소스와 관련된 작업 로그를 보는 방법을 설명드렸습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="af136-106">이 문서에서는 Azure 클래식 포털 및 Azure Portal에서 사용한 보고서를 찾는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="af136-107">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="af136-107">What's new</span></span>

<span data-ttu-id="af136-108">Azure 클래식 포털의 보고서는 다음과 같은 범주로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="af136-109">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-109">Security reports</span></span>
2.  <span data-ttu-id="af136-110">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-110">Activity reports</span></span>
3.  <span data-ttu-id="af136-111">통합 앱 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="af136-112">활동 및 통합 앱 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-112">Activity and integrated app reports</span></span>

<span data-ttu-id="af136-113">Azure Portal의 컨텍스트 기반 보고서의 경우 기존 보고서가 단일 보기에 병합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="af136-114">단일 기본 API는 보기에 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="af136-115">이 보기를 보려면 **Azure Active Directory** 블레이드의 **작업**에서 **감사 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="af136-116">![감사 로그](./media/active-directory-reporting-migration/482.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="af136-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="af136-117">다음과 같은 보고서가 이 보기에 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="af136-118">감사 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-118">Audit report</span></span>
-   <span data-ttu-id="af136-119">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="af136-119">Password reset activity</span></span>
-   <span data-ttu-id="af136-120">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="af136-120">Password reset registration activity</span></span>
-   <span data-ttu-id="af136-121">셀프 서비스 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="af136-121">Self-service groups activity</span></span>
-   <span data-ttu-id="af136-122">Office 365 그룹 이름 변경</span><span class="sxs-lookup"><span data-stu-id="af136-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="af136-123">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="af136-123">Account provisioning activity</span></span>
-   <span data-ttu-id="af136-124">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="af136-124">Password rollover status</span></span>
-   <span data-ttu-id="af136-125">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="af136-125">Account provisioning errors</span></span>


<span data-ttu-id="af136-126">개선된 응용 프로그램 사용 현황 보고서가 **로그인** 보기에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="af136-127">이 보기를 보려면 **Azure Active Directory** 블레이드의 **작업**에서 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="af136-128">![로그인 보기](./media/active-directory-reporting-migration/483.png "로그인 보기")</span><span class="sxs-lookup"><span data-stu-id="af136-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="af136-129">**로그인** 보기에는 모든 사용자 로그인이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="af136-130">이 정보를 사용하여 응용 프로그램 사용 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="af136-131">**관리** 섹션의 **Enterprise 응용 프로그램** 개요에서도 응용 프로그램 사용 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="af136-132">![Enterprise 응용 프로그램](./media/active-directory-reporting-migration/484.png "Enterprise 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="af136-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="af136-133">특정 보고서에 액세스</span><span class="sxs-lookup"><span data-stu-id="af136-133">Access a specific report</span></span>

<span data-ttu-id="af136-134">Azure Portal에서 단일 보기를 제공하지만 사용자는 특정 보고서를 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="af136-135">감사 로그</span><span class="sxs-lookup"><span data-stu-id="af136-135">Audit logs</span></span>

<span data-ttu-id="af136-136">고객 피드백에 대한 응답으로 Azure Portal에서 고급 필터링을 사용하여 원하는 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="af136-137">사용할 수 있는 필터 중 하나는 Azure AD의 다양한 작업 로그 유형을 나열하는 *작업 범주*입니다.</span><span class="sxs-lookup"><span data-stu-id="af136-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="af136-138">원하는 내용만 표시되도록 결과 범위를 좁히려면 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="af136-139">예를 들어 셀프 서비스 암호 재설정과 관련된 작업만 보려면 **셀프 서비스 암호 관리** 범주를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="af136-140">사용자에게 표시되는 범주는 사용자가 현재 작업 중인 리소스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="af136-141">![필터 감사 로그 페이지의 범주 옵션](./media/active-directory-reporting-migration/06.png "필터 감사 로그 페이지의 범주 옵션")</span><span class="sxs-lookup"><span data-stu-id="af136-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="af136-142">작업 범주에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-142">Activity categories include:</span></span>

- <span data-ttu-id="af136-143">핵심 디렉터리</span><span class="sxs-lookup"><span data-stu-id="af136-143">Core Directory</span></span>
- <span data-ttu-id="af136-144">셀프 서비스 암호 관리</span><span class="sxs-lookup"><span data-stu-id="af136-144">Self-service Password Management</span></span>
- <span data-ttu-id="af136-145">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="af136-145">Self-service Group Management</span></span>
- <span data-ttu-id="af136-146">계정 프로비전</span><span class="sxs-lookup"><span data-stu-id="af136-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="af136-147">응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="af136-147">Application usage</span></span>

<span data-ttu-id="af136-148">모든 앱 또는 단일 앱의 응용 프로그램 사용 현황에 대한 세부 정보를 보려면 **작업**에서 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="af136-149">결과의 범위를 좁히려면 사용자 이름 또는 응용 프로그램 이름을 필터링하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="af136-150">![로그인 이벤트 필터링 페이지](./media/active-directory-reporting-migration/07.png "로그인 이벤트 필터링 페이지")</span><span class="sxs-lookup"><span data-stu-id="af136-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="af136-151">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="af136-152">Azure AD 비정상 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="af136-153">하나의 중앙 보기를 제공하도록 Azure 클래식 포털의 Azure AD 비정상 작업 보안 보고서가 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="af136-154">이 보기에는 Azure AD가 감지하여 보고할 수 있는 모든 보안 관련 위험 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="af136-155">다음 테이블에는 Azure Portal의 Azure AD 비정상 작업 보안 보고서 및 해당하는 위험 이벤트 형식이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="af136-156">Azure AD 비정상 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="af136-157">ID 보호 위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="af136-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="af136-158">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="af136-158">Users with leaked credentials</span></span> | <span data-ttu-id="af136-159">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="af136-159">Leaked credentials</span></span> |
| <span data-ttu-id="af136-160">비정상적인 로그인 작업</span><span class="sxs-lookup"><span data-stu-id="af136-160">Irregular sign-in activity</span></span> | <span data-ttu-id="af136-161">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="af136-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="af136-162">감염 가능성이 있는 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="af136-163">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="af136-164">알 수 없는 원본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="af136-165">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="af136-166">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="af136-167">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="af136-168">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="af136-169">다음 Azure AD 비정상 작업 보안 보고서는 Azure Portal에 위험 이벤트로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="af136-170">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="af136-171">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="af136-172">이러한 보고서는 아직은 Azure 클래식 포털에 제공되지만 어느 시점부터는 더 이상 제공되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af136-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="af136-173">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af136-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="af136-174">검색된 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="af136-174">Detected risk events</span></span>

<span data-ttu-id="af136-175">Azure Portal의 **Azure Active Directory** 블레이드 **보안** 섹션에서는 검색된 위험 이벤트에 대한 보고서에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="af136-176">검색된 위험 이벤트는 다음과 같은 보고서에서 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="af136-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="af136-177">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="af136-177">Users at Risk</span></span>
- <span data-ttu-id="af136-178">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="af136-178">Risky Sign-ins</span></span>

<span data-ttu-id="af136-179">![보안 보고서](./media/active-directory-reporting-migration/04.png "보안 보고서")</span><span class="sxs-lookup"><span data-stu-id="af136-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="af136-180">보안 보고서에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af136-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="af136-181">Azure Active Directory 포털의 위험에 노출된 사용자 보안 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="af136-182">Azure Active Directory 포털의 위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="af136-183">Azure 클래식 포털 및 Azure Portal의 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="af136-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="af136-184">이 섹션의 테이블에는 Azure 클래식 포털의 기존 보고서가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="af136-185">또한 Azure Portal에서 동일한 정보를 얻는 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af136-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="af136-186">모든 감사 데이터를 보려면 **Azure Active Directory** 블레이드의 **작업**에서 **감사 로그**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="af136-187">![감사 로그](./media/active-directory-reporting-migration/61.png "감사 로그")</span><span class="sxs-lookup"><span data-stu-id="af136-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="af136-188">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="af136-188">Azure classic portal</span></span>                 | <span data-ttu-id="af136-189">Azure Portal에서 찾으려면</span><span class="sxs-lookup"><span data-stu-id="af136-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="af136-190">감사 로그</span><span class="sxs-lookup"><span data-stu-id="af136-190">Audit logs</span></span>                           | <span data-ttu-id="af136-191">**작업 범주**로 **핵심 디렉터리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="af136-192">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="af136-192">Password reset activity</span></span>              | <span data-ttu-id="af136-193">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="af136-194">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="af136-194">Password reset registration activity</span></span> | <span data-ttu-id="af136-195">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="af136-196">셀프 서비스 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="af136-196">Self-service groups activity</span></span>         | <span data-ttu-id="af136-197">**작업 범주**로 **셀프 서비스 그룹 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="af136-198">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="af136-198">Account provisioning activity</span></span>        | <span data-ttu-id="af136-199">**작업 범주**로 **계정 사용자 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="af136-200">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="af136-200">Password rollover status</span></span>             | <span data-ttu-id="af136-201">**작업 범주**로 **자동 앱 암호 롤오버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="af136-202">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="af136-202">Account provisioning errors</span></span>          | <span data-ttu-id="af136-203">**작업 범주**로 **계정 사용자 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="af136-204">Office 365 그룹 이름 변경</span><span class="sxs-lookup"><span data-stu-id="af136-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="af136-205">**작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="af136-206">**작업 리소스 유형**으로 **그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="af136-207">**작업 원본**으로 **O365 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="af136-208">**응용 프로그램 사용 현황** 보고서를 보려면 **Azure Active Directory** 블레이드의 **관리**에서 **Enterprise 응용 프로그램**을 선택한 다음 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af136-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="af136-209">![Enterprise 응용 프로그램 로그인 보고서](./media/active-directory-reporting-migration/199.png "Enterprise 응용 프로그램 로그인 보고서")</span><span class="sxs-lookup"><span data-stu-id="af136-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="af136-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af136-210">Next steps</span></span>

<span data-ttu-id="af136-211">보고 개요는 [Azure Active Directory 보고](active-directory-reporting-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af136-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
