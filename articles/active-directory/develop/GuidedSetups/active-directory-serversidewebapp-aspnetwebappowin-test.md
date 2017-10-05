---
title: "Azure AD v2 ASP.NET 웹 서버 시작 - 테스트 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="16d8d-103">코드 테스트</span><span class="sxs-lookup"><span data-stu-id="16d8d-103">Test your code</span></span>

<span data-ttu-id="16d8d-104">`F5` 키를 눌러 Visual Studio에서 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="16d8d-105">브라우저가 열리고 *http://localhost:{port}*로 이동합니다. 이 페이지에는 *Microsoft로 로그인* 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="16d8d-106">계속해서 이 단추를 클릭하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="16d8d-107">테스트할 준비가 되면 회사 또는 학교(Azure Active Directory)나 개인(live.com, outlook.com) 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Microsoft로 로그인 브라우저 창](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Microsoft로 로그인 브라우저 창](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="16d8d-110">예상 결과</span><span class="sxs-lookup"><span data-stu-id="16d8d-110">Expected results</span></span>
<span data-ttu-id="16d8d-111">로그인하면 사용자는 Microsoft 응용 프로그램 등록 포털의 응용 프로그램 등록 정보에 지정된 HTTPS URL인 웹 사이트의 홈페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="16d8d-112">이제 이 페이지에 *Hello {User}*({User} 님, 안녕하세요?) 및 로그아웃 링크, 사용자의 클레임을 표시하는 링크(앞에서 만든 권한 부여 컨트롤러에 대한 링크)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="16d8d-113">사용자의 클레임 보기</span><span class="sxs-lookup"><span data-stu-id="16d8d-113">See user's claims</span></span>
<span data-ttu-id="16d8d-114">사용자의 클레임을 보려면 하이퍼링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="16d8d-115">그러면 인증된 사용자에게만 제공되는 보기 및 컨트롤러로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="16d8d-116">예상 결과</span><span class="sxs-lookup"><span data-stu-id="16d8d-116">Expected results</span></span>
 <span data-ttu-id="16d8d-117">로그온한 사용자의 기본 속성을 포함하는 표가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="16d8d-118">속성</span><span class="sxs-lookup"><span data-stu-id="16d8d-118">Property</span></span> | <span data-ttu-id="16d8d-119">값</span><span class="sxs-lookup"><span data-stu-id="16d8d-119">Value</span></span> | <span data-ttu-id="16d8d-120">설명</span><span class="sxs-lookup"><span data-stu-id="16d8d-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="16d8d-121">이름</span><span class="sxs-lookup"><span data-stu-id="16d8d-121">Name</span></span> | <span data-ttu-id="16d8d-122">{User Full Name}</span><span class="sxs-lookup"><span data-stu-id="16d8d-122">{User Full Name}</span></span> | <span data-ttu-id="16d8d-123">사용자의 이름과 성</span><span class="sxs-lookup"><span data-stu-id="16d8d-123">The user’s first and last name</span></span>
|<span data-ttu-id="16d8d-124">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="16d8d-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="16d8d-125">로그온한 사용자를 식별하는 데 사용되는 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="16d8d-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="16d8d-126">제목</span><span class="sxs-lookup"><span data-stu-id="16d8d-126">Subject</span></span>| <span data-ttu-id="16d8d-127">{Subject}</span><span class="sxs-lookup"><span data-stu-id="16d8d-127">{Subject}</span></span>|<span data-ttu-id="16d8d-128">웹에서 사용자 로그온을 고유하게 식별하는 문자열</span><span class="sxs-lookup"><span data-stu-id="16d8d-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="16d8d-129">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="16d8d-129">Tenant ID</span></span>| <span data-ttu-id="16d8d-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="16d8d-130">{Guid}</span></span>| <span data-ttu-id="16d8d-131">사용자의 Azure Active Directory 조직을 고유하게 나타내는 *guid*.</span><span class="sxs-lookup"><span data-stu-id="16d8d-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="16d8d-132">또한 인증 요청에 포함된 모든 사용자 클레임을 포함하는 표가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="16d8d-133">모든 클레임과 ID 토큰 및 설명 목록은 이 [문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "ID 토큰의 클레임 목록")을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16d8d-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="16d8d-134">*[Authorize]* 특성이 있는 메서드 액세스 테스트(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="16d8d-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="16d8d-135">이 단계에서는 익명 사용자로 인증된 컨트롤러 액세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="16d8d-136">사용자 로그아웃 링크를 선택하고 로그아웃 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="16d8d-137">이제 브라우저에서 http://localhost:{port}/authenticated를 입력하여 `[Authorize]` 특성으로 보호되는 컨트롤러에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="16d8d-138">예상 결과</span><span class="sxs-lookup"><span data-stu-id="16d8d-138">Expected results</span></span>
<span data-ttu-id="16d8d-139">보기를 보려면 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="16d8d-140">추가 정보</span><span class="sxs-lookup"><span data-stu-id="16d8d-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="16d8d-141">전체 웹 사이트 보호</span><span class="sxs-lookup"><span data-stu-id="16d8d-141">Protect your entire web site</span></span>
<span data-ttu-id="16d8d-142">전체 웹 사이트를 보호하려면 `Global.asax` `Application_Start` 메서드의 `GlobalFilters`에 `AuthorizeAttribute`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="16d8d-143">**한 조직의 사용자만 응용 프로그램에 로그인하도록 제한하는 방법**</span><span class="sxs-lookup"><span data-stu-id="16d8d-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="16d8d-144">기본적으로 Azure Active Directory와 통합된 회사 또는 조직의 회사 및 학교 계정뿐만 아니라 개인 계정(outlook.com, live.com 등)도 응용 프로그램에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="16d8d-145">응용 프로그램에서 한 Azure Active Directory 조직의 로그인만 허용하도록 하려면 *web.config*의 `Tenant` 매개 변수를 `Common`에서 조직의 테넌트 이름(예: *contoso.onmicrosoft.com*)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="16d8d-146">그런 다음 *OWIN 시작 클래스*의 `ValidateIssuer` 인수를 `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="16d8d-147">특정 조직 목록의 사용자만 허용하려면 `ValidateIssuer`를 true로 설정하고 `ValidIssuers` 매개 변수를 사용하여 조직 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="16d8d-148">또 다른 방법으로 IssuerValidator 매개 변수를 사용하여 발급자의 유효성을 검사하는 사용자 지정 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="16d8d-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="16d8d-149">`TokenValidationParameters`에 대한 자세한 내용은 [이](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN 문서") MSDN 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16d8d-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

