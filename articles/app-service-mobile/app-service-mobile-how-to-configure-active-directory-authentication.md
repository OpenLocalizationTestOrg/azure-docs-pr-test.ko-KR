---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Azure Active Directory 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 Azure Active Directory 인증 tooconfigure 합니다."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

이 항목에서는 Azure Active Directory를 인증 공급자로 tooconfigure Azure 앱 서비스 toouse 합니다.

## <a name="express"> </a>기본 설정을 사용하여 Azure Active Directory 구성
1. Hello에 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. **설정**을 클릭한 다음 **인증/권한 부여**를 클릭합니다.
2. 경우 hello 인증 / 권한 부여 기능은 활성화 되지 않으면, 너무 hello 스위치 설정**에**합니다.
3. **Azure Active Directory**를 클릭한 다음 **관리 모드**에서 **Express**를 클릭합니다.
4. 클릭 **확인** tooregister hello 응용 프로그램을 Azure Active Directory에 있습니다. 이렇게 하면 새롭게 등록됩니다. Toochoose 기존 등록을 대신 원하는 클릭 **기존 앱 선택** 한 다음 테 넌 트 내에서 이전에 만든된 등록의 hello 이름을 검색 합니다.
   누릅니다 hello 등록 tooselect 클릭 **확인**합니다. 클릭 **확인** hello Azure Active Directory 설정 블레이드에서 합니다.
   
   ![][0]
   
   기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다. 앱 코드에서 사용자 권한을 부여해야 합니다.
