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
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="cea49-103">인증 tooyour Windows 앱 추가</span><span class="sxs-lookup"><span data-stu-id="cea49-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="cea49-104">이 항목에서는 tooadd 클라우드 기반 인증 tooyour 모바일 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="cea49-105">이 자습서에서는 Azure 앱 서비스에서 지 원하는 id 공급자를 사용 하 여 모바일 앱에 대 한 인증 toohello 유니버설 Windows 플랫폼 (UWP) 빠른 시작 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="cea49-106">인증 되 고 모바일 앱 백엔드에서 권한이 성공적으로 되 고, 후 hello 사용자 ID 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="cea49-107">이 자습서는 hello 모바일 앱 빠른 시작을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="cea49-108">Hello 자습서를 먼저 완료 해야 [모바일 앱 시작](app-service-mobile-windows-store-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="cea49-109"><a name="register"></a>인증에 대 한 앱을 등록 하 고 hello 응용 프로그램 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="cea49-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="cea49-110"><a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가</span><span class="sxs-lookup"><span data-stu-id="cea49-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="cea49-111">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="cea49-112">Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="cea49-113">이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체.</span><span class="sxs-lookup"><span data-stu-id="cea49-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="cea49-114">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="cea49-115">고유 tooyour 모바일 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="cea49-116">hello 서버 쪽에서 tooenable hello 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="cea49-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="cea49-117">Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="cea49-118">Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="cea49-119">Hello에 **외부 리디렉션 Url 허용**, 입력 `url_scheme_of_your_app://easyauth.callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="cea49-120">hello **url_scheme_of_your_app** 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="cea49-121">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="cea49-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="cea49-122">Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="cea49-123">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-123">Click **OK**.</span></span>

5. <span data-ttu-id="cea49-124">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-124">Click **Save**.</span></span>

## <span data-ttu-id="cea49-125"><a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한</span><span class="sxs-lookup"><span data-stu-id="cea49-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="cea49-126">이제 해당 익명 액세스 tooyour 백 엔드 비활성화 됨을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="cea49-127">Hello 시작 프로젝트로 설정 hello UWP 앱 프로젝트를 배포 하 고 hello 응용 프로그램 실행 hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="cea49-128">Hello 앱 tooaccess 인증 되지 않은 사용자로 모바일 응용 프로그램 코드를 시도 하기 때문에이 문제가 발생 하지만 hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="cea49-129">다음으로 응용 프로그램 서비스에서 리소스를 요청 하기 전에 hello 앱 tooauthenticate 사용자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="cea49-130"><a name="add-authentication"></a>인증 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="cea49-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="cea49-131">Hello UWP 앱 프로젝트에서 MainPage.xaml.cs 파일 하 고 다음 코드 조각 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
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
   
    <span data-ttu-id="cea49-132">이 코드는 Facebook 로그인 하 여 hello 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="cea49-133">Facebook 이외의 id 공급자를 사용 하는 경우의 hello 값 변경 **MobileServiceAuthenticationProvider** 공급자 toohello 값을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="cea49-134">Hello 대체 **OnNavigatedTo()** MainPage.xaml.cs에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="cea49-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="cea49-135">추가한 다음으로 **로그인** 인증을 트리거하는 단추 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="cea49-136">다음 코드 조각 toohello MainPage.xaml.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
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
4. <span data-ttu-id="cea49-137">Hello MainPage.xaml 프로젝트 파일을 열고 hello를 정의 하는 hello 요소를 찾습니다. **저장** 단추 및 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
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
5. <span data-ttu-id="cea49-138">다음 코드 조각 toohello App.xaml.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

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
6. <span data-ttu-id="cea49-139">Package.appxmanifest 파일을 열고 너무 탐색**선언**에 **사용 가능한 선언** 드롭다운 목록에서 선택 **프로토콜** 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="cea49-140">이제 hello 구성할 **속성** 의 hello **프로토콜** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="cea49-141">**표시 이름**, 응용 프로그램의 toodisplay toousers hello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="cea49-142">**이름**에 {url_scheme_of_your_app}를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="cea49-143">Hello F5 키 toorun hello 응용 프로그램 키를 눌러을 hello 클릭 **로그인** 단추 및 선택한 id 공급자와 hello 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="cea49-144">로그인에 성공한 후 hello 앱 오류 없이 실행 되 고 백 엔드 수 tooquery 하 고 업데이트 toodata를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="cea49-145"><a name="tokens"></a>Hello 인증 토큰 hello 클라이언트에 저장</span><span class="sxs-lookup"><span data-stu-id="cea49-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="cea49-146">두 hello id 공급자는 표준 로그인, hello 클라이언트 toocontact 필요한 표시 하 고 hello 이러한 앱이 시작 될 때마다 응용 프로그램 서비스 hello 하는 hello 이전 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="cea49-147">뿐만 아니라이 메서드를 비효율적으로 실행할 수 있습니다는로 사용-관련 문제는 고객이 많은 toostart 시도 hello에서 앱 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="cea49-148">더 나은 방법은 toocache hello 권한 부여에서 반환 된 토큰 응용 프로그램 서비스 및 try toouse이는 공급자 기반 로그인에 사용 하기 전에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="cea49-149">클라이언트 관리 또는 서비스 관리 인증 사용 여부에 관계 없이 응용 프로그램 서비스에서 발급 하는 hello 토큰을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="cea49-150">이 자습서에서는 서비스 관리 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="cea49-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cea49-151">Next steps</span></span>
<span data-ttu-id="cea49-152">이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="cea49-153">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="cea49-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="cea49-154">Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 여 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend 푸시 알림을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="cea49-155">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="cea49-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="cea49-156">오프 라인 tooadd는 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="cea49-157">오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자에 게 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea49-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
