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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="8e590-103">인증 tooyour Xamarin Forms 앱 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="8e590-104">개요</span><span class="sxs-lookup"><span data-stu-id="8e590-104">Overview</span></span>
<span data-ttu-id="8e590-105">이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 tooauthenticate 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="8e590-106">이 자습서에서는 hello Xamarin Forms 퀵 스타트 프로젝트 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 인증을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="8e590-107">Hello 사용자 ID 값이 표시 되 고 인증 되 고 모바일 앱의 승인을, 후 하 고 제한 된 수 tooaccess 테이블 데이터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e590-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e590-108">Prerequisites</span></span>
<span data-ttu-id="8e590-109">이 자습서와 함께 최상의 결과 hello hello를 먼저 완료 하는 권장 [Xamarin Forms 응용 프로그램 만들기] [ 1] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="8e590-110">이 자습서를 완료하면 다중 플랫폼 TodoList 앱인 Xamarin.Forms 프로젝트가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="8e590-111">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 인증 확장 프로그램 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="8e590-112">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="8e590-113">인증을 위해 앱 등록 및 App Services 구성</span><span class="sxs-lookup"><span data-stu-id="8e590-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="8e590-114"><a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="8e590-115">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="8e590-116">Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="8e590-117">이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체.</span><span class="sxs-lookup"><span data-stu-id="8e590-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="8e590-118">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="8e590-119">고유 tooyour 모바일 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="8e590-120">hello 서버 쪽에서 tooenable hello 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="8e590-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="8e590-121">Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="8e590-122">Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="8e590-123">Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="8e590-124">hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="8e590-125">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="8e590-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="8e590-126">Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="8e590-127">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-127">Click **OK**.</span></span>

