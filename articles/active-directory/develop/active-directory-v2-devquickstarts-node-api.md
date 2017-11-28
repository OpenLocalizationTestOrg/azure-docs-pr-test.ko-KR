---
title: "Node.js를 사용 하 여 Azure Active Directory v2.0 웹 API aaaSecure | Microsoft Docs"
description: "Toobuild는 Node.js API와 회사 또는 학교 계정을 모두 개인 Microsoft 계정에서 토큰을 수락 하는 웹 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="02439-103">Node.js를 사용하여 웹 API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="02439-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="02439-104">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02439-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="02439-105">에 대해 알아보세요 hello v2.0 끝점 또는 hello v1.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="02439-106">Hello Azure Active Directory (Azure AD) v 2.0 끝점을 사용 하는 경우 사용할 수 있습니다 [OAuth 2.0](active-directory-v2-protocols.md) 액세스 토큰 tooprotect web API입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="02439-107">OAuth 2.0 액세스 토큰을 사용하여 개인 Microsoft 계정 및 작업 또는 학교 계정 모두를 가진 사용자는 웹 API에 안전하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="02439-108">*Passport* 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="02439-109">유연한 모듈식 Passport는 어떤 Express 기반 또는 restify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="02439-110">Passport에서는 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 또는 기타 옵션을 사용하여 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="02439-111">Microsoft는 Azure AD에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="02439-112">이 문서에서는 보여줍니다 tooinstall 모듈 hello 하 고 다음 hello Azure AD를 추가 하는 방법 `passport-azure-ad` 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="02439-113">다운로드</span><span class="sxs-lookup"><span data-stu-id="02439-113">Download</span></span>
<span data-ttu-id="02439-114">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="02439-115">수 toofollow hello 자습서 [hello 응용 프로그램의 구조를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="02439-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="02439-116">이 자습서의 hello 끝 완료 hello 응용 프로그램을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="02439-117">1: 앱 등록</span><span class="sxs-lookup"><span data-stu-id="02439-117">1: Register an app</span></span>
<span data-ttu-id="02439-118">새 앱 만들기 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 하거나 팔 로우 [자세한 단계는 이러한](active-directory-v2-app-registration.md) tooregister 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="02439-119">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-119">Make sure you:</span></span>

* <span data-ttu-id="02439-120">복사 hello **응용 프로그램 Id** tooyour 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="02439-121">이 자습서에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="02439-122">Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="02439-123">복사 hello **리디렉션 URI** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="02439-124">Hello URI의 기본값을 사용 해야 `urn:ietf:wg:oauth:2.0:oob`합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="02439-125">2: Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="02439-125">2: Install Node.js</span></span>
<span data-ttu-id="02439-126">이 자습서에 대 한 toouse hello 샘플에서 수행 해야 [Node.js 설치](http://nodejs.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="02439-127">3: MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="02439-127">3: Install MongoDB</span></span>
<span data-ttu-id="02439-128">이 샘플을 사용 하는 toosuccessfully 있으면 [MongoDB 설치](http://www.mongodb.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="02439-129">이 샘플에서 사용 하 여 MongoDB toomake 영구 REST API 서버 인스턴스에서.</span><span class="sxs-lookup"><span data-stu-id="02439-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="02439-130">이 문서에서는 hello 기본 설치 및 서버 끝점을 사용 하 여 MongoDB에 대 한 가정: mongodb://localhost 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="02439-131">4: 설치 hello restify web API의에서 모듈</span><span class="sxs-lookup"><span data-stu-id="02439-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="02439-132">Resitfy toobuild REST API 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="02439-133">Restify는 Express에서 파생된 작고 유연한 Node.js 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="02439-134">Restify 강력한 toobuild 연결 위에 REST Api를 사용할 수 있는 기능 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="02439-135">Restify 설치</span><span class="sxs-lookup"><span data-stu-id="02439-135">Install restify</span></span>
1.  <span data-ttu-id="02439-136">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="02439-137">경우 hello **azure ad** 디렉터리 존재 하지 않거나, 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="02439-138">Restify 설치:</span><span class="sxs-lookup"><span data-stu-id="02439-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="02439-139">hello이이 명령의 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="02439-140">오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="02439-140">Did you get an error?</span></span>
<span data-ttu-id="02439-141">Hello를 사용 하는 경우 일부 운영 체제에서 `npm` 명령,이 메시지가 표시 될 수 있습니다: `Error: EPERM, chmod '/usr/local/bin/..'`합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="02439-142">hello 오류 하면 관리자 권한으로 실행 중인 hello 계정 사용을 시도 하는 요청에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="02439-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="02439-143">이 경우 명령을 사용 하 여 hello `sudo` toorun `npm` 더 높은 권한 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="02439-144">관련 오류 어 tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="02439-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="02439-145">Restify를 설치할 때 이 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="02439-146">Restify DTrace를 사용 하 여 REST 호출 강력한 메커니즘 tootrace 했습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="02439-147">그러나 DTrace는 많은 운영 체제에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="02439-148">이 오류 메시지는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="02439-149">5: 웹 API에 Passport.js 설치</span><span class="sxs-lookup"><span data-stu-id="02439-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="02439-150">Hello 명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="02439-151">Passport.js 설치:</span><span class="sxs-lookup"><span data-stu-id="02439-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="02439-152">hello hello 명령의 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="02439-153">6: passport azure ad tooyour 웹 API에 추가</span><span class="sxs-lookup"><span data-stu-id="02439-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="02439-154">그런 다음 passport azure ad를 사용 하 여 hello OAuth 전략을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="02439-155">`passport-azuread`는 Azure AD를 Passport와 함께 연결하는 전략 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="02439-156">이 REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="02439-157">OAuth 2.0은 알려진 모든 토큰 유형을 발급할 수 있는 프레임워크를 제공하지만 일반적으로 특정 토큰 유형이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="02439-158">전달자 토큰은 자주 사용 되는 tooprotect 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="02439-159">전달자 토큰은 발급 가장 광범위 하 게 hello 유형의 OAuth 2.0에서 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="02439-160">많은 OAuth 2.0 구현 전달자 토큰 발급 토큰의 형식만 hello 있다고 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="02439-161">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-162">Hello Passport.js 설치 `passport-azure-ad` 모듈:</span><span class="sxs-lookup"><span data-stu-id="02439-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="02439-163">hello hello 명령의 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="02439-164">7: MongoDB 모듈 tooyour 웹 API에 추가</span><span class="sxs-lookup"><span data-stu-id="02439-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="02439-165">이 샘플에서는 데이터 저장소로 MongoDB를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="02439-166">설치 Mongoose 널리 사용 되는 플러그 인, toomanage 모델과 스키마:</span><span class="sxs-lookup"><span data-stu-id="02439-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="02439-167">MongoDB 라고도 함 MongoDB에 대 한 hello 데이터베이스 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="02439-168">8: 추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="02439-168">8: Install additional modules</span></span>
<span data-ttu-id="02439-169">Hello 남은 필요한 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="02439-170">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-171">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-171">Enter hello following commands.</span></span> <span data-ttu-id="02439-172">hello 명령을 hello node_modules 디렉터리 모듈에에서 다음을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="02439-173">9: 종속성에 대한 Server.js 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="02439-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="02439-174">Hello 대부분의 웹 API 서버에 대 한 hello 기능은 Server.js 파일을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="02439-175">대부분의 코드 toothis 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-175">Add most of your code toothis file.</span></span> <span data-ttu-id="02439-176">프로덕션 환경에 대 한 별도 경로 및 컨트롤러와 같은 hello 기능을 더 작은 파일로 리팩터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="02439-177">이 문서에서는 이 목적을 위해 Server.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="02439-178">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-179">선택한 편집기를 사용하여 Server.js 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02439-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="02439-180">다음 정보 toohello 파일 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="02439-181">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-181">Save hello file.</span></span> <span data-ttu-id="02439-182">Tooit를 즉시 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="02439-183">10: config 파일 toostore Azure AD 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="02439-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="02439-184">이 코드 파일에서 Azure AD 포털 tooPassport.js hello 구성 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="02439-185">Hello 웹 API toohello 포털 hello 문서의 hello 시작 부분에 추가 했을 때 이러한 구성 값을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="02439-186">Hello 코드를 복사한 후 hello 값이 매개이 변수 중에서 어떤 tooput을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="02439-187">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-188">편집기에서 Config.js 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02439-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="02439-189">Hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="02439-190">필요한 값</span><span class="sxs-lookup"><span data-stu-id="02439-190">Required values</span></span>

*   <span data-ttu-id="02439-191">**IdentityMetadata**: 여기에 `passport-azure-ad` hello IDP (id 공급자) 및 hello 키 toovalidate hello JSON 웹 토큰 (Jwt)에 대 한 구성 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="02439-192">Azure AD를 사용 하는 경우 원하지 않을 것 toochange이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="02439-193">**대상 그룹**: hello 포털에서 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="02439-194">키는 자주 롤링됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="02439-195">항상 hello "openid_keys" URL에서 끌어오도록 하 고 해당 hello 앱 hello 인터넷에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="02439-196">11: hello 구성 tooyour Server.js 파일 추가</span><span class="sxs-lookup"><span data-stu-id="02439-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="02439-197">응용 프로그램에 방금 만든 hello 구성 파일에서 tooread hello 값 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="02439-198">응용 프로그램에 필요한 리소스로 hello.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="02439-199">Hello 전역 변수 toothose Config.js에 있는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="02439-200">Hello 명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-201">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02439-201">In an editor, open Server.js.</span></span> <span data-ttu-id="02439-202">Hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="02439-203">새 섹션 tooServer.js를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="02439-204">12: Mongoose를 사용 하 여 hello MongoDB 모델 및 스키마 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="02439-205">다음으로 REST API 서비스에서 이러한 3개의 파일을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="02439-206">이 문서에서 사용 하 여 MongoDB toostore 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="02439-207">이 부분은 *4단계*에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="02439-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="02439-208">11 단계에서 만든 hello Config.js 파일에서 데이터베이스 라고 *tasklist \ / s*합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="02439-209">그건 mongoose_auth_local 연결 URL의 hello 끝에 사용할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="02439-210">이 데이터베이스 MongoDB에 미리 toocreate 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="02439-211">hello를 데이터베이스가 만들어집니다 hello 먼저 (hello 데이터베이스가 아직 없는 경우) 서버 응용 프로그램의 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="02439-212">MongoDB 데이터베이스 toouse 어떤 hello 서버에 지시 받고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="02439-213">다음으로, 해야 toowrite 몇 가지 추가 코드 toocreate hello 모델 및 스키마 서버의 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="02439-214">hello 모델</span><span class="sxs-lookup"><span data-stu-id="02439-214">hello model</span></span>
<span data-ttu-id="02439-215">hello 스키마 모델은 매우 기본적인입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-215">hello schema model is very basic.</span></span> <span data-ttu-id="02439-216">필요한 경우 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="02439-217">hello 스키마 모델에는 이러한 값은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="02439-218">**이름**.</span><span class="sxs-lookup"><span data-stu-id="02439-218">**NAME**.</span></span> <span data-ttu-id="02439-219">hello 사람 toohello 할당 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-219">hello person assigned toohello task.</span></span> <span data-ttu-id="02439-220">**문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-220">This is a **string** value.</span></span>
*   <span data-ttu-id="02439-221">**작업**.</span><span class="sxs-lookup"><span data-stu-id="02439-221">**TASK**.</span></span> <span data-ttu-id="02439-222">hello 작업의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-222">hello name of hello task.</span></span> <span data-ttu-id="02439-223">**문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-223">This is a **string** value.</span></span>
*   <span data-ttu-id="02439-224">**날짜**.</span><span class="sxs-lookup"><span data-stu-id="02439-224">**DATE**.</span></span> <span data-ttu-id="02439-225">hello 날짜 hello 작업으로 인 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-225">hello date that hello task is due.</span></span> <span data-ttu-id="02439-226">**datetime** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="02439-227">**완료됨**.</span><span class="sxs-lookup"><span data-stu-id="02439-227">**COMPLETED**.</span></span> <span data-ttu-id="02439-228">Hello 작업은 완료 되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="02439-228">Whether hello task is completed.</span></span> <span data-ttu-id="02439-229">**부울** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="02439-230">Hello 코드에서 hello 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="02439-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="02439-231">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-232">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02439-232">In your editor, open Server.js.</span></span> <span data-ttu-id="02439-233">Hello 구성 항목 아래에 다음 정보는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="02439-234">이 코드 toohello MongoDB 서버에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="02439-235">또한 스키마 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="02439-236">Hello 코드에서 모델을 만들 hello 스키마를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="02439-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="02439-237">Hello 코드 앞에, 아래 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="02439-238">먼저 hello 코드에서 알 수 있습니다, 스키마를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="02439-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="02439-239">다음으로 모델 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02439-239">Next, you create a model object.</span></span> <span data-ttu-id="02439-240">Hello 모델 개체 toostore hello 전체에서 데이터를 정의할 때 코드를 사용 하 여 **경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="02439-241">13: 작업 REST API 서버에 대한 경로 추가</span><span class="sxs-lookup"><span data-stu-id="02439-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="02439-242">와 데이터베이스 모델 toowork를가지고 사용할 REST API 서버에 대 한 hello 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="02439-243">Restify의 경로 정보</span><span class="sxs-lookup"><span data-stu-id="02439-243">About routes in restify</span></span>
<span data-ttu-id="02439-244">경로 restify 정확 하 게 hello 동일한 방식으로 사용 하는 경우 hello 빠른 스택 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="02439-245">Hello hello 클라이언트 응용 프로그램 toocall 예상 되는 URI를 사용 하 여 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="02439-246">일반적으로 경로는 별도 파일에 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="02439-247">이 자습서에서는 Server.js에 경로를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="02439-248">프로덕션 사용을 위해서는 자체 파일로 경로를 팩터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="02439-249">Restify 경로의 일반적인 패턴:</span><span class="sxs-lookup"><span data-stu-id="02439-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="02439-250">Hello 가장 기본적인 수준에서 hello 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="02439-251">Restify (및 Express) hello 기능 toodefine 응용 프로그램 유형 및 다른 끝점을 통해 복잡 한 라우팅 같은 더욱 심층적 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="02439-252">기본 경로 tooyour 서버 추가</span><span class="sxs-lookup"><span data-stu-id="02439-252">Add default routes tooyour server</span></span>
<span data-ttu-id="02439-253">Hello 기본 CRUD 경로 추가: **만들**, **검색**, **업데이트**, 및 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="02439-254">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="02439-255">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02439-255">In an editor, open Server.js.</span></span> <span data-ttu-id="02439-256">이전에 만든 데이터베이스 항목 hello 아래 hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="02439-257">오류 hello 경로 대 한 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-257">Add error handling for hello routes</span></span>
<span data-ttu-id="02439-258">발생 한 hello 문제에 대 한 백 toohello 클라이언트 통신할 수 있도록 몇 가지 오류 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="02439-259">이미 작성 하는 hello 코드 아래 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="02439-260">14: 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="02439-260">14: Create your server</span></span>
<span data-ttu-id="02439-261">마지막 일 toodo hello tooadd 서버 인스턴스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="02439-262">hello 서버 인스턴스는 호출을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="02439-263">Restify(및 Express)는 REST API 서버에 사용할 수 있는 심층적인 사용자 지정을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="02439-264">이 자습서에서는 hello 가장 기본 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="02439-265">15: 지금은 인증) (없이 hello 경로 추가</span><span class="sxs-lookup"><span data-stu-id="02439-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="02439-266">16: hello 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-266">16: Run hello server</span></span>
<span data-ttu-id="02439-267">좋습니다 tootest는 인증을 추가 하기 전에 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="02439-268">hello 가장 쉬운 방법은 tootest 서버 명령 프롬프트에서 curl을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="02439-269">toodo이 JSON으로 tooparse 출력을 사용할 수 있는 간단한 유틸리티를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="02439-270">예제 따르는 hello에 사용 하는 hello JSON 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="02439-271">이 전역으로 hello JSON 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="02439-272">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="02439-273">Hello 디렉터리도 변경**azure ad**, 다음 curl을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="02439-274">tooadd 작업:</span><span class="sxs-lookup"><span data-stu-id="02439-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="02439-275">hello 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="02439-276">Brandon에 대한 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="02439-277">이러한 모든 명령이 오류 없이 실행 하는 경우 준비 tooadd OAuth toohello REST API 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="02439-278">*이제 MongoDB를 사용하는 REST API 서버가 완료되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="02439-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="02439-279">17: 인증 tooyour REST API 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="02439-280">실행 중인 REST API를가지고 toouse를 설정 하 여 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02439-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="02439-281">명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="02439-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="02439-282">포함 된 hello oidcbearerstrategy passport azure ad 사용</span><span class="sxs-lookup"><span data-stu-id="02439-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="02439-283">지금까지 권한 부여 없이 일반적인 REST TODO 서버를 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="02439-284">이제 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-284">Now, add authentication.</span></span>

<span data-ttu-id="02439-285">먼저, toouse Passport 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="02439-286">이전 서버 구성 바로 뒤에 이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="02439-287">Api를 작성할 때 사용자 hello hello 토큰에서 고유한 데이터 toosomething 스푸핑 하지 하는 것이 좋습니다 tooalways 링크 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="02439-288">이 서버는 할 일 항목을 저장 하는 경우 hello 토큰 (token.sub 통해 라고 함)에 hello 사용자 구독 ID에 따라 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="02439-289">Hello token.sub을 hello "소유자" 필드에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="02439-290">이렇게 하면 해당 사용자만 hello 사용자 TODOs를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="02439-291">다른 사람이 입력 된 hello TODOs 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="02439-292">"소유자"에 대 한 hello API가 노출 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="02439-293">외부 사용자는 인증되는 경우에 다른 사용자의 TODO를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="02439-294">를 사용 하 여 함께 제공 된 hello Open ID 연결 전달자 전략 `passport-azure-ad`합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="02439-295">이전에 붙여 넣은 코드 뒤에 이 코드를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="02439-296">Passport는 모든 전략(Twitter, Facebook 등)에 유사한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="02439-297">모든 전략 기록기 toohello 패턴을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="02439-298">Hello 전략 전달는 `function()` 토큰을 사용 하 고 `done` 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="02439-299">hello 전략에는 모든 작업을 수행한 후 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02439-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="02439-300">Hello 사용자 및 보관 hello 토큰 저장에 대 한 tooask 다시 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02439-301">hello 앞의 코드는 tooyour 서버를 인증할 수 있는 모든 사용자 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="02439-302">이를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-302">This is known as auto-registration.</span></span> <span data-ttu-id="02439-303">프로덕션 서버에 원하지 toolet 모든 사용자 선택 하는 등록 프로세스를 통해 이동 하는 첫 번째 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="02439-304">일반적으로 소비자 앱에서 참조 하는 hello 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="02439-305">hello 응용 프로그램 수를 Facebook에 tooregister 허용 하지만 다음 묻는 tooenter 추가 정보.</span><span class="sxs-lookup"><span data-stu-id="02439-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="02439-306">명령줄 프로그램이 자습서를 사용 하지 않은 경우 반환 되는 hello 토큰 개체에서 hello 전자 메일을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="02439-307">그런 다음 hello 사용자 tooenter 추가 정보를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="02439-308">Hello 사용자를 추가 하는 테스트 서버 이기 때문에 직접 toohello 메모리 내 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="02439-309">끝점 보호</span><span class="sxs-lookup"><span data-stu-id="02439-309">Protect endpoints</span></span>
<span data-ttu-id="02439-310">Hello를 지정 하 여 끝점 보호 **passport.authenticate()** toouse 원하는 hello 프로토콜을 사용 하 여 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="02439-311">고급 옵션에 대한 서버 코드에서 사용자의 경로를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="02439-312">18: 서버 응용 프로그램 다시 실행</span><span class="sxs-lookup"><span data-stu-id="02439-312">18: Run your server application again</span></span>
<span data-ttu-id="02439-313">끝점에 대 한 OAuth 2.0 보호를 포함 하는 경우 사용 하 여 curl toosee 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="02439-314">이 끝점에 대해 클라이언트 SDK 중 하나를 실행하기 전에 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="02439-315">반환 된 hello 헤더 알려 주어 야 인증 제대로 작동 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="02439-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="02439-316">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="02439-317">Toohello 변경 **azure ad** 디렉터리 및 사용 하 여 curl:</span><span class="sxs-lookup"><span data-stu-id="02439-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="02439-318">기본 POST를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="02439-319">401 응답 hello Passport 계층 tooredirect 시도 나타냅니다 toohello 끝점의 경우이 수행할 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="02439-320">*이제 OAuth 2.0을 사용하는 REST API 서비스가 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="02439-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="02439-321">OAuth 2.0 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="02439-322">이 위해 추가 자습서 tooreview를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02439-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02439-323">Next steps</span></span>
<span data-ttu-id="02439-324">완료 하는 hello 예제 구성 값) (없이 제공 됩니다 참조용으로 [.zip 파일](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="02439-325">GitHub에서 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="02439-326">이제 toomore 고급 항목에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="02439-327">Tootry 경우가 [hello v2.0 끝점을 사용 하는 Node.js 웹 응용 프로그램 보안](active-directory-v2-devquickstarts-node-web.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="02439-328">다음은 몇 가지 추가 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="02439-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="02439-329">Azure AD v2.0 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="02439-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="02439-330">Stack Overflow "azure-active-directory" 태그</span><span class="sxs-lookup"><span data-stu-id="02439-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="02439-331">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="02439-331">Get security updates for our products</span></span>
<span data-ttu-id="02439-332">Toosign을 보안 사고 발생할 때 알림 toobe 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02439-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="02439-333">Hello에 [Microsoft 기술 보안 알림](https://technet.microsoft.com/security/dd252948) 페이지, tooSecurity 권고 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="02439-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

