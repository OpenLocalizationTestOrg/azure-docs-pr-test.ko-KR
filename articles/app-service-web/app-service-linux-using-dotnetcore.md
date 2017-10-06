---
title: "Linux에서 웹 응용 프로그램에서.NET Core aaaUse | Microsoft Docs"
description: "Linux의 Web App에서 .NET Core를 사용합니다."
keywords: "azure app service, 웹앱, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Linux의 Azure Web App에서 .NET Core 사용 #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[웹 앱](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) linux hello Linux 운영 체제를 사용 하 여 확장성이 높은, 자동 패치 웹 호스팅 서비스를 제공 합니다. 이 자습서에 대 한 단계별 지침을 보여 주는 방법을 toocreate는 [.NET Core](https://docs.microsoft.com/aspnet/core/) 응용 프로그램 Linux에서 Azure 웹 앱에 액세스 합니다. 

![Linux에서 Web App][10]

Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다.

## <a name="prerequisites"></a>필수 조건 ##

toocomplete이이 자습서: 

* Hello 설치 [.NET Core SDK](https://www.microsoft.com/net/download/core)합니다.
* [Git](https://git-scm.com/downloads)를 설치합니다.

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>로컬 .NET Core 응용 프로그램 만들기 ##

새 터미널 세션을 시작합니다. 라는 디렉터리를 만들고 `hellodotnetcore`, 현재 디렉터리 tooit hello를 변경 합니다. Hello 다음을 입력 합니다. 

```
dotnet new web
``` 

  이 명령은 세 파일을 만듭니다 (*hellodotnetcore.csproj*, *Program.cs*, 및 *Startup.cs*) 및 한 빈 폴더 (*wwwroot /*) hello 현재 디렉터리입니다. 콘텐츠 hello `.csproj` 파일 hello 다음과 같습니다. 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

ASP.NET Core 패키지를 자동으로 참조 tooan toohello 추가할이 응용 프로그램 웹 응용 프로그램 이므로, *hellodotnetcore.csproj* 파일입니다. hello 패키지의 버전 번호 hello toohello 프레임 워크 선택에 따라 설정 됩니다. .NET Core 1.1이 사용되었으므로 이 예제에서는 ASP.NET Core 버전 1.1.2를 참조합니다.

## <a name="build-and-test-hello-application-locally"></a>빌드 및 hello 응용 프로그램을 로컬로 테스트 ##

빌드하고 hello로.NET Core 응용 프로그램을 실행할 수 `dotnet restore` hello 명령 `dotnet run` 다음과 같이 명령:

```
dotnet restore
dotnet run
```


Hello 응용 프로그램을 시작할 때 hello 앱 tooincoming 요청 포트에서 수신 하는 메시지가 표시 됩니다. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

너무 이동 하 여 테스트`http://localhost:5000/` 브라우저와 합니다. 모든 기능이 제대로 작동하는 경우 결과 텍스트로 "Hello World!"가 hello 결과 텍스트입니다.

![브라우저를 통한 테스트][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서.NET Core 응용 프로그램 만들기 ##

먼저 toocreate 빈 웹 응용 프로그램입니다. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 을 새로 만듭니다 [Linux에서 웹 앱](https://portal.azure.com/#create/Microsoft.AppSvcLinux)합니다.

![웹앱 만들기][1]

Hello 때 **만들기** 페이지가 열립니다, 웹 앱에 대 한 세부 정보를 제공 합니다.

![.NET Core 런타임 스택 선택][2]

Hello 아웃 가이드 toofill로 사용 하 여 hello 다음 표에서 **만들기** 페이지를 선택한 다음 선택 **확인** 및 **만들기** toocreate hello 앱.

| 설정      | 제안 값  | 설명                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| 앱 이름 | hellodotnetcore  | 응용 프로그램의 hello 이름입니다. 이 이름은 고유해야 합니다. |
| 구독 | 기존 구독 선택 | hello Azure 구독입니다. |
| 리소스 그룹 | myResourceGroup |  hello Azure 리소스 그룹 toocontain hello 웹 앱입니다. |
| 앱 서비스 계획 | 기존 App Service 계획 이름 |  앱 서비스 계획 번호입니다.  |
| 컨테이너 구성 | .NET Core 1.1 | 이 웹 앱에 대 한 컨테이너 유형 hello: 기본 제공 필드, Docker, 또는 개인 레지스트리 합니다. |
| 이미지 원본  | 기본 제공  |  hello 이미지의 hello 소스입니다. |
| 런타임 스택  | .NET Core 1.1  | hello 런타임 스택 및 버전입니다.  |

## <a name="deploy-your-application-via-git"></a>Git를 통한 응용 프로그램 배포 ##

Linux에서 Git toodeploy hello.NET Core 응용 프로그램 tooAzure 앱 서비스 웹 앱을 사용 합니다.

hello 새 Azure 웹 앱에 이미 Git 배포를 구성 합니다. Toohello 웹 응용 프로그램 이름에 삽입 한 후 URL을 따라 이동 하 여 hello Git 배포 URL을 찾을 수 있습니다.

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Git URL hello hello 양식 기반 웹 응용 프로그램 이름으로 다음에 있습니다.

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Hello 다음 명령을 toodeploy hello 로컬 응용 프로그램 tooyour Azure 웹 앱을 실행 합니다. 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

아래에 있는 모든 파일 toopush 필요 하지 않습니다 *bin /* 또는 *obj /* 디렉터리 hello 클라우드에서 응용 프로그램은 빌드되므로 응용 프로그램의 hello 경우 소스 파일 tooAzure 푸시됩니다. 이진 파일을 hello 응용 프로그램의 디렉터리에 복사 hello 빌드 프로세스를 완료 한 후 */home/사이트/wwwroot/*합니다.

Hello 원격 배포 작업에 성공 했음을 보고 있는지 확인 합니다. 푸시 작업 이후 패키지 확인 시간이 오래 걸릴 및 빌드 hello 클라우드에서 실행 하는 프로세스 수 있습니다. 파일이 복사되었음을 포함하여 몇 가지 상태 메시지가 표시됩니다. hello 출력에는 비슷한 toohello 다음과 같아야 합니다.

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Hello 배포 완료 되 면 hello 배포 tootake 효과 대 한 웹 앱을 다시 시작 합니다. toodo toohello Azure 포털을 이동 및 toohello 이동 **개요** 웹 응용 프로그램의 페이지입니다. 선택 hello **다시 시작** hello 페이지 단추입니다. 선택 팝업 창에 표시 될 경우 **예** tooconfirm 합니다. 다음과 같이 웹앱을 찾아볼 수 있습니다.

![.NET Core 검색 응용 프로그램이 배포 tooAzure linux 앱 서비스][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>다음 단계
* [Linux의 Azure App Service Web App에 대한 FAQ](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
