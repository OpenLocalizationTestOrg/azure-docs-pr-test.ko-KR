---
title: "Azure AD 로그인으로 시작 및 Node.js를 사용 하 여 로그 아웃 aaaGetting | Microsoft Docs"
description: "어떻게 toobuild Node.js Express MVC 웹 로그인에 대 한 Azure AD와 통합 되는 앱에 알아봅니다."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="c5383-103">Azure AD에서 Node.js 웹앱 로그인 및 로그아웃</span><span class="sxs-lookup"><span data-stu-id="c5383-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="c5383-104">여기서는 Passport를 통해 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-104">Here we use Passport to:</span></span>

* <span data-ttu-id="c5383-105">Sign hello Azure Active Directory (Azure AD)와 toohello 응용 프로그램에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="c5383-106">Hello 사용자에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-106">Display information about hello user.</span></span>
* <span data-ttu-id="c5383-107">Sign hello hello 앱에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="c5383-108">Passport는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="c5383-109">유동 및 모듈형, Passport tooany에 프로그램과 원활 하 게 삭제 될 수 있습니다 Express 기반 웹 응용 프로그램 restify 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="c5383-110">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="c5383-111">Microsoft는 Microsoft Azure Active Directory에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="c5383-112">이 모듈을 설치 하 고 다음 Microsoft Azure Active Directory hello 추가 `passport-azure-ad` 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="c5383-113">toodo이, take hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="c5383-114">앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-114">Register an app.</span></span>
2. <span data-ttu-id="c5383-115">응용 프로그램 toouse hello 설정 `passport-azure-ad` 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="c5383-116">Passport tooissue 로그인 및 로그 아웃 요청 tooAzure AD 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="c5383-117">Hello 사용자에 대 한 데이터를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-117">Print data about hello user.</span></span>

