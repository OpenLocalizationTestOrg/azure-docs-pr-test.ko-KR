---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Hello Azure 검색 REST API에에서 노출 되는 hello 동의어 (미리 보기) 기능에 대 한 기본 설명서입니다."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Azure Search의 동의어(미리 보기)

검색 엔진에서 동의어는 암시적으로 hello 사용자 hello 용어 제공 tooactually가 필요 하지 않고 쿼리를 hello 범위를 확장 하는 동의어를 연결 합니다. 예를 들어 hello 쿼리의 hello 범위 내에서 지정 된 hello 용어 "dog" 및 "애완견" 및 "듯이", "dog", "애완견" 또는 "듯이"가 들어 있는 문서는 동의어 연관 대체 됩니다.

Azure Search에서 동의어 확장은 쿼리 시에 수행됩니다. 중단 없는 tooexisting 작업과 동의어 지도 tooa 서비스를 추가할 수 있습니다. 추가할 수는 **synonymMaps** toorebuild hello 인덱스 필요 없이 속성 tooa 필드 정의 합니다. 자세한 내용은 [인덱스 업데이트](https://docs.microsoft.com/rest/api/searchservice/update-index)를 참조하세요.

## <a name="feature-availability"></a>기능 가용성

기능은 현재에 hello 동의어를 미리 보고에서 지원만 hello 최신 미리 보기 api 버전 (api 버전 = 2016-09-01-미리 보기). 지금은 Azure Portal 지원이 없습니다. Hello 요청 시 hello API 버전이 지정 되므로 가능한 toocombine 일반적으로 사용 가능한 (GA) 및 미리 보기 Api hello에 동일한 응용 프로그램입니다. 그러나 미리 보기 API는 SLA가 적용되지 않으며 기능이 변경될 수 있으므로 프로덕션 응용 프로그램에서 사용하지 않는 것이 좋습니다.

## <a name="how-toouse-synonyms-in-azure-search"></a>Azure에서 toouse 동의어 검색 하는 방법

Azure 검색에서는 동의어 지원은 동의어 맵을 정의 하 고 업로드 tooyour 서비스를 기반으로 합니다. 이러한 맵은 독립적인 리소스(인덱스 또는 데이터 원본 등)를 구성하며 검색 서비스의 모든 인덱스에서 검색 가능한 필드에 의해 사용될 수 있습니다.

동의어 맵과 인덱스는 독립적으로 유지됩니다. 라는 새 속성을 추가 하 여 필드에 hello 동의어 기능을 활성화할 수 동의어 맵을 정의 하 고 업로드 tooyour 서비스 **synonymMaps** hello 필드 정의에 있습니다. 만들기, 업데이트 및 삭제 동의어 지도 항상 전체 문서 작업을 만들 수를 의미 하는 업데이트 하거나 증분식으로 hello 동의어 맵의 부분을 삭제 합니다. 단일 항목을 업데이트하는 경우에도 다시 로드해야 합니다.

동의어를 검색 응용 프로그램에 통합하는 과정은 다음의 두 단계 프로세스로 이루어집니다.

1.  Hello 아래 Api 통해 동의어 맵 tooyour 검색 서비스를 추가 합니다.  

2.  Hello 인덱스 정의의 검색 가능한 필드 toouse hello 동의어 맵을 구성 합니다.

### <a name="synonymmaps-resource-apis"></a>SynonymMaps 리소스 API

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>POST 또는 PUT을 사용하여 서비스 아래에 동의어 맵을 추가하거나 업데이트합니다.

동의어 지도 업로드할지 POST 또는 PUT을 통해 toohello 서비스입니다. 각 규칙 hello 줄 바꿈 문자 ('\n') 구분 해야 합니다. Too5, 무료 서비스에서 동의어 맵 당 000 규칙 및 다른 모든 Sku에서 10, 000 규칙을 정의할 수 있습니다. 각 규칙 too20 확장을 만들 수 있습니다.

이 미리 보기에서 동의어 지도 아래 설명 된 hello Apache Solr 형식 이어야 합니다. 경우 기존 동의어 사전 다른 형식으로 있고 toouse 것을 직접 알려 주시면에 [UserVoice](https://feedback.azure.com/forums/263029-azure-search)합니다.

다음 예제는 hello와 HTTP POST를 사용 하 여 새 동의어 맵을 만들 수 있습니다.

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

또는 PUT을 사용 하 여 하 고 hello URI에서 hello 동의어 맵 이름을 지정할 수 있습니다. Hello 동의어 지도 없는 경우 생성 됩니다.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Apache Solr 동의어 형식

hello Solr 형식은 명시적 및 해당 동의어 매핑을 지원합니다. 매핑 규칙 준수 toohello 오픈 소스 동의어 필터 지정이이 문서에서 설명 하는 Apache Solr의: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter)합니다. 다음은 동등한 동의어에 대한 샘플 규칙입니다.
```
              USA, United States, United States of America
```

검색 쿼리 "미국" 너무 확장 위의 hello 규칙을 사용 하면 "미국" 또는 "미국" 또는 "미국"입니다.

명시적 매핑은 "=>" 화살표로 표시됩니다. 용어 시퀀스로 hello의 왼쪽을 일치 하는 검색 쿼리를 지정 하는 경우 "= >" hello 오른쪽에서 hello 대체 항목으로 바뀝니다. 검색 쿼리가 hello 규칙 아래를 매개 변수로 받아 "워싱턴", "워싱턴" "WA" 모두 다시 작성 됩니다 너무 또는 "WA"입니다. 지정 된 hello 방향으로 적용 되며 다시 기록 하지 않도록 hello 쿼리 "WA" 너무 명시적 매핑만이 경우 "워싱턴"입니다.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>서비스 아래 동의어 맵을 나열합니다.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>서비스 아래 동의어 맵을 가져옵니다.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>서비스 아래 동의어 맵을 삭제합니다.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Hello 인덱스 정의의 검색 가능한 필드 toouse hello 동의어 맵을 구성 합니다.

새 필드 속성 **synonymMaps** toospecify 사용 되는 검색 가능한 필드에 대 한 동의어 맵 toouse 될 수 있습니다. 동의어는 서비스 수준 리소스 맵과 hello 서비스에서 인덱스의 모든 필드에서 참조할 수 있습니다.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** hello 형식 'Edm.String' 또는 'collection (edm.string)'의 검색 가능 필드에 지정할 수 있습니다.

> [!NOTE]
> 이 미리 보기에서는 필드당 하나의 동의어 맵만 있을 수 있습니다. 여러 동의어 맵을 toouse을 원하는 경우 알려 주시면에 [UserVoice](https://feedback.azure.com/forums/263029-azure-search)합니다.

## <a name="impact-of-synonyms-on-other-search-features"></a>동의어가 다른 검색 기능에 미치는 영향

hello 동의어 기능 hello hello OR 연산자가 있는 동의어와 원래 쿼리를 다시 작성합니다. 이러한 이유로 적중 강조 표시 및 점수 매기기 프로필 취급 hello 원래 용어와 동의어 동일 합니다.

동의어 기능 toosearch 쿼리를 적용 되며 toofilters 또는 패싯 적용 되지 않습니다. 마찬가지로, 제안 사항은 hello 원래 용어; 동의어 일치 hello 응답에 표시 되지 않습니다.

동의어가 확장 toowildcard 검색어; 적용 되지 않습니다. 유사 항목, 접두사 및 regex 용어 확장 되지 않습니다.

## <a name="tips-for-building-a-synonym-map"></a>동의어 맵 빌드에 대한 팁

- 간결하고 잘 설계된 동의어 맵은 가능한 일치 항목의 철저한 목록보다 더 효율적입니다. 과도 하 게 크거나 복잡 한 사전 긴 tooparse 걸리고 hello 쿼리 확장 toomany 동의어 hello 쿼리 대기 시간에 영향을 줍니다. 대신 용어를 사용할 수 있습니다 추측을 통해 hello 실제 용어를 얻을 수 있습니다는 [검색 트래픽 분석 보고서](search-traffic-analytics.md)합니다.

- 연습을 준비 단계와 유효성 검사 설정 및 사용 하 여가 보고서 tooprecisely 결정는 용어는 동의어를 일치 하는 구현할 수 있으며 toouse 계속 다음 동의어 맵이 더 나은 결과 생성 하는 유효성 검사로 합니다. "검색 쿼리 결과가 0" 생깁니다 및 타일 "가장 일반적인 검색 쿼리"을 hello hello 미리 정의 된 보고서에 필요한 정보를 hello 합니다.

- 검색 응용 프로그램에 대한 여러 동의어 맵(예: 응용 프로그램이 다국어 고객 기반을 지원하는 언어별 맵)을 만들 수 있습니다. 현재 필드에서는 그중 하나만 사용할 수 있습니다. 언제든지 필드의 synonymMaps 속성을 업데이트할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- 개발 (비-프로덕션) 환경에서 기존 인덱스를 있으면 시험해 작은 사전 toosee 동의어의 hello 추가 점수 매기기 프로필, 적중 횟수 강조 표시 및 제안에 대 한 영향을 포함 하 여 hello 검색 환경을 어떻게 변경 되는지 합니다.

- [검색 트래픽 분석을 사용 하도록 설정](search-traffic-analytics.md) 및 사용 하 여 hello 사용 된 용어 toolearn hello 문서가 대부분와 그는 스토리 반환 하는 Power BI 보고서를 미리 정의 합니다. 이러한 insights armed, hello 사전 tooinclude 동의어 toodocuments 색인에 게 확인 해야 하는 생산성이 저하 쿼리를 수정 합니다.
