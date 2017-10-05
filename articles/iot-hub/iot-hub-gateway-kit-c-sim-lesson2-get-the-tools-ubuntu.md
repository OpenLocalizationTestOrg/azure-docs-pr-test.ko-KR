---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(Ubuntu) | Microsoft Docs"
description: "Ubuntu를 실행하는 호스트 컴퓨터에 도구 및 소프트웨어를 설치하고, IoT Hub를 만들어 장치를 IoT Hub에 등록합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, IoT 클라우드 서비스, 사물 인터넷 소프트웨어, Azure CLI, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="48112-104">도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="48112-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48112-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="48112-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="48112-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="48112-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="48112-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="48112-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="48112-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="48112-108">What you will do</span></span>

- <span data-ttu-id="48112-109">Git, Node.js, Gulp, Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="48112-110">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="48112-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="48112-111">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="48112-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="48112-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="48112-112">What you will learn</span></span>

<span data-ttu-id="48112-113">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="48112-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="48112-114">Git 및 Node.js를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="48112-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="48112-115">Git는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="48112-116">이 단원에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="48112-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="48112-117">Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="48112-118">NPM을 사용하여 Node.js 개발 도구를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="48112-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="48112-119">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="48112-120">NPM은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="48112-121">Visual Studio Code 설치 방법</span><span class="sxs-lookup"><span data-stu-id="48112-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="48112-122">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="48112-123">또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="48112-124">Azure CLI를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="48112-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="48112-125">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="48112-126">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48112-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="48112-127">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="48112-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="48112-128">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="48112-128">What you need</span></span>

- <span data-ttu-id="48112-129">도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="48112-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="48112-130">Ubuntu 16.04 이상을 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="48112-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="48112-131">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="48112-131">Install Git and Node.js</span></span>

<span data-ttu-id="48112-132">Git 및 Node.js를 설치하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="48112-133">`Ctrl + Alt + T`를 눌러 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="48112-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="48112-134">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="48112-135">Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="48112-135">Install Node.js development tools</span></span>

<span data-ttu-id="48112-136">[gulp.js](http://gulpjs.com/)를 사용하여 스크립트 배포 및 실행을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="48112-137">gulp를 설치하려면 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="48112-138">설치에 문제가 발생하면 [문제 해결 안내서](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 일반적인 문제에 대한 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48112-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="48112-139">Node.js에서 개발된 Automation 스크립트를 실행하려면 Node, NPM 및 Gulp가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="48112-140">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="48112-140">Install the Azure CLI</span></span>

<span data-ttu-id="48112-141">Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="48112-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="48112-142">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="48112-143">설치에는 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48112-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="48112-144">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="48112-145">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48112-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="48112-146">![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="48112-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="48112-147">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="48112-147">Install Visual Studio Code</span></span>

<span data-ttu-id="48112-148">이 자습서의 뒷부분에 나오는 Visual Studio 코드를 사용하여 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="48112-149">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="48112-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="48112-150">요약</span><span class="sxs-lookup"><span data-stu-id="48112-150">Summary</span></span>

<span data-ttu-id="48112-151">호스트 컴퓨터에 필요한 모든 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="48112-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="48112-152">다음 작업은 Azure CLI를 사용하여 IoT Hub를 만들고 장치를 IoT Hub에 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48112-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48112-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48112-153">Next steps</span></span>
[<span data-ttu-id="48112-154">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="48112-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
