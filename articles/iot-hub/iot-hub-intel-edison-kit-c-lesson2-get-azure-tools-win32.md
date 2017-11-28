---
title: "Connect Intel Edison (C) tooAzure IoT-2 단원: Azure tools (Windows) | Microsoft Docs"
description: "Windows 7 이상 버전에서 Python 및 hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure cli, IoT 클라우드 서비스, Arduino 클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 46f964541c00674500e4f6a072a9a2547b5b24d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="a9913-104">Azure 도구 얻기(Windows 7 이상)</span><span class="sxs-lookup"><span data-stu-id="a9913-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a9913-105">[Windows 7 이상][windows]</span><span class="sxs-lookup"><span data-stu-id="a9913-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="a9913-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a9913-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a9913-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a9913-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a9913-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="a9913-108">What you will do</span></span>
<span data-ttu-id="a9913-109">Python을 설치 하 고 hello Azure CLI (명령줄 인터페이스 Azure).</span><span class="sxs-lookup"><span data-stu-id="a9913-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a9913-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a9913-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="a9913-111">What you will learn</span></span>
<span data-ttu-id="a9913-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a9913-113">어떻게 tooinstall Python 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-113">How tooinstall Python.</span></span>
* <span data-ttu-id="a9913-114">어떻게 tooinstall hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a9913-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="a9913-115">What you need</span></span>
* <span data-ttu-id="a9913-116">인터넷에 연결된 Windows 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="a9913-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="a9913-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a9913-117">An active Azure subscription.</span></span> <span data-ttu-id="a9913-118">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="a9913-119">Python 설치</span><span class="sxs-lookup"><span data-stu-id="a9913-119">Install Python</span></span>
<span data-ttu-id="a9913-120">Windows 컴퓨터에 [Python을 설치](https://www.python.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="a9913-121">Python 2.7, 3.4 또는 3.5를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="a9913-122">이 자습서는 Python 2.7을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="a9913-123">Python을 이미 설치한 경우 다음 섹션 toohello 이동한 다음 hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="a9913-124">또한 python.exe 및 pip.exe는 설치 된 toohello 시스템 hello 폴더의 tooadd hello 경로 해야 `PATH` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="a9913-125">기본적으로 python.exe는 `C:\Python27`에, pip.exe는 `C:\Python27\Scripts`에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="a9913-126">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-126">Install hello Azure CLI</span></span>
<span data-ttu-id="a9913-127">hello Azure CLI Azure에 대 한 다중 플랫폼 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="a9913-128">명령줄 tooprovision에서 직접 작업 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="a9913-129">tooinstall hello Azure CLI 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="a9913-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a9913-130">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="a9913-131">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="a9913-132">Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="a9913-133">Hello 다음 hello 설치에 성공한 경우 출력 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-133">You see hello following output if hello installation is successful.</span></span>

![성공을 나타내는 출력](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="a9913-135">요약</span><span class="sxs-lookup"><span data-stu-id="a9913-135">Summary</span></span>
<span data-ttu-id="a9913-136">Hello Azure CLI를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="a9913-137">다음 번 toocreate Azure IoT hub 및 장치 id hello Azure CLI를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9913-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9913-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9913-138">Next steps</span></span>
<span data-ttu-id="a9913-139">[IoT Hub 만들기 및 Intel Edison 등록][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="a9913-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
