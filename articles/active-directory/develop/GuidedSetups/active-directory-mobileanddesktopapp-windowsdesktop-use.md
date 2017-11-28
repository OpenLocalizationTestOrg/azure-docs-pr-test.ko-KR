---
title: "Azure AD v2 Windows 데스크톱 시작 - 사용 | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 826ba0a00b26993d4f37f0a8ce587d7bb77e7eb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="e08af-103">MSAL(Microsoft 인증 라이브러리)를 사용하여 Microsoft Graph API에 대한 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e08af-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="e08af-104">이 섹션에서는 MSAL을 사용하여 Microsoft Graph API에 대한 토큰을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-104">This section shows how to use MSAL to get a token the Microsoft Graph API.</span></span>

1.  <span data-ttu-id="e08af-105">`MainWindow.xaml.cs`에서 클래스에 MSAL 라이브러리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-105">In `MainWindow.xaml.cs`, add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="e08af-106">다음으로 <code>MainWindow</code> 클래스 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set the API Endpoint to Graph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set the scope for API call to user.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - to acquire a token requiring user to sign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need to call AcquireTokenAsync to acquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="e08af-107">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e08af-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="e08af-108">대화형 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e08af-108">Getting a user token interactive</span></span>
<span data-ttu-id="e08af-109">`AcquireTokenAsync` 메서드를 호출하면 사용자에게 로그인하라는 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-109">Calling the `AcquireTokenAsync` method results in a window prompting the user to sign in.</span></span> <span data-ttu-id="e08af-110">사용자가 처음으로 보호되는 리소스에 액세스해야 하거나 토큰 획득을 위한 자동 작업에 실패한 경우(예: 사용자의 암호 만료) 일반적으로 사용자는 응용 프로그램에서 대화식으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-110">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="e08af-111">자동으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e08af-111">Getting a user token silently</span></span>
<span data-ttu-id="e08af-112">`AcquireTokenSilentAsync`는 토큰 획득 및 갱신을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="e08af-113">`AcquireTokenAsync`가 처음으로 실행된 후 요청에 대한 호출 또는 토큰 갱신이 자동으로 수행되므로 `AcquireTokenSilentAsync`는 후속 호출을 위해 보호되는 리소스에 액세스하려고 토큰을 얻는 데 일반적으로 사용되는 메서드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-113">After `AcquireTokenAsync` is executed for the first time, `AcquireTokenSilentAsync` is the usual method used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="e08af-114">결국 `AcquireTokenSilentAsync`에 실패합니다(예: 사용자 로그아웃 또는 다른 장치에서 사용자가 암호 변경).</span><span class="sxs-lookup"><span data-stu-id="e08af-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="e08af-115">MSAL이 대화형 작업을 요구해 이 문제를 해결할 수 있다고 감지하면 `MsalUiRequiredException`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-115">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="e08af-116">응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="e08af-117">즉시 `AcquireTokenAsync`에 대한 호출을 수행합니다. 그러면 사용자에게 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting the user to sign-in.</span></span> <span data-ttu-id="e08af-118">이 패턴은 응용 프로그램에 사용자가 사용할 수 있는 오프라인 콘텐츠가 없는 온라인 응용 프로그램에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-118">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="e08af-119">이 안내식 설정에서 생성한 샘플에서는 이 패턴을 사용합니다. 여러분이 처음으로 샘플을 실행하면 로그인하라는 메시지를 볼 수 있습니다. 지금까지 이 응용 프로그램을 사용한 사용자가 없기 때문에 `PublicClientApp.Users.FirstOrDefault()`에는 null 값이 포함되어 있고 `MsalUiRequiredException` 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-119">The sample generated by this guided setup uses this pattern: you can see it in action the first time you execute the sample: because no user ever used the application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="e08af-120">샘플의 코드는 `AcquireTokenAsync`를 호출해 예외를 처리하여 사용자에게 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-120">The code in the sample then handles the exception by calling `AcquireTokenAsync` resulting in prompting the user to sign-in.</span></span>

