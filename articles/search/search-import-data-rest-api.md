---
title: "aaa \"(REST API-Azure 검색) 데이터 업로드 | \"Microsoft Docs"
description: "Tooupload 데이터 tooan 인덱스에서 사용 하 여 Azure 검색 REST API를 hello 하는 방법에 대해 알아봅니다."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>REST API를 hello 업로드 데이터 tooAzure 사용 하 여 검색
> [!div class="op_single_selector"]
>
> * [개요](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST (영문)](search-import-data-rest-api.md)
>
>

이 문서에서는 보여 어떻게 toouse hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport 데이터를 Azure 검색 인덱스입니다.

이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들어야](search-what-is-an-index.md)합니다.

Hello REST API를 사용 하 여 인덱스로 순서 toopush 문서는 HTTP POST 요청 tooyour 인덱스의 URL 끝점을 발급 합니다. hello HTTP 요청 본문은 hello 문서 toobe 추가, 수정 또는 삭제를 포함 하는 JSON 개체의 hello 본문입니다.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure 검색 서비스의 관리 API 키 식별
Hello REST API를 사용 하 여 서비스에 대해 HTTP 요청을 발급 하는 경우 *각* hello api 키 hello를 프로 비전 할 검색 서비스에 대해 생성 된 API 요청에 포함 되어야 합니다. 유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.

