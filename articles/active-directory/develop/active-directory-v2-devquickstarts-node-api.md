---
title: "Node.js를 사용 하 여 Azure Active Directory v2.0 웹 API aaaSecure | Microsoft Docs"
description: "Toobuild는 Node.js API와 회사 또는 학교 계정을 모두 개인 Microsoft 계정에서 토큰을 수락 하는 웹 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Node.js를 사용하여 웹 API 보안 유지
> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용 하십시오. 에 대해 알아보세요 hello v2.0 끝점 또는 hello v1.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

Hello Azure Active Directory (Azure AD) v 2.0 끝점을 사용 하는 경우 사용할 수 있습니다 [OAuth 2.0](active-directory-v2-protocols.md) 액세스 토큰 tooprotect web API입니다. OAuth 2.0 액세스 토큰을 사용하여 개인 Microsoft 계정 및 작업 또는 학교 계정 모두를 가진 사용자는 웹 API에 안전하게 액세스할 수 있습니다.

*Passport* 는 Node.js에 대한 인증 미들웨어입니다. 유연한 모듈식 Passport는 어떤 Express 기반 또는 restify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다. Passport에서는 포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 또는 기타 옵션을 사용하여 인증을 지원합니다. Microsoft는 Azure AD에 대한 전략을 개발했습니다. 이 문서에서는 보여줍니다 tooinstall 모듈 hello 하 고 다음 hello Azure AD를 추가 하는 방법 `passport-azure-ad` 플러그 인 합니다.

## <a name="download"></a>다운로드
이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)합니다. 수 toofollow hello 자습서 [hello 응용 프로그램의 구조를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), 또는 복제 hello 스 켈 레 톤:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

이 자습서의 hello 끝 완료 hello 응용 프로그램을 가져올 수도 있습니다.

## <a name="1-register-an-app"></a>1: 앱 등록
새 앱 만들기 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 하거나 팔 로우 [자세한 단계는 이러한](active-directory-v2-app-registration.md) tooregister 응용 프로그램입니다. 다음을 확인합니다.

* 복사 hello **응용 프로그램 Id** tooyour 응용 프로그램을 할당 합니다. 이 자습서에 필요합니다.
* Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.
* 복사 hello **리디렉션 URI** hello 포털에서 합니다. Hello URI의 기본값을 사용 해야 `urn:ietf:wg:oauth:2.0:oob`합니다.

