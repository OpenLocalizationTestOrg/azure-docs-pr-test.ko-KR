---
featureFlags: usabilla
title: "연결 라스베리 Pi (노드) tooAzure IoT-4 단원: 클라우드-장치 | Microsoft Docs"
description: "hello 샘플 응용 프로그램 플랫폼에서 실행 되 고 IoT 허브에서 들어오는 메시지를 모니터링 합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 tooPi 메시지를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드 toodevice, 클라우드에서 메시지"
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
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="b6831-105">Hello 샘플 응용 프로그램 tooreceive 클라우드-장치 메시지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="b6831-106">이 문서에서는 샘플 응용 프로그램을 Raspberry Pi 3에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="b6831-107">샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="b6831-108">실행할 수도 있습니다 gulp 작업 사용자 컴퓨터 toosend 메시지 tooPi IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="b6831-109">샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="b6831-110">문제가 있는 경우 솔루션 hello에 seek [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b6831-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="b6831-111">What you will do</span></span>
* <span data-ttu-id="b6831-112">Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="b6831-113">배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="b6831-114">IoT 허브 tooPi tooblink hello LED에서에서 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b6831-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="b6831-115">What you will learn</span></span>
<span data-ttu-id="b6831-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-116">In this article, you will learn:</span></span>
* <span data-ttu-id="b6831-117">IoT 허브에서의 toomonitor 받은 메시지</span><span class="sxs-lookup"><span data-stu-id="b6831-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="b6831-118">IoT 허브 tooPi에서 toosend 클라우드-장치 메시지 방법을</span><span class="sxs-lookup"><span data-stu-id="b6831-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6831-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="b6831-119">What you need</span></span>
* <span data-ttu-id="b6831-120">사용하도록 설정된 Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b6831-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="b6831-121">tooset Pi 확인 하려면 어떻게 해야 toolearn [장치 구성](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="b6831-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b6831-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="b6831-123">toolearn 어떻게 toocreate IoT 허브 참조 [IoT 허브를 만들고 등록 라스베리 Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="b6831-124">Hello 샘플 응용 프로그램 tooyour IoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="b6831-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="b6831-125">Hello 리포지토리 폴더에 본인 `iot-hub-node-raspberrypi-getting-started`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="b6831-126">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="b6831-127">공지 hello `app.js` hello에 대 한 파일 `app` 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="b6831-128">hello `app.js` 파일은 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="b6831-129">hello `blinkLED` 함수 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Hello 샘플 응용 프로그램의 리 포 구조](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="b6831-131">다음 명령을 hello를 사용 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="b6831-132">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) 이 컴퓨터에 모든 hello 구성 상속 되므로 toohello 작업 hello 샘플 응용 프로그램 실행 및 배포를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="b6831-133">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-raspberrypi.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="b6831-134">hello `config-raspberrypi.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Hello raspberrypi.json 구성 파일의 내용](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="b6831-136">대체 **[장치 호스트 이름 또는 IP 주소]** hello를 실행 하 여 얻을 수 있는 Pi 또는 hello 호스트 이름의 hello IP 주소로 `devdisco list --eth` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="b6831-137">대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="b6831-138">대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="b6831-139">단원 1에서 **gulp install-tools**를 실행하지 않았다면 이 명령도 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="b6831-140">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b6831-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="b6831-141">배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="b6831-142">hello 명령은 hello 샘플 응용 프로그램 tooPi를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="b6831-143">그런 다음 실행 hello 응용 프로그램 Pi와 호스트에 별도 작업 컴퓨터 toosend 20 깜박임 메시지 tooPi IoT 허브에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="b6831-144">Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="b6831-145">한편, hello gulp 작업 IoT 허브 tooPi에서 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="b6831-146">Pi를 받는 각 깜박임 메시지에 대 한 hello 샘플 응용 프로그램 호출 hello `blinkLED` 함수 tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="b6831-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="b6831-147">Hello led가 깜박입니다 hello로 2 초 마다 작업 IoT 허브 tooPi에서 20 메시지 전송 gulp 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="b6831-148">hello 마지막 하나는 "중지" 메시지를 실행 하는 hello 응용 프로그램 toostop 알려주는입니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="b6831-150">요약</span><span class="sxs-lookup"><span data-stu-id="b6831-150">Summary</span></span>
<span data-ttu-id="b6831-151">IoT 허브 tooPi tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="b6831-152">hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6831-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6831-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6831-153">Next steps</span></span>
[<span data-ttu-id="b6831-154">Hello 켜고 hello LED의 동작 변경</span><span class="sxs-lookup"><span data-stu-id="b6831-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

