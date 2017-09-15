---
title: "Azure AD v2 Windows 데스크톱 시작 - 설정 | Microsoft Docs"
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
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="4919f-103">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="4919f-103">Set up your project</span></span>

<span data-ttu-id="4919f-104">이 섹션에서는 토큰이 필요한 Web API를 쿼리할 수 있도록 Windows Desktop .NET 응용 프로그램(XAML)을 *Microsoft에 로그인*과 통합하는 방식을 설명하기 위해 새 프로젝트를 만드는 방법에 대한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="4919f-105">이 가이드에서 만든 응용 프로그램은 화면에 결과를 표시하기 위한 단추와 로그아웃 단추를 노출시킵니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="4919f-106">이 샘플의 Visual Studio 프로젝트를 다운로드하고 싶으세요?</span><span class="sxs-lookup"><span data-stu-id="4919f-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="4919f-107">[프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip)하면 실행 전 코드 샘플을 구성하는 [구성 단계](#create-an-application-express)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="4919f-108">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4919f-108">Create your application</span></span>
1. <span data-ttu-id="4919f-109">Visual Studio에서: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="4919f-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="4919f-110">[템플릿]에서 `Visual C#`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="4919f-111">`WPF App`(또는 [WPF 응용 프로그램], Visual Studio 버전에 따라 다름)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="4919f-112">프로젝트에 MSAL(Microsoft 인증 라이브러리) 추가</span><span class="sxs-lookup"><span data-stu-id="4919f-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="4919f-113">Visual Studio에서: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="4919f-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="4919f-114">패키지 관리자 콘솔 창에서 다음 내용을 복사/붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="4919f-115">위의 패키지는 MSAL(Microsoft 인증 라이브러리)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="4919f-116">MSAL은 Azure Active Directory v2로 보호되는 API에 액세스하는 데 사용되는 사용자 토큰의 획득, 캐싱 및 새로 고침을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="4919f-117">MSAL을 초기화하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="4919f-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="4919f-118">이 단계를 수행하면 MSAL 라이브러리와의 상호 작용을 처리하는 클래스를 만들 수 있습니다(예: 토큰 처리).</span><span class="sxs-lookup"><span data-stu-id="4919f-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="4919f-119">`App.xaml.cs` 파일을 열고 클래스에 MSAL 라이브러리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="4919f-120">앱 클래스를 다음으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="4919f-121">응용 프로그램 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="4919f-121">Create your application’s UI</span></span>
<span data-ttu-id="4919f-122">아래 섹션에서는 응용 프로그램에서 Microsoft Graph와 같은 보호되는 백 엔드 서버를 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="4919f-123">MainWindow.xaml 파일은 프로젝트 템플릿의 일부로 자동으로 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="4919f-124">이 파일을 열고 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="4919f-125">다음으로 응용 프로그램의 `<Grid>`를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4919f-125">Replace your application’s `<Grid>` with be the following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
