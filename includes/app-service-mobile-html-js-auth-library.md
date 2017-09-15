### <span data-ttu-id="31c40-101"><a name="server-auth"></a>방법: 공급자를 사용하여 인증(서버 흐름)</span><span class="sxs-lookup"><span data-stu-id="31c40-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="31c40-102">Mobile Apps가 앱에서 인증 프로세스를 관리하게 하려면 앱을 ID 공급자에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="31c40-103">그런 다음, Azure 앱 서비스에서 공급자로부터 제공된 응용 프로그램 ID 및 암호를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="31c40-104">자세한 내용은 [앱에 인증 추가](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md)자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31c40-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="31c40-105">ID 공급자를 등록하고 나면 공급자의 이름을 사용하여 `.login()` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="31c40-106">예를 들어 Facebook으로 로그인하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="31c40-107">공급자에 대해 유효한 값은 'aad', 'facebook', 'google', 'microsoftaccount' 및 'twitter'입니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="31c40-108">Google 인증은 서버 흐름을 통해 현재 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="31c40-109">Google을 인증하려면 [클라이언트 흐름 메서드](#client-auth)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="31c40-110">이 경우 Azure App Service는 OAuth 2.0 인증 흐름을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="31c40-111">선택한 공급자의 로그인 페이지가 표시되고 ID 공급자로 성공적으로 로그인한 후에는 App Service 인증 토큰이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="31c40-112">login 함수를 완료하면 사용자 ID와 App Service 인증 토큰을 각각 userId 및 authenticationToken 필드에 표시하는 JSON 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="31c40-113">이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="31c40-114"><a name="client-auth"></a>방법: 공급자를 사용하여 인증(클라이언트 흐름)</span><span class="sxs-lookup"><span data-stu-id="31c40-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="31c40-115">앱이 독립적으로 ID 공급자에 연결한 후 반환된 토큰을 인증을 위해 앱 서비스에 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="31c40-116">이 클라이언트 흐름을 사용하면 단일 로그인 환경을 사용자에게 제공하거나 ID 공급자로부터 더 많은 사용자 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="31c40-117">소셜 인증 기본 예제</span><span class="sxs-lookup"><span data-stu-id="31c40-117">Social Authentication basic example</span></span>

<span data-ttu-id="31c40-118">이 예제에서는 인증을 위해 Facebook 클라이언트 SDK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="31c40-119">이 예제에서는 각 공급자 SDK에서 제공된 토큰이 token 변수에 저장되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="31c40-120">Microsoft 계정 예제</span><span class="sxs-lookup"><span data-stu-id="31c40-120">Microsoft Account example</span></span>

<span data-ttu-id="31c40-121">다음 예제는 Microsoft 계정을 사용하여 Windows 스토어 앱용 Single Sign-On을 지원하는 Live SDK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="31c40-122">이 예제는 login 함수를 호출하여 앱 서비스에 제공된 토큰을 Live Connect에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="31c40-123"><a name="auth-getinfo"></a>방법: 인증된 사용자에 대한 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="31c40-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="31c40-124">모든 AJAX 라이브러리와 함께 HTTP 호출 사용 시 인증 정보를 `/.auth/me` 끝점에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="31c40-125">`X-ZUMO-AUTH` 헤더를 인증 토큰으로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="31c40-126">인증 토큰은 `client.currentUser.mobileServiceAuthenticationToken`에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="31c40-127">예를 들어, fetch API를 사용하려면 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="31c40-128">fetch는 [npm 패키지](https://www.npmjs.com/package/whatwg-fetch)로 제공되거나 [CDNJS](https://cdnjs.com/libraries/fetch)에서 브라우저 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="31c40-129">또한 jQuery 또는 AJAX API를 사용하여 정보를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="31c40-130">데이터는 JSON 개체로 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c40-130">Data is received as a JSON object.</span></span>
