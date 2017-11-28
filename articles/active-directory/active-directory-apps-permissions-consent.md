---
title: "Azure Active Directory에서 앱, 사용 권한 및 동의 | Microsoft Docs"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 일반 id를 Azure AD와 통합 되어 있습니다."
keywords: "Azure AD Connect 란 소개 tooAzure AD, 응용 프로그램, active directory를 설치 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="f7d06-105">Azure Active Directory에서 앱, 사용 권한 및 동의</span><span class="sxs-lookup"><span data-stu-id="f7d06-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="f7d06-106">Azure Active Directory 내에서 응용 프로그램 tooyour 디렉터리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="f7d06-107">hello 응용 프로그램은 응용 프로그램의 hello 종류에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="f7d06-108">hello 클래식 포털에서 tooview 응용 프로그램 디렉터리 선택 하 고 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="f7d06-109">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="f7d06-110">앱 형식</span><span class="sxs-lookup"><span data-stu-id="f7d06-110">Types of apps</span></span>

1. <span data-ttu-id="f7d06-111">**단일 테넌트 앱**</span><span class="sxs-lookup"><span data-stu-id="f7d06-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="f7d06-112">**단일 테 넌 트 앱** -주로 tooas-업무 (LOB) 응용 프로그램을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="f7d06-113">즉 hello 경우 자체 앱을 개발 하 고, 조직 내의 누군가 및 hello 조직 toobe toohello 응용 프로그램에서 수 toosign에 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="f7d06-114">**응용 프로그램 프록시 앱** -Azure AD 응용 프로그램 프록시를 통해 온-프레미스 응용 프로그램을 노출 하는 경우 단일 테 넌 트 응용 프로그램 (더하기 toohello 응용 프로그램 프록시 서비스)에서 테 넌 트에 등록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="f7d06-115">이 앱은 모든 클라우드 상호 작용(예: 인증)에 대한 온-프레미스 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="f7d06-116">(앱 프록시에는 Azure AD Basic 이상이 필요)</span><span class="sxs-lookup"><span data-stu-id="f7d06-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="f7d06-117">**다중 테넌트 앱**</span><span class="sxs-lookup"><span data-stu-id="f7d06-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="f7d06-118">**다른 사용자에 동의할 수 있는 다중 테 넌 트 앱** 처럼 너무 "조직에서 개발 하는 단일 테 넌 트 앱"입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="f7d06-119">(외에도 hello 앱 자체에서 hello 논리) hello 주요 차이점 다른 테 넌 트의 사용자 tooand 로그인 toohello 응용 프로그램에 동의할 수도 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="f7d06-120">**Contoso에서 동의할 수 있고 다른 사용자가 개발하는 다중 테넌트 앱**.</span><span class="sxs-lookup"><span data-stu-id="f7d06-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="f7d06-121">(또는 간략히 "동의한 앱") "다중 테 넌 트 앱 개발 하 고, 조직" hello 긍 적 적인 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="f7d06-122">다른 조직에서 개발 하는 다중 테 넌 트 응용 프로그램 때 조직의 사용자가 동의 toohello 앱을 업데이트 하 고 tooit 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="f7d06-123">**Microsoft 자사 앱** - Microsoft 서비스를 나타내는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="f7d06-124">동의는 hello 서비스에 가입 하는 hello 팩트에 의해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="f7d06-125">경우에 따라 특별 한 UX 및가 access toohello 앱 관련 된 정책을 설정할 때 주로 사용 되는 특정 자사 응용 프로그램에 대 한 논리</span><span class="sxs-lookup"><span data-stu-id="f7d06-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="f7d06-126">**사전 통합된 앱** -hello 추가할 수 있는 Azure AD 앱 갤러리에서에서 제공 되는 앱 tooyour 디렉터리 tooprovide 단일 로그온 (및 경우에 따라 프로 비전) toopopular SaaS 앱.</span><span class="sxs-lookup"><span data-stu-id="f7d06-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="f7d06-127">**Azure AD single sign-on**: SAML 2.0 또는 OpenID Connect와 같은 지원되는 로그인 프로토콜을 통해 Azure AD와 통합할 수 있는 앱에 대한 "실제" SSO입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="f7d06-128">hello 마법사 설정 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="f7d06-129">**암호 single sign on**: Azure AD hello 앱에 대 한 hello 사용자의 자격 증명을 안전 하 게 저장 하 고 hello 자격 증명은 "" hello 로그인 폼에 의해 삽입 hello Azure AD 응용 프로그램 액세스 브라우저 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="f7d06-130">“암호 보관”이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="f7d06-131">권한</span><span class="sxs-lookup"><span data-stu-id="f7d06-131">Permissions</span></span>

