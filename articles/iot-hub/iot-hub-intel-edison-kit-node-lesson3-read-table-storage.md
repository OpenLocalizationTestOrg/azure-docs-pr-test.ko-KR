---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 3: 메시지 모니터링 | Microsoft Docs"
description: "장치-클라우드 메시지가 Azure Table Storage에 기록될 때 해당 메시지를 모니터링합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드의 데이터, 클라우드 데이터 컬렉션, IoT 클라우드 서비스, IoT 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c1a59227cd2bf9d2c9bcaa4212dd5127a95e2779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a4662-104">Azure Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="a4662-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a4662-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="a4662-105">What you will do</span></span>
<span data-ttu-id="a4662-106">Azure Table Storage에 메시지가 기록될 때 Intel Edison에서 IoT Hub로 전송되는 장치-클라우드 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="a4662-107">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="a4662-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a4662-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="a4662-108">What you will learn</span></span>
<span data-ttu-id="a4662-109">이 문서에서는 Gulp 메시지 읽기 작업을 사용하여 Azure Table Storage에 유지되는 메시지를 읽는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a4662-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="a4662-110">What you need</span></span>
<span data-ttu-id="a4662-111">이 과정을 시작하기 전에 [Intel Edison에서 Azure 깜빡이는 샘플 응용 프로그램 실행][run-the-azure-blink-sample-application-on-intel-edison]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a4662-112">저장소 계정에서 새 메시지 읽어오기</span><span class="sxs-lookup"><span data-stu-id="a4662-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a4662-113">이전 문서에서는 Edison에서 샘플 응용 프로그램을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="a4662-114">샘플 응용 프로그램은 Azure IoT Hub에 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="a4662-115">IoT Hub에 보낸 메시지는 Azure 함수 앱을 경유하여 Azure Table Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="a4662-116">Azure Table Storage에서 메시지를 읽어오려면 Azure Storage 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="a4662-117">Azure Table Storage에 저장된 메시지를 읽으려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a4662-118">다음 명령을 실행하여 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a4662-119">첫 번째 명령은 두 번째 명령에 사용되어 연결 문자열을 가져오는 `storage name`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="a4662-120">값을 변경하지 않았다면 `iot-sample`을 `{resource group name}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="a4662-121">다음 명령을 실행하여 Visual Studio Code에서 구성 파일인 `config-edison.json` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="a4662-122">`[Azure storage connection string]`을 1단계에서 가져온 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="a4662-123">`config-edison.json` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="a4662-124">다음 명령을 실행하여 메시지를 다시 보내고 Azure Table Storage에서 해당 메시지를 읽어옵니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="a4662-125">Azure Table Storage에서 읽어오는 논리는 `azure-table.js` 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="a4662-127">요약</span><span class="sxs-lookup"><span data-stu-id="a4662-127">Summary</span></span>
<span data-ttu-id="a4662-128">Edison을 클라우드의 IoT Hub에 성공적으로 연결했고 깜빡이는 샘플 응용 프로그램을 사용하여 장치-클라우드 메시지를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="a4662-129">또한, Azure 함수 앱을 사용하여 들어오는 IoT Hub 메시지를 Azure Table Storage에 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="a4662-130">이제 IoT Hub에서 Edison으로 클라우드-장치 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4662-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4662-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4662-131">Next steps</span></span>
<span data-ttu-id="a4662-132">[샘플 응용 프로그램을 실행하여 클라우드-장치 메시지 받기][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="a4662-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md