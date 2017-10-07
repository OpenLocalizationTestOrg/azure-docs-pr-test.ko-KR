---
title: "시작 하는 AD Node.js aaaAzure | Microsoft Docs"
description: "어떻게 toobuild Node.js REST 웹 API는 Azure AD와 통합 인증에 대 한 합니다."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Node.js용 web API 시작
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* 는 Node.js에 대한 인증 미들웨어입니다. 유동 및 모듈형, Passport tooany에 프로그램과 원활 하 게 삭제 될 수 있습니다 Express 기반 웹 응용 프로그램 Restify 또는 합니다. 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다. Microsoft는 Microsoft Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다. 이 모듈을 설치 하 고 다음 Microsoft Azure Active Directory hello 추가 `passport-azure-ad` 플러그 인 합니다.

toodo이를 해야 합니다.

1. Azure AD에 응용 프로그램을 등록합니다.
2. 사용자 응용 프로그램 toouse Passport의 설정 `passport-azure-ad` 플러그 인 합니다.
3. 클라이언트 응용 프로그램 toocall hello tooDo 목록 web API를 구성 합니다.

이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/Azure-Samples/active-directory-node-webapi)합니다.

> [!NOTE]
> 어떻게 tooimplement 로그인이 문서에서 다루지 않는, 등록 하거나 Azure AD B2C를 사용 하 여 관리 프로 파일링 합니다. Hello 사용자가 이미 인증 된 후 호출 웹 Api에 집중 합니다.  로 시작 하는 것이 좋습니다 [어떻게 Azure Active Directory 문서와 toointegrate](active-directory-how-to-integrate.md) 에 대 한 Azure Active Directory의 hello 기본 toolearn 합니다.
>
>

무료 tooclone (또는 더 좋은 포크), 그러니까 MIT 라이선스에 따라 GitHub에서 실행 중인이 예제에 대 한 모든 hello 소스 코드 공개 하 고 피드백을 제공 하 고 끌어오기 요청 합니다.

## <a name="about-nodejs-modules"></a>Node.js 모듈 정보
이 연습에서는 Node.js 모듈을 사용합니다. 모듈은 응용 프로그램의 특정 기능을 제공하는 로드 가능한 JavaScript 패키지입니다. 일반적으로 hello NPM 설치 디렉터리에 hello Node.js NPM 명령줄 도구를 사용 하 여 모듈을 설치 합니다. 그러나 hello HTTP 모듈과 같은 일부 모듈 hello 핵심 Node.js 패키지에 포함 됩니다.

Hello에 설치 된 모듈은 저장 **node_modules** Node.js 설치 디렉터리의 hello 루트 디렉터리입니다. 각 모듈 hello에 **node_modules** 디렉터리 자체 유지 **node_modules** 의존 하는 모든 모듈을 포함 하는 디렉터리입니다. 또한 각 필수 모듈에는 **node_modules** 디렉터리가 있습니다. 이 재귀 디렉터리 구조는 hello 종속성 체인을 나타냅니다.

이와 같은 종속성 체인 구조로 인해 응용 프로그램 공간이 커집니다. 하지만 모든 종속성이 충족 되 고 hello 모듈의 개발에 사용 되는 해당 hello 버전은 프로덕션 환경에서 사용도 또한 보장 합니다. 이 옵션 hello 프로덕션 응용 프로그램 동작을 예측 가능성이 더욱 뛰어난 되며 사용자가 영향을 줄 수 있는 버전 문제를 방지 합니다.

## <a name="step-1-register-an-azure-ad-tenant"></a>1단계: Azure AD 등록
이 샘플 toouse, Azure Active Directory 테 넌 트가 필요 합니다. 확실 하지 않은 경우 어떤 테 넌 트 되었거나 tooget 하나를 확인 하려면 어떻게 해야 [tooget는 Azure AD 테 넌 트](active-directory-howto-tenant.md)합니다.

