---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(Windows) | Microsoft Docs"
description: "Windows를 실행하는 호스트 컴퓨터에 도구 및 소프트웨어를 설치하고, IoT Hub를 만들어 장치를 IoT Hub에 등록합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, IoT 클라우드 서비스, 사물 인터넷 소프트웨어, Azure CLI, Windows에 Git 설치, gulp 실행, Node Js Windows 설치, Windows에 NPM 설치, Windows에 Python 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0d8ba03df63d0b8657a9e275fc636e806c66b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="411da-104">도구 얻기(Windows 7 이상)</span><span class="sxs-lookup"><span data-stu-id="411da-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="411da-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="411da-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="411da-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="411da-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="411da-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="411da-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="411da-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="411da-108">What you will do</span></span>

- <span data-ttu-id="411da-109">Git, Node.js, Gulp, Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="411da-110">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="411da-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="411da-111">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="411da-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="411da-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="411da-112">What you will learn</span></span>

<span data-ttu-id="411da-113">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="411da-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="411da-114">[Git](https://git-scm.com/) 및 [Node.js](https://nodejs.org/en/)를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="411da-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="411da-115">Git는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="411da-116">이 단원에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="411da-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="411da-117">Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="411da-118">[NPM](https://www.npmjs.com/)을 사용하여 Node.js 개발 도구를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="411da-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="411da-119">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="411da-120">NPM은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="411da-121">Visual Studio Code 설치 방법</span><span class="sxs-lookup"><span data-stu-id="411da-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="411da-122">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="411da-123">또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="411da-124">Python을 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="411da-124">How to install Python.</span></span>
  - <span data-ttu-id="411da-125">Python은 널리 사용되는 높은 수준의 범용 해석형 동적 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="411da-126">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="411da-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="411da-127">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="411da-128">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="411da-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="411da-129">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="411da-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="411da-130">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="411da-130">What you need</span></span>

- <span data-ttu-id="411da-131">도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="411da-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="411da-132">Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="411da-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="411da-133">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="411da-133">Install Git and Node.js</span></span>

<span data-ttu-id="411da-134">다음 링크를 클릭하여 Windows용 Git 및 Node.js LTS를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="411da-135">Windows용 Git 얻기</span><span class="sxs-lookup"><span data-stu-id="411da-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="411da-136">Windows용 Node.js LTS 얻기</span><span class="sxs-lookup"><span data-stu-id="411da-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="411da-137">Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="411da-137">Install Node.js development tools</span></span>

<span data-ttu-id="411da-138">[gulp.js](http://gulpjs.com/)를 사용하여 스크립트 배포 및 실행을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="411da-139">`Windows + R`을 누르고 `cmd`를 입력한 후 `Enter`을 눌러 명령 프롬프트 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="411da-140">설치에 문제가 발생하면 [문제 해결 안내서](iot-hub-gateway-kit-c-troubleshooting.md)에서 일반적인 문제에 대한 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="411da-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="411da-141">Node.js에서 개발된 Automation 스크립트를 실행하려면 Node, NPM 및 Gulp가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="411da-142">Python 설치</span><span class="sxs-lookup"><span data-stu-id="411da-142">Install Python</span></span>

<span data-ttu-id="411da-143">Python 2.7, 3.4 또는 3.5에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="411da-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="411da-144">이 자습서에서 Python 2.7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="411da-145">Python을 이미 설치한 경우 다음 섹션으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="411da-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="411da-146">Windows용 Python 얻기</span><span class="sxs-lookup"><span data-stu-id="411da-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="411da-147">python.exe 및 pip.exe가 설치되어 있는 폴더의 경로를 시스템 `PATH` 환경 변수에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="411da-148">기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="411da-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="411da-149">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="411da-149">Install the Azure CLI</span></span>

<span data-ttu-id="411da-150">Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="411da-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="411da-151">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="411da-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="411da-152">다음 명령을 실행하여 CLI 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="411da-153">설치에는 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="411da-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="411da-154">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="411da-155">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="411da-155">You should see the following output if the installation is successful.</span></span>

   ![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="411da-157">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="411da-157">Install Visual Studio Code</span></span>

<span data-ttu-id="411da-158">이 자습서의 뒷부분에 나오는 Visual Studio 코드를 사용하여 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="411da-159">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/windows)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="411da-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="411da-160">요약</span><span class="sxs-lookup"><span data-stu-id="411da-160">Summary</span></span>

<span data-ttu-id="411da-161">호스트 컴퓨터에 필요한 모든 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="411da-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="411da-162">다음 작업은 Azure CLI를 사용하여 IoT Hub를 만들고 장치를 IoT Hub에 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="411da-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="411da-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="411da-163">Next steps</span></span>
[<span data-ttu-id="411da-164">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="411da-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
