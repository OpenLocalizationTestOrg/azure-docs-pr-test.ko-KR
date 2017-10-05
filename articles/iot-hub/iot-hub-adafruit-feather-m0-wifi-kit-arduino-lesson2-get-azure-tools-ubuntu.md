---
title: "Azure IoT에 Arduino 연결 - 단원 2: Azure 도구(Ubuntu) | Microsoft Docs"
description: "Ubuntu에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure cli, IoT 클라우드 서비스, Arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="9c3d2-104">Azure 도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="9c3d2-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="9c3d2-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="9c3d2-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9c3d2-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9c3d2-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9c3d2-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9c3d2-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9c3d2-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="9c3d2-108">What you will do</span></span>

<span data-ttu-id="9c3d2-109">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="9c3d2-110">문제가 발생하면 Adafruit Feather M0 WiFi Arduino 보드에 대한 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)에서 솔루션을 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9c3d2-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9c3d2-111">What you will learn</span></span>
<span data-ttu-id="9c3d2-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-112">In this article, you will learn:</span></span>
* <span data-ttu-id="9c3d2-113">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="9c3d2-114">Azure CLI의 IoT 하위 그룹을 추가하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c3d2-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9c3d2-115">What you need</span></span>
* <span data-ttu-id="9c3d2-116">인터넷에 연결된 Ubuntu 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="9c3d2-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-117">An active Azure subscription.</span></span> <span data-ttu-id="9c3d2-118">계정이 없는 경우 몇 분 만에 [무료 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="9c3d2-119">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="9c3d2-119">Install the Azure CLI</span></span>
<span data-ttu-id="9c3d2-120">Azure CLI는 명령줄에서 직접 작업하여 리소스를 프로비전하고 관리할 수 있도록 하는 Azure를 위한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="9c3d2-121">최신 Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="9c3d2-122">터미널 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="9c3d2-123">Azure CLI를 설치하는 데 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="9c3d2-124">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="9c3d2-125">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-125">You should see the following output if the installation is successful.</span></span>

![성공을 나타내는 출력][output]

## <a name="summary"></a><span data-ttu-id="9c3d2-127">요약</span><span class="sxs-lookup"><span data-stu-id="9c3d2-127">Summary</span></span>
<span data-ttu-id="9c3d2-128">Azure CLI를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="9c3d2-129">다음 작업은 Azure CLI를 사용하여 Azure IoT Hub 및 장치 ID를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c3d2-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c3d2-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c3d2-130">Next steps</span></span>
<span data-ttu-id="9c3d2-131">[IoT Hub 만들기 및 Arduino 보드 등록][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="9c3d2-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md