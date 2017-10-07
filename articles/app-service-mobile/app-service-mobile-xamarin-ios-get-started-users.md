---
title: "Xamarin iOS 모바일 앱에 대 한 인증 aaaGet 시작 됨"
description: "자세한 방법을 다양 한 AAD, Google, Facebook, Twitter 및 Microsoft를 포함 하 여 id 공급자를 통해 Xamarin iOS 앱의 toouse 모바일 앱 tooauthenticate 사용자입니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>인증 tooyour Xamarin.iOS 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 tooauthenticate 사용자입니다. 이 자습서에서는 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 인증 toohello Xamarin.iOS 퀵 스타트 프로젝트를 추가 합니다. Hello 사용자 ID 값이 표시 되 고 인증 되 고 모바일 앱의 승인을, 후 하 고 제한 된 수 tooaccess 테이블 데이터 됩니다.

Hello 자습서를 먼저 완료 해야 [Xamarin.iOS 앱 만들기]합니다. 사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 인증 확장 프로그램 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>인증을 위해 앱 등록 및 App Services 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가

보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다. Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다. 이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체. 그러나 선택한 어떤 URL 체계도 사용 가능합니다. 고유 tooyour 모바일 응용 프로그램 이어야 합니다. hello 서버 쪽에서 tooenable hello 리디렉션:

1. Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.

2. Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.

3. Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.  hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.  이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).  Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.

4. **확인**을 클릭합니다.

5. **Save**를 클릭합니다.

## <a name="restrict-permissions-tooauthenticated-users"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. Visual Studio 또는 Xamarin Studio에서 장치 또는 에뮬레이터에 hello client 프로젝트를 실행 합니다. Hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다. hello hello 디버거의 로깅된 toohello 콘솔입니다. 따라서 Visual Studio에서 hello 오류 hello 출력 창에 표시 됩니다.

&nbsp;&nbsp;인증 되지 않은 사용자로 모바일 앱 백 엔드 tooaccess 가져오려고 hello 앱이 무단된 오류가 발생 합니다. hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.

다음으로 인증된 된 사용자와 hello 모바일 앱 백 엔드에서 hello 클라이언트 응용 프로그램 toorequest 리소스를 업데이트 합니다.

## <a name="add-authentication-toohello-app"></a>인증 toohello 앱 추가
이 섹션에서는 데이터를 표시 하기 전에 hello 앱 toodisplay 로그인 화면을 수정 합니다. Hello 앱 시작 시 tooyour 앱 서비스 하지 연결 되지 않습니다를 데이터가 표시 되지 않습니다. Hello 처음으로 해당 hello 사용자를 수행한 다음 hello 새로 고침 제스처 hello 로그인 화면이 표시 됩니다. 성공적으로 로그인 한 후 hello 할 일 항목 목록이 표시 됩니다.

1. Hello 클라이언트 프로젝트를 열고 hello 파일 **QSTodoService.cs** hello 다음 추가 및 문을 사용 하 여 및 `MobileServiceUser` 접근자 toohello QSTodoService 클래스 사용:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. 라는 새 메서드 추가 **Authenticate** 너무**QSTodoService** 정의 뒤 hello로:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] Facebook 이외의 id 공급자를 사용 하는 경우 변경 너무 전달 된 값이 hello**LoginAsync** hello 다음의 tooone 위에: _MicrosoftAccount_, _Twitter_, _Google_, 또는 _WindowsAzureActiveDirectory_합니다.

3. **QSTodoListViewController.cs**를 엽니다. Hello 메서드 정의를 수정할 **ViewDidLoad** hello 호출 너무 제거**RefreshAsync()** hello 끝 근처에:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Hello 방법을 수정 **RefreshAsync** tooauthenticate 경우 hello **사용자** 속성이 null입니다. Hello 코드 hello 메서드 정의의 hello 위쪽에 다음을 추가 합니다.
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. 열기 **AppDelegate.cs**, hello 메서드 뒤에 추가 합니다.

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. 열기 **Info.plist** 파일, 너무 탐색**URL 형식** hello에 **고급** 섹션. 이제 hello 구성할 **식별자** 및 hello **URL 스키마** URL 형식과 클릭 **URL 형식 추가**합니다. **URL 스키마** {url_scheme_of_your_app}로 hello 동일 해야 합니다.
7. Visual Studio 또는 Xamarin Studio tooyour 장치 또는 에뮬레이터를 대상으로 하는 hello 클라이언트 프로젝트를 실행 하려면 Mac에서 Xamarin 빌드 호스트 연결 되어 있습니다. Hello 앱 데이터가 표시 되지 않습니다 확인 합니다.
   
    Hello hello 로그인 화면 tooappear 발생 하는 항목 목록을 아래로 잡아당겨 hello 새로 고침 제스처를 수행 합니다. 성공적으로 유효한 자격 증명을 입력 하 고 나면 hello 앱 hello 할 일 항목 목록이 표시 됩니다 하 고 업데이트 toohello 데이터를 만들 수 있습니다.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Xamarin.iOS 앱 만들기]: app-service-mobile-xamarin-ios-get-started.md