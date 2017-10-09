---
title: "로컬 Docker 컨테이너에 aaaDebugging 앱 | Microsoft Docs"
description: "Toomodify 로컬 Docker 컨테이너에서 실행 되는 응용 프로그램 편집 및 새로 고침을 통해 hello 컨테이너 새로 고침 및 디버깅 중단점을 설정 방법에 대해 알아봅니다"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>로컬 Docker 컨테이너에서 앱 디버깅
## <a name="overview"></a>개요
hello Visual Studio Tools for Docker에 일관 된 방식으로 toodevelop 하며 Linux Docker 컨테이너에서 로컬로 응용 프로그램의 유효성을 검사 합니다.
Toorestart hello 컨테이너 코드 변경 될 때마다 않아도 됩니다.
이 문서에서는 toouse hello 기능 toostart "편집 및 새로 고침" 로컬 Docker 컨테이너에서 ASP.NET Core 웹 앱, 필요한 변경 하 고 해당 변경 내용을 hello 브라우저 toosee를 새로 고칩니다 하는 방법을 보여 줍니다.
또한 이렇게 하면 어떻게 tooset 디버깅 중단점.

> [!NOTE]
> Windows 컨테이너 지원은 향후 릴리스에서 제공됩니다.
>
>

## <a name="prerequisites"></a>필수 조건
hello 다음 도구를 설치 합니다.

* [최신 버전의 Visual Studio](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

로컬로 Docker 컨테이너 toorun 로컬 docker 클라이언트를 필요 합니다.
Hello를 사용할 수 있습니다 [Docker 도구 상자](https://www.docker.com/products/docker-toolbox)Hyper-v toobe 비활성화 해야 하거나 사용할 수 있습니다, [Windows 용 Docker](https://www.docker.com/get-docker), Hyper-v를 사용 하 고 Windows 10을 필요 합니다.

Docker 도구 상자를 사용 하 여 직접 해야 너무[hello Docker 클라이언트를 구성 합니다.](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. 웹앱 만들기
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Docker 지원 추가
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. 코드 편집 및 새로 고침
tooquickly 반복 변경은 컨테이너 내에서 응용 프로그램을 시작 하 고 IIS Express와 마찬가지로 보기 toomake 변경 내용을 계속 합니다.

1. 너무 hello 솔루션 구성 설정`Debug` 누릅니다  **&lt;CTRL + f 5 >** toobuild 프로그램 docker 이미지 및 로컬로 실행 합니다.

    Hello 컨테이너 이미지 빌드된 Docker 컨테이너에서 실행 되 면 Visual Studio 기본 브라우저에서 hello 웹 앱이 시작 됩니다.
    Hello Microsoft Edge 브라우저를 사용 하는 하거나 그렇지 않으면 오류가 있는 경우 참조 [문제 해결](vs-azure-tools-docker-troubleshooting-docker-errors.md) 섹션.
2. 여기서 여기 toomake 변경 내용이 있는 페이지에 대 한 toohello를 이동 합니다.
3. Studio tooVisual 돌아가서 열 `Views\Home\About.cshtml`합니다.
4. Hello hello 파일의 HTML 콘텐츠 toohello 끝 다음을 추가 하 고 hello 변경 내용을 저장 합니다.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Hello.NET 빌드 완료 된 후 이러한 선을 표시 hello 출력 창, 보기, 백 tooyour 브라우저 전환한 hello 페이지에 대 한 새로 고침 합니다.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. 변경 내용이 적용되었습니다.

## <a name="4-debug-with-breakpoints"></a>4. 중단점으로 디버깅
에서는 변경 내용이 할 경우가 종종 추가 hello 디버깅 Visual Studio의 기능을 활용 하 여 검사 합니다.

1. 자동으로 닫히고 반환 tooVisual Studio`Controllers\HomeController.cs`
2. Hello 다음 hello About() 메서드의 hello 내용을 바꿉니다.

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. 중단점 toohello hello의 왼쪽 집합 `string message`... 줄.
4. 적중  **&lt;f 5 >** toostart 디버깅 합니다.
5. 에 대 한 페이지 toohit toohello 중단점으로 이동 합니다.
6. TooVisual Studio tooview hello 중단점을 전환 하 고 메시지의 hello 값을 삽입 합니다.

   ![][2]

## <a name="summary"></a>요약
와 [Docker 용 Visual Studio 2015 Tools](https://aka.ms/DockerToolsForVS), Docker 컨테이너 내에서 개발의 hello 프로덕션 현실감 로컬로 작업할 hello 생산성을 얻을 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
[Visual Studio Docker 개발 문제 해결](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Visual Studio, Windows 및 Azure와 함께 Docker에 대해 자세히 알아보기
* [Visual Studio용 Docker 도구](http://aka.ms/dockertoolsforvs) - 컨테이너에서 .NET Core 코드를 개발함
* [Visual Studio Team Services용 Docker 도구](http://aka.ms/dockertoolsforvsts) -docker 컨테이너를 빌드하고 배포함
* [Visual Studio Code용 Docker 도구](http://aka.ms/dockertoolsforvscode) - 향후 제공될 더 많은 E2E 시나리오와 함께, docker 파일을 편집하기 위한 언어 서비스
* [Windows 컨테이너 정보](http://aka.ms/containers)- Windows Server 및 Nano Server 정보
* [Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service 콘텐츠](http://aka.ms/AzureContainerService)
* Docker가 있는 작업의 더 많은 예제를 참조 하십시오. [Docker 작업](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) hello에서 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 연결 [데모](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)합니다. Hello HealthClinic.biz 데모에서 자세한 퀵 스타트를 참조 하십시오. [Azure 개발자 도구 퀵 스타트](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)합니다.

## <a name="various-docker-tools"></a>다양한 Docker 도구
[일부 뛰어난 docker 도구 (Steve Lasker의 블로그)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>좋은 문서
[NGINX tooMicroservices 소개](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>프레젠테이션
* [Steve Lasker: VS 라이브 Las Vegas 2016 - Docker e2e](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [빌드 2016-여기서 있습니다에서 데모 @ 소개 tooASP.NET 코어](https://channel9.msdn.com/Events/Build/2016/B810)
* [컨테이너에서 .NET 앱 개발, Channel 9](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
