---
title: "Azure Cosmos DB DocumentDB API에 대 한 쿼리 메트릭을 aaaSQL | Microsoft Docs"
description: "Tooinstrument 및 디버그 hello Azure Cosmos DB 요청 SQL 쿼리 성능 방법에 대해 알아봅니다."
keywords: "sql 구문, sql 쿼리, 여러 SQL 쿼리, json 쿼리 언어, 데이터베이스 개념 및 sql 쿼리, 집계 함수"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Azure Cosmos DB와 함께 쿼리 성능 튜닝
Azure Cosmos DB에서는 스키마 또는 보조 인덱스를 요구하지 않고도 [데이터를 쿼리하기 위한 SQL API](documentdb-sql-query.md)를 제공합니다. 이 문서에서는 hello를 다음 개발자를 위한 정보를 제공 합니다.

* Azure Cosmos DB의 SQL 쿼리 실행 작동 방식에 대한 대략적인 정보
* 쿼리 요청 및 응답 헤더, 클라이언트 SDK 옵션에 대한 세부 정보
* 쿼리 성능에 대한 팁 및 모범 사례
* SQL 실행 통계 toodebug tooutilize 성능을 쿼리 하는 방법의 예

## <a name="about-sql-query-execution"></a>SQL 쿼리 실행 정보

Azure Cosmos DB tooany 증가할 수 있는 컨테이너의 데이터를 저장할 [저장소 크기 또는 요청 처리량](partition-data.md)합니다. Azure Cosmos DB hello 표지 toohandle 데이터 증가 또는 프로 비전 된 처리량을 증가 실제 파티션 간에 데이터를 원활 하 게 조정합니다. Hello REST API 또는 hello 지원 중 하나를 사용 하 여 SQL 쿼리 tooany 컨테이너를 실행할 수 있습니다 [DocumentDB Sdk](documentdb-sdk-dotnet.md)합니다.

분할에 대한 간략한 개요: 데이터를 실제 파티션 간에 분할하는 방법을 결정하는 파티션 키(예: “city”)를 정의합니다. 데이터 속하는 tooa 단일 파티션 키 (예를 들어 "city" "Seattle" = =) 실제 파티션 내에 저장 하지만 일반적으로 단일 실제 파티션의 파티션 키가 여러 개 있습니다. 파티션 저장소 크기에 도달 하면 hello 서비스 원활 하 게 hello 파티션 새로운 두 개의 파티션으로 분할 하 고 이러한 파티션에서 hello 파티션 키를 균등 하 게 나눕니다. 파티션을 일시적으로 hello Api 사용 하 여 추상화의 "파티션 키 범위는" hello 범위 파티션 키 해시를 나타냅니다. 

쿼리 tooAzure Cosmos DB를 실행 하면 hello SDK 다음 논리 단계를 수행 합니다.

* Hello SQL 쿼리 toodetermine hello 쿼리 실행 계획을 구문 분석 합니다. 
* 다음과 같은 hello 쿼리 hello 파티션 키에 대 한 필터를 포함 하는 경우 `SELECT * FROM c WHERE c.city = "Seattle"`, 라우트된 tooa는 단일 파티션 합니다. Hello 쿼리 파티션 키에 대 한 필터 없을 면 모든 파티션에서 실행 되 고 결과 병합 됩니다 클라이언트 쪽입니다.
* hello 쿼리 계열의 각 파티션 내에서 실행 또는 클라이언트 구성에 따라 병렬, 합니다. 각 파티션에서 hello 쿼리 하나를 수행할 수 또는 더 왕복 hello 쿼리 복잡성에 따라 구성 된 페이지 크기 및 처리량 hello 컬렉션의 사용자를 프로 비전 합니다. Hello 개수를 반환 하는 각 실행 [요청 단위](request-units.md) 및 필요에 따라 쿼리 실행에서 쿼리 실행 통계를 사용 합니다. 
* hello SDK 파티션에서 hello 쿼리 결과의 요약을 수행합니다. 예를 들어 hello 쿼리는 ORDER BY 여러 파티션에 있을 경우 다음 개별 파티션의 결과를 tooreturn 병합 정렬 결과 전체적으로 정렬 된 순서로 되어 있습니다. Hello 쿼리 등의 집계는 경우 `COUNT`, 개별 파티션에서 hello 수는 합한 tooproduce hello 전체 수입니다.

hello Sdk 쿼리 실행에 대 한 다양 한 옵션을 제공합니다. 예를 들어.NET 이러한 옵션은 hello에서 사용할 수 있는 `FeedOptions` 클래스입니다. hello 다음 표에 이러한 옵션 및 쿼리 실행 시간에 미치는 영향 있습니다. 

