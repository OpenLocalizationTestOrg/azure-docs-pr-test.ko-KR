---
title: "Azure AD를 사용한 계정 공유 | Microsoft Docs"
description: "Azure Active Directory를 통해 조직이 온-프레미스 앱과 소비자 클라우드 서비스에 대해 안전하게 계정을 공유할 수 있는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: b40335eda9dffe75e65d004837a1d67914db15b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sharing-accounts-with-azure-ad"></a><span data-ttu-id="6a909-103">Azure AD와 계정 공유</span><span class="sxs-lookup"><span data-stu-id="6a909-103">Sharing accounts with Azure AD</span></span>
## <a name="overview"></a><span data-ttu-id="6a909-104">개요</span><span class="sxs-lookup"><span data-stu-id="6a909-104">Overview</span></span>
<span data-ttu-id="6a909-105">경우에 따라 조직에서는 여러 사용자에 단일 사용자 이름 및 암호를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-105">Sometimes organizations need to use a single username and password for multiple people.</span></span> <span data-ttu-id="6a909-106">일반적으로 다음 두 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-106">This typically happens in two cases:</span></span>

* <span data-ttu-id="6a909-107">온-프레미스 앱이나 소비자 클라우드 서비스 등, 각 사용자에 대한 고유의 로그인과 암호가 필요한 응용 프로그램을 액세스할 때(예: 기업 소셜 미디어 계정)</span><span class="sxs-lookup"><span data-stu-id="6a909-107">When accessing applications that require a unique login and password for each user, whether on-premises apps or consumer cloud services ( e.g. corporate social media accounts).</span></span>
* <span data-ttu-id="6a909-108">다중 사용자 환경을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="6a909-108">When creating multi-user environments.</span></span> <span data-ttu-id="6a909-109">상승된 권한을 갖는 단일 로컬 계정을 만들고 이 계정을 사용하여 핵심 설정, 관리 및 복구 작업을 수행할 수 있습니다(예: Office 365에는 로컬 “글로벌 관리자" 계정, Salesforce에는 루트 계정).</span><span class="sxs-lookup"><span data-stu-id="6a909-109">You may have a single, local account that has elevated privileges and can be used to do core setup, administration, and recovery activities (e.g. the local "global administrator" account for Office 365 or the root account in Salesforce).</span></span>

<span data-ttu-id="6a909-110">일반적으로 이러한 계정은 자격 증명(사용자 이름/암호)을 적합한 개인에게 배포하거나 신뢰할 수 있는 여러 에이전트가 액세스할 수 있는 공유 위치에 저장하여 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-110">Traditionally, these accounts would be shared by distributing the credentials (username/password) to the right individuals or storing them in a shared location where multiple trusted agents can access them.</span></span>

<span data-ttu-id="6a909-111">전통적인 공유 모델에는 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-111">The traditional sharing model has several drawbacks:</span></span>

* <span data-ttu-id="6a909-112">새 응용 프로그램에 대한 액세스를 활성화하려면 액세스가 필요한 모든 사용자에게 자격 증명을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-112">Enabling access to new applications requires you to distribute credentials to everyone that needs access.</span></span>
* <span data-ttu-id="6a909-113">각 공유 응용 프로그램에는 공유 자격 증명의 고유한 자체 세트가 필요할 수 있으므로 사용자가 여러 자격 증명 세트를 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-113">Each shared application may require its own unique set of shared credentials, requiring users to remember multiple sets of credentials.</span></span> <span data-ttu-id="6a909-114">사용자가 여러 자격 증명을 기억해야 한다면, 편의를 위해 위험한 행동을 할 가능성이 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-114">When users have to remember many credentials, the risk increases that they will resort to risky practices.</span></span> <span data-ttu-id="6a909-115">(예: 암호를 적어).</span><span class="sxs-lookup"><span data-stu-id="6a909-115">(e.g. writing down passwords).</span></span>
* <span data-ttu-id="6a909-116">응용 프로그램에 누가 액세스 권한이 있는지 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-116">You can't tell who has access to an application.</span></span>
* <span data-ttu-id="6a909-117">응용 프로그램에 누가 *액세스했는지* 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-117">You can't tell who has *accessed* an application.</span></span>
* <span data-ttu-id="6a909-118">응용 프로그램에 대한 액세스를 제거해야 할 때 자격 증명을 업데이트하고 다시 해당 응용 프로그램에 액세스가 필요한 모든 사용자에게 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-118">When you need to remove access to an application, you have to update the credentials and re-distribute them to everyone that needs access to that application.</span></span>

## <a name="azure-active-directory-account-sharing"></a><span data-ttu-id="6a909-119">Azure Active Directory 계정 공유</span><span class="sxs-lookup"><span data-stu-id="6a909-119">Azure Active Directory account sharing</span></span>
<span data-ttu-id="6a909-120">Azure AD는 이러한 단점을 제거하는 새로운 방법의 공유 계정 사용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-120">Azure AD provides a new approach to using shared accounts that eliminates these drawbacks.</span></span>

<span data-ttu-id="6a909-121">Azure AD 관리자는 해당 응용 프로그램에 대해 액세스 패널을 사용하고 가장 적합한 Single Sign On 형식을 선택하여 액세스할 수 있는 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-121">The Azure AD administrator configures which applications a user can access by using the Access Panel and choosing the type of single sign-on best suited for that application.</span></span> <span data-ttu-id="6a909-122">이러한 유형 중 하나인 *암호 기반 Single Sign-on*을 통해 Azure AD는 해당 앱의 로그온 프로세스 중에 일종의 "broker"로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-122">One of those types, *password-based single-sign on*, lets Azure AD act as a kind of "broker" during the sign-on process for that app.</span></span>

<span data-ttu-id="6a909-123">사용자가 조직 계정으로 한번에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-123">Users log in once with their organizational account.</span></span> <span data-ttu-id="6a909-124">정기적으로 데스크톱 또는 전자 메일에 액세스하는 데 사용하는 동일한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-124">This is the same account that they regularly use to access their desktop or email.</span></span> <span data-ttu-id="6a909-125">사용자는 자신에게 할당된 응용 프로그램만 확인하고 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-125">They can discover and access only those applications that they are assigned to.</span></span> <span data-ttu-id="6a909-126">공유 계정을 사용하면 이 응용 프로그램 목록이 수에 관계없이 공유 자격 증명을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-126">With shared accounts, this list of applications can include any number of shared credentials.</span></span> <span data-ttu-id="6a909-127">최종 사용자는 자신이 사용하는 다양한 계정을 기억하거나 기록해 둘 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-127">The end user doesn't need to remember or write down the various accounts they may be using.</span></span>

<span data-ttu-id="6a909-128">공유 계정을 사용하면 관리뿐 아니라 활용성도 높아지며 보안도 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-128">Shared accounts not only increase oversight and improve usability, they also enhance your security.</span></span> <span data-ttu-id="6a909-129">자격 증명을 사용할 권한이 있는 사용자는 공유 암호를 보는 것이 아니라 조정된 인증 흐름의 일환으로 암호를 사용할 권한을 받는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-129">Users with permissions to use the credentials don't see the shared password, but rather get permissions to use the password as part of an orchestrated authentication flow.</span></span> <span data-ttu-id="6a909-130">또한 일부 암호 SSO 응용 프로그램을 통해 Azure AD가 대규모의 복잡한 암호를 사용하여 주기적으로 암호를 롤오버(업데이트)하도록 지정하여 계정 보안을 증대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-130">Further, with some password SSO applications, you have the option to have Azure AD periodically rollover (update) the password using large, complex passwords, increasing the account security.</span></span> <span data-ttu-id="6a909-131">관리자는 응용 프로그램에 액세스 권한을 쉽게 부여 또는 취소할 수 있으며 누가 계정에 액세스 권한이 있고 누가 과거에 액세스했는지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-131">The administrator can easily grant or revoke access to an application and also know who has access to the account and who accessed it in the past.</span></span>

<span data-ttu-id="6a909-132">Azure AD는 모든 유형의 암호 Single Sign-on 응용 프로그램 전체에서EMS(Enterprise Mobility Suite), 프리미엄 또는 기본 라이선스 사용자의 공유 계정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-132">Azure AD supports shared accounts for any Enterprise Mobility Suite (EMS), Premium, or Basic licensed users, across all types of password single sign on applications.</span></span> <span data-ttu-id="6a909-133">응용 프로그램 갤러리에서 수천 개의 사전 통합된 응용 프로그램에서 계정을 공유하고, [사용자 지정 SSO 앱](active-directory-sso-integrate-saas-apps.md)으로 자체 암호 인증 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-133">You can share accounts for any of thousands of pre-integrated applications in the application gallery and can add your own password-authenticating application with [custom SSO apps](active-directory-sso-integrate-saas-apps.md).</span></span>

<span data-ttu-id="6a909-134">계정에 공유를 사용하는 Azure AD 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-134">Azure AD features that enable account sharing include:</span></span>

* [<span data-ttu-id="6a909-135">암호 SSO(Single sign-on)</span><span class="sxs-lookup"><span data-stu-id="6a909-135">Password single sign-on</span></span>](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* <span data-ttu-id="6a909-136">암호 SSO(Single sign-on) 에이전트</span><span class="sxs-lookup"><span data-stu-id="6a909-136">Password single sign-on agent</span></span>
* [<span data-ttu-id="6a909-137">그룹 할당</span><span class="sxs-lookup"><span data-stu-id="6a909-137">Group assignment</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* <span data-ttu-id="6a909-138">사용자 지정 암호 앱</span><span class="sxs-lookup"><span data-stu-id="6a909-138">Custom Password apps</span></span>
* [<span data-ttu-id="6a909-139">앱 사용 대시보드/보고서</span><span class="sxs-lookup"><span data-stu-id="6a909-139">App usage dashboard/reports</span></span>](active-directory-passwords-get-insights.md)
* <span data-ttu-id="6a909-140">최종 사용자 액세스 패널</span><span class="sxs-lookup"><span data-stu-id="6a909-140">End user access portals</span></span>
* [<span data-ttu-id="6a909-141">앱 프록시</span><span class="sxs-lookup"><span data-stu-id="6a909-141">App proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="6a909-142">Active Directory 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="6a909-142">Active Directory Marketplace</span></span>](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a><span data-ttu-id="6a909-143">계정 공유</span><span class="sxs-lookup"><span data-stu-id="6a909-143">Sharing an account</span></span>
<span data-ttu-id="6a909-144">Azure AD를 사용하여 계정을 공유하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-144">To use Azure AD to share an account you will need to:</span></span>

* <span data-ttu-id="6a909-145">응용 프로그램 [앱 갤러리](https://azure.microsoft.com/marketplace/active-directory/)나 [사용자 지정 응용 프로그램](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx) 추가</span><span class="sxs-lookup"><span data-stu-id="6a909-145">Add an application [app gallery](https://azure.microsoft.com/marketplace/active-directory/) or [custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span></span>
* <span data-ttu-id="6a909-146">암호 SSO(Single Sign-On)에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="6a909-146">Configure the application for password Single Sign-On (SSO)</span></span>
* <span data-ttu-id="6a909-147">[그룹 기반 할당](active-directory-accessmanagement-group-saasapps.md) 을 사용하고 옵션을 선택하여 공유 자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="6a909-147">Use [group based assignment](active-directory-accessmanagement-group-saasapps.md) and select the option to enter a shared credential</span></span>
* <span data-ttu-id="6a909-148">선택 사항: Facebook, Twitter 또는 LinkedIn 등의 일부 응용 프로그램에서는 [Azure AD 자동 암호 롤오버](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="6a909-148">Optional: in some applications, such as Facebook, Twitter, or LinkedIn, you can enable the option for [Azure AD automated password roll-over](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span></span>

<span data-ttu-id="6a909-149">또한 MFA(Multi-Factor Authentication)로 공유 계정의 보안을 강화하고([Azure AD를 통한 응용 프로그램 보호](../multi-factor-authentication/multi-factor-authentication-get-started.md)에 대한 자세한 정보) [Azure AD 셀프 서비스](active-directory-accessmanagement-self-service-group-management.md) 그룹 관리를 사용하여 응용 프로그램에 대한 액세스 권한이 있는 관리자에게 기능을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a909-149">You can also make your shared account more secure with Multi-Factor Authentication (MFA) (learn more about [securing applications with Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) and you can delegate the ability to manage who has access to the application using [Azure AD Self-service](active-directory-accessmanagement-self-service-group-management.md) Group Management.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6a909-150">관련 문서</span><span class="sxs-lookup"><span data-stu-id="6a909-150">Related articles</span></span>
* [<span data-ttu-id="6a909-151">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="6a909-151">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6a909-152">조건부 액세스를 사용한 앱 보호</span><span class="sxs-lookup"><span data-stu-id="6a909-152">Protecting apps with conditional access</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="6a909-153">셀프 서비스 그룹 관리/SSAA</span><span class="sxs-lookup"><span data-stu-id="6a909-153">Self-service group management/SSAA</span></span>](active-directory-accessmanagement-self-service-group-management.md)

