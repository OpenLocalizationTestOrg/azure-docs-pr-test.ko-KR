---
title: Azure Active Directory B2C | Microsoft Docs
description: "Azure Active Directory B2C를 사용하여 로그인, 등록 및 프로필 관리를 포함하는 Windows 데스크톱 응용 프로그램을 빌드하는 방법을 알아봅니다."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="508b5-103">Azure AD B2C: Windows 데스크톱 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="508b5-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="508b5-104">Azure AD(Azure Active Directory) B2C를 사용하여 몇 가지 간단한 단계에서 강력한 셀프 서비스 ID 관리 기능을 데스크톱 앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="508b5-105">이 문서에서는 사용자 등록, 로그인 및 프로필 관리를 포함하는 .NET WPF(Windows Presentation Foundation) "할 일 모음" 앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="508b5-106">이 앱에서는 사용자 이름 또는 전자 메일을 사용하여 등록 및 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="508b5-107">또한 Facebook 및 Google과 같은 소셜 계정을 사용하여 등록 및 로그인하는 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="508b5-108">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="508b5-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="508b5-109">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="508b5-110">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="508b5-111">아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="508b5-112">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="508b5-112">Create an application</span></span>
<span data-ttu-id="508b5-113">다음으로 B2C 디렉터리에서 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="508b5-114">앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="508b5-115">앱을 만들려면 [다음 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="508b5-116">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-116">Be sure to:</span></span>

* <span data-ttu-id="508b5-117">응용 프로그램에 **네이티브 클라이언트** 를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="508b5-118">**리디렉션 URI** `urn:ietf:wg:oauth:2.0:oob`를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="508b5-119">이 코드 샘플에 대한 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="508b5-120">앱에 할당된 **응용 프로그램 ID** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="508b5-121">이 시간은 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="508b5-122">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="508b5-122">Create your policies</span></span>
<span data-ttu-id="508b5-123">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="508b5-124">이 코드 샘플은 등록, 로그인 및 프로필 편집 등 세 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="508b5-125">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 각 형식에 대한 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="508b5-126">세 가지 정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="508b5-127">ID 공급자 블레이드에서 **사용자 ID 등록** 또는 **메일 등록** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="508b5-128">등록 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="508b5-129">모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="508b5-130">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="508b5-131">각 정책을 만든 후에 **이름**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="508b5-132">접두사 `b2c_1_`이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="508b5-133">이러한 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="508b5-134">세 가지 정책을 성공적으로 만들면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="508b5-135">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="508b5-135">Download the code</span></span>
<span data-ttu-id="508b5-136">이 자습서에 대한 코드는 [GitHub에서 유지 관리됩니다](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="508b5-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="508b5-137">진행하면서 샘플을 빌드하기 위해 [골격 프로젝트를 .zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="508b5-138">구조를 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="508b5-139">완성된 앱도 [.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)하거나 동일한 리포지토리의 `complete` 분기에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="508b5-140">샘플 코드를 다운로드한 후 Visual Studio .sln 파일을 열어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="508b5-141">`TaskClient` 프로젝트는 사용자와 상호 작용하는 WPF 데스크톱 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="508b5-142">이 자습서에서는 Azure에 호스트되는 각 사용자의 할 일 목록을 저장하는 백 엔드 작업 웹 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="508b5-143">웹 API를 빌드할 필요가 없습니다. 이미 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="508b5-144">Web API가 Azure AD B2C를 사용하여 요청을 안전하게 인증하는 방법을 알아보려면 [Web API 시작 문서](active-directory-b2c-devquickstarts-api-dotnet.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="508b5-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="508b5-145">정책 실행</span><span class="sxs-lookup"><span data-stu-id="508b5-145">Execute policies</span></span>
<span data-ttu-id="508b5-146">앱은 인증 메시지를 전송하여 Azure AD B2C와 통신하며 이는 HTTP 요청의 일부로 실행하고자 하는 정책을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="508b5-147">.NET 데스크톱 응용 프로그램의 경우 MSAL(미리 보기 Microsoft 인증 라이브러리)을 사용하여 OAuth 2.0 인증 메시지를 보내고 정책을 실행하고 Web API를 호출하는 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="508b5-148">MSAL 설치</span><span class="sxs-lookup"><span data-stu-id="508b5-148">Install MSAL</span></span>
<span data-ttu-id="508b5-149">Visual Studio 패키지 관리자 콘솔을 사용하여 MSAL을 `TaskClient` 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="508b5-150">B2C 세부 정보 입력</span><span class="sxs-lookup"><span data-stu-id="508b5-150">Enter your B2C details</span></span>
<span data-ttu-id="508b5-151">`Globals.cs` 파일을 열고 각각의 속성 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="508b5-152">이 클래스는 일반적으로 사용되는 값을 참조하기 위해 `TaskClient` 전반에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="508b5-153">PublicClientApplication 만들기</span><span class="sxs-lookup"><span data-stu-id="508b5-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="508b5-154">MSAL의 기본 클래스는 `PublicClientApplication`입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="508b5-155">이 클래스는 Azure AD B2C 시스템에 있는 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="508b5-156">앱이 시작되면 `MainWindow.xaml.cs`에서 `PublicClientApplication` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="508b5-157">이를 창 전체에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="508b5-158">등록 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="508b5-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="508b5-159">사용자가 등록하려는 경우 이전에 만든 등록 정책을 사용하는 등록 흐름을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="508b5-160">MSAL을 사용하여 `pca.AcquireTokenAsync(...)`를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="508b5-161">`AcquireTokenAsync(...)` 에 전달하는 매개 변수는 받을 토큰의 종류, 인증 요청에서 사용되는 정책 등을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="508b5-162">로그인 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="508b5-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="508b5-163">등록 흐름을 시작하는 것과 동일한 방식으로 로그인 흐름을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="508b5-164">사용자가 로그인하면 로그인 정책을 사용하여 동일한 방식으로 MSAL을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="508b5-165">프로필 편집 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="508b5-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="508b5-166">다시 동일한 방식으로 프로필 편집 정책을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="508b5-167">이 모든 경우에 MSAL은 `AuthenticationResult` 에서 토큰을 반환하거나 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="508b5-168">MSAL에서 토큰을 가져올 때마다 `AuthenticationResult.User` 개체를 사용하여 UI와 같은 앱의 사용자 데이터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="508b5-169">또한 ADAL은 응용 프로그램의 다른 부분에 사용하기 위해 토큰을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="508b5-170">앱 시작에서 토큰 확인</span><span class="sxs-lookup"><span data-stu-id="508b5-170">Check for tokens on app start</span></span>
<span data-ttu-id="508b5-171">또한 MSAL를 사용하여 사용자의 로그인 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="508b5-172">이 앱에서 사용자가 앱을 닫았다가 다시 연 후에도 로그인된 상태를 유지하게 하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="508b5-173">`OnInitialized` 재정의 내부에서 MSAL의 `AcquireTokenSilent` 메서드를 사용하여 캐시된 토큰을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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
```

## <a name="call-the-task-api"></a><span data-ttu-id="508b5-174">태스크 API 호출</span><span class="sxs-lookup"><span data-stu-id="508b5-174">Call the task API</span></span>
<span data-ttu-id="508b5-175">MSAL을 사용하여 정책을 실행하고 토큰을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="508b5-176">이러한 토큰 중 하나를 사용하여 태스크 API를 호출하려는 경우 MSAL의 `AcquireTokenSilent` 메서드를 다시 사용하여 캐쉬된 토큰을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

<span data-ttu-id="508b5-177">`AcquireTokenSilentAsync(...)`에 대한 호출이 성공하고 캐시에 토큰이 발견되면 HTTP 요청의 `Authorization` 헤더에 토큰을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="508b5-178">태스크 웹 API는 이 헤더를 사용하여 사용자 할 일 목록에 대한 읽기 요청을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="508b5-179">사용자를 로그아웃</span><span class="sxs-lookup"><span data-stu-id="508b5-179">Sign the user out</span></span>
<span data-ttu-id="508b5-180">마지막으로 사용자가 **로그아웃**을 선택한 경우 MSAL을 사용하여 앱에서 사용자의 세션을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="508b5-181">MSAL을 사용하는 경우 토큰 캐시에서 모든 토큰을 삭제하는 방식으로 이 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="508b5-182">샘플 앱 실행</span><span class="sxs-lookup"><span data-stu-id="508b5-182">Run the sample app</span></span>
<span data-ttu-id="508b5-183">마지막으로 샘플을 빌드하하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="508b5-184">메일 주소 또는 사용자 이름을 사용하여 앱에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="508b5-185">로그아웃했다가 동일한 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="508b5-186">해당 사용자의 프로필을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-186">Edit that user's profile.</span></span> <span data-ttu-id="508b5-187">로그아웃했다가 다른 사용자로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="508b5-188">소셜 IDP 추가</span><span class="sxs-lookup"><span data-stu-id="508b5-188">Add social IDPs</span></span>
<span data-ttu-id="508b5-189">현재, 앱은 **로컬 계정**을 사용하는 사용자 등록 및 로그인만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="508b5-190">이들은 사용자 이름 및 암호를 사용하는 B2C 디렉터리에 저장된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="508b5-191">Azure AD B2C를 사용하면 코드를 변경하지 않고도 다른 IDP(ID 공급자)에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="508b5-192">소셜 IDP를 앱에 추가하려면 이 문서 중에서 상세한 지침을 수행하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="508b5-193">지원하려는 각 IDP의 경우 해당 시스템에서 응용 프로그램을 등록하고 클라이언트 ID를 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="508b5-194">Facebook을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="508b5-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="508b5-195">Google을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="508b5-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="508b5-196">Amazon을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="508b5-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="508b5-197">LinkedIn을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="508b5-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="508b5-198">B2C 디렉터리에 ID 공급자를 추가한 후 [정책 참조 문서](active-directory-b2c-reference-policies.md)에서 설명한 대로 새 IDP를 포함하도록 세 가지 정책을 각각 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="508b5-199">정책을 저장한 후 앱을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="508b5-200">ID 환경 각각에서 로그인 및 등록으로 추가된 새 IDP가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="508b5-201">정책을 실험하고 샘플 앱에서 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="508b5-202">IDP를 추가 또는 제거하거나 응용 프로그램 클레임을 조작하거나 등록 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="508b5-203">어떻게 정책, 인증 요청 및 MSAL을 모두 함께 연결하는지 확인할 수 있을 때까지 실험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="508b5-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="508b5-204">참조를 위해 완료된 샘플은 [.zip 파일로 제공](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)됩니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="508b5-205">또한 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="508b5-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
