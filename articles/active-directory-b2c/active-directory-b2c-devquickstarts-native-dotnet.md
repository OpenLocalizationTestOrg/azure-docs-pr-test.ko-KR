---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Toobuild Windows 데스크톱 응용 프로그램 하는 로그인, 등록, 포함 방법과 Azure Active Directory B2C를 사용 하 여 프로 파일 관리 합니다."
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="450fc-103">Azure AD B2C: Windows 데스크톱 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="450fc-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="450fc-104">Azure Active Directory (Azure AD) B2C를 사용 하 여 몇 가지 간단한 단계에서 강력한 셀프 서비스 id 관리 기능 tooyour 데스크톱 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="450fc-105">이 문서에서는 보여 어떻게 toocreate 등록, 로그인, 사용자 및 프로필 관리를 포함 하는 "할 일 목록".NET Windows Presentation Foundation (WPF) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="450fc-106">hello 앱 사용자 이름 또는 전자 메일을 사용 하 여 등록 및 로그인에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="450fc-107">또한 Facebook 및 Google과 같은 소셜 계정을 사용하여 등록 및 로그인하는 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="450fc-108">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="450fc-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="450fc-109">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="450fc-110">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="450fc-111">아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="450fc-112">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="450fc-112">Create an application</span></span>
<span data-ttu-id="450fc-113">다음으로 응용 프로그램 toocreate B2C 디렉터리에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="450fc-114">Azure AD 정보가 필요한 toosecurely 통신할 수 있는지 응용 프로그램에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="450fc-115">응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="450fc-116">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-116">Be sure to:</span></span>

