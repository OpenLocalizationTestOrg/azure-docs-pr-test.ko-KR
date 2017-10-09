---
title: "Connect Raspberry Pi (C) tooAzure IoT-3 단원: 샘플을 실행 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooRaspberry tooyour IoT hub 메시지를 보내고 hello led가 깜박이 Pi 3을 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "깜박임 LED 클라우드 Pi, 클라우드에서 LED 깜빡이기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="03aca-104">샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행</span><span class="sxs-lookup"><span data-stu-id="03aca-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="03aca-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="03aca-105">What you will do</span></span>
<span data-ttu-id="03aca-106">Toodeploy 및 보내는 라스베리 Pi 3에서 실행을 예제 응용 프로그램 메시지 tooyour IoT hub 방법을 표시이 문서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="03aca-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="03aca-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="03aca-108">What you will learn</span></span>
<span data-ttu-id="03aca-109">하면 toouse hello 도구 toodeploy gulp 하 고 원주율 hello 샘플 Node.js 응용 프로그램을 실행 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="03aca-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="03aca-110">What you need</span></span>
* <span data-ttu-id="03aca-111">이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="03aca-112">IoT Hub 및 장치 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="03aca-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="03aca-113">장치 연결 문자열 hello Pi tooconnect tooyour IoT 허브에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="03aca-114">IoT 허브 연결 문자열 hello tooconnect tooyour IoT 허브는 사용할 수 있는 IoT 허브 toomanage hello 장치에 사용 되는 tooconnect toohello id 레지스트리에입니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="03aca-115">Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="03aca-116">사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="03aca-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="03aca-117">Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="03aca-118">`{my hub name}`IoT hub를 생성 하 고 Pi 등록 지정한 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="03aca-119">Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="03aca-120">사용 하 여 `myraspberrypi` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="03aca-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="03aca-121">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="03aca-121">Configure hello device connection</span></span>
1. <span data-ttu-id="03aca-122">Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="03aca-123">단원 1에서 **gulp install-tools**를 실행하지 않았다면 이 명령도 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="03aca-124">장치 구성 파일 열기 hello `config-raspberrypi.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="03aca-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="03aca-126">Hello 바꾸기 작업을 수행 하는 hello 확인 `config-raspberrypi.json` 파일:</span><span class="sxs-lookup"><span data-stu-id="03aca-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="03aca-127">대체 **[장치 호스트 이름 또는 IP 주소]** 에서 가져온 hello 장치 IP 주소 또는 호스트 이름으로 `device-discovery-cli` 또는 장치를 구성할 때 상속 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="03aca-128">대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="03aca-129">대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="03aca-130">이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="03aca-131">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-131">Keep it as is.</span></span>

<span data-ttu-id="03aca-132">업데이트 hello `config-raspberrypi.json` hello 샘플 응용 프로그램에서 컴퓨터를 배포할 수 있도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="03aca-133">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="03aca-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="03aca-134">배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="03aca-135">Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="03aca-135">Verify that hello sample application works</span></span>
<span data-ttu-id="03aca-136">연결 된 tooPi 2 초 마다 깜박입니다.이 hello LED 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="03aca-137">Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="03aca-138">또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="03aca-139">샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="03aca-141">요약</span><span class="sxs-lookup"><span data-stu-id="03aca-141">Summary</span></span>
<span data-ttu-id="03aca-142">배포 되었으며 Pi toosend 장치-클라우드 메시지 tooyour IoT 허브에서 hello 새 깜박임 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="03aca-143">이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="03aca-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03aca-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03aca-144">Next steps</span></span>
[<span data-ttu-id="03aca-145">Azure Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="03aca-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

