---
title: "aaaAuthentication 및 Azure 앱 서비스의 권한 부여 | Microsoft Docs"
description: "개념적 참조 및 간략하게 hello 인증 / 권한 부여 Azure 앱 서비스에 대 한 기능"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Azure 앱 서비스의 인증 및 권한 부여
## <a name="what-is-app-service-authentication--authorization"></a>앱 서비스 인증/권한 부여란?
앱 서비스 인증 / 권한 부여는 hello 앱 백 엔드에 toochange 코드가 없는 있도록 사용자의 응용 프로그램 toosign 프로그램에 대 한 방식으로 제공 하는 기능입니다. 제공을 쉽게 tooprotect 응용 프로그램 및 작업 사용자별 데이터를 사용 합니다.

앱 서비스는 페더레이션된 ID를 사용하며 여기서 타사 ID 공급자는 계정을 저장하고 사용자를 인증합니다. hello 응용 프로그램 hello 앱에 없는 toostore 자체 해당 정보를 hello 공급자의 id 정보에 의존 합니다. 응용 프로그램 서비스는 hello 초기 5 개 id 공급자 지원: Azure Active Directory, Facebook, Google, Microsoft 계정 및 Twitter 합니다. 앱에 사용할 수 이러한 identity 공급자 tooprovide 개수에 관계 없이 사용자에 게 옵션으로에 로그인 할. tooexpand hello 기본 제공 지원, 다른 id 공급자를 통합할 수 있습니다 또는 [사용자 고유의 사용자 지정 id 솔루션][custom-auth]합니다.

Tooget 당장 시작 하려면 다음 자습서 hello 중 하나를 참조:

