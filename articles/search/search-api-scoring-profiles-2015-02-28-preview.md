---
title: "aaaScoring 프로필 (Azure 검색 REST API 버전 2015-02-28-미리 보기) | Microsoft Docs"
description: "Azure 검색은 사용자가 정의한 점수 매기기 프로필을 기초로 순위의 결과를 조정할 수 있도록 하는 호스팅되는 클라우드 검색 서비스입니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>점수 매기기 프로필(Azure 검색 REST API 버전 2015-02-28-Preview)
> [!NOTE]
> 이 문서에서는 점수 매기기 프로필을 사용할 수 있는 hello 설명 [2015-02-28-preview](search-api-2015-02-28-preview.md)합니다. 현재 없는 hello 사이 차이점이 없고 `2016-09-01` 버전에서 문서화 된 [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) 및 hello `2015-02-28-Preview` 버전 여기에서 설명 하지만 म이 문서 그래도 순서 tooprovide 문서 검사에서 hello 간에 전체 API입니다.
>
>

## <a name="overview"></a>개요
점수 매기기 검색 결과에 반환 된 모든 항목에 대 한 검색 점수 toohello 계산을 참조 합니다. hello 점수는 항목의 관련성 hello 현재 검색 작업의 hello 컨텍스트에서 표시기입니다. hello 점수가 높을수록 hello, hello hello 항목 보다 적절 합니다. 검색 결과 항목은 순위에서 높은 toolow, 각 항목에 대해 계산 된 hello 검색 점수에 따라 정렬 합니다.

Azure 검색에서는 기본 toocompute 초기 점수, 점수 매기기를 사용 하지만 점수 매기기 프로필을 통해 hello 계산을 사용자 지정할 수 있습니다. 점수 매기기 프로필 검색 결과에서 항목의 순위 hello에 대 한 제어 강화를 제공합니다. 예를 들어 잠재 수익이에 따라 tooboost 항목 원하는 항목이 또는 너무 오랫동안 재고에 포함 되어 있었던 항목이 상승할 수 있습니다.

점수 매기기 프로필에는 필드, 함수 및 매개 변수는 구성 hello 인덱스 정의의 일부입니다.

toogive 'g e o' 라는 같은 hello 다음 예제에서는 간단한 프로필 점수 매기기 프로필 대략 어떤 이해할 수 있습니다. 이 항목을 상승 시킵니다 hello 검색 단어 hello에 포함 된 `hotelName` 필드입니다. 또한 hello 사용 `distance` hello 현재 위치의 10km 이내 toofavor 항목 작동 합니다. 'I n n' hello 용어를 검색 하는 경우 호텔이 hello 호텔 이름의 toobe 일부 'i n n' 포함 하는 문서 상위 hello 검색 결과에 표시 됩니다.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

이 점수 매기기 프로필의 경우 쿼리는 toouse hello 쿼리 문자열에 대해 toospecify hello 프로필으로 공식화 됩니다. 아래 hello 쿼리 hello 쿼리 매개 변수를 알 수 있듯이 `scoringProfile=geo` hello 요청에서 합니다.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

