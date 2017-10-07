---
title: "연결 Intel Edison (노드) tooAzure IoT-3 단원: 메시지를 보낼 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooIntel Edison tooyour IoT hub 메시지를 보내고 hello led가 깜박이를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스 arduino toocloud 데이터 보내기"
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
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="31942-104">샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행</span><span class="sxs-lookup"><span data-stu-id="31942-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="31942-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="31942-105">What you will do</span></span>
<span data-ttu-id="31942-106">Toodeploy 및 전송 하는 Intel Edison에서 실행을 예제 응용 프로그램 메시지 tooyour IoT hub 방법을 표시이 문서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31942-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="31942-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="31942-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="31942-108">What you will learn</span></span>
<span data-ttu-id="31942-109">Toouse hello 도구 toodeploy gulp 하는 방법에 대해 알아봅니다 쿼리하고 Edison에 hello 샘플 C 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="31942-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="31942-110">What you need</span></span>
* <span data-ttu-id="31942-111">이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들][process-and-store-iot-hub-messages]합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="31942-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="31942-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="31942-113">hello 장치 연결 문자열은 사용한 tooconnect Edison tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="31942-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="31942-114">hello IoT 허브 연결 문자열은 사용한 tooconnect Edison hello IoT 허브를 표시 하 여 IoT 허브 toohello 장치 id입니다.</span><span class="sxs-lookup"><span data-stu-id="31942-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="31942-115">Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="31942-116">사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="31942-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="31942-117">Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="31942-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="31942-118">`{my hub name}`IoT hub를 생성 하 고 Edison 등록 지정한 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="31942-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="31942-119">Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="31942-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="31942-120">사용 하 여 `myinteledison` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="31942-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="31942-121">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="31942-121">Configure hello device connection</span></span>
1. <span data-ttu-id="31942-122">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="31942-123">장치 구성 파일 열기 hello `config-edison.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="31942-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="31942-125">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-edison.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="31942-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="31942-126">대체 **[장치 호스트 이름 또는 IP 주소]** hello 장치 IP 주소 장치를 구성 했을 때를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="31942-127">대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31942-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="31942-128">대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31942-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31942-129">이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31942-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="31942-130">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="31942-131">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="31942-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="31942-132">배포 및 실행 hello 샘플 응용 프로그램 Edison hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="31942-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="31942-133">Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="31942-133">Verify that hello sample application works</span></span>
<span data-ttu-id="31942-134">연결 된 tooEdison 2 초 마다 깜박입니다.이 hello LED 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="31942-135">Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="31942-136">또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31942-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="31942-137">샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="31942-139">요약</span><span class="sxs-lookup"><span data-stu-id="31942-139">Summary</span></span>
<span data-ttu-id="31942-140">배포 되었으며 toosend 장치-클라우드 메시지 tooyour IoT 허브에서 Edison hello 새 깜박임 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="31942-141">이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="31942-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31942-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31942-142">Next steps</span></span>
<span data-ttu-id="31942-143">[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="31942-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md