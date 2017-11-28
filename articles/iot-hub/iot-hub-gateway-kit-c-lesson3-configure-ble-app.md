---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 3: 샘플 앱 실행 | Microsoft Docs"
description: "IoT hub 및 배포용 SensorTag에서 배포용 샘플 응용 프로그램 tooreceive 데이터를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "배포용 응용 프로그램, 센서 모니터 응용 프로그램, 센서 데이터 수집, 센서, 센서 데이터 toocloud의 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="69e91-104">BLE 샘플 응용 프로그램 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="69e91-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="69e91-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="69e91-105">What you will do</span></span>

- <span data-ttu-id="69e91-106">Hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="69e91-107">SensorTag 및 Intel NUC 간에 hello 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="69e91-108">배포용 (Bluetooth 낮은 에너지) 샘플 응용 프로그램에 대 한 hello Azure CLI tooget SensorTag 정보와 IoT 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="69e91-109">구성 하 고 hello 배포용 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="69e91-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="69e91-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="69e91-111">What you will learn</span></span>

<span data-ttu-id="69e91-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-112">In this article, you will learn:</span></span>

- <span data-ttu-id="69e91-113">어떻게 tooconfigure 및 실행된 hello 배포용 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="69e91-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="69e91-114">What you need</span></span>

<span data-ttu-id="69e91-115">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-115">You must have successfully completed</span></span>

- [<span data-ttu-id="69e91-116">IoT Hub 만들기 및 SensorTag 등록</span><span class="sxs-lookup"><span data-stu-id="69e91-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="69e91-117">Hello 샘플 리포지토리 toohello 호스트 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="69e91-118">tooclone hello 샘플 리포지토리 hello 호스트 컴퓨터에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="69e91-119">Windows에서 명령 프롬프트 창을 열거나 macOS 또는 Ubuntu에서 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="69e91-120">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="69e91-121">SensorTag 및 Intel NUC 간 hello 연결 설정</span><span class="sxs-lookup"><span data-stu-id="69e91-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="69e91-122">hello 연결을 tooset hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="69e91-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="69e91-123">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="69e91-124">열기 `config-gateway.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="69e91-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="69e91-125">다음 코드 줄을 hello 찾기 및 바꾸기 `[device hostname or IP address]` Intel NUC의 hello IP 주소 또는 호스트 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="69e91-126">![config gateway의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="69e91-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="69e91-127">Hello 다음 명령을 실행 하 여 Intel NUC에 도우미 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="69e91-128">다음 그림에서는 hello 및 녹색 LED가 깜박입니다 hello로 hello 전원 단추를 눌러 SensorTag를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![센서 태그 켜기](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="69e91-130">Hello 다음 명령을 실행 하 여 스캔 SensorTag 장치:</span><span class="sxs-lookup"><span data-stu-id="69e91-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="69e91-131">Hello 다음 명령을 실행 하 여 hello SensorTag 및 Intel NUC 간의 hello 연결을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="69e91-132">대체 `{mac address}` hello 이전 단계에서 가져온 MAC 주소 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="69e91-133">SensorTag의 hello 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="69e91-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="69e91-134">tooget hello hello 다음 hello 호스트 컴퓨터에서 명령을 실행 SensorTag의 Azure IoT 허브 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="69e91-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="69e91-135">`{IoT hub name}`사용한 hello IoT 허브 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="69e91-136">Iot 게이트웨이 사용 하 여의 hello 값으로 `{resource group name}` mydevice의 hello 값으로 사용 하 여 `{device id}` hello 값 2 단원에서에서 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="69e91-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="69e91-137">Hello 배포용 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="69e91-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="69e91-138">tooconfigure 및 실행된 hello 배포용 샘플 응용 프로그램에서는 hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="69e91-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="69e91-139">열기 `config-sensortag.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="69e91-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="69e91-141">Hello 대체 hello 코드에서 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="69e91-142">대체 `[IoT hub name]` 사용한 hello IoT 허브 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="69e91-143">대체 `[IoT device connection string]` 가져온 SensorTag의 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="69e91-144">대체 `[device_mac_address]` hello 가져온 SensorTag의 MAC 주소 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="69e91-145">Hello 배포용 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="69e91-146">toorun hello 배포용 샘플 응용 프로그램에서는 hello 호스트 컴퓨터에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="69e91-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="69e91-147">SensorTag를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="69e91-148">배포 및 실행 hello 배포용 샘플 응용 프로그램 Intel NUC hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="69e91-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="69e91-149">Hello 배포용 샘플 응용 프로그램이 작동 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="69e91-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="69e91-150">이제 hello 다음과 같은 출력을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-150">You should now see an output like hello following:</span></span>

![BLE 샘플 응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="69e91-152">온도 데이터 수집을 유지 하 고 tooyour IoT 허브를 전송 하는 hello 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="69e91-153">hello 샘플 응용 프로그램 보낸 40 초 후에 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="69e91-154">요약</span><span class="sxs-lookup"><span data-stu-id="69e91-154">Summary</span></span>

<span data-ttu-id="69e91-155">성공적으로 SensorTag와 Intel NUC 간에 hello 연결을 설정 하 고 수집 하 고 SensorTag tooyour IoT 허브에서 데이터를 전송 하는 배포용 샘플 응용 프로그램을 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="69e91-156">Toolearn 준비를 하는 방법을 IoT hub 받은 tooverify hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="69e91-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69e91-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69e91-157">Next steps</span></span>
[<span data-ttu-id="69e91-158">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="69e91-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)