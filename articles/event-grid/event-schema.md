---
title: "aaaAzure 이벤트 표 형태 이벤트 스키마"
description: "Azure 이벤트 표 형태 있는 이벤트에 대해 제공 되는 hello 속성을 설명 합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a>Event Grid 이벤트 스키마

이 문서에서는 이벤트에 대 한 hello 속성 및 스키마를 제공 합니다. 이벤트는 다섯 개의 필수 문자열 속성 집합과 필수 **데이터** 개체로 구성되어 있습니다. hello 속성은 모든 게시자에서 일반적인 tooall 이벤트입니다. hello **데이터** 개체에 특정 tooeach 게시자 되는 속성이 포함 되어 있습니다. 시스템 항목에 대 한 이러한 속성은 저장소 또는 이벤트 허브와 같은 특정 toohello 리소스 공급자입니다.

이벤트는 이벤트 표 형태 tooAzure 여러 이벤트 개체를 포함할 수 있는 배열에 전송 됩니다. 이벤트는 하나 뿐 이면 hello 배열 길이는 1에 있습니다. 
 
## <a name="event-properties"></a>이벤트 속성

모든 이벤트 hello 들어갑니다 다음 최상위 수준 데이터 같은 합니다.

| 속성 | 형식 | 설명 |
| -------- | ---- | ----------- |
| 토픽 | string | 전체 리소스 경로 toohello 이벤트 소스입니다. 이 필드는 쓸 수 없습니다. |
| subject | string | 게시자 정의 된 경로 toohello 이벤트 제목입니다. |
| eventType | string | 이 이벤트 소스에 대 한 이벤트 유형을 등록 한 hello 중 하나입니다. |
| eventTime | string | hello 시간 hello 이벤트 hello 공급자의 UTC 시간을 기반으로 생성 됩니다. |
| id | string | Hello 이벤트에 대 한 고유 식별자입니다. |
| 데이터 | object | 이벤트 데이터 특정 toohello 리소스 공급자입니다. |

## <a name="available-event-sources"></a>사용할 수 있는 이벤트 원본

이벤트 원본 hello 이벤트 표 형태를 통해 소비에 대 한 이벤트 게시:

* 리소스 그룹(관리 작업)
* Azure 구독(관리 작업)
* Event Hubs
* 사용자 지정 토픽

## <a name="azure-subscriptions"></a>Azure 구독

Azure 구독에서 이제 VM이 생성되거나 저장소 계정이 삭제될 때와 같이 Azure Resource Manager에서 관리 이벤트를 내보낼 수 있습니다.

### <a name="available-event-types"></a>사용할 수 있는 이벤트 유형

- **Microsoft.Resources.ResourceWriteSuccess**: 리소스 만들기 또는 업데이트 작업이 성공할 때 발생합니다.  
- **Microsoft.Resources.ResourceWriteFailure**: 리소스 만들기 또는 업데이트 작업이 실패할 때 발생합니다.  
- **Microsoft.Resources.ResourceWriteCancel**: 리소스 만들기 또는 업데이트 작업이 취소될 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteSuccess**: 리소스 삭제 작업이 성공할 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteFailure**: 리소스 삭제 작업이 실패할 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteCancel**: 리소스 삭제가 취소될 때 발생합니다. 템플릿 배포가 취소되면 발생합니다.

### <a name="example-event-schema"></a>예제 이벤트 스키마

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a>리소스 그룹

Resource Manager에서 이제 VM이 생성되거나 저장소 계정이 삭제될 때와 같이 Azure Resource Manager에서 관리 이벤트를 내보낼 수 있습니다.

### <a name="available-event-types"></a>사용할 수 있는 이벤트 유형

- **Microsoft.Resources.ResourceWriteSuccess**: 리소스 만들기 또는 업데이트 작업이 성공할 때 발생합니다.  
- **Microsoft.Resources.ResourceWriteFailure**: 리소스 만들기 또는 업데이트 작업이 실패할 때 발생합니다.  
- **Microsoft.Resources.ResourceWriteCancel**: 리소스 만들기 또는 업데이트 작업이 취소될 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteSuccess**: 리소스 삭제 작업이 성공할 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteFailure**: 리소스 삭제 작업이 실패할 때 발생합니다.  
- **Microsoft.Resources.ResourceDeleteCancel**: 리소스 삭제가 취소될 때 발생합니다. 템플릿 배포가 취소되면 발생합니다.

### <a name="example-event"></a>예제 이벤트

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a>Event Hubs

이벤트 허브 이벤트는 현재 파일 toostorage hello 캡처 기능을 사용 하 여 자동으로 전송 하는 경우에 내보내집니다.

### <a name="available-event-types"></a>사용할 수 있는 이벤트 유형

- **Microsoft.EventHub.CaptureFileCreated**: 캡처 파일이 생성될 때 발생합니다.

### <a name="example-event"></a>예제 이벤트

이 샘플 이벤트 캡처 파일을 저장 하는 경우 발생 하는 이벤트 허브 이벤트의 hello 스키마를 보여 줍니다. 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a>데이터 이동

Event Grid와의 통합에 등록한 비공개 미리 보기의 Azure Blob Storage입니다.

### <a name="available-event-types"></a>사용할 수 있는 이벤트 유형

- **Microsoft.Storage.BlobCreated**: Blob이 생성될 때 발생합니다.
- **Microsoft.Storage.BlobDeleted**: Blob이 삭제될 때 발생합니다.

### <a name="example-event"></a>예제 이벤트

이 샘플 이벤트 blob를 만들 때 발생 하는 저장소 이벤트의 hello 스키마를 보여 줍니다. 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a>사용자 지정 토픽

사용자 지정 이벤트의 데이터 페이로드 hello 사용자에 의해 정의 되 고 모든 포맷이 JSON 될 수 있습니다. hello 최상위 수준 데이터에 정의 된 표준 리소스 이벤트에 따라 필드 동일 hello를 포함 되어야 합니다. 이벤트 toocustom 항목을 게시 하는 경우 라우팅 및 필터링 하 여 이벤트 tooaid의 hello 주제를 모델링 하는 것이 좋습니다.

### <a name="example-event"></a>예제 이벤트

다음 예제는 hello 사용자 지정 항목에 대 한 이벤트를 보여 줍니다.
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a>다음 단계

* 소개 tooEvent 표를 참조 하십시오. [이벤트 표 형태는 무엇입니까?](overview.md)
* 이벤트 표 형태 구독을 만드는 방법에 대해 toolearn 참조 [이벤트 표 형태 구독 스키마](subscription-creation-schema.md)합니다.
