---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 3: 메시지 읽기 | Microsoft Docs"
description: "IoT Hub에서 메시지를 읽으려면 호스트 컴퓨터에서 샘플 코드를 실행합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드의 데이터, 클라우드 데이터 수집, iot 클라우드 서비스, iot 데이터"
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5c03b-104">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="5c03b-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5c03b-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="5c03b-105">What you will do</span></span>

- <span data-ttu-id="5c03b-106">IoT Hub에서 메시지를 읽으려면 호스트 컴퓨터에서 샘플 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="5c03b-107">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="5c03b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5c03b-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="5c03b-108">What you will learn</span></span>

<span data-ttu-id="5c03b-109">Gulp 도구를 사용하여 IoT Hub에서 메시지를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="5c03b-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5c03b-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="5c03b-110">What you need</span></span>

- <span data-ttu-id="5c03b-111">[시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램 구성 및 실행](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)의 시뮬레이트된 장치 샘플</span><span class="sxs-lookup"><span data-stu-id="5c03b-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="5c03b-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="5c03b-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="5c03b-113">장치 연결 문자열은 시뮬레이트된 장치를 IoT Hub에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="5c03b-114">IoT Hub 연결 문자열은 IoT Hub에 연결할 수 있는 장치를 관리하기 위해 IoT Hub의 ID 레지스트리에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="5c03b-115">다음 명령을 실행하여 리소스 그룹에 있는 모든 IoT Hub를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="5c03b-116">변경하지 않았다면 `iot-gateway`을 `{resource group name}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="5c03b-117">다음 명령을 실행하여 IoT Hub 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="5c03b-118">`{my hub name}`은 단원 2에서 지정했던 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="5c03b-119">샘플 코드에 대한 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="5c03b-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="5c03b-120">다음 단계를 수행 `config-azure.json`에 있는 IoT hub 및 장치 연결 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="5c03b-121">콘솔 창에서 다음 명령을 실행하여 Visual Studio 코드에서 `config-azure.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="5c03b-122">`config-azure.json` 파일에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![config azure의 스크린 샷](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="5c03b-124">`[IoT hub connection string]`을 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5c03b-125">IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="5c03b-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="5c03b-126">시뮬레이트된 장치 샘플 응용 프로그램을 실행하고 다음 명령으로 IoT Hub 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="5c03b-127">명령은 2초마다 IoT 허브로 메시지를 보내는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="5c03b-128">또한 메시지를 수신할 하위 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="5c03b-129">보내고 받는 메시지는 모두 호스트 시스템의 동일한 콘솔 창에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="5c03b-130">응용 프로그램은 40초에서 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-130">The application will exit in 40 seconds.</span></span>

![보낸 메시지와 수신한 메시지가 있는 시뮬레이트된 샘플 응용 프로그램](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="5c03b-132">요약</span><span class="sxs-lookup"><span data-stu-id="5c03b-132">Summary</span></span>

<span data-ttu-id="5c03b-133">시뮬레이트된 장치를 사용하여 IoT Hub에 데이터를 보내는 샘플 응용 프로그램을 성공적으로 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="5c03b-134">IoT Hub에 보낸 메시지도 읽었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c03b-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c03b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c03b-135">Next steps</span></span>
[<span data-ttu-id="5c03b-136">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="5c03b-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


