---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 1: 도구 다운로드(macOS) | Microsoft Docs"
description: "macOS에 Edison의 첫 번째 샘플 응용 프로그램에 필요한 도구 및 소프트웨어를 다운로드하여 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 개발 도구, IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, mac에 Git 설치, gulp 실행, Node Js mac 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="9eee6-104">도구 얻기(macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="9eee6-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9eee6-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="9eee6-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9eee6-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9eee6-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9eee6-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9eee6-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9eee6-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="9eee6-108">What you will do</span></span>
<span data-ttu-id="9eee6-109">Intel Edison의 첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="9eee6-110">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="9eee6-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9eee6-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9eee6-111">What you will learn</span></span>
<span data-ttu-id="9eee6-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-112">In this article, you will learn:</span></span>

* <span data-ttu-id="9eee6-113">Git 및 Node.js를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9eee6-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="9eee6-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9eee6-115">이 문서에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9eee6-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9eee6-117">NPM을 사용하여 추가 Node.js 개발 도구를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9eee6-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="9eee6-118">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9eee6-119">[NPM](https://www.npmjs.com)은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9eee6-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9eee6-120">What you need</span></span>
<span data-ttu-id="9eee6-121">이 작업을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="9eee6-122">개발 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="9eee6-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="9eee6-123">macOS Yosemite(10.10) 이상을 실행하는 Mac.</span><span class="sxs-lookup"><span data-stu-id="9eee6-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="9eee6-124">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="9eee6-124">Install Git and Node.js</span></span>
<span data-ttu-id="9eee6-125">Git 및 Node.js를 설치하려면 다음 단계를 따라 [Homebrew](http://brew.sh) 패키지 관리 유틸리티를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9eee6-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="9eee6-126">Homebrew를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-126">Install Homebrew.</span></span> <span data-ttu-id="9eee6-127">Homebrew를 이미 설치한 경우 2단계로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9eee6-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="9eee6-128">`Cmd + Space`를 누르고 `Terminal`을 입력하여 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="9eee6-129">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="9eee6-130">다음 명령을 실행하여 Git 및 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9eee6-131">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="9eee6-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="9eee6-132">[gulp.js](http://gulpjs.com)를 사용하여 샘플 응용 프로그램이 Edison에 배포되는 것을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="9eee6-133">터미널에 다음 명령을 실행하여 `gulp`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="9eee6-134">macOS에 Node.js 및 이러한 추가 개발 도구를 설치할 때 문제가 있는 경우 일반적인 문제의 솔루션에 관한 [문제 해결 가이드][troubleshooting]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eee6-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9eee6-135">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="9eee6-135">Install Visual Studio Code</span></span>
<span data-ttu-id="9eee6-136">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="9eee6-137">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9eee6-138">이 자습서의 뒷부분에 나오는 샘플 코드를 편집하는 데 이 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9eee6-139">요약</span><span class="sxs-lookup"><span data-stu-id="9eee6-139">Summary</span></span>
<span data-ttu-id="9eee6-140">첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="9eee6-141">다음 작업은 Edison에서 샘플 응용 프로그램을 만들고, 배포하고, 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9eee6-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eee6-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9eee6-142">Next steps</span></span>
<span data-ttu-id="9eee6-143">[깜박임 응용 프로그램 만들기 및 배포][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="9eee6-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