2.  <span data-ttu-id="e08af-121">또한 응용 프로그램에서는 대화형 로그인이 필요하다는 시각적 표시를 사용자에게 보여줍니다. 따라서 사용자가 로그인할 적절한 시간을 선택하거나 이후에 응용 프로그램이 `AcquireTokenSilentAsync`를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-121">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="e08af-122">이는 사용자가 중단 없이 응용 프로그램의 기능을 사용할 수 있는 경우(예: 응용 프로그램에 사용 가능한 오프라인 콘텐츠가 있는 경우) 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-122">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="e08af-123">이 경우 사용자가 보호되는 리소스에 액세스하거나 오래된 정보를 새로 고치기 위해 로그인할 시점을 결정하거나 응용 프로그램이 일시적으로 사용할 수 없게 된 후 네트워크가 복원된 경우 `AcquireTokenSilentAsync`를 다시 시도하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-123">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="e08af-124">방금 가져온 토큰을 사용하여 Microsoft Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="e08af-124">Call the Microsoft Graph API using the token you just obtained</span></span>

1. <span data-ttu-id="e08af-125">`MainWindow.xaml.cs`에 아래의 새 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-125">Add the new method below to your `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="e08af-126">이 메서드는 인증 헤더를 사용하여 Graph API에 대한 `GET` 요청을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-126">The method is used to make a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request to a URL using an HTTP Authorization header
/// </summary>
/// <param name="url">The URL</param>
/// <param name="token">The token</param>
/// <returns>String containing the results of the GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add the token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="e08af-127">보호되는 API에 대한 REST 호출에 관한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="e08af-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="e08af-128">이 샘플 응용 프로그램에서 `GetHttpContentWithToken` 메서드는 토큰이 필요한 보호되는 리소스에 대한 HTTP `GET` 요청을 실행한 다음 호출자에게 콘텐츠를 반환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-128">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="e08af-129">이 메서드는 *HTTP 인증 헤더*에 획득된 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-129">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="e08af-130">이 샘플에서 리소스는 사용자 프로필 정보를 표시하는 Microsoft Graph API *me* 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-130">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="e08af-131">사용자를 로그아웃하는 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="e08af-131">Add a method to sign out the user</span></span>

1. <span data-ttu-id="e08af-132">`MainWindow.xaml.cs`에 다음 메서드를 추가하면 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-132">Add the following method to your `MainWindow.xaml.cs` to sign out the user:</span></span>

```csharp
/// <summary>
/// Sign out the current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="e08af-133">로그아웃에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e08af-133">More info on Sign-Out</span></span>

<span data-ttu-id="e08af-134">`SignOutButton_Click`은 MSAL 사용자 캐시에서 사용자를 제거하여 MSAL에 현재 사용자를 잊으라고 효율적으로 전달합니다. 따라서 대화식으로 수행되는 경우에만 토큰 획득을 위한 이후 요청에 성공하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-134">`SignOutButton_Click` removes the user from MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>
<span data-ttu-id="e08af-135">이 샘플의 응용 프로그램이 단일 사용자를 지원하더라도 MSAL은 동시에 여러 계정에 로그인할 수 있는 시나리오를 지원합니다(예: 사용자 한 명이 여러 계정을 가질 수 있는 메일 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="e08af-135">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="e08af-136">기본 토큰 정보 표시</span><span class="sxs-lookup"><span data-stu-id="e08af-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="e08af-137">`MainWindow.xaml.cs`에 다음 메서드를 추가하면 토큰에 대한 기본 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-137">Add the following method to to your `MainWindow.xaml.cs` to display basic information about the token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in the token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="e08af-138">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e08af-138">More Information</span></span>

<span data-ttu-id="e08af-139">*OpenID Connect*를 통해 획득된 토큰에는 사용자와 관련된 정보의 일부가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent to the user.</span></span> <span data-ttu-id="e08af-140">`DisplayBasicTokenInfo`는 토큰에 포함된 기본 정보를 표시합니다(예: 사용자 표시 이름 및 ID, 토큰 만료 날짜 및 액세스 토큰 자체를 나타내는 문자열).</span><span class="sxs-lookup"><span data-stu-id="e08af-140">`DisplayBasicTokenInfo` displays basic information contained in the token: for example, the user's display name and ID, as well as the token expiration date and the string representing the access token itself.</span></span> <span data-ttu-id="e08af-141">사용자가 볼 수 있도록 이러한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-141">This information is displayed for you to see.</span></span> <span data-ttu-id="e08af-142">*Microsoft Graph API 호출* (Call Microsoft Graph API) 단추를 여러 번 누르면 동일한 토큰이 후속 요청에 다시 사용된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-142">You can hit the *Call Microsoft Graph API* button multiple times and see that the same token was reused for subsequent requests.</span></span> <span data-ttu-id="e08af-143">MSAL이 토큰 갱신 시점이라고 판단한 경우에는 만료 날짜가 연장된 것도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e08af-143">You can also see the expiration date being extended when MSAL decides it is time to renew the token.</span></span>
<!--end-collapse-->

