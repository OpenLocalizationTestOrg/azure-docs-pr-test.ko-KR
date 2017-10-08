---
title: "aaa \"인덱스 (REST API-Azure 검색) | \"Microsoft Docs"
description: "Hello Azure 검색 HTTP REST API를 사용 하 여 코드에서 인덱스를 만듭니다."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Hello REST API를 사용 하 여 Azure 검색 인덱스 만들기
> [!div class="op_single_selector"]
>
> * [개요](search-what-is-an-index.md)
> * [포털](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST (영문)](search-create-index-rest-api.md)
>
>

이 문서에서는 Azure 검색을 만드는 hello 과정 안내 합니다 [인덱스](https://docs.microsoft.com/rest/api/searchservice/Create-Index) Azure 검색 REST API를 hello를 사용 하 여 합니다.

이 가이드를 수행하고 인덱스를 만들기 전에 이미 [Azure 검색 서비스를 만들어야](search-create-service-portal.md)합니다.

toocreate hello REST API를 사용 하 여 Azure 검색 인덱스를 단일 HTTP POST 요청 tooyour Azure 검색 서비스의 URL 끝점에서 발생 합니다. 인덱스 정의 올바른 형식의 JSON 콘텐츠로 hello 요청 본문에 포함 됩니다.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure 검색 서비스의 관리 API 키 식별
Azure 검색 서비스를 프로 비전 했으므로 hello REST API를 사용 하 여 서비스의 URL 끝점에 대해 HTTP 요청을 실행할 수 있습니다. *모든* hello api 키 hello를 프로 비전 할 검색 서비스에 대해 생성 된 API 요청에 포함 해야 합니다. 유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.

1. toofind hello에 로그인 해야 서비스의 api 키 [Azure 포털](https://portal.azure.com/)
2. Tooyour Azure 검색 서비스 블레이드로 이동
3. Hello에 "키" 아이콘을 클릭

서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.

* 기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다. 두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.
* 프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.

인덱스 만들기의 hello 용도로 사용할 수 있습니다 프로그램 주 또는 보조 관리자 키입니다.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>올바른 형식의 JSON 형식을 사용하여 Azure 검색 인덱스 정의
단일 HTTP POST 요청 tooyour 서비스 프로그램 인덱스가 생성 됩니다. HTTP POST 요청의 본문 hello Azure 검색 인덱스를 정의 하는 단일 JSON 개체에 포함 됩니다.

1. hello이 JSON 개체의 첫 번째 속성에는 인덱스의 hello 이름입니다.
2. 이 JSON 개체의 hello 두 번째 속성은 명명 된 JSON 배열 `fields` 인덱스의 각 필드에 대 한 별도 JSON 개체가 들어 있는입니다. 여러 개의 이름/값 쌍을 포함할 각 JSON 개체 각 hello 필드 특성 "name"을 포함 하 여 "type"에 대 한 등.

각 필드 hello를 할당 해야 하는 대로 인덱스를 디자인할 때 염두에 검색 사용자 환경과 비즈니스 요구 유지 한다는 것 [적절 한 특성](https://docs.microsoft.com/rest/api/searchservice/Create-Index)합니다. 검색 기능 (필터링, 패싯, 정렬 등 전체 텍스트 검색) 되는 이러한 특성 제어 toowhich 필드를 적용 합니다. 지정 하지 않으면 모든 특성에 대 한 hello 기본 특히 해제 하지 않는 한 tooenable hello 해당 검색 기능 됩니다.

예를 들어 인덱스 "호텔"의 이름을 지정하고 필드를 다음과 같이 정의했습니다.

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

어떻게 생각 응용 프로그램에서 사용 됩니다에 따라 각 필드에 대 한 hello 인덱스 특성 선택한 신중 하 게 합니다. 예를 들어 `hotelId` 고유 키를 설정 하 여 해당 필드에 대 한 전체 텍스트 검색 비활성화 되므로 호텔 가능성이 알 수 없고에 대 한를 검색 하는 해당 사용자는 `searchable` 너무`false`, 공간 hello 인덱스에 저장 합니다.

형식의 인덱스에는 정확히 하나의 필드 점에 유의 하십시오 `Edm.String` hello로 지정 해야 hello 'key' 필드입니다.

위의 hello 인덱스 정의 언어 분석기를 사용 하 여 hello에 대 한 `description_fr` 것은 의도 한 toostore 프랑스어 텍스트 필드입니다. 참조 [hello 언어 지원 항목](https://docs.microsoft.com/rest/api/searchservice/Language-support) hello 해당 뿐만 아니라 [블로그 게시물](https://azure.microsoft.com/blog/language-support-in-azure-search/) 언어 분석기에 대 한 자세한 내용은 합니다.

## <a name="issue-hello-http-request"></a>발행 hello HTTP 요청
1. 인덱스 정의 사용 하 여 hello 요청 본문으로, HTTP POST 요청 tooyour Azure 검색 서비스 끝점 URL을 실행 합니다. Hello URL에 있는지 toouse hello 호스트 이름, 서비스 이름 이어야 하 고 적절 한 hello 배치 `api-version` 쿼리 문자열 매개 변수로 (hello 현재 API 버전은 `2016-09-01` 게시 하는이 문서는 hello 시)입니다.
2. Hello 요청 헤더에 지정 hello `Content-Type` 으로 `application/json`합니다. 알아야 tooprovide hello에서 단계 1 식별 된 서비스의 관리자 키 `api-key` 헤더입니다.

Tooprovide 고유한 서비스 이름 및 api 키 tooissue hello 요청을 아래 갖습니다.

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


성공적인 요청의 경우 상태 코드 201(생성됨)이 표시되어야 합니다. Hello REST API를 통해 인덱스를 만드는 방법에 대 한 자세한 내용은 hello를 방문 하세요 [API 참조 여기](https://docs.microsoft.com/rest/api/searchservice/Create-Index)합니다. 오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.

완료 되 면 인덱스 및 원하는 toodelete와 것을 방금 HTTP DELETE 요청을 실행 합니다. 예를 들어 다음은 hello "호텔" 인덱스 삭제는 방법입니다.

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>다음 단계
Azure 검색 인덱스를 만든 후 준비가 끝납니다 너무[hello 인덱스에 콘텐츠를 업로드](search-what-is-data-import.md) 데이터 검색을 시작할 수 있도록 합니다.
