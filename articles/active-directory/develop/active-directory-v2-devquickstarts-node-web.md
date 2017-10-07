---
title: "Node.js 웹 응용 프로그램에 대 한 로그인 aaaAzure Active Directory v2.0 | Microsoft Docs"
description: "어떻게 toobuild는 Node.js 웹 모두 개인 Microsoft 계정 및 회사 또는 학교 계정을 사용 하 여 사용자가 로그인 하는 앱에 알아봅니다."
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
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>로그인 tooa Node.js 웹 응용 프로그램 추가

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용 하십시오. 에 대해 알아보세요 hello v2.0 끝점 또는 hello v1.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 

이 자습서에서는 다음 작업 Passport toodo hello를 사용 합니다.

* 웹 앱에서 Azure Active Directory (Azure AD)를 사용 하 여 hello 사용자를 로그인 하 고 hello v2.0 끝점.
* Hello 사용자에 대 한 정보를 표시 합니다.
* Sign hello hello 앱에서 사용자입니다.

**Passport** 는 Node.js에 대한 인증 미들웨어입니다. 유연한 모듈식 Passport는 어떤 Express 기반 또는 restify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다. Passport에서는 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 또는 기타 옵션을 사용하여 인증을 지원합니다. Microsoft는 Azure AD에 대한 전략을 개발했습니다. 이 문서에서는 보여줍니다 tooinstall 모듈 hello 하 고 다음 hello Azure AD를 추가 하는 방법 `passport-azure-ad` 플러그 인 합니다.

