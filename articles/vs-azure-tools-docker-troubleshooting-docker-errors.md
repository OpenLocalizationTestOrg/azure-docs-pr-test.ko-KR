---
title: "Visual Studio를 사용하여 Windows에서 Docker 클라이언트 오류 문제 해결 | Microsoft Docs"
description: "Visual Studio를 사용하여 웹앱을 만들고 Docker에 배포하는 경우 발생하는 문제를 해결합니다."
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
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="fac60-103">Visual Studio Docker 개발 문제 해결</span><span class="sxs-lookup"><span data-stu-id="fac60-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="fac60-104">Visual Studio Tools for Docker 미리 보기로 작업하는 경우 미리 보기의 특성으로 인해 몇 가지 문제가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="fac60-105">다음은 몇 가지 일반적인 문제 및 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="fac60-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="fac60-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="fac60-107">**Linux 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="fac60-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="fac60-108">.NET Core 웹 또는 콘솔 응용 프로그램을 디버그할 때 빌드 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="fac60-109">이 오류는 프로젝트가 Windows용 Docker에 있을 때 드라이브 공유와 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="fac60-110">다음과 같은 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="fac60-111">이 문제를 해결하려면:</span><span class="sxs-lookup"><span data-stu-id="fac60-111">To resolve this issue:</span></span>

1. <span data-ttu-id="fac60-112">알림 영역에서 **Windows용 Docker**를 마우스 오른쪽 단추로 클릭한 다음 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="fac60-113">**공유 드라이브**를 선택하고 프로젝트가 있는 드라이브를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="fac60-114">**Windows 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="fac60-114">**Windows containers**</span></span>

<span data-ttu-id="fac60-115">다음 문제는 Windows 컨테이너에서 .NET Framework 웹 및 콘솔 응용 프로그램 디버깅과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="fac60-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fac60-116">Prerequisites</span></span>

1. <span data-ttu-id="fac60-117">.NET Core 및 Docker 미리 보기 워크로드가 있는 Visual Studio 2017 RC(또는 이상)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="fac60-118">최신 Windows 업데이트 패치가 있는 Windows 10 1주년 업데이트</span><span class="sxs-lookup"><span data-stu-id="fac60-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="fac60-119">특히 [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="fac60-120">[Windows용 Docker](https://docs.docker.com/docker-for-windows/)(빌드 1.13.0 이상)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="fac60-121">**Windows 컨테이너로 전환**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="fac60-122">알림 영역에서 **Windows용 Docker**를 클릭한 다음 **Windows 컨테이너로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="fac60-123">컴퓨터가 다시 시작되면 이 설정이 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="fac60-124">콘솔 응용 프로그램을 디버그하는 동안 Visual Studio의 출력 창에 콘솔 출력이 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="fac60-125">이것은 현재 이 시나리오에 맞게 디자인되지 않은 Visual Studio 디버거(msvsmon.exe)의 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="fac60-126">이 시나리오에 대한 지원은 이후 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="fac60-127">Visual Studio에서 콘솔 응용 프로그램의 출력을 보려면 **디버그하지 않고 시작**에 해당하는 **Docker: 프로젝트 시작**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="fac60-128">릴리스 구성을 사용하여 웹 응용 프로그램을 디버그하면 (403) 사용 권한 없음 오류를 나타내며 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="fac60-129">이 문제를 해결하려면 솔루션에서 web.release.config를 열고 다음 줄을 주석 처리하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="fac60-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="fac60-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="fac60-131">**Linux 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="fac60-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="fac60-132">볼륨 매핑의 유효성을 검사할 수 없음</span><span class="sxs-lookup"><span data-stu-id="fac60-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="fac60-133">볼륨 매핑의 경우 응용 프로그램의 소스 코드 및 이진 파일을 컨테이너에 있는 앱 폴더와 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="fac60-134">특정 볼륨 매핑은 docker-compose.dev.debug.yml 및 docker-compose.dev.release.yml 내에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="fac60-135">호스트 컴퓨터에서 파일이 변경되면 컨테이너는 비슷한 폴더 구조에서 이러한 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="fac60-136">볼륨 매핑을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="fac60-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="fac60-137">알림 영역에서 **모비**를 클릭하고 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="fac60-138">**공유 드라이브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="fac60-139">프로젝트를 호스팅하는 드라이브와 %USERPROFILE%이 있는 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="fac60-140">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-140">Click **Apply**.</span></span>

<span data-ttu-id="fac60-141">볼륨 매핑이 작동하는지를 테스트하려면 하나 이상의 드라이브가 공유된 후 Visual Studio 내에서 다시 빌드하고 F5를 선택하거나 명령 프롬프트에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="fac60-142">이 예제에서는 사용자 폴더가 드라이브 C에 있으며 공유되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="fac60-143">다른 드라이브를 공유하는 경우 필요에 따라 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="fac60-144">Linux 컨테이너에서 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="fac60-145">Users/Public 폴더의 디렉토리 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="fac60-146">아무 파일도 표시되지 않고, /c/Users/Public 폴더는 비어 있지 않다면, 볼륨 매핑이 제대로 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="fac60-147">`/c/Users/Public` 디렉토리의 내용을 보려면 웜홀 디렉토리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="fac60-148">Linux VM에서 작업하는 경우 컨테이너 파일 시스템은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="fac60-149">빌드 : "PrepareForBuild" 태스크가 예기치 않게 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="fac60-150">Microsoft.DotNet.Docker.CommandLine.ClientException: 연결하려는 동안 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="fac60-151">기본 Docker 호스트가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="fac60-152">명령 프롬프트를 열고 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="fac60-153">오류를 반환하는 경우 **Windows용 Docker** 데스크톱 앱을 시작하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="fac60-154">데스크톱 앱을 실행하는 경우 알림 영역에 **모비**가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="fac60-155">**모비**를 마우스 오른쪽 단추로 클릭하고 **설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="fac60-156">**다시 설정**을 클릭한 다음 Docker를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="fac60-157">컨테이너에서 Docker 지원 추가 또는 ASP.NET Core 응용 프로그램 디버그(F5)를 시도할 때 오류 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="fac60-158">확장을 제거하고 설치한 후에 Visual Studio의 MEF(Managed Extensibility Framework) 캐시가 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="fac60-159">이 경우에는 Docker 지원을 추가 및/또는 ASP.NET Core 응용 프로그램을 실행 또는 디버그(F5)할 때 다양한 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="fac60-160">임시 해결 방법으로 MEF 캐시를 삭제하고 다시 생성하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="fac60-161">Visual Studio의 모든 인스턴스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="fac60-162">%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="fac60-163">다음 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="fac60-164">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="fac60-165">시나리오를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fac60-165">Attempt the scenario again.</span></span>
