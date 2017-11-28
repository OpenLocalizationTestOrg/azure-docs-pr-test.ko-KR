---
title: "로컬 Docker 컨테이너에서 앱 디버깅 | Microsoft Docs"
description: "로컬 Docker 컨테이너에서 실행 중인 앱을 수정하고, 편집 및 새로 고침을 통해 컨테이너를 새로 고치고, 디버깅 중단점을 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: fcd58736d8915a61683a416fb9bf3892ba7b7bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="1c668-103">로컬 Docker 컨테이너에서 앱 디버깅</span><span class="sxs-lookup"><span data-stu-id="1c668-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="1c668-104">개요</span><span class="sxs-lookup"><span data-stu-id="1c668-104">Overview</span></span>
<span data-ttu-id="1c668-105">Visual Studio Tools for Docker는 Linux Docker 컨테이너에서 로컬로 응용 프로그램을 개발하고 유효성을 검사하는 일관된 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-105">The Visual Studio Tools for Docker provides a consistent way to develop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="1c668-106">코드를 변경할 때마다 컨테이너를 다시 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="1c668-107">이 문서에서는 "편집 및 새로 고침" 기능을 사용하여 로컬 Docker 컨테이너에서 ASP.NET Core 웹앱을 시작하고 필요한 내용을 변경한 다음 브라우저를 새로 고쳐 변경 내용을 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="1c668-108">또한 이 문서에서는 디버깅을 위한 중단점 설정 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="1c668-109">Windows 컨테이너 지원은 향후 릴리스에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="1c668-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1c668-110">Prerequisites</span></span>
<span data-ttu-id="1c668-111">다음과 같은 도구를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="1c668-112">최신 버전의 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c668-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="1c668-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="1c668-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="1c668-114">로컬에서 Docker 컨테이너를 실행하려면 로컬 Docker 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="1c668-115">[Docker 도구 상자](https://www.docker.com/products/docker-toolbox)는 Hyper-V를 비활성화한 후 사용할 수 있습니다. 또는 [Windows용 Docker](https://www.docker.com/get-docker)(Hyper-V를 사용하고 Windows 10을 필요로 함)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="1c668-116">Docker 도구 상자를 사용하는 경우 [Docker 클라이언트를 구성](vs-azure-tools-docker-setup.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="1c668-117">1. 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1c668-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="1c668-118">2. Docker 지원 추가</span><span class="sxs-lookup"><span data-stu-id="1c668-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="1c668-119">3. 코드 편집 및 새로 고침</span><span class="sxs-lookup"><span data-stu-id="1c668-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="1c668-120">변경을 신속하게 반복할 수 있도록, 응용 프로그램을 컨테이너에서 시작하고, IIS Express에서 하는 것처럼 변경 내용을 보며, 계속해서 변경해 나갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="1c668-121">솔루션 구성을 `Debug`로 설정하고 **&lt;CTRL + F5>** 키를 눌러 Docker 이미지를 빌드하고 로컬에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="1c668-122">컨테이너 이미지가 빌드되고 Docker 컨테이너에서 실행되면 Visual Studio는 기본 브라우저에서 웹앱을 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-122">Once the container image has been built and is running in a Docker container, Visual Studio will launch the Web app in your default browser.</span></span>
    <span data-ttu-id="1c668-123">Microsoft Edge 브라우저를 사용하거나 달리 오류가 있는 경우 [문제 해결](vs-azure-tools-docker-troubleshooting-docker-errors.md) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c668-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="1c668-124">정보 페이지로 이동하며 정보 페이지에서 변경을 수행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="1c668-125">Visual Studio로 돌아가서 `Views\Home\About.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="1c668-126">파일의 끝에 다음 HTML 콘텐츠를 추가하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="1c668-127">출력 창을 보는 가운데 .NET 빌드가 완료되고 이러한 줄이 표시될 때 브라우저로 전환하고 정보 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="1c668-128">변경 내용이 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="1c668-129">4. 중단점으로 디버깅</span><span class="sxs-lookup"><span data-stu-id="1c668-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="1c668-130">흔히 변경은 Visual Studio의 디버깅 기능을 활용한 추가적인 검사를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="1c668-131">Visual Studio로 돌아가서 `Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="1c668-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="1c668-132">About() 메서드 내용을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="1c668-133">`string message`... 줄 왼쪽에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="1c668-134">**&lt;F5>** 키를 눌러 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="1c668-135">중단점에 도달하려면 정보 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="1c668-136">Visual Studio로 전환하여 중단점을 보고, 메시지의 값을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="1c668-137">요약</span><span class="sxs-lookup"><span data-stu-id="1c668-137">Summary</span></span>
<span data-ttu-id="1c668-138">[Visual Studio 2015용 Docker 도구](https://aka.ms/DockerToolsForVS)를 사용하여, Docker 컨테이너 내에서 개발하는 프로덕션 현실감과 함께 로컬에서 작업하는 생산성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c668-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1c668-139">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1c668-139">Troubleshooting</span></span>
[<span data-ttu-id="1c668-140">Visual Studio Docker 개발 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1c668-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="1c668-141">Visual Studio, Windows 및 Azure와 함께 Docker에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="1c668-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="1c668-142">[Visual Studio용 Docker 도구](http://aka.ms/dockertoolsforvs) - 컨테이너에서 .NET Core 코드를 개발함</span><span class="sxs-lookup"><span data-stu-id="1c668-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="1c668-143">[Visual Studio Team Services용 Docker 도구](http://aka.ms/dockertoolsforvsts) -docker 컨테이너를 빌드하고 배포함</span><span class="sxs-lookup"><span data-stu-id="1c668-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="1c668-144">[Visual Studio Code용 Docker 도구](http://aka.ms/dockertoolsforvscode) - 향후 제공될 더 많은 E2E 시나리오와 함께, docker 파일을 편집하기 위한 언어 서비스</span><span class="sxs-lookup"><span data-stu-id="1c668-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="1c668-145">[Windows 컨테이너 정보](http://aka.ms/containers)- Windows Server 및 Nano Server 정보</span><span class="sxs-lookup"><span data-stu-id="1c668-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="1c668-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service 콘텐츠](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="1c668-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="1c668-147">Docker를 사용한 더 많은 예는 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [데모](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)의 [Docker 작업](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c668-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="1c668-148">HealthClinic.biz 데모에서 더 빠른 시작은 [Azure 개발자 도구 빠른 시작](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c668-148">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="1c668-149">다양한 Docker 도구</span><span class="sxs-lookup"><span data-stu-id="1c668-149">Various Docker tools</span></span>
[<span data-ttu-id="1c668-150">일부 뛰어난 docker 도구 (Steve Lasker의 블로그)</span><span class="sxs-lookup"><span data-stu-id="1c668-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="1c668-151">좋은 문서</span><span class="sxs-lookup"><span data-stu-id="1c668-151">Good articles</span></span>
[<span data-ttu-id="1c668-152">NGINX의 마이크로 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="1c668-152">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="1c668-153">프레젠테이션</span><span class="sxs-lookup"><span data-stu-id="1c668-153">Presentations</span></span>
* [<span data-ttu-id="1c668-154">Steve Lasker: VS 라이브 Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="1c668-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="1c668-155">ASP.NET Core @ 빌드 2016 - Where You At Demo 소개</span><span class="sxs-lookup"><span data-stu-id="1c668-155">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="1c668-156">컨테이너에서 .NET 앱 개발, Channel 9</span><span class="sxs-lookup"><span data-stu-id="1c668-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
