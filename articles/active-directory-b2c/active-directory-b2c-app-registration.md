---
title: "Azure Active Directory B2C: 응용 프로그램 등록 | Microsoft Docs"
description: "Azure Active Directory B2C로 응용 프로그램 등록하는 방법"
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
ms.openlocfilehash: 3d4fe2fa10d848c8b29e4d22d284c0d378f07ae0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="3e3f2-103">Azure Active Directory B2C: 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="3e3f2-104">이 Quickstart를 통해 몇 분 이내에 Microsoft Azure Active Directory(Azure AD) B2C 테넌트에서 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="3e3f2-105">완료되면 Azure B2C 테넌트에서 사용할 수 있도록 응용 프로그램이 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e3f2-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e3f2-106">Prerequisites</span></span>

<span data-ttu-id="3e3f2-107">소비자 등록 및 로그인을 수락하는 응용 프로그램을 만들려면 먼저 Azure Active Directory B2C 테넌트를 사용하여 해당 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="3e3f2-108">[Azure AD B2C 테넌트 만들기](active-directory-b2c-get-started.md)에 요약한 단계를 사용하여 자신의 테넌트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="3e3f2-109">Azure Portal의 Azure AD B2C 블레이드에서 만든 응용 프로그램은 동일한 위치에서 관리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="3e3f2-110">PowerShell 또는 다른 포털을 사용하여 B2C 응용 프로그램을 편집할 경우 지원을 받을 수 없게 되며 Azure AD B2C에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="3e3f2-111">[오류가 발생한 앱](#faulted-apps) 섹션에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="3e3f2-112">B2C 설정으로 이동</span><span class="sxs-lookup"><span data-stu-id="3e3f2-112">Navigate to B2C settings</span></span>

<span data-ttu-id="3e3f2-113">B2C 테넌트의 전역 관리자로 [Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="3e3f2-114">등록하려는 응용 프로그램 형식에 따라 다음 단계를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-114">Choose next steps based on the application type you are registering:</span></span>

* [<span data-ttu-id="3e3f2-115">웹 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="3e3f2-116">웹 API 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="3e3f2-117">모바일 또는 네이티브 앱 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="3e3f2-118">웹앱 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="3e3f2-119">웹 응용 프로그램이 Azure AD B2C에서 보호하는 웹 API를 호출하는 경우 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="3e3f2-120">**키** 블레이드로 이동하여 **키 생성** 단추를 클릭하여 응용 프로그램 비밀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-120">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="3e3f2-121">**앱 키** 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-121">Make note of the **App key** value.</span></span> <span data-ttu-id="3e3f2-122">이 값을 응용 프로그램의 코드에서 응용 프로그램 비밀로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-122">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="3e3f2-123">**API 액세스**를 클릭하고 **추가**를 클릭한 다음 웹 API와 범위(사용 권한)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="3e3f2-124">**응용 프로그램 비밀**은 중요한 보안 자격 증명이며 적절하게 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="3e3f2-125">**다음 단계**로 이동</span><span class="sxs-lookup"><span data-stu-id="3e3f2-125">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="3e3f2-126">웹 API 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="3e3f2-127">**게시된 범위**를 클릭하여 필요에 따라 범위를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-127">Click **Published scopes** to add more scopes as necessary.</span></span> <span data-ttu-id="3e3f2-128">기본적으로 "user_impersonation" 범위가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-128">By default, the "user_impersonation" scope is defined.</span></span> <span data-ttu-id="3e3f2-129">user_impersonation 범위가 로그인한 사용자를 대신하여 다른 응용 프로그램이 이 API에 액세스할 수 있는 기능을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-129">The user_impersonation scope gives other applications the ability to access this api on behalf of the signed-in user.</span></span> <span data-ttu-id="3e3f2-130">원하는 경우에 user_impersonation 범위를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-130">If you wish, the user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="3e3f2-131">**다음 단계**로 이동</span><span class="sxs-lookup"><span data-stu-id="3e3f2-131">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="3e3f2-132">모바일 또는 네이티브 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="3e3f2-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="3e3f2-133">**다음 단계**로 이동</span><span class="sxs-lookup"><span data-stu-id="3e3f2-133">Jump to **next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="3e3f2-134">제한 사항</span><span class="sxs-lookup"><span data-stu-id="3e3f2-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="3e3f2-135">웹앱 또는 API 회신 URL 선택</span><span class="sxs-lookup"><span data-stu-id="3e3f2-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="3e3f2-136">현재, Azure AD B2C에 등록된 앱은 제한된 회신 URL 값 집합으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-136">Currently, apps that are registered with Azure AD B2C are restricted to a limited set of reply URL values.</span></span> <span data-ttu-id="3e3f2-137">웹앱 및 서비스에 대한 회산 URL은 스키마 `https`로 시작해야 하고 모든 회신 URL 값은 단일 DNS 도메인을 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-137">The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="3e3f2-138">예를 들어 다음 회신 URL 중 하나가 있는 웹앱은 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="3e3f2-139">등록 시스템은 기존 회신 URL의 전체 DNS 이름을 편집하려는 회신 URL의 DNS 이름과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-139">The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding.</span></span> <span data-ttu-id="3e3f2-140">다음 조건 중 하나라도 충족되는 경우 DNS 이름을 추가하는 요청이 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-140">The request to add the DNS name fails if either of the following conditions is true:</span></span>

* <span data-ttu-id="3e3f2-141">새 회신 URL의 전체 DNS 이름이 기존 회신 URL의 DNS 이름과 일치하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="3e3f2-141">The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.</span></span>
* <span data-ttu-id="3e3f2-142">새 회신 URL의 전체 DNS 이름이 기존 회신 URL의 하위 도메인이 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="3e3f2-142">The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.</span></span>

<span data-ttu-id="3e3f2-143">예를 들어 앱에 다음 회신 URL이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="3e3f2-143">For example, if the app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="3e3f2-144">다음과 같이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-144">You can add to it, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="3e3f2-145">이 경우 DNS 이름이 정확히 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-145">In this case, the DNS name matches exactly.</span></span> <span data-ttu-id="3e3f2-146">또는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="3e3f2-147">이 경우 login.contoso.com의 DNS 하위 도메인을 참조합니다. 회신 URL로 login-east.contoso.com 및 login-west.contoso.com을 사용하는 앱을 원하는 경우 다음 회신 URL을 순서대로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-147">In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="3e3f2-148">뒤의 두 개는 첫 번째 회신 URL의 하위 도메인이므로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-148">You can add the latter two because they are subdomains of the first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="3e3f2-149">네이티브 앱 리디렉션 URI 선택</span><span class="sxs-lookup"><span data-stu-id="3e3f2-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="3e3f2-150">모바일/네이티브 응용 프로그램에 대한 리디렉션 URI를 선택하는 경우 두 가지 중요한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="3e3f2-151">**고유**: 리디렉션 URI의 체계는 모든 응용 프로그램에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-151">**Unique**: The scheme of the redirect URI should be unique for every application.</span></span> <span data-ttu-id="3e3f2-152">예제에서는(com.onmicrosoft.contoso.appname://redirect/path) 체계로 com.onmicrosoft.contoso.appname을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as the scheme.</span></span> <span data-ttu-id="3e3f2-153">이 패턴을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-153">We recommend following this pattern.</span></span> <span data-ttu-id="3e3f2-154">두 개의 응용 프로그램이 동일한 체계를 공유하는 경우 "앱 선택" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-154">If two applications share the same scheme, the user sees a "choose app" dialog.</span></span> <span data-ttu-id="3e3f2-155">사용자가 잘못 선택하는 경우 로그인이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-155">If the user makes an incorrect choice, the login fails.</span></span>
* <span data-ttu-id="3e3f2-156">**전체**: 리디렉션 URI에는 체계 및 경로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="3e3f2-157">경로는 도메인 뒤에 하나 이상의 슬래시를 포함해야 합니다(예: //contoso/는 작동, //contoso는 실패).</span><span class="sxs-lookup"><span data-stu-id="3e3f2-157">The path must contain at least one forward slash after the domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="3e3f2-158">리디렉션 uri에 밑줄과 같은 특수 문자가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-158">Ensure there are no special characters like underscores in the redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="3e3f2-159">오류가 발생한 앱</span><span class="sxs-lookup"><span data-stu-id="3e3f2-159">Faulted apps</span></span>

<span data-ttu-id="3e3f2-160">B2C 응용 프로그램은 다음에서 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="3e3f2-161">[Azure 클래식 포털](https://manage.windowsazure.com/) 및 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/)과 같은 다른 응용 프로그램 관리 포털.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="3e3f2-162">Graph API 또는 PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="3e3f2-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="3e3f2-163">위에서 설명한 대로 B2C 응용 프로그램을 편집하고 Azure Portal의 Azure AD B2C 기능 블레이드에서 다시 편집하려는 경우 오류가 발생한 앱이 되고 응용 프로그램은 Azure AD B2C와 함께 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-163">If you edit the B2C application as described above and try to edit it again in the Azure AD B2C features blade on the Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="3e3f2-164">응용 프로그램을 삭제하고 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-164">You have to delete the application and create it again.</span></span>

<span data-ttu-id="3e3f2-165">앱을 삭제하려면 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/)로 이동하고 거기에서 응용 프로그램을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-165">To delete the app, go to the [Application Registration Portal](https://apps.dev.microsoft.com/) and delete the application there.</span></span> <span data-ttu-id="3e3f2-166">응용 프로그램을 표시하려면 응용 프로그램의 소유자여야 합니다(테넌트의 관리자가 아님).</span><span class="sxs-lookup"><span data-stu-id="3e3f2-166">In order for the application to be visible, you need to be the owner of the application (and not just an admin of the tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e3f2-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e3f2-167">Next steps</span></span>

<span data-ttu-id="3e3f2-168">Azure AD B2C로 등록된 응용 프로그램이 있다면 작동할 [빠른 시작 자습서](active-directory-b2c-overview.md#get-started) 중 하나를 완료하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3f2-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) to get up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e3f2-169">등록, 로그인 및 암호 재설정으로 ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3e3f2-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)