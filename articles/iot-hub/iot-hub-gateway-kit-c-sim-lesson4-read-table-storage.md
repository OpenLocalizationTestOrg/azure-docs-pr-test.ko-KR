---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 4: 테이블 저장소 | Microsoft Docs"
description: "Intel NUC tooyour IoT 허브에서 메시지를 저장 하 고 tooAzure 테이블 저장소에 쓰는 hello 클라우드에서 읽어 주시기 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드에서 데이터 검색, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="829fe-104">Azure Table Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="829fe-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="829fe-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="829fe-105">What you will do</span></span>

- <span data-ttu-id="829fe-106">보내는 메시지 tooyour IoT hub 게이트웨이에 hello 게이트웨이 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="829fe-107">Azure 테이블 저장소에 호스트 컴퓨터 tooread 메시지에서 예제 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-107">Run sample code on your host computer tooread messages in your Azure Table storage.</span></span>

<span data-ttu-id="829fe-108">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="829fe-109">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="829fe-109">What you will learn</span></span>

<span data-ttu-id="829fe-110">어떻게 toouse hello gulp Azure 테이블 저장소 도구 toorun hello 샘플 코드 tooread 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="829fe-111">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="829fe-111">What you need</span></span>

<span data-ttu-id="829fe-112">성공적으로 포함 해야 다음 작업 hello 수행:</span><span class="sxs-lookup"><span data-stu-id="829fe-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="829fe-113">[Hello Azure 함수 앱 및 hello Azure 저장소 계정을 만든](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="829fe-114">[Hello 게이트웨이 샘플 응용 프로그램 실행](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="829fe-115">[IoT Hub에서 메시지 읽기](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="829fe-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="829fe-116">Azure Storage 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="829fe-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="829fe-117">이 단원의 초반부에 Azure Storage 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="829fe-118">실행할 명령을 수행 하는 hello hello Azure 저장소 계정의 tooget hello 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="829fe-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="829fe-119">모든 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="829fe-120">Azure Storage 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="829fe-121">사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` hello 값 2 단원에서에서 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="829fe-121">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="829fe-122">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="829fe-122">Configure hello device connection</span></span>

<span data-ttu-id="829fe-123">업데이트 hello `config-azure.json` hello 호스트 컴퓨터에서 실행 되는 hello 샘플 코드는 Azure 테이블 저장소에 메시지를 읽을 수 있도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="829fe-124">tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="829fe-125">장치 구성 파일 열기 hello `config-azure.json` hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="829fe-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![구성](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="829fe-127">대체 `[Azure storage connection string]` 가져온 Azure 저장소 연결 문자열 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="829fe-128">`[IoT hub connection string]`은 3단원의 [Azure IoT Hub에서 메시기 읽기](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) 섹션에서 이미 바꿨어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="829fe-129">Azure Table Storage에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="829fe-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="829fe-130">Hello 게이트웨이 샘플 응용 프로그램을 실행 하 고 다음 명령을 hello 하 여 Azure 테이블 저장소 메시지 읽기:</span><span class="sxs-lookup"><span data-stu-id="829fe-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="829fe-131">IoT hub 새 메시지가 도착 하는 경우 Azure 테이블 저장소에 Azure 함수 응용 프로그램 toosave 메시지를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="829fe-132">hello `gulp run` 명령은 메시지 tooyour IoT 허브에서 전송 하는 게이트웨이 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="829fe-133">와 `table-storage` 매개 변수에 생성 Azure 테이블 저장소에 메시지를 저장 하는 자식 프로세스 tooreceive hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="829fe-134">hello 메시지를 보내는 지 모든에 즉시 표시 hello 같은 콘솔 창에는 수신 호스트 컴퓨터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="829fe-135">hello 예제 응용 프로그램 인스턴스는 40 초 후에 자동으로 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp 읽기](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="829fe-137">요약</span><span class="sxs-lookup"><span data-stu-id="829fe-137">Summary</span></span>

<span data-ttu-id="829fe-138">Azure 함수 응용 프로그램에서 저장 된 Azure 테이블 저장소에 hello 샘플 코드 tooread hello 메시지를 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="829fe-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
