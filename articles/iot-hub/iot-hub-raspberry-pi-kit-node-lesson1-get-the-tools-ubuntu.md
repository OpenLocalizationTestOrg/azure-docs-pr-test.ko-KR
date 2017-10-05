---
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 1: 도구 다운로드(Ubuntu) | Microsoft Docs"
description: "Ubuntu에 Pi의 첫 번째 샘플 응용 프로그램에 필요한 도구 및 소프트웨어를 다운로드하여 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 개발, IoT 소프트웨어, 사물 인터넷 소프트웨어, Ubuntu에 Git 설치, gulp 실행, Node Js Ubuntu 설치"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de583be0cdce058c83091f421376812e8013d76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="8f4ee-104">도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="8f4ee-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f4ee-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="8f4ee-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="8f4ee-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="8f4ee-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="8f4ee-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="8f4ee-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="8f4ee-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="8f4ee-108">What you will do</span></span>
<span data-ttu-id="8f4ee-109">Raspberry Pi 3의 첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="8f4ee-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f4ee-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="8f4ee-111">What you will learn</span></span>
<span data-ttu-id="8f4ee-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-112">In this article, you will learn:</span></span>

* <span data-ttu-id="8f4ee-113">Git 및 Node.js를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="8f4ee-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="8f4ee-115">이 문서에 대한 샘플 응용 프로그램은 Git에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="8f4ee-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="8f4ee-117">NPM을 사용하여 추가 Node.js 개발 도구를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="8f4ee-118">Node.js의 최소 필수 버전은 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="8f4ee-119">[NPM](https://www.npmjs.com)은 Node.js에 대한 패키지 관리자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="8f4ee-120">필요한 내용</span><span class="sxs-lookup"><span data-stu-id="8f4ee-120">What do you need</span></span>
<span data-ttu-id="8f4ee-121">이 작업을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="8f4ee-122">개발 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="8f4ee-123">Ubuntu 16.04 이상을 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="8f4ee-124">Git, Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="8f4ee-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="8f4ee-125">키보드 바로 가기 키 `Ctrl + Alt + T`를 사용하여 터미널을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="8f4ee-126">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="8f4ee-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="8f4ee-127">[gulp.js](http://gulpjs.com)를 사용하여 샘플 응용 프로그램이 Pi에 배포되는 것을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="8f4ee-128">또한 [device-discovery-cli](https://github.com/Azure/device-discovery-cli)를 사용하여 IoT 장치에 대한 네트워크 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="8f4ee-129">터미널에 다음 명령을 실행하여 `gulp` 및 `device-discovery-cli`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="8f4ee-130">Ubuntu에 Node.js 및 이러한 추가 개발 도구를 설치할 때 문제가 있는 경우 일반적인 문제의 솔루션에 관한 [문제 해결 가이드](iot-hub-raspberry-pi-kit-node-troubleshooting.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="8f4ee-131">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="8f4ee-131">Install Visual Studio Code</span></span>
<span data-ttu-id="8f4ee-132">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="8f4ee-133">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="8f4ee-134">이 자습서의 뒷부분에 나오는 샘플 코드를 편집하는 데 이 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="8f4ee-135">요약</span><span class="sxs-lookup"><span data-stu-id="8f4ee-135">Summary</span></span>
<span data-ttu-id="8f4ee-136">첫 번째 샘플 응용 프로그램에 필요한 개발 도구 및 소프트웨어를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="8f4ee-137">다음 작업은 Pi에서 샘플 응용 프로그램을 만들고, 배포하고, 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f4ee-137">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f4ee-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f4ee-138">Next steps</span></span>
[<span data-ttu-id="8f4ee-139">깜박임 샘플 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="8f4ee-139">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

