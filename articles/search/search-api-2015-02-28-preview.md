---
title: "검색 서비스 REST API 버전 2015-02-28-preview aaaAzure | Microsoft Docs"
description: "Azure 검색 서비스 REST API 버전 2015-02-28-Preview에는 자연어 분석기 및 moreLikeThis 검색과 같은 실험적 기능이 포함되어 있습니다."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>Azure 검색 서비스 REST API: 버전 2015-02-28-Preview
이 문서에 대 한 hello 참조 설명서는 `api-version=2015-02-28-Preview`합니다. 이 미리 보기는 현재 일반 공급 버전 hello 확장 [api 버전 2015-02-28 =](https://msdn.microsoft.com/library/dn798935.aspx), hello 같은 실험적 기능을 제공 하 여:

* `moreLikeThis`쿼리 매개 변수 hello [문서 검색](#SearchDocs) API입니다. 다른 문서를 관련 tooanother 특정 문서를 찾습니다.

몇 가지 추가 부분의 hello `2015-02-28-Preview` REST API에 별도로 제공 합니다. 내용은 다음과 같습니다.

* [점수 매기기 프로필](search-api-scoring-profiles-2015-02-28-preview.md)
* [인덱서](search-api-indexers-2015-02-28-preview.md)

Azure 검색 서비스는 여러 버전으로 제공됩니다. 너무를 참조 하십시오[검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 대 한 자세한 내용은 합니다.

## <a name="apis-in-this-document"></a>이 문서의 API
Azure 검색 서비스 API는 API 작업을 위한 두 URL 구문, 즉 simple 및 OData(자세한 내용은 [OData(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) 를 참조하세요). hello 다음 목록은 hello 간단한 구문입니다.

[인덱스 만들기](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[인덱스 업데이트](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[인덱스 가져오기](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[인덱스 나열](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[인덱스 통계 가져오기](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[테스트 분석기](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[인덱스 삭제](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[인덱스 내에서 데이터 추가, 삭제 및 업데이트](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[문서 검색](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[문서 조회](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[문서 수 계산](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[제안](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>인덱스 작업
Azure 검색 서비스에서 간단한 HTTP 요청(POST, GET, PUT, DELETE)을 통해 지정된 인덱스 리소스에 대해 인덱스를 만들고 관리할 수 있습니다. 인덱스 toocreate를 처음 게시 하면 hello 인덱스 스키마를 설명 하는 JSON 문서입니다. hello 스키마 hello index, 해당 데이터 형식 및 수 수 사용 방법 (예를 들어 전체 텍스트 검색, 필터, 정렬 또는 패싯)의 hello 필드를 정의 합니다. 또한 점수 매기기 프로필, 확인 기 및 기타 특성 tooconfigure hello hello 인덱스의 동작을 정의합니다.

hello 다음 예에서는 hello 설명 필드 두 언어로 정의 된 호텔 정보 검색에 사용 되는 스키마를 보여 줍니다. Hello 필드 사용량 특성을 제어 하는 방법을 확인 합니다. 예를 들어 hello `hotelId` hello 문서 키로 사용 됩니다 (`"key": true`) 및 전체 텍스트 검색에서 제외 되었습니다 (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Hello 인덱스를 만든 후에 hello 인덱스를 채울 문서를 업로드 합니다. 이 작업을 수행하는 다음 단계는 [문서 추가 또는 업데이트](#AddOrUpdateDocuments) 를 참조하세요.

Azure 검색의 한 비디오 지침은 tooindexing, 참조 hello [Azure 검색에 대 한 채널 9의 Cloud Cover 에피소드](http://go.microsoft.com/fwlink/p/?LinkId=511509)합니다.

<a name="CreateIndex"></a>

## <a name="create-index"></a>인덱스 만들기
인덱스는 hello 기본 방법은 구성 하 고 Azure 검색에서 문서를 검색, 비슷한 toohow 테이블은 데이터베이스에서 레코드를 구성 합니다. 각 인덱스에 모든 toohello 인덱스 스키마 (필드 이름, 데이터 형식 및 속성)을 준수 하지만 기타 검색 동작을 정의 하는 추가 구문 (확인 기, 점수 매기기 프로필 및 CORS 옵션)도 지정 하는 문서 컬렉션입니다.

HTTP POST 또는 PUT 요청을 사용하여 Azure 검색 서비스 내에서 새 인덱스를 만들 수 있습니다. hello hello 요청 본문은 hello 인덱스 및 구성 정보를 지정 하는 JSON 스키마입니다.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

또는 PUT을 사용 하 여 하 고 hello URI에서 hello 인덱스 이름을 지정할 수 있습니다. Hello 인덱스가 없는 경우 생성 됩니다.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

인덱스를 만들면 hello 문서 저장 및 검색 작업에 사용의 hello 구조를 결정 합니다. 채우는 hello 인덱스는 별도 작업 합니다. 이 단계에는 [인덱서](https://msdn.microsoft.com/library/azure/mt183328.aspx)(지원되는 데이터 원본에 사용 가능)를 사용하거나 [문서 추가, 업데이트 또는 삭제](https://msdn.microsoft.com/library/azure/dn798930.aspx) 작업을 수행할 수 있습니다. hello 반전 된 인덱스는 hello 문서를 게시 하는 경우에 생성 됩니다.

**참고**: 가격 책정 계층으로 사용할 수 있는 인덱스의 최대 수 hello 다릅니다. hello 무료 서비스 too3 인덱스를 허용합니다. 표준 서비스에서는 검색 서비스당 인덱스 50개를 만들 수 있습니다. 자세한 내용은 [한도 및 제약 조건](http://msdn.microsoft.com/library/azure/dn798934.aspx)을 참조하세요.

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **Create Index** POST 또는 PUT 메서드를 사용 하 여 요청을 생성할 수 있습니다. POST를 사용할 때는 hello 인덱스 스키마 정의와 함께 hello 요청 본문에 인덱스 이름을 제공 해야 합니다. PUT을 사용 hello 인덱스 이름은 hello URL의 일부입니다. Hello 인덱스가 존재 하지 않는 경우 자동으로 만들어집니다. 이미 있는 경우 업데이트 된 toohello 새 정의입니다.

hello 인덱스 이름은 소문자 여야, 문자 또는 숫자로 시작, 없습니다 슬래시나 마침표를을 있어야 128 자 미만입니다. Hello 인덱스 이름은 문자 또는 숫자로 시작 된 후 hello 나머지 hello 이름 포함할 수 있습니다는 문자, 숫자 및 대시만 hello 대시를 연속 되지 않은 상태로.

hello `api-version` 가 필요 합니다. 사용 가능한 버전 목록은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `Content-Type`: 필수 사항입니다. 너무 설정 합니다.`application/json`
* `api-key`: 필수 사항입니다. hello `api-key` 사용 하 여
* hello 요청 tooyour 검색 서비스를 인증 합니다. 문자열 값, 고유 tooyour 서비스 이며 hello **Create Index** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. 두 hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

<a name="RequestData"></a>
**요청 본문 구문**

이 인덱스에 공급할 문서 내의 데이터 필드의 hello 목록을 포함 하는 스키마 정의 포함 하는 hello hello 요청 본문, 점수 매기기 프로필 하는 선택적인 목록 뿐만 아니라 데이터 형식, 특성을 포함 하는 문서에 사용 되는 tooscore 됩니다. 쿼리 시간입니다.

POST 요청에 대 한 이름을 지정 해야 hello 인덱스 hello 요청 본문에 참고 합니다.

있습니다 하나의 키 필드는 hello 인덱스의 수만 있습니다. 문자열 필드 toobe에 있습니다. 이 필드는 hello hello 인덱스 내에 저장 된 각 문서에 대 한 고유 식별자를 나타냅니다.

인덱스의 주요 부분 hello hello 다음과를 같습니다.

* `name`
* `fields` : 이름, 데이터 형식 및 해당 필드에 대해 허용되는 작업을 정의하는 속성을 포함하여 이 인덱스에 공급할 필드입니다.
* `suggesters` : 자동 완성 또는 미리 입력 쿼리에 사용됩니다.
* `scoringProfiles` : 사용자 지정 검색 점수 순위에 사용됩니다. 자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하세요.
* `analyzers``charFilters`, `tokenizers`, `tokenFilters` toodefine 인덱싱/검색 가능한 토큰으로 문서/쿼리는 구분 하는 방법을 사용 합니다. 자세한 내용은 [Azure 검색의 분석](https://aka.ms//azsanalysis) 을 참조하세요.
* `defaultScoringProfile`toooverwrite hello 기본 점수 매기기 동작을 사용 합니다.
* `corsOptions`인덱스에 대 한 tooallow 크로스-원본 쿼리입니다.

hello hello 요청 페이로드 구조를 지정 하는 것에 대 한 구문은 다음과 같습니다. 이 항목에서 샘플 요청이 추가로 제공됩니다.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**인덱스 특성**

hello 다음 특성을 설정할 인덱스를 만들 때. 점수 매기기 및 점수 매기기 프로필에 대한 자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx)를 참조하세요.

`name`세트 hello hello 필드의 이름입니다.

`type`세트 hello hello 필드에 대 한 데이터 형식입니다.

`searchable`-표시 hello 필드 전체 텍스트 검색 가능 합니다. 이렇게 표시된 필드의 경우 인덱싱 중에 단어 분리 등의 분석이 수행됩니다. 설정 하는 경우는 `searchable` "sunny day"와 같은 필드 tooa 값을 내부적으로 됩니다 "sunny"와 "일" hello 개별 토큰으로 구분 합니다. 따라서 이러한 용어에 대한 전체 텍스트 검색을 수행할 수 있습니다. 형식이 `Edm.String` 또는 `Collection(Edm.String)`인 필드는 기본적으로 `searchable`로 설정됩니다. 다른 형식의 필드는 `searchable`로 설정할 수 없습니다.

* **참고**: `searchable` 필드 Azure 검색은 전체 텍스트 검색에 대 한 hello 필드 값의 추가 토큰화 된 버전을 저장 하므로 인덱스에서 추가적인 공간을 사용 합니다. Toosave 공간에 원하는 인덱스 하 고 검색에 포함 하는 필드 toobe 필요 하지 않은 설정, `searchable` 너무`false`합니다.

`filterable`-에서 참조 하는 hello 필드 toobe 허용 `$filter` 쿼리 합니다. `filterable`은(는) 문자열 처리 방법에서 `searchable`와(과) 다릅니다. 형식이 `Edm.String` 또는 `Collection(Edm.String)`이며 `filterable`인 필드의 경우 단어 분리가 수행되지 않으므로 정확하게 일치하는 항목만 비교합니다. 예를 들어, 이러한 필드를 설정 하면 `f` 너무 "sunny day" `$filter=f eq 'sunny'` 일치 하는 항목을 찾을 수 있지만 `$filter=f eq 'sunny day'` 됩니다. 기본적으로 모든 필드는 `filterable` 로 설정됩니다.

`sortable`-기본적으로 hello 시스템 설정, 결과 정렬 하지만 대부분의 사용자가 hello 문서의 필드에 의해 toosort 합니다. 형식이 `Collection(Edm.String)`인 필드는 `sortable`로 설정할 수 없습니다. 기타 모든 필드는 기본적으로 `sortable` 로 설정됩니다.

`facetable` - 일반적으로 범주별 적중 횟수를 포함하는 검색 결과 표시에 사용됩니다. 디지털 카메라를 검색한 다음 브랜드, 메가픽셀, 가격 등을 기준으로 적중 항목을 표시하는 경우를 예로 들 수 있습니다. 형식이 `Edm.GeographyPoint`인 필드에는 이 옵션을 사용할 수 없습니다. 기타 모든 필드는 기본적으로 `facetable` 로 설정됩니다.

* **참고**: `filterable`, `sortable` 또는 `facetable`인 `Edm.String` 형식 필드의 최대 길이는 32KB입니다. 이 이러한 필드는 단일 검색 용어로 처리 되는데 Azure 검색에서 용어의 hello 최대 길이 32KB 때문입니다. Tooexplicitly 할 toostore 단일 문자열 필드에 이보다 많은 텍스트를 해야 하는 경우 설정 `filterable`, `sortable`, 및 `facetable` 너무`false` 인덱스 정의의 합니다.
* **참고**: 특성이 너무 설정 없음 hello 위의 필드에 있으면`true` (`searchable`, `filterable`, `sortable`, 또는`facetable`) hello 필드는 hello 반전 된 인덱스에서 제외 됩니다. 쿼리에서 사용되지는 않지만 검색 결과에는 필요한 필드의 경우 이 옵션을 사용하면 유용합니다. 이러한 필드를 제외 하 고 hello 인덱스에서 성능이 향상 됩니다.

`key`-부호 hello 필드 hello 인덱스 내의 문서에 대 한 고유 식별자를 포함 하는 것입니다. Hello로 정확히 하나의 필드를 선택 해야 합니다. `key` 필드가 형식 이어야 합니다 `Edm.String`합니다. 키 필드는 hello 통해 직접 문서를 사용 하는 toolook 수 [조회 API](#LookupAPI)합니다.

`retrievable`-Hello 필드는 검색 결과에 반환 될 수 있는지 여부를 설정 합니다.  정렬 또는 점수 매기기 메커니즘은 필터로 toouse 필드 (예를 들어, 여백)을 원하는 하지만 hello 필드 toobe 표시 toohello 최종 사용자를 원하지 않는 경우에 유용 합니다. `true` for `key` 로 설정해야 합니다.

`analyzer`-설정 검색 시간 및 인덱싱 단계에서 hello 필드에 대 한 hello 분석기 toouse의 이름을 hello 합니다. 값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다. 이 옵션은 `searchable` 필드에만 사용할 수 있으며 `searchAnalyzer` 또는 `indexAnalyzer`와 함께 설정할 수 없습니다.  Hello 분석기를 선택한 후에 hello 필드에 대 한 변경할 수 없습니다.

`searchAnalyzer`세트 hello hello 필드에 대 한 검색 시 사용 하는 hello 분석기의 이름입니다. 값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다. 이 옵션은 `searchable` 필드에만 사용할 수 있습니다. 와 함께 설정 되어야 `indexAnalyzer` hello와 함께 설정할 수 없습니다 및 `analyzer` 옵션입니다. 이 분석기는 기존 필드에서 업데이트할 수 있습니다.

`indexAnalyzer`세트 hello hello 필드에 대 한 인덱싱 단계에서 사용 되는 hello 분석기의 이름입니다. 값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다. 이 옵션은 `searchable` 필드에만 사용할 수 있습니다. 와 함께 설정 되어야 `searchAnalyzer` hello와 함께 설정할 수 없습니다 및 `analyzer` 옵션입니다. Hello 분석기를 선택한 후에 hello 필드에 대 한 변경할 수 없습니다.

`suggesters`집합에는 검색 모드 및 제안에 대 한 hello 내용의 hello 소스 필드 hello 합니다. 자세한 내용은 [확인기](#Suggesters) 를 참조하세요.

`scoringProfiles` - 검색 결과에서 더 위쪽에 표시할 항목을 제어할 수 있는 사용자 지정 점수 매기기 동작을 정의합니다. 점수 매기기 프로필은 필드 가중치와 함수로 구성됩니다. 참조 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 점수 매기기 프로필에서 사용 되는 hello 특성에 대 한 자세한 내용은 합니다.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**언어 지원**

검색 가능 필드에서는 대개 단어 분리, 텍스트 정규화, 용어 필터링 등을 포함하는 분석이 수행됩니다. 기본적으로 Azure 검색의 검색 가능 필드 hello로 분석 [Apache Lucene 표준 분석기](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) 요소 뒤에 텍스트를 나눕니다 하는["유니코드 텍스트 구분"](http://unicode.org/reports/tr29/) 규칙입니다. 또한 표준 분석기 hello 모든 문자 tootheir 소문자 형식으로 변환합니다. 인덱싱된 문서와 검색 용어는 인덱싱 및 쿼리 처리 중 hello 분석을 통해 이동합니다.

Azure 검색은 다양한 언어를 지원합니다. 각 언어를 사용하려면 지정된 언어의 특성을 고려할 수 있는 비표준 텍스트 분석기가 필요합니다. Azure 검색에서는 다음 두 가지 유형의 분석기를 제공합니다.

* Lucene에서 지원하는 35개의 분석기
* Office 및 Bing에서 사용되는 Microsoft 소유 자연어 처리 기술로 지원되는 50개의 분석기

일부 개발자 들이 선호할 수 hello Lucene의 더 친숙 한, 단순, 오픈 소스 솔루션입니다. Lucene 분석기는 속도가 더 하지만 hello Microsoft 분석기 보조 정리 하는 등의 기능이 고급, 단어 (독일어, 덴마크어, 네덜란드어, 스웨덴어, 노르웨이어, 에스토니아어, 완료, 헝가리어, 슬로바키아어과 같은 언어)에서 decompounding 및 엔터티 인식 (Url 전자 메일, 날짜, 숫자)입니다. 가능 하면 한 더 적합할 두 hello Microsoft 및 Lucene 분석기 toodecide의 비교를 실행 해야 합니다.

***비교 방법***

영어에 대 한 hello Lucene 분석기 hello 표준 분석기를 확장합니다. 이 분석기는 단어에서 소유격(후행 's)을 제거하고, [Porter 형태소 분석 알고리즘](http://tartarus.org/~martin/PorterStemmer/)에 따라 형태소 분석을 적용하며, 영어의 [중지 단어](http://en.wikipedia.org/wiki/Stop_words)를 제거합니다.

반면 hello Microsoft 분석기 형태소 분석 하는 대신 보조 정리를 수행합니다. 즉, 어형이 변화되고 불규칙한 단어 형태 관련 검색 결과에서 더 정확한 결과로 처리할 수 있습니다.(자세한 내용은 [Azure 검색 MVA 프레젠테이션](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) 의 모듈 7 보기)

Microsoft 분석기를 사용 하 여 인덱싱 Lucene 동등한 hello 언어에 따라 보다 느린 두 toothree 시간이 평균적 됩니다. 검색 성능은 평균 크기 쿼리에 크게 영향을 받지 않아야 합니다.

***구성***

Hello 인덱스 정의의 각 필드에 대 한 hello를 설정할 수 있습니다 `analyzer` 언어 및 공급 업체를 지정 하는 속성 tooan 분석기 이름입니다. hello 인덱싱 및 해당 필드에 대 한 검색 하는 경우 동일한 분석기 적용 됩니다.
예를 들어 영어, 프랑스어, 스페인어 호텔 설명 나란히 hello에 존재 하는 대 한 개별 필드가 점이 같은 인덱스입니다. 사용 하 여 hello ['searchFields' 쿼리 매개 변수](#SearchQueryParameters) toospecify 쿼리에 대해 어떤 언어별 필드 toosearch 합니다. Hello를 포함 하는 쿼리 예제를 검토할 수 있습니다 `analyzer` 속성 [문서 검색](#SearchDocs)합니다. 

***분석기 목록***

아래에 Microsoft 및 Lucene 분석기 이름과 함께 지원 되는 언어의 hello 목록입니다.

<table style="font-size:12">
    <tr>
        <th>언어</th>
        <th>Microsoft 분석기 이름</th>
        <th>Lucene 분석기 이름</th>
    </tr>
    <tr>
        <td>아랍어</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>아르메니아어</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>벵골어</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>바스크어</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>불가리아어</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>카탈로니아어</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>중국어 간체</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>중국어 번체</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>크로아티아어</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>체코어</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>덴마크어</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>네덜란드어</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>영어</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>에스토니아어</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>핀란드어</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>프랑스어</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>갈리시아어</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>독일어</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>그리스어</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>구자라트어</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>히브리어</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>힌디어</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>헝가리어</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>아이슬란드어</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>인도네시아어(공용어)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>아일랜드어</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>이탈리아어</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>일본어</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>카나다어</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>한국어</td>
        <td>ko.microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>라트비아어</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>리투아니아어</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>말라얄람어</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>말레이어(라틴 문자)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>마라티어</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>노르웨이어</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>페르시아어</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>폴란드어</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>포르투갈어(브라질)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>포르투갈어(포르투갈)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>펀잡어</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>루마니아어</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>러시아어</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>세르비아어(키릴자모)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>세르비아어(라틴 문자)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>슬로바키아어</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>슬로베니아어</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>스페인어</td>
        <td>es.microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>스웨덴어</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>타밀어</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>텔루구어</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>태국어</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>터키어</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>우크라이나어</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>우르두어</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>베트남어</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Azure 검색에서는 추가적으로 언어에 관계없는 분석기 구성을 제공합니다.</td>
    <tr>
        <td>표준 ASCII 접기</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>유니코드 텍스트 구분(표준 토크나이저)입니다.</li>
            <li>ASCII 접기 필터-유니코드 문자를 해당 ASCII 문자로 toohello 처음 127 ASCII 문자 집합에 속하지 않는 변환 합니다. 분음 부호(악센트)를 제거하는 데 유용합니다.</li>
        </ul>
        </td>
    </tr>
</table>

이름에 <i>lucene</i> 주석이 포함된 모든 분석기는 [Apache Lucene 언어 분석기](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html)를 통해 구동됩니다. Hello ASCII 접기 필터에 대 한 자세한 정보를 찾을 수 [여기](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html)합니다.

**확인기**

A `suggester` 검색에서 자동 완성 사용 되는 toosupport 인덱스의 필드를 정의 합니다. 일반적으로 부분 검색 문자열이 toohello 보내집니다 [제안 API](#Suggestions) hello 사용자가 검색 쿼리를 입력 하 고 hello API는 제안된 구 집합을 반환 합니다. Hello 인덱스에서 정의 하는 확인 기 필드는 사용 되는 toobuild hello 미리 입력 검색 용어를 결정 합니다. 구성 세부 정보는 [확인기](#Suggesters) 를 참조하세요.

**점수 매기기 프로필**

A `scoringProfile` 사용자 지정 점수 매기기 동작을 제어할 수 있는 상위 hello 검색 결과에 표시 되는 항목을 정의 합니다. 점수 매기기 프로필은 필드 가중치와 함수로 구성됩니다. toouse hello 쿼리 문자열에서 이름으로 프로필을 지정 합니다.

점수 매기기 프로필 기본 결과 집합에 있는 모든 항목에 대 한 검색 점수 hello 장면 toocompute 뒤 작동 합니다. Hello 내부 명명 되지 않은 점수 매기기 프로필을 사용할 수 있습니다. 또는 설정할 `defaultScoringProfile` toouse hello 쿼리 문자열에서 사용자 지정 프로필을 지정 하지 않으면 때마다 호출 됩니다. hello 기본값으로 사용자 지정 프로필.

참조 [tooa 검색 인덱스 (Azure 검색 서비스 REST API) 프로필 추가 점수 매기기](search-api-scoring-profiles-2015-02-28-preview.md) 대 한 자세한 내용은 합니다.

**CORS 옵션**

클라이언트 쪽 Javascript hello 브라우저 모든 교차 원본 요청 하면 이후 기본적으로 Api를 호출할 수 없습니다. CORS (크로스-원본 자원 공유)를 사용 하도록 설정 하 여 hello 설정 `corsOptions` 특성 tooallow 크로스-원본 쿼리가 tooyour 인덱스입니다. 보안상 쿼리 API에서만 CORS가 지원됩니다. CORS에 대해 hello 다음 옵션을 설정할 수 있습니다.

* `allowedOrigins`(필수): 액세스 tooyour 인덱스 부여 되는 원본 목록입니다. 이 허용 된 tooquery 인덱스 (올바른 API 키 hello를 제공 한다고 가정할 경우)이 원본에서 제공 하는 모든 Javascript 코드 수 있다는 것을 의미 합니다. 각 원본은 일반적으로 hello 폼의 `protocol://fully-qualified-domain-name:port` hello 포트는 생략 되는 경우가 많습니다. 자세한 내용은 [이 문서](http://go.microsoft.com/fwlink/?LinkId=330822) 를 참조하세요.
  * Tooallow 액세스 tooall origin 포함 `*` hello에 단일 항목으로 `allowedOrigins` 배열입니다. **프로덕션 검색 서비스에서는 이러한 방식을 사용하지 않는 것이 좋습니다.** 개발 또는 디버깅용으로는 이 기능이 유용할 수 있습니다.
* `maxAgeInSeconds`(선택 사항): 브라우저에서는이 값 toodetermine hello 기간 (초) toocache CORS 실행 전 응답을 사용 합니다. 이 값은 음수가 아닌 정수여야 합니다. 이 값은 더 나은 성능은 hello hello 더 큰 하지만 hello 긴 좋아지지만 CORS 정책 변경 내용 tootake 효과입니다. 이 값을 설정하지 않으면 기본 기간인 5분이 사용됩니다.

<a name="CreateUpdateIndexExample"></a>
**요청 본문 예제**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**응답**

요청이 성공적으로 실행되면 “201 생성됨”이 반환됩니다.

기본적으로 hello 응답 본문에는 생성 된 hello 인덱스 정의 대 한 JSON hello를 포함 됩니다. 경우 hello `Prefer` 요청 헤더가 너무 설정 되어`return=minimal`, hello 응답 본문은 비어 있게 및 hello 성공 상태 코드 됩니다 "204 콘텐츠 없음" 대신 "201 생성 됨"입니다. PUT 또는 POST 사용된 toocreate hello 인덱스 했는지 여부에 관계 없이 유용 합니다.

**설명**

현재는 인덱스 스키마 업데이트가 제한적으로 지원됩니다. 필드 형식을 변경하는 등 인덱싱을 다시 수행해야 하는 모든 스키마 업데이트는 현재 지원되지 않습니다. 기존 필드를 변경 하거나 삭제할 수 없습니다, 없지만 새 필드는 언제 든 지 기존 인덱스 tooan 추가할 수 있습니다. 새 필드를 추가 하는 경우 모든 기존 문서 hello 인덱스에서 해당 필드에 대해 null 값을 자동으로 포함 됩니다. 새 문서 toohello 인덱스 추가 될 때까지 추가 저장 공간이 없는 사용 됩니다.

<a name="Suggesters"></a>

## <a name="suggesters"></a>확인기
Azure 검색의 hello 제안 기능은는 검색 상자에 입력 하는 응답 toopartial 문자열 입력에 잠재적 검색 용어 목록을 제공 하는 미리 입력 또는 자동 완성 쿼리 기능입니다. 상용 웹 검색 엔진 사용 시 쿼리 제안을 보았을 것입니다. Bing에 ".NET"를 입력하면 ".NET 4.5", ".NET Framework 3.5" 등에 대한 용어 목록이 생성됩니다. Hello 검색 서비스 REST API를 사용할 때 사용자 지정 Azure 검색 응용 프로그램에서 제안을 구현 hello 다음을 사항이 필요 합니다.

* 추가 하 여 제안을 사용 하도록 설정 된 **확인 기** 제공 hello 이름, 검색 모드 및 필드 목록이을 미리 입력 하려면 인덱스에 생성이 호출 됩니다. 예를 들어 "시애틀"에 발생 합니다 "sea"라는 부분 검색 문자열을 입력 하 여 원본 필드로 "cityName"을 지정 하면 "Seaside" 및 "Seatac" (세 개 모두가 실제 도시 이름임)으로 제공 쿼리 제안 toohello 사용자.
* Hello를 호출 하 여 제안을 호출 [제안 API](#Suggestions) 응용 프로그램 코드에서. 일반적으로 hello 사용자가 검색 쿼리를 입력 하 고이 API는 제안된 구 집합을 반환 하는 동안 부분 검색 문자열이 toohello 서비스에 전송 됩니다.

이 문서에서는 설명 방법을 tooconfigure는 **확인 기**합니다. Hello도 검토 해야 [제안 API](#Suggestions) 는 확인 기 사용 되는 방법에 대 한 내용은 합니다.

**사용 현황**

`Suggesters`hello 인덱스에 생성 되 고 사용 되는 경우에 가장 효과적 toosuggest 특정 한 용어나 구보다는 대신에 대해 설명 합니다. hello 적합 한 필드는 제목, 이름 및 항목을 식별할 수 있는 비교적 짧은 기타 구입니다. 반면 범주/태그 등의 반복 필드나 설명/주석 등의 매우 긴 필드는 확인기를 사용하기에 덜 적합합니다.

Hello 인덱스 정의의 일환으로, 단일 확인 기 toohello를 추가할 수 있습니다 `suggesters` 컬렉션입니다. 확인 기를 정의 하는 속성에는 hello 다음과를 같습니다.

* `name`: hello 이름 hello 확인 기입니다. Hello 확인 기 이름을 hello를 사용 하 여 hello를 호출할 때 `suggest` API입니다.
* `searchMode`: 제안 가능한 구를 사용 하는 전략 toosearch hello 합니다. hello 현재 지원 되는 유일한 모드는 `analyzingInfixMatching`, 구 또는 문장 hello 중간 hello 시작 부분에서 유연 일치를 수행 합니다.
* `sourceFields`: 제안에 대 한 hello 내용의 hello 소스 있는 하나 이상의 필드의 목록입니다. 형식이 `Edm.String` 및 `Collection(Edm.String)`인 필드만 제안 원본으로 사용할 수 있습니다. 또한 사용자 지정 언어 분석기가 설정되지 않은 필드만 사용할 수 있습니다.

**확인기 예제**

확인 기는 hello 인덱스의 일부입니다. 하나의 확인 기 hello에 존재할 수 `suggesters` hello와 함께 hello 최신 버전의 컬렉션 필드 컬렉션 및 `scoringProfiles`합니다.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Azure 검색의 hello 공개 미리 보기 버전을 사용 하는 경우 `suggesters` 했던 이전 부울 속성을 바꿉니다 (`"suggestions": false`) (3 ~ 25 자) 사이의 짧은 문자열에 대 한만 접두사 제안을 지원입니다. 를 대체할 `suggesters`, 지원 또는 필드 콘텐츠의 hello 중간 hello 시작 부분에서 반환 될 확률이 높아집니다 검색 문자열에 일치 하는 용어를 발견 하는 일치 하는 중 위 합니다. Hello 일반 공급 릴리스 이상에서는 이것이 이제 hello 제안 API hello 으로만 구현입니다. 이전 hello `suggestions` 에 도입 된 속성 `api-version=2014-07-31-Preview` toowork 해당 버전에서는 계속 하지만 hello에서는 작동 하지 않습니다 `2015-02-28` 또는 이후 버전의 Azure 검색 합니다.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>인덱스 업데이트
HTTP PUT 요청을 사용하여 Azure 검색 내에서 기존 인덱스를 업데이트할 수 있습니다. 새 필드 toohello 기존 스키마 추가, CORS 옵션 수정 및 점수 매기기 프로필 수정 업데이트 포함할 수 있습니다. 자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하세요. Hello 요청 URI에 hello 인덱스 tooupdate의 hello 이름을 지정합니다.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**중요:** 인덱스 스키마 업데이트에 대 한 지원은 제한 toooperations hello 검색 인덱스를 다시 작성 하는 설정이 필요 하지 않은 합니다. 필드 형식을 변경하는 등 인덱싱을 다시 수행해야 하는 모든 스키마 업데이트는 현재 지원되지 않습니다. 기존 필드를 변경하거나 삭제할 수는 없지만 언제든지 새 필드를 추가할 수는 있습니다. hello에 마찬가지 너무`suggesters`합니다. Hello 시간 hello 필드에서 tooa 기가 추가 되지만에서 필드를 제거할 수 없는 새 필드를 추가할 수 `suggesters` 너무 추가할 수 없습니다 기존 필드`suggesters`합니다.

새 필드 tooan 인덱스에 추가할 때는 hello 인덱스의 모든 기존 문서는 해당 필드에 대해 null 값을 자동으로 포함 됩니다. 새 문서 toohello 인덱스 추가 될 때까지 추가 저장 공간이 없는 사용 됩니다.

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **업데이트 인덱스** HTTP PUT을 사용 하 여 요청을 생성 합니다. PUT을 사용 hello 인덱스 이름은 hello URL의 일부입니다. Hello 인덱스가 존재 하지 않는 경우 자동으로 만들어집니다. Hello 인덱스가 이미 있으면 업데이트 된 toohello 새 정의 됩니다.

hello 인덱스 이름은 소문자 여야, 문자 또는 숫자로 시작, 없습니다 슬래시나 마침표를을 있어야 128 자 미만입니다. Hello 인덱스 이름은 문자 또는 숫자로 시작 된 후 hello 나머지 hello 이름 포함할 수 있습니다는 문자, 숫자 및 대시만 hello 대시를 연속 되지 않은 상태로.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `Content-Type`: 필수 사항입니다. 너무 설정 합니다.`application/json`
* `api-key`: 필수 사항입니다. hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **인덱스 업데이트가** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문 구문**

Hello 본문 hello 원래 스키마 정의 포함 해야 기존 인덱스를 업데이트할 때 뿐만 아니라 hello 뿐만 아니라 hello 새 필드를 추가 하는 점수 매기기 프로필, CORS 옵션 및 확인 기 있는 경우 수정. Hello 점수 매기기 프로필과 CORS 옵션 수정 하지 않는 경우 hello 인덱스를 만들 때에서 hello 원본을 포함 해야 합니다. 일반적 업데이트에 대 한 최상의 패턴 toouse hello는으로 가져오기 tooretrieve hello 인덱스 정의 수정 하십시오. 다음 PUT으로 업데이트 합니다.

hello 스키마 구문 편의 위해 인덱스 여기에 재현 되어 toocreate를 사용 합니다. 자세한 내용은 [인덱스 만들기](#CreateIndex) 를 참조하세요.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**응답**

요청이 성공적으로 실행되면 “204 콘텐츠 없음”이 반환됩니다.

기본적으로 hello 응답 본문은 비어 있게 됩니다. 그러나 경우 hello, `Prefer` 요청 헤더가 너무 설정 되어`return=representation`, hello 응답 본문에는 업데이트 된 hello 인덱스 정의 대 한 JSON hello 포함 됩니다. 이 경우 hello 성공 상태 코드를 됩니다 "200 확인"입니다.

**사용자 지정 분석기로 인덱스 정의 업데이트**

분석기, 토크나이저, 토큰 필터 또는 문자 필터는 일단 정의한 후에는 수정할 수 없습니다. 새로 추가할 수 있습니다 tooan 기존 인덱스는 경우에 hello `allowIndexDowntime` 플래그가 tootrue hello 인덱스 업데이트 요청에 설정 되어 있습니다. 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

이 작업을 오프 라인으로 인덱스 적어도 몇 초로 인덱싱 및 쿼리를 넣는 참고 toofail를 요청 합니다. Hello 인덱스의 성능 및 쓰기 가용성은 매우 큰 인덱스에 대 한 hello 인덱스를 업데이트 한 후 몇 분 동안 장애가 있는 사용자의 이상일 수 있습니다.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>인덱스 나열
hello **목록 인덱스** 작업 목록을 반환 hello 인덱스의 현재 Azure 검색 서비스에 있습니다.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **목록 인덱스** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: 필수 사항입니다. hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **목록 인덱스** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

아래에는 예제 응답 본문이 나와 있습니다.

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

참고에 관심이 toojust hello 속성 아래로 hello 응답을 필터링 할 수 있습니다. 인덱스 이름 목록만 하려는 경우 OData hello를 사용 하는 예를 들어 `$select` 쿼리 옵션:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

이 경우 위 예제는 hello hello 응답은 다음과 같이 표시 됩니다.

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

많은 인덱스 검색 서비스에 있는 경우에 유용한 기술 toosave 대역폭입니다.

<a name="GetIndex"></a>

## <a name="get-index"></a>인덱스 가져오기
hello **가져올 인덱스** Azure 검색에서 hello 인덱스 정의 가져옵니다.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **가져올 인덱스** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello [인덱스 이름] hello 요청 URI에에서는 인덱스 tooreturn hello 인덱스 컬렉션에서 지정합니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **가져올 인덱스** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

Hello 예제 JSON을 참조에서 [만들고 인덱스를 업데이트할](#CreateUpdateIndexExample) hello 응답 페이로드의 예입니다.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>인덱스 삭제
hello **인덱스 삭제** 작업 Azure 검색 서비스에서 인덱스 및 관련된 문서를 제거 합니다. Hello API 또는 hello 서비스 대시보드에서 hello Azure 포털에서 hello 인덱스 이름을 가져올 수 있습니다. 자세한 내용은 [인덱스 나열](#ListIndexes) 을 참조하세요.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **인덱스 삭제** hello DELETE 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello [인덱스 이름] hello 요청 URI에에서는 인덱스 toodelete hello 인덱스 컬렉션에서 지정합니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: 필수 사항입니다. hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 URL입니다. hello **인덱스 삭제** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘204 콘텐츠 없음’이 반환됩니다.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>인덱스 통계 가져오기
hello **인덱스 통계 가져오기** 작업 hello 현재 인덱스와 저장소 사용량에 대 한 문서 수를 Azure 검색에서 반환 합니다.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> 문서 수와 저장소 크기에 대한 통계는 실시간이 아니라 몇 분 간격으로 수집됩니다. 이 API에서 반환 되는 hello 통계는 최근 인덱싱 작업에 의해 발생 한 변경 내용을 나타내지 않을 수도 있습니다.
> 
> 

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **인덱스 통계 가져오기** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello 요청 URI의에서 [index name] hello hello 지정 된 인덱스에 대 한 hello 서비스 tooreturn 인덱스 통계를 나타냅니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **인덱스 통계 가져오기** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

형식에 따라 hello에 hello 응답 본문은입니다.

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>테스트 분석기
hello **분석 API** 분석기를 토큰으로 텍스트를 중단 하는 방법을 보여 줍니다.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **분석 API** hello POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **분석 API** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.

Hello 인덱스 이름과 hello 서비스 이름 tooconstruct hello 요청 URL 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

또는

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

hello `analyzer_name`, `tokenizer_name`, `token_filter_name` 및 `char_filter_name` hello 인덱스에 대 한 미리 정의 된 또는 사용자 지정 분석기, 토크 나이저, 토큰 필터 및 char 필터의 toobe 유효한 이름을 지정 해야 합니다. 어휘 분석의 hello 프로세스에 대 한 자세한 참조 toolearn [Azure 검색의 분석](https://aka.ms/azsanalysis)합니다.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

형식에 따라 hello에 hello 응답 본문은입니다.

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**분석 API 예제**

**요청**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**응답**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>문서 작업
Azure 검색에서 인덱스 hello 클라우드에 저장 되 고 toohello 서비스 업로드 하는 JSON 문서를 사용 하 여 채워집니다. 업로드 하는 모든 hello 문서 검색 데이터의 hello 모음으로 구성 됩니다. 문서에는 필드가 포함되며, 이러한 필드 중 일부는 문서 업로드 시 검색 용어로 토큰화됩니다. hello `/docs` hello Azure 검색 API에에서 URL 세그먼트는 인덱스의 문서 hello 컬렉션을 나타냅니다. 업로드 같은 hello 컬렉션에서 수행 된 모든 작업, 병합, 삭제 또는 문서를 쿼리 수행 하므로 hello Url은 단일 인덱스의 hello 컨텍스트에서 이러한 작업은 항상 시작에 대 한 `/indexes/[index name]/docs` 지정된 된 인덱스 이름에 대 한 합니다.

응용 프로그램 코드 JSON 문서 tooupload tooAzure 검색을 생성 해야 하거나 사용할 수 있습니다는 [인덱서](https://msdn.microsoft.com/library/dn946891.aspx) tooload 이면 hello 데이터 원본이 Azure Cosmos DB 나 Azure SQL 데이터베이스에 설명 합니다. 일반적으로 인덱스는 사용자가 제공하는 단일 데이터 집합에서 채워집니다.

Toosearch 원하는 각 항목에 대 한 문서에 계획 해야 합니다. 예를 들어 영화 대여 응용 프로그램은 영화당 문서 하나를, 상점 응용 프로그램은 SKU당 문서 하나를, 온라인 교육 과정 응용 프로그램은 과정당 문서 하나를, 리서치 업체는 리포지토리의 학술 문서당 문서 하나를 포함할 수 있습니다.

문서는 하나 이상의 필드로 구성됩니다. 필드는 Azure 검색에서 검색 용어로 토큰화되는 텍스트를 포함할 수 있으며 필터 또는 점수 매기기 프로필에서 사용할 수 있는 토큰화되지 않는 값 또는 텍스트가 아닌 값도 포함할 수 있습니다. hello 이름, 데이터 형식 및 각 필드에 대해 지원 되는 검색 기능에 의해 결정 됩니다 hello 인덱스 스키마. 각 인덱스 스키마의 hello 필드 중 하나는 ID로 지정 해야 하며 각 문서 hello 인덱스에서 해당 문서를 고유 하 게 식별 하는 hello ID 필드에 대 한 값 있어야 합니다. 다른 모든 문서 필드 선택 사항이 며 지정 하지 않으면 기본 tooa null 값 됩니다. Hello 검색 인덱스의 공간을 null 값을 사용 하지 않는 참고 합니다.

문서를 업로드할 수 있습니다, 전에 해야 이미 만든 hello 인덱스 hello 서비스에 있습니다. 이 첫 단계에 대한 자세한 내용은 [인덱스 만들기](#CreateIndex) 를 참조하세요.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>문서 추가, 업데이트 또는 삭제
HTTP POST를 사용하여 지정한 인덱스에서 문서를 업로드, 병합, 병합하거나 업로드 또는 삭제할 수 있습니다. 업데이트의 많은 수에 대 한 문서 (일괄 처리당 문서 too1000) 또는 일괄 처리당 약 16MB를 일괄 처리할 것이 좋습니다.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. HTTP POST를 사용하여 지정한 인덱스에서 문서를 업로드, 병합, 병합하거나 업로드 또는 삭제할 수 있습니다.

hello 요청 URI [index name]에 포함 됩니다. 인덱스 toopost 문서를 지정 합니다. 한 번에만 문서 tooone 인덱스를 게시할 수 있습니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `Content-Type`: 필수 사항입니다. 너무 설정 합니다.`application/json`
* `api-key`: 필수 사항입니다. hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **문서 추가** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

hello hello 요청 본문을 포함 하나 또는 자세한 문서 toobe 인덱싱됩니다. 고유 키로 문서를 식별합니다. 각 문서는 upload, merge, mergeOrupload 또는 delete 작업과 연결됩니다. 업로드 요청 키/값 쌍의 집합으로 hello 문서 데이터를 포함 해야 합니다.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> 문서 키에는 문자, 숫자, 대시("-"), 밑줄("_") 및 등호("=")만 포함될 수 있습니다. 자세한 내용은 [명명 규칙](https://msdn.microsoft.com/library/azure/dn857353.aspx)을 참조하세요.
> 
> 

**문서 작업**

* `upload`: 업로드 작업은 유사 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다. Hello 업데이트 경우에서 모든 필드가 바뀌는 것을 참고 합니다.
* `merge`: 병합 업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다. Hello 문서가 존재 하지 않는 경우 hello 병합 실패 합니다. 병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다. 여기에는 `Collection(Edm.String)`형식 필드가 포함됩니다. 예를 들어 hello 문서 있으면 필드 값을 가진 "tags" `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` "tags" hello "tags" 필드의 최종 값 hello 됩니다 `["economy", "pool"]`합니다. `["budget", "economy", "pool"]`이 되지 **않습니다**.
* `mergeOrUpload`: 처럼 동작 `merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우. Hello 문서 존재 하지 않는 경우 처럼 동작 `upload` 새 문서를 사용 합니다.
* `delete`: 삭제 hello 인덱스에서 hello 지정 된 문서를 제거합니다. 모든 필드에서 지정 하는 참고는 `delete` hello 키 필드 이외의 작업은 무시 됩니다. 문서에서 개별 필드 tooremove 사용 `merge` 대신 하 고 간단 하 게 hello 필드 명시적으로 설정 너무`null`합니다.

**응답**

작업 성공 시의 응답에는 상태 코드 200 (OK)가 반환됩니다. 이 응답은 모든 항목이 올바르게 인덱싱되었음을 의미합니다. 이 hello로 표시 `status` tootrue hello 뿐만 아니라 모든 항목에 대 한 설정 속성 `statusCode` tooeither 201 (문서에 대 한 새로 업로드 된) 또는 200 (병합 또는 삭제 된 문서)에 대 한 설정 속성:

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

하나 이상의 항목이 성공적으로 인덱싱되지 않은 경우 상태 코드 207(다중 상태)이 반환됩니다. 인덱싱되지 않은 된 항목은 hello `status` toofalse 필드를 설정 합니다. hello `errorMessage` 및 `statusCode` 속성 인덱싱 오류 hello에 대 한 hello 이유를 표시 합니다.

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

다음 표에서 hello hello 다양 한 문서별 hello 응답에서 반환 될 수 있는 상태 코드에 설명 합니다. 임시 오류 상태를 나타내는 다른 동안 hello 요청 자체의 문제를 나타낼 일부 참고 합니다. hello 후자 지연 후에 다시 시도해 야 합니다.

<table style="font-size:12">
    <tr>
        <th>상태 코드</th>
        <th>의미</th>
        <th>재시도 가능</th>
        <th>참고 사항</th>
    </tr>
    <tr>
        <td>200</td>
        <td>문서가 성공적으로 수정되었거나 삭제되었습니다.</td>
        <td>해당 없음</td>
        <td>삭제 작업은 <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>입니다. 즉, 문서 키 hello 인덱스에 없는 경우에 삭제 작업은 해당 키가 있는 발생 합니다는 200 상태 코드입니다.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>문서를 성공적으로 만들었습니다.</td>
        <td>해당 없음</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>인덱싱되는 것을 방해 하는 hello 문서에 오류가 발생 했습니다.</td>
        <td>아니요</td>
        <td>무엇이 잘못 된 hello 문서 hello에 대 한 응답 hello 오류 메시지가 표시 됩니다.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>hello 인덱스에 키를 제공 하는 hello 존재 하지 않아 hello 문서를 병합할 수 없습니다.</td>
        <td>아니요</td>
        <td>새 문서를 만들기 때문에 업로드에 이 오류가 발생하지 않으며 <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>이므로 삭제에 오류가 발생하지 않습니다.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Tooindex 문서를 시도할 때 버전 충돌이 검색 되었습니다.</td>
        <td>예</td>
        <td>동시에 두 번 이상 문서 동일 tooindex hello 려 할 경우 발생할 수 있습니다.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>hello 인덱스 이므로 일시적으로 사용할 수 없습니다 'hello 'allowIndexDowntime 플래그 집합 too'true로 업데이트 되었습니다 '.</td>
        <td>예</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>검색 서비스 tooheavy 부하 가능 인해 일시적으로 사용할 수 없는 경우</td>
        <td>예</td>
        <td>이 경우 다시 시도 하기 전에 대기 해야 할 코드 또는 hello 서비스 사용 불가 연장 될 위험이 있습니다.</td>
    </tr>
</table> 

**참고**: 한 가지 가능한 이유 hello 시스템의 부하가 클라이언트 코드를 207 응답이 자주에서 발생 합니다. Hello를 확인 하 여이 확인할 수 있습니다 `statusCode` 503에 대 한 속성. Hello 대/소문자, 이것이 권장 ***인덱싱 요청 제한***합니다. 그렇지 않은 경우 인덱싱 트래픽이 감소 하지 hello 시스템 503 오류가 발생 한 모든 요청을 거부 시작할 수 있습니다.

상태 코드 429 hello 인덱스 당 문서 수의 할당량이 초과 되었다는 것을 나타냅니다. 이 경우에는 새 인덱스를 만들거나 업그레이드를 통해 용량 제한을 높여야 합니다.

**예제:**

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>문서 검색
A **검색** 작업이 GET 또는 POST 요청으로 발생 하 고 일치 하는 문서를 선택 하는 것에 대 한 hello 조건을 제공 하는 매개 변수를 지정 합니다.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**대신 toouse 게시 하는 경우**

HTTP GET toocall hello를 사용 하는 경우 **검색** API 해야 toobe 인식 hello 요청 URL의 hello 길이 8KB를 초과할 수 없습니다. 이 크기는 일반적으로 대부분의 응용 프로그램에서 충분합니다. 그러나 일부 응용 프로그램은 매우 큰 쿼리 또는 OData 필터 식을 생성합니다. 이러한 응용 프로그램의 경우 GET보다 더 많은 필터와 쿼리를 허용할 수 있는 HTTP POST를 사용하는 것이 좋습니다. POST, 용어 또는 쿼리에서 절 hello 수와 hello을 제한 하 hello 원시 쿼리 POST에 대 한 hello 요청 크기 제한 약 16MB 이므로의 hello 크기가 아니라 요소인 합니다.

> [!NOTE]
> Hello POST 요청 크기 제한의 용량이 클 경우에 검색 쿼리 및 필터 식을 임의의 복잡 한 수 없습니다. 검색 쿼리 및 필터 복잡성 제한에 대한 자세한 내용은 [Lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx) 및 [OData 식 구문](https://msdn.microsoft.com/library/dn798921.aspx)을 참조하세요.
> 
> 

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **검색** hello GET 또는 POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello 요청 URI는 인덱스 tooquery hello 매개 변수와 일치 하는 모든 문서에 대 한을 지정 합니다. GET 요청의 경우 hello hello 쿼리 문자열에 대해 매개 변수를 지정 하 고 hello 경우 POST의 본문 hello 요청에 요청 합니다.

모범 사례로 GET 요청을 만들 때, 기억 너무[URL로 인코드할](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) 특정 쿼리 매개 변수를 호출할 때 REST API를 직접 hello 합니다. **검색** 작업의 경우 다음이 포함됩니다.

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

URL 인코딩은 위의 쿼리 매개 변수는 hello에만 권장 됩니다. 실수로 URL로 인코딩할 수 있습니다 (다음의 모든 hello?)는 전체 쿼리 문자열 hello, 요청이 중단 됩니다.

또한 URL 인코딩은 필요한 경우에 REST API를 사용 하 여 직접 가져올 hello를 호출 합니다. 호출할 때 필요한은 URL 인코딩 없이 **검색** POST를 사용 하 여 hello를 사용 하는 경우 [.NET 클라이언트 라이브러리](https://msdn.microsoft.com/library/dn951165.aspx), URL 인코딩을 처리 합니다.

<a name="SearchQueryParameters"></a>
**쿼리 매개 변수**

**검색** 은 쿼리 조건을 제공하고 검색 동작을 지정하는 여러 매개 변수를 허용합니다. 호출할 때 이러한 매개 변수 hello URL에 쿼리 문자열을 제공 **검색** GET을 통해 및를 호출할 때 hello 요청 본문의 JSON 속성으로 **검색** POST 통해. hello 일부 매개 변수의 구문에는 GET 및 POST 간에 약간 다릅니다. 이러한 차이가 아래에 나와 있습니다.

`search=[string]`(선택 사항)-hello에 대 한 텍스트 toosearch 합니다. `searchFields`를 지정하지 않으면 기본적으로 모든 `searchable` 필드가 검색됩니다. 검색할 때 `searchable` 필드, hello 검색 텍스트 자체가 토큰화 되므로 여러 용어를 공백으로 구분할 수 있습니다 (예: `search=hello world`). 모든 용어를 사용 하 여 toomatch `*` (이 기능은 유용 부울 필터 쿼리에서). 효과가 너무 설정 같음 hello에이 매개 변수를 생략`*`합니다. 참조 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx) hello 검색 구문에 사양에 대 한 합니다.

* **참고**: hello 결과 수 놀라운를 통해 쿼리할 때 `searchable` 필드입니다. 숫자, 등에서 아포스트로피, 쉼표와 같은 논리 toohandle의 경우 일반적인 tooEnglish 텍스트를 포함 하는 hello 토크 나이저입니다. 예를 들어 `search=123,456` 영어에서 큰 수의 천 구분 기호로 쉼표를 사용 하므로 hello 개별 용어인 123과 456, 보다는 단일 용어 123456 일치 합니다. 이러한 이유로 tooseparate 용어 문장 부호가 아닌 공백을 hello에 사용할 수 있는 권장 `search` 매개 변수입니다.

`searchMode=any|all`(선택 사항 너무 기본값`any`)-hello 검색 용어 중 일부 또는 모두 일치 기준으로 하는 순서 toocount hello 문서의 일치 해야 하는지 여부입니다.

`searchFields=[string]`(선택 사항)-hello 목록을 쉼표로 구분 된 필드 이름 toosearch hello에 대 한 텍스트를 지정 합니다. 대상 필드는 `searchable`로 표시되어야 합니다.

`queryType=simple|full`(선택 사항 너무 기본값`simple`)와 같은 기호에 대 한 허용 하는 간단한 쿼리 언어를 사용 하 여 텍스트를 "단순" 너무 검색 하는 집합을 해석할 때-+, * 및 ""입니다. 쿼리는 기본적으로 각 문서의 모든 검색 가능 필드(또는 `searchFields`에 나타난 필드)에 걸쳐 평가됩니다. Hello 쿼리 유형을 너무 설정 되 면`full` 검색 텍스트 필드별 및가 중 검색이 허용 하는 hello Lucene 쿼리 언어를 사용 하 여 해석 됩니다. 참조 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx) 및 [Lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx) hello 검색 구문에 사양에 대 한 합니다. 

> [!NOTE]
> 범위 검색의 hello Lucene $filter 유사한 기능을 제공 하는 대신 쿼리 언어를 사용할 수 없습니다.
> 
> 

`moreLikeThis=[key]`(선택) **중요:** 이 기능은 `2015-02-28-Preview`에서만 사용할 수 있습니다. 이 옵션은 hello 텍스트 검색 매개 변수를 포함 하는 쿼리에 사용할 수 없습니다 `search=[string]`합니다. hello `moreLikeThis` 매개 변수는 hello 문서 키로 지정 된 유사한 toohello 문서는 문서를 찾습니다. 검색 요청으로 설정 되는 경우 `moreLikeThis`, 검색 용어 목록을 hello 빈도 및 흔히 볼 hello 소스 문서에서 조건에 따라 생성 됩니다. 이러한 용어가 사용 되는 toomake hello 요청 합니다. 기본적으로 모든 내용을 hello `searchable` 필드가 하지 않는 한 것으로 간주 `searchFields` 가 사용 되는 toorestrict 검색 되는 필드입니다.  

`$skip=#`(선택 사항)-검색 수가 hello tooskip; 결과 100, 000 보다 클 수 없습니다. Tooscan 문서 순서에 필요한 경우 있지만 사용할 수 없습니다 `$skip` toothis 제한으로 인해 사용 하는 것이 좋습니다 `$orderby` 완전히 정렬 된 키에 및 `$filter` 범위를 가진 대신를 쿼리해야 합니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$skip` 대신 `skip`입니다.
> 
> 

`$top=#`(선택 사항)-tooretrieve 결과 하는 hello 수 검색 합니다. 이와 함께에서 사용할 수 있습니다 `$skip` 검색 결과의 tooimplement 클라이언트 쪽 페이징 합니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$top` 대신 `top`입니다.
> 
> 

`$count=true|false`(선택 사항 너무 기본값`false`)-toofetch hello 총 결과 수 있는지 여부를 지정 합니다. 이 값은 hello와 일치 하는 모든 문서 hello 개수 `search` 및 `$filter` 매개 변수를 무시 하 고 `$top` 및 `$skip`합니다. 이 값을 너무 설정`true` 성능 영향을 줄 수 있습니다. 참고가 반환 하는 hello 개수는 근사값입니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$count` 대신 `count`입니다.
> 
> 

`$orderby=[string]`(선택 사항)-toosort hello 쉼표로 구분 된 식 결과의 목록입니다. 각 식은 필드 이름 또는 호출 toohello 가능 `geo.distance()` 함수입니다. 각 식은 올 수 있는 `asc` tooindicated 오름차순 및 `desc` 내림차순 tooindicate 합니다. hello 기본값은 오름차순입니다. 동률 문서의 hello 일치 점수에 의해 손상 됩니다. 하지 않으면 `$orderby` hello 기본 정렬 순서는 문서 일치 점수 기준 내림차순 지정 됩니다. `$orderby`절은 32개로 제한됩니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$orderby` 대신 `orderby`입니다.
> 
> 

`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다. 지정 하지 않으면 hello 스키마에서 검색 가능한로 표시 된 모든 필드가 포함 됩니다. 이 매개 변수를 너무 설정 하 여 모든 필드를 명시적으로 요청할 수 있습니다`*`합니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$select` 대신 `select`입니다.
> 
> 

`facet=[string]`(0 개 이상)-하 여 필드 toofacet 합니다. Hello 문자열 매개 변수 toocustomize hello 패싯 쉼표로 구분 된 00z를 포함할 수 있습니다는 필요에 따라 `name:value` 쌍입니다. 유효한 매개 변수는 다음과 같습니다.

* `count` (패싯 용어의 최대 개수, 기본값은 10). 최대값 없음 있지만 값이 높을수록 hello 패싯 필드에 고유 용어가 많이 포함 하는 경우에 특히 해당 성능 저하를 유발 합니다.
  * 예를 들어: `facet=category,count:5` 패싯 결과에서 상위 5 개 범주를 hello 가져옵니다.  
  * **참고**: 경우 hello `count` 매개 변수는 고유 용어의 hello 번호 보다 작은, hello 결과가 정확 하 게 불완전할 수 있습니다. 이 패싯 쿼리가 여러 분할으로 분산 된 toohello 방식 때문입니다. 증가 `count` 일반적으로 증가 hello 정확도 hello 용어 개수의 있지만 성능은 저하 됩니다.
* `sort`(중 하나 `count` toosort *내림차순* 개수 별로 `-count` toosort *오름차순* 개수 별로 `value` toosort *오름차순* 값, 또는 `-value` toosort *내림차순* 값별로)
  * 예를 들어: `facet=category,count:3,sort:count` 가져옵니다 hello 각 도시 이름과 사용 하 여 문서의 hello 번호로 순서를 내림차순으로 패싯 결과의 상위 세 가지 범주가 있습니다. 예를 들어 hello 상위 3 개 범주가 Budget, Motel, Luxury 이며 각는 및 적중 수가 5, 6, 및 4, 않으면 hello 버킷 됩니다 hello 순서로 Motel, Budget, Luxury 합니다.
  * 예: `facet=rating,sort:-value` 는 값을 기준으로 내림차순으로 정렬된 가능한 모든 등급의 버킷을 생성합니다. 예를 들어 hello 등급 인 1 too5에서 5, 4, 3, 2, 1, 문서 각 등급에 일치 하는 관계 없이 hello 버킷 정렬 됩니다.
* `values`(파이프로 구분된 숫자 또는 패싯 항목 값의 동적 집합을 지정하는 `Edm.DateTimeOffset` 값)
  * 예를 들어: `facet=baseRate,values:10|20` 세 개의 버킷이 생성:, 및 20, 20 이상의 용 점을 포함 하지 toobut 10에 대 한 10 toobut 기본 숙박료가 0에 대 한 합니다.
  * 예: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z`는 각각 2010년 2월 이전에 리노베이션된 호텔과 2010년 2월 1일 이후에 리노베이션된 호텔에 대한 버킷 2개를 생성합니다.
* `interval`(숫자의 경우 0보다 큰 정수 간격 또는 날짜/시간 값의 경우 `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year`)
  * 예: `facet=baseRate,interval:100`은 기본 요금 범위 100을 기준으로 버킷을 생성합니다. 예를 들어 기본 요금이 모두 $60에서 $600 사이에 속한 경우 0-100, 100-200, 200-300, 300-400, 400-500 및 500-600에 대한 버킷이 생성됩니다.
  * 예: `facet=lastRenovationDate,interval:year`는 호텔이 리노베이션된 각 연도에 대해 하나의 버킷을 생성합니다.
* `timeoffset` ([+-]hh:mm, [+-]hhmm, 또는 [+-]hh) `timeoffset`은 선택 사항입니다. Hello와 결합할 수만 있습니다 `interval` 옵션을 선택한 경우에만 적용 된 tooa 필드 형식의 `Edm.DateTimeOffset`합니다. hello 값에 대 한 hello UTC 시간 오프셋된 tooaccount 시간 경계 설정 지정 합니다.
  * 예를 들어: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` 사용 하 여 hello 01시: 00 UTC (hello 대상 표준 시간대에서 자정)에서 시작 하는 일 경계
* **참고**: `count` 및 `sort` 에 결합할 수 있습니다 hello 같은 패싯 사양 있지만 함께 사용할 수 없는 `interval` 또는 `values`, 및 `interval` 및 `values` 함께 결합할 수 없습니다.
* **참고**: `timeoffset`을 지정하지 않은 경우 날짜 시간의 간격 패싯은 UTC 시간을 기준으로 계산됩니다. 예를 들어:에 대 한 `facet=lastRenovationDate,interval:day`, hello 일 경계 00시: 00 UTC에서 시작 합니다. 

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `facet` 대신 `facets`입니다. 또한 문자열의 JSON 배열로 지정할 수도 있습니다. 여기서 각 문자열은 별도의 패싯 식입니다.
> 
> 

`$filter=[string]` (선택) - 표준 OData 구문의 구조화된 검색 식입니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$filter` 대신 `filter`입니다.
> 
> 

`highlight=[string]` (선택) - 적중 항목을 강조 표시하는 데 사용되는 쉼표로 구분된 필드 이름 집합입니다. `searchable` 필드만 적중 항목 강조 표시에 사용할 수 있습니다.

`highlightPreTag=[string]`(선택 사항 너무 기본값`<em>`)-태그 toohit 밝은 앞에 추가 하는 문자열입니다. `highlightPostTag`로 설정해야 합니다.

> [!NOTE]
> 호출할 때 **검색** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.
> 
> 

`highlightPostTag=[string]`(선택 사항 너무 기본값`</em>`)-toohit 하이라이트를 추가 하는 문자열 태그입니다. `highlightPreTag`로 설정해야 합니다.

> [!NOTE]
> 호출할 때 **검색** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.
> 
> 

`scoringProfile=[string]`(선택 사항)-점수 매기기 프로필 tooevaluate의 hello 이름을 순서 toosort hello 결과에 일치 하는 문서에 대 한 점수와 일치 합니다.

`scoringParameter=[string]`점수 매기기 함수에 정의 된 각 매개 변수에 대해 hello 값을 나타냅니다 (0 개 이상)-(예를 들어 `referencePointParameter`) hello 형식을 사용 하 여 `name-value1,value2,...`합니다.

* 예를 들어 점수 매기기 프로필 hello 함수를 정의 하는 경우 "mylocation" hello 쿼리 문자열 옵션 라는 매개 변수를 것 `&scoringParameter=mylocation--122.2,44.8`합니다. 첫 번째 대시 hello hello 두 번째 대시 hello 첫 번째 값 (이 예제의 경도)의 일부인 동안 hello 값 목록에서 hello 이름과 구분 합니다.
* 점수 매기기 매개 변수 태그에 대 한 승격 하는 포함 될 수 있습니다 쉼표와 같은 단일 따옴표를 사용 하 여 hello 목록에서 이러한 값 이스케이프 수 있습니다. Hello 값 자체 작은따옴표가 들어 있으면 이중 이스케이프 확인할 수 있습니다.
  * 예를 들어 "mytag" 라는 매개 변수를 승격 하는 태그를가 하 고 tooboost hello 태그에 값 "Hello, O'Brien" 및 "Smith", hello 쿼리 문자열 옵션 것 `&scoringParameter=mytag-'Hello, O''Brien',Smith`합니다. 따옴표는 쉼표를 포함하는 값에만 필요합니다.

> [!NOTE]
> POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `scoringParameter` 대신 `scoringParameters`입니다. 또한 문자열의 JSON 배열로 지정할 수도 있습니다. 여기서 각 문자열은 별도의 `name-values` 쌍입니다.
> 
> 

`minimumCoverage`(선택 사항 기본값 too100)-0과 100 쿼리 toobe hello에 대 한 순서 대로 검색 쿼리에서 포함 되어야 하는 hello 인덱스의 hello 백분율을 나타내는 사이의 숫자를 성공으로 보고 합니다. 기본적으로 전체 인덱스 hello 사용할 수 있어야 하거나 `Search` 503 HTTP 상태 코드가 반환 됩니다. 설정한 경우 `minimumCoverage` 및 `Search` 성공 하면 HTTP 200을 반환 하 고 포함 한 `@search.coverage` hello에 대 한 응답 hello 쿼리에 포함 된 hello 인덱스의 hello 백분율을 나타내는 값입니다.

> [!NOTE]
> 이 매개 변수 tooa 값 100 검색 가용성 복제본을 하나만 사용 하 여 서비스에 대해서도 보장 하는 데 유용할 수 있습니다 보다 낮게 설정 합니다. 그러나 일부 일치 하는 문서가 toobe hello 검색 결과 보장 됩니다. 검색 회수는 가용성, 보다 더 중요 한 tooyour 응용 프로그램을 경우 최상의 tooleave `minimumCoverage` 100 기본값으로 지정 합니다.
> 
> 

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

참고:이 작업에 대 한 hello `api-version` 호출 여부에 관계 없이 hello URL에 쿼리 매개 변수로 지정 **검색** GET 또는 POST입니다.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 URL입니다. hello **검색** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

GET의 경우: 없음.

POST의 경우:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**부분 검색 응답의 연속 작업**

경우에 따라 Azure 검색 모든 hello 단일 검색 응답에서 요청 된 결과 반환할 수 없습니다. Hello 쿼리 지정 하 여 너무 많은 문서를 요청 하는 경우와 같은 다양 한 이유로 발생할 수 있습니다 `$top` 에 대 한 값을 지정 하거나 `$top` 는 너무 큽니다. 이러한 경우 Azure 검색 hello에 포함할 `@odata.nextLink` hello 응답 본문에 주석 및 `@search.nextPageParameters` POST 요청을 것입니다. 검색 요청 tooget hello 다음의 다른 부분 hello 검색 응답의 이러한 주석 tooformulate hello 값을 사용할 수 있습니다. 이 라고는 ***연속*** 원래 검색 요청 hello 및 hello 주석은 일반적으로 호출 ***연속 토큰***합니다. 참조 [hello 감시할](#SearchResponse) hello 구문 이러한 주석의 및 나타나는 hello 응답 본문에 대 한 자세한 내용은 합니다. 

hello Azure 검색에서 연속 토큰을 반환할 수 있습니다는 이유 원인은 구현의 및 제목 toochange입니다. 강력한 클라이언트에는 항상 준비 toohandle 예상 보다 더 적은 문서가 반환 됩니다 대 한 경우 연속 토큰이 포함된 toocontinue 문서를 검색 해야 합니다. 또한 사용 해야 하는 hello 순서 toocontinue에 hello 원래 요청으로 동일한 HTTP 메서드입니다. 예를 들어 GET 요청을 보냈으면 보내는 모든 연속 작업 요청에서도 GET을 사용해야 합니다(POST도 마찬가지).

<a name="SearchResponse"></a>
**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**예제:**

Hello에서 추가 예제를 찾을 수 있습니다 [Azure 검색의 OData 식 구문](https://msdn.microsoft.com/library/azure/dn798921.aspx) 페이지.

1)    인덱스 검색 hello 날짜별으로 내림차순으로 정렬 합니다.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    패싯 검색에서 hello 색인을 검색 하 고 특정 범위의 baseRate 항목 뿐만 아니라 범주, 등급, 태그, 패싯 검색:

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    필터를 사용 하 여 범위를 좁힐 hello 이전 패싯 쿼리 결과 hello 사용자가 클릭 한 후 rating 3 및 "Motel" 범주:

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) 패싯 검색에서 쿼리에 반환되는 고유 항목의 상한을 설정합니다. hello 기본값은 10 이지만 늘리거나 hello를 사용 하 여이 값을 줄일 수 `count` hello에 대 한 매개 변수 `facet` 특성:

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    의 특정 필드 내 인덱스 검색 hello 예를 들어 언어별 필드:

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) 여러 필드에서 hello 인덱스를 검색 합니다. 예를 들어 저장할 수 있으며 모든 내 여러 언어로 쿼리 검색 가능한 필드 hello 같은 인덱스입니다.  영어와 프랑스어 설명에에서 함께 존재 hello 동일한 경우 문서를 반환할 수 있습니다 임의로 또는 모두에 hello 쿼리 결과:

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

한 번에 하나의 인덱스만 쿼리할 수 있습니다. 한 번에 하나의 tooquery 하려는 경우가 아니면 각 언어에 대해 여러 인덱스를 만들지 마십시오.

7)    페이징-항목의 Get hello 첫 페이지 (페이지 크기는 10):

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    페이징-항목의 Get hello 두 번째 페이지 (페이지 크기는 10):

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    특정 필드 집합을 검색합니다.

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  특정 필터 식과 일치하는 문서를 검색합니다.

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Hello 색인을 검색 하 고 적중된 항목이 강조 표시 된 조각 반환

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Hello 인덱스를 검색 하는 참조 위치에서 가까운 toofarther에서 순으로 정렬 하는 문서를 반환 합니다.

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) 거리 점수 매기기 설명한 "geo" 라는 점수 매기기 프로필은 검색 hello 인덱스 가정 하는 경우, "currentLocation" 및 포함 된 매개 변수 정의 하나 라는 하나의 매개 변수 정의

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) 사용 하 여 hello 인덱스에서 문서를 찾습니다 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx)합니다. 이 쿼리 hello "comfort" 및 "위치" 있지만 "motel" 하지 검색 가능한 필드에 포함 하는 호텔을 반환 합니다.

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Hello 사용 `searchMode=all` 위에 있습니다. 이 매개 변수를 포함 하 여 기본값을 재정의 hello의 `searchMode=any`등과는 `-motel` "AND NOT" 대신 "OR NOT"을 의미 합니다. 없이 `searchMode=all`"OR NOT"는 검색 결과 제한 하는 것이 아니라 확장 얻게 하 고이 비 직관적인 toosome 사용자가 수 있습니다.

15) 사용 하 여 hello 인덱스에서 문서를 찾습니다 [lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx)합니다. 이 쿼리는 호텔 hello 범주 필드 hello 용어 "budget" 및 "리 최근에" hello 구가 포함 된 모든 검색 가능한 필드를 포함 하는 위치를 반환 합니다. Hello 용어 부스트 값 (3)의 결과 "리 최근에" hello 구가 포함 된 문서는 순위가 더 높은

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>문서 조회
hello **문서 조회** Azure 검색에서 문서를 검색 하는 작업입니다. 사용자가 특정 검색 결과 클릭 하 고 해당 문서에 대 한 특정 세부 정보를 toolook 하려는 경우에 유용 합니다.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **문서 조회** 요청을 다음과 같이 생성할 수 있습니다.

    GET /indexes/[index name]/docs/key?[query parameters]

또는 hello 기존의 OData 구문을 키 조회에 사용할 수 있습니다.

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

hello 요청 URI [index name]에 포함 됩니다. [key], 인덱스에서 문서 tooretrieve를 지정 하 고 있습니다. 한 번에 하나의 문서만 가져올 수 있습니다. 사용 하 여 **검색** tooget 단일 요청에서 여러 문서입니다.

**쿼리 매개 변수**

`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다. 지정 되지 않았거나 너무 설정 하는 경우`*`, hello 스키마에서 검색 가능한 것으로 표시 하는 모든 필드가 hello 프로젝션에 포함 됩니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

참고:이 작업에 대 한 hello `api-version` 쿼리 매개 변수로 지정 됩니다.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 URL입니다. hello **문서 조회** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**예제**

'2' 키를 가진 hello 문서 조회

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

OData 구문을 사용 하 여 ' 3' 키를 가진 조회 hello 문서:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>문서 수 계산
hello **문서 수 계산** hello 수 검색 인덱스의 문서를 검색 하는 작업입니다. hello `$count` 구문 hello OData 프로토콜의 일부입니다.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **문서 수 계산** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello 요청 URI의에서 [index name] hello hello 서비스 tooreturn 모든 항목의 수 hello 지정 된 인덱스의 문서 컬렉션 hello에에서 지시합니다.

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `Accept`:이 값을 너무 설정 해야`text/plain`합니다.
* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 URL입니다. hello **문서 수 계산** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

없음.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

hello 응답 본문을 일반 텍스트로 서식이 지정 된 정수로 hello 개수 값을 포함 합니다.

<a name="Suggestions"></a>

## <a name="suggestions"></a>제안
hello **제안** 부분 검색 입력을 기준으로 제안을 검색 하는 작업입니다. 일반적으로 사용자가 검색 용어를 입력 하는 대로 검색 상자 tooprovide 미리 입력 제안에 사용 됩니다.

제안 요청 대상 문서를 제공 하기 위한 것, 동일한 입력을 검색 하므로 hello를 제안 된 후보 문서가 여러 개이면 hello와 일치 하는 경우에 텍스트를 반복 될 수 있습니다. 사용할 수 있습니다 `$select` tooretrieve 다른 문서 필드 (hello 문서 키 포함)는 문서는 각 제안에 대 한 hello 원본 알 수 있도록 합니다.

**제안** 작업이 GET 또는 POST 요청으로 발생합니다.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**대신 toouse 게시 하는 경우**

HTTP GET toocall hello를 사용 하는 경우 **제안** API 해야 toobe 인식 hello 요청 URL의 hello 길이 8KB를 초과할 수 없습니다. 이 크기는 일반적으로 대부분의 응용 프로그램에서 충분합니다. 그러나 일부 응용 프로그램은 매우 큰 쿼리, 특히 OData 필터 식을 생성합니다. 이러한 응용 프로그램의 경우 GET보다 더 많은 필터를 허용할 수 있는 HTTP POST를 사용하는 것이 좋습니다. POST, 필터에서 절 hello 수는 hello 제한 요소를 POST에 대 한 hello 요청 크기 제한 약 16MB 이므로 hello 원시 필터 문자열의 크기를 hello 하지 않습니다.

> [!NOTE]
> Hello POST 요청 크기 제한의 용량이 클 경우에 필터 식은 복잡 한 일 수 없습니다. 필터 복잡성 제한에 대한 자세한 내용은 [OData 식 구문](https://msdn.microsoft.com/library/dn798921.aspx) 을 참조하세요.
> 
> 

**요청**

서비스 요청에는 HTTPS를 사용해야 합니다. hello **제안** hello GET 또는 POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.

hello 요청 URI에는 hello 인덱스 tooquery hello 이름을 지정합니다. Hello 부분적으로 입력된 된 검색 용어도 등의 매개 변수는 GET 요청의 경우 hello hello 쿼리 문자열에 지정 된 한 hello 경우 POST의 본문 hello 요청에 요청 합니다.

모범 사례로 GET 요청을 만들 때, 기억 너무[URL로 인코드할](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) 특정 쿼리 매개 변수를 호출할 때 REST API를 직접 hello 합니다. **제안** 작업의 경우 다음이 포함됩니다.

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

URL 인코딩은 위의 쿼리 매개 변수는 hello에만 권장 됩니다. 실수로 URL로 인코딩할 수 있습니다 (다음의 모든 hello?)는 전체 쿼리 문자열 hello, 요청이 중단 됩니다.

또한 URL 인코딩은 필요한 경우에 REST API를 사용 하 여 직접 가져올 hello를 호출 합니다. 호출할 때 필요한은 URL 인코딩 없이 **제안** POST를 사용 하 여 hello를 사용 하는 경우 [.NET 클라이언트 라이브러리](https://msdn.microsoft.com/library/dn951165.aspx), URL 인코딩을 처리 합니다.

**쿼리 매개 변수**

**제안** 은 쿼리 조건을 제공하고 검색 동작을 지정하는 여러 매개 변수를 허용합니다. 호출할 때 이러한 매개 변수 hello URL에 쿼리 문자열을 제공 **제안** GET을 통해 및를 호출할 때 hello 요청 본문의 JSON 속성으로 **제안** POST 통해. hello 일부 매개 변수의 구문에는 GET 및 POST 간에 약간 다릅니다. 이러한 차이가 아래에 나와 있습니다.

`search=[string]`-hello 검색 텍스트 toouse toosuggest 쿼리 합니다. 최소 1자가 되어야 하며 100자를 넘지 않아야 합니다.

`highlightPreTag=[string]`(선택 사항)-toosearch 적중 항목 앞에 추가 하는 문자열 태그입니다. `highlightPostTag`로 설정해야 합니다.

> [!NOTE]
> 호출할 때 **제안** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.
> 
> 

`highlightPostTag=[string]`(선택 사항)-toosearch 적중 항목을 추가 하는 문자열 태그입니다. `highlightPreTag`로 설정해야 합니다.

> [!NOTE]
> 호출할 때 **제안** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.
> 
> 

`suggesterName=[string]`-hello에 지정 된 hello hello 확인 기 이름을 `suggesters` hello 인덱스 정의의 일부인 컬렉션입니다. 이 `suggester` 에 따라 제안된 쿼리 용어를 검색할 필드가 결정됩니다. 자세한 내용은 [확인기](#Suggesters) 를 참조하세요.

`fuzzy=[boolean]`(옵션, 기본값 = false)-설정 된 경우 tootrue이 API는 제안을 찾습니다 hello 검색 텍스트에 대체 되었거나 누락 된 문자는 경우에 합니다. 이 경우 일부 시나리오에서는 검색 환경이 개선되지만, 유사 제안 검색 속도가 느려지며 리소스가 더 많이 사용되므로 성능은 저하됩니다.

`searchFields=[string]`(선택 사항)-hello 목록을 쉼표로 구분 된 필드 이름 toosearch hello에 대 한 검색 텍스트를 지정 합니다. 대상 필드가 제안을 사용하도록 설정되어 있어야 합니다.

`$top=#`(옵션, 기본값 = 5)-hello 제안 tooretrieve의 수입니다. 값은 1~100 사이의 숫자여야 합니다.

> [!NOTE]
> POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$top` 대신 `top`입니다.
> 
> 

`$filter=[string]`(선택 사항)-제안에 대 한 hello 문서를 필터링 하는 식으로 간주 합니다.

> [!NOTE]
> POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$filter` 대신 `filter`입니다.
> 
> 

`$orderby=[string]`(선택 사항)-toosort hello 쉼표로 구분 된 식 결과의 목록입니다. 각 식은 필드 이름 또는 호출 toohello 가능 `geo.distance()` 함수입니다. 각 식은 올 수 있는 `asc` tooindicated 오름차순 및 `desc` 내림차순 tooindicate 합니다. hello 기본값은 오름차순입니다. `$orderby`절은 32개로 제한됩니다.

> [!NOTE]
> POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$orderby` 대신 `orderby`입니다.
> 
> 

`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다. 지정 하지 않으면 문서 키만 hello 및 제안 텍스트가 반환 됩니다. 이 매개 변수를 너무 설정 하 여 모든 필드를 명시적으로 요청할 수`*`합니다.

> [!NOTE]
> POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$select` 대신 `select`입니다.
> 
> 

`minimumCoverage`(선택 사항 기본값 too80)-0과 100 hello 쿼리 toobe 되려면에서 제안 쿼리에서 포함 되어야 하는 hello 인덱스의 hello 백분율을 나타내는 사이의 숫자를 성공으로 보고 합니다. 기본적으로 hello 인덱스의 80% 이상을 사용할 수 있어야 하거나 `Suggest` 503 HTTP 상태 코드가 반환 됩니다. 설정한 경우 `minimumCoverage` 및 `Suggest` 성공 하면 HTTP 200을 반환 하 고 포함 한 `@search.coverage` hello에 대 한 응답 hello 쿼리에 포함 된 hello 인덱스의 hello 백분율을 나타내는 값입니다.

> [!NOTE]
> 이 매개 변수 tooa 값 100 검색 가용성 복제본을 하나만 사용 하 여 서비스에 대해서도 보장 하는 데 유용할 수 있습니다 보다 낮게 설정 합니다. 그러나 일부 일치 하는 제안은 toobe hello 결과 보장 됩니다. 회수 가용성, 다음의 모범 하지 toolower 보다 더 중요 한 tooyour 응용 프로그램인 경우 `minimumCoverage` 기본값인 80 아래 합니다.
> 
> 

`api-version=[string]` (필수). hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다. 자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.

참고:이 작업에 대 한 hello `api-version` 호출 여부에 관계 없이 hello URL에 쿼리 매개 변수로 지정 **제안** GET 또는 POST입니다.

**요청 헤더**

hello 목록 다음 필요한 hello와 선택적 요청 헤더를 설명 합니다.

* `api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 URL입니다. hello **제안** 요청 hello로 관리자 키 또는 쿼리 키를 지정할 수 `api-key`합니다.

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

**요청 본문**

GET의 경우: 없음.

POST의 경우:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Hello 프로젝션 옵션을 사용 하는 tooretrieve 필드 hello 배열의 각 요소에 포함 됩니다.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**예제**

Hello 부분 검색 입력 'l u x' 인 제안 5 개 검색

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
