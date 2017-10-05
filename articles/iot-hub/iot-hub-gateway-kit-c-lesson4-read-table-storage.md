---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 4: 테이블 저장소 | Microsoft Docs"
description: "Intel NUC의 메시지를 IoT Hub에 저장하고 Azure Table Storage에 기록한 다음 클라우드에서 읽습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드에서 데이터 검색, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="65e40-104">Azure Table Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="65e40-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="65e40-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="65e40-105">What you will do</span></span>

- <span data-ttu-id="65e40-106">IoT Hub에 메시지를 보내는 게이트웨이에서 게이트웨이 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="65e40-107">그런 다음 호스트 컴퓨터에서 샘플 코드를 실행하여 Azure Table Storage의 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span></span> 

<span data-ttu-id="65e40-108">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="65e40-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="65e40-109">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="65e40-109">What you will learn</span></span>

<span data-ttu-id="65e40-110">Gulp 도구로 샘플 코드를 실행하여 Azure Table Storage의 메시지를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="65e40-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="65e40-111">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="65e40-111">What you need</span></span>

<span data-ttu-id="65e40-112">다음 작업을 성공적으로 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="65e40-113">[Azure 함수 앱 및 Azure Storage 계정 만들기](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="65e40-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="65e40-114">[게이트웨이 샘플 응용 프로그램 실행](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="65e40-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="65e40-115">[IoT Hub에서 메시지 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="65e40-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="65e40-116">Azure Storage 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="65e40-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="65e40-117">이 단원의 초반부에 Azure Storage 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="65e40-118">Azure Storage 계정의 연결 문자열을 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="65e40-119">모든 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="65e40-120">Azure Storage 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="65e40-121">단원 2에서 값을 변경하지 않았다면 `{resource group name}` 값으로 iot-gateway를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="65e40-122">장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="65e40-122">Configure the device connection</span></span>

<span data-ttu-id="65e40-123">호스트 컴퓨터에서 실행되는 샘플 코드가 Azure Table Storage의 메시지를 읽을 수 있도록 `config-azure.json` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="65e40-124">장치 연결을 구성하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="65e40-125">다음 명령을 실행하여 장치 구성 파일 `config-azure.json`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![구성](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="65e40-127">`[Azure storage connection string]`을 가져온 Azure Storage 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="65e40-128">`[IoT hub connection string]`은 3단원의 [Azure IoT Hub에서 메시기 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) 섹션에서 이미 바꿨어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="65e40-129">Azure Table Storage에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="65e40-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="65e40-130">게이트웨이 샘플 응용 프로그램을 실행하고 다음 명령으로 Azure Table Storage 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="65e40-131">새 메시지가 도착하면 IoT Hub가 Azure 함수 응용 프로그램을 트리거하여 Azure Table Storage에 메시지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="65e40-132">`gulp run` 명령은 IoT Hub에 메시지를 보내는 게이트웨이 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="65e40-133">`table-storage` 매개 변수를 사용하면 Azure Table Storage에 저장된 메시지를 수신할 하위 프로세스도 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="65e40-134">보내고 받는 메시지는 모두 호스트 시스템의 동일한 콘솔 창에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="65e40-135">샘플 응용 프로그램 인스턴스는 40초 후 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp 읽기](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="65e40-137">요약</span><span class="sxs-lookup"><span data-stu-id="65e40-137">Summary</span></span>

<span data-ttu-id="65e40-138">샘플 코드를 실행하여 Azure 함수 응용 프로그램에서 저장한 Azure Table Storage의 메시지를 읽었습니다.</span><span class="sxs-lookup"><span data-stu-id="65e40-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>