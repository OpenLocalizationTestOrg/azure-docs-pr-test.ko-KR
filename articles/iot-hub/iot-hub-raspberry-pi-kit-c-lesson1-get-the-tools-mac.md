---
title: "Connect Raspberry Pi (C) tooAzure IoT-1 단원: 도구 (macOS) 가져오기 | Microsoft Docs"
description: "다운로드 하 고 macOS에서 hello 필요한 도구와 hello 첫 번째 Pi에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, mac에 git 설치, gulp 실행, node js mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="9ea3b-104">Hello 도구 (macOS 10.10) 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ea3b-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ea3b-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="9ea3b-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="9ea3b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="9ea3b-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="9ea3b-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="9ea3b-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="9ea3b-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="9ea3b-108">What you will do</span></span>
<span data-ttu-id="9ea3b-109">Hello 개발 도구와 hello 첫 번째 라스베리 Pi 3에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="9ea3b-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9ea3b-111">프로그래밍 언어의 기본 논리 hello hello C 이지만, Node.js 도구 hello 단원 toodiscover 장치에 사용 되 빌드 및 배포 예제 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9ea3b-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9ea3b-112">What you will learn</span></span>
<span data-ttu-id="9ea3b-113">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-113">In this article, you will learn:</span></span>

* <span data-ttu-id="9ea3b-114">어떻게 tooinstall Git 및 Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="9ea3b-115">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9ea3b-116">이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9ea3b-117">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9ea3b-118">어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="9ea3b-119">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9ea3b-120">[NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ea3b-121">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9ea3b-121">What you need</span></span>
<span data-ttu-id="9ea3b-122">toocomplete이 작업을이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="9ea3b-123">인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="9ea3b-124">macOS Yosemite(10.10) 이상을 실행하는 Mac.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="9ea3b-125">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="9ea3b-125">Install Git and Node.js</span></span>
<span data-ttu-id="9ea3b-126">Git tooinstall 및 Node.js를 사용 하 여 hello [Homebrew](http://brew.sh) 다음이 단계를 수행 하 여 관리 유틸리티를 패키지:</span><span class="sxs-lookup"><span data-stu-id="9ea3b-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="9ea3b-127">Homebrew를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-127">Install Homebrew.</span></span> <span data-ttu-id="9ea3b-128">Homebrew를 이미 설치한 경우 2 toostep를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="9ea3b-129">키를 눌러 `Cmd + Space` 입력 `Terminal` tooopen 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="9ea3b-130">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="9ea3b-131">Hello 다음 명령을 실행 하 여 Git 및 Node.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9ea3b-132">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="9ea3b-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="9ea3b-133">사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooyour Pi의 tooautomate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="9ea3b-134">사용 하 여 hello [장치-검색-cli](https://github.com/Azure/device-discovery-cli) IoT 장치에 대 한 tooretrieve 네트워크 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="9ea3b-135">설치 `gulp` 및 `device-discovery-cli` hello 다음 hello 터미널에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="9ea3b-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="9ea3b-136">MacOS에서 Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9ea3b-137">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="9ea3b-137">Install Visual Studio Code</span></span>
<span data-ttu-id="9ea3b-138">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="9ea3b-139">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9ea3b-140">이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9ea3b-141">요약</span><span class="sxs-lookup"><span data-stu-id="9ea3b-141">Summary</span></span>
<span data-ttu-id="9ea3b-142">필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="9ea3b-143">hello 다음 작업은 toocreate, 배포 및 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ea3b-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ea3b-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ea3b-144">Next steps</span></span>
[<span data-ttu-id="9ea3b-145">만들기 및 hello 깜박임 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="9ea3b-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