5. <span data-ttu-id="8e590-128">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="8e590-129">Tooauthenticated 사용자 사용 권한 제한</span><span class="sxs-lookup"><span data-stu-id="8e590-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="8e590-130">인증 toohello 이식 가능한 클래스 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="8e590-131">모바일 앱 hello를 사용 하 여 [LoginAsync] [ 3] hello에 대 한 확장 메서드 [MobileServiceClient] [ 4] toosign 앱 서비스와 사용자의 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="8e590-132">이 샘플에서는 hello 앱에 hello 공급자의 로그인 인터페이스를 표시 하는 서버 관리 인증 흐름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="8e590-133">자세한 내용은 [서버 관리 인증][5]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e590-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="8e590-134">프로덕션 앱에서 향상된 사용자 환경을 제공하기 위해 대신 [클라이언트 관리 인증][6]을 사용하는 것을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="8e590-135">Xamarin Forms 프로젝트와 tooauthenticate 정의 **IAuthenticate** hello 앱에 대 한 hello 이식 가능한 클래스 라이브러리에에서 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="8e590-136">그런 다음 추가 **로그인** hello 클릭할 수 있는 이식 가능한 클래스 라이브러리에에서 정의 된 단추 toohello 사용자 인터페이스 toostart 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="8e590-137">인증을 거친 후 hello 모바일 앱 백 엔드에서 데이터 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="8e590-138">구현 hello **IAuthenticate** 앱에서 지 원하는 각 플랫폼에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="8e590-139">Visual Studio 또는 Xamarin Studio에서 사용 하 여 hello 프로젝트를 App.cs를 열고 **휴대용** 이식 가능한 클래스 라이브러리 프로젝트는 hello 이름에 다음 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="8e590-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="8e590-140">Hello 다음 추가 App.cs에서 `IAuthenticate` 인터페이스 정의 바로 hello 앞 `App` 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="8e590-141">플랫폼별 구현을 tooinitialize hello 인터페이스 추가 다음 정적 멤버 toohello hello **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="8e590-142">Hello 다음 추가 hello 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml 열고 **단추** hello 요소 *buttonsPanel* hello 기존 단추 레이아웃 요소:</span><span class="sxs-lookup"><span data-stu-id="8e590-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="8e590-143">이 단추는 모바일 앱 백 엔드로 서버 관리 인증을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="8e590-144">Hello 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml.cs를 연 다음 필드 toohello 다음 hello 추가 `TodoList` 클래스:</span><span class="sxs-lookup"><span data-stu-id="8e590-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="8e590-145">Hello 대체 **OnAppearing** 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="8e590-145">Replace hello **OnAppearing** method with hello following code:</span></span>

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

    <span data-ttu-id="8e590-146">이 코드는 데이터를만 새로 고칠 hello 서비스에서 인증 된 후 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="8e590-147">Hello hello에 대 한 처리기를 다음 추가 **Clicked** 이벤트 toohello **TodoList** 클래스:</span><span class="sxs-lookup"><span data-stu-id="8e590-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="8e590-148">변경 내용을 저장 하 고 오류가 없는지 확인 하는 hello 이식 가능한 클래스 라이브러리 프로젝트를 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="8e590-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="8e590-149">인증 toohello Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="8e590-150">이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello Android 응용 프로그램 프로젝트에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="8e590-151">Android 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="8e590-152">Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **로봇** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8e590-153">Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외는 응용 프로그램 시작 후에 발생 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="8e590-154">hello 401 코드는 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="8e590-155">MainActivity.cs hello Android 프로젝트에서 열고 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="8e590-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="8e590-156">업데이트 hello **MainActivity** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="8e590-157">업데이트 hello **MainActivity** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate**  인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="8e590-158">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider][7]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="8e590-159">내 코드 다음 hello 추가 <application> AndroidManifest.xml의 노드:</span><span class="sxs-lookup"><span data-stu-id="8e590-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="8e590-160">다음 코드 toohello hello 추가 **OnCreate** hello 방식의 **MainActivity** hello 호출 전에 너무 클래스`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8e590-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="8e590-161">이 코드에서는 hello 인증자 hello 로드 하기 전에 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="8e590-162">Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="8e590-163">인증 toohello iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="8e590-164">이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello iOS 앱 프로젝트에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="8e590-165">iOS 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="8e590-166">Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **iOS** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8e590-167">Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="8e590-168">hello 401 응답 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 때문에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="8e590-169">AppDelegate.cs hello iOS 프로젝트에서 열고 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="8e590-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="8e590-170">업데이트 hello **AppDelegate** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="8e590-171">업데이트 hello **AppDelegate** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate**  인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="8e590-172">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="8e590-173">OpenUrl (UIApplication 응용 프로그램, NSUrl url NSDictionary 옵션) 메서드 오버 로드를 추가 하 여 hello AppDelegate 클래스 업데이트</span><span class="sxs-lookup"><span data-stu-id="8e590-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="8e590-174">다음 줄의 코드 toohello hello 추가 **FinishedLaunching** hello 먼저 메서드 호출을 통해서도`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8e590-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="8e590-175">이 코드에서는 hello 인증자 hello 앱 로드 되기 전에 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="8e590-176">추가 **{url_scheme_of_your_app}** Info.plist에서 tooURL 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="8e590-177">Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="8e590-178">인증 tooWindows 10 (Phone 포함)를 추가 응용 프로그램 프로젝트</span><span class="sxs-lookup"><span data-stu-id="8e590-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="8e590-179">이 섹션에서는 어떻게 tooimplement hello **IAuthenticate** hello Windows 10 앱 프로젝트에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="8e590-180">동일한 단계가 hello를 사용 하 여 유니버설 Windows 플랫폼 (UWP) 프로젝트에 적용 하는 hello **UWP** (위에 언급 변경과) 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="8e590-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="8e590-181">Windows 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="8e590-182">"Visual Studio에서 마우스 오른쪽 단추로 클릭 하거나 hello **UWP** 프로젝트, 다음 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8e590-183">Hello 디버거에서 toostart hello 프로젝트 F5 키를 눌러 다음 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="8e590-184">hello 401 응답 hello 백 엔드에 대 한 액세스는 제한 된 tooauthorized 사용자만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="8e590-185">MainPage.xaml.cs hello Windows 앱 프로젝트에 대 한 열고 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="8e590-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="8e590-186">대체 `<your_Portable_Class_Library_namespace>` 이식 가능한 클래스 라이브러리에 대 한 hello 네임 스페이스를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="8e590-187">업데이트 hello **MainPage** 클래스 tooimplement hello **IAuthenticate** 인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="8e590-188">업데이트 hello **MainPage** 클래스를 추가 하 여 한 **MobileServiceUser** 필드 및 **Authenticate** hello에 필요한 메서드를 **IAuthenticate** 인터페이스, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="8e590-189">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="8e590-190">Hello 다음 hello에 대 한 hello 생성자의 코드 줄을 추가 **MainPage** hello 호출 전에 너무 클래스`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8e590-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="8e590-191">대체 `<your_Portable_Class_Library_namespace>` 이식 가능한 클래스 라이브러리에 대 한 hello 네임 스페이스를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="8e590-192">사용 중인 경우 **UWP**, hello 다음 추가 **OnActivated** 메서드 재정의 toohello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="8e590-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="8e590-193">Hello 메서드 재정의 이미 있는 경우에서 코드 조각 앞 hello hello 조건부 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="8e590-194">이 코드는 유니버설 Windows 프로젝트에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="8e590-195">Package.appxmanifest에 **{url_scheme_of_your_app}**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="8e590-196">Hello 응용 프로그램을 다시 작성 하를 실행 한 후 hello 인증 공급자를 선택 하 고 인증된 된 사용자 수 tooaccess 데이터 확인을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e590-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e590-197">Next steps</span></span>
<span data-ttu-id="8e590-198">이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="8e590-199">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="8e590-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="8e590-200">Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 여 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend 푸시 알림을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="8e590-201">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="8e590-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="8e590-202">오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="8e590-203">오프 라인 동기화 최종 사용자가 toointeract 보기, 추가 또는 네트워크 연결이 없는 경우에 데이터 요금-수정-모바일 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e590-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