<span data-ttu-id="f7d06-132">앱 등록 될 때 hello 앱 등록 (즉, hello 개발자)를 수행 하는 hello 사용자에 액세스 해야 하는 어떤 권한을 hello 앱 및 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="f7d06-133">(hello 리소스가, 다른 앱으로 정의 된 자체입니다.) 예를 들어 앱 hello "Office 365 Exchange Online" 리소스에에서 대 한 hello "hello 로그인 한 사용자로는 사서함 액세스" 권한이 필요는 상태는 누군가가 메일 판독기 응용 프로그램을 구축:</span><span class="sxs-lookup"><span data-stu-id="f7d06-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="f7d06-134">하나의 응용 프로그램 (클라이언트 hello) toorequest 특정 권한 다른 응용 프로그램 (hello 리소스) 으로부터 hello 리소스 응용 프로그램의 hello 개발자는 존재 하는 hello 사용 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="f7d06-135">Microsoft, hello "Office 365 Exchange Online" 리소스 앱의 hello 소유자 예제에서는 "hello 로그인 한 사용자로는 사서함 액세스" 이라는 권한을 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="f7d06-136">사용 권한을 정의할 때는 hello 권한 승인할 수, 또는 관리자 동의 요구 하면 hello 앱 개발자 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="f7d06-137">이렇게 하면 개발자가 tooallow 사용자 tooconsent 자신의 tooapps만 중요도 낮은 권한 요청에 있지만 admins tooconsent toomore 중요 한 사용 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="f7d06-138">예를 들어, "Azure Active Directory" 리소스 응용 프로그램을 hello, 정의 않으므로 사용자가 동의할 수 tooapps, 제한 된 읽기 전용 권한을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="f7d06-139">그러나 관리자 동의에는 전체 읽기 권한 및 전체 쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="f7d06-140">네이티브 클라이언트는 인증되지 않으므로 네이티브 클라이언트 앱으로 정의된 앱은 위임된 권한만 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="f7d06-141">따라서 토큰을 획득할 때는 실제 관련된 사용자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="f7d06-142">Web Apps 및 Web API(기밀 클라이언트)는 액세스 토큰을 가져올 때 항상 Azure AD로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="f7d06-143">응용 프로그램 전용 권한 요청의 hello 가능성도 가집니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="f7d06-144">예를 들어 한 백 엔드 서비스에 tooauthenticate tooanother 백 엔드 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="f7d06-145">앱 전용 권한을 요청하는 응용 프로그램은 관리자의 동의를 항상 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="f7d06-146">요약:</span><span class="sxs-lookup"><span data-stu-id="f7d06-146">Summarizing:</span></span>



- <span data-ttu-id="f7d06-147">응용 프로그램 (클라이언트)에 다른 앱 (리소스)에 대 한 필요한 hello 권한을 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="f7d06-148">(리소스) 응용 프로그램 권한을 노출된 tooother 앱 (클라이언트) 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="f7d06-149">권한은 앱 전용 권한이거나 위임된 권한일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="f7d06-150">위임된 권한은 “사용자 동의 허용” 또는 “관리자 동의 필요”로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="f7d06-151">응용 프로그램 (선언 노출 하는 권한을)를 여는 리소스 또는 둘 다로 (선언 하 여 필요 하다 고 권한 tooa 리소스)을 클라이언트로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="f7d06-152">컨트롤</span><span class="sxs-lookup"><span data-stu-id="f7d06-152">Controls</span></span>

