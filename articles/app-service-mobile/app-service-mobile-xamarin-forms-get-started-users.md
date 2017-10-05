---
title: "Xamarin.Forms 앱에서 Mobile Apps에 대한 인증 시작 | Microsoft Docs"
description: "Mobile Apps를 사용하여 AAD, Google, Facebook, Twitter, Microsoft 등의 다양한 ID 공급자를 통해 Xamarin Forms 앱 사용자를 인증하는 방법을 알아봅니다."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="e497e-103">Xamarin Forms 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="e497e-104">개요</span><span class="sxs-lookup"><span data-stu-id="e497e-104">Overview</span></span>
<span data-ttu-id="e497e-105">이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 사용자를 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="e497e-106">이 자습서에서는 App Service가 지원하는 ID 공급자를 사용하여 Xamarin.Forms 빠른 시작 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="e497e-107">모바일 앱에서 인증이 완료되고 권한이 부여되고 나면 사용자 ID 값이 표시되고 제한된 테이블 데이터에 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e497e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e497e-108">Prerequisites</span></span>
<span data-ttu-id="e497e-109">이 자습서를 통한 최상의 결과를 얻기 위해 먼저 [Xamarin.Forms 앱 만들기][1] 자습서를 완료하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="e497e-110">이 자습서를 완료하면 다중 플랫폼 TodoList 앱인 Xamarin.Forms 프로젝트가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="e497e-111">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 인증 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="e497e-112">서버 확장 패키지에 대한 자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용][2]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e497e-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="e497e-113">인증을 위해 앱 등록 및 App Services 구성</span><span class="sxs-lookup"><span data-stu-id="e497e-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e497e-114"><a name="redirecturl"></a>허용되는 외부 리디렉션 URL에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="e497e-115">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e497e-116">이를 통해 인증 시스템은 인증 프로세스가 완료되면 앱으로 다시 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="e497e-117">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e497e-118">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e497e-119">이 체계는 모바일 응용 프로그램에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="e497e-120">서버 쪽에서 리디렉션을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="e497e-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="e497e-121">[Azure Portal]에서 해당 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e497e-122">**인증/권한 부여** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e497e-123">**허용되는 외부 리디렉션 URL**에서 `url_scheme_of_your_app://easyauth.callback`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e497e-124">이 문자열의 **url_scheme_of_your_app**은 모바일 응용 프로그램에 대한 URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e497e-125">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="e497e-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e497e-126">여러 위치에서 URL 체계에 따라 모바일 응용 프로그램 코드를 조정해야 할 경우 선택한 문자열을 적어두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="e497e-127">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-127">Click **OK**.</span></span>

