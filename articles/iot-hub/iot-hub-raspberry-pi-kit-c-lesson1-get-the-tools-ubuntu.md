---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 단원 1: 도구 다운로드(Ubuntu) | Microsoft Docs"
description: "Ubuntu에 Pi의 첫 번째 샘플 응용 프로그램에 필요한 도구 및 소프트웨어를 다운로드하여 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="35c3a-104">도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="35c3a-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35c3a-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="35c3a-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="35c3a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="35c3a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="35c3a-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="35c3a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="35c3a-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="35c3a-108">What you will do</span></span>
<span data-ttu-id="35c3a-109">Raspberry Pi 3의 첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="35c3a-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="35c3a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="35c3a-111">기본 논리의 프로그래밍 언어는 C이며, Node.js 도구는 장치를 검색하고 샘플 응용 프로그램을 빌드하고 배포하는 단원에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="35c3a-112">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="35c3a-112">What you will learn</span></span>
<span data-ttu-id="35c3a-113">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-113">In this article, you will learn:</span></span>

* <span data-ttu-id="35c3a-114">Git 및 Node.js를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="35c3a-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="35c3a-115">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="35c3a-116">이 문서에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="35c3a-117">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="35c3a-118">NPM을 사용하여 추가 Node.js 개발 도구를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="35c3a-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="35c3a-119">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="35c3a-120">[NPM](https://www.npmjs.com)은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="35c3a-121">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="35c3a-121">What you need</span></span>
<span data-ttu-id="35c3a-122">이 작업을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="35c3a-123">개발 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="35c3a-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="35c3a-124">Ubuntu 16.04 이상을 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="35c3a-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="35c3a-125">Git, Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="35c3a-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="35c3a-126">키보드 바로 가기 키 `Ctrl + Alt + T`를 사용하여 터미널을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="35c3a-127">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="35c3a-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="35c3a-128">[gulp.js](http://gulpjs.com)를 사용하여 샘플 응용 프로그램이 Pi에 배포되는 것을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="35c3a-129">[device-discovery-cli](https://github.com/Azure/device-discovery-cli)를 사용하여 IoT 장치에 대한 네트워크 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="35c3a-130">터미널에 다음 명령을 실행하여 `gulp` 및 `device-discovery-cli`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="35c3a-131">Ubuntu에 Node.js 및 이러한 추가 개발 도구를 설치할 때 문제가 있는 경우 일반적인 문제의 솔루션에 관한 [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c3a-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="35c3a-132">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="35c3a-132">Install Visual Studio Code</span></span>
<span data-ttu-id="35c3a-133">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="35c3a-134">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="35c3a-135">이 자습서의 뒷부분에 나오는 샘플 코드를 편집하는 데 이 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="35c3a-136">요약</span><span class="sxs-lookup"><span data-stu-id="35c3a-136">Summary</span></span>
<span data-ttu-id="35c3a-137">첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="35c3a-138">다음 작업은 Pi에서 샘플 응용 프로그램을 만들고, 배포하고, 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35c3a-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35c3a-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35c3a-139">Next steps</span></span>
[<span data-ttu-id="35c3a-140">깜박임 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="35c3a-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

