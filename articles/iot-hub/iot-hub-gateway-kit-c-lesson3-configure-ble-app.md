---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 3: 샘플 앱 실행 | Microsoft Docs"
description: "BLE 샘플 응용 프로그램을 실행하여 BLE SensorTag 및 IoT Hub에서 데이터를 수신합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ble 앱, 센서 모니터 앱, 센서 데이터 수집, 센서의 데이터, 센서 데이터를 클라우드로"
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="3bc7f-104">BLE 샘플 응용 프로그램 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="3bc7f-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3bc7f-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="3bc7f-105">What you will do</span></span>

- <span data-ttu-id="3bc7f-106">샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="3bc7f-107">SensorTag와 Intel NUC 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="3bc7f-108">Azure CLI를 사용하여 BLE(Bluetooth Low Energy) 샘플 응용 프로그램에 대한 IoT Hub 및 SensorTag 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="3bc7f-109">그런 다음 BLE 샘플 응용 프로그램 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="3bc7f-110">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3bc7f-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="3bc7f-111">What you will learn</span></span>

<span data-ttu-id="3bc7f-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-112">In this article, you will learn:</span></span>

- <span data-ttu-id="3bc7f-113">BLE 샘플 응용 프로그램을 구성하고 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="3bc7f-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3bc7f-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="3bc7f-114">What you need</span></span>

<span data-ttu-id="3bc7f-115">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-115">You must have successfully completed</span></span>

- [<span data-ttu-id="3bc7f-116">IoT Hub 만들기 및 SensorTag 등록</span><span class="sxs-lookup"><span data-stu-id="3bc7f-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="3bc7f-117">호스트 컴퓨터에 샘플 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="3bc7f-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="3bc7f-118">샘플 리포지토리를 복제하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3bc7f-119">Windows에서 명령 프롬프트 창을 열거나 macOS 또는 Ubuntu에서 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="3bc7f-120">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="3bc7f-121">SensorTag와 Intel NUC 간에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="3bc7f-122">연결을 설정하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3bc7f-123">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="3bc7f-124">다음 명령을 실행하여 Visual Studio Code에서 `config-gateway.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="3bc7f-125">다음 코드 줄을 찾아 `[device hostname or IP address]`를 Intel NUC의 IP 주소 또는 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="3bc7f-126">![config gateway의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="3bc7f-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="3bc7f-127">다음 명령을 실행하여 Intel NUC에 도우미 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="3bc7f-128">다음 그림과 같이 전원 단추를 눌러 SensorTag를 켜면 녹색 LED가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![센서 태그 켜기](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="3bc7f-130">다음 명령을 실행하여 SensorTag 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="3bc7f-131">다음 명령을 실행하여 SensorTag 및 Intel NUC 간의 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="3bc7f-132">`{mac address}`를 이전 단계에서 가져온 MAC 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="3bc7f-133">SensorTag의 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="3bc7f-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="3bc7f-134">SensorTag의 Azure IoT Hub 연결 문자열을 가져오려면 호스트 컴퓨터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="3bc7f-135">`{IoT hub name}`은 사용한 IoT Hub 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="3bc7f-136">단원 2에서 값을 변경하지 않았다면 iot-gateway를 `{resource group name}` 값으로 사용하고 mydevice를 `{device id}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="3bc7f-137">BLE 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="3bc7f-137">Configure the BLE sample application</span></span>

<span data-ttu-id="3bc7f-138">BLE 샘플 응용 프로그램을 구성하고 실행하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3bc7f-139">다음 명령을 실행하여 Visual Studio Code에서 `config-sensortag.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="3bc7f-141">코드에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="3bc7f-142">`[IoT hub name]`을 사용한 IoT Hub 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="3bc7f-143">`[IoT device connection string]`을 가져온 SensorTag 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="3bc7f-144">`[device_mac_address]`를 가져온 SensorTag의 MAC 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="3bc7f-145">BLE 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="3bc7f-146">BLE 샘플 응용 프로그램을 실행하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="3bc7f-147">SensorTag를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="3bc7f-148">다음 명령을 실행하여 Intel NUC에 BLE 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="3bc7f-149">BLE 샘플 응용 프로그램 작동 확인</span><span class="sxs-lookup"><span data-stu-id="3bc7f-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="3bc7f-150">이제 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-150">You should now see an output like the following:</span></span>

![BLE 샘플 응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="3bc7f-152">샘플 응용 프로그램은 계속 온도 데이터를 수집하여 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="3bc7f-153">샘플 응용 프로그램은 보내고 40초 후에 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="3bc7f-154">요약</span><span class="sxs-lookup"><span data-stu-id="3bc7f-154">Summary</span></span>

<span data-ttu-id="3bc7f-155">SensorTag와 Intel NUC 간의 연결을 성공적으로 설정하고 SensorTag에서 데이터를 수집하여 IoT Hub로 보내는 BLE 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="3bc7f-156">이제 IoT Hub가 데이터를 수신했는지 확인하는 방법을 배울 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7f-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bc7f-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bc7f-157">Next steps</span></span>
[<span data-ttu-id="3bc7f-158">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="3bc7f-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)