## <a name="download"></a>다운로드
이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs)합니다. 수 toofollow hello 자습서 [hello 응용 프로그램의 구조를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

이 자습서의 hello 끝 완료 hello 응용 프로그램을 가져올 수도 있습니다.

## <a name="1-register-an-app"></a>1: 앱 등록
새 앱 만들기 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 하거나 팔 로우 [자세한 단계는 이러한](active-directory-v2-app-registration.md) tooregister 응용 프로그램입니다. 다음을 확인합니다.

* 복사 hello **응용 프로그램 Id** tooyour 응용 프로그램을 할당 합니다. 이 자습서에 필요합니다.
* Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.
* 복사 hello **리디렉션 URI** hello 포털에서 합니다. Hello URI의 기본값을 사용 해야 `urn:ietf:wg:oauth:2.0:oob`합니다.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: 필수 tooyour 디렉터리 추가
명령 프롬프트에서 디렉터리 toogo tooyour 루트 폴더를 변경할 수 없는 경우 이미 있습니다. Hello 다음 명령을 실행 합니다.

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

또한 사용 `passport-azure-ad` hello 빠른 시작의 hello 기본 정의:

* `npm install passport-azure-ad`

이렇게 하면 hello 라이브러리가 설치 하는 `passport-azure-ad` 사용 합니다.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: 응용 프로그램 toouse hello passport-노드-js 전략 설정
Hello Express 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 설정 합니다. Passport tooissue 로그인 및 로그 아웃 요청을 사용 하 여, 관리 hello 사용자의 세션 하 무엇 보다도 hello 사용자에 대 한 정보를 가져옵니다.

1.  Hello hello 프로젝트의 루트에 있는 hello Config.js 파일을 엽니다. Hello에 `exports.creds` 섹션 응용 프로그램의 구성 값을 입력 합니다.
  
  * `clientID`: hello **응용 프로그램 Id** hello Azure 포털에서에서 할당 된 tooyour 응용 프로그램입니다.
  * `returnURL`: hello **리디렉션 URI** hello 포털에 입력 합니다.
  * `clientSecret`: hello 포털에서 생성 하는 hello 암호입니다.

2.  Hello hello 프로젝트의 루트에 있는 hello App.js 파일을 엽니다. 와 함께 제공 되 tooinvoke hello OIDCStrategy stratey `passport-azure-ad`를 호출한 다음 hello 추가:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle 로그인 요청을 받은 방금 참조 hello 전략을 사용 합니다.

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
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

Passport는 모든 전략(Twitter, Facebook 등)에 유사한 패턴을 사용합니다. 모든 전략 기록기 toohello 패턴을 준수합니다. Hello 전략 전달는 `function()` 토큰을 사용 하 고 `done` 매개 변수로 합니다. hello 전략에는 모든 작업을 수행한 후 반환 됩니다. Hello 사용자 및 보관 hello 토큰 저장에 대 한 tooask 다시 필요 하지 않습니다.

  > [!IMPORTANT]
  > hello 앞의 코드는 tooyour 서버를 인증할 수 있는 모든 사용자 합니다. 이를 자동 등록이라고 합니다. 프로덕션 서버에 원하지 toolet 모든 사용자 선택 하는 등록 프로세스를 통해 이동 하는 첫 번째 필요 없이 합니다. 일반적으로 소비자 앱에서 볼 수 있는 hello 패턴입니다. hello 응용 프로그램 수를 Facebook에 tooregister 허용 하지만 다음 묻는 tooenter 추가 정보. 명령줄 프로그램이 자습서를 사용 하지 않은 경우 반환 되는 hello 토큰 개체에서 hello 전자 메일을 추출할 수 있습니다. 그런 다음 hello 사용자 tooenter 추가 정보를 요청할 수 있습니다. Hello 사용자를 추가 하는 테스트 서버 이기 때문에 직접 toohello 메모리 내 데이터베이스입니다.
  > 
  > 

4.  에서는 로그인 한 사용자의 tookeep 추적을 사용 하는 hello 메서드 추가 Passport에 필요 합니다. 직렬화 및 역직렬화 hello 사용자의 정보가 포함 됩니다.

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  Hello Express 엔진을 로드 하는 hello 코드를 추가 합니다. 기본 /views hello를 사용 하 고 Express /routes 패턴 제공 합니다.

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
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  Hello POST 라우팅합니다 hello 실제 로그인 요청 toohello 해당 전달 추가 `passport-azure-ad` 엔진:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: tooAzure AD 요청을 사용 하 여 Passport tooissue 로그인 및 로그 아웃
응용 프로그램은 이제 hello OpenID Connect 인증 프로토콜을 사용 하 여 hello v2.0 끝점과 toocommunicate를 설정 됩니다. hello `passport-azure-ad` 전략 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 hello 사용자 세션을 유지 관리의 모든 hello 세부 사항을 처리 합니다. Toodo 남아 있는 모든 toogive 사용자에 게는 방식으로 toosign에 및 기호 출력 및 toogather hello 사용자가 로그인에 대 한 자세한 내용은 합니다.

1.  Hello 추가 **기본**, **로그인**, **계정**, 및 **로그 아웃** 메서드 tooyour App.js 파일:

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
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  Hello 세부 정보는 다음과 같습니다.
    
    * hello `/` 경로 toohello index.ejs 보기를 리디렉션합니다. Hello 사용자 (있는 경우) hello 요청에 전달 됩니다.
    * hello `/account` 먼저 라우팅할 *인증 되었음을 보장* (에 구현 하는 코드 다음 hello). 그런 다음 hello 사용자 hello 요청에 전달합니다. 이 hello 사용자에 대 한 자세한 정보를 얻을 수 있도록 합니다.
    * hello `/login` 전화 프로그램 `azuread-openidconnect` 에서 인증자 `passport-azuread`합니다. Hello 사용자에 게 콜백 너무 리디렉션합니다 하에 성공 하지 않는`/login`합니다.
    * hello `/logout` 경로 hello logout.ejs 뷰 (및 경로)를 호출 합니다. 쿠키를 지우고 반환 hello 사용자 백 tooindex.ejs 합니다.

2.  Hello 추가 **EnsureAuthenticated** 에서 이전에 사용한 메서드와 `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  App.js, hello 서버를 만듭니다.

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: hello 웹 사이트에서 사용자에 게 표시 하는 Express에서 경로 및 hello 보기 만들기
Hello 경로 및 toohello 사용자 정보를 표시 하는 뷰를 추가 합니다. 또한 처리 hello hello 경로 및 뷰 `/logout` 및 `/login` 만든 경로입니다.

1. Hello 루트 디렉터리에 만들 hello `/routes/index.js` 경로입니다.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  Hello 루트 디렉터리에 만들 hello `/routes/user.js` 경로입니다.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`및 `/routes/user.js` hello 요청 tooyour 뷰, 있는 경우에 hello 사용자를 포함 하 여 따라 전달 하는 간단한 경로가 있습니다.

3.  Hello 루트 디렉터리에 만들 hello `/views/index.ejs` 보기. 이 페이지는 **로그인** 및 **로그아웃** 메서드를 호출합니다. Hello 사용할 수도 `/views/index.ejs` toocapture 계정 정보를 확인 합니다. 조건부 hello를 사용할 수 있습니다 `if (!user)` hello 요청을 통해 전달 되는 hello 사용자로 합니다. 이는 사용자가 로그인했다는 증거입니다.

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

4.  Hello 루트 디렉터리에 만들 hello `/views/account.ejs` 보기. hello `/views/account.ejs` 보기에서는 tooview 추가 정보는 `passport-azuread` hello 사용자 요청에 넣습니다.

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

5.  레이아웃을 추가합니다. Hello 루트 디렉터리에 만들 hello `/views/layout.ejs` 보기.

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

6.  toobuild 응용 프로그램을 실행 하 고 실행 `node app.js`합니다. 그런 다음 너무 이동`http://localhost:3000`합니다.

7.  개인 Microsoft 계정이나 회사 또는 학교 계정으로 로그인합니다. Note hello 사용자의 id hello /account 목록에 반영 됩니다. 

이제 산업 표준 프로토콜을 사용하여 보호되는 웹앱을 만들었습니다. 앱에서 개인 및 회사 또는 학교 계정을 사용하여 사용자를 인증할 수 있습니다.

## <a name="next-steps"></a>다음 단계
완료 하는 hello 예제 구성 값) (없이 제공 됩니다 참조용으로 [.zip 파일](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip)합니다. GitHub에서 복제할 수도 있습니다.

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

다음으로, 고급 항목 toomore에 이동할 수 있습니다. Tootry를 설정할 수 있습니다.

[Hello v2.0 끝점을 사용 하 여 Node.js web API 보호](active-directory-v2-devquickstarts-node-api.md)

다음은 몇 가지 추가 리소스입니다.

* [Azure AD v2.0 개발자 가이드](active-directory-appmodel-v2-overview.md)
* [Stack Overflow "azure-active-directory" 태그](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기
Toosign을 보안 사고 발생할 때 알림 toobe 사용 하는 것이 좋습니다. Hello에 [Microsoft 기술 보안 알림](https://technet.microsoft.com/security/dd252948) 페이지, tooSecurity 권고 경고를 구독 합니다.

