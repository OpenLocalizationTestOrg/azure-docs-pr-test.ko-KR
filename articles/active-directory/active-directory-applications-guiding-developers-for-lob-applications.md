---
title: "Azure AD에 대 한 aaaDevelop 앱 | Microsoft Docs"
description: "Hello IT 전문가 용으로 작성 된,이 문서에서는 Active Directory와 Azure 응용 프로그램 통합에 대 한 지침을 제공 합니다."
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
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="9f543-103">Azure Active Directory용 기간 업무 앱 개발</span><span class="sxs-lookup"><span data-stu-id="9f543-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="9f543-104">이 가이드에서는 Azure AD (Active Directory).hello 용 기간 업무 (LoB) 응용 프로그램 개발의 개요를 의도 한 대상 그룹은 Active Directory/Office 365 전역 관리자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="9f543-105">개요</span><span class="sxs-lookup"><span data-stu-id="9f543-105">Overview</span></span>
<span data-ttu-id="9f543-106">Azure AD와 통합된 응용 프로그램을 구축하면 조직의 사용자에게 Office 365를 사용하여 Single Sign-On을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="9f543-107">Hello 응용 프로그램에서 Azure AD 사용 hello 응용 프로그램에 대 한 인증 정책을 hello 제어할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="9f543-108">조건부 액세스 및 multi-factor authentication (MFA)를 사용 하 여 tooprotect 앱 확인 하는 방법에 대 한 자세한 toolearn [구성 액세스 규칙](active-directory-conditional-access-azuread-connected-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="9f543-109">응용 프로그램 toouse Azure Active Directory에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="9f543-110">개발자가 Azure AD tooauthenticate 사용자를 사용 하 고 전자 메일, 일정 및 문서와 같은 리소스에 액세스 toouser 요청 수를 의미 hello 응용 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="9f543-111">디렉터리(게스트 아님)의 멤버는 응용 프로그램을 등록할 수 있습니다.( *응용 프로그램 개체 만들기*라고 함)</span><span class="sxs-lookup"><span data-stu-id="9f543-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="9f543-112">응용 프로그램 등록 하는 사용자 toodo hello 후행을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="9f543-113">Azure AD가 인식하는 응용 프로그램에 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="9f543-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="9f543-114">구입 하거나 응용 프로그램 hello 하는 자세한 암호/키 자체 tooauthenticate tooAD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="9f543-115">브랜드 hello hello 사용자 정의 이름, 로고 등으로 Azure 포털에서에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="9f543-116">Azure AD 권한 부여 기능 tootheir 앱 적용 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="9f543-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="9f543-117">역할 기반 액세스 제어(RBAC)</span><span class="sxs-lookup"><span data-stu-id="9f543-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="9f543-118">OAuth 권한 부여 서버와 azure Active Directory (보안 hello 응용 프로그램에 의해 노출 되는 API)</span><span class="sxs-lookup"><span data-stu-id="9f543-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="9f543-119">포함 하 여 예상 대로 필요한 사용 권한이 필요한 응용 프로그램 toofunction hello에 대 한 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="9f543-120">앱 사용 권한(전역 관리자만 해당)</span><span class="sxs-lookup"><span data-stu-id="9f543-120">App permissions (global administrators only).</span></span> <span data-ttu-id="9f543-121">예: 다른 Azure AD 응용 프로그램 또는 역할 멤버 자격 상대 tooan Azure 리소스, 리소스 그룹의에서 역할 멤버 자격 또는 구독</span><span class="sxs-lookup"><span data-stu-id="9f543-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="9f543-122">위임된 권한(모든 사용자).</span><span class="sxs-lookup"><span data-stu-id="9f543-122">Delegated permissions (any user).</span></span> <span data-ttu-id="9f543-123">예: Azure AD, 로그인 및 프로필 읽기</span><span class="sxs-lookup"><span data-stu-id="9f543-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="9f543-124">기본적으로 모든 멤버는 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-124">By default, any member can register an application.</span></span> <span data-ttu-id="9f543-125">응용 프로그램 toospecific 멤버를 등록 하기 위한 toorestrict 사용 권한을 확인 하려면 어떻게 해야 toolearn [응용 프로그램 tooAzure AD에 추가 하는 방법을](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="9f543-126">여기은 어떤 사용자 전역 관리자에 게 필요 toodo toohelp 개발자 확인 합니다 응용 프로그램 프로덕션에 대 한 준비:</span><span class="sxs-lookup"><span data-stu-id="9f543-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="9f543-127">액세스 규칙 구성(액세스 정책/MFA)</span><span class="sxs-lookup"><span data-stu-id="9f543-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="9f543-128">Hello 앱 toorequire 사용자 할당을 구성 하 고 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="9f543-129">Hello 기본 사용자 승인 환경에 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="9f543-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="9f543-130">액세스 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="9f543-130">Configure access rules</span></span>
<span data-ttu-id="9f543-131">응용 프로그램별 액세스 규칙 tooyour SaaS 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="9f543-132">예를 들어 MFA를 요구할 수도 있고 신뢰할 수 있는 네트워크 액세스 toousers 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="9f543-133">이 대 한 세부 정보 hello hello 문서에서 사용할 수 있는 [구성 액세스 규칙](active-directory-conditional-access-azuread-connected-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="9f543-134">Hello 앱 toorequire 사용자 할당을 구성 하 고 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="9f543-135">기본적으로 사용자는 할당되지 않아도 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="9f543-136">그러나 hello 응용 프로그램 역할을 노출 하는 경우 또는 사용자의 액세스 패널에 응용 프로그램 tooappear hello를 하려는 경우 사용자 할당을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="9f543-137">사용자 할당 요구</span><span class="sxs-lookup"><span data-stu-id="9f543-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="9f543-138">Azure AD Premium 또는 Enterprise Mobility Suite(EMS) 구독자인 경우 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="9f543-139">Toohello 응용 프로그램 그룹을 지정 toodelegate 진행 중인 액세스 관리 toohello 그룹의 소유자를 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="9f543-140">Hello 그룹을 만들거나 hello 담당자 그룹 관리 기능을 사용 하 여 조직 toocreate hello 그룹에 게 요청 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="9f543-141">Tooan 응용 프로그램 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="9f543-142">Tooan 응용 프로그램 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="9f543-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="9f543-143">사용자 동의 무시</span><span class="sxs-lookup"><span data-stu-id="9f543-143">Suppress user consent</span></span>
<span data-ttu-id="9f543-144">기본적으로 각 사용자의 동의 환경 toosign를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="9f543-145">사용자에 게 toogrant 권한을 tooan 응용 프로그램 요청 hello 승인 환경을 그러한 결정에 익숙하지 않은 사용자에 게 혼란을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="9f543-146">신뢰할 수 있는 응용 프로그램의 경우 조직을 대신 하 여 승인 toohello 응용 프로그램에 의해 hello 사용자 경험을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="9f543-147">사용자 승인 및 동의 hello에 대 한 자세한 내용은 Azure의 경험 하십시오 참조 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f543-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="9f543-148">관련 문서</span><span class="sxs-lookup"><span data-stu-id="9f543-148">Related Articles</span></span>
* [<span data-ttu-id="9f543-149">보안 된 원격 액세스 tooon 온-프레미스 응용 프로그램을 Azure AD 응용 프로그램 프록시를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9f543-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="9f543-150">Azure Conditional Access Preview for SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="9f543-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="9f543-151">Azure AD와 tooapps 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="9f543-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="9f543-152">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="9f543-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
