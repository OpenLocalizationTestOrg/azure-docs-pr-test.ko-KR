---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 2: Azure 도구(Ubuntu) | Microsoft Docs"
description: "Ubuntu에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure cli, IoT 클라우드 서비스, Arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 65248e14d0ea05a44efe76e66e1ef519285982b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="8c12c-104">Azure 도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="8c12c-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8c12c-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="8c12c-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="8c12c-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="8c12c-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="8c12c-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="8c12c-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8c12c-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="8c12c-108">What you will do</span></span>
<span data-ttu-id="8c12c-109">Azure 명령줄 인터페이스(Azure CLI) 설치.</span><span class="sxs-lookup"><span data-stu-id="8c12c-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="8c12c-110">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="8c12c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8c12c-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="8c12c-111">What you will learn</span></span>
<span data-ttu-id="8c12c-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="8c12c-113">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="8c12c-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="8c12c-114">Azure CLI의 IoT 하위 그룹을 추가하는 방법.</span><span class="sxs-lookup"><span data-stu-id="8c12c-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8c12c-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="8c12c-115">What you need</span></span>
* <span data-ttu-id="8c12c-116">인터넷에 연결된 Ubuntu 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8c12c-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="8c12c-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="8c12c-117">An active Azure subscription.</span></span> <span data-ttu-id="8c12c-118">계정이 없는 경우 몇 분 만에 [무료 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="8c12c-119">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="8c12c-119">Install the Azure CLI</span></span>
<span data-ttu-id="8c12c-120">Azure CLI는 명령줄에서 직접 작업하여 리소스를 프로비전하고 관리할 수 있도록 하는 Azure를 위한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="8c12c-121">최신 Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8c12c-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="8c12c-122">터미널 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="8c12c-123">Azure CLI를 설치하는 데 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="8c12c-124">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="8c12c-125">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-125">You should see the following output if the installation is successful.</span></span>

![성공을 나타내는 출력](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="8c12c-127">요약</span><span class="sxs-lookup"><span data-stu-id="8c12c-127">Summary</span></span>
<span data-ttu-id="8c12c-128">Azure CLI를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="8c12c-129">다음 작업은 Azure CLI를 사용하여 Azure IoT Hub 및 장치 ID를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c12c-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c12c-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c12c-130">Next steps</span></span>
<span data-ttu-id="8c12c-131">[IoT Hub 만들기 및 Intel Edison 등록][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="8c12c-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
