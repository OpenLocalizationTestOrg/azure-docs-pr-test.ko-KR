---
title: "UWP(유니버설 Windows 플랫폼) 앱에 인증 추가 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱을 사용하여 AAD, Google, Facebook, Twitter, Microsoft 등의 다양한 ID 공급자를 사용해서 UWP(유지버설 Windows 플랫폼) 앱 사용자를 인증하는 방법을 알아봅니다."
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="c3cdb-103">Windows 앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="c3cdb-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="c3cdb-104">이 항목에서는 모바일 앱에 클라우드 기반 인증을 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="c3cdb-105">이 자습서에서는 Azure 앱 서비스가 지원하는 ID 공급자를 사용하여 모바일 앱용 UWP(유니버설 Windows 플랫폼) 빠른 시작 프로젝트에 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="c3cdb-106">모바일 앱 백 엔드에서 인증되고 권한이 부여된 후 사용자 ID 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="c3cdb-107">이 자습서는 모바일 앱 퀵 스타트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="c3cdb-108">먼저 [모바일 앱 시작](app-service-mobile-windows-store-dotnet-get-started.md)자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="c3cdb-109"><a name="register"></a>인증을 위해 앱 등록 및 앱 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c3cdb-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="c3cdb-110"><a name="redirecturl"></a>허용되는 외부 리디렉션 URL에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="c3cdb-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="c3cdb-111">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="c3cdb-112">이를 통해 인증 시스템은 인증 프로세스가 완료되면 앱으로 다시 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="c3cdb-113">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="c3cdb-114">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="c3cdb-115">이 체계는 모바일 응용 프로그램에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="c3cdb-116">서버 쪽에서 리디렉션을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="c3cdb-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="c3cdb-117">[Azure Portal]에서 해당 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c3cdb-118">**인증/권한 부여** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c3cdb-119">**허용되는 외부 리디렉션 URL**에서 `url_scheme_of_your_app://easyauth.callback`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="c3cdb-120">이 문자열의 **url_scheme_of_your_app**은 모바일 응용 프로그램에 대한 URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c3cdb-121">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="c3cdb-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c3cdb-122">여러 위치에서 URL 체계에 따라 모바일 응용 프로그램 코드를 조정해야 할 경우 선택한 문자열을 적어두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="c3cdb-123">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-123">Click **OK**.</span></span>

5. <span data-ttu-id="c3cdb-124">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-124">Click **Save**.</span></span>

## <span data-ttu-id="c3cdb-125"><a name="permissions"></a>사용 권한을 인증된 사용자로 제한</span><span class="sxs-lookup"><span data-stu-id="c3cdb-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="c3cdb-126">이제 백 엔드에 대한 익명 액세스가 비활성화되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="c3cdb-127">시작 프로젝트로 설정된 UWP 앱 프로젝트를 사용하여 앱을 배포하고 실행합니다. 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="c3cdb-128">이 예외는 앱이 인증되지 않은 사용자로 모바일 앱 코드에 액세스하려고 시도하는데 *TodoItem* 테이블에서 이제 인증을 요구하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="c3cdb-129">다음에는 앱 서비스에서 리소스를 요청하기 전에 사용자를 인증하도록 앱을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="c3cdb-130"><a name="add-authentication"></a>앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="c3cdb-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="c3cdb-131">UWP 앱 프로젝트 파일 MainPage.xaml.cs에서 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="c3cdb-132">이 코드는 Facebook 로그인으로 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="c3cdb-133">Facebook 이외의 ID 공급자를 사용하는 경우 위의 **MobileServiceAuthenticationProvider** 값을 공급자에 대한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="c3cdb-134">MainPage.xaml.cs에서 **OnNavigatedTo()** 메서드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="c3cdb-135">다음으로, 인증을 트리거하는 앱에 **로그인** 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="c3cdb-136">MainPage.xaml.cs에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="c3cdb-137">MainPage.xaml 프로젝트 파일을 열고 **저장** 단추를 정의하는 요소를 찾아서 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="c3cdb-138">App.xaml.cs에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="c3cdb-139">Package.appxmanifest 파일을 열고 **선언**으로 이동한 후 **사용 가능한 선언** 드롭다운 목록에서 **프로토콜**을 선택하고 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="c3cdb-140">이제 **프로토콜** 선언의 **속성**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="c3cdb-141">**표시 이름**에서 응용 프로그램의 사용자에게 표시할 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="c3cdb-142">**이름**에 {url_scheme_of_your_app}를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="c3cdb-143">F5 키를 눌러 앱을 실행하고 **로그인** 단추를 클릭한 다음 선택한 ID 공급자로 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="c3cdb-144">성공적으로 로그인되고 나면 앱이 오류 없이 실행되고 백 엔드를 쿼리하여 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="c3cdb-145"><a name="tokens"></a>클라이언트에 인증 토큰 저장</span><span class="sxs-lookup"><span data-stu-id="c3cdb-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="c3cdb-146">이전 예제에서는 앱이 시작될 때마다 클라이언트가 ID 공급자와 앱 서비스 둘 다에 접근해야 하는 표준 로그인을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="c3cdb-147">이 방법은 비효율적일 뿐 아니라 많은 고객이 동시에 앱을 시작하려고 할 경우 사용 관련 문제가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="c3cdb-148">더 나은 접근 방법은 앱 서비스에서 반환된 권한 부여 토큰을 캐시한 다음 공급자 기반 로그인을 사용하기 전에 이 토큰을 먼저 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="c3cdb-149">클라이언트 관리 인증 또는 서비스 관리 인증을 사용하는지에 관계없이 앱 서비스에서 발급된 토큰을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="c3cdb-150">이 자습서에서는 서비스 관리 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="c3cdb-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3cdb-151">Next steps</span></span>
<span data-ttu-id="c3cdb-152">이 기본 인증 자습서를 완료했으므로 다음 자습서 중 하나를 계속하는 것을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="c3cdb-153">앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="c3cdb-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="c3cdb-154">앱에 푸시 알림 지원을 추가하고 모바일 앱 백 엔드를 구성하여 푸시 알림을 보내는 Azure Notification Hubs를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="c3cdb-155">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="c3cdb-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="c3cdb-156">모바일 앱 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="c3cdb-157">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cdb-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