5. <span data-ttu-id="e497e-128">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="e497e-129">사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="e497e-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="e497e-130">이식 가능한 클래스 라이브러리에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="e497e-131">Mobile Apps는 [MobileServiceClient][4]에서 [LoginAsync][3] 확장 메서드를 사용하여 App Service 인증으로 사용자를 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="e497e-132">이 샘플에서는 서버 관리 인증 흐름을 사용하여 앱에서 공급자의 로그인 인터페이스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="e497e-133">자세한 내용은 [서버 관리 인증][5]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e497e-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="e497e-134">프로덕션 앱에서 향상된 사용자 환경을 제공하기 위해 대신 [클라이언트 관리 인증][6]을 사용하는 것을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="e497e-135">Xamarin Forms 프로젝트를 사용하여 인증하기 위해서 앱에 대한 이식 가능한 클래스 라이브러리에 **IAuthenticate** 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="e497e-136">또한 이식 가능한 클래스 라이브러리에 정의된 사용자 인터페이스를 업데이트하여 **로그인** 단추를 추가합니다. 사용자는 이 단추를 클릭하여 인증을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="e497e-137">인증에 성공하면 Mobile App 백 엔드에서 데이터가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="e497e-138">앱에서 지원되는 각 플랫폼에 대해 **IAuthenticate** 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="e497e-139">Visual Studio 또는 Xamarin Studio에서 이름에 **이식 가능**이 있는 프로젝트(이식 가능한 클래스 라이브러리 프로젝트)에서 App.cs를 연 후 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="e497e-140">App.cs에 `App` 클래스 정의 직전에 다음과 같은 `IAuthenticate` 인터페이스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="e497e-141">플랫폼 전용 구현으로 인터페이스를 초기화하도록 **App** 클래스에 다음 정적 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="e497e-142">이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml을 열고 **buttonsPanel** 레이아웃 요소의 다음 *Button* 요소를 기존 단추 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="e497e-143">이 단추는 모바일 앱 백 엔드로 서버 관리 인증을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="e497e-144">이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml.cs를 연 후 다음 필드를 `TodoList` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="e497e-145">**OnAppearing** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="e497e-146">이렇게 코드를 변경하면 사용자가 인증된 후에만 데이터가 새로 고침됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="e497e-147">**TodoList** 클래스에 **Clicked** 이벤트에 대한 다음 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="e497e-148">변경 내용을 저장하고 이식 가능한 클래스 라이브러리 프로젝트를 다시 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="e497e-149">Android 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-149">Add authentication to the Android app</span></span>
<span data-ttu-id="e497e-150">이 섹션에는 Android 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="e497e-151">Android 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="e497e-152">Visual Studio 또는 Xamarin Studio에서 **droid** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e497e-153">F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e497e-154">백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e497e-155">Android 프로젝트에서 MainActivity.cs를 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="e497e-156">다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **MainActivity** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="e497e-157">다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **MainActivity** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="e497e-158">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider][7]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="e497e-159">AndroidManifest.xml의 <application> 노드 안에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="e497e-160">`LoadApplication()`에 대한 호출 이전에 **MainActivity** 클래스의 **OnCreate** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="e497e-161">이 코드를 사용하면 앱이 로드되기 전에 인증자가 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="e497e-162">앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="e497e-163">iOS 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="e497e-164">이 섹션에는 iOS 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="e497e-165">iOS 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="e497e-166">Visual Studio 또는 Xamarin Studio에서 **iOS** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e497e-167">F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e497e-168">백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 응답이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e497e-169">iOS 프로젝트에서 AppDelegate.cs를 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="e497e-170">다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **AppDelegate** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="e497e-171">다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **AppDelegate** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="e497e-172">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="e497e-173">OpenUrl(UIApplication 앱, NSUrl url NSDictionary 옵션) 메서드 오버로드를 추가하여 AppDelegate 클래스 업데이트</span><span class="sxs-lookup"><span data-stu-id="e497e-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="e497e-174">`LoadApplication()`에 대한 호출 이전에 **FinishedLaunching** 메서드에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="e497e-175">이 코드를 사용하면 앱이 로드되기 전에 인증자가 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="e497e-176">Info.plist의 URL 체계에 **{url_scheme_of_your_app}**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="e497e-177">앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="e497e-178">Windows 10(Phone 포함) 앱 프로젝트에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="e497e-179">이 섹션에는 Windows 10 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="e497e-180">동일한 단계가 UWP(유니버설 Windows 플랫폼) 프로젝트에도 적용되지만 **UWP** 프로젝트(명시된 변경 내용 포함)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="e497e-181">Windows 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="e497e-182">Visual Studio에서 **UWP** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e497e-183">F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e497e-184">백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e497e-185">Windows 앱 프로젝트에 대한 MainPage.xaml.cs를 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="e497e-186">`<your_Portable_Class_Library_namespace>` 를 이식 가능한 클래스 라이브러리의 네임스페이스로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="e497e-187">다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **MainPage** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="e497e-188">다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **MainPage** 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="e497e-189">Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="e497e-190">`LoadApplication()`에 대한 호출 이전에 **MainPage** 클래스에 대한 생성자에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="e497e-191">`<your_Portable_Class_Library_namespace>` 를 이식 가능한 클래스 라이브러리의 네임스페이스로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="e497e-192">**UWP**를 사용하는 경우 **App** 클래스에 다음 **OnActivated** 메서드 재정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="e497e-193">메서드 재정의가 이미 있는 경우 위의 코드 조각에서 조건부 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="e497e-194">이 코드는 유니버설 Windows 프로젝트에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="e497e-195">Package.appxmanifest에 **{url_scheme_of_your_app}**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="e497e-196">앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e497e-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e497e-197">Next steps</span></span>
<span data-ttu-id="e497e-198">이 기본 인증 자습서를 완료했으므로 다음 자습서 중 하나를 계속하는 것을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="e497e-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="e497e-199">앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="e497e-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="e497e-200">앱에 푸시 알림 지원을 추가하고 모바일 앱 백 엔드를 구성하여 푸시 알림을 보내는 Azure Notification Hubs를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="e497e-201">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="e497e-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="e497e-202">모바일 앱 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="e497e-203">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e497e-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
