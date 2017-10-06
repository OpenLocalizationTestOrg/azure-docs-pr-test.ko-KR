---
title: "연결 Intel Edison (노드) tooAzure IoT-4 단원: 메시지를 받을 | Microsoft Docs"
description: "샘플 응용 프로그램은 Edison에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 tooEdison 메시지를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "웹에서 수행한 Arduino 제어, 웹을 통해 수행한 Arduino 제어"
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
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="634bd-105">클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행</span><span class="sxs-lookup"><span data-stu-id="634bd-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="634bd-106">이 문서에서는 샘플 응용 프로그램을 Intel Edison에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="634bd-107">샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="634bd-108">실행할 수도 있습니다 gulp 작업 사용자 컴퓨터 toosend 메시지 tooEdison IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="634bd-109">샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="634bd-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="634bd-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="634bd-111">What you will do</span></span>
* <span data-ttu-id="634bd-112">Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="634bd-113">배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="634bd-114">IoT 허브 tooEdison tooblink hello LED에서에서 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="634bd-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="634bd-115">What you will learn</span></span>
<span data-ttu-id="634bd-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-116">In this article, you will learn:</span></span>
* <span data-ttu-id="634bd-117">어떻게 IoT 허브에서 toomonitor 들어오는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="634bd-118">IoT 허브 tooEdison에서 toosend 클라우드-장치 메시지 방법을</span><span class="sxs-lookup"><span data-stu-id="634bd-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="634bd-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="634bd-119">What you need</span></span>
* <span data-ttu-id="634bd-120">Intel Edison, 사용하도록 설정.</span><span class="sxs-lookup"><span data-stu-id="634bd-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="634bd-121">tooset Edison를 확인 하려면 어떻게 해야 toolearn [장치 구성][configure-your-device]합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="634bd-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634bd-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="634bd-123">toolearn 어떻게 toocreate IoT 허브 참조 [Azure IoT Hub를 만들][create-your-azure-iot-hub]합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="634bd-124">Hello 샘플 응용 프로그램 tooyour IoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="634bd-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="634bd-125">Hello 리포지토리 폴더에 본인 `iot-hub-node-edison-getting-started`합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="634bd-126">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="634bd-127">hello에 hello 파일 `app` 하위 폴더는 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="634bd-128">hello `blinkLED` 함수 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Hello 샘플 응용 프로그램의 리 포 구조][repo-structure]
2. <span data-ttu-id="634bd-130">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="634bd-131">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] 이 컴퓨터에 모든 hello 구성 상속 되므로 hello 단계 toohello 배포 작업을 건너뛸 수 있습니다 및 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="634bd-132">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-edison.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="634bd-133">hello `config-edison.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Hello edison.json 구성 파일의 내용](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="634bd-135">대체 **[장치 호스트 이름 또는 IP 주소]** hello 장치 IP 주소 장치를 구성 했을 때를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="634bd-136">대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="634bd-137">대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="634bd-138">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="634bd-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="634bd-139">배포 및 실행 hello 샘플 응용 프로그램 Edison hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="634bd-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="634bd-140">hello gulp 명령은 hello 샘플 응용 프로그램 tooEdison를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="634bd-141">그런 다음 실행 hello 응용 프로그램 호스트에 별도 작업 및 Edison 컴퓨터 toosend 20 깜박임 메시지 tooEdison IoT 허브에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="634bd-142">Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="634bd-143">한편, hello gulp 작업 IoT 허브 tooEdison에서 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="634bd-144">Edison 받는 각 깜박임 메시지에 대 한 hello 샘플 응용 프로그램 호출 hello `blinkLED` 함수 tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="634bd-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="634bd-145">Hello led가 깜박입니다 hello로 2 초 마다 작업 IoT 허브 tooEdison에서 20 메시지 전송 gulp 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="634bd-146">hello 마지막 하나는 "중지" 메시지 hello 응용 프로그램이 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="634bd-148">요약</span><span class="sxs-lookup"><span data-stu-id="634bd-148">Summary</span></span>
<span data-ttu-id="634bd-149">IoT 허브 tooEdison tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="634bd-150">hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="634bd-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="634bd-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="634bd-151">Next steps</span></span>
<span data-ttu-id="634bd-152">[Hello 켜고 hello LED의 동작 변경][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="634bd-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md