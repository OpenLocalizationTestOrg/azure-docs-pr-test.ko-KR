---
title: "Azure IoT에 Arduino 연결 - 단원 2: Azure 도구(Windows) | Microsoft Docs"
description: "Windows 7 이상 버전에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 클라우드 서비스, arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1f121d9f22f8a7c8582df4d2e62191cec364da46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="22795-104">Azure 도구 얻기(Windows 7 이상)</span><span class="sxs-lookup"><span data-stu-id="22795-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="22795-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="22795-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="22795-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="22795-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="22795-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="22795-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="22795-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="22795-108">What you will do</span></span>

<span data-ttu-id="22795-109">Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="22795-110">문제가 발생하면 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)에서 Adafruit Feather M0 WiFi Arduino 보드에 대한 솔루션을 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="22795-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="22795-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="22795-111">What you will learn</span></span>
<span data-ttu-id="22795-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22795-112">In this article, you will learn:</span></span>
* <span data-ttu-id="22795-113">Python을 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="22795-113">How to install Python.</span></span>
* <span data-ttu-id="22795-114">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="22795-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="22795-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="22795-115">What you need</span></span>
* <span data-ttu-id="22795-116">인터넷에 연결된 Windows 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="22795-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="22795-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="22795-117">An active Azure subscription.</span></span> <span data-ttu-id="22795-118">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22795-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="22795-119">Python 설치</span><span class="sxs-lookup"><span data-stu-id="22795-119">Install Python</span></span>
<span data-ttu-id="22795-120">Windows 컴퓨터에 [Python을 설치](https://www.python.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="22795-121">Python 2.7, 3.4 또는 3.5를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22795-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="22795-122">이 자습서는 Python 2.7을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="22795-123">Python을 이미 설치한 경우 다음 섹션으로 이동하여 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="22795-124">python.exe 및 pip.exe가 설치되어 있는 폴더의 경로를 시스템 `PATH` 환경 변수에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="22795-125">기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22795-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="22795-126">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="22795-126">Install the Azure CLI</span></span>
<span data-ttu-id="22795-127">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="22795-128">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22795-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="22795-129">Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="22795-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="22795-130">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22795-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="22795-131">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="22795-132">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22795-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="22795-133">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22795-133">You see the following output if the installation is successful.</span></span>

![성공을 나타내는 출력][output]

## <a name="summary"></a><span data-ttu-id="22795-135">요약</span><span class="sxs-lookup"><span data-stu-id="22795-135">Summary</span></span>
<span data-ttu-id="22795-136">Azure CLI를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="22795-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="22795-137">다음 작업은 Azure CLI를 사용하여 Azure IoT Hub 및 장치 ID를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22795-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22795-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22795-138">Next steps</span></span>
<span data-ttu-id="22795-139">[IoT Hub 만들기 및 Arduino 보드 등록][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="22795-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md