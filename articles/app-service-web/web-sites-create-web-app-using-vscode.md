---
title: "Visual Studio Code에서 ASP.NET Core 웹 앱 aaaCreate"
description: "이 자습서에서는 toocreate ASP.NET Core 웹 앱 Visual Studio 코드를 사용 하 여 하는 방법을 보여 줍니다."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Visual Studio Code에서 ASP.NET Core 웹앱 만들기
## <a name="overview"></a>개요
이 자습서에서는 어떻게 toocreate ASP.NET Core 웹 앱에서 사용 하 여 [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) 너무 배포[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)합니다. 

> [!NOTE]
> 이 문서에서는 tooweb 앱, 있지만 tooAPI 앱 및 모바일 앱도 적용. 
> 
> 

ASP.NET Core에서는 ASP.NET을 완전히 다시 디자인했습니다. ASP.NET Core는 .NET을 사용하여 최신 클라우드 기반 웹앱을 빌드하기 위한 새로운 오픈 소스 크로스 플랫폼 프레임 워크입니다. 자세한 내용은 참조 [소개 tooASP.NET 코어](http://docs.asp.net/latest/conceptual-overview/aspnet.html)합니다. Azure 앱 서비스 웹앱에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>필수 조건
* [VS Code](http://code.visualstudio.com/Docs/setup)를 설치합니다.
* Git 설치 - [Chocolatey](https://chocolatey.org/packages/git) 또는 [git-scm.com](http://git-scm.com/downloads)에서 설치할 수 있습니다. 새 tooGit 인 경우 선택 [git scm.com](http://git-scm.com/downloads) 너무 hello 옵션을 선택 하 고**hello Windows 명령 프롬프트에서에서 Git 사용**합니다. Git를 설치한 다음도 해야 tooset hello Git 사용자 이름 및 전자 메일 (VS Code에서 커밋이 수행 중) 하는 경우 hello 자습서의 뒷부분에서 필요에 따라 합니다.  

## <a name="install-aspnet-core"></a>ASP.NET Core 설치
ASP.NET Core는 OS X, Linux 및 Windows에서 실행되는 최신 클라우드 및 웹앱을 빌드하기 위한 린(lean) .NET 스택입니다. 것에서 작성 된 hello tooprovide를 접지 하거나 배포 된 toohello 클라우드 또는 온-프레미스를 실행 하는 앱에 대 한 최적화 된 개발 프레임입니다. 오버헤드를 최소화하는 모듈식 구성 요소로 구성되므로 솔루션을 구성하는 동안 유연성이 유지할 수 있습니다.

이 자습서는 디자인 된 tooget hello 최신 개발 버전의 ASP.NET Core 응용 프로그램 작성을 시작 합니다. hello 지침에 따라 특정 tooWindows 됩니다. OS X, Linux 및 Windows에 대한 설치 지침은 [ASP.NET Core 시작](https://docs.microsoft.com/aspnet/core/getting-started)을 참조하세요. 


> [!NOTE]
> OS X, Linux 및 Windows에 대한 자세한 설치 지침은 [ASP.NET Core 설치](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)를 참조하세요. 
> 
> 

## <a name="create-hello-web-app"></a>Hello 웹 앱 만들기
이 섹션에서는 tooscaffold는 새 응용 프로그램의 ASP.NET 웹 앱 hello.NET CLI 도구를 사용 하 여 하는 방법을 보여 줍니다. 

1. Hello 명령 프롬프트 toocreate hello 프로젝트 폴더와 스 캐 폴드 hello 앱에서 hello 다음을 입력 합니다.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 생성기](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello 필요한 NuGet 패키지를 hello 다음 명령을 실행 합니다.
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Hello 웹 응용 프로그램을 로컬로 실행
Hello 웹 앱을 생성 하 고 hello 앱에 대 한 모든 hello NuGet 패키지를 검색 했으므로 hello 웹 응용 프로그램을 로컬로 실행할 수 있습니다.

1. Hello 응용 프로그램을 실행 (hello `dotnet run` 만료 될 때 명령이 hello 앱 빌드할):
    ```terminal
    dotnet run
    ```
2. 브라우저를 열고 url toohello 이동 합니다.
   
    **http://localhost:5000**
   
    hello 웹 응용 프로그램의 기본 페이지가 hello 다음과 같이 표시 됩니다.
   
    ![브라우저의 로컬 웹앱](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. 브라우저를 닫습니다. Hello에 **명령 창**, 키를 눌러 **Ctrl + C** hello 응용 프로그램 및 닫기 hello tooshut **명령 창**합니다. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서 웹 앱 만들기
hello 다음 단계는 안내 있습니다 hello Azure 포털에서에서 웹 앱을 만드는.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **새로** hello에 hello 포털의 왼쪽 위에 있습니다.
3. **웹앱 > 웹앱**을 클릭합니다.
   
    ![Azure 새 웹앱](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. **이름**에 대한 값을 입력합니다(예: **SampleWebAppDemo**). Note이 이름은 고유 toobe 필요 하 고 hello 포털 tooenter hello 이름 할 때를 적용 합니다. 따라서 입력 하 여 다른 값을 선택 해야 toosubstitute 해당 값을 각 **SampleWebAppDemo** 이 자습서에서 볼 수 있는 합니다. 
5. 기존 **앱 서비스 계획** 을 선택하거나 새 앱 서비스 계획을 만듭니다. 새 계획을 만들면 hello 가격 책정 계층, 위치 및 기타 옵션을 선택 합니다. 앱 서비스 계획에 대 한 자세한 내용은 hello 문서 참조 [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.
   
    ![Azure 새 웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. **만들기**를 클릭합니다.
   
    ![웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Hello 새 웹 앱에 대 한 Git 게시를 사용 하도록 설정
Git는 사용할 수 있는 toodeploy Azure 앱 서비스 웹 앱 분산된 버전 제어 시스템입니다. Hello 코드 로컬 Git 리포지토리에서 웹 앱에 대 한 쓰기 저장할 및 tooa 원격 리포지토리에 푸시하여 코드 tooAzure를 배포 합니다.   

1. Hello에 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **찾아보기**를 클릭합니다.
3. 클릭 **웹 앱** tooview Azure 구독에 연결 된 hello 웹 응용 프로그램의 목록입니다.
4. 이 자습서에서 만든 hello 웹 앱을 선택 합니다.
5. Hello 웹 앱 블레이드 클릭 **설정** > **연속 배포**합니다. 
   
    ![Azure 웹앱 호스트](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. **원본 선택 > 로컬 Git 리포지토리**를 클릭합니다.
7. **확인**을 클릭합니다.
   
    ![Azure 로컬 Git 리포지토리](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. 이전에 웹앱 또는 다른 앱 서비스 앱을 게시하기 위해 배포 자격 증명을 설정하지 않은 경우 지금 설정합니다.
   
   * **설정** > **배포 자격 증명**을 클릭합니다. hello **배포 자격 증명 설정** 블레이드를 표시 됩니다.
   * 사용자 이름 및 암호를 만듭니다.  나중에 Git를 설정할 때 이 암호가 필요합니다.
   * **Save**를 클릭합니다.
9. 웹앱의 블레이드에서 **설정 > 속성**을 클릭합니다. 아래에 표시 된 toois를 배포 하는 hello 원격 Git 리포지토리의 hello URL **GIT URL**합니다.
10. 복사 hello **GIT URL** hello 자습서에서 나중에 사용할 값입니다.
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>웹 앱 tooAzure 앱 서비스를 게시 합니다.
이 섹션에서는 로컬 Git 리포지토리를 만들 쿼리하고 해당 리포지토리 tooAzure toodeploy에서 웹 앱 tooAzure 강제 합니다.

1. VS Code 선택 hello **Git** hello 왼쪽된 탐색 모음에서 옵션입니다.
   
    ![VS Code의 Git 아이콘](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. 선택 **Initialize git 리포지토리** toomake 있는지 작업 영역은 git 소스 제어입니다. 
   
    ![Git 초기화](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Hello 명령 창을 열고 웹 응용 프로그램의 디렉터리 toohello 디렉터리를 변경 합니다. 그런 다음 hello 다음 명령을 입력 합니다.
   
        git config core.autocrlf false
   
    이 명령은 CRLF 끝과 LF 끝이 사용된 텍스트에 대한 문제를 방지합니다.
4. VS Code에서 커밋 메시지를 추가 하 고 hello 클릭 **커밋 모든** 아이콘을 확인 합니다.
   
    ![Git 모두 커밋](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Hello Git 창 아래에 나열 된 파일이 없는 참조 Git 처리가 완료 되 면 **변경**합니다. 
   
    ![Git 변경 내용 없음](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. 뒤로 toohello 웹 앱 위치한 명령 창 위치 hello 명령 프롬프트 가리키는 toohello 디렉터리를 변경 합니다.
7. Hello 앞에서 복사한 Git URL (끝에 ".git")를 사용 하 여 업데이트 tooyour 웹 응용 프로그램을 푸시하여에 대 한 원격 참조를 만듭니다.
   
        git remote add azure [URL for remote repository]
8. VS Code에서 생성 된 자동으로 추가 된 tooyour push 명령이 수 있도록 로컬 Git toosave 자격 증명를 구성 합니다.
   
        git config credential.helper store
9. Hello 다음 명령을 입력 하 여 변경 내용을 tooAzure 푸시하십시오. 이 초기 푸시 tooAzure 후 VS Code에서 모든 hello 푸시 명령 수 toodo 수 있습니다. 
   
        git push -u azure master
   
    Azure에서 만든 hello 암호를 묻는 메시지가 나타납니다. **참고: 암호는 표시되지 않습니다.**
   
    hello 출력 명령 위에 hello에서 성공적으로 배포 되었는지 메시지와 함께 종료 됩니다.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Git 기능을 기본적으로 hello를 사용 하 여 hello를 선택 하 여 VS 코드에 직접 다시 게시할 수 변경 tooyour 응용 프로그램을 만들면 **모든 커밋** hello 옵션 뒤 **푸시** 옵션입니다. Hello 있습니다 **푸시** hello 드롭 다운 메뉴 다음 toohello에서 사용할 수 있는 옵션 **모든 커밋** 및 **새로 고침** 단추입니다.
> 
> 

Toocollaborate 프로젝트에서 필요한 경우 tooAzure 푸시하여 사이 tooGitHub 푸시하는 것이 좋습니다.

## <a name="run-hello-app-in-azure"></a>Azure의 hello 앱 실행
웹 앱을 배포한 했으므로 hello 앱 Azure에서 호스트 하는 동안를 실행 해 보겠습니다. 

이 작업은 두 가지 방법으로 수행할 수 있습니다.

* 브라우저를 열고 다음과 같이 웹 응용 프로그램의 hello 이름을 입력 합니다.   
  
        http://SampleWebAppDemo.azurewebsites.net
* 에 Azure 포털 hello 웹 앱에 대 한 웹 앱 블레이드 hello을 찾아서 클릭 **찾아보기** tooview 앱 
* 앱을 확인합니다.

![Azure 웹앱](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>요약
이 자습서에서는 방법에 대해 배웠습니다 toocreate VS Code의 웹 앱 및 tooAzure 배포 합니다. VS Code에 대 한 자세한 내용은 hello 문서 참조 [Visual Studio Code 이유?](https://code.visualstudio.com/Docs/) App Service Web Apps에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요. 

