---
title: "Azure 검색에서 텍스트 검색 엔진 (Lucene) 아키텍처 aaaFull | Microsoft Docs"
description: "관련된 tooAzure 검색으로 전체 텍스트 검색에 대 한 Lucene 쿼리 처리 및 문서 검색 개념을 설명 합니다."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Azure Search에서 전체 텍스트 검색의 작동 방식

이 문서는 Azure Search에서 Lucene 전체 텍스트 검색이 작동하는 방식에 대해 자세히 이해할 필요가 있는 개발자를 위해 작성되었습니다. 텍스트 쿼리의 경우 Azure Search는 대부분의 시나리오에서 예상된 결과를 원활하게 제공하지만, 가끔은 "예상과 다른" 결과를 얻기도 합니다. 이러한 상황에서는 Lucene 쿼리 실행의 4 단계로 hello에 배경 것 (구문 분석, 어휘 분석 쿼리, 문서 일치 점수 매기기) 특정 변경 내용을 tooquery 매개 변수를 식별 하거나 인덱스 구성 hello 제공 하는 데 도움이 원하는 결과입니다. 

> [!Note] 
> Azure Search는 전체 텍스트 검색에 Lucene을 사용하지만 Lucene이 완전히 통합된 것은 아닙니다. 에서는 선택적으로 노출할 고 Lucene 기능 tooenable hello 시나리오 중요 tooAzure 검색을 확장 합니다. 

## <a name="architecture-overview-and-diagram"></a>아키텍처 개요 및 다이어그램

Hello 쿼리 텍스트 tooextract 검색 용어를 구문 분석으로 시작 된 전체 텍스트 검색 쿼리를 처리 합니다. hello 검색 엔진 인덱스 tooretrieve 문서를 사용 하 여 일치 하는 조건입니다. 개별 쿼리 용어는 경우에 따라 분할 됩니다 및 다시 구성에 새 폼 toocast 보다 광범위 한 네트워크를 통해 잠재적인 일치 항목으로 간주 될 수 있습니다. 그런 다음 결과 집합은 관련성 점수 할당된 tooeach 개별 일치 하는 문서도 정렬 됩니다. Hello hello 순위 목록 위쪽에 있는 toohello 호출 응용 프로그램을 반환 됩니다.

다시 정리하면, 쿼리 실행은 다음과 같은 네 단계로 구성됩니다. 

1. 쿼리 구문 분석 
2. 어휘 분석 
3. 문서 검색 
4. 점수 매기기 

아래 hello 다이어그램 hello 사용 되는 구성 요소 tooprocess를 검색 요청을 보여 줍니다. 

 ![Azure Search의 Lucene 쿼리 아키텍처 다이어그램][1]


| 핵심 구성 요소 | 기능 설명 | 
|----------------|------------------------|
|**쿼리 파서** | 쿼리 연산자에서 쿼리 용어를 구분 하 고 hello 쿼리 구조 (쿼리 트리) 전송 toobe toohello 검색 엔진을 만듭니다. |
|**분석기** | 쿼리 용어에 대한 어휘 분석을 수행합니다. 이 프로세스에는 쿼리 용어의 변환, 제거 또는 확장이 포함될 수 있습니다. |
|**Index** | 효율적인 데이터 구조 toostore를 사용 하 고 인덱싱된 문서에서 추출 된 검색 가능한 용어를 구성 합니다. |
|**검색 엔진** | 반전 된 인덱스를 검색 하 고 포함 하는 hello의 hello 내용에 따라 문서 점수입니다. |

## <a name="anatomy-of-a-search-request"></a>검색 요청 분석

검색 요청은 결과 집합에 반환할 완전한 규격입니다. 가장 간단한 형태는 어떠한 조건도 없는 빈 쿼리입니다. 매개 변수를 포함 하는 예제는 좀 더 현실적인 조건은 필터 식과 정렬 규칙을 가진 toocertain 아마도 범위가 지정 된 필드를 쿼리 하는 여러 하십시오.  

hello 다음 예제는 검색 요청 tooAzure 검색을 보낼 수 있습니다 hello를 사용 하 여 [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)합니다.  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

이 요청에 대 한 hello 검색 엔진은 다음 hello지 않습니다.

