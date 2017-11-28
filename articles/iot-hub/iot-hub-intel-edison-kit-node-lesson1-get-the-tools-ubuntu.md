---
title: "Intel Edison (노드) tooAzure IoT-1과 연결: 도구 (Ubuntu) 가져오기 | Microsoft Docs"
description: "다운로드 및 ubuntu hello 필요한 도구와 hello 첫 번째 Edison에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 개발 도구, IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="daa09-104">Hello 도구 (Ubuntu 16.04) 가져오기</span><span class="sxs-lookup"><span data-stu-id="daa09-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="daa09-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="daa09-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="daa09-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="daa09-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="daa09-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="daa09-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="daa09-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="daa09-108">What you will do</span></span>
<span data-ttu-id="daa09-109">Hello 개발 도구와 hello 첫 번째 Intel Edison에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="daa09-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="daa09-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="daa09-111">What you will learn</span></span>
<span data-ttu-id="daa09-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-112">In this article, you will learn:</span></span>

* <span data-ttu-id="daa09-113">어떻게 tooinstall Git 및 Node.js</span><span class="sxs-lookup"><span data-stu-id="daa09-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="daa09-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="daa09-115">이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="daa09-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="daa09-117">어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="daa09-118">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="daa09-119">[NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="daa09-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="daa09-120">What you need</span></span>
<span data-ttu-id="daa09-121">toocomplete이 작업을이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="daa09-122">인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="daa09-123">Ubuntu 16.04 이상을 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="daa09-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="daa09-124">Git, Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="daa09-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="daa09-125">사용 하 여 hello에 대 한 바로 가기 키 `Ctrl + Alt + T` tooopen 다음 터미널 하 고 실행할 hello 명령:</span><span class="sxs-lookup"><span data-stu-id="daa09-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="daa09-126">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="daa09-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="daa09-127">사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooEdison의 tooautomate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="daa09-128">설치 `gulp` hello 다음 hello 터미널에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="daa09-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="daa09-129">Ubuntu Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="daa09-130">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="daa09-130">Install Visual Studio Code</span></span>
<span data-ttu-id="daa09-131">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="daa09-132">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="daa09-133">이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="daa09-134">요약</span><span class="sxs-lookup"><span data-stu-id="daa09-134">Summary</span></span>
<span data-ttu-id="daa09-135">필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="daa09-136">hello 다음 작업은 toocreate, 배포 및 Edison에 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa09-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa09-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="daa09-137">Next steps</span></span>
<span data-ttu-id="daa09-138">[만들기 및 hello 깜박임 샘플 응용 프로그램 배포][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="daa09-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
