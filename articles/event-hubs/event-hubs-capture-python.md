---
title: "Azure Event Hubs 캡처 연습 | Microsoft Docs"
description: "Azure Python SDK를 통해 Event Hubs 캡처 기능을 사용하는 방법을 보여 주는 샘플입니다."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="079b2-103">Event Hubs 캡처 연습: Python</span><span class="sxs-lookup"><span data-stu-id="079b2-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="079b2-104">Event Hubs 캡처는 이벤트 허브의 스트리밍 데이터를 선택한 Azure Blob Storage 계정에 자동으로 전달할 수 있게 해주는 Event Hubs의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="079b2-105">이 기능을 통해 손쉽게 실시간 스트리밍 데이터에 대한 일괄 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="079b2-106">이 문서에서는 Python과 함께 Event Hubs 캡처를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="079b2-107">Event Hubs 캡처에 대한 자세한 내용은 [개요 문서](event-hubs-archive-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="079b2-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="079b2-108">이 샘플에서는 [Azure Python SDK](https://azure.microsoft.com/develop/python/)를 사용하여 캡처 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="079b2-109">sender.py 프로그램이 JSON 형식으로 Event Hubs에 시뮬레이트된 환경 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="079b2-110">이벤트 허브는 캡처 기능을 사용하여 이 데이터를 Blob Storage에 일괄적으로 쓰도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="079b2-111">그런 다음 capturereader.py 앱이 이러한 Blob을 읽고 장치당 추가 파일을 만들어 .csv 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="079b2-112">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="079b2-112">What will be accomplished</span></span>

1. <span data-ttu-id="079b2-113">Azure Portal을 사용하여 Azure Blob Storage 계정 및 Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="079b2-114">Azure Portal을 사용하여 이벤트 허브 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="079b2-115">Azure Portal을 사용하여 캡처 기능이 활성화된 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="079b2-116">Python 스크립트를 사용하여 이벤트 허브에 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="079b2-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="079b2-117">다른 Python 스크립트로 캡처에서 파일 읽기 및 처리</span><span class="sxs-lookup"><span data-stu-id="079b2-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="079b2-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="079b2-118">Prerequisites</span></span>

- <span data-ttu-id="079b2-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="079b2-119">Python 2.7.x</span></span>
- <span data-ttu-id="079b2-120">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="079b2-120">An Azure subscription</span></span>
- <span data-ttu-id="079b2-121">활성 [Event Hubs 네임스페이스 및 이벤트 허브](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="079b2-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="079b2-122">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="079b2-123">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="079b2-124">포털의 왼쪽 탐색 창에서 **새로 만들기**, **저장소**, **저장소 계정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="079b2-125">저장소 계정 블레이드에서 필드를 완성한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="079b2-126">**배포 성공** 메시지가 나타나면 새 저장소 계정의 이름을 클릭하고 **Essentials** 블레이드에서 **Blob**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="079b2-127">**Blob service** 블레이드가 열리면 맨 위의 **+ 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="079b2-128">컨테이너 이름을 **capture**로 지정한 다음 **Blob service** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="079b2-129">왼쪽 블레이드에서 **선택키** 를 클릭하고 저장소 계정 이름과 **key1** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="079b2-130">메모장이나 기타 다른 위치에 임시로 이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="079b2-131">이벤트 허브로 이벤트를 보내는 Python 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="079b2-132">선호하는 Python 편집기(예: [Visual Studio Code][Visual Studio Code])를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="079b2-133">**sender.py**라는 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="079b2-134">이 스크립트는 이벤트 허브에 200개의 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="079b2-135">이 이벤트는 JSON 형식으로 전송한 간단한 환경 판독값입니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="079b2-136">다음 코드를 sender.py에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-136">Paste the following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="079b2-137">Event Hubs 네임스페이스를 만들 때 얻은 네임스페이스 이름, 키 값 및 이벤트 허브 이름을 사용하도록 앞의 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="079b2-138">캡처 파일을 읽는 Python 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="079b2-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="079b2-139">블레이드를 채우고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="079b2-140">**capturereader.py**라는 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="079b2-141">이 스크립트는 캡처된 파일을 읽고 장치마다 파일을 만들어 해당 장치에 대한 데이터만 씁니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="079b2-142">capturereader.py에 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-142">Paste the following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="079b2-143">호출의 저장소 계정 이름 및 키의 적절한 값을 `startProcessing`에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="079b2-144">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="079b2-144">Run the scripts</span></span>
1. <span data-ttu-id="079b2-145">해당 경로에 Python을 포함하는 명령 프롬프트를 열고 다음 명령을 실행하여 Python 필수 구성 요소 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="079b2-146">이전 버전의 Azure Storage나 Azure가 있는 경우 **--upgrade** 옵션을 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="079b2-147">또한 다음을 실행해야 할 수도 있습니다(대부분의 시스템에는 필요 없음).</span><span class="sxs-lookup"><span data-stu-id="079b2-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="079b2-148">sender.py 및 capturereader.py를 저장한 디렉터리로 변경하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="079b2-149">이 명령은 발신자를 실행하는 새 Python 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="079b2-150">이제 몇 분 정도 기다리면 캡처가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="079b2-151">그런 다음 원래 명령 창에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="079b2-152">이 캡처 프로세서는 로컬 디렉터리를 사용하여 저장소 계정/컨테이너에서 모든 Blob을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="079b2-153">비어 있지 않은 모든 Blob을 처리하고 로컬 디렉터리에 .csv 파일로 결과를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="079b2-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="079b2-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="079b2-154">Next steps</span></span>

<span data-ttu-id="079b2-155">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="079b2-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="079b2-156">[Event Hubs 캡처 개요][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="079b2-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="079b2-157">[Event Hubs를 사용하는 응용 프로그램 예제][sample application that uses Event Hubs] 전체.</span><span class="sxs-lookup"><span data-stu-id="079b2-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="079b2-158">[Event Hubs를 사용하는 이벤트 처리 확장][Scale out Event Processing with Event Hubs] 샘플</span><span class="sxs-lookup"><span data-stu-id="079b2-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="079b2-159">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="079b2-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
