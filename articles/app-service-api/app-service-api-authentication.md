---
title: "Azure App Service의 API 앱에 대한 인증 및 권한 부여 | Microsoft Docs"
description: "Azure 앱 서비스에서 API 앱에 대해 제공하는 인증 및 권한 부여 서비스에 대해 알아보세요."
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
ms.openlocfilehash: f9fd533dfbd54517232f9dae5000ed4779baebd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a><span data-ttu-id="71dc1-103">Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="71dc1-103">Authentication and authorization for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="71dc1-104">개요</span><span class="sxs-lookup"><span data-stu-id="71dc1-104">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="71dc1-105">이 항목은 웹, 모바일 및 API 앱을 다루는 통합된 [앱 서비스 인증/권한 부여](../app-service/app-service-authentication-overview.md) 항목으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="71dc1-106">Azure App Service는 [OAuth 2.0](#oauth) 및 [OpenID Connect](#oauth)를 구현하는 기본 제공 인증 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-106">Azure App Service offers built-in authentication and authorization services that implement [OAuth 2.0](#oauth) and [OpenID Connect](#oauth).</span></span> <span data-ttu-id="71dc1-107">이 문서에서는 Azure 앱 서비스의 API 앱에 사용할 수 있는 서비스 및 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-107">This article describes the services and options that are available for API Apps in Azure App Service.</span></span>

<span data-ttu-id="71dc1-108">다음 다이어그램에서는 앱 서비스 인증의 몇 가지 주요 특징을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-108">The following diagram illustrates some key characteristics of App Service authentication:</span></span>

* <span data-ttu-id="71dc1-109">들어오는 API 요청을 전처리합니다. 즉, 앱 서비스에서 지원하는 모든 언어 또는 프레임워크와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-109">It preprocesses incoming API requests, which means it works with any language or framework supported by App Service.</span></span>
* <span data-ttu-id="71dc1-110">사용자 고유의 코드에서 얼마나 많은 인증이 작동하도록 할지에 대한 여러 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-110">It gives you several options for how much authentication work you want to do in your own code.</span></span>
* <span data-ttu-id="71dc1-111">최종 사용자 및 서비스 계정 인증 모두에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-111">It works for both end user and service account authentication.</span></span> 
* <span data-ttu-id="71dc1-112">여기서는 Azure Active Directory, Facebook, Google, Twitter 및 Microsoft 계정의 5가지 ID 공급자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-112">It supports five identity providers: Azure Active Directory, Facebook, Google, Twitter, and Microsoft Account.</span></span>
* <span data-ttu-id="71dc1-113">API 앱, 웹앱 및 모바일 앱에 대해서도 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-113">It works the same for API Apps, Web Apps, and Mobile Apps.</span></span>

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a><span data-ttu-id="71dc1-114">언어 알 수 없음</span><span class="sxs-lookup"><span data-stu-id="71dc1-114">Language agnostic</span></span>
<span data-ttu-id="71dc1-115">앱 서비스 인증 처리는 요청이 API 앱에 도달하기 전에 발생하므로 API 앱에 대해 작동하는 인증 기능은 임의 언어 또는 프레임워크로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-115">App Service authentication processing happens before requests reach your API app, which means that the authentication features work for API apps written in any language or framework.</span></span>  <span data-ttu-id="71dc1-116">사용자 API는 ASP.NET, Java, Node.js 또는 앱 서비스에서 지원하는 모든 프레임워크를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-116">Your API can be based on ASP.NET, Java, Node.js, or any framework that App Service supports.</span></span>

<span data-ttu-id="71dc1-117">앱 서비스가 HTTP 요청의 인증 헤더에서 JSON 웹 토큰(JWT)을 전달하고 임의 언어 또는 프레임워크로 작성된 코드는 해당 토큰에서 필요한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-117">App Service passes on the JSON web token (JWT) in the Authorization header of an HTTP request, and code written in any language or framework can get the information it needs from the token.</span></span> <span data-ttu-id="71dc1-118">또한 앱 서비스는 다음과 같은 몇 가지 특수 헤더를 설정하여 가장 일반적으로 사용되는 클레임에 보다 쉽게 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-118">In addition, App Service gives you easier access to the most commonly used claims by setting some special headers, such as the following:</span></span>

* <span data-ttu-id="71dc1-119">X-MS-CLIENT-PRINCIPAL-NAME</span><span class="sxs-lookup"><span data-stu-id="71dc1-119">X-MS-CLIENT-PRINCIPAL-NAME</span></span>
* <span data-ttu-id="71dc1-120">X-MS-CLIENT-PRINCIPAL-ID</span><span class="sxs-lookup"><span data-stu-id="71dc1-120">X-MS-CLIENT-PRINCIPAL-ID</span></span>
* <span data-ttu-id="71dc1-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span><span class="sxs-lookup"><span data-stu-id="71dc1-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span></span>
* <span data-ttu-id="71dc1-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span><span class="sxs-lookup"><span data-stu-id="71dc1-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span></span>

<span data-ttu-id="71dc1-123">.NET API에서 `Authorize` 특성을 사용할 수 있으며, 세분화된 권한 부여의 경우 클레임 정보는 .NET 클래스에 자동으로 채워지기 때문에 클레임을 기반으로 코드를 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-123">In a .NET API, you can use the `Authorize` attribute, and for fine-grained authorization you can easily write code based on claims because claims information is populated for you in .NET classes.</span></span>

## <a name="multiple-protection-options"></a><span data-ttu-id="71dc1-124">여러 보호 옵션</span><span class="sxs-lookup"><span data-stu-id="71dc1-124">Multiple protection options</span></span>
<span data-ttu-id="71dc1-125">앱 서비스는 익명 HTTP 요청이 API 앱에 도달하지 못하도록 하고 모든 요청을 전달하고 이를 포함하는 요청에 대한 토큰의 유효성을 검사하거나 작업 없이 모든 요청을 통과시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-125">App Service can prevent anonymous HTTP requests from reaching your API app, it can pass on all requests and validate tokens for requests that include them, or it can let through all requests without taking any action on them:</span></span>

1. <span data-ttu-id="71dc1-126">인증된 요청만 API 앱에 도달하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-126">Allow only authenticated requests to reach your API app.</span></span>
   
    <span data-ttu-id="71dc1-127">브라우저에서 익명 요청을 받으면 앱 서비스는 선택한 인증 공급자(Azure AD, Google, Twitter 등)의 로그온 페이지로 리디렉션합니다</span><span class="sxs-lookup"><span data-stu-id="71dc1-127">If an anonymous request is received from a browser, App Service will redirect to a logon page for the authentication provider (Azure AD, Google, Twitter, etc.) that you choose.</span></span> 
   
    <span data-ttu-id="71dc1-128">이 옵션을 사용하면 앱에서 인증 코드를 전혀 작성하지 않아도 되며 가장 중요한 클레임이 HTTP 헤더에 제공되므로 인증 코드가 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-128">With this option, you don't need to write any authentication code at all in your app, and authorization code is simplified because the most important claims are provided in the HTTP headers.</span></span>
2. <span data-ttu-id="71dc1-129">모든 요청이 API 앱에 도달하도록 허용하지만 인증된 요청을 유효성 검사하고 HTTP 헤더에 인증 정보를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-129">Allow all requests to reach your API app, but validate authenticated requests and pass along authentication information in the HTTP headers.</span></span>
   
    <span data-ttu-id="71dc1-130">이 옵션은 익명 요청 처리에 더 많은 유연성을 제공하지만 익명 사용자가 API를 사용하지 못하도록 하려면 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-130">This option gives you more flexibility in handling anonymous requests, but you have to write code if you want to prevent anonymous users from using your API.</span></span> <span data-ttu-id="71dc1-131">가장 일반적인 클레임은 HTTP 요청의 헤더에 전달되기 때문에 인증 코드는 비교적 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-131">Since the most popular claims are passed in the headers of HTTP requests, authorization code is relatively simple.</span></span>
3. <span data-ttu-id="71dc1-132">모든 요청이 API 앱에 도달하도록 허용하고 요청에서 인증 정보에 어떠한 작업도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-132">Allow all requests to reach your API, take no action on authentication information in the requests.</span></span>
   
    <span data-ttu-id="71dc1-133">이 옵션은 인증 및 권한 부여 작업을 전적으로 응용 프로그램 코드의 몫으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-133">This option leaves the tasks of authentication and authorization entirely up to your application code.</span></span>

<span data-ttu-id="71dc1-134">[Azure 포털](https://portal.azure.com/)의 **인증/권한 부여** 블레이드에서 원하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-134">In the [Azure portal](https://portal.azure.com/), you select the option you want on the **Authentication / Authorization** blade.</span></span>

![](./media/app-service-api-authentication/authblade.png)

<span data-ttu-id="71dc1-135">옵션 1과 2에 대해 **App Service 인증**을 설정하고 **요청이 인증되지 않은 경우에 수행할 동작** 드롭다운 목록에서 **로그인** 또는 **작업 없음(요청 허용)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-135">For options 1 and 2, turn on **App Service Authentication**, and in the **Action to take when request is not authenticated** drop-down list choose **Log in** or **Allow request (no action)**.</span></span>  <span data-ttu-id="71dc1-136">**로그인**을 선택한 경우 인증 공급자를 선택하고 해당 공급자를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-136">If you choose **Log in**, you have to choose an authentication provider and configure that provider.</span></span>

![](./media/app-service-api-authentication/actiontotake.png)

<span data-ttu-id="71dc1-137">인증 공급자 구성 블레이드를 구성하는 방법을 설명하는 자세한 지침은 [앱 서비스 응용 프로그램을 구성하여 Azure Active Directory 로그인을 사용하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-137">For detailed information about how to configure authentication, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="71dc1-138">이 문서는 모바일 앱 뿐만 아니라 API 앱에 적용되고 다른 인증 공급자에 대한 다른 문서에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-138">The article applies to API apps as well as mobile apps, and it links to other articles for the other authentication providers.</span></span>

## <span data-ttu-id="71dc1-139"><a id="internal"></a> 서비스 계정 인증</span><span class="sxs-lookup"><span data-stu-id="71dc1-139"><a id="internal"></a> Service account authentication</span></span>
<span data-ttu-id="71dc1-140">앱 서비스 인증은 한 API 앱에서 다른 API 앱을 호출하는 경우와 같은 내부 시나리오에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-140">App Service authentication works for internal scenarios such as for calling from one API app to another API app.</span></span> <span data-ttu-id="71dc1-141">이 시나리오에서는 최종 사용자 자격 증명 대신, 서비스 계정에 대한 자격 증명을 사용하여 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-141">In this scenario you get a token by using credentials for a service account instead of end user credentials.</span></span> <span data-ttu-id="71dc1-142">Azure Active Directory에서 서비스 계정은 *서비스 주체* 라고도 하며, 이러한 계정을 사용하는 인증을 서비스 간 시나리오라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-142">A service account is also known as a *service principal* in Azure Active Directory, and authentication using such an account is also known as a service-to-service scenario.</span></span> 

<span data-ttu-id="71dc1-143">서비스 간 시나리오의 경우 Azure Active Directory를 사용하여 호출된 API 앱을 보호하고 API 앱을 호출할 때 AAD 서비스 주체 권한 부여 토큰을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-143">For service-to-service scenarios, protect the called API app by using Azure Active Directory, and provide an AAD service principal authorization token when you call the API app.</span></span> <span data-ttu-id="71dc1-144">AAD 응용 프로그램에서 클라이언트 ID 및 클라이언트 암호를 제공하여 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-144">You get a token by providing the client ID and client secret from the AAD application.</span></span> <span data-ttu-id="71dc1-145">모바일 서비스 Zumo 토큰을 처리하는 데 사용되는 것과 같은 특수한 Azure 전용 코드는 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-145">No special Azure-only code is required, such as used to be true for handling the Mobile Services Zumo token.</span></span> <span data-ttu-id="71dc1-146">ASP.NET API 앱을 사용한 이 시나리오의 예는 [API 앱에 대한 서비스 주체 인증](app-service-api-dotnet-service-principal-auth.md)자습서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-146">An example of this scenario using ASP.NET API apps is covered by the tutorial [Service principal authentication for API Apps](app-service-api-dotnet-service-principal-auth.md).</span></span>

<span data-ttu-id="71dc1-147">앱 서비스 인증을 사용하지 않고 서비스 간 시나리오를 처리하려면 클라이언트 인증서 또는 기본 인증을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-147">If you want to handle a service-to-service scenario without using App Service authentication, you can use client certificates or basic authentication.</span></span> <span data-ttu-id="71dc1-148">Azure의 클라이언트 인증서에 대한 자세한 내용은 [웹앱에 대한 TLS 상호 인증을 구성하는 방법](../app-service-web/app-service-web-configure-tls-mutual-auth.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-148">For information about client certificates in Azure, see [How To Configure TLS Mutual Authentication for Web Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span> <span data-ttu-id="71dc1-149">ASP.NET에서 기본 인증에 대한 자세한 내용은 [ASP.NET Web API 2에서의 인증 필터](http://www.asp.net/web-api/overview/security/authentication-filters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-149">For information about basic authentication in ASP.NET, see [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).</span></span>

<span data-ttu-id="71dc1-150">앱 서비스 논리 앱에서 API 앱으로 서비스 계정 인증은 [논리 앱으로 앱 서비스에서 호스팅되는 사용자 지정 API 사용](../logic-apps/logic-apps-custom-hosted-api.md)에 설명된 특수 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-150">Service account authentication from an App Service logic app to an API app is a special case that is explained in [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>

## <a name="mobile-client-authentication"></a><span data-ttu-id="71dc1-151">모바일 클라이언트 인증</span><span class="sxs-lookup"><span data-stu-id="71dc1-151">Mobile client authentication</span></span>
<span data-ttu-id="71dc1-152">모바일 클라이언트에서 인증을 처리하는 방법에 대한 내용은 [모바일 앱을 위한 인증에 대한 설명서](../app-service-mobile/app-service-mobile-ios-get-started-users.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-152">For information about how to handle authentication from mobile clients, see the [documentation on authentication for mobile apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md).</span></span> <span data-ttu-id="71dc1-153">앱 서비스 인증은 모바일 앱 및 API 앱에서 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-153">App Service authentication works the same way for mobile apps and API apps.</span></span>

## <a name="more-information"></a><span data-ttu-id="71dc1-154">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="71dc1-154">More information</span></span>
<span data-ttu-id="71dc1-155">Azure 앱 서비스에서 인증 및 권한 부여에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-155">For more information about authentication and authorization in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="71dc1-156">앱 서비스 인증/권한 부여 확장</span><span class="sxs-lookup"><span data-stu-id="71dc1-156">Expanding App Service authentication / authorization</span></span>](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* <span data-ttu-id="71dc1-157">[앱 서비스 응용 프로그램을 구성하여 Azure Active Directory 로그인을 사용하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (페이지 맨 위에 있는 다른 인증 공급자에 대한 링크를 포함합니다.)</span><span class="sxs-lookup"><span data-stu-id="71dc1-157">[How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (Includes links for other authentication providers at the top of the page.)</span></span> 

<span data-ttu-id="71dc1-158">OAuth 2.0, OpenID Connect 및 JSON 웹 토큰(JWT)에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-158">For more information about OAuth 2.0, OpenID Connect, and JSON Web Tokens (JWT), see the following resources.</span></span>

* [<span data-ttu-id="71dc1-159">OAuth 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="71dc1-159">Getting started with OAuth 2.0</span></span>](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [<span data-ttu-id="71dc1-160">OAuth2, OpenID Connect 및 JWT(JSON 웹 토큰) 소개 - Pluralsight 과정(영문)</span><span class="sxs-lookup"><span data-stu-id="71dc1-160">Introduction to OAuth2, OpenID Connect and JSON Web Tokens (JWT) - Pluralsight Course</span></span>](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [<span data-ttu-id="71dc1-161">ASP.NET에서 여러 클라이언트에 대한 RESTful API 빌드 및 보안 설정 - Pluralsight 과정(영문)</span><span class="sxs-lookup"><span data-stu-id="71dc1-161">Building and Securing a RESTful API for Multiple Clients in ASP.NET - Pluralsight course</span></span>](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

<span data-ttu-id="71dc1-162">Azure Active Directory에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71dc1-162">For more information about Azure Active Directory, see the following resources.</span></span>

* [<span data-ttu-id="71dc1-163">Azure AD 시나리오</span><span class="sxs-lookup"><span data-stu-id="71dc1-163">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="71dc1-164">Azure AD 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="71dc1-164">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="71dc1-165">Azure AD 샘플</span><span class="sxs-lookup"><span data-stu-id="71dc1-165">Azure AD samples</span></span>](http://aka.ms/aadsamples)

## <a name="next-steps"></a><span data-ttu-id="71dc1-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71dc1-166">Next steps</span></span>
<span data-ttu-id="71dc1-167">이 문서에서는 API 앱에 사용할 수 있는 앱 서비스의 인증 및 권한 부여 기능을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-167">This article has explained authentication and authorization features of App Service that you can use for API apps.</span></span> <span data-ttu-id="71dc1-168">시작 시리즈의 다음 자습서는 [앱 서비스 API 앱의 사용자 인증](app-service-api-dotnet-user-principal-auth.md)을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71dc1-168">The next tutorial in the getting started series shows how to implement [user authentication in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).</span></span>

