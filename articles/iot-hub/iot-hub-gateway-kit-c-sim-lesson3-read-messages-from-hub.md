---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 3: 메시지 읽기 | Microsoft Docs"
description: "IoT 허브에서 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 데이터 수집, iot 클라우드 서비스, iot 데이터의 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="08f85-104">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="08f85-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="08f85-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="08f85-105">What you will do</span></span>

- <span data-ttu-id="08f85-106">샘플에서 코드를 실행할 호스트 컴퓨터 tooread 메시지 IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="08f85-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="08f85-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="08f85-108">What you will learn</span></span>

<span data-ttu-id="08f85-109">어떻게 toouse hello gulp IoT 허브에서 도구 tooread 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08f85-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="08f85-110">What you need</span></span>

- <span data-ttu-id="08f85-111">hello 시뮬레이션 된 장치 샘플에서 [구성 및 실행 하는 시뮬레이션 된 장치 클라우드 샘플 응용 프로그램 업로드](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="08f85-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="08f85-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="08f85-113">hello 장치 연결 문자열은 시뮬레이션 된 장치 tooconnect tooyour IoT 허브에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="08f85-114">IoT 허브 연결 문자열 hello tooconnect tooyour IoT 허브는 사용할 수 있는 IoT 허브 toomanage hello 장치에 사용 되는 tooconnect toohello id 레지스트리에입니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="08f85-115">Hello 다음 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="08f85-116">사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` 변경 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="08f85-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="08f85-117">Hello 다음 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="08f85-118">`{my hub name}`2 단원에서에서 지정한 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="08f85-119">Hello 샘플 코드에 대 한 hello 장치 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="08f85-120">IoT 허브와 장치 연결 구성을 업데이트 `config-azure.json` hello 다음 단계를 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="08f85-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="08f85-121">열기 `config-azure.json` hello 다음 콘솔 창에서 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="08f85-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="08f85-122">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-azure.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="08f85-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![config azure의 스크린 샷](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="08f85-124">대체 `[IoT hub connection string]` IoT 허브 연결 문자열 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="08f85-125">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="08f85-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="08f85-126">Hello 시뮬레이션 된 장치에 대 한 샘플 응용 프로그램을 실행 하 고 다음 명령을 hello에서 IoT Hub 메시지를 읽을:</span><span class="sxs-lookup"><span data-stu-id="08f85-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="08f85-127">hello 명령은 메시지 tooyour IoT hub 2 초 마다 전송 하는 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="08f85-128">또한 자식 프로세스 tooreceive hello 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="08f85-129">hello 메시지를 보내는 지 모든에 즉시 표시 hello 같은 콘솔 창에는 수신 호스트 컴퓨터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="08f85-130">hello 응용 프로그램에 40 초 후에 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-130">hello application will exit in 40 seconds.</span></span>

![보낸 메시지와 수신한 메시지가 있는 시뮬레이트된 샘플 응용 프로그램](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="08f85-132">요약</span><span class="sxs-lookup"><span data-stu-id="08f85-132">Summary</span></span>

<span data-ttu-id="08f85-133">성공적으로 시뮬레이션 된 장치와 hello 샘플 응용 프로그램 toosend 데이터 tooyour IoT 허브를 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="08f85-134">IoT hub tooyour 보낸 hello 메시지 읽은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f85-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08f85-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08f85-135">Next steps</span></span>
[<span data-ttu-id="08f85-136">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="08f85-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


