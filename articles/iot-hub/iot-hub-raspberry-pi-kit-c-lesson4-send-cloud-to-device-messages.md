---
title: "Connect Raspberry Pi (C) tooAzure IoT-4 단원: 클라우드-장치 | Microsoft Docs"
description: "샘플 응용 프로그램은 Pi에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 tooPi 메시지를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드 toodevice, 클라우드에서 메시지"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="2e30e-105">클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행</span><span class="sxs-lookup"><span data-stu-id="2e30e-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="2e30e-106">이 문서에서는 샘플 응용 프로그램을 Raspberry Pi 3에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="2e30e-107">샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="2e30e-108">실행할 수도 있습니다 gulp 작업 사용자 컴퓨터 toosend 메시지 tooPi IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="2e30e-109">샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="2e30e-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2e30e-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="2e30e-111">What you will do</span></span>
* <span data-ttu-id="2e30e-112">Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="2e30e-113">배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="2e30e-114">IoT 허브 tooPi tooblink hello LED에서에서 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2e30e-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="2e30e-115">What you will learn</span></span>
<span data-ttu-id="2e30e-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="2e30e-117">어떻게 IoT 허브에서 toomonitor 들어오는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="2e30e-118">IoT 허브 tooPi에서 toosend 클라우드-장치 메시지 방법을</span><span class="sxs-lookup"><span data-stu-id="2e30e-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2e30e-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2e30e-119">What you need</span></span>
* <span data-ttu-id="2e30e-120">사용하도록 설정된 Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2e30e-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="2e30e-121">tooset Pi 확인 하려면 어떻게 해야 toolearn [장치 구성](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="2e30e-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e30e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="2e30e-123">toolearn 어떻게 toocreate IoT 허브 참조 [IoT 허브를 만들고 등록 라스베리 Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="2e30e-124">Hello 샘플 응용 프로그램 tooyour IoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="2e30e-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="2e30e-125">Hello 리포지토리 폴더에 본인 `iot-hub-c-raspberrypi-getting-started`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="2e30e-126">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="2e30e-127">공지 hello `app.c` hello에 대 한 파일 `app` 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="2e30e-128">hello `app.c` 파일은 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="2e30e-129">hello `blinkLED` 함수 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Hello 샘플 응용 프로그램의 리 포 구조](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="2e30e-131">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="2e30e-132">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) 이 컴퓨터에 모든 hello 구성 상속 되므로 toostep toohello 작업 hello 샘플 응용 프로그램 실행 및 배포를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="2e30e-133">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-raspberrypi.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="2e30e-134">hello `config-raspberrypi.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Hello raspberrypi.json 구성 파일의 내용](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="2e30e-136">대체 **[장치 호스트 이름 또는 IP 주소]** Pi의 IP 주소 또는 호스트 이름으로 hello를 실행 하 여 얻을 수 있는 `devdisco list --eth` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="2e30e-137">대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="2e30e-138">대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="2e30e-139">단원 1에서 **gulp install-tools**를 실행하지 않았다면 이 명령도 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2e30e-140">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2e30e-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="2e30e-141">배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="2e30e-142">hello gulp 명령 실행 도구 설치 작업을 먼저 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="2e30e-143">다음 샘플 응용 프로그램 tooPi hello를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="2e30e-144">마지막으로 실행 hello 응용 프로그램 Pi와 호스트에 별도 작업 컴퓨터 toosend 20 깜박임 메시지 tooPi IoT 허브에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="2e30e-145">Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="2e30e-146">한편, hello gulp 작업 IoT 허브 tooPi에서 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="2e30e-147">Pi를 받는 각 깜박임 메시지에 대 한 hello 샘플 응용 프로그램 호출 hello `blinkLED` 함수 tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="2e30e-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="2e30e-148">Hello led가 깜박입니다 hello로 2 초 마다 작업 IoT 허브 tooPi에서 20 메시지 전송 gulp 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="2e30e-149">hello 마지막 하나는 "중지" 메시지 hello 응용 프로그램이 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="2e30e-151">요약</span><span class="sxs-lookup"><span data-stu-id="2e30e-151">Summary</span></span>
<span data-ttu-id="2e30e-152">IoT 허브 tooPi tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="2e30e-153">hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e30e-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e30e-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e30e-154">Next steps</span></span>
[<span data-ttu-id="2e30e-155">Hello 켜고 hello LED의 동작 변경</span><span class="sxs-lookup"><span data-stu-id="2e30e-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
