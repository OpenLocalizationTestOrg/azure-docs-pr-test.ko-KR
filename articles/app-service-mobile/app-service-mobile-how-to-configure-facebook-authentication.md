---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Facebook 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 tooconfigure Facebook 인증 합니다."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Facebook 로그인
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

이 항목에서는 tooconfigure Azure 앱 서비스를 인증 공급자로 Facebook toouse 합니다.

이 항목의 toocomplete hello 절차, 확인 된 전자 메일 주소와 휴대폰 번호를 보유 하는 Facebook 계정이 있어야 합니다. 새 Facebook 계정을 toocreate 너무 이동[facebook.com]합니다.

## <a name="register"> </a>Facebook을 사용하여 응용 프로그램 등록
1. Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. **URL**을 복사합니다. 이 tooconfigure Facebook 앱을 사용 합니다.
2. 다른 브라우저 창에서 탐색 toohello [Facebook Developers] 계정 자격 증명을 웹 사이트 및 사용자가 Facebook으로 로그인 합니다.
3. (선택 사항) 이미를 등록 하지 않은 경우 클릭 **앱** > **개발자 등록**, 다음 hello 방침에 동의 및 hello 등록 단계를 수행 합니다.
4. **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**를 클릭합니다. 
5. **표시 이름**, 앱 형식에 대 한 고유한 이름을 입력 하면 **Contact Email**, 선택는 **범주** 응용 프로그램에 대 한 클릭 **응용프로그램ID만들기**hello 보안 검사를 완료 합니다. 새로운 Facebook 응용 프로그램에 대 한 개발자 대시보드 toohello 이동합니다.
6. "Facebook 로그인"에서 **시작**을 클릭합니다. 응용 프로그램의 추가 **리디렉션 URI** 너무**유효한 OAuth 리디렉션 Uri**, 클릭 **변경 내용 저장**합니다. 
   
   > [!NOTE]
   > 프로그램 리디렉션 URI는 hello 경로 추가 되므로 응용 프로그램의 hello URL */.auth/login/facebook/callback*합니다. 예: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.
   > 
   > 
7. Hello 왼쪽 탐색에서 클릭 **설정을**합니다. Hello에 **응용 프로그램 암호** 필드를 클릭 **표시**, 암호를 제공 하 여 요청 다음의 hello 값을 기록 하는 경우 **앱 ID** 및 **응용 프로그램 암호**. Azure 이후 tooconfigure 이러한 응용 프로그램 사용합니다.
   
   > [!IMPORTANT]
   > hello 응용 프로그램 암호는는 중요 한 보안 자격 증명입니다. 다른 사람과 이 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.
   > 
   > 
8. Facebook 계정을 사용 하는 tooregister hello 응용 프로그램 이었던 hello가 hello 응용 프로그램의 관리자입니다. 지금은 관리자만 이 응용 프로그램에 로그인할 수 있습니다. tooauthenticate 다른 Facebook 계정을 클릭 **응용 프로그램 검토** 사용 하도록 설정 하 고 **만들기 < your-응용 프로그램-이름 > 공개** tooenable Facebook 인증을 사용 하는 일반 공용 액세스 합니다.

## <a name="secrets"></a>추가 Facebook 정보 tooyour 응용 프로그램
1. Hello에 다시 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. **설정** > **인증 / 권한 부여**를 클릭하고 **App Service 인증**이 **켜기**인지 확인합니다.
2. 클릭 **Facebook**, 이전에 얻은 hello 앱 ID 및 응용 프로그램 암호 값을 붙여, 필요한 경우 응용 프로그램에 필요한 모든 범위를 사용 하도록 설정 차례로 클릭 **확인**합니다.
   
    ![][0]
   
    기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다. 앱 코드에서 사용자 권한을 부여해야 합니다.
3. (선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자가 Facebook에 의해 인증 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Facebook**합니다. 이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청은 인증에 대 한 리디렉션된 tooFacebook 키를 누릅니다.
4. 인증 구성이 완료되면 **저장**을 클릭합니다.

이제 준비 toouse Facebook 인증에 대 한 응용 프로그램입니다.

## <a name="related-content"> </a>관련 콘텐츠
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure 포털]: https://portal.azure.com/