| 옵션 | 설명 |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Toobe 파티션이 둘 이상에서 실행 해야 하는 모든 쿼리에 tootrue는 설정 되어야 합니다. 이 명시적 플래그 tooenable 개발 기간 동안 toomake 합리적인 성능 균형 있습니다. |
| `EnableScanInQuery` | 설정 되어야 합니다 tootrue 인덱싱에서 옵트아웃 했습니다 있지만 그래도 검색을 통해 toorun hello 쿼리를 원하는 경우. Hello에 대 한 인덱싱을 경우 해당 요청에 필터 경로 사용할 수 없습니다. | 
| `MaxItemCount` | hello 왕복 toohello 서버당 tooreturn 항목의 최대 수입니다. 너무-1을 설정 하 여 hello 서버 hello 항목 수를 관리 하도록 할 수 있습니다. 또는이 값 tooretrieve 소수의 왕복에 따라 항목을 낮출 수 있습니다. 
| `MaxBufferedItemCount` | 클라이언트 쪽 옵션 이며 크로스 파티션 ORDER BY 수행할 때 toolimit hello 메모리 소비를 사용 하십시오. 더 높은 값 크로스 파티션 정렬 hello 대기 시간을 줄일 수 있습니다. |
| `MaxDegreeOfParallelism` | Hello hello Azure DocumentDB 데이터베이스 서비스에서에서 병렬 쿼리 실행 중에 클라이언트 쪽을 실행 하는 동시 작업 수를 가져오거나 설정 합니다. 양수 속성 값을 넘 toohello 집합 값의 hello 수를 제한합니다. 0 보다 tooless에 설정 된 경우 hello 시스템 hello toorun 동시 작업 수를 자동으로 결정 합니다. |
| `PopulateQueryMetrics` | 컴파일 시간, 인덱스 루프 시간 및 문서 로드 시간과 같은 다양한 쿼리 실행 단계에서 소요한 시간에 대한 통계 정보를 자세히 로깅할 수 있습니다. Azure 지원 toodiagnose 쿼리 성능 문제에 쿼리 통계의 출력을 공유할 수 있습니다. |
| `RequestContinuation` | 모든 쿼리에 의해 반환 된 hello 불투명 연속 토큰을 전달 하 여 쿼리 실행을 재개할 수 있습니다. hello continuation 토큰 쿼리 실행에 필요한 모든 상태를 캡슐화 합니다. |
| `ResponseContinuationTokenLimitInKb` | Hello hello 서버에서 반환 된 hello 연속 토큰의 최대 크기를 제한할 수 있습니다. 이 필요할 수 있습니다 tooset 응용 프로그램 호스트에 응답 헤더 크기에 제한 된 경우. 이 속성 설정 hello 증가할 수 있습니다 전체 기간과 RUs hello 쿼리에 대 한 사용 합니다.  |

예를 들어 보겠습니다 예제 쿼리는 파티션 키를 사용 하 여 컬렉션에서 요청에 `/city` hello 파티션으로 키 및 100000 000RU/s 처리량의를 통해 프로 비전 합니다. 이 쿼리를 사용 하 여 요청 `CreateDocumentQuery<T>` hello 다음과 같은.NET에서:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

hello SDK 조각 위에 표시 된 해당 toohello REST API 요청을 수행 합니다.

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Tooa REST API를 해당 하는 각 쿼리 실행 페이지 `POST` hello로 `Accept: application/query+json` 헤더 및 본문 hello에에서 hello SQL 쿼리 합니다. 각 쿼리를 사용 하면 하나 이상의 라운드 트립을 toohello 서버 hello로 또는 `x-ms-continuation` 토큰 클라이언트와 서버 hello tooresume 실행 간에 발생할 표시 됩니다. FeedOptions에서 hello 구성 옵션에는 요청 헤더의 hello 형태로 toohello 서버를 전달 됩니다. 예를 들어 `MaxItemCount` 너무 해당`x-ms-max-item-count`합니다. 

hello 요청을 반환 합니다 (보기 편하도록 자른) hello 다음 응답:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

