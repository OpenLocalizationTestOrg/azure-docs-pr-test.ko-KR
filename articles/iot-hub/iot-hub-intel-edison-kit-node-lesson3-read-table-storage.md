---
title: "연결 Intel Edison (노드) tooAzure IoT-3 단원: 메시지도 모니터링 | Microsoft Docs"
description: "Tooyour Azure 테이블 저장소에 작성 된 것 처럼 hello 장치-클라우드 메시지를 모니터링 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 데이터 수집, iot 클라우드 서비스, iot 데이터의 데이터"
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
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="e9b96-104">Azure Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="e9b96-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e9b96-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="e9b96-105">What you will do</span></span>
<span data-ttu-id="e9b96-106">Hello 메시지로 Intel Edison tooyour IoT 허브에서 보낸 모니터 hello 장치-클라우드 메시지 tooyour Azure 테이블 저장소에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-106">Monitor hello device-to-cloud messages that are sent from Intel Edison tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="e9b96-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e9b96-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="e9b96-108">What you will learn</span></span>
<span data-ttu-id="e9b96-109">이 문서에서는 Azure 테이블 저장소에 toouse hello gulp 메시지 읽기 작업 tooread 메시지 유지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9b96-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e9b96-110">What you need</span></span>
<span data-ttu-id="e9b96-111">이 프로세스를 시작 하기 전에 성공적으로 완료 해야 [Intel Edison에 hello Azure 깜박임 샘플 응용 프로그램을 실행][run-the-azure-blink-sample-application-on-intel-edison]합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="e9b96-112">저장소 계정에서 새 메시지 읽어오기</span><span class="sxs-lookup"><span data-stu-id="e9b96-112">Read new messages from your storage account</span></span>
<span data-ttu-id="e9b96-113">Hello 이전 문서 Edison에 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-113">In hello previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="e9b96-114">hello 샘플 응용 프로그램 메시지 tooyour Azure IoT 허브를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="e9b96-115">tooyour IoT hub를 전송 하는 hello 메시지 hello Azure 함수 앱을 통해 Azure 테이블 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="e9b96-116">Azure 테이블 저장소에서 hello Azure 저장소 연결 문자열 tooread 메시지 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="e9b96-117">Azure 테이블 저장소에 저장 된 tooread 메시지는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e9b96-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="e9b96-118">Hello 다음 명령을 실행 하 여 hello 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="e9b96-119">hello 첫 번째 명령은 검색 hello `storage name` hello 두 번째 명령은 tooget hello 연결 문자열에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="e9b96-120">사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="e9b96-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="e9b96-121">구성 파일 열기 hello `config-edison.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="e9b96-121">Open hello configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="e9b96-122">대체 `[Azure storage connection string]` 1 단계에서 가져온 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="e9b96-123">Hello 저장 `config-edison.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-123">Save hello `config-edison.json` file.</span></span>
5. <span data-ttu-id="e9b96-124">메시지를 다시 보내고 hello 다음 명령을 실행 하 여 Azure 테이블 저장소에서 읽기:</span><span class="sxs-lookup"><span data-stu-id="e9b96-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="e9b96-125">hello Azure 테이블 저장소에서 읽기에 대 한 논리는 hello `azure-table.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="e9b96-127">요약</span><span class="sxs-lookup"><span data-stu-id="e9b96-127">Summary</span></span>
<span data-ttu-id="e9b96-128">성공적으로 hello 클라우드에서 Edison tooyour IoT 허브를 연결 하 고 hello 깜박임 샘플 응용 프로그램 toosend 장치-클라우드 메시지를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-128">You've successfully connected Edison tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="e9b96-129">또한 hello Azure 함수 앱 toostore 들어오는 IoT 허브 메시지 tooyour Azure 테이블 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="e9b96-130">이제 IoT 허브 tooEdison에서 클라우드-장치 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b96-130">You can now send cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9b96-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9b96-131">Next steps</span></span>
<span data-ttu-id="e9b96-132">[클라우드-장치 메시지 샘플 응용 프로그램 tooreceive 실행][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="e9b96-132">[Run a sample application tooreceive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md