* <span data-ttu-id="450fc-117">포함 된 **네이티브 클라이언트** hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="450fc-118">복사 hello **리디렉션 URI** `urn:ietf:wg:oauth:2.0:oob`합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="450fc-119">이 코드 샘플에 대 한 hello 기본 URL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="450fc-120">복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="450fc-121">이 시간은 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="450fc-122">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="450fc-122">Create your policies</span></span>
<span data-ttu-id="450fc-123">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="450fc-124">이 코드 샘플은 등록, 로그인 및 프로필 편집 등 세 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="450fc-125">에 설명 된 대로 각 형식에 대 한 정책을 toocreate 필요는 [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="450fc-126">Hello 세 가지 정책을 만들 때 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="450fc-127">선택 **사용자 ID 등록** 또는 **등록 전자 메일** hello identity 공급자 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="450fc-128">등록 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="450fc-129">모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="450fc-130">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="450fc-131">복사 hello **이름** 를 만든 후 각 정책의 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="450fc-132">Hello 접두사 있어야 `b2c_1_`합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="450fc-133">이러한 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="450fc-134">준비 toobuild는 성공적으로 만든 후 hello 세 가지 정책, 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="450fc-135">Hello 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="450fc-135">Download hello code</span></span>
<span data-ttu-id="450fc-136">이 자습서에 대 한 코드를 hello [GitHub에서 유지 관리 됩니다](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="450fc-137">할 수 있습니다 때 toobuild hello 샘플으로 이동 [기본 프로젝트를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="450fc-138">Hello 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="450fc-139">완료 하는 hello 앱 이기도 [.zip 파일로 사용할](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) 컴퓨터나 hello `complete` hello의 분기 같은 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="450fc-140">Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="450fc-141">hello `TaskClient` 프로젝트는 hello 사용자 hello WPF 데스크톱 응용 프로그램 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="450fc-142">이 자습서의 hello 위해 백 엔드 작업 웹 각 사용자의 할 일 목록을 저장 하는 Azure에서 호스트 되는 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="450fc-143">Toobuild hello 웹 API 필요 하지 않습니다, 그리고 이미 보유를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="450fc-144">toolearn web API 안전 하 게 Azure AD B2C를 사용 하 여 요청을 인증 하는 방법 체크 아웃 된 [web API 시작 문서](active-directory-b2c-devquickstarts-api-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="450fc-145">정책 실행</span><span class="sxs-lookup"><span data-stu-id="450fc-145">Execute policies</span></span>
<span data-ttu-id="450fc-146">앱은 tooexecute hello HTTP 요청의 일부로 원하는 hello 정책을 지정 하는 인증 메시지를 전송 하 여 Azure AD B2C와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="450fc-147">.NET 데스크톱 응용 프로그램에 대 한 hello를 사용할 수 있습니다 Microsoft 인증 라이브러리 (MSAL) toosend OAuth 2.0 인증 메시지를 미리 보기, 정책, 실행 및 해당 호출 웹 Api 토큰을 가져오기.</span><span class="sxs-lookup"><span data-stu-id="450fc-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="450fc-148">MSAL 설치</span><span class="sxs-lookup"><span data-stu-id="450fc-148">Install MSAL</span></span>
<span data-ttu-id="450fc-149">MSAL toohello 추가 `TaskClient` hello Visual Studio 패키지 관리자 콘솔을 사용 하 여 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="450fc-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="450fc-150">B2C 세부 정보 입력</span><span class="sxs-lookup"><span data-stu-id="450fc-150">Enter your B2C details</span></span>
<span data-ttu-id="450fc-151">파일 열기 hello `Globals.cs` hello 속성 값을 각각 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="450fc-152">이 클래스는 전체에서 사용 `TaskClient` tooreference 일반적으로 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="450fc-153">Hello PublicClientApplication 만들기</span><span class="sxs-lookup"><span data-stu-id="450fc-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="450fc-154">hello MSAL의 기본 클래스는 `PublicClientApplication`합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="450fc-155">이 클래스는 Azure AD B2C hello 시스템에서 응용을 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="450fc-156">Hello 앱 초기화 인스턴스를 만드는 경우의 `PublicClientApplication` 에서 `MainWindow.xaml.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="450fc-157">이 hello 창 전체에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="450fc-158">등록 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="450fc-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="450fc-159">사용자를 toosigns opts를 원하는 tooinitiate 만든 hello 등록 정책을 사용 하는 등록 흐름 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="450fc-160">MSAL을 사용하여 `pca.AcquireTokenAsync(...)`를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="450fc-161">매개 변수를 너무 hello`AcquireTokenAsync(...)` 토큰을 받으면 hello 인증 요청에 사용 되는 hello 정책 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="450fc-162">로그인 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="450fc-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="450fc-163">Hello에서 로그인 흐름을 시작할 수는 등록 흐름을 시작 하는 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="450fc-164">사용자가 로그인 하는 경우 동일한 hello 확인 호출 tooMSAL, 정책에 로그인을 사용 하 여이 시간:</span><span class="sxs-lookup"><span data-stu-id="450fc-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="450fc-165">프로필 편집 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="450fc-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="450fc-166">다시 실행할 수 있습니다 편집 프로필 정책 hello와 동일한 방식:</span><span class="sxs-lookup"><span data-stu-id="450fc-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="450fc-167">이 모든 경우에 MSAL은 `AuthenticationResult` 에서 토큰을 반환하거나 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="450fc-168">MSAL에서 토큰을 가져올 때마다 hello를 사용할 수 있습니다 `AuthenticationResult.User` hello UI 같은 hello 앱의 tooupdate hello 사용자 데이터 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="450fc-169">ADAL도 캐시 hello hello 응용 프로그램의 다른 부분에 사용 하기 위해 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="450fc-170">앱 시작에서 토큰 확인</span><span class="sxs-lookup"><span data-stu-id="450fc-170">Check for tokens on app start</span></span>
<span data-ttu-id="450fc-171">또한 MSAL tookeep hello 사용자의 로그인 상태를 추적을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="450fc-172">이 응용 프로그램에서 이러한 hello 응용 프로그램을 종료할 & 다시 열어 후에 로그인 hello 사용자 tooremain을 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="450fc-173">Hello 내 다시 `OnInitialized` MSAL의 사용을 재정의 `AcquireTokenSilent` 캐시 된 토큰에 대 한 메서드 toocheck:</span><span class="sxs-lookup"><span data-stu-id="450fc-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="450fc-174">Hello 작업 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-174">Call hello task API</span></span>
<span data-ttu-id="450fc-175">가 이제 MSAL tooexecute 정책을 사용 하 고 토큰을 가져올 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="450fc-176">이러한 토큰 toocall hello 작업 API 하나 toouse 하려는 경우 MSAL의 다시 사용할 수 있습니다 `AcquireTokenSilent` 캐시 된 토큰에 대 한 메서드 toocheck:</span><span class="sxs-lookup"><span data-stu-id="450fc-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="450fc-177">호출을 너무 hello 때`AcquireTokenSilentAsync(...)` 성공 토큰이 hello 캐시에서 발견 될 hello 토큰 toohello를 추가할 수 있습니다 및 `Authorization` hello HTTP 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="450fc-178">hello 작업 웹 API에는이 헤더 tooauthenticate hello 요청 tooread hello 사용자의 할 일 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="450fc-179">Out hello 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="450fc-179">Sign hello user out</span></span>
<span data-ttu-id="450fc-180">마지막으로, MSAL를 사용할 수 있습니다 hello 앱 hello 사용자가을 선택할 때 사용 하 여 사용자의 세션 tooend **로그 아웃**합니다.  MSAL를 사용할 때이 모든 hello 토큰이 hello 토큰 캐시의 선택을 취소 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="450fc-181">Hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="450fc-181">Run hello sample app</span></span>
<span data-ttu-id="450fc-182">마지막으로, 빌드 및 hello 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="450fc-183">전자 메일 주소 또는 사용자 이름을 사용 하 여 hello 앱 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="450fc-184">로그 아웃 하 고 다시 로그인 hello로 동일 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="450fc-185">해당 사용자의 프로필을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-185">Edit that user's profile.</span></span> <span data-ttu-id="450fc-186">로그아웃했다가 다른 사용자로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="450fc-187">소셜 IDP 추가</span><span class="sxs-lookup"><span data-stu-id="450fc-187">Add social IDPs</span></span>
<span data-ttu-id="450fc-188">Hello 앱만 사용자 등록 및 로그인에 사용 하는 현재 지원 **로컬 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="450fc-189">이들은 사용자 이름 및 암호를 사용하는 B2C 디렉터리에 저장된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="450fc-190">Azure AD B2C를 사용하면 코드를 변경하지 않고도 다른 IDP(ID 공급자)에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="450fc-191">tooadd 소셜 IDPs tooyour 응용 프로그램에 따라 hello 방법을 다음이 문서에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="450fc-192">에 대 한 각 IDP toosupport 5d; 응용 프로그램 tooregister 해당 시스템에 필요 하 고 클라이언트 ID를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="450fc-193">Facebook을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="450fc-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="450fc-194">Google을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="450fc-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="450fc-195">Amazon을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="450fc-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="450fc-196">LinkedIn을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="450fc-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="450fc-197">Hello에 설명 된 tooinclude로 새 IDPs hello 세 정책을 각각 tooedit hello id 공급자 tooyour B2C 디렉터리를 추가한 후 필요한 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="450fc-198">정책을 저장 한 후 hello 앱을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="450fc-199">각 identity 경험 있는 로그인 및 등록 옵션으로 새 IDPs 추가 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="450fc-200">정책을 테스트 하 여 수 있으며 샘플 앱에 hello 효과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="450fc-201">IDP를 추가 또는 제거하거나 응용 프로그램 클레임을 조작하거나 등록 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="450fc-202">어떻게 정책, 인증 요청 및 MSAL을 모두 함께 연결하는지 확인할 수 있을 때까지 실험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="450fc-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="450fc-203">참조용으로 hello 완료 샘플 [.zip 파일로 제공](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="450fc-204">또한 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450fc-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
