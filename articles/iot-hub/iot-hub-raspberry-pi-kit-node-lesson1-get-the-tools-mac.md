---
title: "연결 라스베리 Pi (노드) tooAzure IoT-1 단원: 도구 (macOS) 가져오기 | Microsoft Docs"
description: "다운로드 하 고 macOS에서 hello 필요한 도구와 hello 첫 번째 Pi에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Python Mac 설치, Mac에 Git 설치, gulp 실행, Node Js Mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="4acd6-104">Hello 도구 (macOS 10.10) 가져오기</span><span class="sxs-lookup"><span data-stu-id="4acd6-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4acd6-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="4acd6-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="4acd6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4acd6-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="4acd6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="4acd6-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="4acd6-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="4acd6-108">What you will do</span></span>
<span data-ttu-id="4acd6-109">Hello 개발 도구와 hello 첫 번째 라스베리 Pi 3에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="4acd6-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4acd6-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="4acd6-111">What you will learn</span></span>
<span data-ttu-id="4acd6-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-112">In this article, you will learn:</span></span>

* <span data-ttu-id="4acd6-113">어떻게 tooinstall Git 및 Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="4acd6-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="4acd6-115">이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="4acd6-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="4acd6-117">어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="4acd6-118">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="4acd6-119">[NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4acd6-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="4acd6-120">What you need</span></span>
<span data-ttu-id="4acd6-121">toocomplete이 작업을이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="4acd6-122">인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="4acd6-123">macOS Yosemite(10.10) 이상을 실행하는 Mac.</span><span class="sxs-lookup"><span data-stu-id="4acd6-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="4acd6-124">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="4acd6-124">Install Git and Node.js</span></span>
<span data-ttu-id="4acd6-125">Git tooinstall 및 Node.js를 사용 하 여 hello [Homebrew](http://brew.sh) 다음이 단계를 수행 하 여 관리 유틸리티를 패키지:</span><span class="sxs-lookup"><span data-stu-id="4acd6-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="4acd6-126">Homebrew를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-126">Install Homebrew.</span></span> <span data-ttu-id="4acd6-127">Homebrew를 이미 설치한 경우 2 toostep를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="4acd6-128">키를 눌러 `Cmd + Space` 입력 `Terminal` tooopen 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="4acd6-129">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="4acd6-130">Hello 다음 명령을 실행 하 여 Git 및 Node.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="4acd6-131">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="4acd6-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="4acd6-132">사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooPi의 tooautomate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="4acd6-133">사용 하 여 hello [장치-검색-cli](https://github.com/Azure/device-discovery-cli) IoT 장치에 대 한 tooretrieve 네트워크 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="4acd6-134">설치 `gulp` 및 `device-discovery-cli` hello 다음 hello 터미널에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="4acd6-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="4acd6-135">MacOS에서 Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-raspberry-pi-kit-node-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="4acd6-136">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="4acd6-136">Install Visual Studio Code</span></span>
<span data-ttu-id="4acd6-137">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="4acd6-138">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="4acd6-139">이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="4acd6-140">요약</span><span class="sxs-lookup"><span data-stu-id="4acd6-140">Summary</span></span>
<span data-ttu-id="4acd6-141">필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="4acd6-142">hello 다음 작업은 toocreate, 배포 및 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acd6-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4acd6-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4acd6-143">Next steps</span></span>
[<span data-ttu-id="4acd6-144">만들기 및 hello 깜박임 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4acd6-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