이 쿼리는 hello 용어 'i n n'에서 검색 하 고 hello 현재 위치에 전달 합니다. 이 쿼리에는 `scoringParameter`등의 다른 매개 변수도 포함되어 있습니다. 쿼리 매개 변수에 대해서는 [문서 검색(Azure 검색 API)](search-api-2015-02-28-preview.md#SearchDocs)에서 설명합니다.

클릭 [예제](#example) tooreview 점수 매기기 프로필의 보다 자세한 예입니다.

## <a name="what-is-default-scoring"></a>기본 점수 매기기
점수 매기기에서는 순위를 기준으로 정렬된 결과 집합의 각 항목에 대한 검색 점수를 계산합니다. 검색 결과 집합에 있는 모든 항목은 검색 점수를 할당 한 다음 toolowest 가장 높은 순위를 지정 합니다. 점수가 높은 hello로 항목 toohello 응용 프로그램에 반환 됩니다. 기본적으로 hello 상위 50 개는 반환 되지만 hello를 사용할 수 있습니다 `$top` 매개 변수 tooreturn 더 작거나 더 큰 단일 응답에서 too1000) (위쪽 항목 수가 있습니다.

기본적으로 검색 점수 hello 데이터 및 hello 쿼리의 통계 속성에 따라 계산 됩니다. Azure 검색 hello 쿼리 문자열의 hello 검색 용어를 포함 하는 문서를 찾습니다 (일부 또는 모두에 따라 `searchMode`), 높은 hello 검색 단어의 여러 인스턴스를 포함 하는 문서 점수를 할당 합니다. hello 검색 점수 위로 올라가면서 높을수록도 hello 문서 내에서 공통 되지만 hello 데이터 모음 hello 용어는 거의 하는 경우. 이 접근 방식 toocomputing 관련성에 대 한 hello 별로 TF-IDF 라고 또는 (용어 빈도 역 문서 빈도).

사용자 지정 정렬 되어 있는 경우 결과 다음을 기준으로 검색 점수 toohello 호출 응용 프로그램 반환 되기 전에 합니다. 경우 `$top` 를 지정 하지 않은 항목 50 개가 hello 가장 높은 검색 점수가 반환 됩니다.

전체 결과 집합에서 검색 점수 값이 반복될 수 있습니다. 예를 들어 점수가 1.2인 항목이 10개, 1.0인 항목이 20개, 0.5인 항목이 20개 있을 수 있습니다. 여러 적중 동일한 검색 점수 hello 있는, hello 동일한 점수가 매겨진된 항목의 순서를 정의 하지 않으면 및 안정적이 지 않은 합니다. Hello 쿼리를 다시 실행 하 고 표시 될 수 있습니다 항목은 자리를 이동 합니다. 즉, 두 항목의 점수가 같은 경우 어떤 항목이 먼저 표시되는지 보장되지 않습니다.

## <a name="when-toouse-custom-scoring"></a>때 toouse 사용자 지정 점수 매기기
Hello 기본 순위 지정 동작 하지 않는 이동에 충분히 멀리 비즈니스 목표를 충족할 경우에 하나 이상의 점수 매기기 프로필을 만들어야 합니다. 새로 추가하는 항목의 검색 관련성을 높게 설정하려는 경우를 예로 들 수 있습니다. 이익률을 포함하는 필드나 잠재 수익을 나타내는 다른 필드의 경우에도 마찬가지입니다. Tooyour 비즈니스 혜택을 얻을 적중 승격 점수 매기기 프로필 toouse를 결정 하는 데 중요 한 요인이 될 수 있습니다.

또한 관련성 기반 순서 지정도 점수 매기기 프로필을 통해 구현됩니다. 검색 결과를 페이지를 지난 hello에서 사용한 가격, 날짜, 등급 또는 관련성 정렬할 것이 좋습니다. Azure 검색에서는 점수 매기기 프로필 hello ' 관련성 ' 옵션을 사항이 발생 합니다. 관련성의 정의 hello 제어 하는를 기반으로 비즈니스 목표와 hello 유형의 검색 환경 toodeliver 원하는 합니다.

<a name="example"></a>

## <a name="example"></a>예제
위에서 설명한 것처럼 인덱스 스키마에 정의된 하나 이상의 점수 매기기 프로필을 통해 사용자 지정된 점수 매기기를 구현합니다.

이 예제에서는 두 점수 매기기 프로필을 통해 인덱스의 스키마를 hello (`boostGenre`, `newAndHighlyRated`). 쿼리 매개 변수는 hello 프로필 tooscore hello 결과 집합을 사용 하는 프로필 중 하나를 포함 하는이 인덱스에 대해 쿼리 합니다.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>워크플로
사용자 지정 tooimplement hello 인덱스를 정의 하는 점수 매기기 프로필 toohello 스키마를 추가 동작을 평가 합니다. 인덱스 내에서 too16 점수 매기기 프로필을 사용할 수 있습니다 (참조 [서비스 제한](search-limits-quotas-capacity.md)), 지정된 된 쿼리 시 프로필이 두 개를 지정할 수 있습니다.

Hello로 시작 [템플릿](#bkmk_template) 이 항목에서 제공 합니다.

이름을 입력합니다. 점수 매기기 프로필은 선택 사항이 있지만 하나를 추가 하는 경우에 hello 이름은 필수입니다. 수 있는지 toofollow hello 필드에 대 한 명명 규칙 (문자로 시작 하며 특수 문자와 예약어). 자세한 내용은 [이름 지정 규칙](http://msdn.microsoft.com/library/azure/dn857353.aspx) 을 참조하세요.

hello 점수 매기기 프로필의 hello 본문은 가중치가 적용 된 필드와 함수에서 생성 됩니다.

### <a name="weights"></a>Weights
hello `weights` 점수 매기기 프로필의 속성 상대적 가중치 tooa 필드를 지정 하는 이름-값 쌍을 지정 합니다. Hello에 [예제](#example), hello albumTitle, genre 및 artistName 필드가 승격 된 1.5, 5, 2, 각각. 이유는 장르 훨씬 크게 상승 보다 다른 hello? 검색은 어느 정도 유형이 같은 데이터에 대해 수행 하는 경우 (hello 경우 '장르' hello에서와 마찬가지로 `musicstoreindex`), hello 상대 가중치의 편차가 더 커야 할 수 있습니다. 예를 들어 hello에에서 `musicstoreindex`, '록'은 장르로와 같은 구가 사용된 하는 장르 설명에 나타납니다. 장르 toooutweigh 장르 설명 하려는 경우 hello genre 필드 훨씬 높은 상대 가중치를 필요 합니다.

### <a name="functions"></a>함수
함수는 특정 컨텍스트에 대해 추가 계산을 수행해야 하는 경우 사용됩니다. 올바른 함수 유형은 `freshness`, `magnitude`, `distance` 및 `tag`입니다. 각 함수에 고유한 tooit는 매개 변수가 있습니다.

* `freshness`항목이 최신 또는 오래 tooboost은 하려는 경우 사용 해야 합니다. 이 함수는 datetime 필드(`Edm.DataTimeOffset`)에만 사용할 수 있습니다. 참고 hello `boostingDuration` 특성 hello freshness 함수에만 사용 됩니다.
* `magnitude`어떻게 높거나 낮은 숫자 값에 따라 tooboost은 하려는 경우 사용 해야 합니다. 이 함수를 사용해야 하는 시나리오에는 이익률, 최고 가격, 최저 가격 또는 다운로드 수를 기준으로 상승시키는 경우가 포함됩니다. Hello 역 패턴 (예를 들어 tooboost 가격이 낮은 항목 더 높은 가격 항목 보다 더 많은) 하려는 경우 hello 범위를 높은 toolow 되돌릴 수 있습니다. 가격이 $ 100에서의 범위 지정 된 너무 $1, 설정한 `boostingRangeStart` 100 및 `boostingRangeEnd` 1 tooboost hello 가격이 낮은 항목에 있습니다. 이 함수는 double 및 integer 필드에서만 사용할 수 있습니다.
* `distance`사용 해야 tooboost 하려는 경우 근접도 나 지리적 위치입니다. 이 함수는 `Edm.GeographyPoint` 필드에만 사용할 수 있습니다.
* `tag`사용 해야 tooboost 하려는 경우 문서 및 검색 쿼리 사이 공통 됩니다. 이 함수는 `Edm.String` 및 `Collection(Edm.String)` 필드에만 사용할 수 있습니다.

#### <a name="rules-for-using-functions"></a>함수 사용 규칙
* 함수 유형(freshness, magnitude, distance, tag)은 소문자여야 합니다.
* 함수는 null 또는 빈 값을 포함할 수 없습니다. 특히 fieldname를 포함 하는 경우 것 tooset 것 toosomething 합니다.
* 함수에 적용 된 toofilterable 필드 수만 있습니다. 필터링 가능한 필드에 대한 자세한 내용은 [인덱스 만들기](search-api-2015-02-28-preview.md#CreateIndex) 를 참조하세요.
* 함수는 인덱스의 hello fields 컬렉션에 정의 된 적용된 toofields 수만 있습니다.

Hello 인덱스를 정의한 후 hello 인덱스 스키마와 문서를 차례로 업로드 하 여 hello 인덱스를 작성 합니다. 이러한 작업에 대한 지침은 [인덱스 만들기](search-api-2015-02-28-preview.md#CreateIndex) 및 [문서 추가, 업데이트 또는 삭제](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)를 참조하세요. Hello 인덱스가 작성 되 면 검색 데이터를 사용 하는 점수 매기기 프로필이 있어야 합니다.

<a name="bkmk_template"></a>

## <a name="template"></a>템플릿
이 섹션에는 hello 구문 및 점수 매기기 프로필에 대 한 템플릿을 보여 줍니다. 너무 참조[인덱스 특성 참조](#bkmk_indexref) hello hello 특성에 대 한 설명은 다음 섹션에 있습니다.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
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
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>점수 매기기 프로필 속성 참조
> [!NOTE]
> 점수 매기기 함수는 필터링 가능한 적용된 toofields 수만 있습니다.
>
>

| 속성 | 설명 |
| --- | --- |
| `name` |필수입니다. Hello 점수 매기기 프로필의 hello 이름입니다. 이 다음과 같은 명명 규칙 필드의 hello 합니다. 문자로 시작 해야 하며, 마침표, 콜론을 사용할 수 없습니다 것 또는 @ 기호를 hello 구 (대/소문자 구분) "azureSearch"로 시작할 수 없습니다. |
| `text` |Hello Weights 속성을 포함합니다. |
| `weights` |선택 사항입니다. 필드 이름 및 상대적 가중치를 지정하는 이름-값 쌍입니다. 상대적 가중치는 양의 정수 또는 부동 소수점 숫자여야 합니다. 해당 하는 가중치 없이 필드 이름을 hello를 지정할 수 있습니다. 가중치는 상대 tooanother 한 필드의 사용 되는 tooindicate hello 중요도입니다. |
| `functions` |선택 사항입니다. Note 점수 매기기 함수는 필터링 가능한 적용된 toofields만 될 수 있습니다. |
| `type` |점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다. 함수 toouse hello 유형을 나타냅니다. 유효한 값은 `magnitude`, `freshness`, `distance` 또는 `tag`입니다. 각 점수 매기기 프로필에 둘 이상의 함수를 포함할 수 있습니다. hello 함수 이름에는 소문자 여야 합니다. |
| `boost` |점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다. 원점수의 승수로 사용되는 양수입니다. 같은 too1 수 없습니다. |
| `fieldName` |점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다. 점수 매기기 함수는 hello 인덱스의 hello 필드 컬렉션의 일부 이며 필터링 가능한 적용된 toofields 수만 있습니다. 예를 들어 freshness는 datetime 필드에, magnitude는 integer/double 필드에, distance는 location 필드에, tag는 string/string collection 필드에 사용할 수 있습니다. 필드는 함수 정의당 하나만 지정할 수 있습니다. 에 대 한 예제에서는 toouse magnitude를 두 번에 같은 프로필 hello, tooinclude 두 개의 magnitude 정의 각 필드에 하나씩 필요 합니다. |
| `interpolation` |점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다. hello에서에서 점수 부스트가 증가 hello 범위 toohello hello 범위 끝의 hello 시작에 대 한 hello 경사를 정의 합니다. 유효한 값은 `linear`(기본값), `constant`, `quadratic` 또는 `logarithmic`입니다. 자세한 내용은 [보간 설정](#bkmk_interpolation)을 참조하세요. |
| `magnitude` |hello magnitude 점수 매기기 함수는 숫자 필드에 대 한 값의 hello 범위를 기준으로 사용 되는 tooalter 순위입니다. 이 hello 가장 일반적인 사용 예는 다음과 같습니다.<ul><li>별 등급: hello "별 등급" 필드 내의 hello 값에 따라 Alter hello 점수 매기기입니다. 관련 항목이 두 개이면, hello hello 등급이 높은 항목이 먼저 표시 됩니다.</li><li>여백: 두 문서를 관련 된 경우는 소매점 이익이 더 높은 tooboost 문서 파악할 수도 있습니다.</li><li>클릭 횟수: 동작 tooproducts 또는 페이지를 통해 추적 하는 응용 프로그램 클릭, magnitude tooboost 항목 tooget hello 트래픽 대부분을 사용할 수 있습니다.</li><li>다운로드 횟수: 대부분의 다운로드 hello에 있는 항목을 상승 시킬 응용 프로그램 다운로드를 추적 하는 hello magnitude 함수 사용에 대 한 합니다.</li></ul> |
| `magnitude:boostingRangeStart` |집합 hello magnitude의 점수를 매길 hello 범위의 값을 시작 합니다. hello 값은 정수 또는 부동 소수점 숫자 여야 합니다. 별 등급 1~4에서 시작 값은 1이고 50%를 초과하는 이익의 경우에는 시작 값이 50입니다. |
| `magnitude:boostingRangeEnd` |Magnitude의 점수를 매길 hello 범위의 hello 끝 값을 설정 합니다. hello 값은 정수 또는 부동 소수점 숫자 여야 합니다. 별 등급 1~4에서 끝 값은 4가 됩니다. |
| `magnitude:constantBoostBeyondRange` |유효한 값은 true 또는 false(기본값)입니다. Tootrue, 설정 된 경우 전체 부스트가 hello tooapply toodocuments hello hello 범위의 상위 끝 보다 높은 hello 대상 필드에 대 한 값이 계속 됩니다. False 인 경우,이 함수의 부스트가 hello hello 범위 밖의 hello 대상 필드의 값이 적용 된 toodocuments 수 없습니다. |
| `freshness` |hello freshness 점수 매기기 함수는 DateTimeOffset 필드에서 값을 기반으로 하는 항목에 대 한 점수 순위 사용된 tooalter입니다. 예를 들어 보다 최근 날짜의 항목에 오래된 날짜의 항목보다 더 높은 순위를 지정할 수 있습니다. (참고 수 있다는 것은 가능한 toorank 항목 등의 미래 날짜와 일정 이벤트 hello 나중에 있는 항목이 더 가깝기 때문 toohello를 추가 항목 보다 더 높은 순위 수 있도록 합니다.) 현재 서비스 릴리스 hello hello 범위의 한쪽 끝 수정 될 toohello 현재 시간입니다. hello 다른 쪽 끝은 hello에 따라 hello 과거에 한 번 `boostingDuration`합니다. 음수를 사용 하 여 tooboost hello 향후에 시간 범위 `boostingDuration`합니다. hello 속도 hello에 hello 적용 보간 toohello 점수 매기기 프로필에 의해 결정 됩니다 최대 및 최소 범위도의 변경 내용을 승격 (아래 hello 그림 참조). tooreverse hello 적용 된 상승 계수를 1 보다 작은 상승 계수를 선택 합니다. |
| `freshness:boostingDuration` |특정 문서에 대해 상승을 중지할 만료 기간을 설정합니다. 참조 [boostingDuration 설정](#bkmk_boostdur) hello 다음 구문 및 예제에 대 한 섹션에에서 있습니다. |
| `distance` |hello 거리 점수 매기기 함수는 사용 되는 tooaffect hello 정도에 따라 문서의 계산 닫습니다 하거나 상대 tooa 참조 지리적 위치를 합니다. hello 참조 위치 매개 변수에서 hello 쿼리의 일부로 제공 됩니다 (hello를 사용 하 여 `scoringParameter` 쿼리 매개 변수) lon, lat 인수로 합니다. |
| `distance:referencePointParameter` |매개 변수 toobe 쿼리 toouse 참조 위치도 전달 합니다. scoringParameter는 쿼리 매개 변수입니다. 쿼리 매개 변수의 설명은 [문서 검색](search-api-2015-02-28-preview.md#SearchDocs) 을 참조하세요. |
| `distance:boostingDistance` |범위를 승격 하는 hello 끝나는 hello 참조 위치에서 킬로미터 단위로 hello 거리를 나타내는 숫자입니다. |
| `tag` |hello 태그 점수 매기기 함수는 사용 문서 및 검색 쿼리는 태그를 기준으로 문서의 tooaffect hello 계산 합니다. Hello 검색 쿼리 공통 된 태그가 포함 된 문서를 높일 됩니다. hello 검색 쿼리는 각 검색 요청에 점수 매기기 매개 변수로 제공 됩니다에 대 한 태그를 hello (hello를 사용 하 여 `scoringParameter` 쿼리 매개 변수). |
| `tag:tagsParameter` |매개 변수 toobe toospecify 태그는 특정 요청에 대 한 쿼리에 전달 합니다. `scoringParameter` 은(는) 쿼리 매개 변수입니다. 쿼리 매개 변수의 설명은 [문서 검색](search-api-2015-02-28-preview.md#SearchDocs) 을 참조하세요. |
| `functionAggregation` |선택 사항입니다. 함수를 지정할 때만 적용됩니다. 유효한 값은 `sum`(기본값), `average`, `minimum`, `maximum` 또는 `firstMatching`입니다. 검색 점수는 여러 함수를 비롯한 여러 변수에서 계산되는 단일 값입니다. 이 특성은 모든 hello 함수 hello 상승이 적용 된 toohello 기본 문서 점수가 있는 단일 집계 상승으로 결합 되는 방식을 나타냅니다. 기본 점수 hello hello 문서 및 hello 검색 쿼리에서 계산 된 hello tf idf 값을 기반으로 합니다. |
| `defaultScoringProfile` |검색 요청을 실행할 때 점수 매기기 프로필이 지정되어 있지 않으면 기본 점수 매기기(tf-idf만)가 사용됩니다. 기본 점수 매기기 프로필 이름을 설정할 수 있습니다 여기서 hello 검색 요청에 특정 프로필이 지정 하는 경우 Azure 검색 toouse 해당 프로필을 발생 합니다. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>보간 설정
보간을 hello에서에서 점수 부스트가 증가 hello 범위 toohello hello 범위 끝의 hello 시작에 대 한 toodefine hello 기울기를 사용 합니다. 보간 다음 hello는 사용할 수 있습니다.

* `Linear`: Hello max 및 min 범위 내에 있는 항목에 대 한 hello 적용 부스트 toohello 항목은 지속적으로 감소 시간 내에 수행 됩니다. Linear는 점수 매기기 프로필에 대 한 hello 기본 보간입니다.
* `Constant`: Hello 시작 범위와 끝 범위 내에 있는 항목에 대 한 일정 한 상승이 순위 결과 toohello 적용된 됩니다.
* `Quadratic`: 비교 tooa 지속적으로 감소 부스트 있는 선형 보간 Quadratic 작은 속도로 처음 줄어듭니다 한 다음 hello 끝 범위가 가까워지면 간격 감소는 훨씬 더 높은 합니다. 이 보간 옵션은 tag 점수 매기기 함수에서 허용되지 않습니다.
* `Logarithmic`: 비교 tooa 지속적으로 감소 부스트 있는 선형 보간 Logarithmic 더 높은 속도로 처음 줄어듭니다 한 다음 hello 끝 범위가 가까워지면 감소 훨씬 작은 간격 합니다. 이 보간 옵션은 tag 점수 매기기 함수에서 허용되지 않습니다.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>boostingDuration 설정
`boostingDuration`hello freshness 함수의 특성이입니다. 사용할 있습니다 tooset 부스트 만료 기한을 중지 되는 특정 문서에 대 한. 예를 들어 tooboost 제품 라인 이나 브랜드 10 일 프로 모션 기간에 대 한 해당 문서에 대 한 hello 10 일 기간을 "P10D"을 지정 합니다. Tooboost 예정 이벤트 hello에 다음 주 지정 또는 "-P7D"입니다.

`boostingDuration` 의 형식은 XSD "dayTimeDuration" 값(ISO 8601 기간 값의 제한된 하위 집합)으로 지정해야 합니다. 이 대 한 hello 패턴은: `[-]P[nD][T[nH][nM][nS]]`합니다.

다음 표에서 hello 몇 가지 예제를 제공 합니다.

| 기간 | boostingDuration |
| --- | --- |
| 1일 |"P1D" |
| 2일 12시간 |"P2DT12H" |
| 15분 |"PT15M" |
| 30일, 5시간, 10분, 6.334초 |"P30DT5H10M6.334S" |

더 많은 예제를 보려면 [XML 스키마: Datatypes(W3.org 웹 사이트)](http://www.w3.org/TR/xmlschema11-2/)를 참조하세요.

**참고 항목**
MSDN의 [Azure Search 서비스 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) <br/>
MSDN의 [인덱스 만들기(Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)<br/>
[점수 매기기 프로필 tooa 검색 인덱스를 추가](http://msdn.microsoft.com/library/azure/dn798928.aspx) msdn<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
