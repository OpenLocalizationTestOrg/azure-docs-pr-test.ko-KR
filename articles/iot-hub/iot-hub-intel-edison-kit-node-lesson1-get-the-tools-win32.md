---
title: "Intel Edison (노드) tooAzure IoT-1과 연결: 도구 (Windows) 가져오기 | Microsoft Docs"
description: "다운로드 하 고 Windows 7 이상 버전에서 hello 필요한 도구와 hello 첫 번째 Edison에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 개발 도구, IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Windows에 Git 설치, gulp 실행, Node Js Windows 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="bc473-104">Hello 도구 (Windows 7 이상) 가져오기</span><span class="sxs-lookup"><span data-stu-id="bc473-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="bc473-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="bc473-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="bc473-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="bc473-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="bc473-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="bc473-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bc473-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="bc473-108">What you will do</span></span>
<span data-ttu-id="bc473-109">Hello 개발 도구와 hello 첫 번째 Intel Edison에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="bc473-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bc473-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="bc473-111">What you will learn</span></span>
<span data-ttu-id="bc473-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-112">In this article, you will learn:</span></span>

* <span data-ttu-id="bc473-113">어떻게 tooinstall Git 및 Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="bc473-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="bc473-115">이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="bc473-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="bc473-117">어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="bc473-118">Node.js의 hello 최소 버전 요구 사항을 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="bc473-119">[NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bc473-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="bc473-120">What you need</span></span>

<span data-ttu-id="bc473-121">toocomplete이 작업을이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="bc473-122">인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="bc473-123">Windows를 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="bc473-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bc473-124">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="bc473-124">Install Git and Node.js</span></span>

<span data-ttu-id="bc473-125">Hello toodownload 아래에 링크를 클릭 하 고 Git 및 Windows 용 LTS Node.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="bc473-126">Windows용 Git 얻기</span><span class="sxs-lookup"><span data-stu-id="bc473-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="bc473-127">Windows용 Node.js LTS 얻기</span><span class="sxs-lookup"><span data-stu-id="bc473-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="bc473-128">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="bc473-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="bc473-129">사용 하 여 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooEdison의 tooautomate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="bc473-130">관리자로 명령 프롬프트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="bc473-131">설치 `gulp` hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="bc473-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="bc473-132">컴퓨터에 Node.js 및 다음과 같은 추가 Node.js 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="bc473-133">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="bc473-133">Install Visual Studio Code</span></span>

<span data-ttu-id="bc473-134">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/windows)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="bc473-135">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bc473-136">이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="bc473-137">요약</span><span class="sxs-lookup"><span data-stu-id="bc473-137">Summary</span></span>

<span data-ttu-id="bc473-138">필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="bc473-139">hello 다음 작업은 toocreate, 배포 및 Edison에 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc473-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc473-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc473-140">Next steps</span></span>

<span data-ttu-id="bc473-141">[만들기 및 hello 깜박임 응용 프로그램 배포][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="bc473-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