hello 쿼리에서 반환 된 hello 키 응답 헤더 hello 다음과를 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
| `x-ms-item-count` | hello hello 응답에서 반환 하는 항목 수입니다. 이 제공 된 hello에 종속 `x-ms-max-item-count`, hello hello 최대 응답 페이로드 크기, hello 프로 비전 된 처리량 및 쿼리 실행 시간 내에 포함 될 수 있는 항목의 수입니다. |  
| `x-ms-continuation:` | hello 쿼리, 사용 가능한 추가 결과 hello 연속 토큰 tooresume 실행 합니다. | 
| `x-ms-documentdb-query-metrics` | hello hello 실행에 대 한 통계를 쿼리 합니다. 쿼리 실행의 다양 한 단계 hello에 소요 된 시간이 통계를 포함 하는 구분 기호로 분리 된 문자열입니다. 이면 반환된 `x-ms-documentdb-populatequerymetrics` 너무 설정`True`합니다. | 
| `x-ms-request-charge` | 수가 hello [요청 단위](request-units.md) hello 쿼리에 사용 합니다. | 

Hello REST API 요청 헤더 및 옵션에 대 한 내용은 참조 하십시오. [hello DocumentDB REST API를 사용 하 여 리소스를 쿼리](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api)합니다.

## <a name="best-practices-for-query-performance"></a>쿼리 성능에 대한 모범 사례
hello 다음은 Azure Cosmos DB 쿼리 성능에 영향을 주는 hello 가장 일반적인 요소입니다. 이 문서에서 이러한 각 항목에 대해 자세히 살펴보겠습니다.

| 비율 | 팁 | 
| ------ | -----| 
| 프로비전된 처리량 | 쿼리당 RU를 측정 하 고 쿼리에 대 한 프로 비전 된 처리량이 필요한 hello 있는지 확인 합니다. | 
| 분할 및 파티션 키 | 짧은 대기 시간에 대 한 hello 필터 절의 hello 파티션 키 값이 있는 쿼리를 선호 합니다. |
| SDK 및 쿼리 옵션 | 직접 연결 같은 SDK 모범 사례를 따르고 클라이언트 쪽 쿼리 실행 옵션을 조정합니다. |
| 네트워크 대기 시간 | 네트워크 오버 헤드가 측정에 대 한 계정 및 지역에 가장 가까운 멀티 호 밍 Api tooread hello에서 사용 합니다. |
| 인덱싱 정책 | 필요한 hello 인덱싱 경로/에 대 한 정책을 hello 쿼리 가졌는지 확인 합니다. |
| 쿼리 실행 메트릭 | Hello 쿼리 실행 메트릭 tooidentify 잠재적인 캡슐화 셰이프를 쿼리 및 데이터를 분석 합니다.  |

### <a name="provisioned-throughput"></a>프로비전된 처리량
Cosmos DB에서 각각 초당 RU(요청 단위)로 표현된 예약된 처리량을 포함하는 데이터의 컨테이너를 만듭니다. 1KB 문서의 읽기는 1 RU, 고 (쿼리 포함) 모든 작업은 고정 된 수의 복잡성에 따라 RUs의 정규화 된 tooa 합니다. 예를 들어 사용자 컨테이너에 대해 프로비전된 1000 RU/s가 있고 5RU를 사용하는 `SELECT * FROM c WHERE c.city = 'Seattle'`과 같은 쿼리가 있는 경우 이러한 쿼리는 초당 (1000 RU/s) / (5 RU/query) = 200 query/s를 수행할 수 있습니다. 

200 개 이상의 쿼리/초를 제출할 경우 hello 서비스 200/s 위에 속도 제한 들어오는 요청을 시작 합니다. 따라서 이러한 쿼리에 대 한 긴 대기 시간이 나타날 수 있습니다, hello Sdk 백오프/재시도 수행 하 여이 사례를 자동으로 처리 합니다. 사용자를 프로 비전 하는 hello 처리량 toohello 증가 값 쿼리 대기 시간 및 처리량 향상 필요 합니다. 

요청 단위에 대해 자세히 toolearn 참조 [요청 단위](request-units.md)합니다.

### <a name="partitioning-and-partition-keys"></a>분할 및 파티션 키
Azure Cosmos DB와 함께 일반적으로 쿼리는에 수행 hello 순서에 따라 가장 빠른/가장 효율적인에서 tooslower/덜 효율적입니다. 

* 단일 파티션 키 및 항목 키에 대해 GET 수행
* 단일 파티션 키에 대해 필터 절이 있는 쿼리
* 속성에 대해 같음 또는 범위 필터 절이 없는 쿼리
* 필터가 없는 쿼리

해당 필요 tooconsult 모든 파티션이 필요 높은 대기 시간을 쿼리하고 더 높은 RUs를 사용할 수 있습니다. 각 파티션의 모든 속성에 대해 자동 인덱싱에 있으므로 hello 쿼리 제공 될 수 효율적으로 hello 인덱스에서이 예제의 합니다. Hello 병렬 처리 수준 옵션을 사용 하 여 더 빠른 파티션을 걸쳐 있는 쿼리를 만들 수 있습니다.