## <a name="step-2-create-an-application"></a>2단계: 응용 프로그램 만들기
다음 앱 통신할 필요 하다 고 toosecurely 한 정보를 제공 Azure AD 디렉터리에 응용 프로그램을 만듭니다.  Hello 클라이언트 응용 프로그램 및 web API 둘 다 단일 나타내는 **응용 프로그램 ID** 이 경우 하나의 논리 앱 구성 되므로 합니다.  응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-how-applications-are-added.md)합니다. 기간 업무 앱을 빌드하는 경우 [이 추가 지침이 유용할 수 있습니다](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate 응용 프로그램:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 위쪽 메뉴에서 계정을 선택 합니다. 그런 다음 hello **디렉터리** 목록 tooregister 원하는 hello Active Directory 테 넌 트 응용 프로그램을 선택 합니다.

3. Hello hello 왼쪽 메뉴에서 선택 **더 서비스**를 선택한 후 **Azure Active Directory**합니다.

4. **앱 등록**을 선택하고 **추가**를 선택합니다.

5. Hello 프롬프트 toocreate에 따라 한 **웹 응용 프로그램 및/또는 WebAPI**합니다.

      * hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend 사용자에 설명 합니다.

      * hello **로그온 URL** hello 응용 프로그램의 기본 URL입니다.  기본 URL의 hello 샘플 코드는 hello `https://localhost:8080`합니다.

6. 등록 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다. 이 값이 필요한 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 페이지.

7. Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다. hello **앱 ID URI** 응용 프로그램에 대 한 고유 식별자입니다. hello 규칙은 toouse `https://<tenant-domain>/<app-name>`예를 들면: `https://contoso.onmicrosoft.com/my-first-aad-app`합니다.

8. 만들기는 **키** hello에서 응용 프로그램에 대 한 **설정** 페이지를 선택한 다음 위치에 복사 합니다. 곧 이 키가 필요합니다.

## <a name="step-3-download-nodejs-for-your-platform"></a>3단계: 사용자 플랫폼을 위한 Node.js 다운로드
이 샘플을 사용 하는 toosuccessfully Node.js 설치 중인 있어야 합니다.

[http://nodejs.org](http://nodejs.org)에서 Node.js를 설치합니다.

## <a name="step-4-install-mongodb-on-your-platform"></a>4단계: 플랫폼에 MongoDB 설치
이 샘플을 사용 하는 toosuccessfully MongoDB 설치 되어 작동 있어야 합니다. MongoDB toomake hello 영구 REST API를 사용 하 여 여러 서버 인스턴스에 있습니다.

[http://mongodb.org](http://www.mongodb.org)에서 MongoDB를 설치합니다.

> [!NOTE]
> 이 연습에서는 사용 하는 hello 기본 설치 및 서버 끝점, MongoDB에 대 한이 문서 작성 시 hello mongodb://localhost 변수인 가정 합니다.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>5 단계: web API에에서 hello Restify 모듈을 설치
사용 하 여 Restify toobuild REST API입니다. Restify는 Express에서 파생된 작고 유연한 Node.js 응용 프로그램 프레임워크입니다. Connect 위에 REST API를 구축하기 위한 강력한 기능 집합을 포함합니다.

### <a name="install-restify"></a>Restify 설치
1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 디렉터리입니다. 경우 hello **azure ad** 디렉터리 존재 하지 않거나, 만들지 않습니다.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Hello 다음 명령을 입력 합니다.

    `npm install restify`

    이 명령은 Restify를 설치합니다.

#### <a name="did-you-get-an-error"></a>오류가 발생했나요?
일부 운영 체제에서 NPM 매개 변수를 사용하면 **오류: EPERM, chmod '/usr/local/bin/..'** 오류 메시지와 및 관리자 권한으로 실행 중인 hello 계정을 시도 하면 오류입니다. 이 경우 더 높은 권한 수준 hello sudo 명령 toorun NPM을 사용 합니다.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>DTRACE 관련 오류가 발생했나요?
Restify를 설치할 때 다음과 같은 오류가 발생할 수 있습니다.

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```
Restify는 DTrace를 사용하여 REST 호출을 추적하는 강력한 메커니즘을 제공합니다. 그러나 DTrace가 없는 운영 체제가 많습니다. 이러한 오류는 무시해도 됩니다.

hello이이 명령의 출력에 출력 뒤 비슷한 toohello 같아야 합니다.

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a>6단계: web API에 Passport.js 설치
[Passport](http://passportjs.org/) 는 Node.js에 대한 인증 미들웨어입니다. 유동 및 모듈형, Passport tooany에 프로그램과 원활 하 게 삭제 될 수 있습니다 Express 기반 웹 응용 프로그램 Restify 또는 합니다. 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.

Microsoft는 Azure Active Directory에 대한 전략을 개발했습니다. 이 모듈을 설치 하 고 hello Azure Active Directory 전략 플러그 인을 추가 합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 디렉터리입니다.

2. tooinstall passport.js hello 다음 명령을 입력 합니다.

    `npm install passport`

    hello 명령의 hello 출력 비슷한 toohello 다음과 같아야 합니다.

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>7 단계: Passport Azure AD tooyour 웹 API 추가
다음 OAuth 전략 hello를 사용 하 여 추가 `passport-azure-ad`, Azure Active Directory tooPassport 연결 하는 전략의 모음입니다. 이 REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.

> [!NOTE]
> OAuth2는 알려진 모든 토큰 유형을 발급할 수 있는 프레임워크를 제공하지만 일반적으로 특정 토큰 유형만 사용됩니다. 전달자 토큰은 끝점을 보호 하는 데 가장 일반적으로 사용 하는 hello 토큰입니다. OAuth2 토큰의 유형 hello 가장 광범위 하 게 실행 됩니다. 여러 구현 hello 유형의 발급 된 토큰을 전달자 토큰 가정 합니다.
>
>

Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 디렉터리입니다.

형식 hello 다음 명령은 tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

hello hello 명령의 출력에 출력 뒤 비슷한 toohello 같아야 합니다.


    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>8 단계: MongoDB 모듈 tooyour 웹 API에 추가
데이터 저장소로 MongoDB를 사용하겠습니다. 이런 이유로 tooinstall 필요 hello 널리 사용 되는 플러그 인 호출된 Mongoose toomanage 모델 및 스키마입니다. 또한 tooinstall hello 데이터베이스 드라이버 (라고도 하는 MongoDB) MongoDB에 대 한 필요 합니다.

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>9단계: 추가 모듈 설치
그런 다음 필요한 모듈을 남은 hello를 설치 합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. 이러한 모듈의 명령을 tooinstall 다음 hello 입력 프로그램 **node_modules** 디렉터리:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>10단계: 종속성을 적용하여 server.js 만들기
hello server.js 파일 API 웹 서버에 대 한 대부분의 hello 기능을 제공합니다. 대부분의 코드 toothis 파일의 추가합니다. 프로덕션 환경에 대 한 별도 경로 및 컨트롤러와 같은 더 작은 파일로 hello 기능을 리팩터링 하는 것이 좋습니다. 이 데모에서는 이 기능에 server.js를 사용합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. 만들기는 `server.js` 선호 하는 편집기에서 파일을 다음 hello 다음 정보를 추가 합니다.

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Hello 파일을 저장 합니다. 에서는 tooit 곧 반환 합니다.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>11 단계: Azure AD 설정을 구성 파일 toostore 만들
이 코드 파일에서 Azure Active Directory 포털 tooPassport.js hello 구성 매개 변수를 전달합니다. Hello 연습의 첫 번째 부분 hello hello 웹 API toohello 포털을 추가 했을 때 이러한 구성 값을 생성 합니다. Hello 코드를 복사한 후 hello 값이 매개이 변수 중에서 어떤 tooput을 설명 합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. 만들기는 `config.js` 선호 하는 편집기에서 파일을 다음 hello 다음 정보를 추가 합니다.

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Hello 파일을 저장 합니다.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>12 단계: 구성 값 tooyour server.js 파일 추가
이 값이 필요 tooread 이러한 만든 hello.config 파일에서 응용 프로그램에서 합니다. toodo이 응용 프로그램의 hello.config 파일을 필요한 리소스로 추가 합니다. 그런 다음 hello config.js 문서의 hello 전역 변수 toomatch hello 변수를 설정 했습니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. Open 프로그램 `server.js` 선호 하는 편집기에서 파일을 다음 hello 다음 정보를 추가 합니다.

    ```Javascript
    var config = require('./config');
    ```
3. 그런 다음 새 섹션을 너무 추가`server.js` 코드 다음 hello로:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Hello 파일을 저장 합니다.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>13 단계: Mongoose를 사용 하 여 hello MongoDB 모델 및 스키마 정보 추가
이제 이러한 모든 준비를 REST API 서비스에이 세 파일 조합으로 지불 toostart를 하려고 합니다.

이 연습 4 단계에서에서 설명한 대로 작업 MongoDB toostore 사용 했습니다.

Hello에 `config.js` 파일 11 단계에서에서 만든, 데이터베이스 호출 `tasklist`기 때문에 해당 hello 끝에 넣을까요, 우리의 **mogoose_auth_local** 연결 URL입니다. 이 데이터베이스 MongoDB에 미리 toocreate 필요 없습니다. 대신, MongoDB이을 수행해 줍니다 hello에 먼저 만듭니다 (해당 hello 데이터베이스는 존재 하지 않는 것으로 가정) 서버 응용 프로그램의 실행 합니다.

MongoDB 데이터베이스 hello 서버 말씀 했습니다 했으므로 toouse 같은, toowrite 몇 가지 추가 코드 toocreate hello 모델 및 스키마에 필요한 대로 서버 작업입니다.

### <a name="discussion-of-hello-model"></a>Hello 모델에 대 한 설명
Microsoft의 스키마 모델은 간단합니다. 필요에 따라 확장할 수 있습니다.

이름: hello toohello 작업 배정 된 hello 사용자의 이름입니다. **문자열**입니다.

작업: hello 작업 자체입니다. **문자열**입니다.

Hello 작업이 만료 되 날짜: hello 날짜입니다. **DATETIME**입니다.

완료: hello 작업이 고 요약 작업이 완료 되었는지 여부 여부. **부울**입니다.

### <a name="creating-hello-schema-in-hello-code"></a>Hello 코드에서 hello 스키마 만들기
1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. Open 프로그램 `server.js` 선호 하는 편집기에서 파일을 다음 hello 다음 hello 구성 항목 아래에 정보를 추가 합니다.

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
Hello 코드에서 있음 스키마 먼저 만듭니다. Toostore hello 전체에서 데이터 정의 하면 코드에서 사용 하는 모델 개체를 생성 한 다음 우리의 **경로**합니다.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>14단계: Task REST API 서버에 대한 경로 추가
와 데이터베이스 모델 toowork 았는 REST API 서버 계속 사용 하는 hello 경로 추가 해 보겠습니다.

### <a name="about-routes-in-restify"></a>Restify의 경로 정보
경로 동일 하 게 작동 Restify hello에 방식으로 수행 hello Express에에서 쌓입니다. Hello hello 클라이언트 응용 프로그램 toocall 예상 되는 URI를 사용 하 여 경로 정의 합니다. 일반적으로 경로는 별도 파일에 정의합니다. 여기서 hello server.js 파일에이 경로 넣습니다. 프로덕션 사용을 위해서는 자체 파일에서 이러한 경로를 팩터링하는 것이 좋습니다.

Restify 경로의 일반적인 패턴은 다음과 같습니다.

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


가장 기본적인 수준에서 hello 패턴입니다. Resitfy(및 Express)는 응용 프로그램 유형을 정의하고, 여러 끝점에 복잡한 라우팅을 제공하는 등 훨씬 수준 높은 기능을 제공합니다. 여기서는 이러한 경로를 간단하게 유지하겠습니다.

### <a name="add-default-routes-tooour-server"></a>기본 경로 tooour 서버 추가
에서는 이제 hello 만들기, 검색, 업데이트의 기본 CRUD 경로 추가 및 삭제 합니다.

1. Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

    `cd azuread`

2. 열기 hello `server.js` 선호 하는 편집기에서 파일을 다음 hello 다음 hello 이전 데이터베이스 항목을 변경한 아래 정보를 추가 합니다.

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}

```

### <a name="add-error-handling-in-our-apis"></a>API에서 오류 처리 추가
```

///--- Errors for communicating something interesting back toohello client.

function MissingTaskError() {
    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'MissingTask',
        message: '"task" is a required parameter',
        constructorOpt: MissingTaskError
    });

    this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);


function TaskExistsError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'TaskExists',
        message: owner + ' already exists',
        constructorOpt: TaskExistsError
    });

    this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);


function TaskNotFoundError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 404,
        restCode: 'TaskNotFound',
        message: owner + ' was not found',
        constructorOpt: TaskNotFoundError
    });

    this.name = 'TaskNotFoundError';
}

util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="step-15-create-your-server"></a>15단계: 서버 만들기
데이터베이스를 정의했으며 경로가 정위치에 있습니다. 마지막 일 toodo hello 대 한 호출을 관리 하는 hello 서버 인스턴스를 추가 됩니다.

Restify (및 Express) REST API 서버에 대 한 사용자 지정의 많은 할 수 있는 있지만 다시 하겠습니다 toouse hello 가장 기본적인 설치 가이드입니다.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>16 단계: 지금은 인증) (없이 hello 경로 toohello 서버 추가
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>17 단계: OAuth 지원 추가) (이전 hello 서버 실행
인증을 추가하기 전에 서버를 테스트합니다.

가장 쉬운 방법은 tootest hello 서버를 명령줄에서 curl을 사용 합니다. 그 전에 tooparse 출력 JSON 수 있는 유틸리티가 필요 합니다.

1. Hello 다음 JSON 도구 (예제 따르는 모든 hello이이 도구를 사용 하는 데 사용)를 설치 합니다.

    `$npm install -g jsontool`

    이 전역으로 hello JSON 도구를 설치합니다. 완료 한 것, 했으므로 hello 서버와 죠.

2. 먼저 mongoDB 인스턴스가 실행되고 있는지 확인합니다.

    `$sudo mongod`

3. 그런 다음 toohello 디렉터리를 변경 하 고 컬링 시작:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. 그런 다음 다음과 같은 방식으로 작업을 추가할 수 있습니다.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    hello 응답 해야 합니다.

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    또한 다음 방식으로 Brandon에 대한 작업을 나열할 수 있습니다.

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

이 모든가 작동 하는 경우 여러분 준비 tooadd OAuth toohello REST API 서버.

MongoDB를 사용하는 REST API 서버가 완료되었습니다.

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>18 단계: 인증 tooour REST API 서버를 추가 합니다.
이제 REST API가 실행되고 있으니 Azure AD를 사용하여 더욱 유용하게 만들어 보겠습니다.

Hello 명령줄에서 디렉터리 toohello 변경 **azure ad** 폴더 수 없는 경우 이미 있습니다.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Passport azure ad에 포함 되어 있는 OIDCBearerStrategy hello를 사용 하 여
지금까지 권한 부여 없이 일반적인 REST TODO 서버를 빌드했습니다. 이 지점에서 통합 작업을 시작합니다.

1. 먼저 tooindicate toouse Passport 한다고 합니다. 다른 서버 구성 바로 뒤에 이 코드를 추가합니다.

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > 작성 하는 경우, Api 사용자 hello hello 토큰에서 고유한 hello 데이터 toosomething 항상 연결 하는 것이 좋습니다 스푸핑할 수 없습니다. 이 서버는 할 일 항목을 저장 하는 경우 hello "소유자" 필드에 포함 하는 hello 토큰 (token.oid 통해 라고 함)에서 hello 사용자의 hello 개체 ID에 따라 저장 합니다. 이렇게 하면 해당 사용자만 자신의 TODO 항목에 액세스할 수 있습니다. 가 없는 노출 "소유자"의 API hello에 외부 사용자가 인증 되는 경우에 다른 TODOs hello를 요청할 수 있습니다.                    

2. 다음와 함께 제공 되는 hello 전달자 전략 사용 `passport-azure-ad`합니다. 지금은 hello 코드에서을 곧 hello 나머지에 설명 합니다. 위에서 붙여넣은 코드 뒤에 이 코드를 넣습니다.

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport는 모든 전략 작성자가 준수하는 유사한 패턴을 모든 전략(Twitter, Facebook 등)에 대해 사용합니다. 우리는 토큰 및 취소는 포함 된 함수를 변수로 전달할 hello 매개 변수 참조 hello 전략을 보고 합니다. 작업을 수행한 후 hello 전략 toous 다시 제공 됩니다. 이 용어가 들어 후 म 저장 hello 사용자 및 보관 hello 토큰에 대 한 tooask 다시 필요 하지 않습니다.

> [!IMPORTANT]
> 이전 코드 hello tooauthenticate tooour 서버에서 발생 하는 모든 사용자를 사용 합니다. 이를 자동 등록이라고 합니다. 프로덕션 서버에서는 사용자가 결정한 등록 프로세스를 통과하지 않은 사람에게는 액세스를 허용하지 않는 것이 좋습니다. 이 일반적으로 hello 패턴을 사용 하면 Facebook과 tooregister 있지만 다음 toofill 추가 정보를 요청 하는 소비자 앱에 표시 합니다. 명령줄 프로그램을을이 없으면 म 토큰 개체를 반환 하 고 다음 hello 사용자 toofill 추가 정보를 요청 하는 hello에서 hello 전자 메일을 추출 하 고 있을 수 없습니다. 테스트 서버 이기 때문에 여기서 추가 하기만 toohello 메모리 내 데이터베이스입니다.
>
>

### <a name="protect-some-endpoints"></a>일부 끝점 보호
Hello를 지정 하 여 끝점 보호 `passport.authenticate()` toouse 원하는 hello 프로토콜을 사용 하 여 호출 합니다.

서버 코드 않는 무언가 더 흥미로운 toomake hello 경로 편집 하십시오.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>19단계: 서버 응용 프로그램을 다시 실행하고 사용자를 거부하는지 확인
사용해 봅시다 `curl` 이제이 끝점에 대해 OAuth2 보호 사항이 있는 경우 다시 toosee 합니다. 이 끝점에 대해 클라이언트 SDK 중 하나를 실행하기 전에 이 작업을 수행합니다. hello 반환 된 헤더에 있어야 충분 한 tootell hello 오른쪽 경로 아래의 예정 되어 있는 경우 us입니다.

1. 먼저 mongoDB 인스턴스가 실행되고 있는지 확인합니다.

    `$sudo mongod`

2. 그런 다음 toohello 디렉터리를 변경 하 고 컬링 시작 합니다.

      `$ cd azuread` `$ node server.js`

3. 기본 POST를 시도합니다.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401은 원하는 여기 hello 응답입니다. 이 응답 hello Passport 계층 시도 tooredirect 권한이 toohello 끝점의 경우이 수행할 것을 나타냅니다.

## <a name="next-steps"></a>다음 단계
OAuth2 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다. 자세한 연습을 통해 toogo가 필요 합니다.

어떻게 tooimplement REST API를 사용 하 여 Restify 이제 배운 및 OAuth2 합니다. 서비스를 개발 하 고 학습에 충분 한 코드 tookeep 있습니다 어떻게이 예에서 toobuild 합니다.

관심이 있는 경우 hello 다음 단계에서의 ADAL 탐험,으로 계속 작업 하는 것이 좋습니다 몇 가지 지원 되는 ADAL 클라이언트는 다음과 같습니다.

Tooyour 개발자 컴퓨터를 복제 하 한 hello 연습에서 설명 된 대로 구성 합니다.

[iOS용 ADAL(영문)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[Android용 ADAL(영문)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
