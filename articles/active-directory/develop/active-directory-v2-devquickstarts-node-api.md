---
title: "Node.js를 사용하여 Azure Active Directory v2.0 웹 API 보안 유지 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정 둘 다의 토큰을 허용하는 Node.js 웹 API를 빌드하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="7b4ec-103">Node.js를 사용하여 웹 API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="7b4ec-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="7b4ec-104">일부 Azure Active Directory 시나리오 및 기능은 v2.0 끝점에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="7b4ec-105">v2.0 끝점을 사용해야 하는지 v1.0 끝점을 사용해야 하는지를 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="7b4ec-106">Azure AD(Azure Active Directory) v2.0 끝점을 사용하는 경우 [OAuth 2.0](active-directory-v2-protocols.md) 액세스 토큰을 사용하여 웹 API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="7b4ec-107">OAuth 2.0 액세스 토큰을 사용하여 개인 Microsoft 계정 및 작업 또는 학교 계정 모두를 가진 사용자는 웹 API에 안전하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="7b4ec-108">*Passport* 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="7b4ec-109">유연한 모듈식 Passport는 어떤 Express 기반 또는 restify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="7b4ec-110">Passport에서는 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 또는 기타 옵션을 사용하여 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="7b4ec-111">Microsoft는 Azure AD에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="7b4ec-112">이 문서에서는 모듈을 설치한 다음 Azure AD `passport-azure-ad` 플러그 인을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="7b4ec-113">다운로드</span><span class="sxs-lookup"><span data-stu-id="7b4ec-113">Download</span></span>
<span data-ttu-id="7b4ec-114">이 자습서에 대한 코드는 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="7b4ec-115">자습서에 따라 [.zip 파일로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip)하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="7b4ec-116">또한 이 자습서의 끝 부분에서는 완성된 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="7b4ec-117">1: 앱 등록</span><span class="sxs-lookup"><span data-stu-id="7b4ec-117">1: Register an app</span></span>
<span data-ttu-id="7b4ec-118">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 [이러한 세부 단계](active-directory-v2-app-registration.md)에 따라 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="7b4ec-119">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-119">Make sure you:</span></span>

