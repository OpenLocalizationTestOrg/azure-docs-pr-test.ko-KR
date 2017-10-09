---
title: "AD aaaAzure v2 Windows 데스크톱 시작-설치 | Microsoft Docs"
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
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="a9d04-103">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="a9d04-103">Set up your project</span></span>

<span data-ttu-id="a9d04-104">방법에 대 한 단계별 지침을 제공 하는이 섹션 toocreate 새 프로젝트 toodemonstrate 어떻게 toointegrate Windows 데스크톱.NET 응용 프로그램 (XAML)와 *Microsoft를 사용 하 여 로그인* 토큰 요구 하는 웹 Api를 쿼리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="a9d04-105">이 가이드에서 만든 hello 응용 프로그램 화면 및 로그 아웃 단추는 단추 toograph 및 표시 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="a9d04-106">Toodownload이이 샘플의 Visual Studio 프로젝트를 대신 선호?</span><span class="sxs-lookup"><span data-stu-id="a9d04-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="a9d04-107">[프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) toohello 건너뛸 [구성 단계](#create-an-application-express) tooconfigure hello 코드 샘플을 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="a9d04-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="a9d04-108">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a9d04-108">Create your application</span></span>
1. <span data-ttu-id="a9d04-109">Visual Studio에서: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="a9d04-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="a9d04-110">[템플릿]에서 `Visual C#`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="a9d04-111">선택 `WPF App` (또는 *WPF 응용 프로그램* 에서 Visual Studio의 hello 버전에 따라)</span><span class="sxs-lookup"><span data-stu-id="a9d04-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="a9d04-112">Hello Microsoft 인증 라이브러리 (MSAL) tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="a9d04-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="a9d04-113">Visual Studio에서: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="a9d04-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="a9d04-114">Hello 패키지 관리자 콘솔 창에서에서 hello 다음 복사/붙여넣기:</span><span class="sxs-lookup"><span data-stu-id="a9d04-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="a9d04-115">위의 hello 패키지는 hello Microsoft 인증 라이브러리 (MSAL)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="a9d04-116">MSAL 가져오는, 캐싱 및 사용자 사용 toskens tooaccess Azure Active Directory v 2에 의해 보호 되는 Api를 새로 고침을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="a9d04-117">Hello 코드 tooinitialize MSAL 추가</span><span class="sxs-lookup"><span data-stu-id="a9d04-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="a9d04-118">이 단계를 사용 하면 토큰의 처리와 같은 MSAL 라이브러리와 클래스 toohandle 상호 작용을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="a9d04-119">열기 hello `App.xaml.cs` 파일을 MSAL 라이브러리 toohello 클래스에 대 한 hello 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="a9d04-120">Hello, 클래스 toohello 다음 앱을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="a9d04-121">응용 프로그램 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="a9d04-121">Create your application’s UI</span></span>
<span data-ttu-id="a9d04-122">hello 섹션 아래의 응용 프로그램에서 Microsoft Graph와 같은 보호 된 백 엔드 서버를 쿼리할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="a9d04-123">MainWindow.xaml 파일은 프로젝트 템플릿의 일부로 자동으로 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="a9d04-124">이 파일이이 파일을 열고 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a9d04-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="a9d04-125">응용 프로그램의 대체 `<Grid>` hello 다음 수:</span><span class="sxs-lookup"><span data-stu-id="a9d04-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
