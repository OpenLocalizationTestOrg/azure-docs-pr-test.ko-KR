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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Microsoft 인증 라이브러리 (MSAL) toosign-hello 사용자 hello를 사용 하 여

1.  `app.js`라는 파일을 만듭니다. Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `JavaScript File`:
2.  다음 코드 tooyour hello 추가 `app.js` 파일:

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
### <a name="more-information"></a>추가 정보

사용자가 hello를 클릭 한 후 *' Microsoft Graph API 호출 '* 처음으로 hello에 대 한 단추 `callGraphApi` 메서드 호출 `loginRedirect` toosign hello 사용자 계정입니다. 이 방법은 hello 사용자 toohello 리디렉션 *Microsoft Azure Active Directory v2 끝점* tooprompt hello 사용자의 자격 증명의 유효성을 검사 합니다. 성공적으로 로그인을 결과로 hello 사용자가 원래 리디렉션된 백 toohello *index.html* 페이지 및 토큰을 받으면에서 처리 `msal.js` hello 토큰에 포함 된 hello 정보가 캐시 됩니다. 이 토큰 hello 라고 *ID 토큰* hello 사용자 표시 이름 같은 hello 사용자에 대 한 기본 정보를 포함 합니다. Toouse 하려는 경우 모든 데이터 제공 해야이 토큰은 토큰 hello 하 여 백 엔드 서버 tooguarantee 여 유효성이 검사 되었는지 toomake 목적이 토큰으로 실행 되었습니다 tooa 응용 프로그램에 대 한 유효한 사용자.

이 가이드에 의해 생성 된 SPA hello 미치지 않으며 hello ID 토큰의 직접 사용 하 여 – 대신 호출 `acquireTokenSilent` 및/또는 `acquireTokenRedirect` tooacquire는 *액세스 토큰* tooquery hello Microsoft Graph API를 사용 합니다. Hello ID 토큰의 유효성을 검사 하는 샘플 해야 할 경우에 대해 살펴봅니다 [이](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 샘플") github-예제 응용 프로그램 hello 샘플 사용 토큰 유효성 검사는 ASP.NET 웹 API입니다.

#### <a name="getting-a-user-token-interactively"></a>대화형으로 사용자 토큰 가져오기

Hello 후 초기 로그인, hello를 원하지 않는 요청 사용자 tooreauthenticate toorequest 필요할 때마다 토큰 tooaccess 리소스 – 따라서 *acquireTokenSilent* 해야 hello 시간 tooacquire 토큰의 대부분을 사용 합니다. 그러나 경우에 tooforce 사용자가 Azure Active Directory v2 끝점 – 상호 작용 해야 하는 몇 가지 예로:
-   사용자가 할 수 tooreenter 자격 증명 hello 암호 만료 되었기 때문에
-   사용자 요구 tooconsent hello 액세스 tooa 리소스를 요청 하는 응용 프로그램
-   2단계 인증이 필요합니다.

호출 hello *acquireTokenRedirect(scope)* 사용자가 Azure Active Directory v2 toohello 끝점 리디렉션에 (또는 *acquireTokenPopup(scope)* 팝업 창에 결과) 필요한 확인 하 여 두 자격 증명을 제공 hello 동의 toohello와 toointeract 리소스 또는 완료 hello 2 단계 인증에 필요 합니다.

#### <a name="getting-a-user-token-silently"></a>자동으로 사용자 토큰 가져오기
hello ` acquireTokenSilent` 토큰 획득 및 갱신 사용자 상호 작용 없이 처리 합니다. 후 `loginRedirect` (또는 `loginPopup`) 처음으로 hello에 대 한 실행 `acquireTokenSilent` hello 일반적으로 사용 되는 방법 tooobtain 사용 되는 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.
`acquireTokenSilent`수 실패할 경우에 따라-예를 들어 hello 사용자의 암호가 만료 되었습니다. 응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.

1.  너무 호출할`acquireTokenRedirect` 즉시 메시지를 표시에서 발생 하는 hello에 대 한 사용자 toosign 합니다. 이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 hello 응용 프로그램 사용 가능한 toohello 사용자의 인증 되지 않은 콘텐츠가 없는 경우. 이 단계별된 설치 프로그램에 의해 생성 된 hello 예제는이 패턴을 사용 합니다.

2. 응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `acquireTokenSilent` 나중에 있습니다. 이 일반적으로 hello 사용자 중단 되지 않고 hello 응용 프로그램의 다른 기능을 사용할 수 있습니다-예를 들어 인증 되지 않은 콘텐츠가 없으면 hello 응용 프로그램에서 사용할 수 있는 경우에 사용 됩니다. 이 경우 hello 사용자 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보 오래 된 경우를 결정할 수도 있습니다.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.

다음 코드 tooyour hello 추가 `app.js` 파일:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>보호되는 API에 대한 REST 호출에 관한 추가 정보

이 가이드에서 만든 hello 예제 응용 프로그램에서는 hello `callWebApiWithToken()` 메서드는 사용 되는 toomake HTTP `GET` 토큰 한 후 hello 콘텐츠 toohello 호출자를 요구 하는 보호 된 리소스에 대 한 요청입니다. 이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다. 이 가이드에서 만든 hello 샘플 응용 프로그램에서는 hello 리소스는 hello Microsoft Graph API *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Hello 사용자 아웃 메서드 toosign 추가

다음 코드 tooyour hello 추가 `app.js` 파일:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
