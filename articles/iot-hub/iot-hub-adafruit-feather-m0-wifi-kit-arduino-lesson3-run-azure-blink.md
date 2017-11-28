---
title: "Connect Arduino (C) tooAzure IoT-3 단원: 샘플을 실행 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooAdafruit 페더 M0 WiFi tooyour IoT hub 메시지를 보내고 hello led가 깜박이를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스 arduino toocloud 데이터 보내기"
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="7bec3-104">샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행</span><span class="sxs-lookup"><span data-stu-id="7bec3-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7bec3-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="7bec3-105">What you will do</span></span>
<span data-ttu-id="7bec3-106">이 문서에서는 보여 toodeploy 및 프로그램 Adafruit 페더 M0 WiFi Arduino에서 샘플 응용 프로그램 실행을 해당 보내는 메시지 tooyour IoT 허브 보드 어떻게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="7bec3-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7bec3-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="7bec3-108">What you will learn</span></span>
<span data-ttu-id="7bec3-109">하면 toouse hello 도구 toodeploy gulp 하 고 Arduino 보드에 hello 샘플 Arduino 응용 프로그램을 실행 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7bec3-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="7bec3-110">What you need</span></span>
* <span data-ttu-id="7bec3-111">이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들][process-and-store-iot-hub-messages]합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="7bec3-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="7bec3-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="7bec3-113">장치 연결 문자열 hello 사용 되는 tooconnect Arduino 보드 tooyour IoT 허브는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="7bec3-114">hello IoT 허브 연결 문자열은 프로그램 Arduino 나타내는 IoT 허브 toohello 장치 id 보드 hello IoT 허브에서 사용 되는 tooconnect입니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="7bec3-115">Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="7bec3-116">사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7bec3-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="7bec3-117">Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="7bec3-118">`{my hub name}`IoT 허브를 만들고 Arduino 보드를 등록 하는 때를 지정 하는 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="7bec3-119">Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="7bec3-120">사용 하 여 `mym0wifi` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7bec3-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="7bec3-121">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="7bec3-121">Configure hello device connection</span></span>
<span data-ttu-id="7bec3-122">tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="7bec3-123">Hello hello 장치 검색 cli 사용 하 여 hello 장치의 직렬 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="7bec3-124">Toohello 다음과 유사한 출력을 확인 및 Arduino 보드에 대 한 hello usb COM 포트를 찾을 해야 하면:</span><span class="sxs-lookup"><span data-stu-id="7bec3-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![장치 검색][device-discovery]

2. <span data-ttu-id="7bec3-126">파일 열기 hello `config.json` 단원 폴더 hello와의 COM 포트 번호를 발견 하는 hello hello 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="7bec3-128">Windows 플랫폼에서 hello COM 포트에 대 한 형식이 지므로 hello의 `COM1, COM2, ...`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="7bec3-129">macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="7bec3-130">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="7bec3-131">장치 구성 파일 열기 hello `config-arduino.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="7bec3-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="7bec3-133">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-arduino.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="7bec3-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="7bec3-134">대체 **[Wi-fi SSID]** toohello 인터넷 연결에 Wi-fi SSID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="7bec3-135">**[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="7bec3-136">Wi-fi 암호 필요 하지 않은 경우 hello 문자열을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="7bec3-137">대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="7bec3-138">대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7bec3-139">이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="7bec3-140">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="7bec3-141">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bec3-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="7bec3-142">배포 하 고 hello 다음 명령을 실행 하 여 Arduino 보드에 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="7bec3-143">hello 기본 gulp 작업 실행 `install-tools` 및 `run` 순차적으로 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="7bec3-144">때 있습니다 [hello 깜박임 앱 배포][deployed-the-blink-app]를 개별적으로 이러한 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="7bec3-145">Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7bec3-145">Verify that hello sample application works</span></span>
<span data-ttu-id="7bec3-146">Hello GPIO #0 온보드 led가 깜박입니다.이 2 초 마다 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="7bec3-147">Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="7bec3-148">또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="7bec3-149">샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="7bec3-151">요약</span><span class="sxs-lookup"><span data-stu-id="7bec3-151">Summary</span></span>
<span data-ttu-id="7bec3-152">배포 되었으며 Arduino 보드 toosend 장치-클라우드 메시지 tooyour IoT 허브에서 hello 새 깜박임 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="7bec3-153">이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bec3-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bec3-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bec3-154">Next steps</span></span>
<span data-ttu-id="7bec3-155">[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="7bec3-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md