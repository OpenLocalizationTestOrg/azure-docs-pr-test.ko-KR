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
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="319cd-103">인증 tooyour Xamarin.iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="319cd-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="319cd-104">이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 tooauthenticate 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="319cd-105">이 자습서에서는 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 인증 toohello Xamarin.iOS 퀵 스타트 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="319cd-106">Hello 사용자 ID 값이 표시 되 고 인증 되 고 모바일 앱의 승인을, 후 하 고 제한 된 수 tooaccess 테이블 데이터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="319cd-107">Hello 자습서를 먼저 완료 해야 [Xamarin.iOS 앱 만들기]합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="319cd-108">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 인증 확장 프로그램 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="319cd-109">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="319cd-110">인증을 위해 앱 등록 및 App Services 구성</span><span class="sxs-lookup"><span data-stu-id="319cd-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="319cd-111">응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가</span><span class="sxs-lookup"><span data-stu-id="319cd-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="319cd-112">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="319cd-113">Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="319cd-114">이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체.</span><span class="sxs-lookup"><span data-stu-id="319cd-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="319cd-115">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="319cd-116">고유 tooyour 모바일 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="319cd-117">hello 서버 쪽에서 tooenable hello 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="319cd-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="319cd-118">Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="319cd-119">Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="319cd-120">Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="319cd-121">hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="319cd-122">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="319cd-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="319cd-123">Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="319cd-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-124">Click **OK**.</span></span>

5. <span data-ttu-id="319cd-125">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="319cd-126">Tooauthenticated 사용자 사용 권한 제한</span><span class="sxs-lookup"><span data-stu-id="319cd-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="319cd-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="319cd-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="319cd-128">Visual Studio 또는 Xamarin Studio에서 장치 또는 에뮬레이터에 hello client 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="319cd-129">Hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="319cd-130">hello hello 디버거의 로깅된 toohello 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="319cd-131">따라서 Visual Studio에서 hello 오류 hello 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="319cd-132">&nbsp;&nbsp;인증 되지 않은 사용자로 모바일 앱 백 엔드 tooaccess 가져오려고 hello 앱이 무단된 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="319cd-133">hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="319cd-134">다음으로 인증된 된 사용자와 hello 모바일 앱 백 엔드에서 hello 클라이언트 응용 프로그램 toorequest 리소스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="319cd-135">인증 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="319cd-135">Add authentication toohello app</span></span>
<span data-ttu-id="319cd-136">이 섹션에서는 데이터를 표시 하기 전에 hello 앱 toodisplay 로그인 화면을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="319cd-137">Hello 앱 시작 시 tooyour 앱 서비스 하지 연결 되지 않습니다를 데이터가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="319cd-138">Hello 처음으로 해당 hello 사용자를 수행한 다음 hello 새로 고침 제스처 hello 로그인 화면이 표시 됩니다. 성공적으로 로그인 한 후 hello 할 일 항목 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="319cd-139">Hello 클라이언트 프로젝트를 열고 hello 파일 **QSTodoService.cs** hello 다음 추가 및 문을 사용 하 여 및 `MobileServiceUser` 접근자 toohello QSTodoService 클래스 사용:</span><span class="sxs-lookup"><span data-stu-id="319cd-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="319cd-140">라는 새 메서드 추가 **Authenticate** 너무**QSTodoService** 정의 뒤 hello로:</span><span class="sxs-lookup"><span data-stu-id="319cd-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="319cd-141">Facebook 이외의 id 공급자를 사용 하는 경우 변경 너무 전달 된 값이 hello**LoginAsync** hello 다음의 tooone 위에: _MicrosoftAccount_, _Twitter_, _Google_, 또는 _WindowsAzureActiveDirectory_합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="319cd-142">**QSTodoListViewController.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="319cd-143">Hello 메서드 정의를 수정할 **ViewDidLoad** hello 호출 너무 제거**RefreshAsync()** hello 끝 근처에:</span><span class="sxs-lookup"><span data-stu-id="319cd-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
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
4. <span data-ttu-id="319cd-144">Hello 방법을 수정 **RefreshAsync** tooauthenticate 경우 hello **사용자** 속성이 null입니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="319cd-145">Hello 코드 hello 메서드 정의의 hello 위쪽에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="319cd-146">열기 **AppDelegate.cs**, hello 메서드 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="319cd-147">열기 **Info.plist** 파일, 너무 탐색**URL 형식** hello에 **고급** 섹션.</span><span class="sxs-lookup"><span data-stu-id="319cd-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="319cd-148">이제 hello 구성할 **식별자** 및 hello **URL 스키마** URL 형식과 클릭 **URL 형식 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="319cd-149">**URL 스키마** {url_scheme_of_your_app}로 hello 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="319cd-150">Visual Studio 또는 Xamarin Studio tooyour 장치 또는 에뮬레이터를 대상으로 하는 hello 클라이언트 프로젝트를 실행 하려면 Mac에서 Xamarin 빌드 호스트 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="319cd-151">Hello 앱 데이터가 표시 되지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="319cd-152">Hello hello 로그인 화면 tooappear 발생 하는 항목 목록을 아래로 잡아당겨 hello 새로 고침 제스처를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="319cd-153">성공적으로 유효한 자격 증명을 입력 하 고 나면 hello 앱 hello 할 일 항목 목록이 표시 됩니다 하 고 업데이트 toohello 데이터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="319cd-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Xamarin.iOS 앱 만들기]: app-service-mobile-xamarin-ios-get-started.md