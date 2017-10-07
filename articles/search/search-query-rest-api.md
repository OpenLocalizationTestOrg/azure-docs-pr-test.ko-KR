---
title: "aaa \"는 인덱스 (REST API-Azure 검색) 쿼리하여 | \"Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성 하 고 검색 매개 변수 toofilter 및 정렬 검색 결과 사용 합니다."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Hello REST API를 사용 하 여 Azure 검색 인덱스를 쿼리 합니다.
> [!div class="op_single_selector"]
>
> * [개요](search-query-overview.md)
> * [포털](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST (영문)](search-query-rest-api.md)
>
>

이 문서에서는 방법을 사용 하 여 인덱스 tooquery hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.

이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들고](search-what-is-an-index.md) [데이터로 채워야](search-what-is-data-import.md) 합니다. 배경 정보는 [Azure Search에서 전체 텍스트 검색의 작동 방식](search-lucene-query-architecture.md)을 참조하세요.

## <a name="identify-your-azure-search-services-query-api-key"></a>Azure 검색 서비스의 쿼리 API 키 식별
Hello Azure 검색 REST API에 대해 모든 검색 작업의 핵심 구성 요소는 hello *api 키* 프로 비전 하는 hello 서비스에 대해 생성 된 합니다. 유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.

1. toofind toohello에 로그인 하려면 서비스의 api 키 [Azure 포털](https://portal.azure.com/)
2. Tooyour Azure 검색 서비스 블레이드로 이동
3. Hello "키" 아이콘을 클릭 합니다.

서비스에는 *관리자 키* 및 *쿼리 키*가 있습니다.

* 기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다. 두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.
* 프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.

Hello 인덱스는 쿼리를 위해 쿼리 키 중 하나를 사용할 수 있습니다. 쿼리에 대 한 관리자 키도 사용할 수 있지만이 더 잘 hello를 다음과 같이 응용 프로그램 코드의 쿼리 키를 사용 해야 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege)합니다.

## <a name="formulate-your-query"></a>쿼리 작성
두 가지 너무[hello REST API를 사용 하 여 인덱스를 검색할](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)합니다. 한 가지 방법은 tooissue HTTP POST 요청 쿼리 매개 변수를 hello 요청 본문의 JSON 개체에 정의 되어 있는 합니다. 다른 방법으로 hello hello 요청 URL 내에서 쿼리 매개 변수를 정의 되어 있는 tooissue HTTP GET 요청입니다. 게시물에 더 [제한을 완화](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello 크기의 GET 보다 쿼리 매개 변수입니다. 따라서 GET을 사용하는 것이 보다 편리한 특별한 경우가 아니라면 게시를 사용하는 것이 좋습니다.

POST 및 GET, 해야 tooprovide 프로그램 *서비스 이름*, *인덱스 이름*, 및 적절 한 hello *API 버전* (hello 현재 API 버전은 `2016-09-01` hello 시 이 문서를 게시 하는)는 hello에 URL을 요청 합니다. Hello에 대 한 GET, *쿼리 문자열* hello에 hello URL의 끝 hello 쿼리 매개 변수가 제공 됩니다. Hello URL 형식에 대 한 아래를 참조 하십시오.

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

hello는 POST 동일 hello는 대 한 하지만 hello 쿼리 문자열 매개 변수에서 api 버전만 서식을 지정 합니다.

#### <a name="example-queries"></a>예제 쿼리
다음은 "호텔"이라는 인덱스에 대한 몇 가지 예제 쿼리입니다. 이러한 쿼리는 가져오기 및 게시 형식으로 표시됩니다.

Hello 용어 '예산' hello 전체 인덱스 검색 하 고만 hello 반환 `hotelName` 필드:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

적용 된 필터 toohello 인덱스 toofind 호텔 매일 밤 마다 $150 보다 저렴 하 고 hello 반환 `hotelId` 및 `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

검색 hello 전체 인덱스, 특정 필드에 따라 순서 (`lastRenovationDate`) hello 맨 위의 두 결과 가져오고 상태만 표시 내림차순으로 `hotelName` 및 `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>HTTP 요청 제출
쿼리를 HTTP 요청 URL(가져오기의 경우) 또는 본문(게시의 경우)의 일부로 작성했으므로 요청 헤더를 정의하고 쿼리를 제출할 수 있습니다.

#### <a name="request-and-request-headers"></a>요청 및 요청 헤더
가져오기에 두 개의 요청 헤더 또는 게시에 세 개의 요청 헤더를 정의해야 합니다.

1. hello `api-key` 헤더 단계에서 찾은 I 위의 toohello 쿼리 키를 설정 해야 합니다. Hello로 관리자 키를 사용할 수도 있습니다 `api-key` tooindexes 읽기 전용 액세스 및 문서 배타적으로 부여 하는 대로 쿼리 키를 사용 하는 헤더가 없지만 것이 좋습니다.
2. hello `Accept` 헤더 너무 설정 되어 있어야`application/json`합니다.
3. POST, hello `Content-Type` 헤더 너무 설정 해야`application/json`합니다.

인덱스에 대해 HTTP GET 요청 toosearch hello "호텔" hello hello 용어 "motel"에 대 한 검색 하는 간단한 쿼리를 사용 하 여 Azure 검색 REST API를 사용 하 여 아래를 참조 하십시오.

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

다음 동일 hello은 쿼리 예에서는 HTTP POST를 사용 하 여이 시간:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

성공적인 쿼리 요청은 상태 코드 됩니다 `200 OK` hello 검색 결과가 hello 응답 본문에서 JSON으로 반환 됩니다. 어떤 hello 호텔"hello" 인덱스에 있는 샘플 데이터 hello 채워집니다 가정할 때, 쿼리 모양 위에 hello에 대 한 결과 다음과 같습니다 [데이터 가져오기를 사용 하 여 Azure 검색 REST API hello](search-import-data-rest-api.md) (JSON 쉽도록 서식이 지정 된 해당 hello 참고).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn을 방문 하세요 hello "응답" 섹션의 [문서 검색](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)합니다. 오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.
