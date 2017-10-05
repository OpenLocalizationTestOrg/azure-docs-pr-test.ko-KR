---
title: "Azure B2C용 Node.js 웹앱에 로그인 추가 | Microsoft Docs"
description: "B2C 테넌트를 사용하여 사용자가 로그인하는 Node.js 웹앱을 작성하는 방법입니다."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="a3613-103">Azure AD B2C: Node.js 웹앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="a3613-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="a3613-104">**Passport** 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="a3613-105">매우 유연한 모듈식 Passport는 어떤 Express 기반 또는 Resitify 웹 응용 프로그램에도 원활하게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="a3613-106">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="a3613-107">Microsoft는 Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a3613-108">여기서는 이 모듈을 설치하고 Azure AD `passport-azure-ad` 플러그 인에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="a3613-109">이렇게 하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-109">To do this, you need to:</span></span>

1. <span data-ttu-id="a3613-110">Azure AD를 사용하여 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="a3613-111">앱을 설정하여 `passport-azure-ad` 플러그 인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="a3613-112">Passport를 사용하여 Azure AD에 로그인 및 로그아웃 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="a3613-113">사용자 데이터를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-113">Print user data.</span></span>

<span data-ttu-id="a3613-114">이 자습서에 대한 코드는 [GitHub에서 유지 관리됩니다](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="a3613-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="a3613-115">자습서에 따라 [.zip 파일로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="a3613-116">구조를 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="a3613-117">전체 응용 프로그램은 이 자습서 마지막 부분에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a3613-118">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="a3613-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="a3613-119">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="a3613-120">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a3613-121">아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a3613-122">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a3613-122">Create an application</span></span>

<span data-ttu-id="a3613-123">다음으로 B2C 디렉터리에서 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="a3613-124">앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="a3613-125">하나의 논리 앱을 구성하기 때문에 클라이언트 앱과 웹 API는 모두 단일 **응용 프로그램 ID**에서 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="a3613-126">앱을 만들려면 [다음 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a3613-127">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-127">Be sure to:</span></span>

- <span data-ttu-id="a3613-128">응용 프로그램에 **웹앱**/**웹 API**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="a3613-129">**회신 URL**로 `http://localhost:3000/auth/openid/return`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="a3613-130">이 코드 샘플에 대한 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="a3613-131">응용 프로그램에 **응용 프로그램 암호** 를 만들고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="a3613-132">이 시간은 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-132">You will need it later.</span></span> <span data-ttu-id="a3613-133">참고로 이 값은 사용하기 전에 [XML 이스케이프](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="a3613-134">앱에 할당된 **응용 프로그램 ID** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="a3613-135">나중에도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a3613-136">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="a3613-136">Create your policies</span></span>

<span data-ttu-id="a3613-137">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a3613-138">이 앱은 등록, 로그인 및 Facebook을 사용하여 로그인 등 세 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="a3613-139">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 각 형식에 이 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="a3613-140">세 가지 정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="a3613-141">등록 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="a3613-142">모든 정책에서 **표시 이름** 및 **개체 ID** 응용 프로그램 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="a3613-143">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="a3613-144">각 정책을 만든 후에 **이름**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="a3613-145">접두사 `b2c_1_`이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="a3613-146">이러한 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a3613-147">세 가지 정책을 만들었다면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="a3613-148">이 문서는 방금 만든 정책을 사용하는 방법을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="a3613-149">Azure AD B2C에서 정책 작동 방법을 알아보려면 [.NET 웹앱 시작 자습서](active-directory-b2c-devquickstarts-web-dotnet.md)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="a3613-150">필수 구성 요소를 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="a3613-151">아직 수행하지 않은 경우 명령줄에서 디렉터리를 루트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="a3613-152">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-152">Run the following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="a3613-153">또한 빠른 시작의 골격에 있는 미리 보기에 `passport-azure-ad`를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="a3613-154">이는 `passport-azure-ad`가 의존하는 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="a3613-155">Passport-Node.js 전략을 사용하도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="a3613-156">OpenID Connect 인증 프로토콜을 사용하도록 빠른 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a3613-157">Passport는 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하며, 사용자에 대한 정보를 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="a3613-158">프로젝트 루트에 있는 `config.js` 파일을 열고 `exports.creds` 섹션에 앱의 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="a3613-159">`clientID`: 등록 포털에서 앱에 할당된 **응용 프로그램 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="a3613-160">`returnURL`: 포털에서 입력한 **리디렉션 URI**입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="a3613-161">`tenantName`: 앱의 테넌트 이름(예: **contoso.onmicrosoft.com**)입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="a3613-162">프로젝트의 루트에서 `app.js` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="a3613-163">다음 호출을 추가하여 `passport-azure-ad`와 함께 제공되는 `OIDCStrategy` 전략을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="a3613-164">로그인 요청을 처리하도록 참조한 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="a3613-165">Passport는 Twitter, Facebook을 포함한 모든 전략에 비슷한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="a3613-166">모든 전략 작성자는 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="a3613-167">전략을 보면 매개 변수로 토큰을 가진 `function()` 및 `done`을 전달하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="a3613-168">전략은 모든 작업을 완료한 후에 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="a3613-169">사용자를 저장하고 다시 요청하지 않아도 되도록 토큰을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="a3613-170">앞의 코드는 서버에서 인증한 모든 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="a3613-171">이는 자동 등록입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-171">This is autoregistration.</span></span> <span data-ttu-id="a3613-172">프로덕션 서버를 사용하는 경우 설정한 등록 프로세스를 통해 마치지 않으면 사용자를 통과시키지 않으려 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="a3613-173">소비자 앱에서 이 패턴을 종종 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="a3613-174">Facebook을 사용하여 등록할 수 있지만 추가 정보를 입력하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="a3613-175">응용 프로그램이 샘플이 아니라면 반환된 토큰 개체에서 메일을 추출하고 사용자에게 추가 정보를 입력하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="a3613-176">테스트 서버이므로 메모리 내 데이터베이스에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="a3613-177">Passport의 필요에 따라 로그인한 사용자를 추적할 수 있도록 하는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="a3613-178">여기에는 사용자 정보의 직렬화 및 역직렬화가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="a3613-179">빠른 엔진을 로드하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="a3613-180">다음 예제에서는 빠른 설치가 제공하는 기본값 `/views` 및 `/routes` 패턴의 사용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="a3613-181">실제 로그인 요청을 `passport-azure-ad` 엔진에 전달하는 `POST` 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="a3613-182">Passport를 사용하여 Azure AD에 로그인 및 로그아웃 요청 실행</span><span class="sxs-lookup"><span data-stu-id="a3613-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="a3613-183">이제 앱이 OpenID Connect 인증 프로토콜을 사용하여 v2.0 끝점과 통신하도록 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a3613-184">`passport-azure-ad`가 인증 메시지를 작성하고, Azure AD에서 토큰의 유효성을 검사하고, 사용자 세션을 유지 관리하는 세부 과정을 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="a3613-185">이제 사용자에게 로그인 및 로그아웃하는 방법을 알려주고 로그인한 사용자에 대한 추가 정보를 수집하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="a3613-186">우선 기본값, 로그인, 계정 및 로그아웃 메서드를 `app.js` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="a3613-187">이러한 메서드를 자세히 검토하려면:</span><span class="sxs-lookup"><span data-stu-id="a3613-187">To review these methods in detail:</span></span>
- <span data-ttu-id="a3613-188">`/` 경로는 요청에서 사용자를 전달하여(있는 경우) `index.ejs` 뷰로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="a3613-189">`/account` 경로는 우선 사용자가 인증되었는지 확인합니다(이에 대한 구현은 아래에 있음).</span><span class="sxs-lookup"><span data-stu-id="a3613-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="a3613-190">그런 다음 사용자에 대한 추가 정보를 얻을 수 있도록 요청에 사용자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="a3613-191">`/login` 경로는 `passport-azure-ad`에서 `azuread-openidconnect` 인증자를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="a3613-192">성공하지 못하면 경로는 사용자를 다시 `/login`으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="a3613-193">`/logout`은 단순히 `logout.ejs`(및 해당 경로)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="a3613-194">쿠키를 비운 다음 사용자를 다시 `index.ejs`로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="a3613-195">`app.js`의 마지막 부분에 `/account` 경로에 사용되는 `EnsureAuthenticated` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="a3613-196">마지막으로, `app.js`에서 서버 자체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="a3613-197">빠른 실행에서 뷰와 경로를 만들어 정책 호출</span><span class="sxs-lookup"><span data-stu-id="a3613-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="a3613-198">이제 `app.js`가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="a3613-199">로그인 및 등록 정책을 호출할 수 있도록 하는 경로 및 뷰를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="a3613-200">또한 만든 `/logout` 및 `/login` 경로를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="a3613-201">루트 디렉터리 아래에 `/routes/index.js` 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="a3613-202">루트 디렉터리 아래에 `/routes/user.js` 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="a3613-203">이러한 간단한 경로는 뷰에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="a3613-204">사용자가 있는 경우 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-204">They include the user, if one is present.</span></span>

<span data-ttu-id="a3613-205">루트 디렉터리 아래에 `/views/index.ejs` 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="a3613-206">로그인 및 로그아웃에 대한 정책을 호출하는 단순한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="a3613-207">또한 이를 사용하여 계정 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-207">You can also use it to grab account information.</span></span> <span data-ttu-id="a3613-208">사용자가 로그인한 증명을 제공하는 요청을 통해 전달되기 때문에 조건부 `if (!user)`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="a3613-209">`passport-azure-ad`가 사용자 요청에 포함한 추가 정보를 볼 수 있도록 루트 디렉터리에 `/views/account.ejs` 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="a3613-210">이제 앱을 작성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-210">You can now build and run your app.</span></span>

<span data-ttu-id="a3613-211">`node app.js`를 실행하고 `http://localhost:3000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="a3613-212">전자 메일 또는 Facebook을 사용하여 앱에 등록 또는 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="a3613-213">로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="a3613-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3613-214">Next steps</span></span>

<span data-ttu-id="a3613-215">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [.zip 파일로 제공](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip)됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="a3613-216">또한 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="a3613-217">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="a3613-218">다음을 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3613-218">You might try:</span></span>

[<span data-ttu-id="a3613-219">Node.js에서 B2C 모델을 사용하여 웹 API 보안</span><span class="sxs-lookup"><span data-stu-id="a3613-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
