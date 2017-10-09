---
title: "aaaAzure 이벤트 표 형태 구독 스키마"
description: "Azure 이벤트 표 형태를 사용 하 여 구독 tooan 이벤트에 대 한 hello 속성을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Event Grid 구독 스키마

이벤트 표 형태 구독 toocreate 요청 toohello Create Event subscriptionoperation 보냅니다. 형식에 따라 hello를 사용 합니다.

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

예를 들어 toocreate 라는 저장소 계정에 대 한 이벤트 구독 `examplestorage` 리소스 그룹 이름은 `examplegroup`를 사용 하 여 hello 다음 서식을 지정:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

hello 문서 hello 속성 및 hello hello 요청 본문에 대 한 스키마를 설명합니다.
 
## <a name="event-subscription-properties"></a>이벤트 구독 속성

| 속성 | 형식 | 설명 |
| -------- | ---- | ----------- |
| destination | object | hello 끝점을 정의 하는 hello 개체입니다. |
| filter | object | Hello 유형의 이벤트를 필터링 하기 위한 선택적 필드입니다. |

### <a name="destination-object"></a>대상 개체

| 속성 | 형식 | 설명 |
| -------- | ---- | ----------- |
| endpointType | string | hello 구독 (webhook/HTTP, 이벤트 허브 또는 큐)에 대 한 끝점의 hello 형식입니다. | 
| endpointUrl | string |  | 

### <a name="filter-object"></a>필터 개체

| 속성 | 형식 | 설명 |
| -------- | ---- | ----------- |
| includedEventTypes | array | Hello 이벤트 유형을 hello 이벤트 메시지에는 정확히 일치 tooone 이러한 이벤트 유형 이름의 경우에 연결 합니다. 이벤트 이름 hello 이벤트 소스에 대 한 hello 등록 된 이벤트 형식 이름 일치 하지 않는 경우 오류가 발생 합니다. 기본값은 모든 이벤트 유형과 일치합니다. |
| subjectBeginsWith | string | 접두사 일치 필터 toohello 제목 필드 hello 이벤트 메시지입니다. 빈 문자열 또는 hello 기본 모두와 일치합니다. | 
| subjectEndsWith | string | 접미사 일치 필터가 toohello 제목 필드 hello 이벤트 메시지입니다. 빈 문자열 또는 hello 기본 모두와 일치합니다. |
| subjectIsCaseSensitive | string | 필터에 대한 대/소문자 구분 일치를 제어합니다. |


## <a name="example-subscription-schema"></a>예제 구독 스키마

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>다음 단계

* 소개 tooEvent 표를 참조 하십시오. [이벤트 표 형태는 무엇입니까?](overview.md)
