---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Microsoft 계정 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 tooconfigure Microsoft 계정을 인증 합니다."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Microsoft 계정 로그인
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

이 항목에서는 Microsoft 계정으로 인증 공급자로 tooconfigure Azure 앱 서비스 toouse 합니다. 

## <a name="register-microsoft-account"> </a>Microsoft 계정을 사용하여 앱 등록
1. Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. 복사 프로그램 **URL**이며 나중에 tooconfigure 응용 프로그램에 Microsoft 계정을 사용 합니다.
2. Toohello 이동 [내 응용 프로그램] hello Microsoft 계정 개발자 센터에서에서 페이지 하 고 필요한 경우 Microsoft 계정으로 로그온 합니다.
3. **앱 추가**를 클릭한 후 응용 프로그램 이름을 입력하고 **응용 프로그램 만들기**를 클릭합니다.
4. Hello 메모 **응용 프로그램 ID**와 마찬가지로 나중에 필요 합니다. 
5. "플랫폼" 아래에서 **플랫폼 추가** 를 클릭하고 "웹"을 선택합니다.
6. 응용 프로그램에 대 한 "리디렉션 Uri" 공급 hello 끝점을 클릭 한 다음 **저장**합니다. 
   
   > [!NOTE]
   > 프로그램 리디렉션 URI는 hello 경로 추가 되므로 응용 프로그램의 hello URL */.auth/login/microsoftaccount/callback*합니다. 예: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.
   
7. "응용 프로그램 암호" 아래에서 **새 암호 생성**을 클릭합니다. 표시 된 hello 값을 기록해 둡니다. Hello 페이지를 벗어나면 되 면 다시 표시 되지 않습니다.

    > [!IMPORTANT]
    > hello 암호가 중요 한 보안 자격 증명 합니다. 클라이언트 응용 프로그램 내에서 배포 하거나 hello 암호 다른 사람과 공유 하지 마십시오.

## <a name="secrets"></a>Microsoft 계정 추가 정보 tooyour 응용 프로그램 서비스 응용 프로그램
1. Hello에 다시 [Azure 포털]tooyour 응용 프로그램을 탐색, 클릭, **설정** > **인증 / 권한 부여**합니다.
2. 경우 hello 인증 / 권한 부여 기능은 활성화 되지 않으면, 전환 **에**합니다.
3. **Microsoft 계정**을 클릭합니다. 이전에 얻은 hello 응용 프로그램 ID 및 암호 값에 붙여 넣고 필요에 따라 응용 프로그램에 필요한 모든 범위를 사용 합니다. 그런 후 **OK**를 클릭합니다.
   
    ![][1]
   
    기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다. 앱 코드에서 사용자 권한을 부여해야 합니다.
4. (선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 Microsoft 계정에 의해 인증 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Microsoft 계정**합니다. 이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청을 리디렉션하 tooMicrosoft 계정 인증에 대 한 합니다.
5. **Save**를 클릭합니다.

이제 준비 toouse Microsoft 계정 인증에 대 한 응용 프로그램입니다.

## <a name="related-content"> </a>관련 콘텐츠
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[내 응용 프로그램]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure 포털]: https://portal.azure.com/
