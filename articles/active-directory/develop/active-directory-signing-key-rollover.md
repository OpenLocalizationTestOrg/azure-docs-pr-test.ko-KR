---
title: "Azure AD에서 키 롤오버 aaaSigning | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에 대 한 키 롤오버에 대 한 유용한 정보를 서명 하는 hello 설명"
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
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="9b78e-103">Azure Active Directory에서 서명 키 롤오버</span><span class="sxs-lookup"><span data-stu-id="9b78e-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="9b78e-104">이 항목에서는 Azure Active Directory (Azure AD) toosign 보안 토큰에 사용 되는 공개 키를 hello에 대 한 tooknow 필요한 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="9b78e-105">것이 중요 한 toonote는 주기적으로 및를 긴급 상황에서는 이러한 키 롤오버를 통해 즉시 롤백할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9b78e-106">Azure AD를 사용 하는 모든 응용 프로그램 수 tooprogrammatically 핸들 hello 키 롤오버 프로세스 하거나 정기적으로 수동 롤오버 프로세스를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="9b78e-107">Hello 키가 작동 방식을 tooassess hello hello 롤오버 tooyour 응용 프로그램에 미치는 방식과 toounderstand 읽고 tooupdate 응용 프로그램, 필요한 경우 정기적으로 수동 롤오버 프로세스 toohandle 키 롤오버를 설정할 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="9b78e-108">Azure AD의 서명 키 개요</span><span class="sxs-lookup"><span data-stu-id="9b78e-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="9b78e-109">Azure AD는 업계 표준 tooestablish 트러스트 자체와 hello 사이 작성 된 공개 키 암호화를 사용을 사용 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="9b78e-110">실질적으로 보안 그룹은 다음 방식으로 hello: Azure AD는 공개 및 개인 키 쌍으로 구성 된 서명 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="9b78e-111">사용자 인증을 위해 Azure AD를 사용 하는 tooan 응용 프로그램에 로그인 하면 Azure AD는 hello 사용자에 대 한 정보를 포함 하는 보안 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="9b78e-112">이 토큰은 응용 프로그램 백 toohello 전송 하기 전에 해당 개인 키를 사용 하 여 Azure AD에서 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="9b78e-113">토큰 hello tooverify가 유효 하 고 실제로 Azure AD에서 공개한, hello 응용 프로그램 hello hello 테 넌 트에 포함 된 Azure AD에 의해 노출 되는 공개 키를 사용 하 여 hello 토큰 서명의 유효성을 검사 해야 [검색 문서 OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) 또는 SAML/Ws-fed [페더레이션 메타 데이터 문서](active-directory-federation-metadata.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="9b78e-114">보안을 위해 Azure AD의 서명 키 롤 주기적으로 고, 비상 시 hello 경우에서 수 롤오버 즉시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9b78e-115">Azure AD와 통합 되어 있는 모든 응용 프로그램 키 롤오버 이벤트 발생할 수 있는 빈도 관계 없이 toohandle를 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="9b78e-116">그렇지 않은 경우 응용 프로그램 토큰에는 만료 된 키 tooverify hello 서명 toouse 시도 hello 로그인 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="9b78e-117">항상 둘 이상의 유효한 키가 hello OpenID Connect 검색 문서 및 hello 페더레이션 메타 데이터 문서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="9b78e-118">응용 프로그램을 준비 해야 toouse hello 키에 지정 된 hello 문서 키가 두 개를 곧 롤오버 될 수 있으므로 다른를 대체할 하 고 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="9b78e-119">어떻게 응용 프로그램이 영향을 받을 경우 tooassess 및 항목에 대 한 어떤 toodo</span><span class="sxs-lookup"><span data-stu-id="9b78e-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="9b78e-120">응용 프로그램에서 키 롤오버를 처리 하는 방법에 따라 다름 hello 유형의 응용 프로그램이 나 어떤 identity 프로토콜 및 라이브러리를 사용 하는 등의 변수</span><span class="sxs-lookup"><span data-stu-id="9b78e-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="9b78e-121">아래 섹션에서는 hello hello 가장 일반적인 유형의 응용 프로그램 hello 키 롤오버의 영향을 받는 방법을 tooupdate 응용 프로그램 toosupport 자동 롤오버 hello 또는 hello 키를 수동으로 업데이트 한 지침을 제공 하는지 여부를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="9b78e-122">리소스에 액세스하는 네이티브 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="9b78e-123">리소스에 액세스하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="9b78e-124">리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="9b78e-125">.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="9b78e-126">.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="9b78e-127">Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="9b78e-128">리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="9b78e-129">리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="9b78e-130">리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API</span><span class="sxs-lookup"><span data-stu-id="9b78e-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="9b78e-131">리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="9b78e-132">리소스를 보호하며 Visual Studio 2010, 2008 또는 WIF(Windows Identity Foundation)를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="9b78e-133">웹 응용 프로그램/리소스를 보호 하는 Api를 사용 하 여 다른 라이브러리 또는 수동으로 구현 하는 hello의 지원 되는 프로토콜</span><span class="sxs-lookup"><span data-stu-id="9b78e-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="9b78e-134">이 설명서는 다음에 적용할 수 **없습니다** .</span><span class="sxs-lookup"><span data-stu-id="9b78e-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="9b78e-135">(사용자 정의 포함)는 Azure AD 응용 프로그램 갤러리에서 추가 하는 응용 프로그램에 대 한 예정 toosigning 키를 가진 별도 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="9b78e-136">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9b78e-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="9b78e-137">온-프레미스 응용 프로그램 프록시를 통해 게시 된 응용 프로그램 서명 키에 대 한 tooworry 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="9b78e-138"><a name="nativeclient"></a>리소스에 액세스하는 네이티브 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="9b78e-139">리소스에만 액세스하는 응용 프로그램(즉,</span><span class="sxs-lookup"><span data-stu-id="9b78e-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9b78e-140">Microsoft Graph, KeyVault, Outlook API 및 다른 Microsoft Api) 일반적으로 토큰을 가져올 및만 toohello 리소스 소유자를 따라 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="9b78e-141">모든 리소스를 보호 하지 않습니다, 있다고 가정 hello 토큰을 검사 하지 않는 하며 따라서 tooensure 올바르게 서명은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="9b78e-142">네이티브 클라이언트 응용 프로그램 데스크톱 또는 모바일,이 범주에 속하는 하 고 따라서 영향을 받지 않습니다 hello 롤오버 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="9b78e-143"><a name="webclient"></a>리소스에 액세스하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="9b78e-144">리소스에만 액세스하는 응용 프로그램(즉,</span><span class="sxs-lookup"><span data-stu-id="9b78e-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9b78e-145">Microsoft Graph, KeyVault, Outlook API 및 다른 Microsoft Api) 일반적으로 토큰을 가져올 및만 toohello 리소스 소유자를 따라 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="9b78e-146">모든 리소스를 보호 하지 않습니다, 있다고 가정 hello 토큰을 검사 하지 않는 하며 따라서 tooensure 올바르게 서명은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="9b78e-147">웹 응용 프로그램 및 웹 응용 프로그램 전용 흐름 hello를 사용 하는 Api (클라이언트 자격 증명 / 클라이언트 인증서)이이 범주에 해당 하 고 따라서 영향을 받지 않습니다 hello 롤오버 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="9b78e-148"><a name="appservices"></a>리소스를 보호하고 Azure 앱 서비스를 사용하여 구축된 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="9b78e-149">Azure 앱 서비스의 인증 / 권한 부여 (EasyAuth) 기능에 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="9b78e-150"><a name="owin"></a>.NET OWIN OpenID Connect, WS-Fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="9b78e-151">응용 프로그램에서.NET OWIN OpenID Connect, Ws-fed 또는 WindowsAzureActiveDirectoryBearerAuthentication 미들웨어 hello를 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9b78e-152">응용 프로그램이 응용 프로그램의 Startup.cs 또는 Startup.Auth.cs 코드 조각은 다음 hello에 대 한 검색 하 여 이러한 항목 중 하나를 사용 중인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="9b78e-153"><a name="owincore"></a>.NET Core OpenID Connect 또는 JwtBearerAuthentication 미들웨어를 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="9b78e-154">응용 프로그램은.NET Core OWIN OpenID Connect hello 또는 JwtBearerAuthentication 미들웨어를 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9b78e-155">응용 프로그램이 응용 프로그램의 Startup.cs 또는 Startup.Auth.cs 코드 조각은 다음 hello에 대 한 검색 하 여 이러한 항목 중 하나를 사용 중인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="9b78e-156"><a name="passport"></a>Node.js passport-azure-ad 모듈을 사용하여 리소스를 보호하는 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="9b78e-157">응용 프로그램 hello Node.js passport ad 모듈을 사용 하는 경우 이미 키 롤오버를 toohandle hello 필수 논리가 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9b78e-158">되는지 확인할 수 있습니다 다음 응용 프로그램의 app.js의 조각 hello에 대 한 검색 하 여 응용 프로그램 passport ad 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="9b78e-159"><a name="vs2015"></a>리소스를 보호하며 Visual Studio 2015 또는 Visual Studio 2017을 사용하여 만든 웹 응용 프로그램/API</span><span class="sxs-lookup"><span data-stu-id="9b78e-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="9b78e-160">Visual Studio 2015 또는 Visual Studio 2017에서 웹 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 빌드한 경우 선택한 **작업 및 학교 계정** hello에서 **인증 변경** 메뉴 이미 hello 필수 논리가 toohandle 키 롤오버를 자동으로 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="9b78e-161">Hello OpenID Connect OWIN 미들웨어에 포함 된이 논리를 검색 및 hello OpenID Connect 검색 문서에서 hello 키를 캐시 하 고 주기적으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="9b78e-162">인증 tooyour 솔루션을 수동으로 추가 하는 경우 응용 프로그램에서는 hello 필수 키 롤오버 논리가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="9b78e-163">Toowrite 필요 합니다 것의 단계를 직접 또는 따라 hello [웹 응용 프로그램 / Api 수동으로 hello 중 하나를 구현 하거나 다른 라이브러리를 사용 하 여 프로토콜을 지원 합니다.](#other)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="9b78e-164"><a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9b78e-165">Visual Studio 2013에서 웹 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 빌드한 경우 선택한 **조직 계정** hello에서 **인증 변경** 메뉴 이미 hello 필요 키 롤오버를 자동으로 논리 toohandle 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="9b78e-166">이 논리는 조직의 고유 식별자 및 hello 프로젝트와 관련 된 두 개의 데이터베이스 테이블에 키 정보를 서명 하는 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="9b78e-167">Hello 프로젝트의 Web.config 파일에 hello 데이터베이스에 대 한 hello 연결 문자열을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="9b78e-168">인증 tooyour 솔루션을 수동으로 추가 하는 경우 응용 프로그램에서는 hello 필수 키 롤오버 논리가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="9b78e-169">Toowrite 필요 합니다 것의 단계를 직접 또는 따라 hello [웹 응용 프로그램 / Api 수동으로 hello 중 하나를 구현 하거나 다른 라이브러리를 사용 하 여 프로토콜을 지원 합니다.](#other)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="9b78e-170">단계를 수행 하는 hello hello 논리가 응용 프로그램에서 제대로 작동 하는지 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="9b78e-171">Visual Studio 2013에서 hello 솔루션을 열고 hello에 클릭 **서버 탐색기** hello 오른쪽 창에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="9b78e-172">**데이터 연결**, **DefaultConnection**, **테이블**을 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="9b78e-173">Hello 찾을 **IssuingAuthorityKeys** 테이블을 마우스 오른쪽 단추로 클릭 하 고 클릭 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="9b78e-174">Hello에 **IssuingAuthorityKeys** 테이블, hello 키에 대 한 toohello 지문 값을 해당 하는 하나 이상의 행이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="9b78e-175">Hello 테이블의 모든 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="9b78e-176">마우스 오른쪽 단추로 클릭 hello **테 넌 트** 테이블을 마우스 클릭 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="9b78e-177">Hello에 **테 넌 트** 테이블, 해당 tooa 고유한 디렉터리 테 넌 트 식별자는 하나 이상의 행이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="9b78e-178">Hello 테이블의 모든 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-178">Delete any rows in hello table.</span></span> <span data-ttu-id="9b78e-179">두 hello의 hello 행을 삭제 하지 않으면 **테 넌 트** 테이블 및 **IssuingAuthorityKeys** 테이블을 런타임 시 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="9b78e-180">빌드하고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-180">Build and run hello application.</span></span> <span data-ttu-id="9b78e-181">Tooyour 계정에 로그인 한 후에 hello 응용 프로그램을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="9b78e-182">Toohello 반환 **서버 탐색기** hello에 hello 값을 살펴보고 및 **IssuingAuthorityKeys** 및 **테 넌 트** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="9b78e-183">이러한가 되어 자동으로 다시 채워집니다 hello hello 페더레이션 메타 데이터 문서에서 적절 한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="9b78e-184"><a name="vs2013"></a>리소스를 보호하며 Visual Studio 2013을 사용하여 만든 웹 API</span><span class="sxs-lookup"><span data-stu-id="9b78e-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9b78e-185">Hello Web API 템플릿을 사용 하 여 Visual Studio 2013에서 web API 응용 프로그램을 만든 경우 다음 선택한 **조직 계정** hello에서 **인증 변경** 메뉴 하면 이미 있는 hello 응용 프로그램에서 필수 논리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="9b78e-186">인증을 수동으로 구성한 경우 아래 지침을 hello toolearn 어떻게 tooconfigure 웹 API tooautomatically 키 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="9b78e-187">hello 다음 코드 조각은 방법을 보여 주는 tooget hello 페더레이션 메타 데이터 문서에서 최신 키 hello hello를 사용 하 여 [JWT 토큰 처리기](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="9b78e-188">hello 코드 조각에서는 데이터베이스, 구성 파일 또는 다른 위치에서 든 관계 없이 Azure AD의 자체 캐싱 메커니즘 이후 지속 hello 키 toovalidate에 대 한 토큰을 사용 하 여 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
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

### <span data-ttu-id="9b78e-189"><a name="vs2012"></a>리소스를 보호하며 Visual Studio 2012를 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="9b78e-190">Visual Studio 2012에서 응용 프로그램을 빌드한 경우 아마도 사용한 Identity hello 및 액세스 도구 tooconfigure 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="9b78e-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="9b78e-191">Hello를 사용 하는 것 역시 [유효성 검사 발급자 이름 레지스트리 VINR ()](https://msdn.microsoft.com/library/dn205067.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="9b78e-192">hello VINR은 신뢰할 수 있는 id 공급자 (Azure AD)에 대 한 정보를 유지 관리 하 고 해당에서 발급 한 toovalidate 토큰을 사용 하는 hello 키.</span><span class="sxs-lookup"><span data-stu-id="9b78e-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="9b78e-193">hello VINR을 사용 하면 쉽게 tooautomatically 업데이트 hello 키 정보 hello 최신 페더레이션 메타 데이터와 관련 된 문서 검사 hello 구성이 최신 hello로 만료 된 경우 디렉터리에 다운로드 하 여 Web.config 파일에 저장 합니다. 문서 및 hello 응용 프로그램 toouse hello 새 키 업데이트 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="9b78e-194">Hello 코드 샘플 또는 연습 문서 Microsoft에서 제공 하는 중 하나를 사용 하 여 응용 프로그램을 만든 경우 hello 키 롤오버 논리가 이미 프로젝트에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="9b78e-195">아래 hello 코드 프로젝트에 이미 존재 한다는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="9b78e-196">응용 프로그램에 아직 없는 경우이 논리를 하 고 올바르게 작동 tooverify tooadd 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="9b78e-197">**솔루션 탐색기**, 참조 toohello 추가 **System.IdentityModel** hello 적절 한 프로젝트에 대 한 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="9b78e-198">열기 hello **Global.asax.cs** 파일을 hello 다음 추가 지시문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9b78e-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="9b78e-199">다음 메서드 toohello hello 추가 **Global.asax.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="9b78e-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="9b78e-200">Hello 호출 **refreshvalidationsettings ()** hello에 대 한 메서드 **application_start ()** 메서드에서 **Global.asax.cs** 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="9b78e-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="9b78e-201">다음이 단계를 따른 후 응용 프로그램의 Web.config hello hello 최신 키를 포함 하 여 hello 페더레이션 메타 데이터 문서에서 최신 정보로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="9b78e-202">이 업데이트는 IIS;에서 응용 프로그램 풀 재활용 될 때마다 발생 합니다. 기본적으로 29 시간 마다 IIS toorecycle 응용 프로그램 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="9b78e-203">Hello 키 롤오버 논리가 작동 tooverify 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="9b78e-204">응용 프로그램 열기 hello 위의 hello 코드를 사용 하 고 있는지 확인 한 후 **Web.config** toohello 이동한 다음 파일  **<issuerNameRegistry>**  블록에서 구체적으로 다음 몇 줄만 작성 hello:</span><span class="sxs-lookup"><span data-stu-id="9b78e-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="9b78e-205">Hello에  **<add thumbprint=””>**  설정, 다른 모든 문자를 대체 하 여 hello 지문 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="9b78e-206">Hello 저장 **Web.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="9b78e-207">Hello 응용 프로그램을 빌드하고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-207">Build hello application, and then run it.</span></span> <span data-ttu-id="9b78e-208">Hello 로그인 프로세스를 완료할 수 응용 프로그램 디렉터리의 페더레이션 메타 데이터 문서에서 hello 필요한 정보를 다운로드 하 여 hello 키를 정상적으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="9b78e-209">로그인 하는 데 문제가 있는 경우 hello를 참조 하 여 응용 프로그램의 hello 변경 올바른지 확인 [추가 로그온 tooYour 웹 응용 프로그램 사용 하 여 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) 항목 또는 다운로드 한 후 조사 아래의 코드 예제는 hello: [ Azure Active Directory 용 다중 테 넌 트 클라우드 응용 프로그램](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="9b78e-210"><a name="vs2010"></a>리소스를 보호하며 Visual Studio 2008 또는 2010 및 .NET 3.5용 WIF(Windows Identity Foundation) v1.0을 사용하여 만든 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9b78e-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="9b78e-211">WIF v 1.0에서 응용 프로그램을 작성 하는 경우 디자인 하는 메커니즘이 제공된 tooautomatically 창 응용 프로그램의 구성 toouse 새 키.</span><span class="sxs-lookup"><span data-stu-id="9b78e-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="9b78e-212">*가장 쉬운 방법은* hello hello 최신 메타 데이터 문서를 검색 하 고 구성을 업데이트할 수 있는 WIF SDK에에서 포함 된 hello FedUtil 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="9b78e-213">Hello hello System 네임 스페이스에는 WIF의 최신 버전을 포함 하 여 응용 프로그램 too.NET 4.5를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="9b78e-214">Hello를 사용 하 여 있습니다 [유효성 검사 발급자 이름 레지스트리 VINR ()](https://msdn.microsoft.com/library/dn205067.aspx) hello 응용 프로그램의 구성 tooperform 자동 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="9b78e-215">이 지침 문서 hello 끝나기 전에 hello 지침에 따라 수동 롤오버를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="9b78e-216">Toouse hello FedUtil tooupdate 구성 지침:</span><span class="sxs-lookup"><span data-stu-id="9b78e-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="9b78e-217">Hello WIF v1.0 SDK가 Visual Studio 2008 또는 2010 용 개발 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="9b78e-218">아직 설치되어 있지 않은 경우 [여기에서 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=4451) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="9b78e-219">Visual Studio에서 hello 솔루션을 열고 다음 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 및 선택 **페더레이션 메타 데이터 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="9b78e-220">이 옵션을 사용할 수 없는 경우 FedUtil 및/또는 hello WIF v1.0 SDK 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="9b78e-221">Hello 프롬프트에서 선택 **업데이트** toobegin 페더레이션 메타 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="9b78e-222">Hello 응용 프로그램이 호스팅된 곳 액세스 toohello 서버 환경에 있으면 FedUtil의 필요에 따라 사용할 수 있습니다 [자동 메타 데이터 업데이트 스케줄러](https://msdn.microsoft.com/library/ee517272.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="9b78e-223">클릭 **마침** toocomplete hello 업데이트 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="9b78e-224"><a name="other"></a>웹 응용 프로그램/리소스를 보호 하는 Api를 사용 하 여 다른 라이브러리 또는 수동으로 구현 하는 hello의 지원 되는 프로토콜</span><span class="sxs-lookup"><span data-stu-id="9b78e-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="9b78e-225">Tooreview hello 라이브러리 해야 또는 hello 또는 hello OpenID Connect 검색 문서에서 키 hello 프로그램 구현 tooensure를 검색 하는 일부 다른 라이브러리를 사용 하는 하거나 수동으로 hello 지원 프로토콜의 구현 된 경우 페더레이션 메타 데이터 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="9b78e-226">이 한 가지 방법은 toocheck toodo tooeither hello OpenID 검색 문서 또는 hello 페더레이션 메타 데이터 문서는 모든 호출에 대 한 코드나 hello 라이브러리 코드의 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="9b78e-227">Hello 키와 업데이트를 적절 하 게 하 여 수행할 것 hello 지침 문서가이 끝나기 전에 hello 지침에 따라 수동 롤오버를 검색할 어딘가에 저장 되는 키 또는 하드 코딩 된 응용 프로그램을 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="9b78e-228">**좋습니다 응용 프로그램 toosupport 자동 롤오버를 향상 시키는** hello를 사용 하 여 Azure AD 롤오버 운율 늘어나거나가이 문서 tooavoid 이후 중단 오버 헤드의 개요에 도달한는 응급 대역의 롤오버입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="9b78e-229">어떻게 tootest 프로그램 응용 프로그램 toodetermine 영향을 받게 됩니다 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9b78e-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="9b78e-230">응용 프로그램 hello 스크립트를 다운로드 하 고 hello 지침에 자동 키 롤오버를 지원 하는지 여부를 확인할 수 있습니다 [이 GitHub 리포지토리 합니다.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="9b78e-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="9b78e-231">어떻게 응용 프로그램 자동 롤오버를 지원 하지 않는 경우 수동 롤오버 tooperform</span><span class="sxs-lookup"><span data-stu-id="9b78e-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="9b78e-232">응용 프로그램은 경우 **하지** 자동 롤오버 지원, 그에 따라 tooestablish 프로세스를 주기적으로 모니터 Azure AD의 서명 키를 수동 롤오버를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="9b78e-233">[이 GitHub 리포지토리](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) 스크립트 및 방법에 대 한 지침이 포함 되어 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78e-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

