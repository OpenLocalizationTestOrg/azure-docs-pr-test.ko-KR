### <span data-ttu-id="ecafa-101"><a name="server-auth"></a>방법: 공급자를 사용하여 인증(서버 흐름)</span><span class="sxs-lookup"><span data-stu-id="ecafa-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="ecafa-102">toohave 모바일 앱 관리 응용 프로그램에서 인증 프로세스 hello, id 공급자와 앱을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="ecafa-103">다음 Azure 앱 서비스에 필요한 tooconfigure hello 응용 프로그램 ID 및 공급자가 제공 하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="ecafa-104">자세한 내용은 hello 자습서를 참조 하십시오. [추가 인증 tooyour 앱](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="ecafa-105">Id 공급자를 등록 하면 호출 hello `.login()` 공급자의 hello 이름의 메서드.</span><span class="sxs-lookup"><span data-stu-id="ecafa-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="ecafa-106">예를 들어 Facebook과 toologin 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="ecafa-107">hello 공급자에 대 한 유효한 값 hello 'aad', 'facebook', 'google', 'microsoftaccount' 및 'twitter' 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="ecafa-108">Google 인증은 서버 흐름을 통해 현재 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="ecafa-109">사용 해야 google tooauthenticate는 [클라이언트 흐름 메서드](#client-auth)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="ecafa-110">이 경우 Azure 앱 서비스는 hello OAuth 2.0 인증 흐름을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="ecafa-111">Hello 선택한 공급자의 hello 로그인 페이지를 표시 하 고 hello id 공급자와 성공적으로 로그인 한 후 앱 서비스 인증 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="ecafa-112">hello 로그인 함수 완료 되 면 hello 사용자 ID와 응용 프로그램 서비스를 노출 하는 JSON 개체로 인증 토큰 hello userId 및 authenticationToken 필드에 각각 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="ecafa-113">이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="ecafa-114"><a name="client-auth"></a>방법: 공급자를 사용하여 인증(클라이언트 흐름)</span><span class="sxs-lookup"><span data-stu-id="ecafa-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="ecafa-115">앱 수 hello id 공급자에 게 문의 독립적으로 하 고 hello 토큰 tooyour 앱 서비스 인증에 대 한 반환을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="ecafa-116">이 클라이언트 흐름 tooprovide를 사용자나 hello id 공급자 로부터 tooretrieve 추가 사용자 데이터에 대 한 단일 로그인 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="ecafa-117">소셜 인증 기본 예제</span><span class="sxs-lookup"><span data-stu-id="ecafa-117">Social Authentication basic example</span></span>

<span data-ttu-id="ecafa-118">이 예제에서는 인증을 위해 Facebook 클라이언트 SDK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="ecafa-119">이 예에서는 hello 토큰 변수에 저장 됨 SDK hello 해당 공급자가 제공 hello 토큰을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="ecafa-120">Microsoft 계정 예제</span><span class="sxs-lookup"><span data-stu-id="ecafa-120">Microsoft Account example</span></span>

<span data-ttu-id="ecafa-121">다음 예제에서는 hello Microsoft 계정을 사용 하 여 단일 로그온 Windows 스토어 앱에 대 한 지원 라이브 SDK hello:</span><span class="sxs-lookup"><span data-stu-id="ecafa-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="ecafa-122">이 예제에서는 토큰을 가져옵니다 Live Connect에서 hello 로그인 함수를 호출 하 여 제공 된 tooyour 앱 서비스는.</span><span class="sxs-lookup"><span data-stu-id="ecafa-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="ecafa-123"><a name="auth-getinfo"></a>방법: hello 인증 된 사용자에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="ecafa-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="ecafa-124">hello에서 hello 인증 정보를 검색할 수 `/.auth/me` AJAX 라이브러리를 사용 하 여 HTTP를 사용 하 여 끝점 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="ecafa-125">Hello 설정 확인 `X-ZUMO-AUTH` 헤더 tooyour 인증 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="ecafa-126">hello 인증 토큰에 저장 된 `client.currentUser.mobileServiceAuthenticationToken`합니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="ecafa-127">예를 들어 toouse hello 인출 API:</span><span class="sxs-lookup"><span data-stu-id="ecafa-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="ecafa-128">fetch는 [npm 패키지](https://www.npmjs.com/package/whatwg-fetch)로 제공되거나 [CDNJS](https://cdnjs.com/libraries/fetch)에서 브라우저 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="ecafa-129">JQuery 또는 다른 AJAX API toofetch hello 정보 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="ecafa-130">데이터는 JSON 개체로 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecafa-130">Data is received as a JSON object.</span></span>
