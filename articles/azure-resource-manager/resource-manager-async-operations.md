---
title: "비동기 작업 aaaAzure | Microsoft Docs"
description: "설명 방법을 tootrack Azure에서 비동기 작업입니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Azure 비동기 작업 추적
Hello 작업을 신속 하 게 완료할 수 없습니다. 때문에 일부 Azure REST 작업을 비동기적으로 실행 합니다. 이 항목에서는 값을 비동기 작업의 tootrack hello 상태 hello 응답에서 반환 하는 방법을 설명 합니다.  

## <a name="status-codes-for-asynchronous-operations"></a>비동기 작업의 상태 코드
비동기 작업은 처음에 다음 중 하나의 HTTP 상태 코드를 반환합니다.

* 201(만들어짐)
* 202(수락됨) 

Hello 작업이 성공적으로 완료 되 면 중 하나를 반환 합니다.

* 200(확인)
* 204(내용 없음) 

Toohello 참조 [REST API 설명서](/rest/api/) 실행 하는 hello 작업에 대 한 toosee hello 응답 합니다. 

## <a name="monitor-status-of-operation"></a>작업의 상태 모니터링
hello 비동기 REST 작업 반환 헤더 값을 toodetermine hello 상태를 사용 하 여 hello 작업 합니다. 세 개의 헤더 값 tooexamine는 될 수 있습니다.

* `Azure-AsyncOperation`-Hello hello 작업의 진행 중인 상태 검사에 대 한 URL입니다. 작업에이 값을 반환 하는 경우 항상 hello 연산의 (위치) 하는 대신 it tootrack hello 상태를 사용 합니다.
* `Location` - 작업이 완료된 시점을 결정하는 URL입니다. Azure-AsyncOperation이 반환되지 않은 경우에만 이 값을 사용합니다.
* `Retry-After`-초 toowait 수가 hello 비동기 작업의 hello 상태를 확인 하기 전에 hello 합니다.

그러나 일부 비동기 작업은 이러한 값을 반환하지 않습니다. 예를 들어, 한 번의 작업 및 다른 작업에 대 한 hello 위치 헤더 값에 대 한 tooevaluate hello Azure AsyncOperation 헤더 값을 할 수 있습니다. 

요청에 대 한 모든 헤더 값을 검색 하는 대로 hello 헤더 값을 검색 합니다. 예를 들어 C#에서는 있습니다 hello 헤더에서 값을 검색 한 `HttpWebResponse` 라는 개체 `response` 코드 다음 hello로:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Azure-AsyncOperation 요청 및 응답

tooget hello 상태 hello 비동기 작업의 Azure AsyncOperation 헤더 값의 GET 요청 toohello URL을 보냅니다.

이 작업 응답 hello hello 본문이 hello 작업에 대 한 정보를 포함합니다. hello 다음 예제는 hello 작업에서 반환 된 hello 가능한 값.

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

`status`만이 모든 응답에 반환됩니다. hello 오류 개체가 hello 상태가 실패 또는 취소 됨 일 때 반환 됩니다. 다른 모든 값은 선택 사항입니다. 따라서 나타나면 hello 응답 hello 예제 보다 다르게 보일 수 있습니다.

## <a name="provisioningstate-values"></a>provisioningState 값

리소스 만들기, 업데이트 또는 삭제(PUT, PATCH, DELETE)하는 작업은 일반적으로 `provisioningState` 값을 반환합니다. 작업이 완료되면 다음 세 가지 값 중 하나가 반환됩니다. 

* 성공함
* Failed
* Canceled

다른 모든 값 hello 작업이 계속 실행 되 고 나타냅니다. hello 리소스 공급자의 상태를 표시 하는 사용자 지정 된 값을 반환할 수 있습니다. 예를 들어 나타날 수 있습니다 **"승인 됨"** hello 요청 수신 되어 실행 중인 경우.

## <a name="example-requests-and-responses"></a>예제 요청 및 응답

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>가상 컴퓨터 시작(Azure-AsyncOperation에서 202)
이 예제에서는 toodetermine의 상태를 hello 하는 방법을 보여 줍니다. **시작** 가상 컴퓨터에 대 한 작업입니다. 형식에 따라 hello에 hello 초기 요청은입니다.

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

상태 코드 202를 반환합니다. Hello 헤더 값에 속하지 표시 됩니다.

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

다른 요청 toothat URL을 보내는 hello 비동기 작업의 toocheck hello 상태입니다.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

hello 연산의 hello 상태를 포함 하는 hello 응답 본문:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>리소스 배포(Azure-AsyncOperation에서 201)

이 예제에서는 toodetermine의 상태를 hello 하는 방법을 보여 줍니다. **배포** 리소스 tooAzure를 배포 하기 위한 작업입니다. 형식에 따라 hello에 hello 초기 요청은입니다.

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

상태 코드 201을 반환합니다. hello hello 응답 본문이 포함 되어 있습니다.

```json
"provisioningState":"Accepted",
```

Hello 헤더 값에 속하지 표시 됩니다.

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

다른 요청 toothat URL을 보내는 hello 비동기 작업의 toocheck hello 상태입니다.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

hello 연산의 hello 상태를 포함 하는 hello 응답 본문:

```json
{"status":"Running"}
```

Hello 배포 완료 되 면 hello 응답 포함 되어 있습니다.

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>저장소 계정 만들기(위치 및 Retry-After에서 202)

이 예제에서는 toodetermine hello의 상태를 hello 하는 방법을 보여 줍니다. **만들** 저장소 계정에 대 한 작업입니다. 형식에 따라 hello에 hello 초기 요청은입니다.

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

요청 본문 hello hello 저장소 계정에 대 한 속성을 포함 되어 있습니다.

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

상태 코드 202를 반환합니다. Hello 헤더 값에 속하지 hello 다음 두 값에 표시 됩니다.

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

개수를 기다린 후 다시 시도 후에 지정 된 시간 (초), 다른 요청 toothat URL을 전송 하 여 hello 비동기 작업의 hello 상태를 확인 합니다.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Hello 요청이 실행 되 고, 상태 코드를 202 나타납니다. Hello 요청이 완료 하는 경우 사용자 상태 코드 200, 수신 및 hello hello 응답 본문이 생성 된 hello 저장소 계정의 hello 속성을 포함 합니다.

## <a name="next-steps"></a>다음 단계

* 각 REST 작업에 대한 설명서는 [REST API 설명서](/rest/api/)를 참조하세요.
* Hello 리소스 관리자 REST API를 통해 리소스를 관리 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 REST API를 사용 하 여 hello](resource-manager-rest-api.md)합니다.
* hello 리소스 관리자 REST API를 통해 서식 파일을 배포 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿 및 리소스 관리자 REST API를 사용 하 여 리소스를 배포](resource-group-template-deploy-rest.md)합니다.
