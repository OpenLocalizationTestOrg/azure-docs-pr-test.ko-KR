---
title: "AD aaaAzure v2 Windows 데스크톱 시작-사용 | Microsoft Docs"
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
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hello Microsoft 인증 라이브러리 (MSAL) tooget 토큰을 사용 하 여 hello Microsoft Graph API에 대 한

이 섹션에서는 toouse MSAL tooget 토큰을 Microsoft Graph API를 hello 하는 방법을 보여 줍니다.

1.  `MainWindow.xaml.cs`, MSAL 라이브러리 toohello 클래스에 대 한 hello 참조를 추가 합니다.

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
다음으로 <code>MainWindow</code> 클래스 코드를 바꿉니다.
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
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
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
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
### <a name="more-information"></a>추가 정보
#### <a name="getting-a-user-token-interactive"></a>대화형 사용자 토큰 가져오기
호출 hello `AcquireTokenAsync` 확인 창에서 메서드 결과에 대 한 사용자 toosign hello 합니다. 응용 프로그램 일반적으로 필요에 대화형으로 hello 사용자 toosign tooaccess 필요한 처음으로 보호 된 리소스 되거나 자동 작업 tooacquire 토큰 실패 (예: hello 사용자의 암호 만료 됨).

#### <a name="getting-a-user-token-silently"></a>자동으로 사용자 토큰 가져오기
`AcquireTokenSilentAsync`는 토큰 획득 및 갱신을 자동으로 처리합니다. 후 `AcquireTokenAsync` 처음으로 hello에 대 한 실행 `AcquireTokenSilentAsync` hello 사용 되는 일반적인 방법 tooobtain 사용 되는 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.
결국 `AcquireTokenSilentAsync` 못합니다-예: hello 사용자가 로그 아웃 또는 다른 장치에서 암호 변경 되었습니다. MSAL 탐지 대화형 작업을 요구 하 여 hello 문제 해결을 발생 시킬는 `MsalUiRequiredException`합니다. 응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.

1.  에 대 한 호출 `AcquireTokenAsync` 즉시 줄어들고 결과적 toosign에 hello 사용자 확인 합니다. 이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 되는 오프 라인 콘텐츠 hello 응용 프로그램의 hello 사용자에 대해 사용할 수 있습니다. hello이 단계별된 설치 프로그램에 의해 생성 된 샘플 사용 하 여이 패턴: 나타나면 작업 hello에 hello 샘플을 실행 하는 처음으로: 사용자 hello 응용 프로그램을 사용 하기 때문에 `PublicClientApp.Users.FirstOrDefault()` null 값이 포함 됩니다 및 `MsalUiRequiredException` 예외가 throw 됩니다. 핸들 예외를 호출 하 여 hello 다음 hello 샘플의 코드를 hello `AcquireTokenAsync` toosign에 hello 사용자 확인 발생 합니다.

2.  응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `AcquireTokenSilentAsync` 나중에 있습니다. 이 일반적으로 hello 사용자 중단 되지 않고 hello 응용 프로그램의 다른 기능을 사용할 수 있습니다-예를 들어 콘텐츠가 오프 라인 hello 응용 프로그램에서 사용할 수 있는 경우에 사용 됩니다. 때 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보를 오래 된 항목 또는 응용 프로그램 tooretry를 결정할 수 hello 사용자 결정할 수는 경우 `AcquireTokenSilentAsync` 네트워크 일시적으로 사용할 수 없게 후 복원 된 경우.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.

1. Hello tooyour 아래 새 메서드 추가 `MainWindow.xaml.cs`합니다. hello 메서드는 사용 되는 toomake는 `GET` 권한 부여 헤더를 사용 하 여 Graph API에 대 한 요청:

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>보호되는 API에 대한 REST 호출에 관한 추가 정보

이 샘플 응용 프로그램에서는 hello `GetHttpContentWithToken` 메서드는 사용 되는 toomake HTTP `GET` 토큰 한 후 hello 콘텐츠 toohello 호출자를 요구 하는 보호 된 리소스에 대 한 요청입니다. 이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다. 이 샘플에 대 한 hello 리소스는 Microsoft Graph API hello *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Hello 사용자 아웃 메서드 toosign 추가

1. 다음 메서드 tooyour hello 추가 `MainWindow.xaml.cs` toosign hello 사용자:

```csharp
/// <summary>
/// Sign out hello current user
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
### <a name="more-info-on-sign-out"></a>로그아웃에 대한 자세한 정보

`SignOutButton_Click`제거 hello MSAL 사용자 캐시에서 사용자 –이 쿼리 효과적으로 확인할 MSAL tooforget hello에 대 한 현재 사용자는 후속 요청 tooacquire 만들어진 경우 toobe 대화형 토큰 성공만 됩니다.
MSAL 여러 계정을 hello에 로그인 될 수 있는 시나리오를 지원 hello 응용 프로그램에서이 샘플에서는 단일 사용자를 지원 하지만 동일한 시간-예로 전자 메일 응용 프로그램 사용자가 계정을 여러 개 있습니다.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>기본 토큰 정보 표시

1. 다음 메서드 tootooyour hello 추가 `MainWindow.xaml.cs` toodisplay hello 토큰에 대 한 기본 정보:

```csharp
/// <summary>
/// Display basic information contained in hello token
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
### <a name="more-information"></a>추가 정보

토큰을 통해 획득 *OpenID Connect* 도 정보 관련 toohello 사용자의 작은 하위 집합을 포함 합니다. `DisplayBasicTokenInfo`hello 토큰에 포함 된 기본 정보가 표시 됩니다: 예를 들어 hello 사용자의 표시 이름 및 ID 뿐만 아니라 자체 hello 액세스 토큰을 나타내는 토큰 만료 날짜 및 hello 문자열 hello 합니다. 이 정보는 toosee 있습니다에 대 한 표시 됩니다. Hello 적중할 수 있습니다 *Microsoft Graph API 호출* 단추를 여러 번 하 고 동일한 토큰 후속 요청에 사용 된 해당 hello를 참조 하십시오. 시간 toorenew hello 토큰 MSAL 결정 하면 확장 하 고 hello 만료 날짜를 확인할 수 있습니다.
<!--end-collapse-->

