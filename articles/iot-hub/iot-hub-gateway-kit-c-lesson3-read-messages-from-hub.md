---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 3: 메시지 읽기 | Microsoft Docs"
description: "IoT 허브에서 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 데이터 수집, iot 클라우드 서비스, iot 데이터의 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="7d376-104">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="7d376-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7d376-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="7d376-105">What you will do</span></span>

- <span data-ttu-id="7d376-106">샘플에서 코드를 실행할 호스트 컴퓨터 tooread 메시지 IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="7d376-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7d376-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="7d376-108">What you will learn</span></span>

<span data-ttu-id="7d376-109">어떻게 toouse hello gulp IoT 허브에서 도구 tooread 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7d376-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="7d376-110">What you need</span></span>

- <span data-ttu-id="7d376-111">hello 3 단원에서에서 성공적으로 실행 된 배포용 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="7d376-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d376-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="7d376-113">hello 장치 연결 문자열은 장치 (TI SensorTag 또는 시뮬레이션 된 장치) tooconnect tooyour IoT 허브에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="7d376-114">IoT 허브 연결 문자열 hello tooconnect tooyour IoT 허브는 사용할 수 있는 IoT 허브 toomanage hello 장치에 사용 되는 tooconnect toohello id 레지스트리에입니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="7d376-115">Hello 다음 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="7d376-116">사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7d376-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="7d376-117">Hello 다음 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="7d376-118">`{my hub name}`2 단원에서에서 지정한 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="7d376-119">Hello 샘플 코드에 대 한 hello 장치 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="7d376-120">Hello 장치 구성 파일 업데이트 `config-azure.json` 호스트 컴퓨터에서 IoT 허브에서 메시지를 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="7d376-121">toodo이를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="7d376-122">열기 `config-azure.json` hello 다음 콘솔 창에서 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="7d376-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="7d376-123">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-azure.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="7d376-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![config azure의 스크린 샷](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="7d376-125">대체 `[IoT hub connection string]` 가져온 IoT 허브 연결 문자열 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="7d376-126">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="7d376-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="7d376-127">TI SensorTag가 있는 경우 이미 SensorTag의 전원을 켜놓았어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="7d376-128">Hello 게이트웨이 샘플 응용 프로그램을 실행 하 고 다음 명령을 hello에서 IoT Hub 메시지를 읽을:</span><span class="sxs-lookup"><span data-stu-id="7d376-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="7d376-129">hello 명령은 읽고 SensorTag 또는 시뮬레이션 된 장치에서 온도 데이터를 패키지 하 고 hello 메시지 tooyour IoT hub 2 초 마다 전송 hello 배포용 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="7d376-130">또한 자식 프로세스 tooreceive hello 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="7d376-131">hello 메시지를 보내는 지 모든에 즉시 표시 hello 같은 콘솔 창에는 수신 호스트 컴퓨터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="7d376-132">hello 예제 응용 프로그램 인스턴스는 40 초 후에 자동으로 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![보낸 메시지와 수신한 메시지가 있는 BLE 샘플 응용 프로그램](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="7d376-134">요약</span><span class="sxs-lookup"><span data-stu-id="7d376-134">Summary</span></span>

<span data-ttu-id="7d376-135">IoT 허브에서 메시지는 샘플 코드 tooread를 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="7d376-136">준비 tooread hello 메시지 Azure 테이블 저장소에 저장 되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d376-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d376-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d376-137">Next steps</span></span>
[<span data-ttu-id="7d376-138">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="7d376-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


