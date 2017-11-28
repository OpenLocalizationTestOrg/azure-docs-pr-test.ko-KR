---
title: "Azure IoT에 Arduino(C) 연결 - 단원 4: 클라우드-장치 | Microsoft Docs"
description: "샘플 응용 프로그램은 Adafruit Feather M0 WiFi에서 실행되며 IoT Hub에서 들어오는 메시지를 모니터링합니다. 새로운 gulp 작업은 IoT Hub에서 Adafruit Feather M0 WiFi로 메시지를 보내여 LED를 깜빡입니다."
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
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="04649-105">샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="04649-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="04649-106">이 문서에서는 Adafruit Feather M0 WiFi Arduino 보드에 샘플 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="04649-107">샘플 응용 프로그램은 IoT Hub에서 들어오는 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="04649-108">컴퓨터에서 gulp 작업을 실행하여 IoT Hub에서 Arduino 보드로 메시지를 보내기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="04649-109">샘플 응용 프로그램이 메시지를 수신하면 LED를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="04649-110">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="04649-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="04649-111">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="04649-111">What you will do</span></span>
* <span data-ttu-id="04649-112">샘플 응용 프로그램을 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="04649-113">샘플 응용 프로그램을 배포 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="04649-114">IoT Hub에서 Arduino 보드로 메시지를 보내고 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="04649-115">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="04649-115">What you will learn</span></span>
<span data-ttu-id="04649-116">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04649-116">In this article, you will learn:</span></span>
* <span data-ttu-id="04649-117">IoT Hub에서 들어오는 메시지를 모니터링하는 방법.</span><span class="sxs-lookup"><span data-stu-id="04649-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="04649-118">IoT Hub에서 Arduino 보드로 클라우드-장치 메시지를 보내는 방법.</span><span class="sxs-lookup"><span data-stu-id="04649-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="04649-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="04649-119">What you need</span></span>
* <span data-ttu-id="04649-120">Arduino 보드를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="04649-121">Arduino 보드를 설정하는 방법을 알아보려면 [장치 구성][configure-your-device]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04649-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="04649-122">Azure 구독에서 만든 IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04649-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="04649-123">IoT Hub를 만드는 방법을 알아보려면 [Azure IoT Hub 만들기][create-your-azure-iot-hub]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04649-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="04649-124">샘플 응용 프로그램을 IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="04649-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="04649-125">repo 폴더 `iot-hub-c-feather-m0-getting-started`에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="04649-126">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04649-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="04649-127">`app` 하위 폴더에서 `app.ino` 파일에 주목합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="04649-128">`app.ino` 파일은 IoT Hub에서 들어오는 메시지를 모니터링할 코드를 포함하는 주요 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="04649-129">`blinkLED` 함수는 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-129">The `blinkLED` function blinks the LED.</span></span>

   ![샘플 응용 프로그램의 Repo 구조][repo-structure]

2. <span data-ttu-id="04649-131">장치 검색 CLI를 사용하여 장치의 직렬 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="04649-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="04649-132">다음과 유사한 출력이 표시되면 Arduino 보드에 대한 usb COM 포트를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![장치 검색][device-discovery]

3. <span data-ttu-id="04649-134">단원 폴더에서 `config.json` 파일을 열고 검색한 COM 포트 번호의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="04649-136">Windows 플랫폼에서 COM 포트는 `COM1, COM2, ...` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="04649-137">macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="04649-138">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="04649-139">`config-arduino.json` 파일에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04649-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="04649-140">이 컴퓨터에서 [Azure 함수 앱 및 저장소 계정 만들기][create-an-azure-function-app-and-storage-account] 단계를 완료했다면 모든 구성이 상속되므로, 샘플 응용 프로그램 배포 및 실행 작업으로 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04649-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="04649-141">다른 컴퓨터에서 [Azure 함수 앱 및 저장소 계정 만들기][create-an-azure-function-app-and-storage-account] 단계를 완료했다면 `config-arduino.json` 파일에서 자리 표시자를 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="04649-142">`config-arduino.json` 파일은 홈 폴더의 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04649-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![config-arduino.json 파일의 내용][config-arduino-json]

   * <span data-ttu-id="04649-144">**[Wi-Fi SSID]**를 인터넷에 연결된 Wi-Fi SSID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04649-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="04649-145">**[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04649-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="04649-146">Wi-Fi에 암호가 필요하지 않은 경우 문자열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="04649-147">**[IoT device connection string]**을 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 명령을 실행하여 가져온 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04649-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="04649-148">**[IoT hub connection string]**을 `az iot hub show-connection-string --name {my hub name}` 명령을 실행하여 가져온 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04649-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="04649-149">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="04649-149">Deploy and run the sample application</span></span>
<span data-ttu-id="04649-150">다음 명령을 실행하여 Arduino 보드에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="04649-151">이 gulp 명령은 Arduino 보드에 샘플 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="04649-152">그런 다음 Arduino 보드에서 응용 프로그램을 실행하고 호스트에서 별도의 작업을 실행하여 20개의 blink 메시지를 IoT Hub에서 Arduino 보드로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04649-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="04649-153">샘플 응용 프로그램이 실행된 후 IoT Hub의 메시지를 수신 대기하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="04649-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="04649-154">그 동안 gulp 작업은 IoT Hub에서 Arduino 보드로 여러 개의 "blink" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04649-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="04649-155">보드에서 blink 메시지를 수신할 때마다 샘플 응용 프로그램이 `blinkLED` 함수를 호출하여 LED를 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="04649-156">gulp 작업이 IoT Hub에서 Arduino 보드에 20개의 메시지를 보내기 때문에 2초마다 LED가 깜박이는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04649-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="04649-157">마지막 깜빡임은 응용 프로그램 실행을 중지하는 "stop" 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-157">The last one is a "stop" message that stops the application from running.</span></span>

![gulp 명령 및 blink 메시지가 있는 샘플 응용 프로그램][sample-application]

## <a name="summary"></a><span data-ttu-id="04649-159">요약</span><span class="sxs-lookup"><span data-stu-id="04649-159">Summary</span></span>
<span data-ttu-id="04649-160">IoT Hub에서 Arduino 보드로 메시지를 보내어 LED를 깜빡이는 데 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="04649-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="04649-161">다음 작업인 LED 켜기 및 끄기 동작 변경은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="04649-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04649-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04649-162">Next steps</span></span>
<span data-ttu-id="04649-163">[LED 켜기 및 끄기 동작 변경][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="04649-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


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