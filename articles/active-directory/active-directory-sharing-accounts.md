---
title: "Azure AD를 사용 하 여 aaaSharing 계정을 | Microsoft Docs"
description: "Azure Active Directory 온-프레미스 응용 프로그램 및 소비자 클라우드 서비스에 대 한 조직 toosecurely 공유 계정을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a><span data-ttu-id="ce863-103">Azure AD와 계정 공유</span><span class="sxs-lookup"><span data-stu-id="ce863-103">Sharing accounts with Azure AD</span></span>
## <a name="overview"></a><span data-ttu-id="ce863-104">개요</span><span class="sxs-lookup"><span data-stu-id="ce863-104">Overview</span></span>
<span data-ttu-id="ce863-105">경우에 따라 조직에서는 여러 사용자에 대 한 toouse 단일 사용자 이름 및 암호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-105">Sometimes organizations need toouse a single username and password for multiple people.</span></span> <span data-ttu-id="ce863-106">일반적으로 다음 두 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-106">This typically happens in two cases:</span></span>

* <span data-ttu-id="ce863-107">온-프레미스 앱이나 소비자 클라우드 서비스 등, 각 사용자에 대한 고유의 로그인과 암호가 필요한 응용 프로그램을 액세스할 때(예: 기업 소셜 미디어 계정)</span><span class="sxs-lookup"><span data-stu-id="ce863-107">When accessing applications that require a unique login and password for each user, whether on-premises apps or consumer cloud services ( e.g. corporate social media accounts).</span></span>
* <span data-ttu-id="ce863-108">다중 사용자 환경을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="ce863-108">When creating multi-user environments.</span></span> <span data-ttu-id="ce863-109">상승 된 권한을 갖는 단일, 로컬 계정에 있을 수 있습니다 및 사용 되는 toodo 핵심 설치, 관리 및 복구 작업 (예: hello 로컬 "전역 관리자" 계정 Salesforce에서 Office 365 또는 hello 루트 계정에 대 한) 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-109">You may have a single, local account that has elevated privileges and can be used toodo core setup, administration, and recovery activities (e.g. hello local "global administrator" account for Office 365 or hello root account in Salesforce).</span></span>

<span data-ttu-id="ce863-110">일반적으로 이러한 계정은 hello 자격 증명 (사용자 이름/암호) toohello 오른쪽 개인 배포 하거나 여러 신뢰할 수 있는 에이전트에 액세스할 수 있는 공유 위치에 저장 하 여 공유할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-110">Traditionally, these accounts would be shared by distributing hello credentials (username/password) toohello right individuals or storing them in a shared location where multiple trusted agents can access them.</span></span>

<span data-ttu-id="ce863-111">기존 공유 모델 hello에 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-111">hello traditional sharing model has several drawbacks:</span></span>

* <span data-ttu-id="ce863-112">응용 프로그램에서 액세스 toonew 사용 액세스 해야 하는 toodistribute 자격 증명 tooeveryone가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-112">Enabling access toonew applications requires you toodistribute credentials tooeveryone that needs access.</span></span>
* <span data-ttu-id="ce863-113">각 공유 응용 프로그램은 자체 고유한 사용자 tooremember 여러 가지 자격 증명을 요구 하는 공유 자격 증명 집합이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-113">Each shared application may require its own unique set of shared credentials, requiring users tooremember multiple sets of credentials.</span></span> <span data-ttu-id="ce863-114">사용자가 tooremember 많은 자격 증명을가지고 hello 위험 toorisky 사례 적용은 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-114">When users have tooremember many credentials, hello risk increases that they will resort toorisky practices.</span></span> <span data-ttu-id="ce863-115">(예: 암호를 적어).</span><span class="sxs-lookup"><span data-stu-id="ce863-115">(e.g. writing down passwords).</span></span>
* <span data-ttu-id="ce863-116">누구에 게 액세스 tooan 응용 프로그램을 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-116">You can't tell who has access tooan application.</span></span>
* <span data-ttu-id="ce863-117">응용 프로그램에 누가 *액세스했는지* 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-117">You can't tell who has *accessed* an application.</span></span>
* <span data-ttu-id="ce863-118">다시 배포 하 고 tooupdate hello 자격 증명이 있어야 tooremove 액세스 tooan 응용 프로그램이 필요할 때 tooeveryone toothat 응용 프로그램에 액세스 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-118">When you need tooremove access tooan application, you have tooupdate hello credentials and re-distribute them tooeveryone that needs access toothat application.</span></span>

