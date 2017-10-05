---
title: "Azure IoT에 Arduino(C) 연결 - 단원 3: 샘플 실행 | Microsoft Docs"
description: "IoT Hub에 메시지를 보내고 LED를 깜빡이는 샘플 응용 프로그램을 Adafruit Feather M0 WiFi에 배포하고 실행합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스, arduino 클라우드에 데이터 보내기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="cba5d-104">샘플 응용 프로그램을 실행하여 장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="cba5d-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cba5d-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="cba5d-105">What you will do</span></span>
<span data-ttu-id="cba5d-106">이 문서는 IoT Hub에 메시지를 보내는 샘플 응용 프로그램을 Adafruit Feather M0 WiFi Arduino 보드에 배포하고 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="cba5d-107">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="cba5d-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cba5d-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="cba5d-108">What you will learn</span></span>
<span data-ttu-id="cba5d-109">Gulp 도구를 사용하여 Arduino 보드에서 샘플 Arduino 응용 프로그램을 배포하고 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cba5d-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="cba5d-110">What you need</span></span>
* <span data-ttu-id="cba5d-111">이 작업을 시작하기 전에 [IoT Hub 메시지를 처리하고 저장하기 위해 Azure 함수 앱 및 저장소 계정 만들기][process-and-store-iot-hub-messages]를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="cba5d-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="cba5d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="cba5d-113">장치 연결 문자열은 Arduino 보드를 IoT Hub에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="cba5d-114">IoT Hub 연결 문자열은 IoT Hub를 장치 ID에 연결하는 데 사용됩니다. 이 ID는 IoT Hub에서 Arduino 보드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="cba5d-115">다음 Azure CLI 명령을 실행하여 리소스 그룹의 모든 IoT Hub를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="cba5d-116">값을 변경하지 않았다면 `iot-sample`을 `{resource group name}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="cba5d-117">다음 Azure CLI 명령을 실행하여 IoT Hub 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="cba5d-118">`{my hub name}`은 IoT Hub를 만들고 Arduino 보드를 등록할 때 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="cba5d-119">다음 명령을 실행하여 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="cba5d-120">값을 변경하지 않았다면 `mym0wifi`을 `{device id}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="cba5d-121">장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="cba5d-121">Configure the device connection</span></span>
<span data-ttu-id="cba5d-122">장치 연결을 구성하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="cba5d-123">장치 검색 cli를 사용하여 장치의 직렬 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="cba5d-124">다음과 유사한 출력이 표시되면 Arduino 보드에 대한 usb COM 포트를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![장치 검색][device-discovery]

2. <span data-ttu-id="cba5d-126">단원 폴더에서 `config.json` 파일을 열고 검색한 COM 포트 번호의 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="cba5d-128">Windows 플랫폼에서 COM 포트는 `COM1, COM2, ...` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="cba5d-129">macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="cba5d-130">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="cba5d-131">다음 명령을 실행하여 Visual Studio Code에서 장치 구성 파일 `config-arduino.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="cba5d-133">`config-arduino.json` 파일에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="cba5d-134">**[Wi-Fi SSID]**를 인터넷에 연결된 Wi-Fi SSID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="cba5d-135">**[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="cba5d-136">Wi-Fi에 암호가 필요하지 않은 경우 문자열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="cba5d-137">**[IoT device connection string]**을 가져온 `device connection string`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="cba5d-138">**[IoT hub connection string]**을 가져온 `iot hub connection string`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cba5d-139">이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="cba5d-140">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="cba5d-141">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="cba5d-141">Deploy and run the sample application</span></span>
<span data-ttu-id="cba5d-142">다음 명령을 실행하여 Arduino 보드에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="cba5d-143">기본 gulp 작업은 `install-tools` 및 `run` 작업을 순차적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="cba5d-144">[깜박임 앱 배포][deployed-the-blink-app] 시 별도로 이러한 작업을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="cba5d-145">샘플 응용 프로그램 작동 확인</span><span class="sxs-lookup"><span data-stu-id="cba5d-145">Verify that the sample application works</span></span>
<span data-ttu-id="cba5d-146">GPIO #0 온보드 LED가 2초마다 깜박여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="cba5d-147">LED가 깜빡일 때마다 샘플 응용 프로그램은 IoT Hub에 메시지를 전송하고 해당 메시지가 IoT Hub에 성공적으로 전송되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="cba5d-148">또한 IoT Hub가 수신한 각 메시지가 콘솔 창에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="cba5d-149">샘플 응용 프로그램은 메시지를 20개 보낸 후에 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-149">The sample application terminates automatically after sending 20 messages.</span></span>

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="cba5d-151">요약</span><span class="sxs-lookup"><span data-stu-id="cba5d-151">Summary</span></span>
<span data-ttu-id="cba5d-152">IoT Hub에 장치-클라우드 메시지를 보내기 위해 Arduino 보드에 깜빡이는 샘플 응용 프로그램을 새로 배포하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="cba5d-153">이제 저장소 계정에 메시지가 작성될 때 해당 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="cba5d-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cba5d-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cba5d-154">Next steps</span></span>
<span data-ttu-id="cba5d-155">[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="cba5d-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md