<span data-ttu-id="f7d06-153">hello 다음은이 모든 동작에 사용할 수 있는 hello 다른 관리 컨트롤의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="f7d06-154">컨트롤에서 hello 클래식 포털에 액세스할 수 있습니다 admin 님 안녕하세요 hello 디렉터리에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="f7d06-155">hello Azure 포털에서 **관리**, **사용자 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="f7d06-156">Tooapps는 사용자가 동의할 수 있는지 여부를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="f7d06-157">Hello 클래식 포털에서 선택 **사용자가 응용 프로그램 사용 권한 tooaccess 데이터가 발생할 수 있습니다.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="f7d06-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="f7d06-158">Hello Azure 포털에서에서 선택 **사용자가 앱 tooaccess 데이터 허용 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="f7d06-159">사용자가 자신의 단일 테 넌 트 LOB 앱을 등록할 수 있는지 여부를 제어할 수 있습니다: hello 클래식 포털 Select에서 **사용자 통합 된 응용 프로그램을 추가할 수 있습니다.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="f7d06-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="f7d06-160">Hello Azure 포털에서에서 선택 **사용자가 앱 tooaccess 데이터 허용 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="f7d06-161">사용자가 단일 테 넌 트 LOB 앱 tooregister 못하게, 경우에 제한은 toowhat를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="f7d06-162">예를 들어 디렉터리 관리자가 아닌 개발자는 다음 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="f7d06-163">사용자는 단일 테넌트 앱을 다중 테넌트 앱으로 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="f7d06-164">단일 테 넌 트 LOB 앱을 등록할 때 사용자가 응용 프로그램 전용 권한을 tooother 응용 프로그램을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="f7d06-165">단일 테 넌 트 LOB 앱을 등록할 때 사용자가 이러한 사용 권한 관리 동의가 필요한 경우 위임 된 사용 권한을 tooother 응용 프로그램을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="f7d06-166">사용자가 변경 내용을 tooapps에 맞지 않음을의 소유자를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="f7d06-167">사용자가 스스로 암호 SSO(즉, “암호 보관”)를 사용하는 사전 통합된 앱을 추가할 수 있는지 여부를 제어할 수 있습니다. ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="f7d06-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="f7d06-168">응용 프로그램에 액세스할 수 있는 조건(즉, 조건부 액세스)을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="f7d06-169">주의 toohello 클라이언트 응용 프로그램 및 toohello 리소스 응용 프로그램을 모두 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="f7d06-170">따라서 해당 hello "Office 365 Exchange Online" 앱 준수 하는 컴퓨터에서 액세스할 수만 조건부 액세스 정책을 설정 하면 말하십시오.</span><span class="sxs-lookup"><span data-stu-id="f7d06-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="f7d06-171">이 정책은 사용자가 toouse 권한을 tooExchange 온라인를 요청 하는 클라이언트 응용 프로그램에도 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="f7d06-172">앱에 알림을 사용 하는 승인된 tooand 된 표시를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="f7d06-173">사용자가 tooan 응용 프로그램을 승인 하면 hello 테 넌 트에 ServicePrincipal 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="f7d06-174">ServicePrincipal 만들기가 hello 감사 보고서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="f7d06-175">사용자 로그인 활동 보고서는 응용 프로그램 hello 사용자가 로그인을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="f7d06-176">예제</span><span class="sxs-lookup"><span data-stu-id="f7d06-176">Example</span></span>

<span data-ttu-id="f7d06-177">예를 들어 테 넌 트의 사용자가 로그인 할 알았습니다 hello "Office 365 용 FabrikamMail" 앱을 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="f7d06-178">“FabrikamMail”은 “Fabrikam, Inc.”에서 게시한 Android용 메일 읽기 프로그램 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="f7d06-179">Hello로 설정 됨 "다중 테 넌 트 앱 Contoso 것에 동의할 수 있는 다른 개발"입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="f7d06-180">사용자가 tooconsent 허용 하는 경우 처음으로 로그인 할 동의 프롬프트 hello를 가져올 있습니다.![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="f7d06-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="f7d06-181">"사서함 액세스"은 "Office 365 Exchange Online" (즉, 교환)에 의해 노출 hello "hello 로그인 한 사용자로는 사서함 액세스" 권한을 hello 사용자 용 동의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="f7d06-182">Office 365에 등록할 때 추가 된 교환 (hello 리소스)에 대 한 hello ServicePrincipal 개체를 조회 하 여 hello 사용 권한을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="f7d06-183">테 넌 트 기록 다양 한 옵션 및 구성 하는 데 사용 되는 hello 앱의 "인스턴스" hello ServicePrincipal 개체의 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="f7d06-184">Hello를 사용 하 여 볼 수 있습니다 `Get-AzureADServicePrincipal` PowerShell에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="f7d06-185">동의는 hello 사용자가 "동의"를 클릭할 때 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="f7d06-186">첫째, hello 테 넌 트의 "Office 365 용 FabrikamMail"에 대 한 ServicePrincipal 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="f7d06-187">ServicePrincipal hello는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="f7d06-188">Tooan 앱 승인 hello 다음은 Oauth2PermissionGrant 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="f7d06-189">hello 사용자 개체</span><span class="sxs-lookup"><span data-stu-id="f7d06-189">hello user object</span></span>
- <span data-ttu-id="f7d06-190">hello 클라이언트 응용 프로그램 서비스 사용자 이름 (SPN)</span><span class="sxs-lookup"><span data-stu-id="f7d06-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="f7d06-191">hello 리소스 응용 프로그램 서비스 사용자 이름 (SPN)</span><span class="sxs-lookup"><span data-stu-id="f7d06-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="f7d06-192">hello 리소스 응용 프로그램에서 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="f7d06-193">Hello FabrikamMail의 경우에서 다음과 같은이:</span><span class="sxs-lookup"><span data-stu-id="f7d06-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="f7d06-194">(**ClientId** FabrikamMail의 서비스 보안 주체 개체 id (만들어진 방금 하나 hello) **PrincipalId** hello 사용자 개체 ID입니다 (hello 사용자가 동의한 것으로 간주), **ResourceId**은 Exchange의 서비스 보안 주체 개체 ID, 범위는 Exchange에 승인 된 하는 hello 권한).</span><span class="sxs-lookup"><span data-stu-id="f7d06-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="f7d06-195">사용자가 tooconsent을 허용 하지 않는 경우 사용 권한이 표시 되는 화면을 반드시 입력 해야 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d06-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

