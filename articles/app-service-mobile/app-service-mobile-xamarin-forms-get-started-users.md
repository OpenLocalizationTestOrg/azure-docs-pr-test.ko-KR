---
title: "Xamarin Forms 앱에서 모바일 앱에 대 한 인증으로 시작 됨 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toouse 모바일 앱 tooauthenticate 사용자가 다양 한 AAD, Google, Facebook, Twitter 및 Microsoft를 포함 하 여 id 공급자를 통해 Xamarin Forms 응용 프로그램의 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>인증 tooyour Xamarin Forms 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>개요
이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 tooauthenticate 사용자입니다. 이 자습서에서는 hello Xamarin Forms 퀵 스타트 프로젝트 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 인증을 추가 합니다. Hello 사용자 ID 값이 표시 되 고 인증 되 고 모바일 앱의 승인을, 후 하 고 제한 된 수 tooaccess 테이블 데이터 됩니다.

## <a name="prerequisites"></a>필수 조건
이 자습서와 함께 최상의 결과 hello hello를 먼저 완료 하는 권장 [Xamarin Forms 응용 프로그램 만들기] [ 1] 자습서입니다. 이 자습서를 완료하면 다중 플랫폼 TodoList 앱인 Xamarin.Forms 프로젝트가 생깁니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 인증 확장 프로그램 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][2]합니다.

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>인증을 위해 앱 등록 및 App Services 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가

보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다. Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다. 이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체. 그러나 선택한 어떤 URL 체계도 사용 가능합니다. 고유 tooyour 모바일 응용 프로그램 이어야 합니다. hello 서버 쪽에서 tooenable hello 리디렉션:

1. Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.

2. Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.

3. Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.  hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.  이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).  Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.

4. **확인**을 클릭합니다.

5. **Save**를 클릭합니다.

## <a name="restrict-permissions-tooauthenticated-users"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>인증 toohello 이식 가능한 클래스 라이브러리 추가
모바일 앱 hello를 사용 하 여 [LoginAsync] [ 3] hello에 대 한 확장 메서드 [MobileServiceClient] [ 4] toosign 앱 서비스와 사용자의 인증입니다. 이 샘플에서는 hello 앱에 hello 공급자의 로그인 인터페이스를 표시 하는 서버 관리 인증 흐름을 사용 합니다. 자세한 내용은 [서버 관리 인증][5]을 참조하세요. 프로덕션 앱에서 향상된 사용자 환경을 제공하기 위해 대신 [클라이언트 관리 인증][6]을 사용하는 것을 고려할 수 있습니다.

Xamarin Forms 프로젝트와 tooauthenticate 정의 **IAuthenticate** hello 앱에 대 한 hello 이식 가능한 클래스 라이브러리에에서 대 한 인터페이스입니다. 그런 다음 추가 **로그인** hello 클릭할 수 있는 이식 가능한 클래스 라이브러리에에서 정의 된 단추 toohello 사용자 인터페이스 toostart 인증 합니다. 인증을 거친 후 hello 모바일 앱 백 엔드에서 데이터 로드 됩니다.

구현 hello **IAuthenticate** 앱에서 지 원하는 각 플랫폼에 대 한 인터페이스입니다.

1. Visual Studio 또는 Xamarin Studio에서 사용 하 여 hello 프로젝트를 App.cs를 열고 **휴대용** 이식 가능한 클래스 라이브러리 프로젝트는 hello 이름에 다음 hello 다음 추가 `using` 문:

        using System.Threading.Tasks;
2. Hello 다음 추가 App.cs에서 `IAuthenticate` 인터페이스 정의 바로 hello 앞 `App` 클래스 정의 합니다.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. 플랫폼별 구현을 tooinitialize hello 인터페이스 추가 다음 정적 멤버 toohello hello **앱** 클래스입니다.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Hello 다음 추가 hello 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml 열고 **단추** hello 요소 *buttonsPanel* hello 기존 단추 레이아웃 요소:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    이 단추는 모바일 앱 백 엔드로 서버 관리 인증을 트리거합니다.
5. Hello 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml.cs를 연 다음 필드 toohello 다음 hello 추가 `TodoList` 클래스:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Hello 대체 **OnAppearing** 메서드 코드 다음 hello로:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    이 코드는 데이터를만 새로 고칠 hello 서비스에서 인증 된 후 않았는지 확인 합니다.
7. Hello hello에 대 한 처리기를 다음 추가 **Clicked** 이벤트 toohello **TodoList** 클래스:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. 변경 내용을 저장 하 고 오류가 없는지 확인 하는 hello 이식 가능한 클래스 라이브러리 프로젝트를 다시 빌드하십시오.

