---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 4: 메시지 수신 | Microsoft Docs"
description: "샘플 응용 프로그램은 Edison에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새로운 gulp 작업은 IoT Hub에서 Edison으로 메시지를 보내고 LED를 깜빡입니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "웹에서 arduino led 제어, 웹을 통한 arduino led 제어"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="199d4-105">샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="199d4-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="199d4-106">이 문서에서는 샘플 응용 프로그램을 Intel Edison에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="199d4-107">샘플 응용 프로그램은 IoT Hub에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="199d4-108">컴퓨터에서 gulp 작업을 실행하여 IoT Hub에서 Edison으로 메시지를 보내기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="199d4-109">샘플 응용 프로그램이 메시지를 수신하면 LED를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="199d4-110">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="199d4-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="199d4-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="199d4-111">What you will do</span></span>
* <span data-ttu-id="199d4-112">샘플 응용 프로그램을 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="199d4-113">샘플 응용 프로그램을 배포 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="199d4-114">IoT Hub에서 Edison으로 메시지를 보내고 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="199d4-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="199d4-115">What you will learn</span></span>
<span data-ttu-id="199d4-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-116">In this article, you will learn:</span></span>
* <span data-ttu-id="199d4-117">IoT Hub에서 들어오는 메시지를 모니터링하는 방법.</span><span class="sxs-lookup"><span data-stu-id="199d4-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="199d4-118">IoT Hub에서 Edison으로 클라우드-장치 메시지를 보내는 방법.</span><span class="sxs-lookup"><span data-stu-id="199d4-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="199d4-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="199d4-119">What you need</span></span>
* <span data-ttu-id="199d4-120">Intel Edison, 사용하도록 설정.</span><span class="sxs-lookup"><span data-stu-id="199d4-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="199d4-121">Edison을 설정하는 방법은 [장치 구성][configure-your-device]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199d4-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="199d4-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="199d4-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="199d4-123">IoT Hub를 만드는 방법을 알아보려면 [Azure IoT Hub 만들기][create-your-azure-iot-hub]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199d4-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="199d4-124">샘플 응용 프로그램을 IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="199d4-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="199d4-125">repo 폴더 `iot-hub-node-edison-getting-started`에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="199d4-126">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="199d4-127">`app` 하위 폴더의 파일은 IoT Hub에서 들어오는 메시지를 모니터링할 코드를 포함하는 핵심 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="199d4-128">`blinkLED` 함수는 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-128">The `blinkLED` function blinks the LED.</span></span>

   ![샘플 응용 프로그램의 Repo 구조][repo-structure]
2. <span data-ttu-id="199d4-130">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="199d4-131">[Azure 함수 앱 및 저장소 계정 만들기][create-an-azure-function-app-and-storage-account] 단계를 이 컴퓨터에서 완료했다면 모든 구성이 상속되므로, 샘플 응용 프로그램 배포 및 실행 작업으로 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="199d4-132">다른 컴퓨터에서 [Azure 함수 앱 및 저장소 계정 만들기][create-an-azure-function-app-and-storage-account] 단계를 완료했다면 `config-edison.json` 파일에서 자리 표시자를 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="199d4-133">`config-edison.json` 파일은 홈 폴더의 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![config-edison.json 파일의 내용](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="199d4-135">**[device hostname or IP address]**를 장치를 구성할 때 적어 둔 장치 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="199d4-136">**[IoT device connection string]**을 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령을 실행하여 가져온 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="199d4-137">**[IoT hub connection string]**을 `az iot hub show-connection-string --name {my hub name}` 명령을 실행하여 가져온 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="199d4-138">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="199d4-138">Deploy and run the sample application</span></span>
<span data-ttu-id="199d4-139">다음 명령을 실행하여 Edison에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="199d4-140">이 gulp 명령은 샘플 응용 프로그램을 Edison에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="199d4-141">그런 다음 Edison에서 응용 프로그램을 실행하고 호스트 컴퓨터에서 별도의 작업을 실행하여 20개의 blink 메시지를 IoT Hub에서 Edison에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="199d4-142">샘플 응용 프로그램이 실행된 후 IoT Hub의 메시지를 수신 대기하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="199d4-143">그 동안 gulp 작업은 IoT Hub에서 Edison에 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="199d4-144">Edison에서 blink 메시지를 수신할 때마다 샘플 응용 프로그램이 `blinkLED` 함수를 호출하여 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="199d4-145">gulp 작업이 IoT Hub에서 Edison에 메시지를 20개 보내기 때문에 2초마다 LED가 깜박이는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="199d4-146">마지막 깜빡임은 응용 프로그램 실행을 중지하는 "stop" 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-146">The last one is a "stop" message that stops the application from running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="199d4-148">요약</span><span class="sxs-lookup"><span data-stu-id="199d4-148">Summary</span></span>
<span data-ttu-id="199d4-149">IoT Hub에서 Edison에 메시지를 보내서 LED를 깜빡이는 데 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="199d4-150">다음 작업인 LED 켜기 및 끄기 동작 변경은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="199d4-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="199d4-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="199d4-151">Next steps</span></span>
<span data-ttu-id="199d4-152">[LED 켜기 및 끄기 동작 변경][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="199d4-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md