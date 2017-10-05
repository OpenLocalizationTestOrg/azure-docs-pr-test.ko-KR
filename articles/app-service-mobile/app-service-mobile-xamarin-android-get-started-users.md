---
title: "Xamarin Android에서 모바일 앱에 대한 인증 시작"
description: "모바일 앱을 사용하여 AAD, Google, Facebook, Twitter, Microsoft 등의 다양한 ID 공급자를 통해 Xamarin Android 앱 사용자를 인증하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="74d03-103">Xamarin Android 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="74d03-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="74d03-104">이 항목에서는 클라이언트 응용 프로그램에서 모바일 앱의 사용자를 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="74d03-105">이 자습서에서는 Azure 모바일 앱이 지원하는 ID 공급자를 사용하여 퀵 스타트 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="74d03-106">모바일 앱에서 인증되고 권한이 부여된 후 사용자 ID 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="74d03-107">이 자습서는 모바일 앱 퀵 스타트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="74d03-108">또한 [Xamarin Android 앱 만들기]자습서를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="74d03-109">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 인증 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="74d03-110">서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74d03-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="74d03-111"><a name="register"></a>인증을 위해 앱 등록 및 앱 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="74d03-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="74d03-112"><a name="redirecturl"></a>허용되는 외부 리디렉션 URL에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="74d03-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="74d03-113">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="74d03-114">이를 통해 인증 시스템은 인증 프로세스가 완료되면 앱으로 다시 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="74d03-115">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="74d03-116">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="74d03-117">이 체계는 모바일 응용 프로그램에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="74d03-118">서버 쪽에서 리디렉션을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="74d03-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="74d03-119">[Azure Portal]에서 해당 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="74d03-120">**인증/권한 부여** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="74d03-121">**허용되는 외부 리디렉션 URL**에서 `url_scheme_of_your_app://easyauth.callback`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="74d03-122">이 문자열의 **url_scheme_of_your_app**은 모바일 응용 프로그램에 대한 URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="74d03-123">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="74d03-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="74d03-124">여러 위치에서 URL 체계에 따라 모바일 응용 프로그램 코드를 조정해야 할 경우 선택한 문자열을 적어두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="74d03-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-125">Click **OK**.</span></span>

5. <span data-ttu-id="74d03-126">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-126">Click **Save**.</span></span>

## <span data-ttu-id="74d03-127"><a name="permissions"></a>사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="74d03-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="74d03-128">Visual Studio 또는 Xamarin Studio에서 클라이언트 프로젝트를 장치 또는 에뮬레이터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="74d03-129">앱 시작 후 상태 코드가 401(권한이 부여되지 않음)인 처리되지 않은 예외가 발생했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="74d03-130">이 예외는 앱이 인증되지 않은 사용자로 모바일 앱 백 엔드에 액세스하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="74d03-131">*TodoItem* 테이블에서 이제 인증을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="74d03-132">다음으로 클라이언트 앱을 업데이트하여 모바일 앱 백엔드에서 인증된 된 사용자를 사용하여 리소스를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="74d03-133"><a name="add-authentication"></a>앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="74d03-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="74d03-134">앱은 데이터가 표시되기 전에 사용자가 **로그인** 단추를 탭하고 인증하는 것을 요구하도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="74d03-135">**TodoActivity** 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-135">Add the following code to the **TodoActivity** class:</span></span>
   
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
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="74d03-136">이렇게 하면 사용자를 인증하는 새 메서드와 새 **로그인** 단추에 대한 메서드 처리기가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="74d03-137">위 예제 코드의 사용자는 Facebook 로그인을 사용하여 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="74d03-138">대화 상자는 한 번 인증된 사용자 ID를 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="74d03-139">Facebook 이외의 ID 공급자를 사용하는 경우, 위의 **LoginAsync**에 전달된 값을 *MicrosoftAccount*, *Twitter*, *Google* 또는 *WindowsAzureActiveDirectory* 중 하나로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="74d03-140">**OnCreate** 메서드에서 다음 코드 줄을 삭제하거나 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="74d03-141">Activity_To_Do.axml 파일에서 기존의 *AddItem* 단추 전에 다음 *LoginUser* 단추 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="74d03-142">Strings.xml 리소스 파일에 다음 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="74d03-143">AndroidManifest.xml 파일을 열고 `<application>` XML 요소 내에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="74d03-144">Visual Studio 또는 Xamarin Studio에서 클라이언트 프로젝트를 장치 또는 에뮬레이터에서 실행하고 선택된 ID 공급자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="74d03-145">성공적으로 로그인하면 앱이 로그인 ID 및 todo 항목 목록을 표시하고 사용자가 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74d03-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="74d03-146">[Xamarin Android 앱 만들기]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="74d03-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>