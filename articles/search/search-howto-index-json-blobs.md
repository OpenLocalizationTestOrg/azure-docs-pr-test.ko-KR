---
title: "blob Azure 검색 인덱서를 사용 하 여 aaaIndexing JSON blob"
description: "Azure 검색 BLOB 인덱서를 사용하여 JSON BLOB 인덱싱"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Azure 검색 BLOB 인덱서를 사용하여 JSON BLOB 인덱싱
이 문서에서는 Azure 검색 blob 인덱서 tooextract tooconfigure JSON이 포함 된 blob의 콘텐츠를 구성 하는 방법을 보여 줍니다.

## <a name="scenarios"></a>시나리오
기본적으로 [Azure 검색 BLOB 인덱서](search-howto-indexing-azure-blob-storage.md) 는 단일 텍스트 청크로 JSON BLOB을 구문 분석합니다. JSON 문서 toopreserve hello 구조를 하려는 경우가 많습니다. 예를 들어 hello JSON 문서

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

tooparse "text", "datePublished" 및 "태그" 필드를 사용 하 여 문서에 Azure 검색을 할 수 있습니다.

Blob이 포함 때 또는 **JSON 개체 배열을**, hello 배열 toobecome 별도 Azure 검색 문서의 각 요소를 사용할 수 있습니다. 예를 들어 이 JSON이 있는 blob가 있다고 가정할 경우  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

각각 "id" 및 "text" 필드가 있는 별도의 3개 문서로 Azure Search 인덱스를 채울 수 있습니다.

> [!IMPORTANT]
> 현재 미리 보기 기능을 구문 분석 하는 hello JSON 배열이입니다. 버전을 사용 하 여 hello REST API 에서만 사용할 수는 **2015-02-28-preview**합니다. 미리 보기 API는 테스트 및 평가 용도로 제공되며 프로덕션 환경에는 사용되지 않는다는 점을 유념하세요.
>
>

## <a name="setting-up-json-indexing"></a>JSON 인덱싱 설정
JSON blob 인덱싱은 비슷한 toohello 일반 문서 추출 합니다. 먼저, 보통 때와 같이 정확히 hello datasource를 만듭니다. 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

그런 다음 아직 없는 경우에 hello 대상 검색 인덱스를 만듭니다. 

마지막 인덱서를 만들고 hello 설정 `parsingMode` 매개 변수가 너무`json` (단일 문서와 각 tooindex blob) 또는 `jsonArray` (blob JSON 배열 포함 하는 경우 및 별도 문서로 처리 하는 배열 toobe의 각 요소를 필요):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

필요한 경우 사용 하 여 **필드 매핑** toopick hello hello 소스 JSON 사용 되는 문서 toopopulate의 속성을 대상 검색 인덱스를 사용 하 여 hello 다음 섹션에 나와 있는 것 처럼 합니다.

> [!IMPORTANT]
> `json` 또는 `jsonArray` 구문 분석 모드를 사용하는 경우 Azure Search는 데이터 원본의 모든 blob이 JSON을 포함한다고 가정합니다. Toosupport JSON의 혼합을 hello에 JSON이 아닌 blob 동일한 데이터 원본에 의견을 보내려면 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search)합니다.
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>필드 매핑 toobuild 문서 검색을 사용 하 여
현재 Azure 검색은 기본 데이터 형식, 문자열 배열 및 GeoJSON 포인트만 지원하므로 임의의 JSON 문서를 직접 인덱싱할 수 없습니다. 사용할 수 있습니다 **필드 매핑** toopick 부분의 JSON 문서 및 "리프트" 해당 문서를 검색 하는 hello의 최상위 계획을 선택 합니다. 에 대 한 필드 매핑 기본 toolearn 참조 [Azure 검색 인덱서 필드 매핑 hello 데이터 소스와 검색 인덱스의 차이점을 브리징](search-indexer-field-mappings.md)합니다.

Tooour 예제 JSON 문서를 다시 전달 합니다.

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

다음 필드는 hello로 검색 인덱스를 있다고 가정해봅시다: `text` 형식의 `Edm.String`, `date` 형식의 `Edm.DateTimeOffset`, 및 `tags` 형식의 `Collection(Edm.String)`합니다. toomap, JSON hello에 적용할 셰이프, 다음 필드 매핑을 hello를 사용 하 여:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

hello hello 매핑에 소스 필드 이름이 지정 된 hello를 사용 하 여 [JSON 포인터](http://tools.ietf.org/html/rfc6901) 표기법입니다. JSON 문서의 슬래시 toorefer toohello 루트를 가진로 시작 하 고이 정보를 원하는 hello 속성 (중첩의 임의 수준)에 전달 슬래시로 구분 된 경로 사용 하 여 선택 합니다.

0 기반 인덱스를 사용 하 여 tooindividual 배열 요소를 참조할 수도 있습니다. 예를 들어 위 예제를 hello에서 hello "tags" 배열의 toopick hello 첫 번째 요소 다음과 같은 필드 매핑을 사용 합니다.

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> 필드 매핑 경로에서 소스 필드 이름을 JSON에서 존재 하지 않는 tooa 속성을 참조 하는 경우 해당 매핑은 오류 없이 건너뜁니다. 다른 스키마를 사용하여 문서를 지원할 수 있도록 이 작업을 수행합니다(일반적인 사용 사례). 유효성을 검사 하지 않으므로 필드 매핑 사양에서 tootake 보험 tooavoid 오타 필요 합니다.
>
>

JSON 문서에 단순한 최상위 속성만 포함되는 경우 필드 매핑이 전혀 필요 없습니다. 예를 들어, JSON이, hello 최상위 속성 "text" 같이, "datePublished" 및 "태그" 직접 매핑합니다 toohello hello 검색 인덱스의 해당 필드를.

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

다음은 필드 매핑이 있는 전체 인덱서 페이로드입니다.

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>중첩된 JSON 배열 인덱싱
JSON 개체의 배열을 하지만 해당 배열 tooindex 원하는 경우에 어떻게은 어딘가에 문서 내에 중첩 hello? Hello를 사용 하 여 hello 배열을 포함 하는 속성을 선택할 수 있습니다 `documentRoot` 구성 속성이 있습니다. 예를 들어 blob은 다음과 같습니다.

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

hello에 포함 된이 구성 tooindex hello 배열을 사용 하 여 `level2` 속성:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Azure Search 개선 지원
기능 또는 향상 된 기능에 대 한 아이디어를 설정한 경우 교류할에 toous 우리의 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search/)합니다.
