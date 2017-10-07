---
title: "이벤트 허브 캡처 연습 aaaAzure | Microsoft Docs"
description: "Hello 이벤트 허브 캡처 기능을 사용 하 여 hello Azure Python SDK toodemonstrate를 사용 하는 샘플입니다."
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
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>Event Hubs 캡처 연습: Python

이벤트 허브 수집은 tooautomatically 있습니다 수 있도록 하는 이벤트 허브의 기능 hello 스트리밍 데이터 이벤트 허브 tooan 선택한 Azure Blob 저장소 계정에에서 제공 됩니다. 이 기능을 사용 하면 쉽게 tooperform 일괄 실시간 스트리밍 데이터에서 처리 합니다. 이 문서에서는 설명 python toouse 이벤트 허브 캡처하는 방법입니다. 이벤트 허브 캡처에 대 한 자세한 내용은 참조 hello [개요 문서](event-hubs-archive-overview.md)합니다.

이 샘플에서는 hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello 캡처 기능입니다. hello sender.py 프로그램 시뮬레이션 된 환경 원격 분석 tooEvent 허브 JSON 형식으로 보냅니다. hello 이벤트 허브 구성 toouse hello 캡처 기능 toowrite 일괄 처리에서이 데이터를 tooblob 저장 합니다. hello capturereader.py 앱 다음 이러한 blob을 읽고 고 장치당, 추가 파일을 만듭니다. 그런 다음 hello 데이터를.csv 파일로 기록 합니다.

## <a name="what-will-be-accomplished"></a>수행될 작업

1. Azure Blob 저장소 계정 및 hello Azure 포털을 사용 하 여 내부에 blob에 대 한 컨테이너를 만듭니다.
2. Hello Azure 포털을 사용 하 여 이벤트 허브 네임 스페이스를 만듭니다.
3. Hello 캡처 기능을 사용 하면, hello Azure 포털을 사용 하 여 이벤트 허브를 만듭니다.
4. Python 스크립트와 함께 데이터 toohello 이벤트 허브를 보냅니다.
5. Hello 캡처의 hello 파일을 읽고 다른 Python 스크립트와 함께 처리 합니다.

## <a name="prerequisites"></a>필수 조건

- Python 2.7.x
- Azure 구독
- 활성 [Event Hubs 네임스페이스 및 이벤트 허브](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기
1. Toohello 로그온 [Azure 포털][Azure portal]합니다.
2. Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **새로**, 클릭 **저장소**, 클릭 하 고 **저장소 계정**합니다.
3. 저장소 계정 블레이드에서 hello hello 필드에 내용을 입력 하 고 클릭 **만들기**합니다.
   
   ![][1]
4. Hello를 본 후 **배포 성공** 메시지 이름을 클릭 하 여 hello hello 및 hello 새 저장소 계정의 **Essentials** 블레이드에서 클릭 **Blob**합니다. Hello 때 **Blob 서비스** 블레이드를 열고, 클릭 **+ 컨테이너** hello 위쪽에 있습니다. 이름 hello 컨테이너 **캡처**, 종가 hello **Blob 서비스** 블레이드입니다.
5. 클릭 **선택키가** hello 왼쪽된 블레이드 및 복사 hello hello 저장소 계정 이름과 hello 값에에서 **key1**합니다. 이러한 값 tooNotepad 또는 일부 다른 임시 위치에 저장 합니다.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Python 스크립트 toosend 이벤트 tooyour 이벤트 허브 만들기
1. 선호하는 Python 편집기(예: [Visual Studio Code][Visual Studio Code])를 엽니다.
2. **sender.py**라는 스크립트를 만듭니다. 이 스크립트는 200 이벤트 tooyour 이벤트 허브를 보냅니다. 이 이벤트는 JSON 형식으로 전송한 간단한 환경 판독값입니다.
3. Hello를 sender.py에 코드를 다음에 붙여 넣습니다.
   
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
4. 네임 스페이스 이름, 키 값 및 가져온 hello 이벤트 허브 네임 스페이스를 만들 때 이벤트 허브 이름 앞에 코드 toouse hello를 업데이트 합니다.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Python 스크립트 tooread 캡처 파일 만들기

1. Hello 블레이드 작성 하 고 클릭 **만들기**합니다.
2. **capturereader.py**라는 스크립트를 만듭니다. 이 스크립트는 hello 파일을 캡처한 시간과 해당 장치에 대 한 장치 toowrite hello 데이터 당 파일을 만듭니다. 읽습니다.
3. Hello를 capturereader.py에 코드를 다음에 붙여 넣습니다.
   
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
4. 저장소 계정 이름과 키 hello 호출 너무에 대 한 있는지 toopaste hello 적절 한 값이 될`startProcessing`합니다.

## <a name="run-hello-scripts"></a>Hello 스크립트 실행
1. Python 그 경로에 있는 명령 프롬프트를 열고을 tooinstall Python에 대 한 필수 구성 요소 패키지가이 명령은 실행 합니다.
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  이전 버전의 azure 저장소 서비스 또는 azure 중 하나를 사용 하도록 설정한 경우 toouse hello 할 수 있습니다 **-업그레이드** 옵션
   
  할 수도 있습니다 toorun hello 뒤 (대부분의 시스템에는 필요 하지 않습니다).
   
  ```
  pip install cryptography
  ```
2. Sender.py 및 capturereader.py, 저장 하 여 디렉터리 toowherever 이동한이 명령을 실행 합니다.
   
  ```
  start python sender.py
  ```
   
  이 명령은 새 Python 프로세스 toorun hello 발신자를 시작합니다.
3. 이제 몇 분 정도 기다렸다가 캡처 toorun hello에 대 한 합니다. Hello 프로그램 원래 명령 창에 다음 명령을 입력 합니다.
   
   ```
   python capturereader.py
   ```

   이 캡처 프로세서 hello 로컬 디렉터리 toodownload hello 저장소 계정/컨테이너에서 모든 hello blob을 사용합니다. 모든 비어 있지 않으며이 처리 하 고 hello 로컬 디렉터리에.csv 파일로 hello 결과 기록 합니다.

## <a name="next-steps"></a>다음 단계

Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [Event Hubs 캡처 개요][Overview of Event Hubs Capture]
* [Event Hubs를 사용하는 응용 프로그램 예제][sample application that uses Event Hubs] 전체.
* hello [이벤트 허브를 사용 하 여 이벤트 처리 확장] [ Scale out Event Processing with Event Hubs] 샘플.
* [Event Hubs 개요][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