1. toofind toohello에 로그인 하려면 서비스의 api 키 [Azure 포털](https://portal.azure.com/)
2. Tooyour Azure 검색 서비스 블레이드로 이동
3. Hello에 "키" 아이콘을 클릭

서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.

* 기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다. 두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.
* 프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.

인덱스에 데이터를 가져올 hello 용도로 사용할 수 있습니다 프로그램 주 또는 보조 관리자 키입니다.

## <a name="decide-which-indexing-action-toouse"></a>인덱싱 동작 toouse 결정
Hello REST API를 사용할 때 JSON 요청 본문 tooyour Azure 검색 인덱스의 끝점 URL 인 HTTP POST 요청 발급할 합니다. HTTP 요청 본문에 hello JSON 개체는 단일 JSON 배열에 포함 됩니다 tooadd tooyour 인덱스 원하는 문서를 나타내는 JSON 개체가 포함 된 "value" 라는, 업데이트 또는 삭제 합니다.

JSON 배열의 각 개체에 hello "value" 인덱싱된 문서 toobe를 나타냅니다. 이러한 각 개체 hello 문서 키를 포함 하 고 원하는 hello 인덱싱 동작 (업로드, 병합, 삭제 등)을 지정 합니다. Hello 아래의 선택한 작업 중 어느 것을 따라 특정 필드만 각 문서에 포함 되어야 합니다.

| @search.action | 설명 | 각 문서에 대해 필요한 필드 | 참고 사항 |
| --- | --- | --- | --- |
| `upload` |`upload` 동작은 비슷한 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다. |키와, toodefine를 원하는 다른 모든 필드 |기존 문서를 업데이트/교체 hello 요청에 지정 되지 않은 모든 필드 갖게 되며 해당 필드가 너무 설정`null`합니다. Hello 필드 tooa null이 아닌 값을 이전에 설정 된 경우에 발생 합니다. |
| `merge` |업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다. Hello 문서 hello 인덱스에 없는 경우 hello 병합 하지 못합니다. |키와, toodefine를 원하는 다른 모든 필드 |병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다. 여기에는 `Collection(Edm.String)`형식 필드가 포함됩니다. 예를 들어 경우 hello 문서는 필드가 `tags` 값으로 `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` 에 대 한 `tags`, hello의 최종 값 hello `tags` 필드가 `["economy", "pool"]`합니다. `["budget", "economy", "pool"]`이 아닙니다. |
| `mergeOrUpload` |이 작업 처럼 동작 `merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우. 처럼 동작 하는 hello 문서가 없는 경우 `upload` 새 문서를 사용 합니다. |키와, toodefine를 원하는 다른 모든 필드 |- |
| `delete` |Hello 인덱스에서 hello 지정 된 문서를 제거합니다. |키만 |Hello 키 필드를 무시 것과 다른 모든 필드 지정 합니다. 문서에서 개별 필드 tooremove 사용 `merge` 대신 하 고 간단 하 게 hello 필드를 명시적으로 설정 toonull 합니다. |

## <a name="construct-your-http-request-and-request-body"></a>HTTP 요청 및 요청 본문 생성
인덱스 작업에 대 한 hello 필요한 필드 값을 수집 했으므로 준비 tooconstruct hello 실제 HTTP 요청와 JSON 데이터를 요청 본문 tooimport 하세요.

#### <a name="request-and-request-headers"></a>요청 및 요청 헤더
Hello URL에 해야 tooprovide 프로그램 서비스 이름, 인덱스 이름 ("호텔"이 경우에서)으로 hello 적절 한 API 버전 (hello 현재 API 버전은 `2016-09-01` 게시 하는이 문서는 hello 시)입니다. Toodefine hello 해야 `Content-Type` 및 `api-key` 요청 헤더입니다. 후자의 hello에 대 한 서비스의 관리자 키 중 하나를 사용 합니다.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>요청 본문
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

이 경우 `upload`, `mergeOrUpload` 및 `delete`를 검색 작업으로 사용합니다.

이 예제 "호텔" 인덱스는 문서 수로 채워진다고 가정합니다. 어떻게 없는 toospecify hello 가능한 문서 필드를 모두 사용 하는 경우 유의 `mergeOrUpload` 어떻게 hello 문서 키만 지정 하 고 (`hotelId`) 사용 하는 경우 `delete`합니다.

또한, 이때 인덱싱 단일 요청에서 too1000 문서 (또는 16MB)를 포함할 수 있습니다.

## <a name="understand-your-http-response-code"></a>HTTP 응답 코드 이해
#### <a name="200"></a>200
성공적인 인덱싱 요청을 제출한 후에 `200 OK`라는 상태 코드로 HTTP 응답을 받게됩니다. hello hello HTTP 응답의 JSON 본문은 다음과 같이 됩니다.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
하나 이상의 항목이 성공적으로 인덱싱되지 않은 경우 상태 코드인 `207` 이 반환됩니다. hello hello HTTP 응답의 JSON 본문에는 hello 실패 한 문서에 대 한 정보가 포함 됩니다.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> 종종 즉, 해당 hello 부하에서 검색 서비스에 도달 함를 요청 하는 인덱스가 됩니다 tooreturn 지점 `503` 응답 합니다. 이 경우 다시 시도하기 전에 클라이언트 코드를 백오프하고 대기하는 것이 좋습니다. 이렇게 하면 hello 시스템 되므로 이후 요청이 성공할 hello 가능성이 증가 일부 시간 toorecover 있습니다. 사용자의 요청을 즉시 다시 시도 제한을 hello 상황을 연장만 됩니다.
>
>

#### <a name="429"></a>429
상태 코드 `429` hello 인덱스 당 문서 수에 할당량이 초과 하는 경우 반환 됩니다.

#### <a name="503"></a>503
상태 코드 `503` 경우 none hello 항목 hello 요청에 성공적으로 인덱싱된 반환 됩니다. 이 오류 hello 시스템 사용량이 많아 지금 요청을 처리할 수 없습니다을 의미 합니다.

> [!NOTE]
> 이 경우 다시 시도하기 전에 클라이언트 코드를 백오프하고 대기하는 것이 좋습니다. 이렇게 하면 hello 시스템 되므로 이후 요청이 성공할 hello 가능성이 증가 일부 시간 toorecover 있습니다. 사용자의 요청을 즉시 다시 시도 제한을 hello 상황을 연장만 됩니다.
>
>

문서 동작 및 성공/오류 응답에 대한 자세한 내용은 [문서 추가, 업데이트 또는 삭제](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)를 참조하세요. 오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.

## <a name="next-steps"></a>다음 단계
Azure 검색 인덱스를 채울 후 준비 toostart 문서에 대 한 쿼리 toosearch 발급 됩니다. 세부 정보는 [Azure 검색 인덱스 쿼리](search-query-overview.md) 를 참조하세요.
