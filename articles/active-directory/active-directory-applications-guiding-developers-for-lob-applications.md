---
title: "Azure AD용 앱 개발 | Microsoft Docs'"
description: "IT 전문가를 위해 작성된 이 문서는 Active Directory와 Azure 응용 프로그램 통합에 대한 지침을 제공합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="0e663-103">Azure Active Directory용 기간 업무 앱 개발</span><span class="sxs-lookup"><span data-stu-id="0e663-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="0e663-104">이 가이드는 Azure Active Directory(AD)에 대한 LoB(기간 업무) 응용 프로그램 개발의 개요를 제공하며, Active Directory/Office 365 전역 관리자용으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="0e663-105">개요</span><span class="sxs-lookup"><span data-stu-id="0e663-105">Overview</span></span>
<span data-ttu-id="0e663-106">Azure AD와 통합된 응용 프로그램을 구축하면 조직의 사용자에게 Office 365를 사용하여 Single Sign-On을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="0e663-107">Azure AD에 응용 프로그램이 있다면 응용 프로그램에 대한 인증 정책을 통한 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="0e663-108">조건부 액세스 및 Multi-Factor Authentication(MFA)을 사용하여 앱을 보호하는 방법에 대한 자세한 내용은 [액세스 규칙 구성](active-directory-conditional-access-azuread-connected-apps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e663-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="0e663-109">Azure Active Directory를 사용하기 위해 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="0e663-110">응용 프로그램을 등록하면 개발자가 Azure AD를 사용하여 사용자를 인증하고 전자 메일, 일정, 문서 등과 같은 사용자 리소스에 대한 액세스를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="0e663-111">디렉터리(게스트 아님)의 멤버는 응용 프로그램을 등록할 수 있습니다.( *응용 프로그램 개체 만들기*라고 함)</span><span class="sxs-lookup"><span data-stu-id="0e663-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="0e663-112">응용 프로그램을 등록하면 사용자가 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="0e663-113">Azure AD가 인식하는 응용 프로그램에 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e663-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="0e663-114">응용 프로그램에서 사용할 수 있는 하나 이상의 암호/키를 가져와서 AD에 자신을 인증</span><span class="sxs-lookup"><span data-stu-id="0e663-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="0e663-115">Azure 포털에서 사용자 지정 이름, 로고 등으로 응용 프로그램 브랜딩</span><span class="sxs-lookup"><span data-stu-id="0e663-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="0e663-116">다음을 포함하여 앱에 대한 Azure AD 권한 부여 기능 적용</span><span class="sxs-lookup"><span data-stu-id="0e663-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="0e663-117">역할 기반 액세스 제어(RBAC)</span><span class="sxs-lookup"><span data-stu-id="0e663-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="0e663-118">OAuth 권한 부여 서버인 Azure Active Directory(응용 프로그램에서 노출된 API 보호)</span><span class="sxs-lookup"><span data-stu-id="0e663-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="0e663-119">응용 프로그램에 예상 대로 작동하는 데 필요한 다음을 포함하는 사용 권한을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="0e663-120">앱 사용 권한(전역 관리자만 해당)</span><span class="sxs-lookup"><span data-stu-id="0e663-120">App permissions (global administrators only).</span></span> <span data-ttu-id="0e663-121">예: 다른 Azure AD 응용 프로그램에서 역할 멤버 자격 또는 Azure 리소스, 리소스 그룹 또는 구독에 상대적인 역할 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="0e663-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="0e663-122">위임된 권한(모든 사용자).</span><span class="sxs-lookup"><span data-stu-id="0e663-122">Delegated permissions (any user).</span></span> <span data-ttu-id="0e663-123">예: Azure AD, 로그인 및 프로필 읽기</span><span class="sxs-lookup"><span data-stu-id="0e663-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="0e663-124">기본적으로 모든 멤버는 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-124">By default, any member can register an application.</span></span> <span data-ttu-id="0e663-125">특정 멤버에 응용 프로그램 등록에 대한 사용 권한을 제한하는 방법을 알아보려면 [Azure AD에 응용 프로그램을 추가하는 방법](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e663-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="0e663-126">다음은 개발자가 자신의 응용 프로그램을 생산할 준비를 돕기 위해 전역 관리자가 수행해야 하는 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="0e663-127">액세스 규칙 구성(액세스 정책/MFA)</span><span class="sxs-lookup"><span data-stu-id="0e663-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="0e663-128">앱을 구성하여 사용자 할당 요구 및 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="0e663-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="0e663-129">기본 사용자 동의 환경 무시</span><span class="sxs-lookup"><span data-stu-id="0e663-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="0e663-130">액세스 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="0e663-130">Configure access rules</span></span>
<span data-ttu-id="0e663-131">SaaS 앱에 응용 프로그램별 액세스 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="0e663-132">예를 들어 MFA를 요구하거나 신뢰할 수 있는 네트워크의 사용자에 대한 액세스만 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="0e663-133">이에 대한 세부 정보는 [액세스 규칙 구성](active-directory-conditional-access-azuread-connected-apps.md)문서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="0e663-134">앱을 구성하여 사용자 할당 요구 및 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="0e663-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="0e663-135">기본적으로 사용자는 할당되지 않아도 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="0e663-136">그러나 응용 프로그램이 역할을 노출하거나 또는 응용 프로그램을 사용자의 액세스 패널에 표시하려는 경우 사용자 할당이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="0e663-137">사용자 할당 요구</span><span class="sxs-lookup"><span data-stu-id="0e663-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="0e663-138">Azure AD Premium 또는 Enterprise Mobility Suite(EMS) 구독자인 경우 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="0e663-139">응용 프로그램에 그룹을 할당하면 그룹의 소유자에게 지속적인 액세스 관리를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="0e663-140">그룹을 만들거나 조직에서 책임 파티를 요청하여 그룹 관리 기능을 사용하여 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="0e663-141">응용 프로그램에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0e663-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="0e663-142">응용 프로그램에 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="0e663-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="0e663-143">사용자 동의 무시</span><span class="sxs-lookup"><span data-stu-id="0e663-143">Suppress user consent</span></span>
<span data-ttu-id="0e663-144">기본적으로 각 사용자는 로그인하기 위해 동의 환경을 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="0e663-145">사용자에게 응용 프로그램에 대한 사용 권한을 부여하도록 요청하는 동의 환경은 그런 결정을 내리는 데 익숙하지 않은 사용자에게 혼란을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="0e663-146">신뢰할 수 있는 응용 프로그램의 경우 조직을 대신하여 응용 프로그램에 동의하여 사용자 환경을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e663-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="0e663-147">Azure에서 동의 및 동의 환경에 대한 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e663-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="0e663-148">관련 문서</span><span class="sxs-lookup"><span data-stu-id="0e663-148">Related Articles</span></span>
* [<span data-ttu-id="0e663-149">Azure AD 응용 프로그램 프록시를 사용하여 온-프레미스 응용 프로그램에 대한 보안 원격 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="0e663-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="0e663-150">Azure Conditional Access Preview for SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="0e663-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="0e663-151">Azure AD를 사용하는 앱에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="0e663-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="0e663-152">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="0e663-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
