---
title: "연결 라스베리 Pi (노드) tooAzure IoT-1 단원: 도구 (Ubuntu) 가져오기 | Microsoft Docs"
description: "다운로드 및 ubuntu hello 필요한 도구와 hello 첫 번째 Pi에 대 한 샘플 응용 프로그램에 대 한 소프트웨어를 설치 합니다."
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
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="02020-104">Hello 도구 (Ubuntu 16.04) 가져오기</span><span class="sxs-lookup"><span data-stu-id="02020-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02020-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="02020-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="02020-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="02020-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="02020-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="02020-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="02020-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="02020-108">What you will do</span></span>
<span data-ttu-id="02020-109">Hello 개발 도구와 hello 첫 번째 라스베리 Pi 3에 대 한 샘플 응용 프로그램에 대 한 hello 소프트웨어를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="02020-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="02020-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="02020-111">What you will learn</span></span>
<span data-ttu-id="02020-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02020-112">In this article, you will learn:</span></span>

* <span data-ttu-id="02020-113">어떻게 tooinstall Git 및 Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="02020-114">[Git](https://git-scm.com)는 오픈 소스 분산 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="02020-115">이 문서에 대 한 hello 샘플 응용 프로그램은 Git에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02020-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="02020-116">[Node.js](https://nodejs.org/en/)는 풍부한 패키지 에코 시스템을 사용하는 JavaScript 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="02020-117">어떻게 toouse NPM tooinstall 추가 Node.js 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="02020-118">hello 필요한 최소 버전의 Node.js 4.5 LTS입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="02020-119">[NPM](https://www.npmjs.com) Node.js에 대 한 패키지 관리자 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="02020-120">필요한 내용</span><span class="sxs-lookup"><span data-stu-id="02020-120">What do you need</span></span>
<span data-ttu-id="02020-121">toocomplete이 작업을이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="02020-122">인터넷 연결 toodownload hello 개발 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="02020-123">Ubuntu 16.04 이상을 실행하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="02020-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="02020-124">Git, Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="02020-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="02020-125">사용 하 여 hello에 대 한 바로 가기 키 `Ctrl + Alt + T` tooopen 다음 터미널 하 고 실행할 hello 명령:</span><span class="sxs-lookup"><span data-stu-id="02020-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="02020-126">추가 Node.js 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="02020-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="02020-127">사용 하면 [gulp.js](http://gulpjs.com) hello 샘플 응용 프로그램 tooPi의 tooautomate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="02020-128">Hello 사용할 수도 [장치-검색-cli](https://github.com/Azure/device-discovery-cli) IoT 장치에 대 한 tooretrieve 네트워크 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="02020-129">설치 `gulp` 및 `device-discovery-cli` hello 다음 hello 터미널에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="02020-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="02020-130">Ubuntu Node.js 및 이러한 추가 개발 도구를 설치 하는 문제가 발생 하는 경우 참조 hello [문제 해결 가이드](iot-hub-raspberry-pi-kit-node-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="02020-131">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="02020-131">Install Visual Studio Code</span></span>
<span data-ttu-id="02020-132">Visual Studio Code를 [다운로드](https://code.visualstudio.com/docs/setup/linux)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="02020-133">Visual Studio Code는 Windows, Linux 및 macOS를 위한 간단하지만 강력한 소스 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="02020-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="02020-134">이 편집기를 사용 하 여 hello 자습서 tooedit hello 샘플 코드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="02020-135">요약</span><span class="sxs-lookup"><span data-stu-id="02020-135">Summary</span></span>
<span data-ttu-id="02020-136">필요한 hello 개발 도구 및 hello 첫 번째 샘플 응용 프로그램에 대 한 소프트웨어를 설치 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="02020-137">hello 다음 작업은 toocreate, 배포 및 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02020-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02020-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02020-138">Next steps</span></span>
[<span data-ttu-id="02020-139">만들기 및 hello 깜박임 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="02020-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

