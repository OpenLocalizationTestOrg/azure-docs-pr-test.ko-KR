---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 시작 | Microsoft Docs"
description: "IoT 게이트웨이 시작 키트 시작, Azure IoT 허브를 만들고, 게이트웨이 toohello IoT 허브 연결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 게이트웨이 시작, azure iot 허브 hello iot toolkit, 사물 인터넷"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="c7640-104">시뮬레이트된 장치에서 IoT Gateway 시작 키트 시작</span><span class="sxs-lookup"><span data-stu-id="c7640-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7640-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="c7640-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="c7640-106">시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="c7640-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="c7640-107">이 자습서에서는 학습 hello의 기본적인 사용 하 여 시작 [IoT 게이트웨이 시작 키트](https://aka.ms/gateway-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="c7640-108">Wind River Linux를 실행하는 Intel NUC로 작업하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="c7640-109">Tooseamleesly Azure IoT 허브를 사용 하 여 장치 toohello 클라우드를 연결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="c7640-110">**아직 키트가 없나요?:** [여기](https://aka.ms/gateway-kit)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="c7640-111">단원 1: NUC 구성</span><span class="sxs-lookup"><span data-stu-id="c7640-111">Lesson 1: Configure your NUC</span></span>
![단원 1 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="c7640-113">Hello Azure IoT 게이트웨이로 키트에서에서 Intel NUC (다음 단위의 컴퓨팅)를 설정 하면이 단원에서는 NUC에 hello Azure IoT 가장자리 패키지를 설치 하 고 샘플 앱 tooverify hello 게이트웨이 기능을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="c7640-114">*예상 시간 toocomplete: 15 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="c7640-115">너무 이동[IoT 게이트웨이로 Intel NUC 설정](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="c7640-116">단원 2: IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c7640-116">Lesson 2: Create your IoT Hub</span></span>
![단원 2 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="c7640-118">이 단원에서는 호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="c7640-119">그런 다음 무료 Azure 계정, Azure IoT hub를 프로 비전 만들고 hello IoT 허브에서 첫 번째 장치를 만들고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="c7640-120">이 단원을 시작하기 전에 1단원을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="c7640-121">Hello 도구 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7640-121">Get hello tools</span></span>
<span data-ttu-id="c7640-122">호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="c7640-123">*예상 시간 toocomplete: 20 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="c7640-124">너무 이동[hello 도구 가져오기](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="c7640-125">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c7640-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="c7640-126">리소스 그룹을 만들고 첫 번째 Azure IoT 허브를 프로 비전 hello Azure CLI를 사용 하 여 첫 번째 장치 toohello IoT 허브를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="c7640-127">*예상 시간 toocomplete: 10 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="c7640-128">너무 이동[IoT hub를 만들고 장치를 등록 합니다.](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="c7640-129">3 단원: hello 시뮬레이션 된 장치에서 메시지를 수신 및 IoT 허브에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="c7640-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="c7640-130">이 단원에서는 스크립트 tooautomate hello 구성 및 시뮬레이션 된 장치 앱의 실행 게이트웨이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="c7640-131">hello 시뮬레이션 된 장치 앱 샘플 온도 데이터를 생성 하 고 tooan IoT 허브 모듈 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="c7640-132">안녕 IoT 허브 모듈 패키지 hello 데이터 수신 및 Azure IoT 가장자리 tooyour IoT hub 제공 hello 게이트웨이 프레임 워크를 통해 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![단원 3 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="c7640-134">시뮬레이트된 장치 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="c7640-134">Configure and run a simulated device</span></span>
<span data-ttu-id="c7640-135">Hello 샘플 코드를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-135">Prepare hello sample codes.</span></span> <span data-ttu-id="c7640-136">다음 구성 하 고 hello 시뮬레이션 된 장치에 대 한 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="c7640-137">*예상 시간 toocomplete: 15 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="c7640-138">너무 이동[실행 시뮬레이션된 된 장치 및 구성](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="c7640-139">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="c7640-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="c7640-140">IoT 허브에서 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="c7640-141">*예상 시간 toocomplete: 15 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="c7640-142">너무 이동[IoT 허브에서 메시지 읽기](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="c7640-143">4 단원: tooAzure 테이블 저장소 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="c7640-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="c7640-144">IoT hub에서 들어오는 메시지를 가져오고 tooAzure 테이블 저장소에 기록 하는 Azure 함수 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![단원 4 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="c7640-146">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c7640-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="c7640-147">Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="c7640-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="c7640-148">*예상 시간 toocomplete: 10 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="c7640-149">너무 이동[Azure 함수 앱 및 Azure 저장소 계정 만들기](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="c7640-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="c7640-150">Azure Table Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="c7640-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="c7640-151">TooAzure 테이블 저장소에 작성 된 것 처럼 hello 게이트웨이-클라우드 메시지를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="c7640-152">*예상 시간 toocomplete: 5 분*</span><span class="sxs-lookup"><span data-stu-id="c7640-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="c7640-153">너무 이동[Azure 테이블 저장소에서 읽은 메시지 지속](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c7640-154">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c7640-154">Troubleshooting</span></span>
<span data-ttu-id="c7640-155">Hello에 솔루션에 대 한 hello 단원 중 문제 수 있으면 확인 [문제 해결](iot-hub-gateway-kit-c-sim-troubleshooting.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c7640-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="c7640-156">자세히 살펴보기</span><span class="sxs-lookup"><span data-stu-id="c7640-156">Explore more</span></span>
<span data-ttu-id="c7640-157">Hello 방문 [Intel IoT 게이트웨이 키트 개발자 영역](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7640-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
