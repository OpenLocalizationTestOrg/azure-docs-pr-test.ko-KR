---
title: "aaaHow tooUse Azure 모바일 앱에 대 한 Apache Cordova 플러그 인"
description: "어떻게 tooUse Azure 모바일 앱에 대 한 Apache Cordova 플러그 인"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>어떻게 toouse Azure 모바일 앱에 대 한 클라이언트 라이브러리를 Apache Cordova
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

이 가이드 최신 버전의 hello를 사용 하 여 tooperform 일반적인 시나리오에 설명 [Azure 모바일 앱에 대 한 Apache Cordova 플러그 인]합니다. 새로운 tooAzure 모바일 앱의 경우 먼저 완료 [Azure 모바일 앱 빠른 시작] toocreate을 백 엔드는 테이블을 만들고 미리 작성 된 Apache Cordova 프로젝트를 다운로드 합니다. 이 가이드에 집중 hello 클라이언트 쪽 Apache Cordova 플러그 인 합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
이 SDK는 iOS, Android 및 Windows 장치에서 Apache Cordova v6.0.0 이상을 지원합니다.  지원 되는 hello 플랫폼은 다음과 같습니다.

* Android API 19-24(Nougat를 통한 KitKat)
* iOS 버전 8.0 이상.
* Windows Phone 8.1
* 범용 Windows 플랫폼

## <a name="Setup"></a>설정 및 필수 조건
이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다. 이 가이드에서는 해당 hello 테이블에 hello 가정 해당 자습서의 hello 테이블이 동일한 스키마입니다. 이 가이드는 또한 hello Apache Cordova 플러그 인 tooyour 코드를 추가 했다고 가정 합니다.  그렇게 하지 않은 경우 hello Apache Cordova 플러그 인 tooyour 프로젝트 hello 명령줄에 추가할 수 있습니다.

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

[첫 번째 Apache Cordova 앱]을 만드는 방법에 대한 자세한 내용은 해당 설명서를 참조하세요.

## <a name="ionic"></a>Ionic v2 앱 설정

tooproperly Ionic v2 프로젝트 구성, 먼저 기본 앱을 만들고 hello Cordova 플러그 인 추가:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

위의 삼각형 너무 hello 추가`app.component.ts` toocreate hello 클라이언트 개체:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

이제 작성 하 고 hello 프로젝트 hello 브라우저에서 실행할 수 있습니다.

```
ionic platform add browser
ionic run browser
```

hello Azure 모바일 앱 Cordova 플러그 인 두 Ionic v1 및 v2 앱을 지원합니다.  Ionic v2 hello 앱 hello에 대 한 추가 선언이 필요는 전용 `WindowsAzure` 개체입니다.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>방법: 사용자 인증
Azure App Service는 Facebook, Google, Microsoft 계정 및 Twitter와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다. 권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다. 서버 스크립트에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를도 사용할 수 있습니다. 자세한 내용은 참조 hello [인증 시작] 자습서입니다.

Apache Cordova 앱의 인증을 사용할 때는 hello Cordova 플러그 인을 다음 사용할 수 있어야 합니다.

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

두 가지의 인증 흐름, 즉 서버 흐름과 클라이언트 흐름이 지원됩니다.  hello 서버 흐름 hello 공급자의 웹 인증 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다. hello 클라이언트 흐름 고려한 장치 전용 기능이 있는 밀접 하 게 통합와 같은 단일 로그온 공급자별 장치 관련 Sdk를 사용 합니다.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>방법: 외부 리디렉션 URL에 대해 모바일 App Service 구성
여러 종류의 Apache Cordova 응용 프로그램 UI OAuth 흐름 루프백 기능 toohandle를 사용 합니다.  Localhost에 OAuth UI 흐름이 hello 인증 서비스만 알고 있으므로 문제를 일으킬 어떻게 tooutilize 기본적으로 서비스입니다.  다음은 문제가 있는 OAuth UI 흐름의 예입니다.

