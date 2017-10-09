---
title: "Azure 검색에 대 한 Cosmos DB 데이터 원본 aaaIndexing | Microsoft Docs"
description: "이 문서에서는 Azure 검색 인덱서를 데이터 소스로 Cosmos DB와 함께 toocreate 합니다."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>인덱서를 사용해서 Cosmos DB를 Azure Search에 연결

Cosmos DB 데이터에 대해 효율적인 검색 환경 tooimplement 하려는 경우 Azure 검색 인덱스에는 Azure 검색 인덱서 toopull 데이터를 사용할 수 있습니다. 이 문서에서는 보여줍니다 어떻게 toowrite 모든 코드 toomaintain 인덱싱 인프라 필요 없이 Azure 검색을 사용한 Azure Cosmos DB toointegrate 합니다.

Cosmos DB 인덱서를 tooset, 있어야는 [Azure 검색 서비스](search-create-service-portal.md)는 index, datasource 및 마지막으로 hello 인덱서를 만듭니다. Hello를 사용 하 여 이러한 개체를 만들 수 있습니다 [포털](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), 또는 [REST API](/rest/api/searchservice/) 모든 비.NET 언어에 대 한 합니다. 

Hello 포털에 대 한 선택 경우 hello [데이터 가져오기 마법사](search-import-data-portal.md) 이러한 모든 리소스의 hello 만들기 과정을 안내 합니다.

> [!NOTE]
> Cosmos DB는 hello 차세대 DocumentDB의입니다. Hello 제품 이름 변경 되 면 있지만 구문은 hello 동일한 이전과 합니다. Toospecify 계속 해 서 `documentdb` 이 인덱서 문서에서 지시한 대로 합니다. 

> [!TIP]
> Hello를 시작할 수 있습니다 **데이터를 가져올** 마법사에서 해당 데이터 원본에 대 한 인덱싱을 hello Cosmos DB 대시보드 toosimplify 합니다. 왼쪽 탐색 영역에서 이동 너무**컬렉션** > **Azure 검색 추가** tooget 시작 합니다.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Azure Search 인덱서 개념
Azure 검색에서는 hello의 생성 및 관리 (Cosmos DB 포함)는 데이터 원본 및 인덱서는 데이터 원본에 대해 작동 하는 합니다.

A **데이터 소스** hello 데이터 tooindex, 자격 증명 및 hello 데이터 (예: 컬렉션 내 문서 수정 됨 또는 삭제)에 대 한 변경 식별에 대 한 정책을 지정 합니다. 여러 인덱서에서 사용할 수 있도록 독립적인 리소스로 hello 데이터 원본이 정의 되었습니다.

**인덱서** hello 데이터 흐름에서 데이터 원본을 대상 검색 인덱스에 설명 합니다. 인덱서를 사용하여 다음을 수행할 수 있습니다.

* Hello 데이터 toopopulate 인덱스의 일회성 복사를 수행 합니다.
* 일정에 따라 hello 데이터 소스에 변경한 내용으로 인덱스를 동기화 합니다. hello 일정은 hello 인덱서 정의의 일부입니다.
* 필요에 따라 요청 시 업데이트 tooan 인덱스를 호출 합니다.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>1단계: 데이터 소스 만들기
데이터 원본 toocreate 게시물을 수행 합니다.

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

hello hello 요청 본문 hello 다음 필드를 포함 해야 하는 hello 데이터 원본 정을 포함 되어 있습니다.

