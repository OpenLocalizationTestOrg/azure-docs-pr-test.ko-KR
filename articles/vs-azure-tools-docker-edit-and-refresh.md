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
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="f395f-103">로컬 Docker 컨테이너에서 앱 디버깅</span><span class="sxs-lookup"><span data-stu-id="f395f-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="f395f-104">개요</span><span class="sxs-lookup"><span data-stu-id="f395f-104">Overview</span></span>
<span data-ttu-id="f395f-105">hello Visual Studio Tools for Docker에 일관 된 방식으로 toodevelop 하며 Linux Docker 컨테이너에서 로컬로 응용 프로그램의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="f395f-106">Toorestart hello 컨테이너 코드 변경 될 때마다 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="f395f-107">이 문서에서는 toouse hello 기능 toostart "편집 및 새로 고침" 로컬 Docker 컨테이너에서 ASP.NET Core 웹 앱, 필요한 변경 하 고 해당 변경 내용을 hello 브라우저 toosee를 새로 고칩니다 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="f395f-108">또한 이렇게 하면 어떻게 tooset 디버깅 중단점.</span><span class="sxs-lookup"><span data-stu-id="f395f-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="f395f-109">Windows 컨테이너 지원은 향후 릴리스에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f395f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f395f-110">Prerequisites</span></span>
<span data-ttu-id="f395f-111">hello 다음 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="f395f-112">최신 버전의 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f395f-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="f395f-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="f395f-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="f395f-114">로컬로 Docker 컨테이너 toorun 로컬 docker 클라이언트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="f395f-115">Hello를 사용할 수 있습니다 [Docker 도구 상자](https://www.docker.com/products/docker-toolbox)Hyper-v toobe 비활성화 해야 하거나 사용할 수 있습니다, [Windows 용 Docker](https://www.docker.com/get-docker), Hyper-v를 사용 하 고 Windows 10을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="f395f-116">Docker 도구 상자를 사용 하 여 직접 해야 너무[hello Docker 클라이언트를 구성 합니다.](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="f395f-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="f395f-117">1. 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f395f-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="f395f-118">2. Docker 지원 추가</span><span class="sxs-lookup"><span data-stu-id="f395f-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="f395f-119">3. 코드 편집 및 새로 고침</span><span class="sxs-lookup"><span data-stu-id="f395f-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="f395f-120">tooquickly 반복 변경은 컨테이너 내에서 응용 프로그램을 시작 하 고 IIS Express와 마찬가지로 보기 toomake 변경 내용을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="f395f-121">너무 hello 솔루션 구성 설정`Debug` 누릅니다  **&lt;CTRL + f 5 >** toobuild 프로그램 docker 이미지 및 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="f395f-122">Hello 컨테이너 이미지 빌드된 Docker 컨테이너에서 실행 되 면 Visual Studio 기본 브라우저에서 hello 웹 앱이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="f395f-123">Hello Microsoft Edge 브라우저를 사용 하는 하거나 그렇지 않으면 오류가 있는 경우 참조 [문제 해결](vs-azure-tools-docker-troubleshooting-docker-errors.md) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f395f-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="f395f-124">여기서 여기 toomake 변경 내용이 있는 페이지에 대 한 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="f395f-125">Studio tooVisual 돌아가서 열 `Views\Home\About.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="f395f-126">Hello hello 파일의 HTML 콘텐츠 toohello 끝 다음을 추가 하 고 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="f395f-127">Hello.NET 빌드 완료 된 후 이러한 선을 표시 hello 출력 창, 보기, 백 tooyour 브라우저 전환한 hello 페이지에 대 한 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="f395f-128">변경 내용이 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="f395f-129">4. 중단점으로 디버깅</span><span class="sxs-lookup"><span data-stu-id="f395f-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="f395f-130">에서는 변경 내용이 할 경우가 종종 추가 hello 디버깅 Visual Studio의 기능을 활용 하 여 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="f395f-131">자동으로 닫히고 반환 tooVisual Studio`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="f395f-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="f395f-132">Hello 다음 hello About() 메서드의 hello 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="f395f-133">중단점 toohello hello의 왼쪽 집합 `string message`... 줄.</span><span class="sxs-lookup"><span data-stu-id="f395f-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="f395f-134">적중  **&lt;f 5 >** toostart 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="f395f-135">에 대 한 페이지 toohit toohello 중단점으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="f395f-136">TooVisual Studio tooview hello 중단점을 전환 하 고 메시지의 hello 값을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="f395f-137">요약</span><span class="sxs-lookup"><span data-stu-id="f395f-137">Summary</span></span>
<span data-ttu-id="f395f-138">와 [Docker 용 Visual Studio 2015 Tools](https://aka.ms/DockerToolsForVS), Docker 컨테이너 내에서 개발의 hello 프로덕션 현실감 로컬로 작업할 hello 생산성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f395f-139">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f395f-139">Troubleshooting</span></span>
[<span data-ttu-id="f395f-140">Visual Studio Docker 개발 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f395f-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="f395f-141">Visual Studio, Windows 및 Azure와 함께 Docker에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="f395f-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="f395f-142">[Visual Studio용 Docker 도구](http://aka.ms/dockertoolsforvs) - 컨테이너에서 .NET Core 코드를 개발함</span><span class="sxs-lookup"><span data-stu-id="f395f-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="f395f-143">[Visual Studio Team Services용 Docker 도구](http://aka.ms/dockertoolsforvsts) -docker 컨테이너를 빌드하고 배포함</span><span class="sxs-lookup"><span data-stu-id="f395f-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="f395f-144">[Visual Studio Code용 Docker 도구](http://aka.ms/dockertoolsforvscode) - 향후 제공될 더 많은 E2E 시나리오와 함께, docker 파일을 편집하기 위한 언어 서비스</span><span class="sxs-lookup"><span data-stu-id="f395f-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="f395f-145">[Windows 컨테이너 정보](http://aka.ms/containers)- Windows Server 및 Nano Server 정보</span><span class="sxs-lookup"><span data-stu-id="f395f-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="f395f-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service 콘텐츠](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="f395f-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="f395f-147">Docker가 있는 작업의 더 많은 예제를 참조 하십시오. [Docker 작업](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) hello에서 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 연결 [데모](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="f395f-148">Hello HealthClinic.biz 데모에서 자세한 퀵 스타트를 참조 하십시오. [Azure 개발자 도구 퀵 스타트](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)합니다.</span><span class="sxs-lookup"><span data-stu-id="f395f-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="f395f-149">다양한 Docker 도구</span><span class="sxs-lookup"><span data-stu-id="f395f-149">Various Docker tools</span></span>
[<span data-ttu-id="f395f-150">일부 뛰어난 docker 도구 (Steve Lasker의 블로그)</span><span class="sxs-lookup"><span data-stu-id="f395f-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="f395f-151">좋은 문서</span><span class="sxs-lookup"><span data-stu-id="f395f-151">Good articles</span></span>
[<span data-ttu-id="f395f-152">NGINX tooMicroservices 소개</span><span class="sxs-lookup"><span data-stu-id="f395f-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="f395f-153">프레젠테이션</span><span class="sxs-lookup"><span data-stu-id="f395f-153">Presentations</span></span>
* [<span data-ttu-id="f395f-154">Steve Lasker: VS 라이브 Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="f395f-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="f395f-155">빌드 2016-여기서 있습니다에서 데모 @ 소개 tooASP.NET 코어</span><span class="sxs-lookup"><span data-stu-id="f395f-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="f395f-156">컨테이너에서 .NET 앱 개발, Channel 9</span><span class="sxs-lookup"><span data-stu-id="f395f-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