1. Hello 가격이 $60 이상 및 300 달러 문서 필터링 합니다.
2. Hello 쿼리를 실행합니다. 이 예제에서는 hello 검색 쿼리 이루어져 구 및 용어: `"Spacious, air-condition* +\"Ocean view\""` (사용자가 일반적으로 입력 하지 마세요 문장 부호, 하지만 포함 하 여 hello 예제에 있도록 tooexplain 분석기를 처리 하는 방법을). 이 쿼리에 대 한 hello 검색 엔진 검색 hello 설명 및 제목 필드에 지정 된 `searchFields` "바다 전망"를 포함 하는 문서에 대 한 및 또한 "보여주며" hello 용어 또는 hello 접두사로 시작 하는 용어에 대해 "air-condition"입니다. hello `searchMode` 매개 변수가 사용 되는 toomatch 모든 용어가 (기본값) 또는 용어 명시적으로 필요 하지 않은 경우 이러한 모든 설정 되어 (`+`).
3. 주문 근접 tooa 지리적 위치를 지정 하 고 다음 toohello 호출 응용 프로그램을 반환 하 여 결과 집합이 호텔 hello 합니다. 

hello이 문서의 대부분은 hello의 처리에 대 한 *검색 쿼리*: `"Spacious, air-condition* +\"Ocean view\""`합니다. 필터링 및 정렬은 본 문서에서 다루지 않습니다. 자세한 내용은 참조 hello [검색 API 참조 설명서](https://docs.microsoft.com/rest/api/searchservice/search-documents)합니다.

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>1단계: 쿼리 구문 분석 

에서 설명한 것 처럼 hello 쿼리 문자열 hello 요청의 hello 첫 번째 줄은: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

파서는 구분 연산자 hello 쿼리 (같은 `*` 및 `+` hello 예제에서) 검색에서 조건 및 hello 검색 쿼리를 해체 *하위 쿼리* 지원 되는 형식의: 

+ 독립 용어(예: spacious)에 대한 *용어 쿼리*
+ 따옴표가 붙은 용어(예: ocean view)에 대한 *구 쿼리*
+ 뒤에 `*` 접두사 연산자가 붙는 용어(예: air-condition)에 대한 *접두사 쿼리*

지원되는 쿼리 유형의 전체 목록은 [Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)을 참조하세요.

Hello 쿼리 "must be" "이어야 합니다" 하는지 여부를 확인 하는 연결 된 하위 쿼리 연산자는 문서에 대 한 순서에 만족 toobe 일치로 간주 합니다. 예를 들어 `+"Ocean view"` "해야"은 due toohello `+` 연산자입니다. 

hello 쿼리 파서 구조에 hello 하위 쿼리를 다시 작성 한 *쿼리 트리* toohello 검색 엔진에 전달 (hello 쿼리를 나타내는 내부 구조). Hello 쿼리 구문 분석의 첫 번째 단계에서는 hello 쿼리 트리는 다음과 같습니다.  

 ![부울 쿼리 searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>지원되는 파서: 단순(simple) 및 전체(full) Lucene 

 Azure Search는 두 쿼리 언어 `simple`(기본값) 및 `full`을 노출합니다. Hello 설정 하 여 `queryType` 검색 요청에 대 한 매개 변수를 알려 hello 쿼리 파서 쿼리 언어 하시 알 수 있도록 연산자 및 구문 toointerpret hello 하는 방법입니다. hello [단순 쿼리 언어](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 직관적이 고 견고는 종종 적합 한 toointerpret 사용자 입력은-클라이언트 쪽 처리 하지 않고 있습니다. 웹 검색 엔진과 비슷한 쿼리 연산자를 지원합니다. hello [전체 Lucene 쿼리 언어](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)를 설정 하 여 얻을 `queryType=full`, 더 많은 연산자와 유사 항목 와일드 카드와 같은 쿼리 유형을, regex, 및 필드 범위 쿼리에 대 한 지원을 추가 하 여 hello 기본 단순 쿼리 언어를 확장 합니다. 예를 들어 단순 쿼리 구문에서 전송되는 정규식은 식이 아닌 쿼리 문자열로 해석됩니다. 이 문서의 예제 요청 hello hello 전체 Lucene 쿼리 언어를 사용합니다.

### <a name="impact-of-searchmode-on-hello-parser"></a>설정은 searchMode hello 파서에 미치는 영향 

구문 분석에 영향을 주는 다른 검색 요청 매개 변수는 hello `searchMode` 매개 변수입니다. 부울 쿼리에 대 한 기본 연산자 hello 제어: 제한 없음 (기본값) 또는 전체.  

때 `searchMode=any`, hello 기본적 보여주며 사이의 hello 공간 구분 하며 air-condition은 또는 (`||`), hello 예제 쿼리 텍스트에 해당 하기: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

명시적 연산자와 같은 `+` 에 `+"Ocean view"`, 부울 쿼리 생성에 명확한 (hello 용어 *해야* 일치). 남은 toointerpret hello 조건 어떻게는 덜 명확: 보여주며 air-condition 및 합니다. Hello 검색 엔진 그동안 일치 바다 전망에 *및* 보여주며 *및* air-condition? 바다 전망 찾을 해야 또는 플러스 *둘 중 하나* 의 용어 남은 hello? 

기본적으로 (`searchMode=any`), hello 검색 엔진 hello 보다 광범위 한 해석을 가정 합니다. "or" 구문을 반영하여 두 필드 중 하나가 일치*해야 합니다*. hello 초기 쿼리 트리 이전에 통해 설명할 hello 두 가지 "는" 작업이 hello 기본값을 보여 줍니다.  

만약 `searchMode=all`로 설정한다면 어떨까요? 이 경우 hello 공간 "및" 작업으로 해석 됩니다. Hello 나머지 용어의 둘 다에 있어야 hello 문서 tooqualify 일치 기준으로 합니다. hello 결과 샘플 쿼리는 다음과 같이 해석 합니다. 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

이 쿼리에 대 한 수정 된 쿼리 트리는 다음과 같습니다.. 여기서 일치 하는 문서는 모두 3 개의 하위 쿼리의 hello 교차 다음과 같습니다. 

 ![부울 쿼리 searchmode all][3]

> [!Note] 
> `searchMode=all` 대신 `searchMode=any`를 선택하는 것은 대표 쿼리를 실행하여 도착할 수 있는 최선의 결정입니다. 가능성이 높은 tooinclude 연산자 (공통 검색 문서를 저장 하는 경우) 인 사용자 수 찾기 결과 보다 직관적인 경우 `searchMode=all` 부울 쿼리 구문에 알립니다. 간의 상호 작용 hello에 대 한 자세한 `searchMode` 연산자, 참조 및 [단순 쿼리 구문을](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)합니다.

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>2단계: 어휘 분석 

어휘 분석기 프로세스 *쿼리 용어* 및 *구를 쿼리* hello 쿼리 트리 구성 후입니다. 분석기는 hello 파서에서 텍스트 입력 제공 tooit hello 하 고 프로세스 hello 텍스트를 토큰화 다시 보내고 용어에 toobe 통합 쿼리 트리를 hello 다음 허용 합니다. 

어휘 분석의 가장 일반적인 형태 hello *언어 분석* 언어를 지정 된 특정 tooa를 규칙에 따라 쿼리 용어를 변환 하는: 

* 단어의 쿼리 용어 toohello 루트 형태 줄이기 
* 필수적이지 않은 단어(영어의 "the" 또는 "and" 같은 중지 단어) 제거 
* 복합 단어를 구성 요소 부분으로 분리 
* 대문자 단어를 소문자로 변환 

이러한 모든 작업 tooerase 차이점 hello 텍스트 입력 hello 인덱스에 저장 된 hello 사용자 및 hello 용어에서 제공 되는 경향이 있습니다. 이러한 작업 뿐만 아니라 텍스트 처리 하 여 자체 hello 언어의 깊이 있는 지식이 필요 합니다. tooadd 언어 인식, Azure 검색의이 계층에서는 목록이 긴 [언어 분석기](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene와 Microsoft에서 합니다.

> [!Note]
> 분석 요구 사항 시나리오에 따라 최소한의 tooelaborate에서 까지입니다. Hello 미리 정의 된 hello 분석기 중 하나를 선택 하거나 직접 만들어 어휘 분석의 복잡성을 제어할 수 있습니다 [사용자 지정 분석기](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search)합니다. 분석기는 범위가 지정 된 toosearchable 필드 이며 필드 정의의 일부로 지정 됩니다. 이렇게 하면 toovary 어휘 분석에 있습니다 필드 별로 합니다. 지정 하지 않으면 hello *표준* Lucene 분석기를 사용 합니다.

예제에서는 이전 tooanalysis hello 초기 쿼리 트리 hello 용어 대문자 "S"와 "Spacious," 않았으며 쿼리 파서 hello 쉼표 hello 쿼리 용어 (쉼표는 쿼리 언어 연산자를 간주 되지 않습니다)의 일부로 해석 됩니다.  

Hello 기본 분석기 hello 용어를 처리할 때 소문자로 "바다 전망" 및 "보여주며" 하 고 hello 쉼표 문자를 제거 합니다. hello 수정 된 쿼리 트리는 다음과 같이 표시 됩니다. 

 ![분석된 용어를 사용한 부울 쿼리][4]

### <a name="testing-analyzer-behaviors"></a>분석기 동작 테스트 

hello를 사용 하는 분석기의 hello 동작을 테스트할 수 [분석 API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer)합니다. Tooanalyze toosee 분석기를 지정 하는 용어에서 생성 하는 것이 원하는 hello 텍스트를 제공 합니다. 예를 들어 hello 표준 분석기를 처리 하는 방법은 toosee 텍스트 "air-condition" hello, hello 다음 요청을 실행할 수 있습니다.

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

hello 표준 분석기 다음 두 개의 토큰, 시작 및 종료 오프셋 (적중 항목 강조 표시에 사용) 뿐 아니라 (구 일치에 사용 됨)의 위치와 같은 특성을 가진에 주석을 달기 hello에 hello 입력된 텍스트를 나눕니다.

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>예외 toolexical 분석 

어휘 분석에 필요한 모든 내용을 용어 쿼리 또는 구 쿼리 tooquery 유형에 적용 됩니다. Tooquery 형식과 접두사 쿼리나 와일드 카드 쿼리, regex 쿼리 – tooa 유사 쿼리 완료 되지 않은 용어 –는 적용 되지 않습니다. Hello 접두사 쿼리 용어를 포함 하 여 형식을 쿼리 하는 것 *air-condition\**  예에서 추가 직접 toohello 쿼리 트리를 hello 분석 단계를 무시 합니다. hello 이러한 형식의 쿼리 용어에 수행 하는 변환 에서만 소문자로 변환 합니다.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>3단계: 문서 검색 

문서 검색 hello 인덱스에 일치 하는 용어를 사용 하 여 toofinding 문서를 참조합니다. 이 단계는 예를 통해 설명하는 것이 가장 빠릅니다. Hello 간단한 스키마를 따르는 것 호텔 인덱스부터 시작 하겠습니다. 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

이 인덱스에는 다음 4 개의 문서 hello 추가 가정 합니다. 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**용어 인덱싱 방식**

toounderstand 검색 하는 데 도움이 tooknow 인덱싱에 대 한 몇 가지 기본 사항입니다. 저장소 hello 단위는 각 검색 가능한 필드에 하나씩를 반전 된 인덱스입니다. 반전된 인덱스 내에는 모든 문서의 모든 정렬된 용어 목록이 있습니다. 각 용어는 toohello 목록을 항목이 발생 하는, 아래 hello 예제에서 분명 하 게 문서를 매핑합니다.

tooproduce hello 용어를 반전 된 인덱스에 hello 검색 엔진 분석을 수행 어휘 문서의 hello 콘텐츠에 대해 유사한 toowhat 쿼리 처리 중에 발생 합니다. 텍스트 입력 tooan 분석기, 소문자, 문장 부호 및 hello 분석기 구성에 따라 등 하이픈이 제거 되어 전달 됩니다. 이것은 일반적인 필요 하지 않음, toouse hello 검색 및 인덱싱 작업을 좀 더 hello 인덱스 조건을 처럼 보이도록 쿼리 용어에 대해 동일한 분석기.

> [!Note]
> Azure Search는 추가적인 `indexAnalyzer` 및 `searchAnalyzer` 필드 매개 변수를 통해 인덱싱 및 검색에 서로 다른 분석기를 지정할 수 있습니다. 지정 하지 않으면 hello hello로 설정 하는 분석기 `analyzer` 속성은 모두 인덱싱 및 검색에 사용 합니다.  

**예제 문서의 반전된 인덱스**

Tooour 예를 들어 hello 반환 **제목** 필드 hello 반전 된 인덱스는 다음과 같습니다.

| 용어 | 문서 목록 |
|------|---------------|
| atman | 1 |
| beach | 2 |
| hotel | 1, 3 |
| ocean | 4  |
| playa | 3 |
| resort | 3 |
| retreat | 4 |

Hello 제목 필드에만 *호텔* 두 문서에 표시: 1, 3.

Hello에 대 한 **설명** 필드 hello 인덱스는 다음과 같습니다.

| 용어 | 문서 목록 |
|------|---------------|
| air | 3
| and | 4
| beach | 1
| conditioned | 3
| comfortable | 3
| distance | 1
| island | 2
| kauaʻi | 2
| located | 2
| north | 2
| ocean | 1, 2, 3
| of | 2
| on |2
| quiet | 4
| rooms  | 1, 3
| secluded | 4
| shore | 2
| spacious | 1
| 안녕하세요 | 1, 2
| 너무| 1
| view | 1, 2, 3
| walking | 1
| 다음으로 바꿀 수 있습니다. | 3


**쿼리 용어를 인덱싱된 용어와 연결**

위의 hello 반전 된 인덱스를 매개 변수로 받아 toohello 예제 쿼리를 반환 하 고 하겠습니다 어떻게 일치 하는 문서를 참조 우리의 예제 쿼리에서 찾을 수 있습니다. 회수할 해당 hello 최종 쿼리 트리는 다음과 같습니다. 

 ![분석된 용어를 사용한 부울 쿼리][4]

쿼리를 실행 하는 동안 개별 쿼리에 대해 실행 됩니다 하지 hello 검색 가능한 필드 독립적으로. 

+ hello TermQuery "보여주며" 일치 문서 1 (호텔 Atman) 합니다. 

+ hello, PrefixQuery "air-condition *", 문서를 모두와 일치 하지 않습니다. 

  이는 종종 개발자를 혼란스럽게 만드는 동작입니다. Hello 용어 갖춘된 hello 문서의 있지만으로 이루어져 두 용어 hello 기본 분석기가 있습니다. 앞에서 부분 용어를 포함한 접두사 쿼리가 분석되지 않은 것을 떠올려 보세요. 따라서 hello에 조회 됩니다 "air-condition" 접두사가 포함 된 용어는 반전 된 인덱스 및 찾을 수 없습니다.

+ hello PhraseQuery "바다 전망" hello 용어 "ocean" 및 "보기"를 조회 하 고 hello 원본 문서에 있는 용어의 근접 단어 hello를 확인 합니다. Hello 설명 필드에이 쿼리를 일치 하는 문서 1, 2 및 3입니다. 공지 문서 4 hello 제목에 hello 용어 ocean을 갖지만 개별 단어가 아닌 hello "바다 전망" 구 살펴볼 때 일치 하는 것으로 간주 되지 않습니다. 

> [!Note]
> 검색 쿼리 hello hello로 설정 하는 hello 필드를 제한 하지 않으면 Azure 검색 인덱스의 모든 검색 가능한 필드에 대해 독립적으로 실행 되 `searchFields` hello 예제 검색 요청에 설명 된 대로 매개 변수입니다. 선택한 hello 필드 중 하나에 일치 하는 문서가 반환 됩니다. 

일치 하는 hello 문서에는 문제의 hello 쿼리에 대 한 전체 hello에 1, 2, 3는 합니다. 

## <a name="stage-4-scoring"></a>4단계: 점수 매기기  

검색 결과 집합의 모든 문서에 관련성 점수가 할당됩니다. hello 관련성 점수 hello 함수 hello 검색 쿼리에 의해 표현 된 대로 가장 대답 사용자는 해당 문서 질문 하기 더 높은 toorank입니다. hello 점수는 조건에 일치 하는 통계 속성에 따라 계산 됩니다. Hello hello 수식을 점수 매기기의 핵심은 [(용어 빈도 문서 빈도 반비례) TF/IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)합니다. 드물게 발생 하 고 일반적인 단어를 포함 하는 쿼리, TF/IDF hello 드문 용어를 포함 하는 결과 승격 합니다. 예를 들어 모든 Wikipedia 문서를 통해 가상 인덱스에서에서 문서 일치 하는 hello 쿼리 *hello 부사장*, 문서에 대해 일치 *부사장* 보다 관련이 높은 것으로 간주 됩니다 에 일치 하는 문서가 *는*합니다.


### <a name="scoring-example"></a>점수 매기기 예제

예제 쿼리를 일치 하는 hello 3 개의 문서를 다시 호출:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

둘 다 hello 때문에 가장 잘 일치 하는 hello 쿼리 1 문서 용어 *보여주며* 및 hello 필요한 구 *바다 전망* hello 설명 필드에 발생 합니다. hello 구만 일치 하는 hello 다음 두 문서 *바다 전망*합니다. 것 수 수 놀라운 것 해당 hello 관련성 점수 문서 2와 3 단계는 다른 hello에 hello 쿼리를 일치 하는 경우에 같은 방법으로 합니다. 수식 점수 매기기 hello TF/IDF 것 보다 더 많은 구성 요소에 때문입니다. 이 예에서는 문서 3에 약간 더 높은 점수가 할당되었는데, 설명이 좀 더 짧기 때문입니다. 에 대 한 자세한 내용은 [Lucene 실용적인 점수 매기기 수식](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) 어떻게 필드 길이 및 기타 요인 영향을 줄 수 toounderstand hello 관련성 점수입니다.

일부 쿼리 유형 (와일드 카드, 접두사, regex) 항상 상수 점수가 기여 toohello 전체 점수를 문서화 합니다. 따라서 hello 순위에 영향을 주지 않고 hello 결과에 포함 된 쿼리 확장 toobe을 통해 발견 된 일치 레코드 수 있습니다. 

이것이 왜 중요한지 예제를 통해 살펴보겠습니다. 와일드 카드 검색을 접두사 검색을 포함 하는 정의 의해 모호 서로 다른 조건에서 매우 많은 수의 hello 입력은 잠재적인 일치 항목으로 부분 문자열 ("tours", "tourettes"에서 발견 된 일치 항목에서 "둘러보기 *"의 입력을 고려해 야, 및 " tourmaline ")입니다. 이러한 결과의 hello 특성 들어 방법이 없습니다 tooreasonably 유추는 용어는 다른 항목 보다 더 중요 합니다. 이러한 이유로 와일드카드, 접두사, regex 쿼리 유형의 결과에 대한 점수를 매길 때에는 용어 빈도를 무시합니다. 일부 또는 전체 용어를 포함 하는 다중 파트 검색 요청을 hello 부분 입력에서 결과 상수와 통합 되어 예기치 않은 잠재적으로 일치 항목으로 tooavoid 바이어스 점수를 매깁니다.

### <a name="score-tuning"></a>점수 조정

두 가지가 tootune 관련성을 평가 Azure 검색에서:

1. **점수 매기기 프로필** 규칙의 집합을 기준으로 결과의 순위를 지정 하는 hello 목록에 문서를 승격 합니다. 예제에서는 문서 hello 설명 필드에 일치 하는 문서 보다 관련이 높은 hello 제목 필드에서 일치 하는 것으로 간주 수 없습니다. 뿐만 아니라 만약 인덱스에 각 호텔의 가격 필드가 있다면 가격이 낮은 문서를 승격할 수 있습니다. 어떻게 너무 자세한[점수 매기기 프로필 tooa 검색 인덱스를 추가 합니다.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **부스트 용어** (hello 전체 Lucene 쿼리 구문에만 사용 가능)에서는 부스트 연산자 `^` 일 수 있는 hello 쿼리 트리의 tooany 부분을 적용 합니다. Hello 접두사에 검색 하는 대신 예에서 *air-condition*\*, hello 정확한 한 용어를 검색할 수 하나 *air-condition* hello 접두사로 사용 하지만 정확한 hello에 일치 하는 문서 또는 부스트 toohello 용어 쿼리를 적용 하 여에 용어는 순위가 더 높은: *항공 조건 ^2 | | air-condition** 합니다. [용어 상승](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost)에 대해 자세히 알아보세요.


### <a name="scoring-in-a-distributed-index"></a>분산된 인덱스에 점수 매기기

Azure 검색의 모든 인덱스를 자동으로 여러 분할 영역으로 분할을 여러 hello 인덱스 배포 tooquickly 허락해 서비스 크기 조정 하는 동안 노드 위로 또는 확장 합니다. 검색 요청이 실행될 때 검색 요청은 각 분할 영역에 대해 독립적으로 실행됩니다. hello 각 분할의 결과 다음 병합 및 (다른 순서가 있지 정의 됨) 하는 경우 점수에 의해 정렬 됩니다. 모든 분할 영역 전체가 아닌 hello 분할 영역 내에서 모든 문서에서 해당 역 문서 빈도 대 한 점수 매기기 함수 가중치 쿼리 용어 빈도 hello 중요 tooknow입니다.

즉, 같은 문서라도 서로 다른 분할 영역에 상주할 경우 관련성 점수가 *다를 수 있습니다*. 에서는 이러한 차이 toomore 짝수 용어 배포 인해 hello hello 인덱스의 문서 수 확장 되면서 toodisappear를 경향이 있습니다. 가능한 tooassume는 분할 영역에 있는 지정 된 문서 배치할 수는 없습니다. 그러나 문서 키를 변경 하지 않는 경우 항상 할당 됩니다 toohello 동일한 분할 합니다.

일반적으로 문서 점수는 문서 순서 안정성에 중요 한 경우 순서에 대 한 hello 최상의 특성이 아닙니다. 예를 들어 점수가 같은 두 개의 문서를 매개 변수로 받아 보장은 없습니다 hello의 후속 실행에 첫 번째로 표시 한 동일한 쿼리 합니다. 문서 점수만 제공 해야 문서 관련성 일반적인 의미 상대 tooother 문서 hello 결과 집합에 합니다.

## <a name="conclusion"></a>결론

인터넷 검색 엔진의 hello 성공 개인 데이터에 대해 전체 텍스트 검색에 대 한 기대 발생 했습니다. 거의 모든 유형의 검색 환경에 대 한 이제 작업도 hello 엔진 toounderstand 용어는 철자가 잘못 입력 된 경우에 또는 불완전 한 의도 취급 됩니다. 실제로 지정하지 않은 거의 비슷한 용어 또는 동의어 기반의 일치 항목까지도 기대할 수 있습니다.

기술적인 측면에서 전체 텍스트 검색은 매우 복잡 한, 고급 언어 분석 및 추출 하 고 확장 하 고, 쿼리 용어 toodeliver 관련 결과 변환 하는 방법으로 체계적인 방법 tooprocessing 요구 합니다. Hello 내재 된 복잡성을 지정 하면 수많은 요인 쿼리의 hello 결과 영향을 줄 수 있습니다. 이러한 이유로 전체 텍스트 검색의 hello toounderstand hello 메커니즘을 시간을 투자 이점을 유형의 예기치 않은 결과 통해 toowork 하려고 할 때 있습니다.  

이 문서는 Azure 검색의 hello 컨텍스트에서 전체 텍스트 검색을 탐색 합니다. 제공 충분 한 배경 toorecognize 잠재적 원인 및 해결 방법의 일반적인 쿼리 문제를 해결 하기 위한 하시기 바랍니다. 

## <a name="next-steps"></a>다음 단계

+ Hello 샘플 인덱스를 작성 하 고 다른 쿼리를 사용해 결과 검토 합니다. 자세한 내용은 [빌드하고 hello 포털에서 인덱스를 쿼리할](search-get-started-portal.md#query-index)합니다.

+ Hello 추가 쿼리 구문을 시도 [문서 검색](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) "예" 섹션 또는 [단순 쿼리 구문을](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) hello 포털에서 검색 탐색기에서 합니다.

+ 검토 [점수 매기기 프로필](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) tootune 검색 응용 프로그램의 순위 지정 하려는 경우.

+ 자세한 내용은 방법 tooapply [언어별 어휘 분석기](https://docs.microsoft.com/rest/api/searchservice/language-support)합니다.

+ 특정 필드에 대해 최소한의 처리 또는 특수한 처리를 수행하려면 [사용자 지정 분석기를 구성](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)하세요.

+ 데모 웹 사이트에서 [표준 및 영어 분석기를 나란히 비교](http://alice.unearth.ai/)하세요. 

## <a name="see-also"></a>참고 항목

[문서 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[단순 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[전체 Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[검색 결과 처리](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
