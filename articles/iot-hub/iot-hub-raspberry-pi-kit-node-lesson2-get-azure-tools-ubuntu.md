---
title: "연결 라스베리 Pi (노드) tooAzure IoT-2 단원: 도구 (Ubuntu) 가져오기 | Microsoft Docs"
description: "Python을 설치 하 고 Azure CLI (명령줄 인터페이스 Azure) ubuntu hello 키를 누릅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 클라우드 서비스, Azure CLI"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0adf91bef41f502e1333fdcc75cfb2fe912364c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="55717-104">Azure 도구 얻기(Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="55717-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55717-105">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="55717-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="55717-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="55717-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="55717-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="55717-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="55717-108">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="55717-108">What you will do</span></span>
<span data-ttu-id="55717-109">Hello Azure CLI (명령줄 인터페이스 Azure)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="55717-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55717-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="55717-111">What you will learn</span></span>
<span data-ttu-id="55717-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55717-112">In this article, you will learn:</span></span>
* <span data-ttu-id="55717-113">어떻게 tooinstall hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="55717-114">어떻게 tooadd hello Azure CLI는 IoT 하위 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="55717-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55717-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="55717-115">What you need</span></span>
* <span data-ttu-id="55717-116">인터넷에 연결된 Ubuntu 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="55717-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="55717-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="55717-117">An active Azure subscription.</span></span> <span data-ttu-id="55717-118">계정이 없는 경우 몇 분 만에 [무료 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55717-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="55717-119">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-119">Install hello Azure CLI</span></span>
<span data-ttu-id="55717-120">hello Azure CLI toowork 명령줄 tooprovision 프로그램에서 직접 사용 하면 Azure에 대 한 다중 플랫폼 명령줄 환경을 제공 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="55717-121">tooinstall 최신 Azure CLI hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="55717-122">Hello 명령을 터미널 창에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="55717-123">5 분 tooinstall hello Azure CLI 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55717-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="55717-124">Hello 다음 명령을 실행 하 여 hello 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="55717-125">Hello 다음 hello 설치에 성공한 경우 출력 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55717-125">You should see hello following output if hello installation is successful.</span></span>

![성공을 나타내는 출력](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="55717-127">요약</span><span class="sxs-lookup"><span data-stu-id="55717-127">Summary</span></span>
<span data-ttu-id="55717-128">Hello Azure CLI를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="55717-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="55717-129">다음 작업은 toocreate Azure IoT hub 및 사용 하 여 장치 id hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="55717-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55717-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55717-130">Next steps</span></span>
[<span data-ttu-id="55717-131">IoT Hub 만들기 및 Raspberry Pi 3 등록</span><span class="sxs-lookup"><span data-stu-id="55717-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

