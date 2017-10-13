---
title: "앱 서비스 응용 프로그램에 대해 Google 인증을 구성하는 방법"
description: "앱 서비스 응용 프로그램에 대해 Google 인증을 구성하는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a>Google 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

이 항목에서는 Google을 인증 공급자로 사용하도록 Azure 앱 서비스를 구성하는 방법을 보여 줍니다.

이 항목의 절차를 완료하려면 검증된 메일 주소가 포함된 Google 계정이 있어야 합니다. 새 Google 계정을 만들려면 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)으로 이동하십시오.

## <a name="register"> </a>Google을 사용하여 응용 프로그램 등록
1. [Azure 포털]에 로그온한 다음 응용 프로그램으로 이동합니다. **URL**을 복사하여 나중에 Google 앱을 구성하는 데 사용합니다.
2. [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) 웹 사이트로 이동하고 Google 계정 자격 증명으로 로그인하고 **프로젝트 만들기**를 클릭하고 **프로젝트 이름**을 입력한 후 **만들기**를 클릭합니다.
3. **Social APIs** 아래에서 **Google+ API**, **Enable**을 차례로 클릭합니다.
4. 왼쪽 탐색에서 **Credentials** > **OAuth consent screen**을 클릭하고 **Email address**를 선택한 다음 **Product Name**을 입력하고 **Save**를 클릭합니다.
5. **Credentials** 탭에서**Create credentials** > **OAuth client ID**를 클릭하고 **Web application**을 선택합니다.
6. 앞서 복사한 App Service **URL**을 **Authorized JavaScript Origins**에 붙여넣고, 리디렉션 URI를**Authorized Redirect URI**에 붙여넣습니다. 리디렉션 URI는 경로 */.auth/login/google/callback*이 추가된 응용 프로그램의 URL입니다. 예: `https://contoso.azurewebsites.net/.auth/login/google/callback` HTTPS 체계를 사용 중인지 확인합니다. 그런 다음 **Create**를 클릭합니다.
7. 다음 화면에서 클라이언트 ID 및 클라이언트 암호 값을 적어 둡니다.

    > [!IMPORTANT]
    > 클라이언트 암호는 중요한 보안 자격 증명입니다. 다른 사람과 이 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.


## <a name="secrets"> </a>응용 프로그램에 Google 정보 추가
1. [Azure 포털]로 돌아가서 응용 프로그램으로 이동합니다. **Settings**를 클릭한 다음 **Authentication / Authorization**을 클릭합니다.
2. 인증/권한 부여 기능이 사용하도록 설정되지 않은 경우 스위치를 **On**으로 전환합니다.
3. **Google**을 클릭합니다. 이전에 가져온 앱 ID 및 앱 암호 값을 붙여넣고 필요에 따라 응용 프로그램에 필요한 범위를 설정합니다. 그런 후 **OK**를 클릭합니다.
   
   ![][1]
   
   기본적으로 앱 서비스는 인증을 제공하지만 사이트 콘텐츠 및 API에 액세스하는 권한을 제한하지는 않습니다. 앱 코드에서 사용자 권한을 부여해야 합니다.
4. (선택 사항) Google에서 인증된 사용자만 사이트에 액세스하도록 제한하려면 **Google**에 **요청이 인증되지 않으면 수행할 동작**을 설정합니다. 이렇게 하려면 모든 요청이 인증되어야 하며 모든 인증되지 않은 요청은 인증을 위해 Google에 리디렉션되어야 합니다.
5. **Save**를 클릭합니다.

이제 앱에서 Google을 인증에 사용할 준비가 되었습니다.

## <a name="related-content"> </a>관련 콘텐츠
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 포털]: https://portal.azure.com/

