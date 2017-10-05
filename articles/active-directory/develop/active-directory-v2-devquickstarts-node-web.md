---
title: "Azure Active Directory v2.0 Node.js 웹앱 로그인 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정을 사용하여 사용자를 로그인하는 Node.js 웹앱을 작성하는 방법을 알아봅니다."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="38e4c-103">Node.js 웹앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="38e4c-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="38e4c-104">일부 Azure Active Directory 시나리오 및 기능은 v2.0 끝점에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="38e4c-105">v2.0 끝점을 사용해야 하는지 v1.0 끝점을 사용해야 하는지를 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38e4c-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="38e4c-106">이 자습서에서는 Passport를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="38e4c-107">웹앱에서 Azure AD(Azure Active Directory) 및 v2.0 끝점을 사용하여 사용자를 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="38e4c-108">사용자에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-108">Display information about the user.</span></span>
* <span data-ttu-id="38e4c-109">앱에서 사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-109">Sign the user out of the app.</span></span>

<span data-ttu-id="38e4c-110">**Passport** 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="38e4c-111">유연한 모듈식 Passport는 어떤 Express 기반 또는 restify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="38e4c-112">Passport에서는 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 또는 기타 옵션을 사용하여 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="38e4c-113">Microsoft는 Azure AD에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="38e4c-114">이 문서에서는 모듈을 설치한 다음 Azure AD `passport-azure-ad` 플러그 인을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="38e4c-115">다운로드</span><span class="sxs-lookup"><span data-stu-id="38e4c-115">Download</span></span>
<span data-ttu-id="38e4c-116">이 자습서에 대한 코드는 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="38e4c-117">자습서에 따라 [.zip 파일로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip)하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="38e4c-118">또한 이 자습서의 끝 부분에서는 완성된 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="38e4c-119">1: 앱 등록</span><span class="sxs-lookup"><span data-stu-id="38e4c-119">1: Register an app</span></span>
<span data-ttu-id="38e4c-120">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 [이러한 세부 단계](active-directory-v2-app-registration.md)에 따라 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="38e4c-121">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-121">Make sure you:</span></span>

* <span data-ttu-id="38e4c-122">앱에 할당된 **응용 프로그램 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="38e4c-123">이 자습서에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="38e4c-124">앱에 대한 **웹** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="38e4c-125">포털에서 **리디렉션 URI** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="38e4c-126">`urn:ietf:wg:oauth:2.0:oob`의 기본 URI 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="38e4c-127">2: 디렉터리에 필수 구성 요소 추가</span><span class="sxs-lookup"><span data-stu-id="38e4c-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="38e4c-128">아직 루트 폴더에 있지 않은 경우 명령 프롬프트에서 디렉터리를 변경하여 루트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="38e4c-129">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-129">Run the following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="38e4c-130">또한 빠른 시작의 구조에서 `passport-azure-ad`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="38e4c-131">그러면 `passport-azure-ad`에서 사용하는 라이브러리가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="38e4c-132">3: passport-node-js 전략을 사용하도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="38e4c-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="38e4c-133">OpenID Connect 인증 프로토콜을 사용하도록 Express 미들웨어를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="38e4c-134">Passport를 사용하여 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하고, 사용자에 대한 정보를 가져오는 등의 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="38e4c-135">프로젝트의 루트에서 Config.js 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="38e4c-136">`exports.creds` 섹션에서 앱의 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="38e4c-137">`clientID`: Azure Portal에서 앱에 할당되는 **응용 프로그램 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="38e4c-138">`returnURL`: 포털에서 입력한 **리디렉션 URI**입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="38e4c-139">`clientSecret`: 포털에서 생성한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="38e4c-140">프로젝트의 루트에서 App.js 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="38e4c-141">`passport-azure-ad`와 함께 제공되는 OIDCStrategy 전략을 호출하려면 다음 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="38e4c-142">로그인 요청을 처리하려면 방금 참조한 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
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

