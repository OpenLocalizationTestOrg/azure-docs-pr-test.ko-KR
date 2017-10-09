---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 2: 도구 다운로드(Windows) | Microsoft Docs"
description: "Windows를 실행 하는 호스트 컴퓨터에 hello 도구와 hello 소프트웨어를 설치 하 고 IoT 허브를 만듭니다. 다음 hello IoT 허브에서 장치를 등록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, IoT 클라우드 서비스, 사물 인터넷 소프트웨어, Azure CLI, Windows에 Git 설치, gulp 실행, Node Js Windows 설치, Windows에 NPM 설치, Windows에 Python 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="eb74e-104">Hello 도구 (Windows 7 이상) 가져오기</span><span class="sxs-lookup"><span data-stu-id="eb74e-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb74e-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="eb74e-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="eb74e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="eb74e-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="eb74e-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="eb74e-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="eb74e-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="eb74e-108">What you will do</span></span>

- <span data-ttu-id="eb74e-109">Git, Node.js, Gulp, Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="eb74e-110">Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="eb74e-111">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb74e-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="eb74e-112">What you will learn</span></span>

<span data-ttu-id="eb74e-113">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="eb74e-114">어떻게 tooinstall [Git](https://git-scm.com/) 및 [Node.js](https://nodejs.org/en/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="eb74e-115">Git는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="eb74e-116">이 단원에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="eb74e-117">Node.js는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="eb74e-118">어떻게 toouse [NPM](https://www.npmjs.com/) tooinstall Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="eb74e-119">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="eb74e-120">NPM은 Node.js 용 hello 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="eb74e-121">Tooinstall 어떻게 Visual Studio 코드.</span><span class="sxs-lookup"><span data-stu-id="eb74e-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="eb74e-122">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 플랫폼 간 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="eb74e-123">또한 디버깅, 포함된 Git 컨트롤, 구문 강조, 지능형 코드 완성, 스니펫 및 코드 리팩터링에 대해 탁월한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="eb74e-124">어떻게 tooinstall Python 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="eb74e-125">Python은 널리 사용되는 높은 수준의 범용 해석형 동적 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="eb74e-126">어떻게 tooinstall hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="eb74e-127">hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="eb74e-128">명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="eb74e-129">어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb74e-130">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="eb74e-130">What you need</span></span>

- <span data-ttu-id="eb74e-131">인터넷 연결 toodownload 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="eb74e-132">Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="eb74e-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="eb74e-133">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="eb74e-133">Install Git and Node.js</span></span>

<span data-ttu-id="eb74e-134">다음 링크 toodownload hello를 클릭 하 고 Git 및 Windows 용 Node.js LTS를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="eb74e-135">Windows용 Git 얻기</span><span class="sxs-lookup"><span data-stu-id="eb74e-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="eb74e-136">Windows용 Node.js LTS 얻기</span><span class="sxs-lookup"><span data-stu-id="eb74e-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="eb74e-137">Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="eb74e-137">Install Node.js development tools</span></span>

<span data-ttu-id="eb74e-138">사용 하면 [gulp.js](http://gulpjs.com/) tooautomate 배포 및 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="eb74e-139">키를 누릅니다 `Windows + R`, 형식 `cmd` 누릅니다 `Enter` tooopen 명령 프롬프트 창 실행된 hello 명령을 누른 다음:</span><span class="sxs-lookup"><span data-stu-id="eb74e-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="eb74e-140">Hello 설치 관련 문제에 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-gateway-kit-c-sim-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="eb74e-141">노드, NPM 및 Gulp는 Node.js에서 개발 된 필요한 toorun 자동화 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="eb74e-142">Python 설치</span><span class="sxs-lookup"><span data-stu-id="eb74e-142">Install Python</span></span>

<span data-ttu-id="eb74e-143">Python 2.7, 3.4 또는 3.5에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="eb74e-144">이 자습서에서 Python 2.7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="eb74e-145">Python을 이미 설치한 경우 다음 섹션 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="eb74e-146">Windows용 Python 얻기</span><span class="sxs-lookup"><span data-stu-id="eb74e-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="eb74e-147">또한 Python.exe 및 pip.exe는 설치 된 toohello 시스템 hello 폴더의 tooadd hello 경로 해야 `PATH` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="eb74e-148">기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="eb74e-149">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-149">Install hello Azure CLI</span></span>

<span data-ttu-id="eb74e-150">tooinstall hello Azure CLI 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="eb74e-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="eb74e-151">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="eb74e-152">Hello 다음 명령을 실행 하 여 hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="eb74e-153">hello 설치에는 5 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="eb74e-154">Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="eb74e-155">Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-155">You should see hello following output if hello installation is successful.</span></span>

   ![Azure CLI 설치 확인](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="eb74e-157">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="eb74e-157">Install Visual Studio Code</span></span>

<span data-ttu-id="eb74e-158">Hello 자습서 tooedit 구성 파일에서 Visual Studio Code를 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="eb74e-159">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/windows)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="eb74e-160">요약</span><span class="sxs-lookup"><span data-stu-id="eb74e-160">Summary</span></span>

<span data-ttu-id="eb74e-161">호스트 컴퓨터에서 모든 hello 필요한 도구와 소프트웨어를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="eb74e-162">다음 작업 toouse hello Azure CLI toocreate IoT hub 이며 IoT hub에 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb74e-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb74e-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb74e-163">Next steps</span></span>
[<span data-ttu-id="eb74e-164">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="eb74e-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