* **이름**: 모든 이름 toorepresent Cosmos DB 데이터베이스를 선택 합니다.
* **형식**: `documentdb`여야 합니다.
* **자격 증명**:
  
  * **connectionString**: 필수입니다. 형식에 따라 hello에서 hello 연결 정보 tooyour Azure Cosmos DB 데이터베이스를 지정 합니다.`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **컨테이너**:
  
  * **이름**: 필수입니다. 인덱싱된 hello Cosmos DB 컬렉션 toobe hello id를 지정 합니다.
  * **쿼리**: 선택 사항입니다. Azure 검색에서 인덱싱할 수 있는 플랫 스키마로 쿼리 tooflatten 임의의 JSON 문서를 지정할 수 있습니다.
* **dataChangeDetectionPolicy**: 권장 사항입니다. [변경된 문서 인덱싱](#DataChangeDetectionPolicy) 섹션을 참조하세요.
* **dataDeletionDetectionPolicy**: 선택 사항입니다. [삭제된 문서 인덱싱](#DataDeletionDetectionPolicy) 섹션을 참조하세요.

### <a name="using-queries-tooshape-indexed-data"></a>데이터를 인덱싱할 tooshape 쿼리를 사용 하 여
Cosmos DB 쿼리 tooflatten 중첩 속성 또는 배열 프로젝트 JSON 속성 및 인덱싱된 hello 데이터 toobe 필터링을 지정할 수 있습니다. 

예제 문서:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

필터 쿼리:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

평면화 쿼리:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
프로젝션 쿼리:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


배열 평면화 쿼리:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>2단계: 인덱스 만들기
대상 Azure 검색 인덱스가 아직 없으면 만듭니다. Hello를 사용 하 여 인덱스를 만들 수 [Azure 포털 UI](search-create-index-portal.md), hello [인덱스 REST API 만들기](/rest/api/searchservice/create-index) 또는 [Index 클래스](/dotnet/api/microsoft.azure.search.models.index)합니다.

다음 예제는 hello id 및 설명 필드와 인덱스를 만듭니다.

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

해당 hello 확인 대상 인덱스의 스키마는 hello 소스 JSON 문서의 hello 스키마 또는 사용자 지정 쿼리 프로젝션 hello 출력 호환 됩니다.

> [!NOTE]
> 분할 된 컬렉션에 대 한 hello 기본 문서 키가 Cosmos DB `_rid` 속성을 너무 기호의 이름이 바뀝니다`rid` Azure 검색에서 합니다. 또한 Cosmos DB의 `_rid` 값은 Azure Search 키에 유효하지 않은 문자를 포함합니다. 이러한 이유로 hello `_rid` 값은 Base64 인코딩.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON 데이터 형식과 Azure 검색 데이터 형식 사이의 매핑
| JSON 데이터 형식 | 호환되는 대상 인덱스 필드 형식 |
| --- | --- |
| Bool |Edm.Boolean, Edm.String |
| 정수와 같이 보이는 숫자 |Edm.Int32, Edm.Int64, Edm.String |
| 부동소수점처럼 보이는 숫자 |Edm.Double, Edm.String |
| String |Edm.String |
| 기본 형식의 배열, 예: ["a", "b", "c"] |Collection(Edm.String) |
| 날짜처럼 보이는 문자열 |Edm.DateTimeOffset, Edm.String |
| GeoJSON 개체, 예: { "type": "Point", "coordinates": [long, lat] } |Edm.GeographyPoint |
| 기타 JSON 개체 |해당 없음 |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>3단계: 인덱서 만들기

Hello 인덱스 및 데이터 소스를 만든 준비 toocreate hello 인덱서 수 있습니다.

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

이 인덱서는 2 시간 마다 실행 (일정 간격을 너무 설정 "PT2H"). 인덱서 toorun 30 분 마다 설정 hello 간격 너무 "에서는 PT30M"입니다. hello 가장 짧은 지원 되는 간격은 5 분입니다. hello 일정은 선택 사항-생략 하는 경우, 인덱서 만들어질 때 한 번만 실행 합니다. 그러나 언제든지 필요할 때 인덱서를 실행할 수 있습니다.   

에 대 한 자세한 내용은 hello 인덱서 API 만들기, 체크 아웃 [인덱서 만들기](https://docs.microsoft.com/rest/api/searchservice/create-indexer)합니다.

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>요청 시 인덱서 실행
인덱서 일정에 따라 주기적으로 더하기 toorunning에서 필요에 따라 호출 될 수도 있습니다.

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> API 실행 결과 반환 하는 경우에 hello 인덱서 호출이 예약 되었습니다 하지만 hello 실제 처리는 비동기적으로 발생 합니다. 

Hello 포털 또는 가져오기 인덱서 상태 API 옆에서는 설명 하는 hello를 사용 하 여 hello 인덱서 상태를 모니터링할 수 있습니다. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>인덱서 상태 가져오기
인덱서의 hello 상태와 실행 기록을 검색할 수 있습니다.

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

전반적인 인덱서 상태, hello 마지막 (또는 진행 중) 인덱서 호출 및 최근 인덱서 호출 기록 hello hello 응답에 포함 되어 있습니다.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

실행 기록을 toohello 50 가장 최근 실행을 완료 합니다 (hello 최신 실행 hello에 대 한 응답에 먼저) 하므로 시간 순서 대로 정렬 되는 포함 되어 있습니다.

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>변경된 문서 인덱싱
hello 용도 데이터 변경 검색 정책을 tooefficiently 변경 된 데이터 항목을 식별 합니다. 현재 지원만 hello 정책은 hello `High Water Mark` hello를 사용 하 여 정책을 `_ts` 다음과 같이 지정 된 Cosmos DB에서 제공 하는 (타임 스탬프) 속성:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

이 정책을 사용 하 여 tooensure 좋은 인덱서 성능 가장 좋습니다. 

사용자 지정 쿼리를 사용 하는 경우 해야 해당 hello `_ts` 속성 hello 쿼리에 의해 프로젝션 됩니다.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>증분 진행률 및 사용자 지정 쿼리
인덱싱하는 동안 진행률 인덱서 실행이 일시적 오류 또는 실행 시간 제한에 의해 중단 되 면 hello 인덱서 중단 된 다음 번 것 처음부터 toore 인덱스 hello 전체 컬렉션을 대신 실행을 가져올 수를 확인 합니다. 대규모 컬렉션을 인덱싱할 때 특히 유용합니다. 

사용자 지정 쿼리를 사용 하는 경우 증분 진행률 tooenable hello 하 여 hello 결과 정렬 하 여 쿼리 확인 `_ts` 열입니다. 따라서 정기적으로 검사를 가리키는 Azure 검색 tooprovide에 대 한 진행률 정보를 사용 하 여 오류의 hello 있을 수 있습니다.   

쿼리에 포함 된 경우에 일부 경우에는 `ORDER BY [collection alias]._ts` 절, Azure 검색 hello 별로 해당 hello 쿼리가 정렬 되 유추 하지 않을 수 있습니다 `_ts`합니다. 있으신가요 Azure 검색 결과 hello를 사용 하 여 정렬 됩니다 `assumeOrderByHighWaterMarkColumn` 구성 속성이 있습니다. toospecify이이 힌트를 만들거나 다음과 같이 인덱서를 업데이트 합니다. 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>삭제된 문서 인덱싱
Hello 컬렉션에서 행을 삭제 하는 경우 일반적으로 원하는 toodelete도 hello 검색 인덱스의 행입니다. 데이터 삭제 검색 정책의 hello 목적은 tooefficiently 삭제 된 데이터 항목을 식별 합니다. 현재 지원만 hello 정책은 hello `Soft Delete` 정책 (삭제는 일종의 플래그로 표시), 다음과 같이 지정 됩니다.

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

사용자 지정 쿼리를 사용 하는 경우 확인에서 참조 하는 hello 속성 `softDeleteColumnName` hello 쿼리에 의해 프로젝션 됩니다.

다음 예제는 hello 일시 삭제 정책을 사용 하 여 데이터 원본을 만듭니다.

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>다음 단계
축하합니다. Cosmos db toointegrate Azure Cosmos DB를 사용 하 여 Azure 검색 인덱서 hello 하는 방법을 배웠습니다.

* hello를 참조 하는 방법에 대 한 Azure Cosmos DB toolearn [Cosmos DB 서비스 페이지](https://azure.microsoft.com/services/documentdb/)합니다.
* Azure 검색에 대해 자세히 어떻게 toolearn 참조 hello [검색 서비스 페이지](https://azure.microsoft.com/services/search/)합니다.
