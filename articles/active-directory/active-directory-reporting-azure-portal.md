---
title: Active Directory reporting aaaAzure | Microsoft Docs
description: "Azure Active Directory 보고에 대한 일반적 개요를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="4316d-103">Azure Active Directory 보고</span><span class="sxs-lookup"><span data-stu-id="4316d-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="4316d-104">Azure Active Directory 보고 기능을 사용하면 환경이 작동하는 방법에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="4316d-105">제공 된 hello 데이터를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="4316d-106">사용자가 앱과 서비스를 활용하는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="4316d-107">사용자 환경의 hello 상태에 영향을 미치는 잠재적인 위험을 검색</span><span class="sxs-lookup"><span data-stu-id="4316d-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="4316d-108">사용자가 자신의 작업을 완료하지 못하게 하는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="4316d-109">hello 보고 아키텍처는 두 가지 주요 사항에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="4316d-110">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-110">Security reports</span></span>
- <span data-ttu-id="4316d-111">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-111">Activity reports</span></span>

![보고](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="4316d-113">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-113">Security reports</span></span>

<span data-ttu-id="4316d-114">Azure Active Directory에서 hello 보안 보고서는 조직의 identities tooprotect 있습니다를 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="4316d-115">Azure Active Directory에는 두 가지 유형의 보안 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="4316d-116">**위험에 대 한 플래그가 지정 된 사용자가** -hello에서 [위험 보안 보고서에 대 한 플래그가 지정 된 사용자](active-directory-reporting-security-user-at-risk.md), 손상 되었을 수 있는 사용자 계정의 개요를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="4316d-117">**위험한 로그인** -hello로 [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md), 장애가 있는 사용자에 의해 수행 된 로그인 시도 사용자 계정의 올바른 소유자를 하지 hello에 대 한 표시기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="4316d-118">**어떤 Azure AD 라이선스가 tooaccess 보안 보고서 필요 한가요?**</span><span class="sxs-lookup"><span data-stu-id="4316d-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="4316d-119">모든 Azure Active Directory 버전에서 위험 플래그가 지정된 사용자 보고서 및 위험한 로그인 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="4316d-120">그러나 보고서 세분성 수준의 hello hello 버전 간에 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="4316d-121">Hello에 **Azure Active Directory Free 및 Basic edition**, 위험 및 위험한 로그인에 대 한 플래그가 지정 된 사용자 목록이 이미 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="4316d-122">hello **Azure Active Directory 프리미엄 1** edition 확장이 모델도 tooexamine를 사용 하 여 각 보고서에 대해 검색 된 위험 이벤트 원본으로 사용 하는 hello의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="4316d-123">hello **Azure Active Directory 프리미엄 2** 버전은 hello로 가장 자세한 위험 이벤트 원본으로 사용 하는 hello에 대 한 정보 및이 통해 있습니다 tooconfigured 자동으로 응답 하는 tooconfigure 보안 정책 제공 위험 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="4316d-124">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-124">Activity reports</span></span>

<span data-ttu-id="4316d-125">Azure Active Directory에는 두 가지 유형의 활동 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="4316d-126">**감사 로그** -hello [감사 로그를 작업 보고서](active-directory-reporting-activity-audit-logs.md) 테 넌 트에 수행 된 모든 태스크의 toohello 기록을 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="4316d-127">**로그인** -hello로 [로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)를 확인할 수 있습니다, hello 감사 로그 보고서에서 보고 하는 hello 작업을 수행한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="4316d-128">hello **감사 로그 보고서** 규정 준수 위한 레코드 시스템 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="4316d-129">다른 사용자에 게 적절 한 hello 데이터 사용 하면 tooaddress 일반적인 시나리오와 같은 제공.</span><span class="sxs-lookup"><span data-stu-id="4316d-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="4316d-130">다른 사용자가 내 테 넌 트에 액세스 tooan 관리 그룹을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="4316d-131">이들에게 액세스 권한을 부여한 사람을 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-131">Who gave them access?</span></span> 

- <span data-ttu-id="4316d-132">특정 앱에 로그인 하는 사용자의 tooknow hello 목록을 원하는 I 이후 최근에 등록 된 응용 프로그램 hello 및 tooknow 잘 수행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="4316d-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="4316d-133">내 테 넌 트에 tooknow 개수 암호 재설정 발생 하 고 원합니다</span><span class="sxs-lookup"><span data-stu-id="4316d-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="4316d-134">**어떤 Azure AD 라이선스가 tooaccess hello 감사 로그 보고서 필요 한가요?**</span><span class="sxs-lookup"><span data-stu-id="4316d-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="4316d-135">라이선스를 보유 하는 기능에 대 한 감사 로그 보고서 hello ´ ù.</span><span class="sxs-lookup"><span data-stu-id="4316d-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="4316d-136">특정 기능에 대 한 라이선스가 있는 경우 액세스 toohello 감사에 대 한 로그 정보를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="4316d-137">자세한 내용은 참조 하십시오. **hello Free, Basic 및 Premium 버전의 일반적으로 사용할 수 있는 기능을 비교** 에 [Azure Active Directory 기능 및 특성](https://www.microsoft.com/cloud-platform/azure-active-directory-features)합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="4316d-138">hello **로그인 활동 보고서** 활성화 tootoofind tooquestions에 같은 응답:</span><span class="sxs-lookup"><span data-stu-id="4316d-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="4316d-139">사용자의 hello 로그인 패턴 이란?</span><span class="sxs-lookup"><span data-stu-id="4316d-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="4316d-140">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="4316d-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="4316d-141">이러한 로그인의 hello 상태는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4316d-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="4316d-142">**하는 어떤 Azure AD 라이선스가 필요 tooaccess 로그인 활동 보고서 hello?**</span><span class="sxs-lookup"><span data-stu-id="4316d-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="4316d-143">tooaccess hello 로그인 활동 보고서, 테 넌 트에 연결 된 Azure AD Premium 라이선스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="4316d-144">프로그래밍 방식 액세스</span><span class="sxs-lookup"><span data-stu-id="4316d-144">Programmatic access</span></span>

<span data-ttu-id="4316d-145">또한 toohello 사용자 인터페이스에서 Azure Active Directory reporting 또한 제공 된 [프로그래밍 방식 액세스](active-directory-reporting-api-getting-started-azure-portal.md) toohello 데이터를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="4316d-146">이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등 매우 유용한 tooyour 응용 프로그램을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="4316d-147">hello Azure AD reporting Api는 REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="4316d-148">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4316d-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4316d-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4316d-149">Next steps</span></span>

<span data-ttu-id="4316d-150">Azure Active Directory의 다양 한 보고서 유형의 tooknow hello에 대 한 자세한 하려는 경우 참조:</span><span class="sxs-lookup"><span data-stu-id="4316d-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="4316d-151">위험 플래그가 지정된 사용자 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="4316d-152">위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="4316d-153">감사 로그 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="4316d-154">로그인 로그 보고서</span><span class="sxs-lookup"><span data-stu-id="4316d-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="4316d-155">Hello 보고 API를 사용 하 여 데이터를 보고 하는 hello hello에 액세스 하는 방법에 대 한 자세한 tooknow, 참조:</span><span class="sxs-lookup"><span data-stu-id="4316d-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="4316d-156">Azure Active Directory 보고 API hello 시작</span><span class="sxs-lookup"><span data-stu-id="4316d-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png