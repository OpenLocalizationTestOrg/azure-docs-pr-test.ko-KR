---
title: "aaaAuthentication 및 Azure 모바일 앱에 대 한 권한 부여 | Microsoft Docs"
description: "개념적 참조 및 간략하게 hello 인증 / 권한 부여 Azure 모바일 앱에 대 한 기능"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Azure 모바일 앱의 인증 및 권한 부여
## <a name="what-is-app-service-authentication--authorization"></a>앱 서비스 인증/권한 부여란?
> [!NOTE]
> 이 항목에는 마이그레이션된 tooa 통합 됩니다 [응용 프로그램 서비스 인증 / 권한 부여](../app-service/app-service-authentication-overview.md) 웹, 모바일 및 API 앱에 설명 하는 항목입니다.
> 
> 

앱 서비스 인증 / 권한 부여는 hello 앱 백 엔드에 필요한 코드 변경 없이 사용자가 응용 프로그램 toolog 수 있는 기능입니다. 제공을 쉽게 tooprotect 응용 프로그램 및 작업 사용자별 데이터를 사용 합니다.

응용 프로그램 서비스는 페더레이션된 id를 사용 하 여 한 타사 **id 공급자** hello 응용 프로그램에서이 id를 사용 하 여 자체 대신 및 계정을 저장 하 고 사용자를 인증 하는 "IDP ("). 응용 프로그램 서비스는 hello 초기 5 개 id 공급자 지원: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft 계정*, 및 *Twitter*합니다. 또한 다른 ID 공급자 또는 사용자 고유의 사용자 지정 ID 솔루션을 통합하여 앱에 이 지원을 확장할 수 있습니다.

앱은 개수에 관계 없이 이러한 ID 공급자를 활용할 수 있으므로 최종 사용자에게 로그인 방법에 대한 옵션을 제공할 수 있습니다.

Tooget 당장 시작 하려면 다음 자습서 hello 중 하나 참조 하십시오.

* [인증 tooyour iOS 앱 추가]
* [인증 tooyour Xamarin.iOS 앱 추가]
* [인증 tooyour Xamarin.Android 앱 추가]
* [인증 tooyour Windows 앱 추가]

## <a name="how-authentication-works"></a>인증 작동 방법
순서 tooauthenticate hello id 공급자 중 하나를 사용 하 여에서 먼저 응용 프로그램에 대 한 tooconfigure hello identity provider tooknow를 해야 합니다. hello id 공급자는 다음 Id 및 제공 백 toohello 응용 프로그램을 제공 하는 비밀 합니다. 이 hello 트러스트 관계를 완료 하 고 앱 서비스 toovalidate 제공 된 id tooit를 허용 합니다.

이러한 단계는 hello 다음 항목에서에서 자세히 설명 합니다.

* [어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]
* [어떻게 tooconfigure 앱 toouse Facebook 로그인]
* [어떻게 tooconfigure 앱 toouse Google 로그인]
* [어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]
* [어떻게 tooconfigure 앱 toouse Twitter 로그인]

모든 hello 백 엔드에 구성 되 면 프로그램 클라이언트 toolog에서 수정할 수 있습니다. 두 가지 접근 방법은 다음과 같습니다.

* 클라이언트 SDK hello 모바일 앱을 통해 코드의 한 줄을 사용 하 여 사용자가에 로그인 합니다.
* 지정한 id 공급자 tooestablish id가 게시 한 SDK를 활용와 관련 된 액세스 tooApp 서비스입니다.

> [!TIP]
> 대부분의 응용 프로그램 보다 네이티브 느낌 로그인 환경 및 tooleverage 새로 고침 지원 및 기타 공급자별 혜택 공급자 SDK tooget 사용 해야 합니다.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>공급자 SDK 없이 인증 작동 방법
공급자 SDK tooset 지 수에 대 한 모바일 앱 tooperform hello 로그인을 허용할 수 있습니다. hello 모바일 앱 클라이언트 SDK를 선택 하 고 완전 hello에 대 한 로그인의 웹 보기 toohello 공급자를 열립니다. 블로그 및 포럼 나타납니다에 경우에 따라이 tooas hello "서버 흐름" 또는 "서버에서 제어 흐름" hello 서버 이후 hello 로그인을 관리 하는 및 참조 hello 클라이언트 SDK hello 공급자 토큰이 오지 않습니다.

hello 코드에는 각 플랫폼에 대 한 hello 인증 자습서에서이 흐름 설명 toostart가 필요 합니다. Hello 흐름의 hello 끝 hello 클라이언트 SDK는 앱 서비스 토큰 않았으며 hello 토큰은 자동으로 연결 된 tooall 요청 toohello 백 엔드 됩니다.

