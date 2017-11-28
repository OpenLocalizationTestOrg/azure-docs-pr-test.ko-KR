---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(macOS) | Microsoft Docs"
description: "Mac 컴퓨터에 도구를 설치 하 고 IoT hub 만들고 hello IoT 허브에서 장치를 등록 합니다."
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
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="c4899-104">Hello 도구 (macOS) 가져오기</span><span class="sxs-lookup"><span data-stu-id="c4899-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4899-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="c4899-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="c4899-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c4899-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="c4899-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="c4899-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="c4899-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="c4899-108">What you will do</span></span>

- <span data-ttu-id="c4899-109">Git, Node.js, Gulp, Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="c4899-110">Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="c4899-111">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c4899-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="c4899-112">What you will learn</span></span>

<span data-ttu-id="c4899-113">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="c4899-114">어떻게 tooinstall [Git](https://git-scm.com/) 및 [Node.js](https://nodejs.org/en/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="c4899-115">Git는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="c4899-116">이 단원에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="c4899-117">Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="c4899-118">어떻게 toouse [NPM](https://www.npmjs.com/) tooinstall Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="c4899-119">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="c4899-120">NPM은 Node.js 용 hello 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="c4899-121">Tooinstall 어떻게 Visual Studio 코드.</span><span class="sxs-lookup"><span data-stu-id="c4899-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="c4899-122">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c4899-123">또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="c4899-124">어떻게 tooinstall Python 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="c4899-125">Python은 널리 사용되는 높은 수준의 범용 해석형 동적 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="c4899-126">어떻게 tooinstall hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="c4899-127">hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="c4899-128">명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="c4899-129">어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c4899-130">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="c4899-130">What you need</span></span>

- <span data-ttu-id="c4899-131">인터넷 연결 toodownload 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="c4899-132">OS X Yosemite(10.10) 이상을 실행하는 Mac 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="c4899-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c4899-133">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="c4899-133">Install Git and Node.js</span></span>

<span data-ttu-id="c4899-134">Git tooinstall 및 Node.js, 다음이 단계를 수행 하 여 hello Homebrew 패키지 관리 유틸리티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="c4899-135">Homebrew를 [다운로드](http://brew.sh/) 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="c4899-136">Homebrew를 이미 설치한 경우 2 toostep를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="c4899-137">키를 눌러 `Cmd + Space` 입력 `Terminal` tooopen 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="c4899-138">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="c4899-139">Hello 다음 명령을 실행 하 여 Git 및 Node.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="c4899-140">Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="c4899-140">Install Node.js development tools</span></span>

<span data-ttu-id="c4899-141">사용 하면 [gulp.js](http://gulpjs.com/) tooautomate 배포 및 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="c4899-142">tooinstall gulp: hello 다음 hello 터미널에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="c4899-143">Hello 설치 관련 문제에 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-gateway-kit-c-sim-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="c4899-144">노드, NPM 및 Gulp는 Node.js에서 개발 된 필요한 toorun 자동화 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="c4899-145">Python 설치</span><span class="sxs-lookup"><span data-stu-id="c4899-145">Install Python</span></span>

<span data-ttu-id="c4899-146">Mac OS X는 Python 2.7이 함께 제공되지만 Homebrew를 통해 Python을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="c4899-147">[Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/)(Mac OS X에 Python 설치)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4899-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="c4899-148">Python 및 pip hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="c4899-149">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-149">Install hello Azure CLI</span></span>

<span data-ttu-id="c4899-150">tooinstall hello Azure CLI 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c4899-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="c4899-151">Hello 명령을 hello 터미널에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="c4899-152">hello 설치에는 5 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="c4899-153">Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="c4899-154">Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-154">You should see hello following output if hello installation is successful.</span></span>

   ![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="c4899-156">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="c4899-156">Install Visual Studio Code</span></span>

<span data-ttu-id="c4899-157">Hello 자습서 tooedit 구성 파일에서 Visual Studio Code를 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="c4899-158">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="c4899-159">요약</span><span class="sxs-lookup"><span data-stu-id="c4899-159">Summary</span></span>

<span data-ttu-id="c4899-160">Mac 컴퓨터에 모든 hello 필요한 도구와 소프트웨어를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="c4899-161">다음 작업 toouse hello Azure CLI toocreate IoT hub 이며 IoT hub에 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4899-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4899-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4899-162">Next steps</span></span>
[<span data-ttu-id="c4899-163">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c4899-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
