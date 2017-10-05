---
title: "Azure IoT에 Intel Edison(C) 연결 - 단원 2: Azure 도구 다운로드(macOS) | Microsoft Docs"
description: "macOS에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 클라우드 서비스, arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="937fd-104">Azure 도구 얻기(macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="937fd-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="937fd-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="937fd-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="937fd-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="937fd-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="937fd-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="937fd-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="937fd-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="937fd-108">What you will do</span></span>
<span data-ttu-id="937fd-109">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="937fd-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="937fd-110">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="937fd-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="937fd-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="937fd-111">What you will learn</span></span>
<span data-ttu-id="937fd-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-112">In this article, you will learn:</span></span>
* <span data-ttu-id="937fd-113">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="937fd-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="937fd-114">Azure CLI의 IoT 하위 그룹을 추가하는 방법.</span><span class="sxs-lookup"><span data-stu-id="937fd-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="937fd-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="937fd-115">What you need</span></span>
* <span data-ttu-id="937fd-116">인터넷에 연결된 Mac.</span><span class="sxs-lookup"><span data-stu-id="937fd-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="937fd-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="937fd-117">An active Azure subscription.</span></span> <span data-ttu-id="937fd-118">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="937fd-119">Python 설치</span><span class="sxs-lookup"><span data-stu-id="937fd-119">Install Python</span></span>
<span data-ttu-id="937fd-120">macOS는 기본적으로 Python 2.7이 탑재되어 있지만 Homebrew를 통해 Python을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="937fd-121">[macOS에서 Python 설치](http://docs.python-guide.org/en/latest/starting/install/osx/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="937fd-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="937fd-122">다음 명령을 실행하여 Python 및 pip를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="937fd-123">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="937fd-123">Install the Azure CLI</span></span>
<span data-ttu-id="937fd-124">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="937fd-125">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="937fd-126">최신 Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="937fd-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="937fd-127">터미널 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="937fd-128">Azure CLI를 설치하는 데 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="937fd-129">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="937fd-130">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-130">You should see the following output if the installation is successful.</span></span>

![성공을 나타내는 출력](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="937fd-132">요약</span><span class="sxs-lookup"><span data-stu-id="937fd-132">Summary</span></span>
<span data-ttu-id="937fd-133">Azure CLI를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="937fd-134">다음 작업은 Azure CLI를 사용하여 Azure IoT Hub 및 장치 ID를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="937fd-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="937fd-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="937fd-135">Next steps</span></span>
<span data-ttu-id="937fd-136">[IoT Hub 만들기 및 Intel Edison 등록][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="937fd-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