### <a name="how-authentication-with-a-provider-sdk-works"></a>공급자 SDK를 통한 인증 작동 방법
Hello 로그인 경험 toointeract hello 플랫폼에서 실행 되 고 OS hello 앱와 보다 긴밀 하 게 허용 하는 공급자 SDK 사용 합니다. 또한 이렇게 하면 공급자 토큰과 훨씬 더 쉽게 tooconsume graph Api를 사용 하면 있으며 hello 사용자 환경을 사용자 지정 하는 hello 클라이언트에 대 한 사용자 정보입니다. 경우에 따라 블로그 및 포럼에 표시이 참조 tooas hello "클라이언트 흐름" 또는 "클라이언트에서 제어 흐름" 코드 이후 hello 클라이언트 hello 로그인을 처리 하는 되 고 hello 클라이언트 코드는 액세스 tooa 공급자 토큰입니다.

공급자 토큰을 가져온 후 toobe tooApp 서비스 유효성 검사를 위해 전송 해야 합니다. Hello 흐름의 hello 끝 hello 클라이언트 SDK는 앱 서비스 토큰 않았으며 hello 토큰은 자동으로 연결 된 tooall 요청 toohello 백 엔드 됩니다. 또한 hello 개발자는 선택 하는 경우 참조 toohello 공급자 토큰을 유지할 수 있습니다.

## <a name="how-authorization-works"></a>권한 부여 작동 원리
앱 서비스 인증 / 권한 부여를 위한 여러 가지 노출 **요청이 인증 되지 않은 경우 동작 tootake**합니다. 코드를 지정 된 요청을 받으면 전에 포함할 수 앱 서비스 검사 toosee hello 요청이 인증 되 면 있으며 그렇지 않은 경우를 거부 하 고 다시 시도 하기 전에 toohave hello 사용자 로그인을 시도 합니다.

한 가지 옵션은 인증 되지 않은 toohave 요청 tooone hello id 공급자의 리디렉션입니다. 웹 브라우저에서이 실제로 걸립니다 hello 사용자 tooa 새 페이지. 그러나 모바일 클라이언트는 이러한 방식으로 리디렉션할 수 없고 인증되지 않은 응답은 HTTP *401 권한 없는* 응답을 받습니다. Hello 첫 번째 요청 하면 클라이언트는 항상 toohello 로그인 끝점 이어야 하 고 만들 수 있습니다이 점을 고려 tooany 다른 Api를 호출 합니다. 로그인 하기 전에 다른 API toocall 시도 하면 클라이언트에 오류가 발생 합니다.

보다 세부적인 toohave를 원하는 경우 인증을 요구 하는 끝점을 통해 컨트롤을 선택할 수 있습니다 "동작 안 함 (요청을 허용 합니다.)" 인증 되지 않은 요청에 대 한 합니다. 모든 인증 결정이 경우에 지연 된 tooyour 응용 프로그램 코드입니다. 또한이 방법을 통해 사용자 지정 권한 부여 규칙에 따라 tooallow 액세스 toospecific 사용자입니다.

## <a name="documentation"></a>설명서
자습서 표시 방법을 따르는 hello tooadd 인증 tooyour 모바일 클라이언트 응용 프로그램 서비스를 사용 하 여:

* [인증 tooyour iOS 앱 추가]
* [인증 tooyour Xamarin.iOS 앱 추가]
* [인증 tooyour Xamarin.Android 앱 추가]
* [인증 tooyour Windows 앱 추가]

자습서 표시 방법을 따르는 hello tooconfigure 앱 서비스 tooleverage 서로 다른 인증 공급자:

* [어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]
* [어떻게 tooconfigure 앱 toouse Facebook 로그인]
* [어떻게 tooconfigure 앱 toouse Google 로그인]
* [어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]
* [어떻게 tooconfigure 앱 toouse Twitter 로그인]

원하는 경우 toouse id 시스템 이외의 hello도 활용할 수는 여기에서 제공 된 하 게 hello [미리 보기를 사용자 지정 인증 지원 hello.NET 서버 SDK에서에서](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)합니다.

[인증 tooyour iOS 앱 추가]: app-service-mobile-ios-get-started-users.md
[인증 tooyour Xamarin.iOS 앱 추가]: app-service-mobile-xamarin-ios-get-started-users.md
[인증 tooyour Xamarin.Android 앱 추가]: app-service-mobile-xamarin-android-get-started-users.md
[인증 tooyour Windows 앱 추가]: app-service-mobile-windows-store-dotnet-get-started-users.md

[어떻게 tooconfigure 앱 toouse Azure Active Directory 로그인]: app-service-mobile-how-to-configure-active-directory-authentication.md
[어떻게 tooconfigure 앱 toouse Facebook 로그인]: app-service-mobile-how-to-configure-facebook-authentication.md
[어떻게 tooconfigure 앱 toouse Google 로그인]: app-service-mobile-how-to-configure-google-authentication.md
[어떻게 tooconfigure 앱 toouse Microsoft 계정 로그인]: app-service-mobile-how-to-configure-microsoft-authentication.md
[어떻게 tooconfigure 앱 toouse Twitter 로그인]: app-service-mobile-how-to-configure-twitter-authentication.md
