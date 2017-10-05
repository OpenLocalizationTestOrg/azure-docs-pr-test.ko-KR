---
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 2: 도구 다운로드(Windows) | Microsoft Docs"
description: "Windows 7 이상 버전에 Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 클라우드 서비스, Azure CLI"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="a4f7d-104">Azure 도구 얻기(Windows 7 이상)</span><span class="sxs-lookup"><span data-stu-id="a4f7d-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4f7d-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="a4f7d-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="a4f7d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a4f7d-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="a4f7d-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a4f7d-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a4f7d-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="a4f7d-108">What you will do</span></span>
<span data-ttu-id="a4f7d-109">Python 및 Azure CLI(Azure 명령줄 인터페이스)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a4f7d-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a4f7d-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="a4f7d-111">What you will learn</span></span>
<span data-ttu-id="a4f7d-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a4f7d-113">Python을 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-113">How to install Python.</span></span>
* <span data-ttu-id="a4f7d-114">Azure CLI를 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a4f7d-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="a4f7d-115">What you need</span></span>
* <span data-ttu-id="a4f7d-116">인터넷에 연결된 Windows 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="a4f7d-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-117">An active Azure subscription.</span></span> <span data-ttu-id="a4f7d-118">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="a4f7d-119">Python 설치</span><span class="sxs-lookup"><span data-stu-id="a4f7d-119">Install Python</span></span>
<span data-ttu-id="a4f7d-120">Windows 컴퓨터에 [Python을 설치](https://www.python.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="a4f7d-121">Python 2.7, 3.4 또는 3.5를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="a4f7d-122">이 자습서는 Python 2.7을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="a4f7d-123">Python을 이미 설치한 경우 다음 섹션으로 이동하여 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="a4f7d-124">python.exe 및 pip.exe가 설치되어 있는 폴더의 경로를 시스템 `PATH` 환경 변수에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="a4f7d-125">기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="a4f7d-126">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="a4f7d-126">Install the Azure CLI</span></span>
<span data-ttu-id="a4f7d-127">Azure CLI는 Azure에 대한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="a4f7d-128">명령줄에서 리소스를 프로비전하고 관리하는 작업을 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-128">You work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="a4f7d-129">Azure CLI를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a4f7d-130">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="a4f7d-131">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="a4f7d-132">다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="a4f7d-133">성공적으로 설치되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-133">You see the following output if the installation is successful.</span></span>

![성공을 나타내는 출력](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="a4f7d-135">요약</span><span class="sxs-lookup"><span data-stu-id="a4f7d-135">Summary</span></span>
<span data-ttu-id="a4f7d-136">Azure CLI를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="a4f7d-137">다음 작업은 Azure CLI를 사용하여 Azure IoT Hub 및 장치 ID를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4f7d-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4f7d-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4f7d-138">Next steps</span></span>
[<span data-ttu-id="a4f7d-139">IoT Hub 만들기 및 Raspberry Pi 3 등록</span><span class="sxs-lookup"><span data-stu-id="a4f7d-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

