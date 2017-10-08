---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 3: 샘플 앱 실행 | Microsoft Docs"
description: "시뮬레이션 된 장치 샘플 앱 toosend 온도 데이터 tooyour IoT 허브를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "데이터 toocloud"
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="d41ba-104">시뮬레이트된 장치 샘플 앱 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="d41ba-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d41ba-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="d41ba-105">What you will do</span></span>

- <span data-ttu-id="d41ba-106">Hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="d41ba-107">시뮬레이션 된 장치 샘플 응용 프로그램에 대 한 hello Azure CLI tooget IoT hub 및 논리적 장치 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="d41ba-108">구성 하 고 hello 시뮬레이션 된 장치에 대 한 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="d41ba-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d41ba-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="d41ba-110">What you will learn</span></span>

<span data-ttu-id="d41ba-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-111">In this article, you will learn:</span></span>

- <span data-ttu-id="d41ba-112">어떻게 tooconfigure와 실행된 hello 장치 샘플 응용 프로그램을 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d41ba-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="d41ba-113">What you need</span></span>

<span data-ttu-id="d41ba-114">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-114">You must have successfully completed</span></span>

- [<span data-ttu-id="d41ba-115">IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="d41ba-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="d41ba-116">Hello 샘플 리포지토리 toohello 호스트 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="d41ba-117">tooclone hello 샘플 리포지토리 hello 호스트 컴퓨터에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="d41ba-118">Windows에서 명령 프롬프트를 열거나 macOS 또는 Ubuntu에서 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="d41ba-119">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="d41ba-120">Hello 시뮬레이션 된 장치 및 사용자 NUC 구성</span><span class="sxs-lookup"><span data-stu-id="d41ba-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="d41ba-121">구성 파일 열기 hello `config.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="d41ba-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="d41ba-122">`"has_sensortag": true`을 `"has_sensortag": false`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![TI SensorTag 장치가 없는 구성](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="d41ba-124">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="d41ba-125">열기 `config-gateway.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="d41ba-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="d41ba-126">다음 코드 줄을 hello 찾기 및 바꾸기 `[device hostname or IP address]` hello Intel NUC의 IP 주소 또는 호스트 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="d41ba-127">![config gateway의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="d41ba-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="d41ba-128">IoT 허브 논리적 장치의 hello 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="d41ba-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="d41ba-129">tooget hello hello 다음 hello 호스트 컴퓨터에서 명령을 실행 하 여 논리적 장치의 Azure IoT 허브 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="d41ba-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="d41ba-130">`{IoT hub name}`사용한 hello IoT 허브 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="d41ba-131">Iot 게이트웨이 사용 하 여의 hello 값으로 `{resource group name}` mydevice의 hello 값으로 사용 하 여 `{device id}` hello 값 2 단원에서에서 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="d41ba-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="d41ba-132">시뮬레이션 된 hello 장치 클라우드 업로드 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="d41ba-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="d41ba-133">샘플 응용 프로그램 업로드 tooconfigure 및 시뮬레이션 실행된 hello 장치 클라우드 hello 호스트 컴퓨터에서 다음이 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d41ba-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="d41ba-134">열기 `config-sensortag.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="d41ba-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag의 스크린샷](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="d41ba-136">Hello 대체 hello 코드에서 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="d41ba-137">대체 `[IoT hub name]` hello IoT 허브 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="d41ba-138">대체 `[IoT device connection string]` IoT 허브 논리적 장치의 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="d41ba-139">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-139">Run hello application.</span></span>

   <span data-ttu-id="d41ba-140">배포 하 고 hello 다음 명령을 실행 하 여 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="d41ba-141">Hello 샘플 응용 프로그램 작동 확인</span><span class="sxs-lookup"><span data-stu-id="d41ba-141">Verify hello sample application works</span></span>

<span data-ttu-id="d41ba-142">이제 hello 다음과 같은 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-142">You should now see output like hello following:</span></span>

![시뮬레이트된 장치 샘플 응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="d41ba-144">hello 응용 프로그램에 40 초 동안 지속 되는 온도 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="d41ba-145">요약</span><span class="sxs-lookup"><span data-stu-id="d41ba-145">Summary</span></span>

<span data-ttu-id="d41ba-146">성공적으로 구성 했는데 실행된 hello 장치 클라우드 업로드 샘플 응용 프로그램 데이터 tooyour IoT 허브 시뮬레이션 된 장치에 전송 하는 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41ba-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d41ba-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d41ba-147">Next steps</span></span>
[<span data-ttu-id="d41ba-148">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="d41ba-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)