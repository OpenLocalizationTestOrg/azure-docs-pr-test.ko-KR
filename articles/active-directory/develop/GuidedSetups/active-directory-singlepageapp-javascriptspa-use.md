---
title: "AD aaaAzure v2 JS SPA 단계별 설치 프로그램-사용 | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="59e99-103">Microsoft 인증 라이브러리 (MSAL) toosign-hello 사용자 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59e99-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="59e99-104">`app.js`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-104">Create a file named `app.js`.</span></span> <span data-ttu-id="59e99-105">Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="59e99-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="59e99-106">다음 코드 tooyour hello 추가 `app.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="59e99-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="59e99-107">추가 정보</span><span class="sxs-lookup"><span data-stu-id="59e99-107">More Information</span></span>

<span data-ttu-id="59e99-108">사용자가 hello를 클릭 한 후 *' Microsoft Graph API 호출 '* 처음으로 hello에 대 한 단추 `callGraphApi` 메서드 호출 `loginRedirect` toosign hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="59e99-109">이 방법은 hello 사용자 toohello 리디렉션 *Microsoft Azure Active Directory v2 끝점* tooprompt hello 사용자의 자격 증명의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="59e99-110">성공적으로 로그인을 결과로 hello 사용자가 원래 리디렉션된 백 toohello *index.html* 페이지 및 토큰을 받으면에서 처리 `msal.js` hello 토큰에 포함 된 hello 정보가 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="59e99-111">이 토큰 hello 라고 *ID 토큰* hello 사용자 표시 이름 같은 hello 사용자에 대 한 기본 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="59e99-112">Toouse 하려는 경우 모든 데이터 제공 해야이 토큰은 토큰 hello 하 여 백 엔드 서버 tooguarantee 여 유효성이 검사 되었는지 toomake 목적이 토큰으로 실행 되었습니다 tooa 응용 프로그램에 대 한 유효한 사용자.</span><span class="sxs-lookup"><span data-stu-id="59e99-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="59e99-113">이 가이드에 의해 생성 된 SPA hello 미치지 않으며 hello ID 토큰의 직접 사용 하 여 – 대신 호출 `acquireTokenSilent` 및/또는 `acquireTokenRedirect` tooacquire는 *액세스 토큰* tooquery hello Microsoft Graph API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="59e99-114">Hello ID 토큰의 유효성을 검사 하는 샘플 해야 할 경우에 대해 살펴봅니다 [이](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 샘플") github-예제 응용 프로그램 hello 샘플 사용 토큰 유효성 검사는 ASP.NET 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="59e99-115">대화형으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="59e99-115">Getting a user token interactively</span></span>

<span data-ttu-id="59e99-116">Hello 후 초기 로그인, hello를 원하지 않는 요청 사용자 tooreauthenticate toorequest 필요할 때마다 토큰 tooaccess 리소스 – 따라서 *acquireTokenSilent* 해야 hello 시간 tooacquire 토큰의 대부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="59e99-117">그러나 경우에 tooforce 사용자가 Azure Active Directory v2 끝점 – 상호 작용 해야 하는 몇 가지 예로:</span><span class="sxs-lookup"><span data-stu-id="59e99-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="59e99-118">사용자가 할 수 tooreenter 자격 증명 hello 암호 만료 되었기 때문에</span><span class="sxs-lookup"><span data-stu-id="59e99-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="59e99-119">사용자 요구 tooconsent hello 액세스 tooa 리소스를 요청 하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="59e99-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="59e99-120">2단계 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-120">Two factor authentication is required</span></span>

<span data-ttu-id="59e99-121">호출 hello *acquireTokenRedirect(scope)* 사용자가 Azure Active Directory v2 toohello 끝점 리디렉션에 (또는 *acquireTokenPopup(scope)* 팝업 창에 결과) 필요한 확인 하 여 두 자격 증명을 제공 hello 동의 toohello와 toointeract 리소스 또는 완료 hello 2 단계 인증에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="59e99-122">자동으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="59e99-122">Getting a user token silently</span></span>
<span data-ttu-id="59e99-123">hello ` acquireTokenSilent` 토큰 획득 및 갱신 사용자 상호 작용 없이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="59e99-124">후 `loginRedirect` (또는 `loginPopup`) 처음으로 hello에 대 한 실행 `acquireTokenSilent` hello 일반적으로 사용 되는 방법 tooobtain 사용 되는 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="59e99-125">`acquireTokenSilent`수 실패할 경우에 따라-예를 들어 hello 사용자의 암호가 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="59e99-126">응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="59e99-127">너무 호출할`acquireTokenRedirect` 즉시 메시지를 표시에서 발생 하는 hello에 대 한 사용자 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="59e99-128">이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 hello 응용 프로그램 사용 가능한 toohello 사용자의 인증 되지 않은 콘텐츠가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="59e99-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="59e99-129">이 단계별된 설치 프로그램에 의해 생성 된 hello 예제는이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="59e99-130">응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `acquireTokenSilent` 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="59e99-131">이 일반적으로 hello 사용자 중단 되지 않고 hello 응용 프로그램의 다른 기능을 사용할 수 있습니다-예를 들어 인증 되지 않은 콘텐츠가 없으면 hello 응용 프로그램에서 사용할 수 있는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="59e99-132">이 경우 hello 사용자 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보 오래 된 경우를 결정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="59e99-133">얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="59e99-134">다음 코드 tooyour hello 추가 `app.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="59e99-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="59e99-135">보호되는 API에 대한 REST 호출에 관한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="59e99-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="59e99-136">이 가이드에서 만든 hello 예제 응용 프로그램에서는 hello `callWebApiWithToken()` 메서드는 사용 되는 toomake HTTP `GET` 토큰 한 후 hello 콘텐츠 toohello 호출자를 요구 하는 보호 된 리소스에 대 한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="59e99-137">이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="59e99-138">이 가이드에서 만든 hello 샘플 응용 프로그램에서는 hello 리소스는 hello Microsoft Graph API *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e99-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="59e99-139">Hello 사용자 아웃 메서드 toosign 추가</span><span class="sxs-lookup"><span data-stu-id="59e99-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="59e99-140">다음 코드 tooyour hello 추가 `app.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="59e99-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
