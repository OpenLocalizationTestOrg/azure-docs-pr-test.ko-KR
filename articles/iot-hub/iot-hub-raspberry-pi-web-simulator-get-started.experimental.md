---
title: "시뮬레이션된 Raspberry Pi-클라우드(Node.js) - Azure IoT Hub에 Raspberry Pi 웹 시뮬레이터 연결 | Microsoft Docs"
description: "Raspberry Pi가 Azure 클라우드에 데이터를 보내도록 Raspberry Pi 웹 시뮬레이터를 Azure IoT Hub에 연결합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspberry pi 시뮬레이터, azure iot raspberry pi, raspberry pi iot hub, raspberry pi에서 클라우드로 데이터 전송, raspberry pi-클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 5b7e209b65ccf6edb32d211797663e5e5b170df8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="9eb68-104">Azure IoT Hub에 Raspberry Pi 온라인 시뮬레이터 연결(Node.js)</span><span class="sxs-lookup"><span data-stu-id="9eb68-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="9eb68-105">이 자습서에서는 Raspberry Pi 온라인 시뮬레이터 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="9eb68-106">그런 다음 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)를 사용하여 Pi 시뮬레이터를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="9eb68-107">물리적 장치가 있는 경우 시작하려면 [Azure IoT Hub에 Raspberry Pi 연결](iot-hub-raspberry-pi-kit-node-get-started.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9eb68-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="9eb68-108">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="9eb68-108">What you do</span></span>

* <span data-ttu-id="9eb68-109">Raspberry Pi 온라인 시뮬레이터의 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="9eb68-110">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-110">Create an IoT hub.</span></span>
* <span data-ttu-id="9eb68-111">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="9eb68-112">Pi에서 샘플 응용 프로그램을 실행하여 IoT Hub로 시뮬레이션된 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="9eb68-113">앞에서 만든 IoT Hub에 시뮬레이션된 Raspberry Pi를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="9eb68-114">그런 다음 시뮬레이터에서 샘플 응용 프로그램을 실행하여 센서 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="9eb68-115">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9eb68-116">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9eb68-116">What you learn</span></span>

* <span data-ttu-id="9eb68-117">Azure IoT Hub를 만들고 새 장치 연결 문자열을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="9eb68-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="9eb68-118">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="9eb68-119">Raspberry Pi 온라인 시뮬레이터를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9eb68-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="9eb68-120">IoT Hub로 센서 데이터를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="9eb68-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="9eb68-121">Raspberry Pi 웹 시뮬레이터 개요</span><span class="sxs-lookup"><span data-stu-id="9eb68-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="9eb68-122">단추를 클릭하여 Raspberry Pi 온라인 시뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="9eb68-123">Raspberry Pi 시뮬레이터 시작</span><span class="sxs-lookup"><span data-stu-id="9eb68-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="9eb68-124">웹 시뮬레이터에는 세 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-124">There are three areas in the web simulator.</span></span>
* <span data-ttu-id="9eb68-125">어셈블리 영역 - 기본 회로에서는 Pi가 BME280 센서 및 LED에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="9eb68-126">미리 보기 버전에서는 이 영역이 잠겨 있으므로 지금은 사용자 지정을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-126">The area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="9eb68-127">코딩 영역 - Raspberry Pi를 사용하여 코딩할 수 있는 온라인 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="9eb68-128">기본 샘플 응용 프로그램을 사용하여 BME280 센서에서 센서 데이터를 손쉽게 수집한 후 Azure IoT Hub로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="9eb68-129">응용 프로그램은 실제 Pi 장치와 완벽하게 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-129">The application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="9eb68-130">통합 콘솔 창 - 코드의 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="9eb68-131">이 창의 맨 위에는 세 개의 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="9eb68-132">**실행** - 코딩 영역에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="9eb68-133">**다시 설정** - 기본 샘플 응용 프로그램으로 코딩 영역을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="9eb68-134">**접기/확장** - 오른쪽에 있는 단추를 사용하여 콘솔 창 접기/확장을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="9eb68-135">Raspberry Pi 웹 시뮬레이터는 현재 미리 보기 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="9eb68-136">[Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator)에서 사용자 의견을 듣고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="9eb68-137">소스 코드는 [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator)에 공개되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Pi 온라인 시뮬레이터 개요](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="9eb68-139">Pi 웹 시뮬레이터에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9eb68-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="9eb68-140">코딩 영역에서 기본 샘플 응용 프로그램으로 작업 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="9eb68-141">15행의 자리 표시자를 Azure IoT Hub 장치 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="9eb68-142">![장치 연결 문자열 바꾸기](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="9eb68-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="9eb68-143">**실행**을 클릭하거나 `npm start`를 입력하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="9eb68-144">IoT Hub로 전송되는 센서 데이터와 메시지를 보여 주는 다음 출력이 표시됩니다. ![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="9eb68-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9eb68-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9eb68-145">Next steps</span></span>

<span data-ttu-id="9eb68-146">샘플 응용 프로그램을 실행하여 센서 데이터를 수집하고 IoT Hub로 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb68-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