## <a name="add-authentication-toohello-android-app"></a>인증 toohello Android 앱 추가
이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello Android 응용 프로그램 프로젝트에 대 한 인터페이스입니다. Android 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **로봇** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.
2. Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외는 응용 프로그램 시작 후에 발생 있는지 확인 합니다. hello 401 코드는 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 때문에 발생 합니다.
3. MainActivity.cs hello Android 프로젝트에서 열고 hello 다음 추가 `using` 문:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 업데이트 hello **MainActivity** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. 업데이트 hello **MainActivity** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate**  인터페이스, 다음과 같습니다.

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider][7]에 대해 다른 값을 선택합니다.

6. 내 코드 다음 hello 추가 <application> AndroidManifest.xml의 노드:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. 다음 코드 toohello hello 추가 **OnCreate** hello 방식의 **MainActivity** hello 호출 전에 너무 클래스`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    이 코드에서는 hello 인증자 hello 로드 하기 전에 초기화 됩니다.
2. Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.

## <a name="add-authentication-toohello-ios-app"></a>인증 toohello iOS 앱 추가
이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello iOS 앱 프로젝트에 대 한 인터페이스입니다. iOS 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **iOS** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.
2. Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다. hello 401 응답 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 때문에 생성 됩니다.
3. AppDelegate.cs hello iOS 프로젝트에서 열고 hello 다음 추가 `using` 문:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 업데이트 hello **AppDelegate** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. 업데이트 hello **AppDelegate** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate**  인터페이스, 다음과 같습니다.

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.

6. OpenUrl (UIApplication 응용 프로그램, NSUrl url NSDictionary 옵션) 메서드 오버 로드를 추가 하 여 hello AppDelegate 클래스 업데이트

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. 다음 줄의 코드 toohello hello 추가 **FinishedLaunching** hello 먼저 메서드 호출을 통해서도`LoadApplication()`:

        App.Init(this);

    이 코드에서는 hello 인증자 hello 앱 로드 되기 전에 초기화 됩니다.

6. 추가 **{url_scheme_of_your_app}** Info.plist에서 tooURL 구성표입니다.

7. Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>인증 tooWindows 10 (Phone 포함)를 추가 응용 프로그램 프로젝트
이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello Windows 10 앱 프로젝트에 대 한 인터페이스입니다. 동일한 단계가 hello를 사용 하 여 유니버설 Windows 플랫폼 (UWP) 프로젝트에 적용 하는 hello **UWP** (위에 언급 변경과) 프로젝트. Windows 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. "Visual Studio에서 마우스 오른쪽 단추로 클릭 하거나 hello **UWP** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.
2. Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다. hello 401 응답 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 발생 합니다.
3. MainPage.xaml.cs hello Windows 앱 프로젝트에 대 한 열고 hello 다음 추가 `using` 문:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    대체 `<your_Portable_Class_Library_namespace>` 이식 가능한 클래스 라이브러리에 대 한 hello 네임 스페이스를 가진 합니다.
4. 업데이트 hello **MainPage** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.

        public sealed partial class MainPage : IAuthenticate
5. 업데이트 hello **MainPage** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate** 인터페이스, 다음과 같습니다.

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.

1. Hello 다음 hello에 대 한 hello 생성자의 코드 줄을 추가 **MainPage** hello 호출 전에 너무 클래스`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    대체 `<your_Portable_Class_Library_namespace>` 이식 가능한 클래스 라이브러리에 대 한 hello 네임 스페이스를 가진 합니다.

3. 사용 중인 경우 **UWP**, hello 다음 추가 **OnActivated** 메서드 재정의 toohello **앱** 클래스:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Hello 메서드 재정의 이미 있는 경우에서 코드 조각 앞 hello hello 조건부 코드를 추가 합니다.  이 코드는 유니버설 Windows 프로젝트에는 필요하지 않습니다.

3. Package.appxmanifest에 **{url_scheme_of_your_app}**을 추가합니다. 

4. Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.

## <a name="next-steps"></a>다음 단계
이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.

* [푸시 알림 tooyour 앱 추가](app-service-mobile-xamarin-forms-get-started-push.md)

  Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 여 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend 푸시 알림을 구성 합니다.
* [앱에 오프라인 동기화 사용](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다. 오프 라인 동기화 최종 사용자가 toointeract 보기, 추가 또는 네트워크 연결이 없는 경우에 데이터 요금-수정-모바일 앱을 허용 합니다.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