<span data-ttu-id="38e4c-143">Passport는 모든 전략(Twitter, Facebook 등)에 유사한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="38e4c-144">모든 전략 작성자는 이 패턴을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="38e4c-145">토큰 및 `done`을 매개 변수로 사용하는 `function()`에 전략을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="38e4c-146">전략은 모든 작업을 수행한 후에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="38e4c-147">사용자를 저장하고 토큰을 보관하여 다시 요청하지 않아도 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="38e4c-148">이전 코드는 서버를 인증할 수 있는 모든 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="38e4c-149">이를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-149">This is known as auto-registration.</span></span> <span data-ttu-id="38e4c-150">프로덕션 서버에서는 선택한 등록 프로세스를 먼저 통과해야만 사용자 액세스를 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="38e4c-151">일반적으로 이 패턴은 소비자 앱에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="38e4c-152">앱에서는 Facebook에 등록할 수 있도록 허용하지만 추가 정보를 입력하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="38e4c-153">이 자습서에서 명령줄 프로그램을 사용하지 않는 경우 반환되는 토큰 개체에서 메일을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="38e4c-154">그런 다음 추가 정보를 입력하도록 사용자에게 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="38e4c-155">테스트 서버이므로 메모리 내 데이터베이스에 직접 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="38e4c-156">Passport의 요구에 따라 로그인한 사용자를 추적하는 데 사용할 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="38e4c-157">여기에는 사용자 정보의 직렬화 및 역직렬화가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="38e4c-158">Express 엔진을 로드하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="38e4c-159">Express가 제공하는 기본 /views 및 /routes 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-159">You use the default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="38e4c-160">실제 로그인 요청을 `passport-azure-ad` 엔진에 전달하는 POST 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="38e4c-161">4: Passport를 사용하여 Azure AD에 로그인 및 로그아웃 요청 실행</span><span class="sxs-lookup"><span data-stu-id="38e4c-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="38e4c-162">이제 앱이 OpenID Connect 인증 프로토콜을 사용하여 v2.0 끝점과 통신하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="38e4c-163">`passport-azure-ad` 전략은 인증 메시지를 작성하고, Azure AD에서 토큰의 유효성을 검사하고, 사용자 세션을 유지 관리하는 모든 세부 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="38e4c-164">이제 사용자에게 로그인 및 로그아웃하는 방법을 알려 주고 로그인한 사용자에 대한 추가 정보를 수집하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="38e4c-165">**기본**, **로그인**, **계정** 및 **로그아웃** 메서드를 App.js 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="38e4c-166">세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-166">Here are the details:</span></span>
    
    * <span data-ttu-id="38e4c-167">`/` 경로는 index.ejs 보기로 리디렉션되며,</span><span class="sxs-lookup"><span data-stu-id="38e4c-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="38e4c-168">요청에서 사용자(있는 경우)를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="38e4c-169">`/account` 경로는 먼저 *인증되었는지 확인*합니다(다음 코드에서 구현).</span><span class="sxs-lookup"><span data-stu-id="38e4c-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="38e4c-170">그런 다음 요청에서 사용자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="38e4c-171">따라서 사용자에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="38e4c-172">`/login` 경로는 `passport-azuread`에서 `azuread-openidconnect` 인증자를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="38e4c-173">성공하지 못하면 경로는 사용자를 다시 `/login`으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="38e4c-174">`/logout` 경로는 logout.ejs 보기(및 경로)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="38e4c-175">이 경로는 쿠키를 지운 다음 사용자를 다시 index.ejs로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="38e4c-176">`/account`의 앞부분에서 사용한 **EnsureAuthenticated** 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="38e4c-177">App.js에서 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="38e4c-178">5: 웹 사이트에서 사용자를 표시하는 보기 및 경로를 Express에서 만들기</span><span class="sxs-lookup"><span data-stu-id="38e4c-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="38e4c-179">사용자에 대한 정보를 표시하는 경로 및 보기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="38e4c-180">또한 경로 및 보기는 만든 `/logout` 및 `/login` 경로를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="38e4c-181">루트 디렉터리에서 `/routes/index.js` 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="38e4c-182">루트 디렉터리에서 `/routes/user.js` 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="38e4c-183">`/routes/index.js` 및 `/routes/user.js`는 사용자(있는 경우)를 포함하여 요청을 보기에 전달하는 간단한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="38e4c-184">루트 디렉터리에서 `/views/index.ejs` 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="38e4c-185">이 페이지는 **로그인** 및 **로그아웃** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="38e4c-186">또한 `/views/index.ejs` 보기를 사용하여 계정 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="38e4c-187">요청에서 사용자를 전달할 때 조건부 `if (!user)`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="38e4c-188">이는 사용자가 로그인했다는 증거입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="38e4c-189">루트 디렉터리에서 `/views/account.ejs` 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="38e4c-190">`/views/account.ejs` 보기에서는 `passport-azuread`가 사용자 요청에 넣는 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="38e4c-191">레이아웃을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-191">Add a layout.</span></span> <span data-ttu-id="38e4c-192">루트 디렉터리에서 `/views/layout.ejs` 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="38e4c-193">앱을 빌드하고 실행하려면 `node app.js`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="38e4c-194">그런 다음 `http://localhost:3000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="38e4c-195">개인 Microsoft 계정이나 회사 또는 학교 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="38e4c-196">사용자의 ID가 /account 목록에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="38e4c-197">이제 산업 표준 프로토콜을 사용하여 보호되는 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="38e4c-198">앱에서 개인 및 회사 또는 학교 계정을 사용하여 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38e4c-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38e4c-199">Next steps</span></span>
<span data-ttu-id="38e4c-200">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [.zip 파일](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="38e4c-201">GitHub에서 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="38e4c-202">다음으로 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="38e4c-203">다음 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-203">You might want to try:</span></span>

[<span data-ttu-id="38e4c-204">v2.0 끝점을 사용하여 Node.js 웹 API의 보안 유지</span><span class="sxs-lookup"><span data-stu-id="38e4c-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="38e4c-205">다음은 몇 가지 추가 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="38e4c-206">Azure AD v2.0 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="38e4c-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="38e4c-207">Stack Overflow "azure-active-directory" 태그</span><span class="sxs-lookup"><span data-stu-id="38e4c-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="38e4c-208">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="38e4c-208">Get security updates for our products</span></span>
<span data-ttu-id="38e4c-209">보안 사고가 발생할 때 알림을 받으려면 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="38e4c-210">[Microsoft 기술 보안 알림](https://technet.microsoft.com/security/dd252948) 페이지에서 보안 권고 알림을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="38e4c-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

