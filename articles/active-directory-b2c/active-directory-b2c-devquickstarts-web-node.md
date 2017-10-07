---
title: "aaaAdd 로그인 tooa Node.js 웹 응용 프로그램에 대 한 Azure B2C | Microsoft Docs"
description: "어떻게 toobuild는 Node.js 웹 B2C 테 넌 트를 사용 하 여 사용자가 로그인 하는 응용 프로그램입니다."
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
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C: 로그인 tooa Node.js 웹 응용 프로그램 추가

**Passport** 는 Node.js에 대한 인증 미들웨어입니다. 매우 유연한 모듈식 Passport는 어떤 Express 기반 또는 Resitify 웹 응용 프로그램에도 원활하게 설치할 수 있습니다. 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.

Microsoft는 Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다. 이 모듈을 설치 하 고 다음 hello Azure AD 추가 `passport-azure-ad` 플러그 인 합니다.

toodo이를 해야 합니다.

1. Azure AD를 사용하여 응용 프로그램을 등록합니다.
2. 응용 프로그램 toouse hello 설정 `passport-azure-ad` 플러그 인 합니다.
3. Passport tooissue 로그인 및 로그 아웃 요청 tooAzure AD 사용 합니다.
4. 사용자 데이터를 인쇄합니다.

이 자습서에 대 한 코드를 hello [GitHub에서 유지 관리 됩니다](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS)합니다. 수에 따라 toofollow, [hello 응용 프로그램의 구조를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip)합니다. Hello 구조를 복제할 수 있습니다.

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

완료 하는 hello 응용 프로그램은이 자습서의 hello 끝에 제공 됩니다.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 가져오기

Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.  디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.

## <a name="create-an-application"></a>응용 프로그램 만들기

다음으로 응용 프로그램 toocreate B2C 디렉터리에 있어야합니다. 이렇게 하면 Azure AD 필요한 정보를 안전 하 게 응용 프로그램과 함께 toocommunicate 있습니다. 클라이언트 응용 프로그램 둘 다 hello 및 web API는 단일으로 표현 됩니다 **응용 프로그램 ID**하나의 논리 앱 구성 되므로, 합니다. 응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다. 다음을 수행해야 합니다.

