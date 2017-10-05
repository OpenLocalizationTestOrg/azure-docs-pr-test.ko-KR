---
title: "Xamarin iOS에서 모바일 앱에 대한 인증 시작"
description: "모바일 앱을 사용하여 AAD, Google, Facebook, Twitter, Microsoft 등의 다양한 ID 공급자를 통해 Xamarin iOS 앱 사용자를 인증하는 방법을 알아봅니다."
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="778a3-103">Xamarin.iOS 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="778a3-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="778a3-104">이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 사용자를 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="778a3-105">이 자습서에서는 앱 서비스가 지원하는 ID 공급자를 사용하여 Xamarin.iOS 빠른 시작 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="778a3-106">모바일 앱에서 인증이 완료되고 권한이 부여되고 나면 사용자 ID 값이 표시되고 제한된 테이블 데이터에 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="778a3-107">[Xamarin.iOS 앱 만들기]자습서를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="778a3-108">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 인증 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="778a3-109">서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="778a3-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="778a3-110">인증을 위해 앱 등록 및 앱 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="778a3-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="778a3-111">허용되는 외부 리디렉션 URL에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="778a3-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="778a3-112">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="778a3-113">이를 통해 인증 시스템은 인증 프로세스가 완료되면 앱으로 다시 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="778a3-114">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="778a3-115">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="778a3-116">이 체계는 모바일 응용 프로그램에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="778a3-117">서버 쪽에서 리디렉션을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="778a3-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="778a3-118">[Azure Portal]에서 해당 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="778a3-119">**인증/권한 부여** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="778a3-120">**허용되는 외부 리디렉션 URL**에서 `url_scheme_of_your_app://easyauth.callback`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="778a3-121">이 문자열의 **url_scheme_of_your_app**은 모바일 응용 프로그램에 대한 URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="778a3-122">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="778a3-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="778a3-123">여러 위치에서 URL 체계에 따라 모바일 응용 프로그램 코드를 조정해야 할 경우 선택한 문자열을 적어두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="778a3-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-124">Click **OK**.</span></span>

5. <span data-ttu-id="778a3-125">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="778a3-126">사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="778a3-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="778a3-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="778a3-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="778a3-128">Visual Studio 또는 Xamarin Studio에서 클라이언트 프로젝트를 장치 또는 에뮬레이터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="778a3-129">앱 시작 후 상태 코드가 401(권한이 부여되지 않음)인 처리되지 않은 예외가 발생했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="778a3-130">오류는 디버거의 콘솔에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="778a3-131">따라서 Visual Studio의 출력 창에 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="778a3-132">&nbsp;&nbsp;이 권한 없음 오류는 앱이 인증되지 않은 사용자로 모바일 앱 백엔드에 액세스하려고 하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="778a3-133">*TodoItem* 테이블에서 이제 인증을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="778a3-134">다음으로 클라이언트 앱을 업데이트하여 모바일 앱 백엔드에서 인증된 된 사용자를 사용하여 리소스를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="778a3-135">앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="778a3-135">Add authentication to the app</span></span>
<span data-ttu-id="778a3-136">이 섹션에서는 데이터 표시 전에 로그인 화면을 표시하도록 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="778a3-137">앱이 시작될 때 앱은 앱 서비스에 연결하지 않으며, 데이터를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="778a3-138">사용자가 새로 고침 제스처를 처음 수행한 다음 로그인 화면이 나타나고, 로그인이 성공하면 todo 항목 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="778a3-139">클라이언트 프로젝트에서 QSTodoService 클래스에 문 및 접근자가 있는 `MobileServiceUser`를 사용하여 **QSTodoService.cs** 파일을 열고 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="778a3-140">다음 정의를 포함하여 새 메서드로 명명된 **Authenticate**를 **QSTodoService**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="778a3-141">Facebook 이외의 ID 공급자를 사용하는 경우, 위의 **LoginAsync**에 전달된 값을 _MicrosoftAccount_, _Twitter_, _Google_ 또는 _WindowsAzureActiveDirectory_ 중 하나로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="778a3-142">**QSTodoListViewController.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="778a3-143">끝 부근의 **RefreshAsync()** 호출을 제거하여 **ViewDidLoad**의 메서드 정의를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="778a3-144">**User** 속성이 null인 경우 인증을 수행하려면 **RefreshAsync** 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="778a3-145">메서드 정의 상단에서 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="778a3-146">**AppDelegate.cs**를 열고 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="778a3-147">**Info.plist** 파일을 열고 **고급** 섹션의 **URL 형식**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="778a3-148">이제 URL 형식의 **식별자** 및 **URL 스키마**를 구성하고 **URL 형식 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="778a3-149">**URL 스키마**는 {url_scheme_of_your_app}와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="778a3-150">Mac 컴퓨터의 Xamarin 빌드 호스트에 연결된 Visual Studio 또는 Xamarin Studio에서 장치 또는 에뮬레이터를 대상으로 하는 클라이언트 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="778a3-151">앱이 데이터를 표시하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="778a3-152">항목 목록을 아래로 끌어서 새로 고침 제스처를 수행하고 로그인 화면이 나타나도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="778a3-153">유효한 자격 증명을 성공적으로 입력하면 앱이 todo 항목 목록을 표시하고 사용자가 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="778a3-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="778a3-154">[Xamarin.iOS 앱 만들기]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="778a3-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>