## <a name="azure-active-directory-account-sharing"></a><span data-ttu-id="ce863-119">Azure Active Directory 계정 공유</span><span class="sxs-lookup"><span data-stu-id="ce863-119">Azure Active Directory account sharing</span></span>
<span data-ttu-id="ce863-120">Azure AD는 새로운 접근 방식을 이러한 단점을 제거 하는 공유 toousing 계정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-120">Azure AD provides a new approach toousing shared accounts that eliminates these drawbacks.</span></span>

<span data-ttu-id="ce863-121">Azure AD 관리자에 게 사용자가 액세스 패널 hello를 사용 하 고 hello 유형의 single sign on 해당 응용 프로그램에 가장 적합 한 선택 하 여 액세스할 수 있는 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-121">hello Azure AD administrator configures which applications a user can access by using hello Access Panel and choosing hello type of single sign-on best suited for that application.</span></span> <span data-ttu-id="ce863-122">이러한 형식 중 하나 *암호 기반 single sign-on*, 해당 앱에 대 한 hello 로그온 프로세스 중 "브로커"의 일종으로 작동 하는 Azure AD를 통해 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-122">One of those types, *password-based single-sign on*, lets Azure AD act as a kind of "broker" during hello sign-on process for that app.</span></span>

<span data-ttu-id="ce863-123">사용자가 조직 계정으로 한번에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-123">Users log in once with their organizational account.</span></span> <span data-ttu-id="ce863-124">이 hello 동일한 계정을 정기적으로 사용 하는 tooaccess 데스크톱 또는 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-124">This is hello same account that they regularly use tooaccess their desktop or email.</span></span> <span data-ttu-id="ce863-125">사용자는 자신에게 할당된 응용 프로그램만 확인하고 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-125">They can discover and access only those applications that they are assigned to.</span></span> <span data-ttu-id="ce863-126">공유 계정을 사용하면 이 응용 프로그램 목록이 수에 관계없이 공유 자격 증명을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-126">With shared accounts, this list of applications can include any number of shared credentials.</span></span> <span data-ttu-id="ce863-127">hello 최종 사용자는 tooremember 필요 하지 않습니다 또는 다양 한 계정을 사용 중일 수도 hello 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-127">hello end user doesn't need tooremember or write down hello various accounts they may be using.</span></span>

<span data-ttu-id="ce863-128">공유 계정을 사용하면 관리뿐 아니라 활용성도 높아지며 보안도 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-128">Shared accounts not only increase oversight and improve usability, they also enhance your security.</span></span> <span data-ttu-id="ce863-129">사용 권한 toouse hello 자격 증명이 있는 사용자 암호를 공유 하는 hello를 표시 되지 않는 하지만 대신 오케스트레이션된 인증 흐름의 일환으로 사용 권한을 toouse hello 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-129">Users with permissions toouse hello credentials don't see hello shared password, but rather get permissions toouse hello password as part of an orchestrated authentication flow.</span></span> <span data-ttu-id="ce863-130">또한 일부 암호 SSO 응용 프로그램을 사용할 경우 hello 옵션 toohave Azure AD 계정 보안 hello 증가 대규모의 복잡 한 암호를 사용 하 여 롤오버 (업데이트) hello 암호 주기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-130">Further, with some password SSO applications, you have hello option toohave Azure AD periodically rollover (update) hello password using large, complex passwords, increasing hello account security.</span></span> <span data-ttu-id="ce863-131">관리자에 게 쉽게 부여할 수 있습니다 또는 tooan 응용 프로그램 액세스를 해지 되 고 또한 액세스 toohello 계정 누가 및 지난 hello에 액세스 하를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-131">hello administrator can easily grant or revoke access tooan application and also know who has access toohello account and who accessed it in hello past.</span></span>

<span data-ttu-id="ce863-132">Azure AD는 모든 유형의 암호 Single Sign-on 응용 프로그램 전체에서EMS(Enterprise Mobility Suite), 프리미엄 또는 기본 라이선스 사용자의 공유 계정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-132">Azure AD supports shared accounts for any Enterprise Mobility Suite (EMS), Premium, or Basic licensed users, across all types of password single sign on applications.</span></span> <span data-ttu-id="ce863-133">Hello 응용 프로그램 갤러리에서 미리 통합 된 응용 프로그램 중 하나에 대 한 계정을 공유할 수 있습니다 및 암호 인증 응용 프로그램 자체에 추가할 수 [SSO의 사용자 지정 앱](active-directory-sso-integrate-saas-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-133">You can share accounts for any of thousands of pre-integrated applications in hello application gallery and can add your own password-authenticating application with [custom SSO apps](active-directory-sso-integrate-saas-apps.md).</span></span>

