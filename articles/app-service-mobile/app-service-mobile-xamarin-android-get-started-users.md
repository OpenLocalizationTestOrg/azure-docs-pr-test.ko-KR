---
title: "Xamarin Android에 모바일 앱에 대 한 인증 aaaGet 시작 됨"
description: "자세한 내용은 방법 toouse 모바일 앱 tooauthenticate 사용자가 다양 한 AAD, Google, Facebook, Twitter 및 Microsoft를 포함 하 여 id 공급자를 통해 Xamarin Android 응용 프로그램의 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>인증 tooyour Xamarin.Android 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

이 항목에서는 클라이언트 응용 프로그램에서 모바일 앱의 tooauthenticate 사용자입니다. 이 자습서에서는 Azure 모바일 앱에서 지원 되는 id 공급자를 사용 하 여 인증 toohello 퀵 스타트 프로젝트를 추가 합니다. 인증 되 고 hello 모바일 앱에에서 권한이 성공적으로 되 고, 후 hello 사용자 ID 값이 표시 됩니다.

이 자습서는 hello 모바일 앱 빠른 시작을 기반으로 합니다. 먼저 hello 자습서를 마쳐야 [Xamarin.Android 앱 만들기]합니다. 사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 인증 확장 프로그램 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

## <a name="register"></a>인증을 위해 앱 등록 및 앱 서비스 구성
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

Visual Studio 또는 Xamarin Studio에서 장치 또는 에뮬레이터에 hello client 프로젝트를 실행 합니다. Hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다. 이 hello 앱 tooaccess 인증 되지 않은 사용자로 백 엔드 모바일 앱을 시도 하기 때문에 발생 합니다. hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.

다음으로 인증된 된 사용자와 hello 모바일 앱 백 엔드에서 hello 클라이언트 응용 프로그램 toorequest 리소스를 업데이트 합니다.

## <a name="add-authentication"></a>인증 toohello 앱 추가
hello 앱은 업데이트 된 toorequire 사용자 tootap hello **로그인** 단추 및 인증 데이터가 표시 됩니다.

1. 다음 코드 toohello hello 추가 **TodoActivity** 클래스:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    이 만들어지고 새 메서드 tooauthenticate 사용자 메서드 처리기에 대 한 새 **로그인** 단추입니다. 위의 hello 예제 코드에 hello 사용자는 Facebook 로그인을 사용 하 여 인증 됩니다. 대화는 인증 후 사용 되는 toodisplay hello 사용자 ID입니다.
   
   > [!NOTE]
   > Facebook 이외의 id 공급자를 사용 하는 경우 변경 너무 전달 된 값이 hello**LoginAsync** hello 다음의 tooone 위에: *MicrosoftAccount*, *Twitter*, *Google*, 또는 *WindowsAzureActiveDirectory*합니다.
   > 
   > 
2. Hello에 **OnCreate** 메서드, delete 또는 다음 코드 줄을 주석 아웃 hello:
   
        OnRefreshItemsSelected ();
3. Hello Activity_To_Do.axml 파일에 hello 다음 추가 *LoginUser* hello 기존 하기 전에 정의 단추 *AddItem* 단추:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Hello 다음 요소 toohello Strings.xml 리소스 파일을 추가 합니다.
   
        <string name="login_button_text">Sign in</string>
5. Hello AndroidManifest.xml 파일을 열고 내부에서 코드를 다음 hello 추가 `<application>` XML 요소:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. Visual Studio 또는 Xamarin Studio에서 장치 또는 에뮬레이터에서 hello client 프로젝트를 실행 하 고 선택한 id 공급자를 사용 하 여 로그인 합니다. 성공적으로 로그인 했으면 hello 앱 로그인 ID에 표시 됩니다 하 고 할 일 항목의 hello 목록은 업데이트 toohello 데이터를 만들 수 있습니다.

<!-- URLs. -->
[Xamarin.Android 앱 만들기]: app-service-mobile-xamarin-android-get-started.md