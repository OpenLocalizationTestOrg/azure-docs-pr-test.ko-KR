---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 3: 메시지 전송 | Microsoft Docs"
description: "IoT Hub에 메시지를 보내고 LED를 깜빡이는 샘플 응용 프로그램을 Intel Edison에 배포하고 실행합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스, arduino 클라우드, arduino 클라우드에 데이터 전송"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="1c382-104">샘플 응용 프로그램을 실행하여 장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="1c382-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1c382-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="1c382-105">What you will do</span></span>
<span data-ttu-id="1c382-106">이 문서는 IoT Hub에 메시지를 보내는 샘플 응용 프로그램을 Intel Edison에 배포하고 실행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="1c382-107">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="1c382-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1c382-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="1c382-108">What you will learn</span></span>
<span data-ttu-id="1c382-109">Gulp 도구를 사용하여 Edison에서 샘플 C 응용 프로그램을 배포하고 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1c382-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="1c382-110">What you need</span></span>
* <span data-ttu-id="1c382-111">이 작업을 시작하기 전에 [IoT Hub 메시지를 처리하고 저장하기 위해 Azure 함수 앱 및 저장소 계정 만들기][process-and-store-iot-hub-messages]를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="1c382-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="1c382-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="1c382-113">장치 연결 문자열은 Edison을 IoT Hub에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="1c382-114">IoT Hub 연결 문자열은 IoT Hub를 장치 ID에 연결하는 데 사용됩니다. 이 ID는 IoT Hub에서 Edison을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="1c382-115">다음 Azure CLI 명령을 실행하여 리소스 그룹에 있는 모든 IoT Hub를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="1c382-116">값을 변경하지 않았다면 `iot-sample`을 `{resource group name}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="1c382-117">다음 Azure CLI 명령을 실행하여 IoT Hub 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="1c382-118">`{my hub name}`은 IoT Hub를 만들고 Edison을 등록할 때 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="1c382-119">다음 명령을 실행하여 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="1c382-120">값을 변경하지 않았다면 `myinteledison`을 `{device id}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="1c382-121">장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1c382-121">Configure the device connection</span></span>
1. <span data-ttu-id="1c382-122">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="1c382-123">다음 명령을 실행하여 Visual Studio Code에서 장치 구성 파일 `config-edison.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="1c382-125">`config-edison.json` 파일에서 다음 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="1c382-126">**[device hostname or IP address]**를 장치를 구성할 때 표시한 장치 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="1c382-127">**[IoT device connection string]**을 가져온 `device connection string`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="1c382-128">**[IoT hub connection string]**을 가져온 `iot hub connection string`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c382-129">이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="1c382-130">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1c382-131">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="1c382-131">Deploy and run the sample application</span></span>
<span data-ttu-id="1c382-132">다음 명령을 실행하여 Edison에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="1c382-133">샘플 응용 프로그램 작동 확인</span><span class="sxs-lookup"><span data-stu-id="1c382-133">Verify that the sample application works</span></span>
<span data-ttu-id="1c382-134">Edison에 연결된 LED가 2초마다 깜빡이는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="1c382-135">LED가 깜빡일 때마다 샘플 응용 프로그램은 IoT Hub에 메시지를 전송하고 해당 메시지가 IoT Hub에 성공적으로 전송되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="1c382-136">또한 IoT Hub가 수신한 각 메시지가 콘솔 창에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="1c382-137">샘플 응용 프로그램은 메시지를 20개 보낸 후에 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-137">The sample application terminates automatically after sending 20 messages.</span></span>

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="1c382-139">요약</span><span class="sxs-lookup"><span data-stu-id="1c382-139">Summary</span></span>
<span data-ttu-id="1c382-140">Edison에서 깜빡이는 샘플 응용 프로그램을 새로 배포하고 실행하여 IoT Hub에 장치-클라우드 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="1c382-141">이제 저장소 계정에 메시지가 작성될 때 해당 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="1c382-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c382-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c382-142">Next steps</span></span>
<span data-ttu-id="1c382-143">[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="1c382-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md