## <a name="2-install-nodejs"></a>2: Node.js 설치
이 자습서에 대 한 toouse hello 샘플에서 수행 해야 [Node.js 설치](http://nodejs.org)합니다.

## <a name="3-install-mongodb"></a>3: MongoDB 설치
이 샘플을 사용 하는 toosuccessfully 있으면 [MongoDB 설치](http://www.mongodb.org)합니다. 이 샘플에서 사용 하 여 MongoDB toomake 영구 REST API 서버 인스턴스에서.

> [!NOTE]
> 이 문서에서는 hello 기본 설치 및 서버 끝점을 사용 하 여 MongoDB에 대 한 가정: mongodb://localhost 합니다.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: 설치 hello restify web API의에서 모듈
Resitfy toobuild REST API 사용합니다. Restify는 Express에서 파생된 작고 유연한 Node.js 응용 프로그램 프레임워크입니다. Restify 강력한 toobuild 연결 위에 REST Api를 사용할 수 있는 기능 집합이 있습니다.

### <a name="install-restify"></a>Restify 설치
1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

    경우 hello **azure ad** 디렉터리 존재 하지 않거나, 만들지 않습니다.

    `mkdir azuread`

2.  Restify 설치:

    `npm install restify`

    hello이이 명령의 출력은 다음과 같이 표시 됩니다.

    ```
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
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>오류가 발생했나요?
Hello를 사용 하는 경우 일부 운영 체제에서 `npm` 명령,이 메시지가 표시 될 수 있습니다: `Error: EPERM, chmod '/usr/local/bin/..'`합니다. hello 오류 하면 관리자 권한으로 실행 중인 hello 계정 사용을 시도 하는 요청에 나옵니다. 이 경우 명령을 사용 하 여 hello `sudo` toorun `npm` 더 높은 권한 수준입니다.

#### <a name="did-you-get-an-error-related-toodtrace"></a>관련 오류 어 tooDTrace?
Restify를 설치할 때 이 메시지가 나타날 수 있습니다.

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
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

Restify DTrace를 사용 하 여 REST 호출 강력한 메커니즘 tootrace 했습니다. 그러나 DTrace는 많은 운영 체제에서 사용할 수 없습니다. 이 오류 메시지는 무시해도 됩니다.


## <a name="5-install-passportjs-in-your-web-api"></a>5: 웹 API에 Passport.js 설치
1.  Hello 명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**합니다.

2.  Passport.js 설치:

    `npm install passport`

    hello hello 명령의 출력은 다음과 같이 표시 됩니다.

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: passport azure ad tooyour 웹 API에 추가
그런 다음 passport azure ad를 사용 하 여 hello OAuth 전략을 추가 합니다. `passport-azuread`는 Azure AD를 Passport와 함께 연결하는 전략 제품군입니다. 이 REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.

> [!NOTE]
> OAuth 2.0은 알려진 모든 토큰 유형을 발급할 수 있는 프레임워크를 제공하지만 일반적으로 특정 토큰 유형이 사용됩니다. 전달자 토큰은 자주 사용 되는 tooprotect 끝점입니다. 전달자 토큰은 발급 가장 광범위 하 게 hello 유형의 OAuth 2.0에서 토큰입니다. 많은 OAuth 2.0 구현 전달자 토큰 발급 토큰의 형식만 hello 있다고 간주 합니다.
> 
> 

1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**합니다.

    `cd azuread`

2.  Hello Passport.js 설치 `passport-azure-ad` 모듈:

    `npm install passport-azure-ad`

    hello hello 명령의 출력은 다음과 같이 표시 됩니다.

    ```
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
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: MongoDB 모듈 tooyour 웹 API에 추가
이 샘플에서는 데이터 저장소로 MongoDB를 사용합니다. 

1.  설치 Mongoose 널리 사용 되는 플러그 인, toomanage 모델과 스키마: 

    `npm install mongoose`

2.  MongoDB 라고도 함 MongoDB에 대 한 hello 데이터베이스 드라이버를 설치 합니다.

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8: 추가 모듈 설치
Hello 남은 필요한 모듈을 설치 합니다.

1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  Hello 다음 명령을 입력 합니다. hello 명령을 hello node_modules 디렉터리 모듈에에서 다음을 설치 합니다.

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9: 종속성에 대한 Server.js 파일 만들기
Hello 대부분의 웹 API 서버에 대 한 hello 기능은 Server.js 파일을 보유합니다. 대부분의 코드 toothis 파일에 추가 합니다. 프로덕션 환경에 대 한 별도 경로 및 컨트롤러와 같은 hello 기능을 더 작은 파일로 리팩터링할 수 있습니다. 이 문서에서는 이 목적을 위해 Server.js를 사용합니다.

1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  선택한 편집기를 사용하여 Server.js 파일을 만듭니다. 다음 정보 toohello 파일 hello를 추가 합니다.

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Hello 파일을 저장 합니다. Tooit를 즉시 반환 됩니다.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: config 파일 toostore Azure AD 설정 만들기
이 코드 파일에서 Azure AD 포털 tooPassport.js hello 구성 매개 변수를 전달합니다. Hello 웹 API toohello 포털 hello 문서의 hello 시작 부분에 추가 했을 때 이러한 구성 값을 만들었습니다. Hello 코드를 복사한 후 hello 값이 매개이 변수 중에서 어떤 tooput을 설명 합니다.

1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  편집기에서 Config.js 파일을 만듭니다. Hello 다음 정보를 추가 합니다.

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>필요한 값

*   **IdentityMetadata**: 여기에 `passport-azure-ad` hello IDP (id 공급자) 및 hello 키 toovalidate hello JSON 웹 토큰 (Jwt)에 대 한 구성 데이터를 찾습니다. Azure AD를 사용 하는 경우 원하지 않을 것 toochange이 있습니다.

*   **대상 그룹**: hello 포털에서 리디렉션 URI입니다.

> [!NOTE]
> 키는 자주 롤링됩니다. 항상 hello "openid_keys" URL에서 끌어오도록 하 고 해당 hello 앱 hello 인터넷에 액세스할 수 있어야 합니다.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: hello 구성 tooyour Server.js 파일 추가
응용 프로그램에 방금 만든 hello 구성 파일에서 tooread hello 값 필요 합니다. 응용 프로그램에 필요한 리소스로 hello.config 파일을 추가 합니다. Hello 전역 변수 toothose Config.js에 있는 설정 합니다.

1.  Hello 명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  편집기에서 Server.js를 엽니다. Hello 다음 정보를 추가 합니다.

    ```Javascript
    var config = require('./config');
    ```

3.  새 섹션 tooServer.js를 추가 합니다.

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: Mongoose를 사용 하 여 hello MongoDB 모델 및 스키마 정보를 추가 합니다.
다음으로 REST API 서비스에서 이러한 3개의 파일을 연결합니다.

이 문서에서 사용 하 여 MongoDB toostore 작업 합니다. 이 부분은 *4단계*에서 다룹니다.

11 단계에서 만든 hello Config.js 파일에서 데이터베이스 라고 *tasklist \ / s*합니다. 그건 mongoose_auth_local 연결 URL의 hello 끝에 사용할 항목입니다. 이 데이터베이스 MongoDB에 미리 toocreate 필요 없습니다. hello를 데이터베이스가 만들어집니다 hello 먼저 (hello 데이터베이스가 아직 없는 경우) 서버 응용 프로그램의 실행 합니다.

MongoDB 데이터베이스 toouse 어떤 hello 서버에 지시 받고 했습니다. 다음으로, 해야 toowrite 몇 가지 추가 코드 toocreate hello 모델 및 스키마 서버의 작업에 대 한 합니다.

### <a name="hello-model"></a>hello 모델
hello 스키마 모델은 매우 기본적인입니다. 필요한 경우 확장할 수 있습니다. 

hello 스키마 모델에는 이러한 값은 같습니다.

*   **이름**. hello 사람 toohello 할당 된 작업입니다. **문자열** 값입니다.
*   **작업**. hello 작업의 hello 이름입니다. **문자열** 값입니다.
*   **날짜**. hello 날짜 hello 작업으로 인 한 것입니다. **datetime** 값입니다.
*   **완료됨**. Hello 작업은 완료 되었는지 여부를 나타냅니다. **부울** 값입니다.

### <a name="create-hello-schema-in-hello-code"></a>Hello 코드에서 hello 스키마 만들기
1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  편집기에서 Server.js를 엽니다. Hello 구성 항목 아래에 다음 정보는 hello를 추가 합니다.

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

이 코드 toohello MongoDB 서버에 연결 합니다. 또한 스키마 개체를 반환합니다.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>Hello 코드에서 모델을 만들 hello 스키마를 사용 하 여
Hello 코드 앞에, 아래 코드 다음 hello를 추가 합니다.

```Javascript
// Create a basic schema toostore your tasks and users.
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

먼저 hello 코드에서 알 수 있습니다, 스키마를 만들어집니다. 다음으로 모델 개체를 만듭니다. Hello 모델 개체 toostore hello 전체에서 데이터를 정의할 때 코드를 사용 하 여 **경로**합니다.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13: 작업 REST API 서버에 대한 경로 추가
와 데이터베이스 모델 toowork를가지고 사용할 REST API 서버에 대 한 hello 경로 추가 합니다.

### <a name="about-routes-in-restify"></a>Restify의 경로 정보
경로 restify 정확 하 게 hello 동일한 방식으로 사용 하는 경우 hello 빠른 스택 작업 합니다. Hello hello 클라이언트 응용 프로그램 toocall 예상 되는 URI를 사용 하 여 경로 정의 합니다. 일반적으로 경로는 별도 파일에 정의합니다. 이 자습서에서는 Server.js에 경로를 저장합니다. 프로덕션 사용을 위해서는 자체 파일로 경로를 팩터링하는 것이 좋습니다.

Restify 경로의 일반적인 패턴:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Hello 가장 기본적인 수준에서 hello 패턴입니다. Restify (및 Express) hello 기능 toodefine 응용 프로그램 유형 및 다른 끝점을 통해 복잡 한 라우팅 같은 더욱 심층적 기능을 제공 합니다.

#### <a name="add-default-routes-tooyour-server"></a>기본 경로 tooyour 서버 추가
Hello 기본 CRUD 경로 추가: **만들**, **검색**, **업데이트**, 및 **삭제**합니다.

1.  명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

    `cd azuread`

2.  편집기에서 Server.js를 엽니다. 이전에 만든 데이터베이스 항목 hello 아래 hello 다음 정보를 추가 합니다.

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
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
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a>오류 hello 경로 대 한 처리를 추가 합니다.
발생 한 hello 문제에 대 한 백 toohello 클라이언트 통신할 수 있도록 몇 가지 오류 처리를 추가 합니다.

이미 작성 하는 hello 코드 아래 코드 다음 hello를 추가 합니다.

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a>14: 서버 만들기
마지막 일 toodo hello tooadd 서버 인스턴스는 합니다. hello 서버 인스턴스는 호출을 관리합니다.

Restify(및 Express)는 REST API 서버에 사용할 수 있는 심층적인 사용자 지정을 갖습니다. 이 자습서에서는 hello 가장 기본 설정을 사용합니다.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: 지금은 인증) (없이 hello 경로 추가
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
// Register a default '/' handler
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
## <a name="16-run-hello-server"></a>16: hello 서버를 실행 합니다.
좋습니다 tootest는 인증을 추가 하기 전에 서버입니다.

hello 가장 쉬운 방법은 tootest 서버 명령 프롬프트에서 curl을 사용 하는 것입니다. toodo이 JSON으로 tooparse 출력을 사용할 수 있는 간단한 유틸리티를 해야 합니다. 

1.  예제 따르는 hello에 사용 하는 hello JSON 도구를 설치 합니다.

    `$npm install -g jsontool`

    이 전역으로 hello JSON 도구를 설치합니다.

2.  MongoDB 인스턴스가 실행되고 있는지 확인합니다.

    `$sudo mongod`

3.  Hello 디렉터리도 변경**azure ad**, 다음 curl을 실행 합니다.

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
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

4.  tooadd 작업:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

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

5.  Brandon에 대한 작업을 나열합니다.

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

이러한 모든 명령이 오류 없이 실행 하는 경우 준비 tooadd OAuth toohello REST API 서버입니다.

*이제 MongoDB를 사용하는 REST API 서버가 완료되었습니다.*

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: 인증 tooyour REST API 서버를 추가 합니다.
실행 중인 REST API를가지고 toouse를 설정 하 여 Azure AD.

명령 프롬프트에서 다음 디렉터리로 hello 너무**azure ad**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>포함 된 hello oidcbearerstrategy passport azure ad 사용
지금까지 권한 부여 없이 일반적인 REST TODO 서버를 빌드했습니다. 이제 인증을 추가합니다.

먼저, toouse Passport 되도록 지정 합니다. 이전 서버 구성 바로 뒤에 이를 추가합니다.

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> Api를 작성할 때 사용자 hello hello 토큰에서 고유한 데이터 toosomething 스푸핑 하지 하는 것이 좋습니다 tooalways 링크 hello 합니다. 이 서버는 할 일 항목을 저장 하는 경우 hello 토큰 (token.sub 통해 라고 함)에 hello 사용자 구독 ID에 따라 저장 합니다. Hello token.sub을 hello "소유자" 필드에 넣습니다. 이렇게 하면 해당 사용자만 hello 사용자 TODOs를 액세스할 수 있습니다. 다른 사람이 입력 된 hello TODOs 액세스할 수 있습니다. "소유자"에 대 한 hello API가 노출 없습니다. 외부 사용자는 인증되는 경우에 다른 사용자의 TODO를 요청할 수 있습니다.
> 
> 

를 사용 하 여 함께 제공 된 hello Open ID 연결 전달자 전략 `passport-azure-ad`합니다. 이전에 붙여 넣은 코드 뒤에 이 코드를 넣습니다.

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Passport는 모든 전략(Twitter, Facebook 등)에 유사한 패턴을 사용합니다. 모든 전략 기록기 toohello 패턴을 준수합니다. Hello 전략 전달는 `function()` 토큰을 사용 하 고 `done` 매개 변수로 합니다. hello 전략에는 모든 작업을 수행한 후 반환 됩니다. Hello 사용자 및 보관 hello 토큰 저장에 대 한 tooask 다시 필요 하지 않습니다.

> [!IMPORTANT]
> hello 앞의 코드는 tooyour 서버를 인증할 수 있는 모든 사용자 합니다. 이를 자동 등록이라고 합니다. 프로덕션 서버에 원하지 toolet 모든 사용자 선택 하는 등록 프로세스를 통해 이동 하는 첫 번째 필요 없이 합니다. 일반적으로 소비자 앱에서 참조 하는 hello 패턴입니다. hello 응용 프로그램 수를 Facebook에 tooregister 허용 하지만 다음 묻는 tooenter 추가 정보. 명령줄 프로그램이 자습서를 사용 하지 않은 경우 반환 되는 hello 토큰 개체에서 hello 전자 메일을 추출할 수 있습니다. 그런 다음 hello 사용자 tooenter 추가 정보를 요청할 수 있습니다. Hello 사용자를 추가 하는 테스트 서버 이기 때문에 직접 toohello 메모리 내 데이터베이스입니다.
> 
> 

### <a name="protect-endpoints"></a>끝점 보호
Hello를 지정 하 여 끝점 보호 **passport.authenticate()** toouse 원하는 hello 프로토콜을 사용 하 여 호출 합니다.

고급 옵션에 대한 서버 코드에서 사용자의 경로를 편집할 수 있습니다.

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18: 서버 응용 프로그램 다시 실행
끝점에 대 한 OAuth 2.0 보호를 포함 하는 경우 사용 하 여 curl toosee 다시 합니다. 이 끝점에 대해 클라이언트 SDK 중 하나를 실행하기 전에 이 작업을 수행합니다. 반환 된 hello 헤더 알려 주어 야 인증 제대로 작동 하는 경우.

1.  MongoDB 인스턴스가 실행되고 있는지 확인합니다.

    `$sudo mongod`

2.  Toohello 변경 **azure ad** 디렉터리 및 사용 하 여 curl:

    `$ cd azuread`

    `$ node server.js`

3.  기본 POST를 시도합니다.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 응답 hello Passport 계층 tooredirect 시도 나타냅니다 toohello 끝점의 경우이 수행할 권한을 부여 합니다.

*이제 OAuth 2.0을 사용하는 REST API 서비스가 있습니다.*

OAuth 2.0 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다. 이 위해 추가 자습서 tooreview를 해야 합니다.

## <a name="next-steps"></a>다음 단계
완료 하는 hello 예제 구성 값) (없이 제공 됩니다 참조용으로 [.zip 파일](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)합니다. GitHub에서 복제할 수도 있습니다.

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

이제 toomore 고급 항목에 이동할 수 있습니다. Tootry 경우가 [hello v2.0 끝점을 사용 하는 Node.js 웹 응용 프로그램 보안](active-directory-v2-devquickstarts-node-web.md)합니다.

다음은 몇 가지 추가 리소스입니다.

* [Azure AD v2.0 개발자 가이드](active-directory-appmodel-v2-overview.md)
* [Stack Overflow "azure-active-directory" 태그](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기
Toosign을 보안 사고 발생할 때 알림 toobe 사용 하는 것이 좋습니다. Hello에 [Microsoft 기술 보안 알림](https://technet.microsoft.com/security/dd252948) 페이지, tooSecurity 권고 경고를 구독 합니다.

