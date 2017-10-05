---
featureFlags: usabilla
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 4: 클라우드-장치 | Microsoft Docs"
description: "샘플 응용 프로그램은 Pi에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새로운 gulp 작업은 IoT Hub에서 Pi로 메시지를 보내고 LED를 깜빡입니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드-장치, 클라우드의 메시지"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="2b4ac-105">샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="2b4ac-105">Run the sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="2b4ac-106">이 문서에서는 샘플 응용 프로그램을 Raspberry Pi 3에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="2b4ac-107">샘플 응용 프로그램은 IoT Hub에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="2b4ac-108">컴퓨터에서 gulp 작업을 실행하여 IoT Hub에서 Pi로 메시지를 보내기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="2b4ac-109">샘플 응용 프로그램이 메시지를 수신하면 LED를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="2b4ac-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2b4ac-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="2b4ac-111">What you will do</span></span>
* <span data-ttu-id="2b4ac-112">샘플 응용 프로그램을 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="2b4ac-113">샘플 응용 프로그램을 배포 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="2b4ac-114">IoT Hub에서 Pi로 메시지를 보내고 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2b4ac-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="2b4ac-115">What you will learn</span></span>
<span data-ttu-id="2b4ac-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-116">In this article, you will learn:</span></span>
* <span data-ttu-id="2b4ac-117">IoT Hub에서 들어오는 메시지를 모니터링하는 방법.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-117">How to monitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="2b4ac-118">IoT Hub에서 Pi로 클라우드-장치 메시지를 보내는 방법.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2b4ac-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2b4ac-119">What you need</span></span>
* <span data-ttu-id="2b4ac-120">사용하도록 설정된 Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="2b4ac-121">Pi를 설정하는 방법은 [장치 구성](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="2b4ac-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="2b4ac-123">IoT Hub를 만드는 방법을 알아보려면 [IoT Hub 만들기 및 Raspberry Pi 3 등록](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="2b4ac-124">샘플 응용 프로그램을 IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="2b4ac-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="2b4ac-125">repo 폴더 `iot-hub-node-raspberrypi-getting-started`에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="2b4ac-126">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="2b4ac-127">`app` 하위 폴더에서 `app.js` 파일에 주목합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-127">Notice the `app.js` file in the `app` subfolder.</span></span> <span data-ttu-id="2b4ac-128">`app.js` 파일은 IoT Hub에서 들어오는 메시지를 모니터링할 코드를 포함하는 주요 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="2b4ac-129">`blinkLED` 함수는 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-129">The `blinkLED` function blinks the LED.</span></span>
   
   ![샘플 응용 프로그램의 Repo 구조](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="2b4ac-131">다음 명령을 사용하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-131">Initialize the configuration file by using the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="2b4ac-132">[Azure 함수 앱 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) 단계를 이 컴퓨터에서 완료했다면 모든 구성이 상속되므로, 샘플 응용 프로그램 배포 및 실행 작업으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span></span> <span data-ttu-id="2b4ac-133">[Azure 함수 앱 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) 단계를 다른 컴퓨터에서 완료했다면 `config-raspberrypi.json` 파일에서 자리 표시자를 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="2b4ac-134">`config-raspberrypi.json` 파일은 홈 폴더의 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>
   
   ![config-raspberrypi.json 파일의 내용](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="2b4ac-136">**[device hostname or IP address]**를 Pi의 IP 주소 또는 `devdisco list --eth` 명령을 실행하여 가져온 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="2b4ac-137">**[IoT device connection string]**을 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` 명령을 실행하여 가져온 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="2b4ac-138">**[IoT hub connection string]**을 `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` 명령을 실행하여 가져온 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="2b4ac-139">단원 1에서 **gulp install-tools**를 실행하지 않았다면 이 명령도 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="2b4ac-140">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="2b4ac-140">Deploy and run the sample application</span></span>
<span data-ttu-id="2b4ac-141">다음 명령을 실행하여 Pi에 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-141">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="2b4ac-142">이 명령은 샘플 응용 프로그램을 Pi에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-142">The command deploys the sample application to Pi.</span></span> <span data-ttu-id="2b4ac-143">그런 다음 Pi에서 응용 프로그램을 실행하고 호스트에서 별도의 작업을 실행하여 20개의 blink 메시지를 IoT Hub에서 Pi에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="2b4ac-144">샘플 응용 프로그램이 실행된 후 IoT Hub의 메시지를 수신 대기하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-144">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="2b4ac-145">그 동안 gulp 작업은 IoT Hub에서 Pi에 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="2b4ac-146">Pi에서 blink 메시지를 수신할 때마다 샘플 응용 프로그램이 `blinkLED` 함수를 호출하여 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="2b4ac-147">gulp 작업이 IoT Hub에서 Pi에 메시지를 20개 보내기 때문에 2초마다 LED가 깜박이는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="2b4ac-148">마지막 깜빡임은 응용 프로그램에게 실행을 중지하도록 알려주는 "stop" 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-148">The last one is a "stop" message that tells the application to stop running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="2b4ac-150">요약</span><span class="sxs-lookup"><span data-stu-id="2b4ac-150">Summary</span></span>
<span data-ttu-id="2b4ac-151">IoT Hub에서 Pi에 메시지를 보내서 LED를 깜빡이는 데 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="2b4ac-152">다음 작업인 LED 켜기 및 끄기 동작 변경은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ac-152">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b4ac-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b4ac-153">Next steps</span></span>
[<span data-ttu-id="2b4ac-154">LED 켜기 및 끄기 동작 변경</span><span class="sxs-lookup"><span data-stu-id="2b4ac-154">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