5. Azure Active Directory에 의해 인증 (선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Azure Active Directory로 로그인**합니다. 이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청은 인증에 대 한 리디렉션된 tooAzure Active Directory 키를 누릅니다.
6. **Save**를 클릭합니다.

이제 준비 toouse Azure Active Directory 인증을 위해 응용 프로그램입니다.

## <a name="advanced"> </a>(대체 방법) 고급 설정을 사용하여 Azure Active Directory를 수동으로 구성
선택할 수도 있습니다 tooprovide 구성 설정을 수동으로 합니다. Hello AAD 테 넌 트 toouse 원하는 hello Azure에 로그인을 테 넌 트 간에 차이가 있는 경우 기본 설정 hello 솔루션입니다. toocomplete hello 구성 먼저 만들어야을 등록 하는 Azure Active Directory에서 및 hello 등록 세부 정보 tooApp 서비스 중 일부를 제공 해야 합니다.

### <a name="register"> </a>Azure Active Directory에 응용 프로그램 등록
1. Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. **URL**을 복사합니다. Azure Active Directory 앱이이 tooconfigure를 사용 합니다.
2. Toohello 로그인 [Azure 클래식 포털] 너무 이동**Active Directory**합니다.
   
    ![][2]
3. 디렉터리를 선택한 다음 선택 hello **응용 프로그램** hello 위쪽 탭 합니다. 클릭 **추가** hello 아래쪽 toocreate 새 응용 프로그램 등록에 있습니다.
4. **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.
5. Hello 추가 응용 프로그램 마법사에서 입력 한 **이름** 응용 프로그램과 클릭 hello에 대 한 **웹 응용 프로그램 및/또는 웹 API** 유형입니다. Toocontinue을 클릭 합니다.
6. Hello에 **로그온 URL** 상자 앞에서 복사한 hello 응용 프로그램 URL을 붙여넣습니다. Hello에 해당 동일한 URL을 입력 **앱 ID URI** 상자입니다. Toocontinue을 클릭 합니다.
7. Hello 응용 프로그램 추가 되 면 클릭 hello **구성** 탭 합니다. Hello 편집 **회신 URL** 아래 **Single Sign on** hello 경로 추가 되므로 응용 프로그램의 toobe hello URL */.auth/login/aad/callback*합니다. 예: `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.
   
    ![][3]
8. **Save**를 클릭합니다. 그런 다음 복사본 hello **클라이언트 ID** hello 앱에 대 한 합니다. 응용 프로그램 toouse 구성한 나중에이 있습니다.
9. Hello 맨 아래 명령 모음에서 **끝점 보기**, 한 다음 복사 hello **페더레이션 메타 데이터 문서** URL 및 브라우저에서 tooit 이동 하거나 기존 문서를 다운로드 합니다.
10. Hello 루트 **EntityDescriptor** 요소 있어야는 **entityID** hello 폼의 특성 `https://sts.windows.net/` 뒤에 GUID 특정 tooyour 테 넌 트 ("테 넌 트 ID" 라고 함). 이 값을 복사하여 **발급자 URL**로 사용합니다. 응용 프로그램 toouse 구성한 나중에이 있습니다.

### <a name="secrets"></a>추가 Azure Active Directory 정보 tooyour 응용 프로그램
1. Hello에 다시 [Azure 포털], tooyour 응용 프로그램을 이동 합니다. **설정**을 클릭한 다음 **인증/권한 부여**를 클릭합니다.
2. Hello 인증/권한 부여 기능은 사용 하지 않는 경우 hello 스위치를 너무 끄려면**에**합니다.
3. **Azure Active Directory**를 클릭한 다음 **관리 모드**에서 **고급**을 클릭합니다. Hello 클라이언트 ID의에서 붙여넣기, 발급자 URL 어떤 것을 이전에 얻은 값. 그런 후 **OK**를 클릭합니다.
   
   ![][1]
   
   기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다. 앱 코드에서 사용자 권한을 부여해야 합니다.
4. Azure Active Directory에 의해 인증 (선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Azure Active Directory로 로그인**합니다. 이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청은 인증에 대 한 리디렉션된 tooAzure Active Directory 키를 누릅니다.
5. **Save**를 클릭합니다.

이제 준비 toouse Azure Active Directory 인증을 위해 응용 프로그램입니다.

## <a name="optional-configure-a-native-client-application"></a>(옵션) 네이티브 클라이언트 응용 프로그램 구성
Azure Active Directory 또한 있습니다 tooregister 네이티브 클라이언트를 매핑 사용 권한 보다 큰 제어를 제공 하는. Hello 같은 라이브러리를 사용 하 여 tooperform 로그인 하려는 경우 필요한이 **Active Directory 인증 라이브러리**합니다.

1. 너무 이동**Active Directory** hello에 [Azure 클래식 포털]합니다.
2. 디렉터리를 선택한 다음 선택 hello **응용 프로그램** hello 위쪽 탭 합니다. 클릭 **추가** hello 아래쪽 toocreate 새 응용 프로그램 등록에 있습니다.
3. **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.
4. Hello 추가 응용 프로그램 마법사에서 입력 한 **이름** 응용 프로그램과 클릭 hello에 대 한 **네이티브 클라이언트 응용 프로그램** 유형입니다. Toocontinue을 클릭 합니다.
5. Hello에 **리디렉션 URI** 상자에 입력 하면 사이트의 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다. 이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다. Windows 응용 프로그램을 만드는 경우 대신 사용 하 여 hello [패키지 SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) URI hello으로 합니다.
6. Hello 네이티브 응용 프로그램 추가 되 면 클릭 hello **구성** 탭 합니다. Hello **클라이언트 ID** 이 값을 기록 합니다.
7. Hello 페이지 toohello 아래로 스크롤 **tooother 응용 프로그램 사용 권한** 섹션 및 클릭 **응용 프로그램을 추가**합니다.
8. 이전에 등록 하는 hello 웹 응용 프로그램 검색 하 고 hello 더하기 아이콘을 클릭 합니다. Hello 검사 tooclose hello 대화 상자를 클릭 합니다. Hello 웹 응용 프로그램 찾을 tooits 등록 이동한 새 회신 URL (예: hello HTTP 버전의 현재 URL)를 추가할 수 없으므로, 저장을 클릭 한 다음 이러한 단계를 반복-hello 응용 프로그램 hello 목록에 표시 해야 합니다.
9. 방금 추가한 hello 새 항목을 열고 hello **위임 된 권한** 드롭다운을 선택 하 고 **액세스 (appName)**합니다. 그런 다음 **Save**를 클릭합니다.

이제 앱 서비스 응용 프로그램에 액세스할 수 있는 네이티브 클라이언트 응용 프로그램을 구성했습니다.

## <a name="related-content"> </a>관련 콘텐츠
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[Azure 포털]: https://portal.azure.com/
[Azure 클래식 포털]: https://manage.windowsazure.com/
[alternative method]:#advanced
