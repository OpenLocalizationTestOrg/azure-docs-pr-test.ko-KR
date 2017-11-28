---
title: "Azure SQL 데이터베이스 tooAzure aaaConnecting 검색 인덱서를 사용 하 여 | Microsoft Docs"
description: "Toopull 데이터를 Azure SQL 데이터베이스 tooan Azure 검색 인덱서를 사용 하 여 인덱스 방법에 대해 알아봅니다."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Azure SQL 데이터베이스 tooAzure 연결 인덱서를 사용 하 여 검색

[Azure Search 인덱스](search-what-is-an-index.md)를 쿼리하기 전에 데이터를 채워야 합니다. Hello 데이터는 Azure SQL 데이터베이스에 거주 하는 경우는 **Azure SQL 데이터베이스에 대 한 Azure 검색 인덱서** (또는 **Azure SQL 인덱서** 줄여서) 코드 toowrite 여백을 제외 하 고 덜 hello 인덱싱 프로세스를 자동화할 수 에 대 한 인프라 toocare 합니다.

이 문서에서는 hello 메커니즘을 사용 하 여 [인덱서](search-indexer-overview.md), 하지만 Azure SQL 데이터베이스 (예를 들어 통합된 변경 내용 추적)와 사용할 수 있는 기능에 대해서도 설명 합니다. 

