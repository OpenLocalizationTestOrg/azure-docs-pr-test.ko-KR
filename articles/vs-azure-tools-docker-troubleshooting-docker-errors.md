---
title: "Visual Studio를 사용 하 여 aaaTroubleshooting Docker 클라이언트 오류 windows | Microsoft Docs"
description: "Visual Studio toocreate를 사용할 때 발생 하는 문제를 해결 하 고 Visual Studio를 사용 하 여 Windows에서 웹 앱 tooDocker를 배포 합니다."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="e301a-103">Visual Studio Docker 개발 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e301a-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="e301a-104">Docker 미리 보기에 대 한 Visual Studio Tools을 사용 하는 경우에 hello 미리 보기의 hello 특성으로 인해 몇 가지 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="e301a-105">다음은 몇 가지 일반적인 문제 및 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="e301a-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="e301a-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="e301a-107">**Linux 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="e301a-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="e301a-108">.NET Core 웹 또는 콘솔 응용 프로그램을 디버그할 때 빌드 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="e301a-109">Windows 용 Docker hello 프로젝트 상주 하는 hello 드라이브를 공유 하는 관련된 toonot 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="e301a-110">Hello 다음과 같은 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="e301a-111">tooresolve이이 문제:</span><span class="sxs-lookup"><span data-stu-id="e301a-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="e301a-112">마우스 오른쪽 단추로 클릭 **Windows 용 Docker** 에 알림 영역 hello 선택한 후 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="e301a-113">선택 **드라이브 공유** hello 프로젝트 있는 hello 드라이브를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="e301a-114">**Windows 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="e301a-114">**Windows containers**</span></span>

<span data-ttu-id="e301a-115">hello 다음과 같은 문제는 Windows 컨테이너에서 특정 toodebugging.NET Framework 웹 및 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="e301a-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e301a-116">Prerequisites</span></span>

1. <span data-ttu-id="e301a-117">Visual Studio 2017 RC (또는 이상) hello.NET Core와 Docker 미리 보기 작업을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="e301a-118">최신 Windows 업데이트 패치가 있는 Windows 10 1주년 업데이트</span><span class="sxs-lookup"><span data-stu-id="e301a-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="e301a-119">특히 [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="e301a-120">[Windows용 Docker](https://docs.docker.com/docker-for-windows/)(빌드 1.13.0 이상)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="e301a-121">**TooWindows 컨테이너 전환** 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="e301a-122">Hello 알림 영역에서 클릭 **Windows 용 Docker**를 선택한 후 **tooWindows 컨테이너 스위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="e301a-123">Hello 컴퓨터를 다시 시작한 후에이 설정이 유지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="e301a-124">콘솔 응용 프로그램을 디버그하는 동안 Visual Studio의 출력 창에 콘솔 출력이 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="e301a-125">이것은 알려진된 문제가이 시나리오에 대 한 현재 설계 되지 않았습니다 hello Visual Studio 디버거 (msvsmon.exe)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="e301a-126">이 시나리오에 대한 지원은 이후 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="e301a-127">Visual studio에서 사용 하 여 hello 콘솔 응용 프로그램에서 toosee 출력 **Docker: 프로젝트 시작**,이 값은 너무**디버깅 하지 않고 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="e301a-128">Hello로 웹 응용 프로그램을 디버깅 릴리스 구성 실패 하 고 (403) 사용할 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="e301a-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="e301a-129">이 문제를 해결 toowork web.release.config hello 솔루션에서 열고 주석으로 처리 하거나 hello 다음 줄을 삭제:</span><span class="sxs-lookup"><span data-stu-id="e301a-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="e301a-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e301a-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="e301a-131">**Linux 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="e301a-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="e301a-132">없습니다 toovalidate 볼륨 매핑</span><span class="sxs-lookup"><span data-stu-id="e301a-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="e301a-133">볼륨 매핑은 필요한 tooshare hello 소스 코드와 hello 컨테이너에서 hello 앱 폴더와 응용 프로그램의 이진 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="e301a-134">특정 볼륨 매핑은 docker-compose.dev.debug.yml 및 docker-compose.dev.release.yml 내에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="e301a-135">호스트 컴퓨터에서 파일을 변경할, hello 컨테이너 유사한 폴더 구조에서 이러한 변경 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="e301a-136">tooenable 볼륨 매핑:</span><span class="sxs-lookup"><span data-stu-id="e301a-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="e301a-137">클릭 **Moby** hello 알림 영역 및 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="e301a-138">**공유 드라이브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="e301a-139">% USERPROFILE % 있는 프로젝트 및 hello 드라이브를 호스트 하는 hello 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="e301a-140">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-140">Click **Apply**.</span></span>

<span data-ttu-id="e301a-141">tootest 볼륨 매핑에 작동 하는 경우 다시 작성 하 고 하나 이상의 드라이브, 이전에 공유 또는 명령 프롬프트에서 코드를 다음 hello 실행 된 후 Visual Studio 내에서 f5 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="e301a-142">이 예제에서는 사용자 폴더가 드라이브 C에 있으며 공유되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="e301a-143">다른 드라이브를 공유하는 경우 필요에 따라 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="e301a-144">Hello 코드 hello Linux 컨테이너에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="e301a-145">디렉터리 hello 사용자/공용 폴더에서 목록을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="e301a-146">아무 파일도 표시되지 않고, /c/Users/Public 폴더는 비어 있지 않다면, 볼륨 매핑이 제대로 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="e301a-147">Hello의 toohello 웜 디렉터리 toosee hello 내용을 변경 `/c/Users/Public` 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="e301a-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="e301a-148">Linux Vm을 사용 하는 경우에 hello 컨테이너 파일 시스템은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="e301a-149">빌드 : "PrepareForBuild" 태스크가 예기치 않게 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="e301a-150">Microsoft.DotNet.Docker.CommandLine.ClientException: 오류가 동안 tooconnect 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="e301a-151">해당 hello 기본 Docker 호스트가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="e301a-152">명령 프롬프트를 열고 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="e301a-153">이 오류를 반환 하면 경우 toostart hello 시도 **Windows 용 Docker** 데스크톱 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="e301a-154">Hello를 데스크톱 응용 프로그램을 실행 중인 경우 다음 **Moby** hello 알림 영역에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="e301a-155">**모비**를 마우스 오른쪽 단추로 클릭하고 **설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="e301a-156">**다시 설정**을 클릭한 다음 Docker를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="e301a-157">오류 대화 상자가 tooadd Docker 지원 하려고 할 때 발생 또는 디버그 (F5)는 컨테이너에서 ASP.NET Core 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e301a-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="e301a-158">제거 후 확장을 설치, Visual Studio에서 프레임 워크 MEF (Managed Extensibility) 캐시 hello 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="e301a-159">이 경우 Docker 지원 추가 및 toorun 시도 하는 다양 한 오류 메시지가 발생할 하거나 (F5) ASP.NET Core 응용 프로그램을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="e301a-160">임시 해결 방법으로 다음 단계를 다시 생성 하 고 toodelete hello MEF 캐시가 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="e301a-161">Visual Studio의 모든 인스턴스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="e301a-162">%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="e301a-163">Hello 다음 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="e301a-164">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="e301a-165">Hello 시나리오를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e301a-165">Attempt hello scenario again.</span></span>
