---
title: "aaaAdd 인증 tooyour 유니버설 Windows 플랫폼 (UWP) 응용 프로그램 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure 앱 서비스 모바일 앱 tooauthenticate 사용자가 다양 한 비롯 한 id 공급자를 사용 하 여 유니버설 Windows 플랫폼 (UWP) 응용 프로그램의: AAD, Google, Facebook, Twitter 및 Microsoft 합니다."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>인증 tooyour Windows 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

이 항목에서는 tooadd 클라우드 기반 인증 tooyour 모바일 앱입니다. 이 자습서에서는 Azure 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 모바일 앱에 대 한 인증 toohello 유니버설 Windows 플랫폼 (UWP) 빠른 시작 프로젝트를 추가 합니다. 인증 되 고 모바일 앱 백엔드에서 권한이 성공적으로 되 고, 후 hello 사용자 ID 값이 표시 됩니다.

이 자습서는 hello 모바일 앱 빠른 시작을 기반으로 합니다. Hello 자습서를 먼저 완료 해야 [모바일 앱 시작](app-service-mobile-windows-store-dotnet-get-started.md)합니다.

## <a name="register"></a>인증에 대 한 앱을 등록 하 고 hello 응용 프로그램 서비스 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가

보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다. Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다. 이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체. 그러나 선택한 어떤 URL 체계도 사용 가능합니다. 고유 tooyour 모바일 응용 프로그램 이어야 합니다. hello 서버 쪽에서 tooenable hello 리디렉션:

1. Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.

2. Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.

3. Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.  hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.  이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).  Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.

4. **확인**을 클릭합니다.

5. **Save**를 클릭합니다.

## <a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

이제 해당 익명 액세스 tooyour 백 엔드 비활성화 됨을 확인할 수 있습니다. Hello 시작 프로젝트로 설정 hello UWP 앱 프로젝트를 배포 하 고 hello 응용 프로그램 실행 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다. Hello 앱 tooaccess 인증 되지 않은 사용자로 모바일 응용 프로그램 코드를 시도 하기 때문에이 문제가 발생 하지만 hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.

다음으로 응용 프로그램 서비스에서 리소스를 요청 하기 전에 hello 앱 tooauthenticate 사용자를 업데이트 합니다.

## <a name="add-authentication"></a>인증 toohello 앱 추가
1. Hello UWP 앱 프로젝트에서 MainPage.xaml.cs 파일 하 고 다음 코드 조각 hello를 추가 합니다.
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    이 코드는 Facebook 로그인 하 여 hello 사용자를 인증합니다. Facebook 이외의 id 공급자를 사용 하는 경우의 hello 값 변경 **MobileServiceAuthenticationProvider** 공급자 toohello 값을 초과 합니다.
2. Hello 대체 **OnNavigatedTo()** MainPage.xaml.cs에서 메서드. 추가한 다음으로 **로그인** 인증을 트리거하는 단추 toohello 응용 프로그램입니다.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. 다음 코드 조각 toohello MainPage.xaml.cs hello를 추가 합니다.
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Hello MainPage.xaml 프로젝트 파일을 열고 hello를 정의 하는 hello 요소를 찾습니다. **저장** 단추 및 코드 다음 hello로 바꿉니다.
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. 다음 코드 조각 toohello App.xaml.cs hello를 추가 합니다.

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Package.appxmanifest 파일을 열고 너무 탐색**선언**에 **사용 가능한 선언** 드롭다운 목록에서 선택 **프로토콜** 클릭 **추가** 단추입니다. 이제 hello 구성할 **속성** 의 hello **프로토콜** 선언 합니다. **표시 이름**, 응용 프로그램의 toodisplay toousers hello 이름을 추가 합니다. **이름**에 {url_scheme_of_your_app}를 추가합니다.
7. Hello F5 키 toorun hello 응용 프로그램 키를 눌러을 hello 클릭 **로그인** 단추 및 선택한 id 공급자와 hello 앱에 로그인 합니다. 로그인에 성공한 후 hello 앱 오류 없이 실행 되 고 백 엔드 수 tooquery 하 고 업데이트 toodata를 확인 합니다.

## <a name="tokens"></a>Hello 인증 토큰 hello 클라이언트에 저장
두 hello id 공급자는 표준 로그인, hello 클라이언트 toocontact 필요한 표시 하 고 hello 이러한 앱이 시작 될 때마다 응용 프로그램 서비스 hello 하는 hello 이전 예제입니다. 뿐만 아니라이 메서드를 비효율적으로 실행할 수 있습니다는로 사용-관련 문제는 고객이 많은 toostart 시도 hello에서 앱 같은 시간입니다. 더 나은 방법은 toocache hello 권한 부여에서 반환 된 토큰 응용 프로그램 서비스 및 try toouse이는 공급자 기반 로그인에 사용 하기 전에 먼저 합니다.

> [!NOTE]
> 클라이언트 관리 또는 서비스 관리 인증 사용 여부에 관계 없이 응용 프로그램 서비스에서 발급 하는 hello 토큰을 캐시할 수 있습니다. 이 자습서에서는 서비스 관리 인증을 사용합니다.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>다음 단계
이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.

* [푸시 알림 tooyour 앱 추가](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 여 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend 푸시 알림을 구성 합니다.
* [앱에 오프라인 동기화 사용](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  오프 라인 tooadd는 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다. 오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자에 게 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