* hello Ripple 에뮬레이터입니다.
* Ionic을 사용하여 라이브 다시 로드.
* Hello 모바일 백 엔드를 로컬로 실행
* Hello 하나의 제공 인증 보다 다른 Azure 앱 서비스의 hello 모바일 백 엔드를 실행 합니다.

이러한 지침은 tooadd 로컬 설정 toohello 구성을 수행 합니다.

1. Toohello 로그인 [Azure 포털]
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 모바일 응용 프로그램의 hello 이름을 클릭 합니다.
3. **도구** 클릭
4. 클릭 **리소스 탐색기** hello 관찰 메뉴를 클릭 한 다음 **이동**합니다.  새 창 또는 탭이 열립니다.
5. Hello 확장 **config**, **authsettings** hello 왼쪽 탐색 창에서 사이트에 대 한 노드.
6. **편집**을 클릭합니다.
7. Hello "allowedExternalRedirectUrls" 요소를 찾습니다.  Toonull 또는 값의 배열에는 설정할 수 있습니다.  Hello 값 toohello 다음 값을 변경 합니다.

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    서비스의 url이 hello hello Url을 대체 합니다.  예로 (hello Node.js 샘플 서비스)에 대 한 "http://localhost:3000" 또는 "http://localhost:4400" (서비스에 대 한 hello Ripple).  그러나 이러한 Url은 예-hello 예에 언급 된 hello 서비스에 대 한 포함 하 여 상황에는 다를 수 있습니다.
8. Hello 클릭 **읽기/쓰기** hello hello 화면 오른쪽 위 모퉁이의 단추입니다.
9. 녹색 hello 클릭 **배치** 단추입니다.

이 시점에 hello 설정이 저장 됩니다.  Hello 설정을 완료 될 때까지 hello 브라우저 창을 닫지 마십시오 저장 합니다.
또한 응용 프로그램 서비스에 대 한 이러한 루프백 Url toohello CORS 설정을 추가 합니다.

1. Toohello 로그인 [Azure 포털]
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 모바일 응용 프로그램의 hello 이름을 클릭 합니다.
3. hello 설정 블레이드에서 자동으로 열립니다.  자동으로 열리지 않으면 **모든 설정**을 클릭합니다.
4. 클릭 **CORS** hello API 메뉴.
5. Tooadd 제공 된 hello 상자에 원하는 hello URL을 입력 하 고 Enter 키를 누릅니다.
6. 필요에 따라 추가 URL을 입력합니다.
7. 클릭 **저장** toosave hello 설정 합니다.

새로운 설정 tootake 효과 hello에 대 한 약 10-15 초 걸립니다.

## <a name="register-for-push"></a>방법: 푸시 알림 등록
Hello 설치 [phonegap 플러그 인 푸시] toohandle 푸시 알림을 합니다.  이 플러그 인 쉽게 추가할 수를 사용 하는 `cordova plugin add` hello 명령줄 또는 Visual Studio 내에서 hello Git 플러그 인 설치 관리자를 통해 명령입니다.  Apache Cordova 앱에서 다음 코드는 푸시 알림을 위해 장치를 등록합니다.

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Hello hello 서버에서 알림 허브 SDK toosend 푸시 알림을 사용 합니다.  클라이언트에서 직접 푸시 알림을 보내지 마세요. 이렇게 하면 지금 사용된 tootrigger 알림 허브에 대 한 서비스 공격의 거부 또는 PNS hello 합니다.  hello PNS에는 이러한 공격으로 인해 트래픽의 b 수입니다.

## <a name="more-information"></a>자세한 정보

우리의 [API 설명서](http://azure.github.io/azure-mobile-apps-js-client/)에서 자세한 API 세부 정보를 찾을 수 있습니다.

<!-- URLs. -->
[Azure 포털]: https://portal.azure.com
[Azure 모바일 앱 빠른 시작]: app-service-mobile-cordova-get-started.md
[인증 시작]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure 모바일 앱에 대 한 Apache Cordova 플러그 인]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[첫 번째 Apache Cordova 앱]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap 플러그 인 푸시]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
