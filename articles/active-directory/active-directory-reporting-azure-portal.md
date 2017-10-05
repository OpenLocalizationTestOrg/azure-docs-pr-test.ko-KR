---
title: "Azure Active Directory 보고 | Microsoft Docs"
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
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="5fa9a-103">Azure Active Directory 보고</span><span class="sxs-lookup"><span data-stu-id="5fa9a-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="5fa9a-104">Azure Active Directory 보고 기능을 사용하면 환경이 작동하는 방법에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="5fa9a-105">제공된 데이터를 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-105">The provided data enables you to:</span></span>

- <span data-ttu-id="5fa9a-106">사용자가 앱과 서비스를 활용하는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="5fa9a-107">환경의 상태에 영향을 줄 수 있는 잠재적인 위험을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="5fa9a-108">사용자가 자신의 작업을 완료하지 못하게 하는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="5fa9a-109">보고 아키텍처는 다음 두 가지 주요 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="5fa9a-110">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-110">Security reports</span></span>
- <span data-ttu-id="5fa9a-111">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-111">Activity reports</span></span>

![보고](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="5fa9a-113">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-113">Security reports</span></span>

<span data-ttu-id="5fa9a-114">Azure Active Directory의 보안 보고서는 조직의 ID를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="5fa9a-115">Azure Active Directory에는 두 가지 유형의 보안 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="5fa9a-116">**위험 플래그가 지정된 사용자** - [위험 플래그가 지정된 사용자 보안 보고서](active-directory-reporting-security-user-at-risk.md)에서 손상되었을 수 있는 사용자 계정에 대한 개요를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="5fa9a-117">**위험한 로그인** - [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md)를 사용하면 사용자 계정의 정당한 소유자가 아닌 사람이 수행한 로그인 시도에 대한 지표를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="5fa9a-118">**보안 보고서에 액세스하는 데 필요한 Azure AD 라이선스는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5fa9a-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="5fa9a-119">모든 Azure Active Directory 버전에서 위험 플래그가 지정된 사용자 보고서 및 위험한 로그인 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="5fa9a-120">그러나 보고서의 세분성 수준은 다음과 같이 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="5fa9a-121">**Azure Active Directory Free 및 Basic 버전**에는 위험 플래그가 지정된 사용자 및 위험한 로그인 목록이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="5fa9a-122">**Azure Active Directory Premium 1** 버전은 각 보고서에서 검색된 기본 위험 이벤트 중 일부를 검사할 수 있게 함으로써 이 모델을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="5fa9a-123">**Azure Active Directory Premium 2** 버전은 기본 위험 이벤트에 대한 가장 자세한 정보를 제공하며, 구성된 위험 수준에 자동으로 응답하는 보안 정책을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="5fa9a-124">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-124">Activity reports</span></span>

<span data-ttu-id="5fa9a-125">Azure Active Directory에는 두 가지 유형의 활동 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="5fa9a-126">**감사 로그** - [감사 로그 활동 보고서](active-directory-reporting-activity-audit-logs.md)는 테넌트에서 수행된 모든 작업 기록에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="5fa9a-127">**로그인** - [로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)를 사용하면 감사 로그 보고서에서 보고한 작업을 수행한 사람을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="5fa9a-128">**감사 로그 보고서**는 규정 준수에 대한 시스템 활동 기록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="5fa9a-129">제공된 데이터를 사용하면 다음과 같은 일반적인 시나리오를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="5fa9a-130">내 테넌트의 누군가가 관리 그룹에 액세스할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="5fa9a-131">이들에게 액세스 권한을 부여한 사람을 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-131">Who gave them access?</span></span> 

- <span data-ttu-id="5fa9a-132">최근에 앱을 등록한 이후 특정 앱에 로그인하고 있는 사용자의 목록과 앱이 잘 작동하는지의 여부를 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="5fa9a-133">내 테넌트에서 발생하고 있는 암호 재설정 횟수를 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="5fa9a-134">**감사 로그 보고서에 액세스하는 데 필요한 Azure AD 라이선스는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5fa9a-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="5fa9a-135">감사 로그 보고서는 라이선스가 있는 기능에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="5fa9a-136">특정 기능에 대한 라이선스가 있으면 해당 기능에 대한 감사 로그 정보에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="5fa9a-137">자세한 내용은 [Azure Active Directory 기능](https://www.microsoft.com/cloud-platform/azure-active-directory-features)의 **Free, Basic 및 Premium 버전의 일반 공급 기능 비교**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="5fa9a-138">**로그인 활동 보고서**는 다음 질문에 대한 대답을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="5fa9a-139">사용자의 로그인 패턴이란?</span><span class="sxs-lookup"><span data-stu-id="5fa9a-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="5fa9a-140">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="5fa9a-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="5fa9a-141">이러한 로그인의 상태란?</span><span class="sxs-lookup"><span data-stu-id="5fa9a-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="5fa9a-142">**로그인 활동 보고서에 액세스하는 데 필요한 Azure AD 라이선스는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5fa9a-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="5fa9a-143">로그인 활동 보고서에 액세스하려면 이와 연결된 Azure AD Premium 라이선스가 테넌트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="5fa9a-144">프로그래밍 방식 액세스</span><span class="sxs-lookup"><span data-stu-id="5fa9a-144">Programmatic access</span></span>

<span data-ttu-id="5fa9a-145">Azure Active Directory 보고에서는 사용자 인터페이스 외에도 [프로그래밍 방식 액세스](active-directory-reporting-api-getting-started-azure-portal.md)를 보고 데이터에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="5fa9a-146">이러한 보고서의 데이터는 SIEM 시스템, 감사 및 비즈니스 인텔리전스 도구와 같은 응용 프로그램에 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="5fa9a-147">Azure AD Reporting API는 일련의 REST 기반 API를 통해 데이터에 프로그래밍 방식으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="5fa9a-148">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5fa9a-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fa9a-149">Next steps</span></span>

<span data-ttu-id="5fa9a-150">Azure Active Directory의 다양한 보고서 유형에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="5fa9a-151">위험 플래그가 지정된 사용자 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="5fa9a-152">위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="5fa9a-153">감사 로그 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="5fa9a-154">로그인 로그 보고서</span><span class="sxs-lookup"><span data-stu-id="5fa9a-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="5fa9a-155">보고 API를 사용하여 보고 데이터에 액세스하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fa9a-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="5fa9a-156">Azure Active Directory 보고 API 시작</span><span class="sxs-lookup"><span data-stu-id="5fa9a-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png