<span data-ttu-id="c5383-118">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="c5383-119">수에 따라 toofollow, [hello 응용 프로그램의 구조를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="c5383-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="c5383-120">완료 하는 hello 응용 프로그램 뿐이 자습서의 hello 끝에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="c5383-121">1단계: 앱 등록</span><span class="sxs-lookup"><span data-stu-id="c5383-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="c5383-122">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c5383-123">Hello hello 페이지의 hello 위쪽 메뉴에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="c5383-124">Hello에서 **디렉터리** 목록 tooregister 원하는 hello Active Directory 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="c5383-125">선택 **더 서비스** hello 메뉴 hello에 왼쪽 쪽의 hello 화면 및 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="c5383-126">**앱 등록**을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="c5383-127">Hello 프롬프트 toocreate에 따라 한 **웹 응용 프로그램** 및/또는 **WebAPI**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="c5383-128">hello **이름** 응용 프로그램의 hello 응용 프로그램 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="c5383-129">hello **로그온 URL** hello 응용 프로그램의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="c5383-130">hello 켈 레 톤의 기본값은 ' http://localhost:3000/auth/openid/반환 '.</span><span class="sxs-lookup"><span data-stu-id="c5383-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="c5383-131">등록 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="c5383-132">Hello 다음에이 값이 필요한 섹션 이므로에서 복사 hello 응용 프로그램 페이지.</span><span class="sxs-lookup"><span data-stu-id="c5383-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="c5383-133">Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="c5383-134">hello **앱 ID URI** 응용 프로그램에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="c5383-135">hello 규칙은 toouse hello 형식 `https://<tenant-domain>/<app-name>`예를 들면: `https://contoso.onmicrosoft.com/my-first-aad-app`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="c5383-136">2 단계: 추가 필수 구성 요소 tooyour 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c5383-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="c5383-137">아닌 경우 이미 여기 hello 명령줄에서 디렉터리 tooyour 루트 폴더를 변경 실행된 hello 명령을 누른 다음:</span><span class="sxs-lookup"><span data-stu-id="c5383-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="c5383-138">또한 동일한 `passport-azure-ad`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="c5383-139">이렇게 하면 hello 라이브러리가 설치 하는 `passport-azure-ad` 에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="c5383-140">3 단계: 앱 toouse hello passport-노드-js 전략 설정</span><span class="sxs-lookup"><span data-stu-id="c5383-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="c5383-141">여기에서는 Express toouse hello OpenID Connect 인증 프로토콜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="c5383-142">Passport는 사용 되는 toodo 문제 로그인 및 로그 아웃 요청을 비롯 한 다양 한 항목을 hello 사용자의 세션을 관리 하 고 hello 사용자에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="c5383-143">toobegin, 열기 hello `config.js` hello hello 프로젝트 루트에 파일을 hello에 응용 프로그램의 구성 값을 입력 한 다음 `exports.creds` 섹션.</span><span class="sxs-lookup"><span data-stu-id="c5383-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="c5383-144">hello `clientID` 는 hello **응용 프로그램 Id** hello 등록 포털에서 할당 된 tooyour 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="c5383-145">hello `returnURL` 는 hello **리디렉션 Uri** hello 포털에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="c5383-146">hello `clientSecret` hello 암호로 hello 포털에서 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="c5383-147">Hello을 열고 `app.js` hello 프로젝트의 hello 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="c5383-148">다음 호출 tooinvoke hello 다음 hello 추가 `OIDCStrategy` 와 함께 제공 되는 전략 `passport-azure-ad`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="c5383-149">그 후 hello 전략에서는 방금 참조 toohandle 우리의 로그인 요청을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
<span data-ttu-id="c5383-150">Passport는 모든 전략 작성자가 준수하는 유사한 패턴을 모든 전략(Twitter, Facebook 등)에 대해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="c5383-151">전달 것에 토큰 및는 완료 하는 함수 hello 매개 변수로 참조 hello 전략을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="c5383-152">작업을 수행한 후 hello 전략 toous 다시 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="c5383-153">그런 다음 있게 하려면이 값 toostore hello 사용자 및 보관 hello 토큰에 대 한 tooask 다시 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="c5383-154">이전 코드 hello tooauthenticate tooour 서버에서 발생 하는 모든 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="c5383-155">이를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-155">This is known as auto-registration.</span></span> <span data-ttu-id="c5383-156">첫 번째 있는 것을 결정 하는 프로세스를 통해 등록 하지 않고 tooa 프로덕션 서버를 인증 하는 모든 사용자를 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="c5383-157">이 일반적으로 hello 패턴을 사용 하면 Facebook과 tooregister 있지만 다음 tooprovide 추가 정보를 요청 하는 소비자 앱에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="c5383-158">샘플 응용 프로그램, 하지 우리 hello 토큰 개체를 반환 하 고 다음 hello 사용자 toofill 추가 정보를 요청 하는에서 hello 사용자의 전자 메일 주소를 추출 하 고 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="c5383-159">테스트 서버 이기 때문에 여기서 추가할 toohello 메모리 내 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="c5383-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="c5383-160">다음으로 파악 하는 tootrack hello 로그인 사용자가 Passport 요구에 따라 hello 메서드를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="c5383-161">이러한 메서드는 직렬화 및 역직렬화 hello 사용자의 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-161">These methods include serializing and deserializing hello user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  <span data-ttu-id="c5383-162">다음으로 hello 코드 tooload hello Express 엔진을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="c5383-163">Hello 기본 /views 사용 여기 및 Express /routes 패턴을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

    ```JavaScript

        // configure Express (section 2)

            var app = express();
            app.configure(function() {
          app.set('views', __dirname + '/views');
          app.set('view engine', 'ejs');
          app.use(express.logger());
          app.use(express.methodOverride());
          app.use(cookieParser());
          app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
          app.use(bodyParser.urlencoded({ extended : true }));
          // Initialize Passport!  Also use passport.session() middleware, toosupport
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="c5383-164">마지막으로, 추가해보겠습니다 hello 라우팅합니다 hello 실제 로그인 요청 toohello 해당 전달 `passport-azure-ad` 엔진:</span><span class="sxs-lookup"><span data-stu-id="c5383-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="c5383-165">4 단계: 사용 하 여 Passport tooissue 로그인 및 로그 아웃 요청 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c5383-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="c5383-166">이제 앱이 올바르게 구성 된 toocommunicate hello 끝점과 hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="c5383-167">`passport-azure-ad`가 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 모든 hello 세부 사항을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="c5383-168">나머지 작업에 방식으로 toosign 및 로그 아웃, 사용자 제공 이며 hello 로그인 한 사용자에 대 한 추가 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="c5383-169">첫째, hello 기본, 로그인, 계정 및 로그 아웃 메서드 tooour 추가해보겠습니다 `app.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="c5383-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="c5383-170">자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="c5383-171">hello `/`경로 (있는 경우) hello 사용자 hello 요청에 전달 되는 toohello index.ejs 뷰에서 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="c5383-172">hello `/account` 먼저 라우팅할 *인증 된 것을 보장* (구현 하는 다음 예제는 hello에), 우리 hello 사용자에 대 한 추가 정보를 얻을 수 있도록 전달 hello 요청에 사용자 hello 다음 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="c5383-173">hello `/login` 우리의 azure ad openidconnect 인증자를 호출 하는 경로 `passport-azuread`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="c5383-174">성공 하지 않는 hello 사용자 백 너무/로그인 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="c5383-175">hello `/logout` 경로 hello logout.ejs (및 경로)는 지웁니다 쿠키를 시킨 다음 반환 hello 사용자 백 tooindex.ejs 단순히 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="c5383-176">Hello의 마지막 부분에 대 한 `app.js`, hello를 추가 하겠습니다. **EnsureAuthenticated** 에 사용 되는 방법과 `/account`앞에 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="c5383-177">마지막으로, 만들겠습니다 hello 서버 자체에서 `app.js`:</span><span class="sxs-lookup"><span data-stu-id="c5383-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="c5383-178">5 단계: toodisplay hello 웹 사이트에서 사용자 만들기 hello 뷰와 경로 Express에서</span><span class="sxs-lookup"><span data-stu-id="c5383-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="c5383-179">이제 `app.js`가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-179">Now `app.js` is complete.</span></span> <span data-ttu-id="c5383-180">단순히 tooadd hello 경로 및 필요 hello 정보를 보여 주는 것 toohello 사용자 가져오기으로 hello 처리 뷰 `/logout` 및 `/login` 만든 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="c5383-181">Hello 만들기 `/routes/index.js` hello 루트 디렉터리 아래 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="c5383-182">Hello 만들기 `/routes/user.js` hello 루트 디렉터리 아래 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="c5383-183">이러한 hello 요청 tooour 뷰, 있는 경우에 hello 사용자를 포함 하 여 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="c5383-184">Hello 만들기 `/views/index.ejs` hello 루트 디렉터리 아래에 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="c5383-185">이 로그인 및 로그 아웃 메서드를 호출 하는 간단한 페이지 하 고 us toograb 계정 정보를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="c5383-186">사용할 수는 hello 조건부 `if (!user)` hello 요청에 통과 하는 hello 사용자가 로그인 한 사용자 한 증명 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. <span data-ttu-id="c5383-187">Hello 만들기 `/views/account.ejs` 추가 정보를 볼 수 있도록 hello 루트 디렉터리 아래 보기는 `passport-azuread` 이 hello 사용자 요청에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. <span data-ttu-id="c5383-188">레이아웃을 추가하여 모양을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="c5383-189">Hello 만들기 ' hello 아래 views/layout.ejs' 보기 루트 디렉터리 /.</span><span class="sxs-lookup"><span data-stu-id="c5383-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a><span data-ttu-id="c5383-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5383-190">Next steps</span></span>
<span data-ttu-id="c5383-191">마지막으로 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-191">Finally, build and run your app.</span></span> <span data-ttu-id="c5383-192">실행 `node app.js`, 한 다음 너무 이동`http://localhost:3000`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="c5383-193">개인 Microsoft 계정 또는 회사 또는 학교 계정으로 로그인 하 고 hello 사용자의 id hello /account 목록에 어떻게 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="c5383-194">이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜로 웹앱이 보안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="c5383-195">참조용으로 hello 완료 (구성 값) 없이 샘플 [.zip 파일로 제공](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="c5383-196">또한 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="c5383-197">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="c5383-198">Tootry를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5383-198">You might want tootry:</span></span>

[<span data-ttu-id="c5383-199">Azure AD를 사용하여 Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="c5383-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
