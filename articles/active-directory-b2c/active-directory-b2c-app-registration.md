---
title: "Azure Active Directory B2C: 응용 프로그램 등록 | Microsoft Docs"
description: "어떻게 tooregister 응용 프로그램을 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="995df-103">Azure Active Directory B2C: 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="995df-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="995df-104">이 Quickstart를 통해 몇 분 이내에 Microsoft Azure Active Directory(Azure AD) B2C 테넌트에서 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="995df-105">완료 되 면 hello Azure B2C 테 넌 트에 사용 하기 위해 응용 프로그램 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="995df-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="995df-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="995df-106">Prerequisites</span></span>

<span data-ttu-id="995df-107">toobuild 소비자를 등록 및 로그인을 허용 하는 응용 프로그램을 먼저 tooregister hello 응용 프로그램을 Azure Active Directory B2C 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="995df-108">에 설명 된 hello 단계를 사용 하 여 자신의 테 넌 트 가져오기 [Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="995df-109">Hello에서 hello Azure 포털에서에서 Azure AD B2C hello 블레이드에서 만든 응용 프로그램을 관리 해야 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="995df-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="995df-110">PowerShell 또는 다른 포털을 사용 하 여 hello B2C 응용 프로그램을 편집 하는 경우 지원 되지 않는 되며 Azure AD B2C 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="995df-111">Hello에 대 한 자세한 내용을 보려면 [응용 프로그램 오류가 발생 한](#faulted-apps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="995df-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="995df-112">TooB2C 설정 이동</span><span class="sxs-lookup"><span data-stu-id="995df-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="995df-113">Toohello 로그인 [Azure 포털](https://portal.azure.com/) 대로 hello hello B2C 테 넌 트의 전역 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="995df-114">등록 하는 hello 응용 프로그램 종류에 따라 다음 단계를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="995df-115">웹 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="995df-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="995df-116">웹 API 등록</span><span class="sxs-lookup"><span data-stu-id="995df-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="995df-117">모바일 또는 네이티브 앱 등록</span><span class="sxs-lookup"><span data-stu-id="995df-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="995df-118">웹앱 등록</span><span class="sxs-lookup"><span data-stu-id="995df-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="995df-119">웹 응용 프로그램이 Azure AD B2C에서 보호하는 웹 API를 호출하는 경우 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="995df-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="995df-120">Toohello 이동 하 여 응용 프로그램 암호를 만들 **키** hello를 클릭 하 고 블레이드 **키 생성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="995df-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="995df-121">Hello 기록 **응용 프로그램 키는** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="995df-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="995df-122">응용 프로그램의 코드에서 hello 응용 프로그램으로 hello 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="995df-123">**API 액세스**를 클릭하고 **추가**를 클릭한 다음 웹 API와 범위(사용 권한)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="995df-124">**응용 프로그램 비밀**은 중요한 보안 자격 증명이며 적절하게 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="995df-125">너무 점프**다음 단계**</span><span class="sxs-lookup"><span data-stu-id="995df-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="995df-126">웹 API 등록</span><span class="sxs-lookup"><span data-stu-id="995df-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="995df-127">클릭 **범위 게시** tooadd 더 필요에 따라 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="995df-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="995df-128">기본적으로 hello "user_impersonation" 범위 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="995df-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="995df-129">범위가 user_impersonation hello hello 로그인 한 사용자를 대신 하 여 다른 응용 프로그램 hello 기능 tooaccess이이 api를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="995df-130">원하는 경우에 범위가 user_impersonation hello를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="995df-131">너무 점프**다음 단계**</span><span class="sxs-lookup"><span data-stu-id="995df-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="995df-132">모바일 또는 네이티브 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="995df-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="995df-133">너무 점프**다음 단계**</span><span class="sxs-lookup"><span data-stu-id="995df-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="995df-134">제한 사항</span><span class="sxs-lookup"><span data-stu-id="995df-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="995df-135">웹앱 또는 API 회신 URL 선택</span><span class="sxs-lookup"><span data-stu-id="995df-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="995df-136">현재 응용 프로그램에 등록 된 Azure AD B2C는 회신 URL 값 집합이 제한 tooa 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="995df-137">웹 앱 및 서비스에 대 한 URL 구성표 hello로 시작 해야 하는 회신 hello `https`, 모든 회신 URL 값 단일 DNS 도메인을 공유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="995df-138">예를 들어 다음 회신 URL 중 하나가 있는 웹앱은 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="995df-139">hello 등록 시스템 hello hello 기존 회신 URL toohello DNS 이름 추가 하는 hello 회신 URL의 전체 DNS 이름과 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="995df-140">hello 요청 tooadd hello DNS 이름에는 hello 다음 조건 중 하나에 해당 하는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="995df-141">hello 새 회신 URL의 hello 전체 DNS 이름에는 hello 기존 회신 URL의 DNS 이름을 hello 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="995df-142">hello 새 회신 URL의 hello 전체 DNS 이름 hello 기존 회신 URL의 하위 도메인이 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="995df-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="995df-143">예를 들어 경우 hello 응용 프로그램에이 회신 URL:</span><span class="sxs-lookup"><span data-stu-id="995df-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="995df-144">다음과 같이 tooit를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="995df-145">이 경우 hello DNS 이름과 정확히 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="995df-146">또는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="995df-147">이 경우 login.contoso.com의 tooa DNS 하위 도메인을 참조 하 합니다. Toohave 로그인 east.contoso.com과 west.contoso.com 로그인 Url 회신으로 되어 있는 앱을 원하는 경우에이 순서 대로 해당 회신 Url을 추가 해야:</span><span class="sxs-lookup"><span data-stu-id="995df-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="995df-148">Hello 첫 번째 회신 URL의 하위 도메인에 있기 때문에 마지막 두 개의 hello를 추가할 수 있습니다 contoso.com입니다.</span><span class="sxs-lookup"><span data-stu-id="995df-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="995df-149">네이티브 앱 리디렉션 URI 선택</span><span class="sxs-lookup"><span data-stu-id="995df-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="995df-150">모바일/네이티브 응용 프로그램에 대한 리디렉션 URI를 선택하는 경우 두 가지 중요한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="995df-151">**고유**: hello 체계 hello 리디렉션 URI의 모든 응용 프로그램에 대 한 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="995df-152">예제 (com.onmicrosoft.contoso.appname://redirect/path) hello 구성표로 com.onmicrosoft.contoso.appname를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="995df-153">이 패턴을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-153">We recommend following this pattern.</span></span> <span data-ttu-id="995df-154">두 개의 응용 프로그램 hello를 공유 하는 경우 동일한 구성표 hello "앱을 선택" 대화 상자가 사용자에 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="995df-155">Hello 사용자가 잘못 선택 하면, hello 로그인 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="995df-156">**전체**: 리디렉션 URI에는 체계 및 경로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="995df-157">hello 경로 hello 도메인 (예를 들어 //contoso/ 작동 및 //contoso 실패) 한 후 하나 이상의 앞에 슬래시를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="995df-158">Hello에 밑줄이 리디렉션 uri와 같은 특수 문자가 없는 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="995df-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="995df-159">오류가 발생한 앱</span><span class="sxs-lookup"><span data-stu-id="995df-159">Faulted apps</span></span>

<span data-ttu-id="995df-160">B2C 응용 프로그램은 다음에서 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="995df-161">[Azure 클래식 포털](https://manage.windowsazure.com/) 및 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/)과 같은 다른 응용 프로그램 관리 포털.</span><span class="sxs-lookup"><span data-stu-id="995df-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="995df-162">Graph API 또는 PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="995df-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="995df-163">위에서 설명한 것 처럼 hello B2C 응용 프로그램을 편집 하 고 tooedit Azure 포털에서 Azure AD B2C hello 기능 블레이드에서 다시 hello, 오류가 발생 한 앱 되며 응용 프로그램을 Azure AD B2C 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="995df-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="995df-164">Toodelete hello 응용 프로그램이 있어야 하 고 다시 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="995df-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="995df-165">toodelete hello 앱 이동 toohello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/) hello 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="995df-166">Hello 응용 프로그램 toobe 표시에 대 한 순서, hello 응용 프로그램의 toobe hello 소유자 (및 hello 테 넌 트의 관리자 뿐 아니라) 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="995df-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="995df-167">Next steps</span></span>

<span data-ttu-id="995df-168">이제는 응용 프로그램에 등록 된 Azure AD B2C 했으므로 중 하나를 완료할 수 있습니다 [우리의 빠른 시작 자습서](active-directory-b2c-overview.md#get-started) tooget 작동 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="995df-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="995df-169">등록, 로그인 및 암호 재설정으로 ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="995df-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)