또한 tooAzure SQL 데이터베이스, Azure 검색에 대 한 인덱서를 제공 [Azure Cosmos DB](search-howto-index-documentdb.md), [Azure Blob 저장소](search-howto-indexing-azure-blob-storage.md), 및 [Azure 테이블 저장소](search-howto-indexing-azure-tables.md)합니다. hello에 사용자 의견을 제공 하는 다른 데이터 원본에 대 한 toorequest 지원 [Azure 검색 사용자 의견 포럼](https://feedback.azure.com/forums/263029-azure-search/)합니다.

## <a name="indexers-and-data-sources"></a>인덱서 및 데이터 원본

A **데이터 소스** 데이터 액세스 및 hello 데이터 (새, 수정 또는 삭제 된 행)의 변경 내용을 효율적으로 식별 하는 정책에 대 한 자격 증명, 어떤 데이터 tooindex를 지정 합니다. 이는 독립된 리소스로 정의되므로 여러 인덱서에서 사용할 수 있습니다.

**인덱서**는 단일 데이터 원본을 대상 검색 인덱스에 연결하는 리소스입니다. 인덱서는 hello 같은 방법으로 다음에 사용 됩니다.

* Hello 데이터 toopopulate 인덱스의 일회성 복사를 수행 합니다.
* 일정에 따라 hello 데이터 소스에 변경한 내용으로 인덱스를 업데이트 합니다.
* 요청 시 tooupdate 필요에 따라 인덱스를 실행 합니다.

단일 인덱서는 테이블 또는 뷰를 하나에 사용할 수 있지만 toopopulate 검색 인덱스를 여러 개를 원하는 경우 여러 인덱서를 만들 수 있습니다. 개념에 대한 자세한 내용은 [인덱서 작업: 일반적인 워크플로](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow)를 참조하세요.

다음을 사용하여 Azure SQL 인덱서를 설정하고 구성할 수 있습니다.

* Hello에서 데이터 가져오기 마법사 [Azure 포털](https://portal.azure.com)
* Azure Search [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* Azure Search [REST API](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations)

이 문서에서는 hello REST API toocreate 사용 **인덱서** 및 **데이터 소스**합니다.

## <a name="when-toouse-azure-sql-indexer"></a>때 toouse Azure SQL 인덱서
Tooyour 데이터와 관련 된 몇 가지 요인에 따라 hello 사용 하 여 Azure SQL 인덱서 수도 적합할 수 있습니다. 데이터 요구 사항을 준수 하는 hello 맞으면 Azure SQL 인덱서를 사용할 수 있습니다.

| 조건 | 세부 정보 |
|----------|---------|
| 단일 테이블 또는 뷰에서 발생한 데이터 | Hello 데이터가 여러 테이블에 분산 되어, hello 데이터의 단일 뷰를 만들 수 있습니다. 그러나 뷰를 사용 하는 경우 수 toouse와 통합 하는 SQL Server 변경 감지 toorefresh 증분 변경 내용 사용 하는 인덱스가 수 없습니다. 자세한 내용은 아래의 [변경 및 삭제된 행 캡처](#CaptureChangedRows)를 참조하세요. |
| 호환되는 데이터 형식 | Azure 검색 인덱스에서 대부분 hello SQL 유형이 지원 됩니다. 목록은 [데이터 형식 매핑](#TypeMapping)을 참조하세요. |
| 실시간 데이터 동기화가 필요하지 않습니다. | 인덱서는 최대 5분마다 테이블을 다시 인덱싱할 수 있습니다. 변경 되 면 데이터 변경 내용을 자주 및 hello 단일 분 또는 초 내에 hello 인덱스에 반영 하는 필요성 toobe hello를 사용 하는 것이 좋습니다 [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) 또는 [.NET SDK](search-import-data-dotnet.md) toopush 직접 행을 업데이트 합니다. |
| 증분 인덱싱 가능 | 큰 데이터 집합 및 일정에 따라 Azure 검색 계획 toorun hello 인덱서 수 있어야 하는 경우 tooefficiently 새, 변경 또는 삭제 된 행을 식별 합니다. 비-증분 인덱싱은 주문 시(일정을 따르지 않고) 인덱싱하거나 100,000 미만의 행을 인덱싱하는 경우에만 허용됩니다. 자세한 내용은 아래의 [변경 및 삭제된 행 캡처](#CaptureChangedRows)를 참조하세요. |

## <a name="create-an-azure-sql-indexer"></a>Azure SQL 인덱서 만들기

1. Hello 데이터 원본 만들기:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Hello에서 hello 연결 문자열을 가져올 수 있습니다 [Azure 포털](https://portal.azure.com); hello를 사용 하 여 `ADO.NET connection string` 옵션입니다.

2. 없는 이미 hello 대상 Azure 검색 인덱스를 만듭니다. Hello를 사용 하 여 인덱스를 만들 수 [포털](https://portal.azure.com) 또는 hello [인덱스 API 만들기](https://docs.microsoft.com/rest/api/searchservice/Create-Index)합니다. 해당 hello 확인 대상 인덱스의 스키마는 hello 원본 테이블의 hello 스키마와 호환-참조 [SQL과 Azure 검색 간에 데이터 형식 매핑](#TypeMapping)합니다.

3. 이름을 지정 하 고 hello 데이터 원본 및 대상 인덱스를 참조 하 여 hello 인덱서를 만듭니다.

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

이 방법으로 만든 인덱서에는 일정이 없습니다. 만들어지면 자동으로 한 번 실행됩니다. 언제든지 **run indexer** 요청을 사용하여 다시 실행할 수 있습니다.

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

인덱서 동작의 몇 가지 측면(예: 배치 크기, 인덱서 실행에 실패하기 전에 건너뛸 수 있는 문서 수)을 사용자 지정할 수 있습니다. 자세한 내용은 [인덱서 API 만들기](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer)를 참조하세요.

Azure 서비스 tooconnect tooyour 데이터베이스 tooallow 할 수 있습니다. 참조 [Azure에서 연결](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) 방법에 대 한 지침은 toodo입니다.

인덱서 상태와 실행 기록을 (인덱싱된 항목 수, 실패 등), 사용 하 여 toomonitor hello는 **인덱서 상태** 요청:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

hello 응답에는 비슷한 toohello 다음과 같아야 합니다.

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

실행 기록을 (있도록 hello 최신 실행 hello에 대 한 응답에 먼저) hello 시간 순서 대로 정렬 되는 가장 최근에 완료 하는 hello 실행 too50를 포함 합니다.
hello 응답에 대 한 추가 정보를 찾을 수 [인덱서 상태 가져오기](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>일정에 따라 인덱서 실행
일정에 따라 주기적으로 hello 인덱서 toorun를 정렬할 수 있습니다. toodo이 hello 추가 **일정** 만들거나 hello 인덱서를 업데이트할 때 속성입니다. 다음 예제에서는 hello PUT 요청 tooupdate hello 인덱서를 보여 줍니다.

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

hello **간격** 매개 변수는 필수입니다. hello 간격에는 두 개의 연속 된 인덱서 실행의 시작 부분 hello 사이의 toohello 시간을 참조합니다. hello 최소 간격은 5 분이 허용 가장 긴 hello은 1 일입니다. 형식은 XSD "dayTimeDuration" 값( [ISO 8601 기간](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) 값의 제한된 하위 집합)이어야 합니다. 이 대 한 hello 패턴은: `P(nD)(T(nH)(nM))`합니다. 예를 들어 15분 간격이면 `PT15M`, 2시간 간격이면 `PT2H`입니다.

선택적 hello **startTime** 때 hello 예약된 실행은 시작 하 여 시작을 나타냅니다. 생략 하는 hello 현재 UTC 시간이 사용 됩니다. 이 시간 이전 – hello 인덱서 hello startTime 이후 지속적으로 실행 된 경우에 처럼 hello 첫 번째 실행 예약 되는 경우 hello 있을 수 있습니다.  

인덱서의 실행은 한 번에 하나만 실행할 수 있습니다. 인덱서 실행이 예약 된 시점을 실행 중인 경우 hello 실행 hello 다음 번 예약된 시간까지 연기 됩니다.

이 예제에서는 toomake를 생각해 봅시다 더 구체적입니다. 구성 된 매시간 일정에 따라 hello म 있다고 가정 합니다.

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

다음과 같은 상황이 발생합니다.

1. 2015 년 3 월 1 일 오전 12시 주위 또는 hello 첫 번째 인덱서 실행 시작 시작됩니다.
2. 이 실행에 20분(또는 1시간 미만의 기간)이 걸리는 것으로 가정합니다.
3. 2015 년 3 월 1 일 오전 1시 주위 또는 hello 두 번째 실행이 시작
4. 이제 이 실행이 오전 2시 10분경에 완료되도록 1시간이 넘게(예: 70분) 걸린다고 가정해 보겠습니다.
5. 세 번째 실행 toostart hello에 대 한 시간을 오전 2 시 있습니다. 그러나 때문에 두 번째 실행 오전 1 시부터 hello 계속 실행 되는 hello 세 번째 실행을 건너뜁니다. 오전 3 시 hello 세 번째 실행이 시작

**PUT indexer** 요청을 사용하여 기존 인덱서에 대한 일정을 추가, 변경 또는 삭제할 수 있습니다.

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>새 행, 변경된 행 및 삭제된 행 캡처

Azure 검색에 사용 하 여 **증분 인덱싱** tooavoid toore 인덱스 전체 테이블이 hello 또는 인덱서가 실행 될 때마다 뷰를 포함 합니다. Azure 검색 두 변경 검색 정책을 toosupport 증분 인덱싱를 제공 합니다. 

### <a name="sql-integrated-change-tracking-policy"></a>SQL 통합 변경 내용 추적 정책
SQL 데이터베이스에서 [변경 내용 추적](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server)을 지원하는 경우 **SQL 통합 변경 내용 추적 정책**을 사용하는 것이 좋습니다. Hello 가장 효율적인 정책입니다. 또한 있습니다 Azure 검색 삭제 tooidentify 행 tooadd 필요 없이 명시적 "소프트 삭제" 열 tooyour 테이블을.

#### <a name="requirements"></a>요구 사항 

+ 데이터베이스 버전 요구 사항:
  * SQL Server 2012 SP3 이상(Azure VM에서 SQL Server를 사용하는 경우)
  * Azure SQL 데이터베이스 V12(Azure SQL 데이터베이스를 사용하는 경우)
+ 테이블만(뷰 제외). 
+ Hello 데이터베이스에서 [설정 변경 내용 추적](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) hello 테이블에 대 한 합니다. 
+ 복합 기본 키 (기본 키 포함 하는 둘 이상의 열이 하나) hello 테이블에 있습니다.  

#### <a name="usage"></a>사용

toouse이이 정책을 만들거나 다음과 같이 데이터 소스를 업데이트 합니다.

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

SQL 통합 변경 내용 추적 정책을 사용할 때는 별도의 데이터 삭제 검색 정책을 지정하지 마세요. 이 정책은 삭제된 행 식별을 기본적으로 지원합니다. 그러나 hello 삭제 검색 toobe "자동"에 대 한 검색 인덱스에 hello 문서 키 해야 수 hello hello hello SQL 테이블의에서 기본 키와 동일 합니다. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>상위 워터마크 변경 검색 정책

이 변경 검색 정책 hello 버전 또는 행을 마지막으로 수정한 시간 캡처 "최고 수 위 표시" 열에 의존 합니다. 뷰를 사용하는 경우 상위 워터 마크 정책을 사용해야 합니다. hello 상위 워터 마크 열 hello 요구 사항을 준수를 충족 해야 합니다.

#### <a name="requirements"></a>요구 사항 

* 모든 삽입 hello 열에 대 한 값을 지정 합니다.
* 모든 업데이트 tooan 항목은 또한 hello 열의 hello 값을 변경 합니다.
* hello 값이 열의 각 삽입 또는 업데이트에 따라 카운터가 증가 합니다.
* 위치를 다음 쿼리로 hello 및 ORDER BY 절을 효율적으로 실행할 수 있습니다.`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Hello를 사용 하는 것이 좋습니다 [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) hello 상위 워터 마크 열의 데이터 형식입니다. 다른 모든 데이터 형식은 사용 되는 경우 변경 내용 추적에 인덱서 쿼리와 동시에 실행 되는 트랜잭션은의 hello 존재에 모든 변경 내용 toocapture를 보장 되지 않습니다. 사용 하는 경우 **rowversion** 읽기 전용 복제본으로 구성에서는 hello 주 복제본에서 hello 인덱서를 가리켜야 합니다. 데이터 동기화 시나리오에는 주 복제본만 사용할 수 있습니다.

#### <a name="usage"></a>사용

toouse 상위 워터 마크 정책 만들거나 다음과 같이 데이터 소스를 업데이트 합니다.

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Hello 원본 테이블에 인덱스가 없으면 hello 상위 워터 마크 열에 hello SQL 인덱서 사용 하는 쿼리 시간 초과 될 수 있습니다. 특히 hello `ORDER BY [High Water Mark Column]` 절 필요 인덱스 toorun 효율적으로 hello 테이블 행을 많이 포함 하는 경우.
>
>

시간 초과 오류가 발생 하면 hello를 사용할 수 있습니다 `queryTimeout` 인덱서 구성 설정 tooset hello 쿼리 제한 시간 tooa 보다 큰 값 hello 기본 5 분 시간 제한입니다. 예를 들어 tooset hello timeout too10 분 만들거나 같은 구성이 hello로 hello 인덱서를 업데이트 합니다.

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Hello을 사용 하지 않도록 설정할 `ORDER BY [High Water Mark Column]` 절. 그러나이 바람직하지에 있기 때문에 오류가 발생 하 여 hello 인덱서 실행이 중단 되 면 hello 인덱서 toore 프로세스 모든 행-나중에 실행 되 면 hello 인덱서 이미 중단 된 hello 시간별 거의 모든 hello 행 처리 하는 경우에 합니다. toodisable hello `ORDER BY` 절을 사용 하 여 hello `disableOrderByHighWaterMarkColumn` hello 인덱서 정의에 설정 합니다.  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Soft Delete 열 삭제 검색 정책
Hello 원본 테이블에서 행을 삭제 하는 경우 싶을 toodelete도 hello 검색 인덱스의 행입니다. 사용 하는 경우 hello SQL 통합 변경 내용 추적 정책을,이 안전 하다 드립니다. 그러나 hello 상위 워터 마크 변경 내용 추적 정책을 삭제 된 행에 도움이 되지 않습니다. 어떤 toodo?

Hello 행을 물리적으로 hello 테이블에서 제거할 경우 Azure 검색에 더 이상 존재 하는 레코드의 방법은 tooinfer hello 표시 되지 않습니다.  그러나 hello 테이블에서 제거 하지 않고 "소프트 삭제" hello 기술을 toologically 행 삭제를 사용할 수 있습니다. 열 tooyour 테이블 또는 뷰를 추가 하 고 해당 열을 사용 하 여 삭제할 것으로 행을 표시 합니다.

Hello 소프트 삭제 기술을 사용 하는 경우 지정할 수 있습니다 hello 일시 삭제 정책을 다음과 같이 만들거나 hello 데이터 소스를 업데이트할 때.

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

hello **softDeleteMarkerValue** 문자열 이어야-사용자가 실제 값의 문자열 표현을 hello를 사용 해야 합니다. 예를 들어 있으면 hello 값이 1 인 표시 된 삭제 된 행 정수 열을 사용 하 여 `"1"`합니다. BIT 열 hello 부울 값 true로 표시 된 삭제 된 행이 있으면 사용 하 여 `"True"`합니다.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>SQL과 Azure Search 데이터 형식 사이의 매핑
| SQL 데이터 형식 | 허용되는 대상 인덱스 필드 유형 | 참고 사항 |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, money decimal numeric |Edm.String |Azure 검색에서는 decimal 형식을 Edm.Double로 변환하면 정밀도가 떨어지기 때문에 이를 지원하지 않습니다. |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |SQL 문자열 hello 문자열이 나타내면 문자열의 JSON 배열을 사용 하는 toopopulate collection (edm.string) 필드 될 수 있습니다.`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| geography |Edm.GeographyPoint |SRID가 4326 (hello 기본값) 인 POINT 유형의 지리 인스턴스만 지원 됩니다. |
| rowversion |해당 없음 |변경 내용 추적에 사용할 수 있지만 행 버전 열 hello 검색 인덱스에 저장할 수 없습니다. |
| time, timespan, binary, varbinary, image, xml, geometry, CLR types |해당 없음 |지원되지 않음 |

## <a name="configuration-settings"></a>구성 설정
SQL 인덱서는 여러 구성 설정을 노출합니다.

| 설정 | 데이터 형식 | 목적 | 기본값 |
| --- | --- | --- | --- |
| queryTimeout |string |집합 hello SQL 쿼리 실행에 대 한 제한 시간 |5분("00:05:00") |
| disableOrderByHighWaterMarkColumn |bool |Hello 상위 워터 마크 정책 tooomit hello ORDER BY 절에서 사용 하는 hello SQL 쿼리를 하면 합니다. [상위 워터 마크 정책](#HighWaterMarkPolicy)을 참조하세요. |false |

이러한 설정은 hello에 사용 됩니다 `parameters.configuration` hello 인덱서 정의의 개체가 있습니다. 예를 들어 tooset hello 쿼리 제한 시간 too10 분 만들거나 같은 구성이 hello로 hello 인덱서를 업데이트 합니다.

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>FAQ

**Q:** Azure의 IaaS VM에서 실행되는 SQL 데이터베이스에서 Azure SQL 인덱서를 사용할 수 있습니까?

예. 그러나 tooallow 사용자 검색 서비스 tooconnect tooyour 데이터베이스가 필요 합니다. 자세한 내용은 참조 [Azure VM에서 Azure 검색 인덱서 tooSQL 서버에서에서 연결을 구성](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md)합니다.

**Q:** 온-프레미스에서 실행되는 SQL 데이터베이스에서 Azure SQL 인덱서를 사용할 수 있습니까?

직접 끌 수는 없습니다. 것을 권장 하거나 이렇게 하면 필요한 데 tooopen 있습니다 데이터베이스 tooInternet 트래픽을 직접 연결을 지원 마십시오 했습니다. 고객은 Azure Data Factory와 같은 브리지 기술을 사용하여 이 시나리오를 성공적으로 수행했습니다. 자세한 내용은 참조 [Azure 데이터 팩터리를 사용 하 여 밀어넣기 데이터 tooan Azure 검색 인덱스](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector)합니다.

**Q:** Azure의 IaaS에서 실행되는 SQL Server가 아닌 데이터베이스에서 Azure SQL 인덱서를 사용할 수 있습니까?

아니요. Hello 인덱서 SQL Server 이외의 다른 데이터베이스를 테스트 하지 않았습니다 때문에이 시나리오에서는 지원 되지 않습니다.  

**Q:** 일정에 따라 실행되는 여러 인덱서를 만들 수 있습니까?

예. 그러나 한 번에 하나의 인덱서만 실행할 수 있습니다. 여러 인덱서를 동시에 실행 해야 할 경우에 검색 단위 하나 보다 검색 서비스 toomore 프로그램를 확장 하는 것이 좋습니다.

**Q:** 인덱서를 실행하면 쿼리 작업이 영향을 받습니까?

예. 검색 서비스의 hello 노드 중 하나에서 인덱서를 실행 하 고 해당 노드의 리소스 인덱싱 및 쿼리 트래픽 및 기타 API 요청을 처리 간에 공유 됩니다. 많은 인덱싱 및 쿼리 작업을 실행하는 경우 503 오류가 자주 발생하거나 응답 시간이 증가하면 [검색 서비스를 확장](search-capacity-planning.md)하는 것이 좋습니다.

**Q: [장애 조치(failover) 클러스터](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)에서 데이터 원본으로 보조 복제본을 사용할 수 있습니까?**

경우에 따라 다릅니다. 테이블 또는 뷰의 전체 인덱싱에 대해 보조 복제본을 사용할 수 있습니다. 

증분 인덱싱의 경우 Azure Search는 SQL 통합 변경 내용 추적 및 상위 워터 마크라는 두 가지 변경 검색 정책을 지원합니다.

읽기 전용 복제본에서 SQL 데이터베이스는 통합된 변경 내용 추적을 지원하지 않습니다. 따라서 상위 워터 마크 정책을 사용해야 합니다. 

표준 권장 사항은 hello 상위 워터 마크 열에 대 한 toouse hello rowversion 데이터 형식. 그러나 rowversion 사용 시 SQL Database의 `MIN_ACTIVE_ROWVERSION` 함수를 사용하는 데, 이는 읽기 전용 복제본에서는 지원되지 않습니다. 따라서 rowversion를 사용 하는 경우 hello 인덱서 tooa 주 복제본을 지정 해야 합니다.

읽기 전용 복제본에 toouse rowversion을 시도 하면 hello 다음 오류가 표시 됩니다. 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**Q: 상위 워터 마크 변경 내용 추적에 대체의 rowversion이 아닌 열을 사용할 수 있습니까?**

권장되지 않습니다. 신뢰할 수 있는 데이터 동기화를 위해서는 **rowversion**만 허용됩니다. 그러나 응용 프로그램 논리에 따라 다음과 같은 경우 안전할 수 있습니다.

+ hello 인덱서 실행 될 때 처리 중인 트랜잭션이 없는 인덱싱하는 hello 테이블에서 확인할 수 (예를 들어 모든 테이블 업데이트 된 일정에 따라 일괄 처리로 수행 하 고 hello Azure 검색 인덱서 일정 hello 테이블과 겹치는 tooavoid 설정 되어 업데이트 일정)입니다.  

+ 정기적으로 누락 된 모든 행을 전체 다시 인덱싱을 toopick을 수행합니다. 