<span data-ttu-id="ce863-134">계정에 공유를 사용하는 Azure AD 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-134">Azure AD features that enable account sharing include:</span></span>

* [<span data-ttu-id="ce863-135">암호 SSO(Single sign-on)</span><span class="sxs-lookup"><span data-stu-id="ce863-135">Password single sign-on</span></span>](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* <span data-ttu-id="ce863-136">암호 SSO(Single sign-on) 에이전트</span><span class="sxs-lookup"><span data-stu-id="ce863-136">Password single sign-on agent</span></span>
* [<span data-ttu-id="ce863-137">그룹 할당</span><span class="sxs-lookup"><span data-stu-id="ce863-137">Group assignment</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* <span data-ttu-id="ce863-138">사용자 지정 암호 앱</span><span class="sxs-lookup"><span data-stu-id="ce863-138">Custom Password apps</span></span>
* [<span data-ttu-id="ce863-139">앱 사용 대시보드/보고서</span><span class="sxs-lookup"><span data-stu-id="ce863-139">App usage dashboard/reports</span></span>](active-directory-passwords-get-insights.md)
* <span data-ttu-id="ce863-140">최종 사용자 액세스 패널</span><span class="sxs-lookup"><span data-stu-id="ce863-140">End user access portals</span></span>
* [<span data-ttu-id="ce863-141">앱 프록시</span><span class="sxs-lookup"><span data-stu-id="ce863-141">App proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="ce863-142">Active Directory 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="ce863-142">Active Directory Marketplace</span></span>](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a><span data-ttu-id="ce863-143">계정 공유</span><span class="sxs-lookup"><span data-stu-id="ce863-143">Sharing an account</span></span>
<span data-ttu-id="ce863-144">Azure AD toouse tooshare 계정을를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-144">toouse Azure AD tooshare an account you will need to:</span></span>

* <span data-ttu-id="ce863-145">응용 프로그램 [앱 갤러리](https://azure.microsoft.com/marketplace/active-directory/)나 [사용자 지정 응용 프로그램](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx) 추가</span><span class="sxs-lookup"><span data-stu-id="ce863-145">Add an application [app gallery](https://azure.microsoft.com/marketplace/active-directory/) or [custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span></span>
* <span data-ttu-id="ce863-146">암호 Single Sign-on (SSO)에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ce863-146">Configure hello application for password Single Sign-On (SSO)</span></span>
* <span data-ttu-id="ce863-147">사용 하 여 [그룹 기반 할당](active-directory-accessmanagement-group-saasapps.md) 선택 hello 옵션 tooenter 공유 자격 증명 및</span><span class="sxs-lookup"><span data-stu-id="ce863-147">Use [group based assignment](active-directory-accessmanagement-group-saasapps.md) and select hello option tooenter a shared credential</span></span>
* <span data-ttu-id="ce863-148">선택 사항: Facebook, Twitter, LinkedIn, 등 일부 응용 프로그램에서 사용할 수 있습니다에 대 한 hello 옵션 [Azure AD 자동 암호 롤오버](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce863-148">Optional: in some applications, such as Facebook, Twitter, or LinkedIn, you can enable hello option for [Azure AD automated password roll-over](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span></span>

<span data-ttu-id="ce863-149">만들 수도 있습니다 공유 계정 보다 안전한 Multi-factor Authentication (MFA)와 (에 대 한 자세한 내용은 [Azure AD와 응용 프로그램 보안](../multi-factor-authentication/multi-factor-authentication-get-started.md)) 사용 하 여 액세스 toohello 응용 프로그램을 가진 hello 기능 toomanage 위임할 수 있습니다 및 [Azure AD 셀프 서비스](active-directory-accessmanagement-self-service-group-management.md) 그룹 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce863-149">You can also make your shared account more secure with Multi-Factor Authentication (MFA) (learn more about [securing applications with Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) and you can delegate hello ability toomanage who has access toohello application using [Azure AD Self-service](active-directory-accessmanagement-self-service-group-management.md) Group Management.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ce863-150">관련 문서</span><span class="sxs-lookup"><span data-stu-id="ce863-150">Related articles</span></span>
* [<span data-ttu-id="ce863-151">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="ce863-151">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ce863-152">조건부 액세스를 사용한 앱 보호</span><span class="sxs-lookup"><span data-stu-id="ce863-152">Protecting apps with conditional access</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="ce863-153">셀프 서비스 그룹 관리/SSAA</span><span class="sxs-lookup"><span data-stu-id="ce863-153">Self-service group management/SSAA</span></span>](active-directory-accessmanagement-self-service-group-management.md)

