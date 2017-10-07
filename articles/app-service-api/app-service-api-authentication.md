---
title: "aaaAuthentication 및 Azure 앱 서비스에서 API 앱에 대 한 권한 부여 | Microsoft Docs"
description: "Azure 앱 서비스 API 앱에 대해 제공 하는 hello 인증 및 권한 부여 서비스를 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a><span data-ttu-id="eb425-103">Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="eb425-103">Authentication and authorization for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="eb425-104">개요</span><span class="sxs-lookup"><span data-stu-id="eb425-104">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="eb425-105">이 항목에는 마이그레이션된 tooa 통합 됩니다 [응용 프로그램 서비스 인증 / 권한 부여](../app-service/app-service-authentication-overview.md) 웹, 모바일 및 API 앱에 설명 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-105">This topic will be migrated tooa consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="eb425-106">Azure App Service는 [OAuth 2.0](#oauth) 및 [OpenID Connect](#oauth)를 구현하는 기본 제공 인증 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-106">Azure App Service offers built-in authentication and authorization services that implement [OAuth 2.0](#oauth) and [OpenID Connect](#oauth).</span></span> <span data-ttu-id="eb425-107">이 문서에서는 hello 서비스 및 Azure 앱 서비스에서 API 앱에 사용할 수 있는 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-107">This article describes hello services and options that are available for API Apps in Azure App Service.</span></span>

<span data-ttu-id="eb425-108">hello 다음 다이어그램에서는 응용 프로그램 서비스 인증의 주요 특징을 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-108">hello following diagram illustrates some key characteristics of App Service authentication:</span></span>

* <span data-ttu-id="eb425-109">들어오는 API 요청을 전처리합니다. 즉, 앱 서비스에서 지원하는 모든 언어 또는 프레임워크와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-109">It preprocesses incoming API requests, which means it works with any language or framework supported by App Service.</span></span>
* <span data-ttu-id="eb425-110">제공 양을 인증이 작동 하기 위한 몇 가지 옵션을 원하는 toodo 사용자 코드에서.</span><span class="sxs-lookup"><span data-stu-id="eb425-110">It gives you several options for how much authentication work you want toodo in your own code.</span></span>
* <span data-ttu-id="eb425-111">최종 사용자 및 서비스 계정 인증 모두에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-111">It works for both end user and service account authentication.</span></span> 
* <span data-ttu-id="eb425-112">여기서는 Azure Active Directory, Facebook, Google, Twitter 및 Microsoft 계정의 5가지 ID 공급자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-112">It supports five identity providers: Azure Active Directory, Facebook, Google, Twitter, and Microsoft Account.</span></span>
* <span data-ttu-id="eb425-113">그 작동 hello API 앱, 웹 앱 및 모바일 앱에 대해 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-113">It works hello same for API Apps, Web Apps, and Mobile Apps.</span></span>

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a><span data-ttu-id="eb425-114">언어 알 수 없음</span><span class="sxs-lookup"><span data-stu-id="eb425-114">Language agnostic</span></span>
<span data-ttu-id="eb425-115">앱 서비스 인증 처리 요청을 모든 언어 또는 프레임 워크에서 작성 된 앱의 API는 hello 인증 기능이 작동 의미 API 앱에 도달 하기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-115">App Service authentication processing happens before requests reach your API app, which means that hello authentication features work for API apps written in any language or framework.</span></span>  <span data-ttu-id="eb425-116">사용자 API는 ASP.NET, Java, Node.js 또는 앱 서비스에서 지원하는 모든 프레임워크를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-116">Your API can be based on ASP.NET, Java, Node.js, or any framework that App Service supports.</span></span>

<span data-ttu-id="eb425-117">앱 서비스는 HTTP 요청의 인증 헤더 hello에에서 hello JSON 웹 토큰 (JWT)에 전달 하 고 작성 된 코드에서 모든 언어 또는 프레임 워크 정보를 얻을 수 hello 필요한 hello에서 토큰.</span><span class="sxs-lookup"><span data-stu-id="eb425-117">App Service passes on hello JSON web token (JWT) in hello Authorization header of an HTTP request, and code written in any language or framework can get hello information it needs from hello token.</span></span> <span data-ttu-id="eb425-118">또한 응용 프로그램 서비스 사용 하면 보다 쉽게 toohello 가장 일반적으로 사용 되는 클레임 hello 다음과 같은 몇 가지 특수 한 헤더를 설정 하 여:</span><span class="sxs-lookup"><span data-stu-id="eb425-118">In addition, App Service gives you easier access toohello most commonly used claims by setting some special headers, such as hello following:</span></span>

* <span data-ttu-id="eb425-119">X-MS-CLIENT-PRINCIPAL-NAME</span><span class="sxs-lookup"><span data-stu-id="eb425-119">X-MS-CLIENT-PRINCIPAL-NAME</span></span>
* <span data-ttu-id="eb425-120">X-MS-CLIENT-PRINCIPAL-ID</span><span class="sxs-lookup"><span data-stu-id="eb425-120">X-MS-CLIENT-PRINCIPAL-ID</span></span>
* <span data-ttu-id="eb425-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span><span class="sxs-lookup"><span data-stu-id="eb425-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span></span>
* <span data-ttu-id="eb425-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span><span class="sxs-lookup"><span data-stu-id="eb425-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span></span>

<span data-ttu-id="eb425-123">.NET API에서 hello를 사용할 수 있습니다 `Authorize` 특성을 쉽게 작성할 수 있는 세분화 된 권한 부여의 코드에 따라 클레임.NET 클래스에 사용자에 대 한 클레임 정보가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-123">In a .NET API, you can use hello `Authorize` attribute, and for fine-grained authorization you can easily write code based on claims because claims information is populated for you in .NET classes.</span></span>

## <a name="multiple-protection-options"></a><span data-ttu-id="eb425-124">여러 보호 옵션</span><span class="sxs-lookup"><span data-stu-id="eb425-124">Multiple protection options</span></span>
<span data-ttu-id="eb425-125">앱 서비스는 익명 HTTP 요청이 API 앱에 도달하지 못하도록 하고 모든 요청을 전달하고 이를 포함하는 요청에 대한 토큰의 유효성을 검사하거나 작업 없이 모든 요청을 통과시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-125">App Service can prevent anonymous HTTP requests from reaching your API app, it can pass on all requests and validate tokens for requests that include them, or it can let through all requests without taking any action on them:</span></span>

1. <span data-ttu-id="eb425-126">인증 된 요청 tooreach만 API 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-126">Allow only authenticated requests tooreach your API app.</span></span>
   
    <span data-ttu-id="eb425-127">앱 서비스는 hello 인증 공급자에 대 한 tooa 로그온 페이지를 리디렉션합니다 익명 요청은 브라우저에서 수신 되 면 (Azure AD, Google, Twitter 등) 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-127">If an anonymous request is received from a browser, App Service will redirect tooa logon page for hello authentication provider (Azure AD, Google, Twitter, etc.) that you choose.</span></span> 
   
    <span data-ttu-id="eb425-128">이 옵션을 사용에서 필요 없는 toowrite 인증 코드 전혀 응용 프로그램 및 권한 부여 코드 단순 하 여 hello 가장 중요 한 클레임 hello HTTP 헤더에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-128">With this option, you don't need toowrite any authentication code at all in your app, and authorization code is simplified because hello most important claims are provided in hello HTTP headers.</span></span>
2. <span data-ttu-id="eb425-129">모든 요청 tooreach API 앱을 허용 하지만 인증 된 요청의 유효성을 검사 하 고 hello HTTP 헤더의 인증 정보를 따라 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-129">Allow all requests tooreach your API app, but validate authenticated requests and pass along authentication information in hello HTTP headers.</span></span>
   
    <span data-ttu-id="eb425-130">이 옵션을이 선택 하면 보다 융통성 있게 익명 요청을 처리 하지만 API를 사용 하 여 익명 사용자가 tooprevent toowrite 코드가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-130">This option gives you more flexibility in handling anonymous requests, but you have toowrite code if you want tooprevent anonymous users from using your API.</span></span> <span data-ttu-id="eb425-131">Hello 가장 인기 있는 클레임의 HTTP 요청 헤더 hello에에서 전달 되는 경우 이후 인증 코드는 비교적 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-131">Since hello most popular claims are passed in hello headers of HTTP requests, authorization code is relatively simple.</span></span>
3. <span data-ttu-id="eb425-132">모든 요청 tooreach API 허용, hello 요청에 인증 정보에 대해 어떤 작업도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-132">Allow all requests tooreach your API, take no action on authentication information in hello requests.</span></span>
   
    <span data-ttu-id="eb425-133">이 옵션의 인증 및 권한 부여 tooyour 응용 프로그램 코드를 완전히 hello 작업을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-133">This option leaves hello tasks of authentication and authorization entirely up tooyour application code.</span></span>

<span data-ttu-id="eb425-134">Hello에 [Azure 포털](https://portal.azure.com/), hello에서 원하는 hello 옵션을 선택 하면 **인증 / 권한 부여** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-134">In hello [Azure portal](https://portal.azure.com/), you select hello option you want on hello **Authentication / Authorization** blade.</span></span>

![](./media/app-service-api-authentication/authblade.png)

<span data-ttu-id="eb425-135">옵션 1 및 2에 대 한 설정 **응용 프로그램 서비스 인증**, 및 hello **요청이 인증 되지 않은 경우 동작 tootake** 드롭다운 목록에서 선택 **로그인** 또는 **요청 허용 동작이 없습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-135">For options 1 and 2, turn on **App Service Authentication**, and in hello **Action tootake when request is not authenticated** drop-down list choose **Log in** or **Allow request (no action)**.</span></span>  <span data-ttu-id="eb425-136">선택 하면 **로그인**, toochoose 인증 공급자도 보유 하 고 해당 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-136">If you choose **Log in**, you have toochoose an authentication provider and configure that provider.</span></span>

![](./media/app-service-api-authentication/actiontotake.png)

<span data-ttu-id="eb425-137">방법에 대 한 자세한 내용은 tooconfigure 인증 참조 [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-137">For detailed information about how tooconfigure authentication, see [How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="eb425-138">hello 문서 tooAPI 앱 뿐 아니라 모바일 앱을 적용 하며 hello에 대 한 tooother 아티클을 다른 인증 공급자 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-138">hello article applies tooAPI apps as well as mobile apps, and it links tooother articles for hello other authentication providers.</span></span>

## <span data-ttu-id="eb425-139"><a id="internal"></a> 서비스 계정 인증</span><span class="sxs-lookup"><span data-stu-id="eb425-139"><a id="internal"></a> Service account authentication</span></span>
<span data-ttu-id="eb425-140">앱 서비스 인증 같은 내부 시나리오 한 API 앱 tooanother API 앱에서 호출 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-140">App Service authentication works for internal scenarios such as for calling from one API app tooanother API app.</span></span> <span data-ttu-id="eb425-141">이 시나리오에서는 최종 사용자 자격 증명 대신, 서비스 계정에 대한 자격 증명을 사용하여 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-141">In this scenario you get a token by using credentials for a service account instead of end user credentials.</span></span> <span data-ttu-id="eb425-142">Azure Active Directory에서 서비스 계정은 *서비스 주체* 라고도 하며, 이러한 계정을 사용하는 인증을 서비스 간 시나리오라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-142">A service account is also known as a *service principal* in Azure Active Directory, and authentication using such an account is also known as a service-to-service scenario.</span></span> 

<span data-ttu-id="eb425-143">서비스 간 시나리오에 대 한 Azure Active Directory를 사용 하 여 API 앱을 호출 하는 hello를 보호 하 고 hello API 앱을 호출할 때 AAD 서비스 주체 권한 부여 토큰을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-143">For service-to-service scenarios, protect hello called API app by using Azure Active Directory, and provide an AAD service principal authorization token when you call hello API app.</span></span> <span data-ttu-id="eb425-144">Hello 클라이언트 ID와 클라이언트 hello AAD 응용 프로그램에서에서 암호를 제공 하 여 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-144">You get a token by providing hello client ID and client secret from hello AAD application.</span></span> <span data-ttu-id="eb425-145">Hello 모바일 서비스 Zumo 토큰을 처리 하기 위한 사용 되는 toobe true와 같이 필요한 된 특별 한 Azure 전용 코드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-145">No special Azure-only code is required, such as used toobe true for handling hello Mobile Services Zumo token.</span></span> <span data-ttu-id="eb425-146">Hello 자습서에서 검사 하는 ASP.NET API 앱을 사용 하 여이 시나리오의 예로 [서비스 API 앱에 대 한 사용자 인증](app-service-api-dotnet-service-principal-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-146">An example of this scenario using ASP.NET API apps is covered by hello tutorial [Service principal authentication for API Apps](app-service-api-dotnet-service-principal-auth.md).</span></span>

<span data-ttu-id="eb425-147">앱 서비스 인증을 사용 하지 않고 toohandle 서비스 간 시나리오를 원하는 경우 클라이언트 인증서 또는 기본 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-147">If you want toohandle a service-to-service scenario without using App Service authentication, you can use client certificates or basic authentication.</span></span> <span data-ttu-id="eb425-148">Azure의 클라이언트 인증서에 대 한 정보를 참조 하십시오. [어떻게 tooConfigure 웹 앱에 대 한 상호 인증 TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-148">For information about client certificates in Azure, see [How tooConfigure TLS Mutual Authentication for Web Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span> <span data-ttu-id="eb425-149">ASP.NET에서 기본 인증에 대한 자세한 내용은 [ASP.NET Web API 2에서의 인증 필터](http://www.asp.net/web-api/overview/security/authentication-filters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb425-149">For information about basic authentication in ASP.NET, see [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).</span></span>

<span data-ttu-id="eb425-150">앱 서비스 논리 앱 tooan API 앱에서 계정 인증 서비스는에서 설명 하는 특별 한 경우 [논리 앱과 앱 서비스에서 호스팅되는 사용자 지정 API를 사용 하 여](../logic-apps/logic-apps-custom-hosted-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-150">Service account authentication from an App Service logic app tooan API app is a special case that is explained in [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>

## <a name="mobile-client-authentication"></a><span data-ttu-id="eb425-151">모바일 클라이언트 인증</span><span class="sxs-lookup"><span data-stu-id="eb425-151">Mobile client authentication</span></span>
<span data-ttu-id="eb425-152">방법에 대 한 내용은 모바일 클라이언트 로부터의 인증 toohandle 참조 hello [모바일 앱에 대 한 인증에 대 한 설명서](../app-service-mobile/app-service-mobile-ios-get-started-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-152">For information about how toohandle authentication from mobile clients, see hello [documentation on authentication for mobile apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md).</span></span> <span data-ttu-id="eb425-153">앱 서비스 인증은 hello 모바일 앱 및 API 앱 모두에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-153">App Service authentication works hello same way for mobile apps and API apps.</span></span>

## <a name="more-information"></a><span data-ttu-id="eb425-154">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="eb425-154">More information</span></span>
<span data-ttu-id="eb425-155">인증 및 Azure 앱 서비스의 권한 부여에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eb425-155">For more information about authentication and authorization in Azure App Service, see hello following resources:</span></span>

* [<span data-ttu-id="eb425-156">앱 서비스 인증/권한 부여 확장</span><span class="sxs-lookup"><span data-stu-id="eb425-156">Expanding App Service authentication / authorization</span></span>](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* <span data-ttu-id="eb425-157">[어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (hello hello 페이지 위쪽에 다른 인증 공급자에 대 한 링크를 포함 합니다.)</span><span class="sxs-lookup"><span data-stu-id="eb425-157">[How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (Includes links for other authentication providers at hello top of hello page.)</span></span> 

<span data-ttu-id="eb425-158">OAuth 2.0, OpenID Connect 및 JSON 웹 토큰 (JWT)에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eb425-158">For more information about OAuth 2.0, OpenID Connect, and JSON Web Tokens (JWT), see hello following resources.</span></span>

* [<span data-ttu-id="eb425-159">OAuth 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="eb425-159">Getting started with OAuth 2.0</span></span>](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [<span data-ttu-id="eb425-160">소개 tooOAuth2 OpenID Connect 및 JSON 웹 토큰 (JWT)-Pluralsight 과정</span><span class="sxs-lookup"><span data-stu-id="eb425-160">Introduction tooOAuth2, OpenID Connect and JSON Web Tokens (JWT) - Pluralsight Course</span></span>](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [<span data-ttu-id="eb425-161">ASP.NET에서 여러 클라이언트에 대한 RESTful API 빌드 및 보안 설정 - Pluralsight 과정(영문)</span><span class="sxs-lookup"><span data-stu-id="eb425-161">Building and Securing a RESTful API for Multiple Clients in ASP.NET - Pluralsight course</span></span>](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

<span data-ttu-id="eb425-162">Azure Active Directory에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eb425-162">For more information about Azure Active Directory, see hello following resources.</span></span>

* [<span data-ttu-id="eb425-163">Azure AD 시나리오</span><span class="sxs-lookup"><span data-stu-id="eb425-163">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="eb425-164">Azure AD 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="eb425-164">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="eb425-165">Azure AD 샘플</span><span class="sxs-lookup"><span data-stu-id="eb425-165">Azure AD samples</span></span>](http://aka.ms/aadsamples)

## <a name="next-steps"></a><span data-ttu-id="eb425-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb425-166">Next steps</span></span>
<span data-ttu-id="eb425-167">이 문서에서는 API 앱에 사용할 수 있는 앱 서비스의 인증 및 권한 부여 기능을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-167">This article has explained authentication and authorization features of App Service that you can use for API apps.</span></span> <span data-ttu-id="eb425-168">hello hello를 가져올 수 있는 다음 자습서 시작 계열 표시 방법을 tooimplement [앱 서비스 API 앱에서 사용자 인증](app-service-api-dotnet-user-principal-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb425-168">hello next tutorial in hello getting started series shows how tooimplement [user authentication in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).</span></span>

