---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(macOS) | Microsoft Docs"
description: "Mac 컴퓨터에 도구를 설치하고, IoT Hub를 만들고, IoT Hub에 장치를 등록합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, IoT 클라우드 서비스, 사물 인터넷 소프트웨어, Azure CLI, Python Mac 설치, Mac에 Git 설치, gulp 실행, Node Js Mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="0ecbf-104">도구 얻기(macOS)</span><span class="sxs-lookup"><span data-stu-id="0ecbf-104">Get the tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ecbf-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="0ecbf-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="0ecbf-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="0ecbf-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="0ecbf-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="0ecbf-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="0ecbf-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="0ecbf-108">What you will do</span></span>

- <span data-ttu-id="0ecbf-109">Git, Node.js, Gulp, Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="0ecbf-110">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="0ecbf-111">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0ecbf-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="0ecbf-112">What you will learn</span></span>

<span data-ttu-id="0ecbf-113">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0ecbf-114">[Git](https://git-scm.com/) 및 [Node.js](https://nodejs.org/en/)를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="0ecbf-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="0ecbf-115">Git는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="0ecbf-116">이 단원에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="0ecbf-117">Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="0ecbf-118">[NPM](https://www.npmjs.com/)을 사용하여 Node.js 개발 도구를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="0ecbf-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="0ecbf-119">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="0ecbf-120">NPM은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="0ecbf-121">Visual Studio Code 설치 방법</span><span class="sxs-lookup"><span data-stu-id="0ecbf-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="0ecbf-122">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="0ecbf-123">또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="0ecbf-124">Python을 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-124">How to install Python.</span></span>
  - <span data-ttu-id="0ecbf-125">Python은 널리 사용되는 높은 수준의 범용 해석형 동적 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="0ecbf-126">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="0ecbf-127">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0ecbf-128">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="0ecbf-129">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="0ecbf-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0ecbf-130">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="0ecbf-130">What you need</span></span>

- <span data-ttu-id="0ecbf-131">도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="0ecbf-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="0ecbf-132">OS X Yosemite(10.10) 이상을 실행하는 Mac 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="0ecbf-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="0ecbf-133">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="0ecbf-133">Install Git and Node.js</span></span>

<span data-ttu-id="0ecbf-134">Git 및 Node.js를 설치하려면 다음 단계를 따라 Homebrew 패키지 관리 유틸리티를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="0ecbf-135">Homebrew를 [다운로드](http://brew.sh/) 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="0ecbf-136">Homebrew를 이미 설치한 경우 2단계로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="0ecbf-137">`Cmd + Space`를 누르고 `Terminal`을 입력하여 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="0ecbf-138">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="0ecbf-139">다음 명령을 실행하여 Git 및 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="0ecbf-140">Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="0ecbf-140">Install Node.js development tools</span></span>

<span data-ttu-id="0ecbf-141">[gulp.js](http://gulpjs.com/)를 사용하여 스크립트 배포 및 실행을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="0ecbf-142">gulp를 설치하려면 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="0ecbf-143">설치에 문제가 발생하면 [문제 해결 안내서](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 일반적인 문제에 대한 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="0ecbf-144">Node.js에서 개발된 Automation 스크립트를 실행하려면 Node, NPM 및 Gulp가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="0ecbf-145">Python 설치</span><span class="sxs-lookup"><span data-stu-id="0ecbf-145">Install Python</span></span>

<span data-ttu-id="0ecbf-146">Mac OS X는 Python 2.7이 함께 제공되지만 Homebrew를 통해 Python을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="0ecbf-147">[Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/)(Mac OS X에 Python 설치)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="0ecbf-148">다음 명령을 실행하여 Python 및 pip를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="0ecbf-149">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="0ecbf-149">Install the Azure CLI</span></span>

<span data-ttu-id="0ecbf-150">Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0ecbf-151">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="0ecbf-152">설치에는 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="0ecbf-153">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="0ecbf-154">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-154">You should see the following output if the installation is successful.</span></span>

   ![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="0ecbf-156">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="0ecbf-156">Install Visual Studio Code</span></span>

<span data-ttu-id="0ecbf-157">이 자습서의 뒷부분에 나오는 Visual Studio 코드를 사용하여 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="0ecbf-158">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="0ecbf-159">요약</span><span class="sxs-lookup"><span data-stu-id="0ecbf-159">Summary</span></span>

<span data-ttu-id="0ecbf-160">Mac 컴퓨터에 필요한 도구 및 소프트웨어를 모두 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="0ecbf-161">다음 작업은 Azure CLI를 사용하여 IoT Hub를 만들고 장치를 IoT Hub에 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecbf-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ecbf-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ecbf-162">Next steps</span></span>
[<span data-ttu-id="0ecbf-163">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="0ecbf-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
