---
title: "Connect Arduino (C) tooAzure IoT-4 단원: 클라우드-장치 | Microsoft Docs"
description: "샘플 응용 프로그램은 Adafruit Feather M0 WiFi에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새 gulp 작업 IoT 허브 tooblink hello LED에서에서 메시지 tooAdafruit 페더 M0 WiFi를 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "웹에서 수행한 Arduino 제어, 웹을 통해 수행한 Arduino 제어"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="780e5-105">클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행</span><span class="sxs-lookup"><span data-stu-id="780e5-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="780e5-106">이 문서에서는 Adafruit Feather M0 WiFi Arduino 보드에 샘플 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="780e5-107">샘플 응용 프로그램 hello IoT 허브에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="780e5-108">실행할 수도 있습니다 gulp 작업 컴퓨터 toosend 메시지 tooyour Arduino 보드 IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="780e5-109">샘플 응용 프로그램 hello hello 메시지를 받으면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="780e5-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="780e5-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="780e5-111">What you will do</span></span>
* <span data-ttu-id="780e5-112">Hello 샘플 응용 프로그램 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="780e5-113">배포 하 고 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="780e5-114">프로그램 IoT 허브 tooyour Arduino 보드 tooblink hello LED에서에서 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="780e5-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="780e5-115">What you will learn</span></span>
<span data-ttu-id="780e5-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-116">In this article, you will learn:</span></span>
* <span data-ttu-id="780e5-117">어떻게 IoT 허브에서 toomonitor 들어오는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="780e5-118">IoT 허브 tooyour Arduino 보드에서에서 toosend 클라우드-장치 메시지 방법을</span><span class="sxs-lookup"><span data-stu-id="780e5-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="780e5-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="780e5-119">What you need</span></span>
* <span data-ttu-id="780e5-120">Arduino 보드를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="780e5-121">tooset Arduino 보드를 확인 하려면 어떻게 해야 toolearn [장치 구성][configure-your-device]합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="780e5-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="780e5-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="780e5-123">toolearn 어떻게 toocreate IoT 허브 참조 [Azure IoT Hub를 만들][create-your-azure-iot-hub]합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="780e5-124">Hello 샘플 응용 프로그램 tooyour IoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="780e5-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="780e5-125">Hello 리포지토리 폴더에 본인 `iot-hub-c-feather-m0-getting-started`합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="780e5-126">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="780e5-127">공지 hello `app.ino` hello에 대 한 파일 `app` 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="780e5-128">hello `app.ino` 파일은 hello 코드 toomonitor hello IoT 허브에서 들어오는 메시지를 포함 하는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="780e5-129">hello `blinkLED` 함수 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Hello 샘플 응용 프로그램의 리 포 구조][repo-structure]

2. <span data-ttu-id="780e5-131">Hello hello 장치 검색 cli 사용 하 여 hello 장치의 직렬 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="780e5-132">Toohello 다음과 유사한 출력을 확인 및 Arduino 보드에 대 한 hello usb COM 포트를 찾을 해야 하면:</span><span class="sxs-lookup"><span data-stu-id="780e5-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![장치 검색][device-discovery]

3. <span data-ttu-id="780e5-134">파일 열기 hello `config.json` hello 단원 폴더 및 폴더의 COM 포트 번호를 발견 하는 hello 입력된 hello 값에서:</span><span class="sxs-lookup"><span data-stu-id="780e5-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="780e5-136">Windows 플랫폼에서 hello COM 포트에 대 한 형식이 지므로 hello의 `COM1, COM2, ...`합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="780e5-137">macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="780e5-138">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="780e5-139">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-arduino.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="780e5-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="780e5-140">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] 이 컴퓨터에 모든 hello 구성 상속 되므로 hello 단계 toohello 배포 작업을 건너뛸 수 있습니다 및 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="780e5-141">Hello 단계를 완료 하는 경우 [Azure 함수 응용 프로그램 및 저장소 계정 만들기] [ create-an-azure-function-app-and-storage-account] tooreplace hello 자리 표시자 hello에 다른 컴퓨터에 필요한 `config-arduino.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="780e5-142">hello `config-arduino.json` 파일은 홈 폴더의 hello 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Hello arduino.json 구성 파일의 내용][config-arduino-json]

   * <span data-ttu-id="780e5-144">대체 **[Wi-fi SSID]** toohello 인터넷 연결에 Wi-fi SSID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="780e5-145">**[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="780e5-146">Wi-fi 암호 필요 하지 않은 경우 hello 문자열을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="780e5-147">대체 **[IoT 장치 연결 문자열]** hello를 실행 하 여 얻을 수 있는 hello 장치 연결 문자열과 함께 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="780e5-148">대체 **[IoT 허브 연결 문자열]** hello를 실행 하 여 얻을 수 있는 IoT 허브 연결 문자열 hello로 `az iot hub show-connection-string --name {my hub name}` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="780e5-149">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="780e5-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="780e5-150">배포 하 고 hello 다음 명령을 실행 하 여 Arduino 보드에 hello 샘플 응용 프로그램을 실행:</span><span class="sxs-lookup"><span data-stu-id="780e5-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="780e5-151">hello gulp 명령은 hello 샘플 응용 프로그램 tooyour Arduino 보드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="780e5-152">그런 다음 실행 hello 응용 프로그램 Arduino 보드 및 호스트에 별도 작업 컴퓨터 toosend 20 깜박임 메시지 tooyour Arduino 보드 IoT 허브에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="780e5-153">Hello 샘플 응용 프로그램을 실행 한 후 toomessages IoT 허브에서 수신 대기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="780e5-154">한편, hello gulp 작업 IoT 허브 tooyour Arduino 보드에서에서 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="780e5-155">Hello 샘플 응용 프로그램에서는 hello 호출 보드 hello 각 깜박임 메시지 수신에 대 한 `blinkLED` 함수 tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="780e5-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="780e5-156">Hello LED 표시 되어야 hello gulp 작업 IoT 허브 tooyour Arduino 보드에서에서 20 개의 메시지를 보내는 2 초 마다 깜박이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="780e5-157">hello 마지막 하나는 "중지" 메시지 hello 응용 프로그램이 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][sample-application]

## <a name="summary"></a><span data-ttu-id="780e5-159">요약</span><span class="sxs-lookup"><span data-stu-id="780e5-159">Summary</span></span>
<span data-ttu-id="780e5-160">프로그램 IoT 허브 tooyour Arduino 보드 tooblink hello LED에서에서 성공적으로 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="780e5-161">hello 다음 작업은 선택 사항: hello 켜고 hello LED의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="780e5-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="780e5-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="780e5-162">Next steps</span></span>
<span data-ttu-id="780e5-163">[Hello 켜고 hello LED의 동작 변경][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="780e5-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md