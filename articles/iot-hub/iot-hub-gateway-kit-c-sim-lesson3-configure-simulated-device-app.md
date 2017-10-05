---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 3: 샘플 앱 실행 | Microsoft Docs"
description: "시뮬레이트된 장치 샘플 앱을 실행하여 온도 데이터를 IoT Hub에 보내기"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "데이터를 클라우드로"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="e1229-104">시뮬레이트된 장치 샘플 앱 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="e1229-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e1229-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="e1229-105">What you will do</span></span>

- <span data-ttu-id="e1229-106">샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-106">Clone the sample repository.</span></span>
- <span data-ttu-id="e1229-107">Azure CLI를 사용하여 시뮬레이트된 장치 샘플 응용 프로그램에 대한 IoT Hub 및 논리적 장치 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="e1229-108">시뮬레이트된 장치 샘플 응용 프로그램을 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="e1229-109">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="e1229-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e1229-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="e1229-110">What you will learn</span></span>

<span data-ttu-id="e1229-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-111">In this article, you will learn:</span></span>

- <span data-ttu-id="e1229-112">시뮬레이트된 장치 샘플 응용 프로그램을 구성하고 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1229-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e1229-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e1229-113">What you need</span></span>

<span data-ttu-id="e1229-114">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-114">You must have successfully completed</span></span>

- [<span data-ttu-id="e1229-115">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="e1229-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="e1229-116">호스트 컴퓨터에 샘플 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="e1229-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="e1229-117">샘플 리포지토리를 복제하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="e1229-118">Windows에서 명령 프롬프트를 열거나 macOS 또는 Ubuntu에서 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="e1229-119">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="e1229-120">시뮬레이트된 장치 및 NUC 구성</span><span class="sxs-lookup"><span data-stu-id="e1229-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="e1229-121">다음 명령을 실행하여 Visual Studio Code에서 구성 파일인 `config.json` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="e1229-122">`"has_sensortag": true`을 `"has_sensortag": false`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![TI SensorTag 장치가 없는 구성](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="e1229-124">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="e1229-125">다음 명령을 실행하여 Visual Studio Code에서 `config-gateway.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="e1229-126">다음 코드 줄을 찾아 `[device hostname or IP address]`를 Intel NUC의 IP 주소 또는 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="e1229-127">![config gateway의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="e1229-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="e1229-128">IoT Hub 논리적 장치의 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="e1229-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="e1229-129">논리적 장치의 Azure IoT Hub 연결 문자열을 가져오려면 호스트 컴퓨터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="e1229-130">`{IoT hub name}`은 사용한 IoT Hub 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="e1229-131">단원 2에서 값을 변경하지 않았다면 iot-gateway를 `{resource group name}` 값으로 사용하고 mydevice를 `{device id}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="e1229-132">시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="e1229-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="e1229-133">시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램을 구성하고 실행하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="e1229-134">다음 명령을 실행하여 Visual Studio Code에서 `config-sensortag.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="e1229-136">코드에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="e1229-137">`[IoT hub name]`을 IoT Hub 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="e1229-138">`[IoT device connection string]`을 IoT Hub 논리적 장치의 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="e1229-139">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-139">Run the application.</span></span>

   <span data-ttu-id="e1229-140">다음 명령을 실행하여 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="e1229-141">샘플 응용 프로그램 작동 확인</span><span class="sxs-lookup"><span data-stu-id="e1229-141">Verify the sample application works</span></span>

<span data-ttu-id="e1229-142">이제 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-142">You should now see output like the following:</span></span>

![시뮬레이트된 장치 샘플 응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="e1229-144">응용 프로그램은 40초 동안 온도 데이터를 IoT Hub로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="e1229-145">요약</span><span class="sxs-lookup"><span data-stu-id="e1229-145">Summary</span></span>

<span data-ttu-id="e1229-146">시뮬레이트된 장치로 IoT Hub에 데이터를 보내는 시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램을 성공적으로 구성하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1229-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1229-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1229-147">Next steps</span></span>
[<span data-ttu-id="e1229-148">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="e1229-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)