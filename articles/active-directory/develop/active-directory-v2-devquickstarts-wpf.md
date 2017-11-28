---
title: ".NET 네이티브 앱 aaaAzure Active Directory v2.0 | Microsoft Docs"
description: "어떻게 toobuild.NET 네이티브 앱 하는 로그인 사용자 두 개인 Microsoft 계정으로 하 고 회사 또는 학교 계정."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="0b01c-103">로그인 tooa Windows 바탕 화면 앱 추가</span><span class="sxs-lookup"><span data-stu-id="0b01c-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="0b01c-104">Hello hello v2.0 끝점과 두 개인 Microsoft 계정에 대 한 지원 및 회사 또는 학교 계정을 사용 하 여 인증 tooyour 데스크톱 앱을 신속 하 게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="0b01c-105">이 앱 toosecurely는 백엔드와 통신할 수 있도록 웹 api를으로 [Microsoft Graph hello](https://graph.microsoft.io) hello 중 몇 [Office 365 통합 Api](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="0b01c-106">모든 Azure AD (Active Directory) 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="0b01c-107">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="0b01c-108">에 대 한 [장치에서 실행 되는.NET 네이티브 앱](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD는 Microsoft Identity 인증 라이브러리 또는 MSAL hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="0b01c-109">웹 서비스 호출에 대 한 토큰을 응용 프로그램 tooget 한 것을 쉽게 toomake는 생활에서 MSAL의 목적으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="0b01c-110">이면 작업이 얼마나 쉬운지 toodemonstrate 여기 빌드합니다.NET WPF 할 일 목록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="0b01c-111">기호 hello에 대 한 사용자 및 가져옵니다 hello를 사용 하 여 토큰에 액세스 [OAuth 2.0 인증 프로토콜](active-directory-v2-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="0b01c-112">OAuth 2.0으로 보안된 백 엔드 To-Do List 웹 서비스를 안전하게 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="0b01c-113">Hello 사용자 아웃 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="0b01c-114">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="0b01c-114">Download sample code</span></span>
<span data-ttu-id="0b01c-115">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="0b01c-116">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="0b01c-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="0b01c-117">완료 하는 hello 앱도이 자습서의 hello 끝에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="0b01c-118">앱 등록</span><span class="sxs-lookup"><span data-stu-id="0b01c-118">Register an app</span></span>
<span data-ttu-id="0b01c-119">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="0b01c-120">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-120">Make sure to:</span></span>

* <span data-ttu-id="0b01c-121">Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="0b01c-122">Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="0b01c-123">MSAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="0b01c-123">Install & Configure MSAL</span></span>
<span data-ttu-id="0b01c-124">이제 앱을 Microsoft에 등록했으며, MSAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="0b01c-125">해야 tooprovide MSAL toobe 수 toocommunicate hello v2.0 끝점에 대 한 순서 대로 사용 하 여 응용 프로그램 등록에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="0b01c-126">패키지 관리자 콘솔 hello를 사용 하 여 MSAL toohello TodoListClient 프로젝트를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="0b01c-127">Hello TodoListClient 프로젝트를 열고 `app.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="0b01c-128">Hello에 hello 요소 hello 값 바꾸기 `<appSettings>` 섹션 tooreflect hello hello 응용 프로그램 등록 포털에 대 한 입력 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="0b01c-129">코드는 MSAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="0b01c-130">hello `ida:ClientId` 는 hello **응용 프로그램 Id** hello 포털에서 복사 하는 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="0b01c-131">Hello TodoList 서비스 프로젝트를 열고 `web.config` hello 프로젝트의 hello 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="0b01c-132">Hello 대체 `ida:Audience` hello로 동일 값 **응용 프로그램 Id** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="0b01c-133">MSAL tooget 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="0b01c-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="0b01c-134">hello 기본적 MSAL 뒤에 응용 프로그램 액세스 토큰을 필요할 때마다 단순히를 호출 하는 `app.AcquireToken(...)`, 및 MSAL rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="0b01c-135">Hello에 `TodoListClient` 프로젝트, 열기 `MainWindow.xaml.cs` hello 찾습니다 `OnInitialized(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0b01c-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="0b01c-136">hello 첫 번째 단계는 tooinitialize 앱의 `PublicClientApplication` -네이티브 응용 프로그램을 나타내는 MSAL의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="0b01c-137">이 MSAL 전달 하는 Azure AD와 toocommunicate 필요한 좌표 hello 및 방법에 설명 toocache 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="0b01c-138">Hello 앱 시작 되 면 म toocheck 고 hello 사용자는 hello 앱에 로그인 하지 않은 경우를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0b01c-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="0b01c-139">그러나 않도록 tooinvoke 로그인 UI 아직-하므로 "로그인" toodo 클릭 hello 사용자 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="0b01c-140">Hello에도 `OnInitialized(...)` 메서드:</span><span class="sxs-lookup"><span data-stu-id="0b01c-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="0b01c-141">Hello 사용자가 로그인 되지 않은 경우 hello "로그인" 단추를 클릭 했습니다 tooinvoke 로그인 UI 원하는 있고 hello 사용자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="0b01c-142">Hello 로그인 단추 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="0b01c-143">Hello 사용자 성공적으로 로그인, MSAL를 수신 하 고, 토큰을 캐시 하 고 toocall hello를 진행할 수 있습니다 `GetTodoList()` 메서드 확신을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="0b01c-144">모든 사용자의 작업 tooget 없어진는 tooimplement hello `GetTodoList()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0b01c-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="0b01c-145">실행</span><span class="sxs-lookup"><span data-stu-id="0b01c-145">Run</span></span>
<span data-ttu-id="0b01c-146">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-146">Congratulations!</span></span> <span data-ttu-id="0b01c-147">이제 작업 중인 hello 기능 tooauthenticate 사용자가 있는.NET WPF 앱을 준비 및 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="0b01c-148">두 프로젝트를 실행하고, 개인 Microsoft 계정이나 회사 또는 학교 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="0b01c-149">작업 toothat 사용자의 할 일 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="0b01c-150">로그 아웃 하 고 자신의 할 일 목록으로 다른 사용자 tooview에 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="0b01c-151">Hello 응용 프로그램을 닫고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="0b01c-152">Hello 사용자의 세션 그대로 어떻게 확인-hello 앱 로컬 파일에 있는 토큰을 캐시 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="0b01c-153">MSAL 하면 쉽게 tooincorporate 일반적인 id 기능 응용 프로그램에 개인 및 회사 계정을 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="0b01c-154">있습니다-캐시 관리, 로그인 토큰이 만료 등 새로 고침 UI hello 사용자 제시 되는 OAuth 프로토콜 지원에 대 한 모든 hello dirty 작업의 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="0b01c-155">Tooknow 실제로 필요한 것은 단일 API 호출 `app.AcquireTokenAsync(...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="0b01c-156">참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="0b01c-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b01c-157">Next steps</span></span>
<span data-ttu-id="0b01c-158">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="0b01c-159">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-159">You may want tootry:</span></span>

* [<span data-ttu-id="0b01c-160">Hello v2.0 끝점과 hello TodoListService 웹 API 보안 설정</span><span class="sxs-lookup"><span data-stu-id="0b01c-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="0b01c-161">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="0b01c-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="0b01c-162">hello v2.0 개발자 가이드 >></span><span class="sxs-lookup"><span data-stu-id="0b01c-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="0b01c-163">StackOverflow "msal" 태그 >></span><span class="sxs-lookup"><span data-stu-id="0b01c-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="0b01c-164">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="0b01c-164">Get security updates for our products</span></span>
<span data-ttu-id="0b01c-165">보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b01c-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

