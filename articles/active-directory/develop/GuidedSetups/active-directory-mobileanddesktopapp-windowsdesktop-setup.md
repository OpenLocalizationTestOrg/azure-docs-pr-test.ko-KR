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
## <a name="set-up-your-project"></a>프로젝트 설정

방법에 대 한 단계별 지침을 제공 하는이 섹션 toocreate 새 프로젝트 toodemonstrate 어떻게 toointegrate Windows 데스크톱.NET 응용 프로그램 (XAML)와 *Microsoft를 사용 하 여 로그인* 토큰 요구 하는 웹 Api를 쿼리할 수 있도록 합니다.

이 가이드에서 만든 hello 응용 프로그램 화면 및 로그 아웃 단추는 단추 toograph 및 표시 결과 표시 합니다.

> Toodownload이이 샘플의 Visual Studio 프로젝트를 대신 선호? [프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) toohello 건너뛸 [구성 단계](#create-an-application-express) tooconfigure hello 코드 샘플을 실행 하기 전에.


### <a name="create-your-application"></a>응용 프로그램 만들기
1. Visual Studio에서: `File` > `New` > `Project`<br/>
2. [템플릿]에서 `Visual C#`을 선택합니다.
3. 선택 `WPF App` (또는 *WPF 응용 프로그램* 에서 Visual Studio의 hello 버전에 따라)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Hello Microsoft 인증 라이브러리 (MSAL) tooyour 프로젝트 추가
1. Visual Studio에서: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Hello 패키지 관리자 콘솔 창에서에서 hello 다음 복사/붙여넣기:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> 위의 hello 패키지는 hello Microsoft 인증 라이브러리 (MSAL)를 설치합니다. MSAL 가져오는, 캐싱 및 사용자 사용 toskens tooaccess Azure Active Directory v 2에 의해 보호 되는 Api를 새로 고침을 처리 합니다.

## <a name="add-hello-code-tooinitialize-msal"></a>Hello 코드 tooinitialize MSAL 추가
이 단계를 사용 하면 토큰의 처리와 같은 MSAL 라이브러리와 클래스 toohandle 상호 작용을 만들 수 있습니다.

1. 열기 hello `App.xaml.cs` 파일을 MSAL 라이브러리 toohello 클래스에 대 한 hello 참조를 추가 합니다.

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Hello, 클래스 toohello 다음 앱을 업데이트 합니다.
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

## <a name="create-your-applications-ui"></a>응용 프로그램 UI 만들기
hello 섹션 아래의 응용 프로그램에서 Microsoft Graph와 같은 보호 된 백 엔드 서버를 쿼리할 수는 방법을 보여 줍니다. MainWindow.xaml 파일은 프로젝트 템플릿의 일부로 자동으로 생성되어야 합니다. 이 파일이이 파일을 열고 아래 hello 지침을 따릅니다.

응용 프로그램의 대체 `<Grid>` hello 다음 수:

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