분할 및 파티션 키에 대해 자세히 toolearn 참조 [Azure Cosmos DB에서 분할](partition-data.md)합니다.

### <a name="sdk-and-query-options"></a>SDK 및 쿼리 옵션
참조 [성능 팁](performance-tips.md) 및 [성능 테스트](performance-testing.md) tooget Azure Cosmos DB에서 클라이언트 쪽 성능에 가장 잘 hello 하는 방법에 대 한 합니다. 사용 하는 기본 연결 수를 가비지 수집의 빈도 같은 플랫폼 관련 구성을 구성 하 고 직접/TCP와 같은 경량 연결 옵션을 사용 하 여 최신 Sdk hello 합니다. 


#### <a name="max-item-count"></a>최대 항목 수
쿼리에 대 한 값의 hello `MaxItemCount` 종단 간 쿼리 시간에 상당한 영향을 미칠 수 있습니다. 각 왕복 toohello 서버는 hello의 항목 수를 초과 하지 않는 반환 `MaxItemCount` (기본값 100 개 항목). 이 tooa 더 높은 값으로 설정 (-1은 최대 및 권장) hello 서버와 클라이언트 큰 결과 집합이 쿼리의 간 왕복 수를 제한 하 여 전체 쿼리 기간 향상 됩니다.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>병렬 처리의 최대 수준
쿼리를 조정 hello `MaxDegreeOfParallelism` tooidentify hello hello 파티션 키 값에 대 한 필터) (없이 크로스 파티션 쿼리를 수행 하는 경우에 특히 응용 프로그램에 대 한 최상의 구성을 합니다. `MaxDegreeOfParallelism`hello 최대 병렬 태스크 수, 동시에 방문 하는 파티션 toobe hello 최대 즉,를 제어 합니다. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

다음을 가정해보세요.
* D = 기본 최대 개수의 병렬 작업이 (= hello 클라이언트 컴퓨터에서 프로세서의 총 수)
* P = 사용자 지정 최대 병렬 작업 수
* N = 방문 toobe에 대 한 쿼리 응답 해야 하는 파티션 수

다음은 P.의 여러 다른 값에 대 한 병렬 쿼리 hello이 작동 하는 방법의 의미
* (P == 0) => 직렬 모드
* (P == 1) => 한 작업의 최대
* (P > 1) => 최소(P, N) 병렬 작업 
* (P < 1) => 최소(N, D) 병렬 작업

SDK 릴리스 정보 및 구현된 클래스와 메서드에 대한 자세한 내용은 [DocumentDB SDK](documentdb-sdk-dotnet.md)를 참조하세요.

### <a name="network-latency"></a>네트워크 대기 시간
참조 [Azure Cosmos DB 글로벌 메일](tutorial-global-distribution-documentdb.md) tooset 글로벌 배포를 하 고 toohello 가장 가까운 지역을 연결 하는 방법에 대 한 합니다. 네트워크 대기 시간 toomake 여러 번 왕복 하거나 여러 큰 결과 hello 쿼리에서 집합을 검색할 때 쿼리 성능에 상당한 영향을에 있습니다. 

hello에 쿼리 실행 메트릭 설명 방법을 tooretrieve hello 서버 쿼리 실행 시간 ( `totalExecutionTimeInMs`), 네트워크 전송 중에 소요 된 시간 및 쿼리 실행에 걸린 시간 구별할 수 있도록 합니다.

### <a name="indexing-policy"></a>인덱싱 정책
인덱싱 경로, 종류, 모드 및 쿼리 실행에 어떻게 영향을 주는지에 대한 내용은 [인덱싱 정책 구성](indexing-policies.md)을 참조하세요. 기본적으로 hello 인덱싱 정책을 사용 하는 문자열에 대해 해시 인덱스가 유효 같음 쿼리에 하지만 범위 쿼리/쿼리 정렬 되지 않습니다. 범위 쿼리 문자열에 대 한 해야 할 경우 hello 모든 문자열에 대 한 범위 인덱스 유형을 지정 하는 것이 좋습니다. 

## <a name="query-execution-metrics"></a>쿼리 실행 메트릭
선택적 hello 전달 하 여 쿼리 실행에 자세한 메트릭을 가져올 수 있습니다 `x-ms-documentdb-populatequerymetrics` 헤더 (`FeedOptions.PopulateQueryMetrics` hello.NET SDK에에서). 반환 된 값을 hello `x-ms-documentdb-query-metrics` hello 고급 쿼리 실행의 문제 해결를 위한 사용 하는 키-값 쌍 뒤에 있습니다. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| 메트릭 | 단위 | 설명 | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | 밀리초 | 쿼리 실행 시간 | 
| `queryCompileTimeInMs` | 밀리초 | 쿼리 컴파일 시간  | 
| `queryLogicalPlanBuildTimeInMs` | 밀리초 | 런타임 toobuild 논리적 쿼리 계획 | 
| `queryPhysicalPlanBuildTimeInMs` | 밀리초 | 런타임 toobuild 실제 쿼리 계획 | 
| `queryOptimizationTimeInMs` | 밀리초 | 쿼리 최적화에 소요된 시간 | 
| `VMExecutionTimeInMs` | 밀리초 | 쿼리 런타임에 소요된 시간 | 
| `indexLookupTimeInMs` | 밀리초 | 실제 인덱스 계층에 소요된 시간 | 
| `documentLoadTimeInMs` | 밀리초 | 문서를 로드하는 데 소요된 시간  | 
| `systemFunctionExecuteTimeInMs` | 밀리초 | 시스템(기본 제공) 함수를 실행하는 데 소요된 총 시간(밀리초)  | 
| `userFunctionExecuteTimeInMs` | 밀리초 | 사용자 정의 함수를 실행하는 데 소요된 총 시간(밀리초) | 
| `retrievedDocumentCount` | 밀리초 | 검색된 총 문서 수  | 
| `retrievedDocumentSize` | 바이트 | 검색된 총 문서 크기(바이트)  | 
| `outputDocumentCount` | count | 출력 문서 수 | 
| `writeOutputTimeInMs` | 밀리초 | 쿼리 실행 시간(밀리초) | 
| `indexUtilizationRatio` | 비율(<=1) | 로드 된 문서의 hello 필터 toohello 수와 일치 하는 문서 수의 비율  | 

hello 클라이언트 Sdk 내부적으로 못할 각 파티션 내에서 여러 쿼리 작업 tooserve hello 쿼리 합니다. 파티션 별 총 결과가 hello를 초과 하는 경우 둘 이상의 호출을 수행 하는 클라이언트 hello `x-ms-max-item-count`쿼리 페이로드 페이지당 hello 최대 크기에 도달할 경우 hello 또는 쿼리 hello에 도달할 경우 hello hello 쿼리가 hello hello 파티션에 대 한 프로 비전 된 처리량을 초과 하는 경우, 시스템 할당 시간 제한입니다. 부분적 쿼리 실행은 각각 해당 페이지에 대해 `x-ms-documentdb-query-metrics`를 반환합니다. 

다음은 몇 가지 샘플 쿼리 및 방법을 toointerpret 쿼리 실행에서 반환 된 hello 메트릭 일부: 

| 쿼리 | 샘플 메트릭 | 설명 | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | hello 검색 문서 수는 100 + 1 toomatch hello TOP 절. 쿼리 시간은 검색이므로 대부분 `WriteOutputTime` 및 `DocumentLoadTime`에서 소요됩니다. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount 높은 (500 + 1 toomatch hello TOP 절) 되었습니다. | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | 키 조회를 위한 IndexLookupTime은 `/N/?`에 대한 인덱스 조회이므로 약 0.9ms가 소요됩니다. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | 범위 검색을 통한 IndexLookupTime에는 `/N/?`에 대한 인덱스 조회이므로 약간 더 많은 시간(1.7ms)이 소요됩니다. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | `DocumentLoadTime`에는 이전 쿼리와 같은 시간이 소요되지만 하나의 속성만 프로젝션하므로 `WriteOutputTime`은 더 짧습니다. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | 213 ms 약에 소요 `UserDefinedFunctionExecutionTime` UDF의 각 값에 hello 실행 `c.N`합니다. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | `/Name/?`의 `IndexLookupTime`에는 약 0.6ms가 소요됩니다. 대부분의 hello의 실행 시간 (ms ~ 7)을 쿼리할 `SystemFunctionExecutionTime`합니다. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | 쿼리는 `LOWER`를 사용하므로 검색으로 수행되고 검색된 문서 2491개 중 500개가 반환됩니다. |


## <a name="next-steps"></a>다음 단계
* toolearn 지원 hello SQL 쿼리 연산자 및 키워드에 대 한 참조 [SQL 쿼리](documentdb-sql-query.md)합니다. 
* 요청 단위에 대 한 toolearn 참조 [요청 단위](request-units.md)합니다.
* 인덱싱 정책에 대 한 toolearn 참조 [인덱싱 정책](indexing-policies.md) 


