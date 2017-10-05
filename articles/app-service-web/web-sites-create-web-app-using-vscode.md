---
title: "Visual Studio Code에서 ASP.NET Core 웹앱 만들기"
description: "이 자습서에서는 Visual Studio Code를 사용하여 ASP.NET Core 웹앱을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Visual Studio Code에서 ASP.NET Core 웹앱 만들기
## <a name="overview"></a>개요
이 자습서에서는 [VS Code(Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode)를 사용하여 ASP.NET Core 웹앱을 만들어 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에 배포하는 방법에 대해 알아봅니다. 

> [!NOTE]
> 이 문서는 웹앱을 참조하지만 API 앱 및 모바일 앱에도 적용됩니다. 
> 
> 

ASP.NET Core에서는 ASP.NET을 완전히 다시 디자인했습니다. ASP.NET Core는 .NET을 사용하여 최신 클라우드 기반 웹앱을 빌드하기 위한 새로운 오픈 소스 크로스 플랫폼 프레임 워크입니다. 자세한 내용은 [ASP.NET Core 소개](http://docs.asp.net/latest/conceptual-overview/aspnet.html)를 참조하세요. Azure 앱 서비스 웹앱에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>필수 조건
* [VS Code](http://code.visualstudio.com/Docs/setup)를 설치합니다.
* Git 설치 - [Chocolatey](https://chocolatey.org/packages/git) 또는 [git-scm.com](http://git-scm.com/downloads)에서 설치할 수 있습니다. Git를 처음 사용하는 경우 [git-scm.com](http://git-scm.com/downloads) 을 선택하고 **Windows 명령 프롬프트에서 Git 사용**옵션을 선택합니다. Git를 설치한 후 자습서의 뒤에 나오는 VS Code에서 커밋을 수행할 때 필요하므로 Git 사용자 이름과 전자 메일을 설정해야 합니다.  

## <a name="install-aspnet-core"></a>ASP.NET Core 설치
ASP.NET Core는 OS X, Linux 및 Windows에서 실행되는 최신 클라우드 및 웹앱을 빌드하기 위한 린(lean) .NET 스택입니다. ASP.NET 5/DNX는 클라우드에 배포되거나 온-프레미스로 실행될 앱에 최적화된 개발 프레임워크를 제공하기 위해 처음부터 다시 제작되었습니다. 오버헤드를 최소화하는 모듈식 구성 요소로 구성되므로 솔루션을 구성하는 동안 유연성이 유지할 수 있습니다.

이 자습서는 ASP.NET Core의 최신 개발 버전으로 응용 프로그램 빌드를 시작하도록 설계되었습니다. 다음은 Windows에 특정한 지침입니다. OS X, Linux 및 Windows에 대한 설치 지침은 [ASP.NET Core 시작](https://docs.microsoft.com/aspnet/core/getting-started)을 참조하세요. 


> [!NOTE]
> OS X, Linux 및 Windows에 대한 자세한 설치 지침은 [ASP.NET Core 설치](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)를 참조하세요. 
> 
> 

## <a name="create-the-web-app"></a>웹앱 만들기
이 섹션에서는 .NET CLI 도구를 사용하여 새 앱 ASP.NET 웹앱을 스캐폴드하는 방법을 보여 줍니다. 

1. 프로젝트 폴더를 만들고 앱을 스캐폴딩하려면 명령 프롬프트에 다음을 입력합니다.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 생성기](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. 필요한 NuGet 패키지를 복원하려면 다음 명령을 실행합니다.
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a>로컬로 웹앱 실행
웹앱을 만들고 앱에 대한 모든 NuGet 패키지를 검색했으므로 이제 웹앱을 로컬로 실행할 수 있습니다.

1. 앱 실행(`dotnet run` 명령은 만료되면 앱을 빌드합니다.):
    ```terminal
    dotnet run
    ```
2. 브라우저를 열고 다음 URL로 이동합니다.
   
    **http://localhost:5000**
   
    웹앱의 기본 페이지가 다음과 같이 표시됩니다.
   
    ![브라우저의 로컬 웹앱](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. 브라우저를 닫습니다. **명령 창**에서 **Ctrl+C**를 눌러 응용 프로그램을 종료하고 **명령 창**을 닫습니다. 

## <a name="create-a-web-app-in-the-azure-portal"></a>Azure 포털에서 웹 앱 만들기
다음 단계에서는 Azure 포털에서 웹앱을 만드는 과정을 안내합니다.

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. 포털의 왼쪽 위에서 **새로 만들기** 를 클릭합니다.
3. **웹앱 > 웹앱**을 클릭합니다.
   
    ![Azure 새 웹앱](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. **이름**에 대한 값을 입력합니다(예: **SampleWebAppDemo**). 이 이름은 고유해야 하며 사용자가 이름을 입력할 때 포털에서 해당 이름을 적용합니다. 따라서 다른 값을 입력할 경우 이 자습서에 표시되는 각 **SampleWebAppDemo** 항목을 해당 값으로 대체해야 합니다. 
5. 기존 **앱 서비스 계획** 을 선택하거나 새 앱 서비스 계획을 만듭니다. 새 계획을 만드는 경우 가격 책정 계층, 위치 및 기타 옵션을 선택합니다. 앱 서비스 계획에 대한 자세한 내용은 [Azure 앱 서비스 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.
   
    ![Azure 새 웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. **만들기**를 클릭합니다.
   
    ![웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a>새 웹앱에 Git 게시 사용
Git는 Azure 앱 서비스 웹앱을 배포하는 데 사용할 수 있는 분산된 버전 제어 시스템입니다. 웹앱에 대해 작성한 코드를 로컬 Git 리포지토리에 저장하고, 원격 리포지토리로 푸시하여 Azure에 코드를 배포합니다.   

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **찾아보기**를 클릭합니다.
3. **웹앱** 을 클릭하여 Azure 구독과 연결된 웹앱의 목록을 확인합니다.
4. 이 자습서에서 만든 웹앱을 선택합니다.
5. 웹앱 블레이드에서 **설정** > **지속적인 배포**를 클릭합니다. 
   
    ![Azure 웹앱 호스트](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. **원본 선택 > 로컬 Git 리포지토리**를 클릭합니다.
7. **확인**을 클릭합니다.
   
    ![Azure 로컬 Git 리포지토리](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. 이전에 웹앱 또는 다른 앱 서비스 앱을 게시하기 위해 배포 자격 증명을 설정하지 않은 경우 지금 설정합니다.
   
   * **설정** > **배포 자격 증명**을 클릭합니다. **배포 자격 증명 설정** 블레이드가 표시됩니다.
   * 사용자 이름 및 암호를 만듭니다.  나중에 Git를 설정할 때 이 암호가 필요합니다.
   * **Save**를 클릭합니다.
9. 웹앱의 블레이드에서 **설정 > 속성**을 클릭합니다. 배포할 원격 Git 리포지토리의 URL이 **GIT URL**아래에 표시됩니다.
10. 이 자습서에서 나중에 사용할 **GIT URL** 값을 복사합니다.
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a>Azure 앱 서비스에 웹앱 게시
이 섹션에서는 로컬 Git 리포지토리를 만들고 해당 리포지토리에서 Azure로 푸시하여 웹앱을 Azure에 배포합니다.

1. VS Code의 왼쪽 탐색 모음에서 **Git** 옵션을 선택합니다.
   
    ![VS Code의 Git 아이콘](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. **git 리포지토리 초기화** 를 선택하여 작업 공간이 git 소스 제어 아래에 오도록 합니다. 
   
    ![Git 초기화](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. 명령 창을 열고 디렉터리를 웹앱의 디렉터리로 변경합니다. 그런 후 다음 명령을 입력합니다.
   
        git config core.autocrlf false
   
    이 명령은 CRLF 끝과 LF 끝이 사용된 텍스트에 대한 문제를 방지합니다.
4. VS Code에서 커밋 메시지를 추가하고 **모두 커밋** 확인 아이콘을 클릭합니다.
   
    ![Git 모두 커밋](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Git 처리가 완료되면 **변경 내용**아래 Git 창에 나열된 파일이 없습니다. 
   
    ![Git 변경 내용 없음](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. 명령 프롬프트가 웹앱이 위치한 디렉터리를 가리키는 명령 창으로 다시 변경합니다.
7. 앞에서 복사한 Git URL(“.git”로 종료됨)을 사용하여 웹앱에 업데이트를 푸시하기 위한 원격 참조를 만듭니다.
   
        git remote add azure [URL for remote repository]
8. 자격 증명이 로컬로 저장되도록 Git을 구성하여 자격 증명이 VS 코드에서 생성된 푸시 명령에 자동으로 추가될 수 있게 합니다.
   
        git config credential.helper store
9. 다음 명령을 입력하여 변경 내용을 Azure에 푸시합니다. 처음으로 Azure에 푸시한 후에는 VS 코드로부터 모든 푸시 명령을 수행할 수 있게 됩니다. 
   
        git push -u azure master
   
    Azure에서 이전에 만든 암호를 입력하라는 메시지가 나타납니다. **참고: 암호는 표시되지 않습니다.**
   
    위 명령의 출력은 배포에 성공했다는 메시지로 종료됩니다.
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> 앱을 변경하면 **모두 커밋** 옵션을 선택한 다음 **푸시** 옵션을 선택하여 기본 Git 기능을 통해 VS 코드에서 직접 다시 게시할 수 있습니다. **모두 커밋** 및 **새로 고침** 단추 옆에 있는 드롭다운 메뉴에서 **푸시** 옵션을 찾을 수 있습니다.
> 
> 

공동 작업해야 하는 프로젝트의 경우에는 Azure로의 푸시 사이에 GitHub으로의 푸시도 고려해야 합니다.

## <a name="run-the-app-in-azure"></a>Azure에서 앱 실행
웹앱을 배포했으므로 이제 Azure에서 호스트된 상태에서 앱을 실행해 보겠습니다. 

이 작업은 두 가지 방법으로 수행할 수 있습니다.

* 브라우저를 열고 웹앱의 이름을 다음과 같이 입력합니다.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Azure 포털에서 웹앱에 대한 웹앱 블레이드를 찾은 다음 기본 브라우저에서 **찾아보기** 를 클릭하여 
* 앱을 확인합니다.

![Azure 웹앱](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>요약
이 자습서에서는 VS Code에서 웹앱을 만들고 Azure에 배포하는 방법을 알아보았습니다. VS Code에 대한 자세한 내용은 [Visual Studio Code를 선택해야 하는 이유?](https://code.visualstudio.com/Docs/) 문서를 참조하세요. App Service Web Apps에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요. 

