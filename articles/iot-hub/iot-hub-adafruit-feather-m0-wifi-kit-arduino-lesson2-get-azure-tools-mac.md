---
title: "연결 Arduino tooAzure IoT-2 단원: Azure tools (macOS) | Microsoft Docs"
description: "macOS에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 클라우드 서비스, arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0ec4131e54af5475cd0b4240480c3fda497e14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="74ed8-104">Azure 도구 얻기(macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="74ed8-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="74ed8-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="74ed8-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="74ed8-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="74ed8-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="74ed8-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="74ed8-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="74ed8-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="74ed8-108">What you will do</span></span>

<span data-ttu-id="74ed8-109">Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="74ed8-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit 페더 M0 WiFi Arduino 보드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="74ed8-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="74ed8-111">What you will learn</span></span>
<span data-ttu-id="74ed8-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-112">In this article, you will learn:</span></span>
* <span data-ttu-id="74ed8-113">어떻게 tooinstall Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="74ed8-114">어떻게 tooadd hello Azure CLI는 IoT 하위 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="74ed8-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="74ed8-115">What you need</span></span>
* <span data-ttu-id="74ed8-116">인터넷에 연결된 Mac.</span><span class="sxs-lookup"><span data-stu-id="74ed8-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="74ed8-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="74ed8-117">An active Azure subscription.</span></span> <span data-ttu-id="74ed8-118">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="74ed8-119">Python 설치</span><span class="sxs-lookup"><span data-stu-id="74ed8-119">Install Python</span></span>
<span data-ttu-id="74ed8-120">MacOS는 hello 초기 Python 2.7 함께 제공, 되지만 Homebrew 통해 Python을 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="74ed8-121">[macOS에서 Python 설치](http://docs.python-guide.org/en/latest/starting/install/osx/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74ed8-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="74ed8-122">Python 및 pip hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="74ed8-123">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-123">Install hello Azure CLI</span></span>
<span data-ttu-id="74ed8-124">hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="74ed8-125">명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-125">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="74ed8-126">tooinstall 최신 Azure CLI hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="74ed8-127">Hello 명령을 터미널 창에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="74ed8-128">5 분 tooinstall hello Azure CLI 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="74ed8-129">Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="74ed8-130">Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-130">You should see hello following output if hello installation is successful.</span></span>

![성공을 나타내는 출력][output]

## <a name="summary"></a><span data-ttu-id="74ed8-132">요약</span><span class="sxs-lookup"><span data-stu-id="74ed8-132">Summary</span></span>
<span data-ttu-id="74ed8-133">Hello Azure CLI를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="74ed8-134">다음 작업은 toocreate Azure IoT hub 및 장치 id를 사용 하 여 hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ed8-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74ed8-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74ed8-135">Next steps</span></span>
<span data-ttu-id="74ed8-136">[IoT Hub 만들기 및 Arduino 보드 등록][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="74ed8-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md