---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 단원 1: 도구 다운로드(macOS) | Microsoft Docs"
description: "macOS에 Pi의 첫 번째 샘플 응용 프로그램에 필요한 도구 및 소프트웨어를 다운로드하여 설치합니다."
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
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="62ee4-104">도구 얻기(macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="62ee4-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62ee4-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="62ee4-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="62ee4-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="62ee4-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="62ee4-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="62ee4-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="62ee4-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="62ee4-108">What you will do</span></span>
<span data-ttu-id="62ee4-109">Raspberry Pi 3의 첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="62ee4-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="62ee4-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="62ee4-111">기본 논리의 프로그래밍 언어는 C이며, Node.js 도구는 장치를 검색하고 샘플 응용 프로그램을 빌드하고 배포하는 단원에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="62ee4-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="62ee4-112">What you will learn</span></span>
<span data-ttu-id="62ee4-113">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-113">In this article, you will learn:</span></span>

* <span data-ttu-id="62ee4-114">Git 및 Node.js를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="62ee4-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="62ee4-115">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="62ee4-116">이 문서에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="62ee4-117">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="62ee4-118">NPM을 사용하여 추가 Node.js 개발 도구를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="62ee4-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="62ee4-119">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="62ee4-120">[NPM](https://www.npmjs.com)은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="62ee4-121">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="62ee4-121">What you need</span></span>
<span data-ttu-id="62ee4-122">이 작업을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="62ee4-123">개발 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="62ee4-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="62ee4-124">macOS Yosemite(10.10) 이상을 실행하는 Mac.</span><span class="sxs-lookup"><span data-stu-id="62ee4-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="62ee4-125">Git 및 Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="62ee4-125">Install Git and Node.js</span></span>
<span data-ttu-id="62ee4-126">Git 및 Node.js를 설치하려면 다음 단계를 따라 [Homebrew](http://brew.sh) 패키지 관리 유틸리티를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="62ee4-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="62ee4-127">Homebrew를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-127">Install Homebrew.</span></span> <span data-ttu-id="62ee4-128">Homebrew를 이미 설치한 경우 2단계로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="62ee4-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="62ee4-129">`Cmd + Space`를 누르고 `Terminal`을 입력하여 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="62ee4-130">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="62ee4-131">다음 명령을 실행하여 Git 및 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="62ee4-132">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="62ee4-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="62ee4-133">[gulp.js](http://gulpjs.com)를 사용하여 샘플 응용 프로그램이 Pi에 배포되는 것을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="62ee4-134">[device-discovery-cli](https://github.com/Azure/device-discovery-cli)를 사용하여 IoT 장치에 대한 네트워크 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="62ee4-135">터미널에 다음 명령을 실행하여 `gulp` 및 `device-discovery-cli`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="62ee4-136">macOS에 Node.js 및 이러한 추가 개발 도구를 설치할 때 문제가 있는 경우 일반적인 문제의 솔루션에 관한 [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62ee4-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="62ee4-137">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="62ee4-137">Install Visual Studio Code</span></span>
<span data-ttu-id="62ee4-138">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/osx)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="62ee4-139">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="62ee4-140">이 자습서의 뒷부분에 나오는 샘플 코드를 편집하는 데 이 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="62ee4-141">요약</span><span class="sxs-lookup"><span data-stu-id="62ee4-141">Summary</span></span>
<span data-ttu-id="62ee4-142">첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="62ee4-143">다음 작업은 Pi에서 샘플 응용 프로그램을 만들고, 배포하고, 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62ee4-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62ee4-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62ee4-144">Next steps</span></span>
[<span data-ttu-id="62ee4-145">깜박임 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="62ee4-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