* <span data-ttu-id="7b4ec-120">앱에 할당된 **응용 프로그램 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="7b4ec-121">이 자습서에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="7b4ec-122">앱용 **Mobile** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="7b4ec-123">포털에서 **리디렉션 URI** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="7b4ec-124">`urn:ietf:wg:oauth:2.0:oob`의 기본 URI 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="7b4ec-125">2: Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-125">2: Install Node.js</span></span>
<span data-ttu-id="7b4ec-126">이 자습서에 샘플을 사용하려면 [Node.js를 설치](http://nodejs.org)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="7b4ec-127">3: MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-127">3: Install MongoDB</span></span>
<span data-ttu-id="7b4ec-128">이 샘플을 성공적으로 사용하려면 [MongoDB를 설치](http://www.mongodb.org)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="7b4ec-129">이 샘플에서는 MongoDB를 사용하여 REST API가 서버 인스턴스 간에 지속되도록 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="7b4ec-130">이 문서에서는 MongoDB에 대한 기본 설치 및 서버 끝점을 사용한다고 가정합니다(mongodb://localhost).</span><span class="sxs-lookup"><span data-stu-id="7b4ec-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="7b4ec-131">4: 웹 API에 Restify 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="7b4ec-132">Resitfy를 사용하여 REST API를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="7b4ec-133">Restify는 Express에서 파생된 작고 유연한 Node.js 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="7b4ec-134">Restify에는 Connect 위에 REST API를 작성하는 데 사용할 수 있는 강력한 기능 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="7b4ec-135">Restify 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-135">Install restify</span></span>
1.  <span data-ttu-id="7b4ec-136">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="7b4ec-137">**azuread** 디렉터리가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="7b4ec-138">Restify 설치:</span><span class="sxs-lookup"><span data-stu-id="7b4ec-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="7b4ec-139">이 명령의 출력은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="7b4ec-140">오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="7b4ec-140">Did you get an error?</span></span>
<span data-ttu-id="7b4ec-141">일부 운영 체제에서 `npm` 명령을 사용하는 경우 이 메시지가 나타날 수 있습니다. `Error: EPERM, chmod '/usr/local/bin/..'`</span><span class="sxs-lookup"><span data-stu-id="7b4ec-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="7b4ec-142">오류 뒤에 관리자 계정으로 실행하라는 요청이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="7b4ec-143">이 문제가 발생하면 `sudo` 명령을 사용하여 더 높은 권한 수준으로 `npm`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="7b4ec-144">DTrace 관련 오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="7b4ec-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="7b4ec-145">Restify를 설치할 때 이 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="7b4ec-146">Restify는 DTrace를 사용하여 REST 호출을 추적하는 강력한 메커니즘을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="7b4ec-147">그러나 DTrace는 많은 운영 체제에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="7b4ec-148">이 오류 메시지는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="7b4ec-149">5: 웹 API에 Passport.js 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="7b4ec-150">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="7b4ec-151">Passport.js 설치:</span><span class="sxs-lookup"><span data-stu-id="7b4ec-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="7b4ec-152">명령의 출력은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="7b4ec-153">6: 웹 API에 passport-azure-ad 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="7b4ec-154">다음으로 passport-azuread를 사용하여 OAuth 전략을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="7b4ec-155">`passport-azuread`는 Azure AD를 Passport와 함께 연결하는 전략 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="7b4ec-156">이 REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7b4ec-157">OAuth 2.0은 알려진 모든 토큰 유형을 발급할 수 있는 프레임워크를 제공하지만 일반적으로 특정 토큰 유형이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="7b4ec-158">전달자 토큰은 끝점을 보호하는 데 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="7b4ec-159">전달자 토큰은 OAuth 2.0에서 가장 널리 발급되는 토큰 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="7b4ec-160">많은 OAuth 2.0 구현에서 발급되는 유일한 토큰 유형이 전달자 토큰이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="7b4ec-161">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-162">Passport.js `passport-azure-ad` 모듈 설치:</span><span class="sxs-lookup"><span data-stu-id="7b4ec-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="7b4ec-163">명령의 출력은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="7b4ec-164">7: 웹 API에 MongoDB 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="7b4ec-165">이 샘플에서는 데이터 저장소로 MongoDB를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="7b4ec-166">모델 및 스키마를 관리하는 데 널리 사용되는 플러그 인인 Mongoose를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="7b4ec-167">MongoDB라고도 하는 MongoDB용 데이터베이스 드라이버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="7b4ec-168">8: 추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="7b4ec-168">8: Install additional modules</span></span>
<span data-ttu-id="7b4ec-169">나머지 필수 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="7b4ec-170">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-171">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-171">Enter the following commands.</span></span> <span data-ttu-id="7b4ec-172">명령은 node_modules 디렉터리에 다음 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="7b4ec-173">9: 종속성에 대한 Server.js 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="7b4ec-174">Server.js 파일은 웹 API 서버에 대한 대부분의 기능을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="7b4ec-175">이 파일에 대부분의 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-175">Add most of your code to this file.</span></span> <span data-ttu-id="7b4ec-176">프로덕션 목적으로, 기능을 별도 경로 및 컨트롤러와 같은 좀 더 작은 파일로 리팩터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="7b4ec-177">이 문서에서는 이 목적을 위해 Server.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="7b4ec-178">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-179">선택한 편집기를 사용하여 Server.js 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="7b4ec-180">파일에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="7b4ec-181">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-181">Save the file.</span></span> <span data-ttu-id="7b4ec-182">잠시 후에 이 파일로 다시 돌아갈 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="7b4ec-183">10: Azure AD 설정을 저장하기 위한 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="7b4ec-184">이 코드 파일은 Azure AD 포털의 구성 매개 변수를 Passport.js에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="7b4ec-185">문서의 시작 부분에서 포털에 웹 API를 추가했을 때 이러한 구성 값을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="7b4ec-186">코드를 복사한 후에 이러한 매개 변수 값에 추가할 항목에 대해 설명할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="7b4ec-187">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-188">편집기에서 Config.js 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="7b4ec-189">다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="7b4ec-190">필요한 값</span><span class="sxs-lookup"><span data-stu-id="7b4ec-190">Required values</span></span>

*   <span data-ttu-id="7b4ec-191">**IdentityMetadata**: `passport-azure-ad`는 여기서 IDP(ID 공급자)에 대한 구성 데이터와 JWT(JSON Web Token)의 유효성을 검사할 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="7b4ec-192">Azure AD를 사용하는 경우 아마도 변경하길 원치 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="7b4ec-193">**audience**: 포털에서의 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7b4ec-194">키는 자주 롤링됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="7b4ec-195">항상 "openid_keys" URL에서 끌어오며 앱에서 인터넷에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="7b4ec-196">11: Server.js 파일에 구성 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="7b4ec-197">응용 프로그램에서 방금 만든 구성 파일로부터 값을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="7b4ec-198">응용 프로그램에서 .config 파일을 필수 리소스로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="7b4ec-199">Config.js에 있는 것으로 전역 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="7b4ec-200">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-201">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-201">In an editor, open Server.js.</span></span> <span data-ttu-id="7b4ec-202">다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="7b4ec-203">Server.js에 새 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="7b4ec-204">12: Moongoose를 사용하여 MongoDB 모델 및 스키마 정보 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="7b4ec-205">다음으로 REST API 서비스에서 이러한 3개의 파일을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="7b4ec-206">이 문서에서 MongoDB를 사용하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="7b4ec-207">이 부분은 *4단계*에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="7b4ec-208">11단계에서 만든 Config.js 파일에서 데이터베이스는 *tasklist*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="7b4ec-209">mongoose_auth_local 연결 URL의 끝에 넣은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="7b4ec-210">MongoDB에서 이 데이터베이스를 미리 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="7b4ec-211">데이터베이스는 서버 응용 프로그램의 첫 번째 실행에서 생성됩니다(데이터베이스가 아직 없다고 가정).</span><span class="sxs-lookup"><span data-stu-id="7b4ec-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="7b4ec-212">서버에 사용할 MongoDB 데이터베이스를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="7b4ec-213">다음으로 서버 작업에 대한 모델 및 스키마를 만드는 몇 가지 추가 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="7b4ec-214">모델</span><span class="sxs-lookup"><span data-stu-id="7b4ec-214">The model</span></span>
<span data-ttu-id="7b4ec-215">스키마 모델은 매우 기본적입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-215">The schema model is very basic.</span></span> <span data-ttu-id="7b4ec-216">필요한 경우 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="7b4ec-217">스키마 모델에는 다음 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-217">The schema model has these values:</span></span>

*   <span data-ttu-id="7b4ec-218">**이름**.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-218">**NAME**.</span></span> <span data-ttu-id="7b4ec-219">작업에 할당된 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-219">The person assigned to the task.</span></span> <span data-ttu-id="7b4ec-220">**문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-220">This is a **string** value.</span></span>
*   <span data-ttu-id="7b4ec-221">**작업**.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-221">**TASK**.</span></span> <span data-ttu-id="7b4ec-222">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-222">The name of the task.</span></span> <span data-ttu-id="7b4ec-223">**문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-223">This is a **string** value.</span></span>
*   <span data-ttu-id="7b4ec-224">**날짜**.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-224">**DATE**.</span></span> <span data-ttu-id="7b4ec-225">작업이 만료되는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-225">The date that the task is due.</span></span> <span data-ttu-id="7b4ec-226">**datetime** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="7b4ec-227">**완료됨**.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-227">**COMPLETED**.</span></span> <span data-ttu-id="7b4ec-228">작업이 완료되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-228">Whether the task is completed.</span></span> <span data-ttu-id="7b4ec-229">**부울** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="7b4ec-230">코드에 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="7b4ec-231">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-232">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-232">In your editor, open Server.js.</span></span> <span data-ttu-id="7b4ec-233">구성 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="7b4ec-234">이 코드는 MongoDB 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="7b4ec-235">또한 스키마 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="7b4ec-236">스키마를 사용하여 코드에서 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="7b4ec-237">위의 코드 아래에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="7b4ec-238">코드를 보면 알 수 있듯이, 먼저 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="7b4ec-239">다음으로 모델 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-239">Next, you create a model object.</span></span> <span data-ttu-id="7b4ec-240">모델 개체를 사용하여 **경로**를 정의할 때 코드 전체에서 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="7b4ec-241">13: 작업 REST API 서버에 대한 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="7b4ec-242">작업할 데이터베이스 모델이 준비되었으므로 REST API 서버에 사용할 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="7b4ec-243">Restify의 경로 정보</span><span class="sxs-lookup"><span data-stu-id="7b4ec-243">About routes in restify</span></span>
<span data-ttu-id="7b4ec-244">Restify의 경로는 Express 스택을 사용할 때 작동하는 방식과 정확하게 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="7b4ec-245">클라이언트 응용 프로그램이 호출할 것으로 예상하는 URI를 사용하여 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="7b4ec-246">일반적으로 경로는 별도 파일에 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="7b4ec-247">이 자습서에서는 Server.js에 경로를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="7b4ec-248">프로덕션 사용을 위해서는 자체 파일로 경로를 팩터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="7b4ec-249">Restify 경로의 일반적인 패턴:</span><span class="sxs-lookup"><span data-stu-id="7b4ec-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="7b4ec-250">가장 기본적인 수준의 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="7b4ec-251">Resitfy(및 Express)는 응용 프로그램 유형 및 여러 끝점에 복잡한 라우팅을 정의하는 기능과 같은 훨씬 수준 높은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="7b4ec-252">서버에 기본 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-252">Add default routes to your server</span></span>
<span data-ttu-id="7b4ec-253">**만들기**, **검색**, **업데이트** 및 **삭제**의 기본 CRUD 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="7b4ec-254">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="7b4ec-255">편집기에서 Server.js를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-255">In an editor, open Server.js.</span></span> <span data-ttu-id="7b4ec-256">이전에 작성한 데이터베이스 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="7b4ec-257">경로에 대한 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-257">Add error handling for the routes</span></span>
<span data-ttu-id="7b4ec-258">발생한 문제에 대해 클라이언트에 다시 통신할 수 있도록 일부 오류 처리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="7b4ec-259">이미 작성한 코드 아래에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="7b4ec-260">14: 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-260">14: Create your server</span></span>
<span data-ttu-id="7b4ec-261">수행할 마지막 작업은 서버 인스턴스를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="7b4ec-262">서버 인스턴스는 호출을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-262">The server instance manages your calls.</span></span>

<span data-ttu-id="7b4ec-263">Restify(및 Express)는 REST API 서버에 사용할 수 있는 심층적인 사용자 지정을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="7b4ec-264">이 자습서에서는 가장 기본 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="7b4ec-265">15: 경로 추가(지금은 인증 없이)</span><span class="sxs-lookup"><span data-stu-id="7b4ec-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="7b4ec-266">16: 서버 실행</span><span class="sxs-lookup"><span data-stu-id="7b4ec-266">16: Run the server</span></span>
<span data-ttu-id="7b4ec-267">인증을 추가하기 전에 서버를 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="7b4ec-268">서버를 테스트하는 가장 쉬운 방법은 명령 프롬프트에서 curl을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="7b4ec-269">이 작업을 수행하려면 JSON으로 출력을 구문 분석하는 데 사용할 수 있는 간단한 유틸리티가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="7b4ec-270">다음 예제에서 사용하는 JSON 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="7b4ec-271">이렇게 하면 JSON 도구가 전역적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="7b4ec-272">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="7b4ec-273">디렉터리를 **azuread**로 변경한 다음 curl을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="7b4ec-274">작업을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="7b4ec-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="7b4ec-275">응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-275">The response should be:</span></span>

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

5.  <span data-ttu-id="7b4ec-276">Brandon에 대한 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="7b4ec-277">이러한 모든 명령이 오류 없이 실행하는 경우 OAuth를 REST API 서버에 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="7b4ec-278">*이제 MongoDB를 사용하는 REST API 서버가 완료되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="7b4ec-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="7b4ec-279">17: REST API 서버에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="7b4ec-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="7b4ec-280">이제 실행 중인 REST API가 있으므로 Azure AD와 함께 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="7b4ec-281">명령 프롬프트에서 디렉터리를 **azuread**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="7b4ec-282">passport-azure-ad에 포함된 oidcbearerstrategy 사용</span><span class="sxs-lookup"><span data-stu-id="7b4ec-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="7b4ec-283">지금까지 권한 부여 없이 일반적인 REST TODO 서버를 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="7b4ec-284">이제 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-284">Now, add authentication.</span></span>

<span data-ttu-id="7b4ec-285">먼저 Passport 사용을 원한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="7b4ec-286">이전 서버 구성 바로 뒤에 이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="7b4ec-287">API를 작성하는 경우 항상 사용자가 스푸핑할 수 없는 토큰의 고유한 항목에 데이터를 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="7b4ec-288">이 서버는 TODO 항목을 저장할 때 토큰의 사용자 구독 ID(token.sub라고 함)를 기준으로 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="7b4ec-289">"소유자" 필드에 token.sub를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="7b4ec-290">이렇게 하면 해당 사용자만 사용자의 TODO에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="7b4ec-291">다른 사람은 입력한 TODO에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="7b4ec-292">"소유자"에 대한 API에 노출이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="7b4ec-293">외부 사용자는 인증되는 경우에 다른 사용자의 TODO를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="7b4ec-294">다음으로 `passport-azure-ad`에 포함된 Open ID Connect 전달자 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="7b4ec-295">이전에 붙여 넣은 코드 뒤에 이 코드를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="7b4ec-296">Passport는 모든 전략(Twitter, Facebook 등)에 유사한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="7b4ec-297">모든 전략 작성자는 이 패턴을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="7b4ec-298">토큰 및 `done`을 매개 변수로 사용하는 `function()`에 전략을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="7b4ec-299">전략은 모든 작업을 수행한 후에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="7b4ec-300">사용자를 저장하고 토큰을 보관하여 다시 요청하지 않아도 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b4ec-301">이전 코드는 서버를 인증할 수 있는 모든 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="7b4ec-302">이를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-302">This is known as auto-registration.</span></span> <span data-ttu-id="7b4ec-303">프로덕션 서버에서는 선택한 등록 프로세스를 먼저 통과해야만 사용자 액세스를 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="7b4ec-304">일반적으로 이 패턴은 소비자 앱에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="7b4ec-305">앱에서는 Facebook에 등록할 수 있도록 허용하지만 추가 정보를 입력하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="7b4ec-306">이 자습서에서 명령줄 프로그램을 사용하지 않는 경우 반환되는 토큰 개체에서 메일을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="7b4ec-307">그런 다음 추가 정보를 입력하도록 사용자에게 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="7b4ec-308">테스트 서버이므로 메모리 내 데이터베이스에 직접 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="7b4ec-309">끝점 보호</span><span class="sxs-lookup"><span data-stu-id="7b4ec-309">Protect endpoints</span></span>
<span data-ttu-id="7b4ec-310">사용하려는 프로토콜을 통해 **passport.authenticate()** 호출을 지정하여 끝점을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="7b4ec-311">고급 옵션에 대한 서버 코드에서 사용자의 경로를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="7b4ec-312">18: 서버 응용 프로그램 다시 실행</span><span class="sxs-lookup"><span data-stu-id="7b4ec-312">18: Run your server application again</span></span>
<span data-ttu-id="7b4ec-313">curl을 다시 사용하여 끝점에 대해 OAuth 2.0 보호가 적용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="7b4ec-314">이 끝점에 대해 클라이언트 SDK 중 하나를 실행하기 전에 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="7b4ec-315">반환되는 헤더는 사용자 인증이 올바르게 작동하는 경우 알려주어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="7b4ec-316">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="7b4ec-317">**azuread** 디렉터리로 변경한 다음 curl을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="7b4ec-318">기본 POST를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="7b4ec-319">401 응답은 Passport 계층이 인증 끝점으로 리디렉션을 시도하고 있음을 나타냅니다. 정확하게 우리가 원하는 대로 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="7b4ec-320">*이제 OAuth 2.0을 사용하는 REST API 서비스가 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="7b4ec-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="7b4ec-321">OAuth 2.0 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="7b4ec-322">이를 위해 추가 자습서를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b4ec-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b4ec-323">Next steps</span></span>
<span data-ttu-id="7b4ec-324">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [.zip 파일](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="7b4ec-325">GitHub에서 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="7b4ec-326">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="7b4ec-327">[v2.0 끝점을 사용하여 Node.js 웹앱의 보안 유지](active-directory-v2-devquickstarts-node-web.md)를 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="7b4ec-328">다음은 몇 가지 추가 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="7b4ec-329">Azure AD v2.0 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="7b4ec-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7b4ec-330">Stack Overflow "azure-active-directory" 태그</span><span class="sxs-lookup"><span data-stu-id="7b4ec-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7b4ec-331">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="7b4ec-331">Get security updates for our products</span></span>
<span data-ttu-id="7b4ec-332">보안 사고가 발생할 때 알림을 받으려면 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="7b4ec-333">[Microsoft 기술 보안 알림](https://technet.microsoft.com/security/dd252948) 페이지에서 보안 권고 알림을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4ec-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

