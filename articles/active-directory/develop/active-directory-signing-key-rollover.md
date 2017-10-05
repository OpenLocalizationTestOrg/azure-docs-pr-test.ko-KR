---
title: "Azure AD에서 서명 키 롤오버 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에 대한 서명 키 롤오버 모범 사례를 설명합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="06f36-103">Azure Active Directory에서 서명 키 롤오버</span><span class="sxs-lookup"><span data-stu-id="06f36-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="06f36-104">이 항목에서는 보안 토큰을 서명하기 위해 Azure AD(Azure Active Directory)에 사용되는 공개 키에 대해 알아야 할 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="06f36-105">이러한 키 롤오버가 정기적으로 있으며, 비상 시에는 곧바로 롤오버될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="06f36-106">Azure AD를 사용하는 모든 응용 프로그램은 키 롤오버 프로세스를 프로그래밍 방식으로 처리하거나 정기적인 수동 롤오버 프로세스를 설정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="06f36-107">키의 작동 방식과 롤오버가 응용 프로그램에 미친 영향을 평가하는 방법, 필요한 경우 키 롤오버를 처리하도록 응용 프로그램을 업데이트하거나 정기적인 수동 롤오버 프로세스를 설정하는 방법을 이해하려면 계속 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="06f36-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="06f36-108">Azure AD의 서명 키 개요</span><span class="sxs-lookup"><span data-stu-id="06f36-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="06f36-109">Azure AD는 업계 표준을 기반으로 하는 공개 키 암호화를 사용하여 Azure AD 자체 및 이를 사용하는 응용 프로그램 간의 트러스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="06f36-110">실질적인 측면에서, Azure AD는 공개 및 개인 키 쌍으로 구성된 서명 키를 사용하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="06f36-111">사용자가 인증을 위해 Azure AD를 사용하는 응용 프로그램에 로그인하면 Azure AD는 사용자에 대한 정보가 포함된 보안 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="06f36-112">이 토큰은 응용 프로그램으로 다시 전송되기 전에 개인 키를 사용하여 Azure AD에 의해 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="06f36-113">해당 토큰이 유효하고 실제로 Azure AD에서 발생한 것인지 확인하기 위해 응용 프로그램은 테넌트의 [OpenID Connect Discovery 문서](http://openid.net/specs/openid-connect-discovery-1_0.html) 또는 SAML/WS-Fed [페더레이션 메타데이터 문서](active-directory-federation-metadata.md)에 포함된 Azure AD가 노출한 공개 키를 사용하여 토큰의 서명을 유효성 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="06f36-114">보안을 위해 Azure AD의 서명 키는 주기적으로 롤링하고, 비상 시에는 곧바로 롤오버될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="06f36-115">빈도에 관계 없이 키 롤오버 이벤트를 처리하기 위해 Azure AD와 통합되는 모든 응용 프로그램을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="06f36-116">없는 경우 응용 프로그램은 토큰에서 서명을 확인하기 위해 만료된 키를 사용하려고 시도하며 서명 요청이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="06f36-117">OpenID Connect discovery 문서와 페더레이션 메타데이터 문서에는 사용 가능한 키가 항상 두 개 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="06f36-118">하나의 키가 곧 롤오버되고 다른 키가 대체되는 방식으로 문서에 지정된 키를 사용하도록 응용 프로그램이 준비되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="06f36-119">응용 프로그램이 영향을 받을지 여부와 그에 대한 대처 방안을 평가하는 방법</span><span class="sxs-lookup"><span data-stu-id="06f36-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="06f36-120">응용 프로그램이 키 롤오버를 처리하는 방식은 응용 프로그램 유형 또는 사용된 ID 프로토콜 및 라이브러리 버전과 같은 변수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="06f36-121">아래 섹션에서는 가장 일반적인 유형의 응용 프로그램이 키 롤오버의 영향을 받는지 여부와 자동 롤오버를 지원하거나 수동으로 키를 업데이트하도록 응용 프로그램을 업데이트하는 방법에 대한 지침을 제공하는지 여부를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="06f36-122">리소스에 액세스하는 네이티브 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="06f36-123">리소스에 액세스하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="06f36-124">리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="06f36-125">.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="06f36-126">.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="06f36-127">Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="06f36-128">리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="06f36-129">리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="06f36-130">리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API</span><span class="sxs-lookup"><span data-stu-id="06f36-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="06f36-131">리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="06f36-132">리소스를 보호하며 Visual Studio 2010, 2008 또는 WIF(Windows Identity Foundation)를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="06f36-133">다른 라이브러리를 사용하거나 지원되는 프로토콜을 수동으로 구현하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="06f36-134">이 설명서는 다음에 적용할 수 **없습니다** .</span><span class="sxs-lookup"><span data-stu-id="06f36-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="06f36-135">Azure AD 응용 프로그램 갤러리에서 추가된 응용 프로그램(사용자 지정 포함)에는 서명 키와 관련하여 별도 설명서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="06f36-136">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="06f36-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="06f36-137">응용 프로그램 프록시를 통해 게시된 온-프레미스 응용 프로그램은 서명 키에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="06f36-138"><a name="nativeclient"></a>리소스에 액세스하는 네이티브 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="06f36-139">리소스에만 액세스하는 응용 프로그램(즉,</span><span class="sxs-lookup"><span data-stu-id="06f36-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="06f36-140">Microsoft Graph, KeyVault, Outlook API 및 기타 Microsoft API)은 일반적으로 토큰만 가져와서 리소스 소유자에게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="06f36-141">리소스를 보호하지 못한다면 토큰을 검사하지 않으므로 제대로 서명되었는지 확인할 필요도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="06f36-142">데스크톱 또는 모바일의 네티이브 클라이언트 응용 프로그램이 이 범주에 해당하므로 롤오버의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="06f36-143"><a name="webclient"></a>리소스에 액세스하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="06f36-144">리소스에만 액세스하는 응용 프로그램(즉,</span><span class="sxs-lookup"><span data-stu-id="06f36-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="06f36-145">Microsoft Graph, KeyVault, Outlook API 및 기타 Microsoft API)은 일반적으로 토큰만 가져와서 리소스 소유자에게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="06f36-146">리소스를 보호하지 못한다면 토큰을 검사하지 않으므로 제대로 서명되었는지 확인할 필요도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="06f36-147">앱 전용 흐름을 사용하는 웹 응용 프로그램 및 웹 API(클라이언트 자격 증명/클라이언트 인증서)가 이 범주에 해당하므로 롤오버의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="06f36-148"><a name="appservices"></a>리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="06f36-149">Azure 앱 서비스의 인증/권한 부여(EasyAuth) 기능에는 이미 키 롤오버를 자동으로 처리하는 데 필요한 논리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="06f36-150"><a name="owin"></a>.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="06f36-151">응용 프로그램에서 .NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용 하는 경우, 자동으로 키 롤오버를 처리하는 데 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="06f36-152">응용 프로그램의 Startup.cs 또는 Startup.Auth.cs에서 다음 코드 조각을 찾아봄으로써 응용 프로그램에서 이들 미들웨어를 사용하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="06f36-153"><a name="owincore"></a>.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="06f36-154">응용 프로그램에서 .NET Core OWIN OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용 하는 경우, 자동으로 키 롤오버를 처리하는 데 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="06f36-155">응용 프로그램의 Startup.cs 또는 Startup.Auth.cs에서 다음 코드 조각을 찾아봄으로써 응용 프로그램에서 이들 미들웨어를 사용하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="06f36-156"><a name="passport"></a>Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="06f36-157">응용 프로그램에서 Node.js passport-ad module을 사용 하는 경우, 자동으로 키 롤오버를 처리하는 데 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="06f36-158">응용 프로그램의 app.js에서 다음 코드 조각을 찾아봄으로써 응용 프로그램 passport ad를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="06f36-159"><a name="vs2015"></a>리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="06f36-160">Visual Studio 2015 또는 Visual Studio 2017에서 웹 응용 프로그램 템플릿을 사용하여 응용 프로그램을 빌드했고 **인증 변경** 메뉴에서 **회사 및 학교 계정**을 선택한 경우 자동으로 키 롤오버를 처리하는 데 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="06f36-161">OWIN OpenID Connect 미들웨어에 포함된 이 논리는 OpenID Connect discovery 문서에서 키를 검색하고 캐시하며 주기적으로 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="06f36-162">인증을 솔루션에 수동으로 추가하면 응용 프로그램에 필요한 키 롤오버 논리가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="06f36-163">사용자가 직접 작성하거나 [웹 응용 프로그램/다른 라이브러리를 사용하거나 지원되는 프로토콜을 수동으로 구현하는 API](#other)의 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="06f36-164"><a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="06f36-165">Visual Studio 2013에서 웹 응용 프로그램 템플릿을 사용하여 응용 프로그램을 빌드했고 **인증 변경** 메뉴에서 **조직 계정**을 선택한 경우 자동으로 키 롤오버를 처리하는 데 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="06f36-166">이 논리는 조직의 고유 ID 및 서명 키 정보를 프로젝트와 연결된 두 데이터베이스 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="06f36-167">프로젝트의 Web.config 파일에서 데이터베이스에 대한 연결 문자열을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="06f36-168">인증을 솔루션에 수동으로 추가하면 응용 프로그램에 필요한 키 롤오버 논리가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="06f36-169">사용자가 직접 작성하거나 [웹 응용 프로그램/다른 라이브러리를 사용하거나 지원되는 프로토콜을 수동으로 구현하는 API](#other)의 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="06f36-170">다음 단계는 응용 프로그램에서 논리가 제대로 작동하는지 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="06f36-171">Visual Studio 2013에서 솔루션을 열고 오른쪽 창에서 **서버 탐색기** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="06f36-172">**데이터 연결**, **DefaultConnection**, **테이블**을 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="06f36-173">**IssuingAuthorityKeys** 테이블을 찾아 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="06f36-174">**IssuingAuthorityKeys** 테이블에는 키에 대한 지문 값에 해당하는 행이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="06f36-175">테이블의 모든 행을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="06f36-176">**테넌트** 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="06f36-177">**테넌트** 테이블에는 고유한 디렉터리 테넌트 식별자에 해당하는 행이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="06f36-178">테이블의 모든 행을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-178">Delete any rows in the table.</span></span> <span data-ttu-id="06f36-179">**테넌트** 테이블 및 **IssuingAuthorityKeys** 테이블 모두에서 행을 삭제하지 않으면 런타임에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="06f36-180">응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-180">Build and run the application.</span></span> <span data-ttu-id="06f36-181">계정에 로그인한 후에 응용 프로그램을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="06f36-182">**서버 탐색기**로 돌아가 **IssuingAuthorityKeys** 및 **테넌트** 테이블에서 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="06f36-183">페더레이션 메타데이터 문서의 적절한 정보로 자동으로 다시 채워진 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="06f36-184"><a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API</span><span class="sxs-lookup"><span data-stu-id="06f36-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="06f36-185">Visual Studio 2013에서 Web API 템플릿을 사용하여 Web API 응용 프로그램을 만들었고 **인증 변경** 메뉴에서 **조직 계정**을 선택한 경우 응용 프로그램에 필요한 논리가 이미 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="06f36-186">인증을 수동으로 구성한 경우 아래 지침을 따라 키 정보를 자동으로 업데이트하는 Web API를 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="06f36-187">다음 코드 조각은 페더레이션 메타데이터 문서에서 최신 키를 가져온 후 [JWT 토큰 처리기](https://msdn.microsoft.com/library/dn205065.aspx) 를 사용하여 토큰의 유효성을 검사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="06f36-188">이 코드 조각은 Azure AD에서 향후 토큰의 유효성을 검사하기 위해 키를 유지하는 데 키 위치에 관계 없이(데이터베이스, 구성 파일 또는 다른 곳) 고유의 캐싱 메커니즘을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="06f36-189"><a name="vs2012"></a>리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="06f36-190">Visual Studio 2012에서 응용 프로그램을 빌드한 경우 응용 프로그램을 구성하는 데 아마도 ID 및 액세스 도구를 사용한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="06f36-191">또한 [발급자 이름 레지스트리 유효성 검사(VINR)](https://msdn.microsoft.com/library/dn205067.aspx)를 사용할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="06f36-192">VINR은 발급된 토큰의 유효성을 검사하는 데 사용된 키와 신뢰할 수 있는 ID 공급자(Azure AD)에 대한 정보의 유지 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="06f36-193">또한 VINR을 통해 해당 디렉터리에 연결된 최신 페더레이션 메타데이터 문서를 다운로드하고 구성이 최신 문서와 함께 만료되었는지 확인하며 필요에 따라 새 키를 사용하도록 응용 프로그램을 업데이트하여 Web.config 파일에 저장된 키 정보를 자동으로 간편하게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="06f36-194">Microsoft에서 제공하는 코드 샘플 또는 연습 문서를 사용하여 응용 프로그램을 만든 경우 키 롤오버 논리가 프로젝트에 이미 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="06f36-195">아래 코드가 프로젝트에 이미 있는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="06f36-196">응용 프로그램에 이 논리가 아직 없는 경우 아래 단계에 따라 추가하고 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="06f36-197">**솔루션 탐색기**에서 참조를 해당 프로젝트에 대한 **System.IdentityModel** 어셈블리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="06f36-198">**Global.asax.cs** 파일을 열고 지시문을 사용하여 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="06f36-199">**Global.asax.cs** 파일에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="06f36-200">아래와 같이 **Global.asax.cs**의 **Application_Start()** 메서드에서 **RefreshValidationSettings()** 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="06f36-201">이러한 단계를 완료하면 응용 프로그램의 Web.config가 최신 키를 포함한 페더레이션 메타데이터 문서의 최신 정보로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="06f36-202">이 업데이트는 응용 프로그램 풀이 IIS에서 재활용될 때마다 발생하며 기본적으로 IIS는 29시간마다 응용 프로그램을 재활용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="06f36-203">아래 단계에 따라 키 롤오버 논리가 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="06f36-204">응용 프로그램이 위의 코드를 사용 중인지를 확인한 후 **Web.config** 파일을 열고 **<issuerNameRegistry>** 블록으로 이동하여 구체적으로 다음 몇 줄을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="06f36-205">**<add thumbprint=””>** 설정에서 모든 문자를 다른 것으로 바꿔서 지문 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="06f36-206">**Web.config** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="06f36-207">응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-207">Build the application, and then run it.</span></span> <span data-ttu-id="06f36-208">로그인 프로세스를 완료할 수 있으면 응용 프로그램은 디렉터리의 페더레이션 메타데이터 문서에서 필요한 정보를 다운로드하여 키를 성공적으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="06f36-209">로그인하는 데 문제가 있는 경우 [Azure AD를 사용하여 웹 응용 프로그램에 로그온 추가](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) 항목을 읽거나 [Azure Active Directory에 대한 다중 테넌트 클라우드 응용 프로그램](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b) 코드 샘플을 다운로드 및 검사하여 응용 프로그램의 변경 내용이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="06f36-210"><a name="vs2010"></a>리소스를 보호하며 Visual Studio 2008 또는 2010 및 .NET 3.5용 WIF(Windows Identity Foundation) v1.0을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="06f36-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="06f36-211">WIF v1.0에서 응용 프로그램을 빌드한 경우 새 키를 사용하도록 응용 프로그램의 구성을 자동으로 새로 고치는 데 제공된 메커니즘이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="06f36-212">*가장 쉬운 방법* WIF SDK에 포함된 FedUtil 도구를 사용합니다. 이 도구를 통해 최신 메타데이터 문서를 검색하고 구성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="06f36-213">응용 프로그램을 시스템 네임스페이스에 있는 최신 버전의 WIF를 포함하는 .NET 4.5로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="06f36-214">그런 다음 [발급자 이름 레지스트리 유효성 검사(VINR)](https://msdn.microsoft.com/library/dn205067.aspx) 를 사용하여 응용 프로그램 구성의 자동 업데이트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="06f36-215">이 지침 문서의 끝에 있는 지침에 따라 수동 롤오버를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="06f36-216">구성을 업데이트하기 위해 FedUtil을 사용하는 지침:</span><span class="sxs-lookup"><span data-stu-id="06f36-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="06f36-217">Visual Studio 2008 또는 2010의 개발 컴퓨터에 WIF v1.0 SDK가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="06f36-218">아직 설치되어 있지 않은 경우 [여기에서 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=4451) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="06f36-219">Visual Studio에서 솔루션을 열고 해당 프로젝트를 마우스 오른쪽 단추로 클릭하고 **페더레이션 메타데이터 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="06f36-220">이 옵션을 사용할 수 없는 경우 FedUtil 및/또는 WIF v1.0 SDK가 설치되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="06f36-221">프롬프트에서 **업데이트** 를 선택하여 페더레이션 메타데이터의 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="06f36-222">응용 프로그램이 호스팅되는 서버 환경에 대한 액세스 권한이 있는 경우 필요에 따라 FedUtil의 [자동 메타데이터 업데이트 스케줄러](https://msdn.microsoft.com/library/ee517272.aspx)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="06f36-223">**마침** 을 클릭하고 업데이트 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="06f36-224"><a name="other"></a>다른 라이브러리를 사용하거나 지원되는 프로토콜을 수동으로 구현하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="06f36-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="06f36-225">다른 라이브러리를 사용하거나 지원되는 프로토콜을 수동으로 구현하는 경우, 키가 OpenID Connect discovery 문서 또는 페더레이션 메타데이터 문서에서 검색되는지 확인하기 위해 라이브러리나 구현을 검토할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="06f36-226">이를 확인하는 하나의 방법은 OpenID discovery 문서 또는 페더레이션 메타데이터 문서에 대한 모든 호출 코드 또는 라이브러리 코드를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="06f36-227">키가 어딘가에 저장되거나 응용 프로그램에 하드 코딩되는 경우 이 지침 문서의 끝에 있는 지침에 따라 수동 롤오버를 수행하여 수동으로 키를 검색하고 적절하게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="06f36-228">**자동 롤오버를 지원하기 위해 응용 프로그램을 향상하는 것이 아주 좋습니다** .</span><span class="sxs-lookup"><span data-stu-id="06f36-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="06f36-229">응용 프로그램을 테스트하여 영향을 받을지 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="06f36-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="06f36-230">스크립트를 다운로드하고 [이 GitHub 리포지토리](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="06f36-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="06f36-231">응용 프로그램이 자동 롤오버를 지원하지 않는 경우 수동 롤오버를 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="06f36-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="06f36-232">응용 프로그램이 자동 롤오버를 지원하지 **않는** 경우 주기적으로 Azure AD의 서명 키를 모니터링하고 적절하게 수동 롤오버를 수행하는 프로세스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="06f36-233">[이 GitHub 리포지토리](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) 는 이 작업을 수행하는 방법에 대한 스크립트 및 지침을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="06f36-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

