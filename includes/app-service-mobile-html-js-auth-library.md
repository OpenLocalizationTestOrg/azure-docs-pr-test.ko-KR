### <a name="server-auth"></a>방법: 공급자를 사용하여 인증(서버 흐름)
toohave 모바일 앱 관리 응용 프로그램에서 인증 프로세스 hello, id 공급자와 앱을 등록 해야 합니다. 다음 Azure 앱 서비스에 필요한 tooconfigure hello 응용 프로그램 ID 및 공급자가 제공 하는 암호입니다.
자세한 내용은 hello 자습서를 참조 하십시오. [추가 인증 tooyour 앱](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md)합니다.

Id 공급자를 등록 하면 호출 hello `.login()` 공급자의 hello 이름의 메서드. 예를 들어 Facebook과 toologin 코드 다음 hello를 사용 합니다.

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

hello 공급자에 대 한 유효한 값 hello 'aad', 'facebook', 'google', 'microsoftaccount' 및 'twitter' 됩니다.

> [!NOTE]
> Google 인증은 서버 흐름을 통해 현재 작동하지 않습니다.  사용 해야 google tooauthenticate는 [클라이언트 흐름 메서드](#client-auth)합니다.

이 경우 Azure 앱 서비스는 hello OAuth 2.0 인증 흐름을 관리합니다.  Hello 선택한 공급자의 hello 로그인 페이지를 표시 하 고 hello id 공급자와 성공적으로 로그인 한 후 앱 서비스 인증 토큰을 생성 합니다. hello 로그인 함수 완료 되 면 hello 사용자 ID와 응용 프로그램 서비스를 노출 하는 JSON 개체로 인증 토큰 hello userId 및 authenticationToken 필드에 각각 반환 합니다. 이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.

###<a name="client-auth"></a>방법: 공급자를 사용하여 인증(클라이언트 흐름)

앱 수 hello id 공급자에 게 문의 독립적으로 하 고 hello 토큰 tooyour 앱 서비스 인증에 대 한 반환을 제공 합니다. 이 클라이언트 흐름 tooprovide를 사용자나 hello id 공급자 로부터 tooretrieve 추가 사용자 데이터에 대 한 단일 로그인 환경이 있습니다.

#### <a name="social-authentication-basic-example"></a>소셜 인증 기본 예제

이 예제에서는 인증을 위해 Facebook 클라이언트 SDK를 사용합니다.

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
이 예에서는 hello 토큰 변수에 저장 됨 SDK hello 해당 공급자가 제공 hello 토큰을 가정 합니다.

#### <a name="microsoft-account-example"></a>Microsoft 계정 예제

다음 예제에서는 hello Microsoft 계정을 사용 하 여 단일 로그온 Windows 스토어 앱에 대 한 지원 라이브 SDK hello:

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

이 예제에서는 토큰을 가져옵니다 Live Connect에서 hello 로그인 함수를 호출 하 여 제공 된 tooyour 앱 서비스는.

###<a name="auth-getinfo"></a>방법: hello 인증 된 사용자에 대 한 정보

hello에서 hello 인증 정보를 검색할 수 `/.auth/me` AJAX 라이브러리를 사용 하 여 HTTP를 사용 하 여 끝점 호출 합니다.  Hello 설정 확인 `X-ZUMO-AUTH` 헤더 tooyour 인증 토큰입니다.  hello 인증 토큰에 저장 된 `client.currentUser.mobileServiceAuthenticationToken`합니다.  예를 들어 toouse hello 인출 API:

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

fetch는 [npm 패키지](https://www.npmjs.com/package/whatwg-fetch)로 제공되거나 [CDNJS](https://cdnjs.com/libraries/fetch)에서 브라우저 다운로드할 수 있습니다. JQuery 또는 다른 AJAX API toofetch hello 정보 사용할 수 있습니다.  데이터는 JSON 개체로 수신됩니다.
