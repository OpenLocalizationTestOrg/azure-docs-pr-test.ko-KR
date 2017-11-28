---
featureFlags: usabilla
title: "연결 라스베리 Pi (노드) tooAzure IoT-3 단원: 테이블 저장소 | Microsoft Docs"
description: "Tooyour Azure 테이블 저장소에 작성 된 것 처럼 hello 장치-클라우드 메시지를 모니터링 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드에서 데이터 검색, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="fe5c7-104">Azure Storage에 유지되는 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="fe5c7-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fe5c7-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="fe5c7-105">What you will do</span></span>
<span data-ttu-id="fe5c7-106">Hello 메시지로 라스베리 Pi 3 tooyour IoT 허브에서 보낸 모니터 hello 장치-클라우드 메시지 tooyour Azure 테이블 저장소에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="fe5c7-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fe5c7-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="fe5c7-108">What you will learn</span></span>
<span data-ttu-id="fe5c7-109">이 문서에서는 Azure 테이블 저장소에 toouse hello gulp 메시지 읽기 작업 tooread 메시지 유지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fe5c7-110">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="fe5c7-110">What you need</span></span>
<span data-ttu-id="fe5c7-111">이 프로세스를 시작 하기 전에 성공적으로 완료 해야 [라스베리 Pi 3에서 hello Azure 깜박임 샘플 응용 프로그램을 실행](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="fe5c7-112">저장소 계정에서 새 메시지 읽어오기</span><span class="sxs-lookup"><span data-stu-id="fe5c7-112">Read new messages from your storage account</span></span>
<span data-ttu-id="fe5c7-113">Hello 이전 문서 원주율 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="fe5c7-114">hello 샘플 응용 프로그램 메시지 tooyour Azure IoT 허브를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="fe5c7-115">tooyour IoT hub를 전송 하는 hello 메시지 hello Azure 함수 앱을 통해 Azure 테이블 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="fe5c7-116">Azure 테이블 저장소에서 hello Azure 저장소 연결 문자열 tooread 메시지 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="fe5c7-117">Azure 테이블 저장소에 저장 된 tooread 메시지는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="fe5c7-118">Hello 다음 명령을 실행 하 여 hello 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="fe5c7-119">hello 첫 번째 명령은 검색 hello `storage name` hello 두 번째 명령은 tooget hello 연결 문자열에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="fe5c7-120">사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="fe5c7-121">구성 파일 열기 hello `config-raspberrypi.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:</span><span class="sxs-lookup"><span data-stu-id="fe5c7-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="fe5c7-122">대체 `[Azure storage connection string]` 1 단계에서 가져온 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="fe5c7-123">Hello 저장 `config-raspberrypi.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="fe5c7-124">메시지를 다시 보내고 hello 다음 명령을 실행 하 여 Azure 테이블 저장소에서 읽기:</span><span class="sxs-lookup"><span data-stu-id="fe5c7-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="fe5c7-125">hello Azure 테이블 저장소에서 읽기에 대 한 논리는 hello `azure-table.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
    ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="fe5c7-127">요약</span><span class="sxs-lookup"><span data-stu-id="fe5c7-127">Summary</span></span>
<span data-ttu-id="fe5c7-128">성공적으로 hello 클라우드에서 Pi tooyour IoT 허브를 연결 하 고 hello 깜박임 샘플 응용 프로그램 toosend 장치-클라우드 메시지를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="fe5c7-129">또한 hello Azure 함수 앱 toostore 들어오는 IoT 허브 메시지 tooyour Azure 테이블 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="fe5c7-130">이제 IoT 허브 tooPi에서 클라우드-장치 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe5c7-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe5c7-131">Next steps</span></span>
[<span data-ttu-id="fe5c7-132">Hello 샘플 응용 프로그램 tooreceive 클라우드-장치 메시지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe5c7-132">Run hello sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

