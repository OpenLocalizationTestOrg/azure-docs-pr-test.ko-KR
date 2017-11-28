---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 시작 | Microsoft Docs"
description: "IoT Gateway 시작 키트를 시작하여 Azure IoT Hub를 만들고 SensorTag 및 게이트웨이를 IoT Hub에 연결합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, iot 게이트웨이, 사물 인터넷 시작, iot 도구 키트"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="2ec6f-104">SensorTag를 사용하여 IoT Gateway 시작 키트 시작</span><span class="sxs-lookup"><span data-stu-id="2ec6f-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ec6f-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="2ec6f-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="2ec6f-106">시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="2ec6f-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="2ec6f-107">이 자습서에서는 [IoT Gateway 시작 키트](https://aka.ms/gateway-kit)를 실행하는 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="2ec6f-108">Wind River Linux 및 [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main)를 실행 중인 Intel NUC로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="2ec6f-109">Azure IoT Hub를 사용하여 장치를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="2ec6f-110">**아직 키트가 없나요?:** [여기](https://aka.ms/gateway-kit)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="2ec6f-111">**SensorTag가 없나요?:** [시뮬레이트된 장치로 시작하거나](iot-hub-gateway-kit-c-sim-get-started.md) [SensorTag를 구입합니다.](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="2ec6f-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="2ec6f-112">단원 1: NUC 구성</span><span class="sxs-lookup"><span data-stu-id="2ec6f-112">Lesson 1: Configure your NUC</span></span>
![단원 1 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="2ec6f-114">이 단원에서는 키트의 Intel NUC(Next Unit of Computing)를 Azure IoT Gateway로 설정하고 NUC에 Azure IoT Edge 패키지를 설치한 다음 샘플 앱을 실행하여 게이트웨이 기능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="2ec6f-115">*예상 완료 시간: 15분*</span><span class="sxs-lookup"><span data-stu-id="2ec6f-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2ec6f-116">[Intel NUC를 IoT Gateway로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)으로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="2ec6f-117">단원 2: IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-117">Lesson 2: Create your IoT Hub</span></span>
![단원 2 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="2ec6f-119">이 단원에서는 호스트 컴퓨터에 도구 및 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="2ec6f-120">그런 다음 무료 Azure 계정을 만들고, Azure IoT Hub를 프로비전하며, IoT Hub에서 첫 번째 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="2ec6f-121">이 단원을 시작하기 전에 1단원을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="2ec6f-122">도구 얻기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-122">Get the tools</span></span>
<span data-ttu-id="2ec6f-123">호스트 컴퓨터에 도구 및 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="2ec6f-124">*예상 완료 시간: 20분* </span><span class="sxs-lookup"><span data-stu-id="2ec6f-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="2ec6f-125">[도구 얻기](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="2ec6f-126">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="2ec6f-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="2ec6f-127">리소스 그룹을 만들고, 첫 번째 Azure IoT Hub를 프로비전하며, Azure CLI를 사용하여 첫 번째 장치를 IoT Hub에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="2ec6f-128">*예상 완료 시간: 10분*  </span><span class="sxs-lookup"><span data-stu-id="2ec6f-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="2ec6f-129">[IoT Hub 만들기 및 장치 등록](iot-hub-gateway-kit-c-lesson2-register-device.md)으로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="2ec6f-130">3단원: SensorTag에서 메시지 수신 및 IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="2ec6f-131">이 단원에서는 스크립트를 사용하여 게이트웨이에서 BLE 샘플 응용 프로그램의 구성 및 실행을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="2ec6f-132">이러한 응용 프로그램은 모듈 컬렉션을 사용하여 데이터 집계 및 변환, 명령 처리 또는 여러 가지 관련 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="2ec6f-133">모듈은 메시지 브로커를 통해 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="2ec6f-134">샘플 응용 프로그램에는 BLE 모듈과 IoT Hub 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="2ec6f-135">BLE 모듈은 BLE SensorTag에서 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="2ec6f-136">IoT Hub 모듈은 받은 데이터를 패키지하고 Azure IoT Edge에 제공된 게이트웨이 프레임워크를 통해 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![단원 3 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="2ec6f-138">BLE 샘플 앱 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="2ec6f-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="2ec6f-139">SensorTag와 게이트웨이 간의 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="2ec6f-140">그런 다음 구성을 완료하고 BLE 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="2ec6f-141">*예상 완료 시간: 15분*</span><span class="sxs-lookup"><span data-stu-id="2ec6f-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2ec6f-142">[BLE 샘플 앱 구성 및 실행](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)으로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="2ec6f-143">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="2ec6f-144">IoT Hub에서 메시지를 읽으려면 호스트 컴퓨터에서 샘플 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="2ec6f-145">*예상 완료 시간: 15분*</span><span class="sxs-lookup"><span data-stu-id="2ec6f-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2ec6f-146">[IoT Hub에서 메시지 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="2ec6f-147">4단원: Azure Table Storage로 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="2ec6f-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="2ec6f-148">IoT Hub에서 들어오는 메시지를 가져와서 Azure Table Storage에 쓰는 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![단원 4 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2ec6f-150">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="2ec6f-151">Azure Resource Manager 템플릿을 사용하여 Azure 함수 앱 및 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="2ec6f-152">*예상 완료 시간: 10분*  </span><span class="sxs-lookup"><span data-stu-id="2ec6f-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="2ec6f-153">[Azure 함수 앱 및 Azure Storage 계정 만들기](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="2ec6f-154">Azure Table Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="2ec6f-155">게이트웨이-클라우드 메시지가 Azure Table Storage에 기록될 때 해당 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="2ec6f-156">*예상 완료 시간: 5분*  </span><span class="sxs-lookup"><span data-stu-id="2ec6f-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="2ec6f-157">[Azure Table Storage에 유지되는 메시지 읽기](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)로 이동</span><span class="sxs-lookup"><span data-stu-id="2ec6f-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2ec6f-158">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2ec6f-158">Troubleshooting</span></span>
<span data-ttu-id="2ec6f-159">단원을 진행하는 동안 문제가 발생하면 [문제 해결](iot-hub-gateway-kit-c-troubleshooting.md) 문서에서 솔루션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="2ec6f-160">자세히 살펴보기</span><span class="sxs-lookup"><span data-stu-id="2ec6f-160">Explore more</span></span>
<span data-ttu-id="2ec6f-161">자세한 내용은 [Intel IoT Gateway Kit 개발자 영역](http://software.intel.com/iot/microsoft-azure)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec6f-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>