* [인증 tooyour iOS 앱 추가] [ iOS] (또는 [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], 또는 [Cordova])
* [Azure App Service의 API Apps에 대한 사용자 인증][apia-user]
* [Azure App Service 시작 - 2부][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>앱 서비스에서 인증이 작동하는 방식
Hello id 공급자 중 하나를 사용 하 여 순서 tooauthenticate에서 먼저 응용 프로그램에 대 한 tooconfigure hello identity provider tooknow를 해야 합니다. hello id 공급자는 Id와 tooApp 서비스를 제공 하는 암호를 제공 합니다. 이 앱 서비스 사용자 어설션을 hello id 공급자에서 인증 토큰 등을 확인할 수 있도록 hello 트러스트 관계를 완료 합니다.

이러한 공급자 중 하나를 사용 하 여 사용자의 toosign, hello 사용자는 해당 공급자에 대 한 사용자가 로그인 하는 리디렉션된 tooan 끝점 이어야 합니다. 고객 웹 브라우저를 사용 하는 경우 사용자가 로그인 하는 모든 인증 되지 않은 사용자 toohello 끝점을 자동으로 연결 하는 응용 프로그램 서비스를 사용할 수 있습니다. 그렇지 않으면 해야 toodirect 고객 너무`{your App Service base URL}/.auth/login/<provider>`여기서 `<provider>` hello 다음 값 중 하나: aad, facebook, google, microsoft 또는 twitter 합니다. 모바일 및 API 시나리오는 이 문서의 뒷부분에 나오는 섹션에 설명되어 있습니다.

웹 브라우저를 통해 응용 프로그램과 상호 작용하는 사용자는 응용 프로그램을 찾아보는 동안 인증을 유지할 수 있도록 쿠키가 제공됩니다. Hello에 표시 되는 모바일, JSON 웹 토큰 (JWT) 등의 다른 클라이언트 형식에 대 한 `X-ZUMO-AUTH` 헤더로, toohello 클라이언트 발급 됩니다. hello 모바일 앱 클라이언트 Sdk는 자동으로 처리 합니다. 또는 Azure Active Directory id 토큰 또는 액세스 토큰 직접에 포함 될 hello `Authorization` 으로 헤더는 [전달자 토큰](https://tools.ietf.org/html/rfc6750)합니다.

앱 서비스는 모든 쿠키 또는 응용 프로그램 tooauthenticate 사용자가 발급 한 토큰 유효성을 검사 합니다. 응용 프로그램에 액세스할 수 있는 toorestrict 참조 hello [권한 부여](#authorization) 이 문서의 뒷부분에 나오는 섹션.

### <a name="mobile-authentication-with-a-provider-sdk"></a>공급자 SDK를 통해 모바일 인증
모든 항목을 구성한 후에 hello 백 엔드 응용 프로그램 서비스를 사용 하 여 모바일 클라이언트 toosign을 수정할 수 있습니다. 두 가지 접근 방법은 다음과 같습니다.

* 지정 된 id 공급자 tooestablish identity를 게시 하는 SDK를 사용 하 여와 관련 된 액세스 tooApp 서비스입니다.
* 코드 한 줄을 사용 하 여 해당 hello 모바일 앱 클라이언트 SDK가 사용자의 로그인 수 있습니다.

> [!TIP]
> 대부분의 응용 프로그램 공급자 SDK tooget 사용자가 로그인 할 때 보다 일관 된 환경, toouse 새로 고침 지원 및 tooget 사용할지 이점도 hello 공급자가 지정 합니다.
> 
> 

공급자 SDK를 사용 하면 사용자가 로그인 할 수 hello 앱 hello 운영 체제와 더 밀접 하 게 통합 된 tooan 환경에서 실행 됩니다. 또한 이렇게 하면 공급자 토큰과 훨씬 더 쉽게 tooconsume graph Api를 사용 하면 있으며 hello 사용자 환경을 사용자 지정 하는 hello 클라이언트에 대 한 사용자 정보입니다. 블로그 및 포럼에 가끔씩 참조 tooas hello "클라이언트 흐름"이 표시 됩니다 또는 "클라이언트에서 제어 흐름" hello 클라이언트에서 코드에 사용자 및 hello 클라이언트 코드에서 서명 때문에 대 한 액세스 tooa 공급자 토큰입니다.

공급자 토큰을 가져온 후 toobe tooApp 서비스 유효성 검사를 위해 전송 해야 합니다. 앱 서비스 hello 토큰 유효성을 검사 한 후 앱 서비스 toohello 클라이언트에 반환 되는 새 앱 서비스 토큰을 만듭니다. hello 모바일 앱 클라이언트 SDK 도우미 메서드 toomanage이이 exchange 않았으며 hello 토큰 tooall 요청 toohello 응용 프로그램 백 엔드를 자동으로 연결 됩니다. 또한 개발자는 선택 하는 경우 참조 toohello 공급자 토큰을 유지할 수 있습니다.

### <a name="mobile-authentication-without-a-provider-sdk"></a>공급자 SDK 없이 모바일 인증
공급자 SDK tooset 하지 않으려면 드립니다에 Azure 앱 서비스 toosign의 hello 모바일 앱 기능을 허용할 수 있습니다. hello 모바일 앱 클라이언트 SDK 선택 해 웹 보기 toohello 공급자 열고 hello 사용자 로그인 됩니다. 경우에 따라 블로그 및 포럼에 표시 됩니다이 참조 tooas hello "서버 흐름" 또는 "서버에서 제어 흐름" hello 서버 사용자가 로그인 하는 hello 프로세스를 관리 하 고 hello 클라이언트 SDK hello 공급자 토큰이 오지 않습니다.

이 흐름은 각 플랫폼에 대 한 hello 인증 자습서에 포함 된 toostart 코드. Hello 흐름의 hello 끝 hello 클라이언트 SDK는 앱 서비스 토큰 않았으며 hello 토큰은 자동으로 연결 된 tooall 요청 toohello 응용 프로그램 백 엔드 됩니다.

### <a name="service-to-service-authentication"></a>서비스 간 인증
사용자가 액세스 tooyour 응용 프로그램을 제공할 수 있습니다, 있지만 다른 응용 프로그램 toocall를 자신의 API도 신뢰할 수 있습니다. 예를 들어 다른 웹앱에서 API를 호출하는 하나의 웹앱을 가질 수 있습니다. 이 시나리오에서 사용자 자격 증명 tooget 토큰 대신 특정 서비스 계정에 대 한 자격 증명을 사용 합니다. Azure Active Directory 용어에서 서비스 계정은 *서비스 주체* 라고도 하며, 이러한 계정을 사용하는 인증을 서비스 간 시나리오라고도 합니다.

> [!IMPORTANT]
> Mobile App은 고객 장치에서 실행되므로 신뢰할 수 있는 응용 프로그램으로 집계되지 *않으며* 서비스 주체 흐름을 사용하면 안 됩니다. 대신 이전에 상세하게 설명된 사용자 흐름을 사용해야 합니다.
> 
> 

서비스 간 시나리오의 경우 앱 서비스가 Azure Active Directory를 사용하여 응용 프로그램을 보호할 수 있습니다. hello 호출 응용 프로그램 tooprovide hello 클라이언트 ID와 클라이언트를 Azure Active Directory에서 암호를 제공 하 여 가져온 되는 Azure Active Directory 서비스 보안 주체 권한 부여 토큰이 필요 합니다. ASP.NET API 앱을 사용 하 여이 시나리오의 예로 hello 자습서에서 설명 되어 [서비스 API 앱에 대 한 사용자 인증][apia-service]합니다.

앱 서비스 인증 toohandle 서비스 간 시나리오 toouse 하려는 경우 클라이언트 인증서 또는 기본 인증을 사용할 수 있습니다. Azure의 클라이언트 인증서에 대 한 정보를 참조 하십시오. [어떻게 tooConfigure 웹 앱에 대 한 상호 인증 TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md)합니다. ASP.NET에서 기본 인증에 대한 자세한 내용은 [ASP.NET Web API 2에서의 인증 필터](http://www.asp.net/web-api/overview/security/authentication-filters)를 참조하세요.

앱 서비스 논리 앱 tooan API 앱에서 계정 인증 서비스는 자세히 설명 하는 특별 한 경우 [논리 앱과 앱 서비스에서 호스팅되는 사용자 지정 API를 사용 하 여](../logic-apps/logic-apps-custom-hosted-api.md)합니다.

## <a name="authorization"></a>앱 서비스에서 권한 부여가 작동하는 방식
응용 프로그램에 액세스할 수 있는 hello 요청에 대 한 모든 권한을 해야 합니다. 앱 서비스 인증 / 권한 부여 동작을 수행 하는 hello를 사용 하 여 구성할 수 있습니다.

* 인증 된 요청 tooreach만 응용 프로그램을 허용 합니다.
  
    브라우저는 익명 요청을 받고, 앱 서비스는 사용자가 로그인 할 수 있도록 선택한 hello id 공급자에 대 한 tooa 페이지를 리디렉션합니다. 반환 되는 응답은 HTTP hello hello를 요청한 경우 모바일 장치에서 *401 권한 없음* 응답 합니다.
  
    이 옵션을 사용 응용 프로그램에서 toowrite 인증 코드를 전혀 필요 하지 않습니다. 더욱 세밀 하 게 권한 부여 해야 할 경우 hello 사용자에 대 한 정보는 사용할 수 있는 tooyour 코드입니다.
* 모든 요청 tooreach 응용 프로그램을 허용 하지만 인증 된 요청을 검사 하 고 hello HTTP 헤더의 인증 정보를 따라 전달 합니다.
  
    이 옵션은 권한 부여 결정 tooyour 응용 프로그램 코드를 지연 시킵니다. 익명 요청 처리를 보다 융통성 있게 제공 하지만 toowrite 코드가 있는 합니다.
* 모든 요청 tooreach 응용 프로그램을 허용 하 고 hello 요청에 인증 정보에 대해 어떤 작업도 없습니다.
  
    이 경우 인증 hello/권한 부여 기능을 해제 합니다. 인증 및 권한 부여 hello 작업은 완전히 tooyour 응용 프로그램 코드입니다.

이전 동작 hello hello에 의해 제어 됩니다 **요청이 인증 되지 않은 경우 동작 tootake** hello Azure 포털에서에서 옵션입니다. 선택 하는 경우 * * 로그인에 *공급자 이름* * *, 모든 요청이 toobe 인증 합니다. **(작업 없음) 요청 허용** hello 권한 부여 결정 tooyour 코드를 통해 인증 정보를 제공 해야 합니다. Toohave 하려는 경우 모든 항목을 처리 하는 코드, 인증 hello를 사용 하지 않도록 설정할 수 / 권한 부여 기능입니다.

## <a name="working-with-user-identities-in-your-application"></a>응용 프로그램에서 사용자 ID 사용
응용 프로그램 서비스는 특수 한 헤더를 사용 하 여 일부 사용자 정보 tooyour 응용 프로그램을 전달 합니다. 외부 요청은 이러한 헤더를 금지하며 앱 서비스 인증/권한 부여를 통해 설정된 경우에만 존재합니다. 다음은 이러한 헤더의 예입니다.

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

모든 언어 또는 프레임 워크에서 작성 된 코드는 이러한 헤더의 hello 필요한 정보를 가져올 수입니다. ASP.NET 4.6 앱에 대 한 hello **ClaimsPrincipal** hello 적절 한 값으로 자동으로 설정 됩니다.

응용 프로그램 hello에 HTTP GET을 통해 사용자 세부 정보를 가져올 수도 `/.auth/me` 응용 프로그램의 끝점입니다. Hello 요청과 함께 포함 된 유효한 토큰 메시지가 사용 되는 hello 공급자에 대 한 세부 정보와 함께 JSON 페이로드를 반환 합니다. (기본 공급자 토큰 및 다른 사용자 정보 hello). hello 모바일 앱 서버 Sdk 도우미 메서드를 제공 toowork이이 데이터를 사용 합니다. 자세한 내용은 참조 [어떻게 toouse hello Azure 모바일 앱 Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), 및 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info)합니다.

## <a name="documentation-and-additional-resources"></a>문서 및 추가 리소스
### <a name="identity-providers"></a>ID 공급자
자습서 표시 방법을 따르는 hello tooconfigure 앱 서비스 toouse 서로 다른 인증 공급자:

* [어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인][AAD]
* [어떻게 tooconfigure 앱 toouse Facebook 로그인][Facebook]
* [어떻게 tooconfigure 앱 toouse Google 로그인][Google]
* [어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인][MSA]
* [어떻게 tooconfigure 앱 toouse Twitter 로그인][Twitter]

이외의 toouse id 시스템 사용 하려는 경우는 hello도 사용할 수는 여기에서 제공 된 하 게 hello [미리 보기를 사용자 지정 인증 지원 hello 모바일 앱.NET 서버 SDK에서에서][custom-auth], 웹 앱에서 사용할 수 있는 모바일 앱 또는 API 앱입니다.

### <a name="web-applications"></a>웹 응용 프로그램
자습서를 따라 hello tooadd 인증 tooa 웹 응용 프로그램 하는 방법을 보여 줍니다.

* [Azure App Service 시작 - 2부][web-getstarted]

### <a name="mobile-applications"></a>모바일 응용 프로그램
자습서를 따라 hello 방법을 사용 하 여 tooadd 인증 tooyour 모바일 클라이언트 hello 서버에서 제어 흐름을 보여 줍니다.

* [인증 tooyour iOS 앱 추가][iOS]
* [인증 tooyour Android 앱 추가][Android]
* [인증 tooyour Windows 앱 추가][Windows]
* [인증 tooyour Xamarin.iOS 앱 추가][Xamarin.iOS]
* [인증 tooyour Xamarin.Android 앱 추가][ Xamarin.Android]
* [인증 tooyour Xamarin.Forms 앱 추가][Xamarin.Forms]
* [인증 tooyour Cordova 앱 추가][Cordova]

리소스를 Azure Active Directory에 대 한 toouse hello 클라이언트에서 제어 흐름을 사용 하려는 경우 다음 hello를 사용 합니다.

* [IOS 용 hello Active Directory 인증 라이브러리를 사용 하 여][ADAL-iOS]
* [Android 용 hello Active Directory 인증 라이브러리를 사용 합니다.][ADAL-Android]
* [Hello Active Directory 인증 라이브러리에 대 한 Windows 및 xamarin이 설치를 사용 하 여][ADAL-dotnet]

Facebook에 대 한 toouse hello 클라이언트에서 제어 흐름을 원하는 경우 리소스를 다음 hello를 사용 합니다.

* [IOS 용 hello Facebook SDK를 사용 하 여](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Twitter에 대 한 toouse hello 클라이언트에서 제어 흐름을 원하는 경우 리소스를 다음 hello를 사용 합니다.

* [iOS용 Twitter 패브릭 사용](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Google에 대 한 toouse hello 클라이언트에서 제어 흐름을 원하는 경우 리소스를 다음 hello를 사용 합니다.

* [Google 로그인 SDK hello를 사용 하 여 iOS 용](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>API 응용 프로그램
자습서 표시 방법을 따르는 hello tooprotect API 앱:

* [Azure App Service의 API Apps에 대한 사용자 인증][apia-user]
* [Azure App Service의 API Apps에 대한 서비스 주체 인증][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
