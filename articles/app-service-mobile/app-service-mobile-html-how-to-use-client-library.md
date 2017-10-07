---
title: "aaaHow tooUse hello Azure 모바일 앱 용 JavaScript SDK"
description: "어떻게 Azure 모바일 앱에 대 한 tooUse v"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>TooUse는 Azure 모바일 앱 용 JavaScript 클라이언트 라이브러리를 hello 하는 방법
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

이 가이드 최신 버전의 hello를 사용 하 여 tooperform 일반적인 시나리오에 설명 [Azure 모바일 앱 용 JavaScript SDK]합니다. 새로운 tooAzure 모바일 앱의 경우 먼저 완료 [Azure 모바일 앱 빠른 시작] toocreate 백 엔드 고 테이블을 만듭니다. 이 가이드에서는 hello 모바일 백 엔드를 사용 하 여 HTML/JavaScript 웹 응용 프로그램에 집중 합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
브라우저 지원 toohello 현재 제한 하 고 마지막 버전의 hello 주요 브라우저: Google Chrome, Microsoft Edge, Microsoft Internet Explorer 및 Mozilla Firefox 합니다.  상대적으로 최신 브라우저와 SDK toofunction hello 라고 생각 됩니다.

hello 패키지는 전역, AMD 지원 하 고 CommonJS 형식을 지정 하므로 유니버설 JavaScript 모듈로 배포 됩니다.

## <a name="Setup"></a>설정 및 필수 조건
이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다. 이 가이드에서는 해당 hello 테이블에 hello 가정 해당 자습서의 hello 테이블이 동일한 스키마입니다.

Hello Azure 모바일 앱의 JavaScript SDK 설치 hello를 통해 수행할 수 있습니다 `npm` 명령:

```
npm install azure-mobile-apps-client --save
```

hello 라이브러리를 ES2015 모듈로 Browserify 등 시스템용 및 AMD 라이브러리로 CommonJS 환경 내에서 사용할 수도 있습니다.  예:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

또한 우리의 CDN에서 직접 다운로드 하 여 미리 작성 된 버전의 hello SDK 사용할 수 있습니다.

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>방법: 사용자 인증
Azure App Service는 Facebook, Google, Microsoft 계정 및 Twitter와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다. 권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다. 서버 스크립트에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를도 사용할 수 있습니다. 자세한 내용은 참조 hello [인증 시작] 자습서입니다.

두 가지의 인증 흐름, 즉 서버 흐름과 클라이언트 흐름이 지원됩니다.  hello 서버 흐름 hello 공급자의 웹 인증 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다. hello 클라이언트 흐름 고려한 장치 전용 기능이 있는 밀접 하 게 통합와 같은 단일 로그온 공급자별 Sdk를 사용 합니다.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>방법: 외부 리디렉션 URL에 대해 모바일 App Service 구성
여러 유형의 JavaScript 응용 프로그램 UI OAuth 흐름 루프백 기능 toohandle를 사용 합니다.  이러한 기능은 다음과 같습니다.

* 로컬로 서비스 실행
* 라이브 다시 로드를 사용 하 여 Ionic 프레임 워크 hello로
* 인증에 대 한 서비스 tooApp을 리디렉션합니다.

로컬로 실행 중 앱 서비스 인증은 기본적으로 모바일 앱 백 엔드에서 tooallow 액세스를 구성 하기 때문에 문제가 발생할 수 있습니다. Hello 단계 toochange hello 응용 프로그램 서비스 설정 tooenable 인증 hello 서버를 로컬로 실행 하는 경우 다음을 사용 합니다.

1. Toohello 로그인 [Azure 포털]
2. 모바일 앱 백 엔드에서 tooyour 이동 합니다.
3. 선택 **리소스 탐색기** hello에 **개발 도구** 메뉴.
4. 클릭 **이동** 새 탭 또는 창에서 모바일 앱 백 엔드에 대 한 tooopen hello 리소스 탐색기입니다.
5. Hello 확장 **config** > **authsettings** 응용 프로그램에 대 한 노드입니다.
6. Hello 클릭 **편집** tooenable hello 리소스의 편집 단추입니다.
7. Hello **allowedExternalRedirectUrls** 요소는 null 이어야 합니다. 배열에 URL을 추가합니다.

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    이 예제는 서비스의 url이 hello hello 배열의 hello Url 바꾸기 `http://localhost:3000` hello 로컬 Node.js 샘플 서비스입니다. 사용 해도 `http://localhost:4400` hello Ripple 서비스 또는 응용 프로그램 구성 된 방식에 따라 다른 URL에 대 한 합니다.
8. Hello hello 페이지의 위쪽에 클릭 **읽기/쓰기**, 클릭 **배치** toosave 업데이트 합니다.

또한 tooadd 해야 hello toohello CORS 허용 목록 설정에 대 한 동일한의 루프백 Url:

1. 뒤로 toohello 이동 [Azure 포털]합니다.
2. 모바일 앱 백 엔드에서 tooyour 이동 합니다.
3. 클릭 **CORS** hello에 **API** 메뉴.
4. 빈 hello에 각 URL을 입력 **허용 된 원본을** 입력란.  새 텍스트 상자가 생성됩니다.
5. **저장**을 클릭합니다.

Hello 백 엔드 업데이트 후에 응용 프로그램에서 수 toouse hello 새 루프백 Url 됩니다.

<!-- URLs. -->
[Azure 모바일 앱 빠른 시작]: app-service-mobile-cordova-get-started.md
[인증 시작]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure 포털]: https://portal.azure.com/
[Azure 모바일 앱 용 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