- 포함 된 **웹 앱**/**웹 API** hello 응용 프로그램에서 합니다.
- **회신 URL**로 `http://localhost:3000/auth/openid/return`을 입력합니다. 이 코드 샘플에 대 한 hello 기본 URL이 있습니다.
- 응용 프로그램에 **응용 프로그램 암호** 를 만들고 복사합니다. 이 시간은 나중에 필요합니다. 이 값 toobe 필요 함을 참고 [XML 이스케이프](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 사용 하기 전에.
- 복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다. 나중에도 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>정책 만들기

Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. 이 앱은 등록, 로그인 및 Facebook을 사용하여 로그인 등 세 가지 ID 환경을 포함합니다. 필요한 toocreate 각 유형의이 정책은에 설명 된 대로 [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)합니다. 세 가지 정책을 만들 때 다음을 확인합니다.

- Hello 선택 **표시 이름** 및 등록 정책에 등록 기타 특성입니다.
- Hello 선택 **표시 이름** 및 **개체 ID** 모든 정책에 대 한 응용 프로그램 클레임입니다. 물론 다른 클레임을 선택할 수 있습니다.
- 복사 hello **이름** 를 만든 후 각 정책의 합니다. Hello 접두사 있어야 `b2c_1_`합니다.  이러한 정책 이름이 나중에 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

준비 toobuild 하 여 세 가지 정책을 만든 후 응용 프로그램입니다.

Note이 여기서 toouse hello 정책 방금 만든 방법 적용 되지 않습니다. toolearn Azure AD B2C의 정책 작동 방식에 대 한 hello로 시작 [.NET 웹 응용 프로그램 시작 자습서](active-directory-b2c-devquickstarts-web-dotnet.md)합니다.

## <a name="add-prerequisites-tooyour-directory"></a>필수 구성 요소 tooyour 디렉터리 추가

Hello 명령줄에서 수 없는 경우 이미 있는 디렉터리 tooyour 루트 폴더를 변경 합니다. Hello 다음 명령을 실행 합니다.

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

또한 사용 `passport-azure-ad` hello 빠른 시작의 hello 구조에서이 미리 보기에 대 한 합니다.

- `npm install passport-azure-ad`

Hello 라이브러리를 설치 하는 `passport-azure-ad` 에 따라 달라 집니다.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>응용 프로그램 toouse hello Passport Node.js 전략 설정
Hello Express 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 구성 합니다. Passport 사용된 tooissue 로그인 및 로그 아웃 요청, 사용자 세션을 관리 되며 사용자가 다른 여러 작업 중에 대 한 정보를 가져옵니다.

열기 hello `config.js` hello 프로젝트의 hello 루트에서 파일을 hello에 응용 프로그램의 구성 값을 입력 `exports.creds` 섹션.
- `clientID`: hello **응용 프로그램 ID** hello 등록 포털에서 tooyour 응용 프로그램을 할당 합니다.
- `returnURL`: hello **리디렉션 URI** hello 포털에 입력 합니다.
- `tenantName`: 응용 프로그램의 예를 들어 hello 테 넌 트 이름 **contoso.onmicrosoft.com**합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

열기 hello `app.js` hello 프로젝트의 hello 루트에 파일입니다. 다음 호출 tooinvoke hello hello 추가 `OIDCStrategy` 와 함께 제공 되는 전략 `passport-azure-ad`합니다.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

방금 toohandle 로그인 요청을 참조 하는 hello 전략을 사용 합니다.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
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
Passport는 Twitter, Facebook을 포함한 모든 전략에 비슷한 패턴을 사용합니다. 모든 전략 기록기 toothis 패턴을 준수합니다. Hello 전략을 보면 전달 있는지 확인할 수 있습니다는 `function()` 토큰 올려진 및 `done` hello 매개 변수로 합니다. hello 전략의 작업을 모두 수행한 후 tooyou 반환 됩니다. Hello 사용자를 저장 하 고 hello 토큰을 스 태 시에 대 한 다시 tooask를 필요 하지 않습니다.

> [!IMPORTANT]
hello 앞의 코드는 모든 사용자 hello 서버를 인증 합니다. 이는 자동 등록입니다. 프로덕션 서버를 사용할 경우 원하지 toolet 사용자에서를 설정 하는 등록 프로세스를 통해 인스턴스용으로 하지 않는 한 합니다. 소비자 앱에서 이 패턴을 종종 볼 수 있습니다. 이러한 사용 하면 tooregister Facebook을 사용 하 여 있지만 다음 요구 toofill 추가 정보입니다. 응용 프로그램을 샘플, 없으면 전자 메일 주소 반환 되는 hello 토큰 개체에서 추출한 hello 사용자 toofill 추가 정보를 요청할 수 했습니다. 테스트 서버 이기 때문에 단순히 toohello 메모리 내 데이터베이스 사용자 추가 합니다.

로그인 한 사용자의 tookeep 트랙 수 있는 hello 메서드 추가 Passport에 필요 합니다. 여기에는 사용자 정보의 직렬화 및 역직렬화가 포함됩니다.

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Hello 코드 tooload hello Express 엔진을 추가 합니다. Hello 다음을 확인할 수 있습니다을 사용 하 여 hello 기본 `/views` 및 `/routes` Express 제공 하는 패턴입니다.

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
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Hello 추가 `POST` 에 게 전달 하는 경로 hello 실제 로그인 요청 toohello `passport-azure-ad` 엔진:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Passport tooissue 로그인 및 로그 아웃 요청 tooAzure AD 사용 하 여

이제 앱이 올바르게 구성 된 toocommunicate hello v2.0 끝점과 hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다. `passport-azure-ad`가 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 세부 사항을 처리 합니다. 나머지 작업 toogive 사용자에 게는의 방식으로 toosign 및 기호 출력 및 toogather 사용자에 게 로그인이 추가 정보입니다.

첫째, hello 기본, 로그인, 계정 및 로그 아웃 메서드 tooyour 추가 `app.js` 파일:

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
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

tooreview 이러한 방법이 자세히:
- hello `/` 경로 리디렉션합니다 toohello `index.ejs` (있는 경우) hello 사용자 hello 요청에 전달 하 여 보기.
- hello `/account` 경로 인증 되는지 먼저 확인 (이 아래에 대 한 구현 hello). 그러면 hello 사용자에 대 한 추가 정보를 얻을 수 있도록 hello 요청에 hello 사용자를 전달 합니다.
- hello `/login` 경로 호출 hello `azuread-openidconnect` 에서 인증자 `passport-azure-ad`합니다. Hello 경로 hello 사용자 다시를 너무 리디렉션합니다 성공 하지 못한 경우`/login`합니다.
- `/logout`은 단순히 `logout.ejs`(및 해당 경로)를 호출합니다. 이 쿠키를 지우고 다음 반환 hello 사용자에 게 콜백 너무`index.ejs`합니다.


마지막 부분 hello에 대 한 `app.js`, hello 추가 `EnsureAuthenticated` hello에 사용 되는 방법과 `/account` 경로입니다.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

마지막으로, 만듭니다 hello 서버 자체에서 `app.js`합니다.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Hello 뷰 만들기 및 정책에 Express toocall에서 보내는

이제 `app.js`가 완료되었습니다. 하기만 하면 tooadd hello 경로 및 toocall hello 로그인 및 등록 정책을 사용할 수 있는 뷰 됩니다. Hello 처리할 수 수도 `/logout` 및 `/login` 만든 경로입니다.

Hello 만들기 `/routes/index.js` hello 루트 디렉터리 아래 경로입니다.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Hello 만들기 `/routes/user.js` hello 루트 디렉터리 아래 경로입니다.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

이러한 간단한 경로 요청 tooyour 보기와 함께 전달합니다. 이 있는 경우 hello 사용자를 포함 됩니다.

Hello 만들기 `/views/index.ejs` hello 루트 디렉터리 아래에 있는 보기입니다. 로그인 및 로그아웃에 대한 정책을 호출하는 단순한 페이지입니다. 사용할 수 있습니다도 toograb 계정 정보. 조건부 hello를 사용할 수 있습니다 `if (!user)` hello 사용자는 통과 하는 대로 tooprovide 증명 해당 hello 사용자 정보 hello 요청이에 로그인 합니다.

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

Hello 만들기 `/views/account.ejs` 추가 정보를 볼 수 있도록 hello 루트 디렉터리 아래 보기는 `passport-azure-ad` hello 사용자 요청에 배치 합니다.

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

이제 앱을 작성하고 실행합니다.

실행 `node app.js` 너무 이동`http://localhost:3000`


등록 또는 toohello 응용 프로그램에서 전자 메일 또는 Facebook을 사용 하 여 로그인 합니다. 로그아웃했다가 다른 사용자로 다시 로그인합니다.

##<a name="next-steps"></a>다음 단계

참조용으로 hello 완료 (구성 값) 없이 샘플 [.zip 파일로 제공](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip)합니다. 또한 GitHub에서 복제할 수 있습니다.

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

고급 항목 toomore에 이동할 수 있습니다. 다음을 시도해 볼 수 있습니다.

[Node.js에서 hello B2C 모델을 사용 하 여 웹 API 보안](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
