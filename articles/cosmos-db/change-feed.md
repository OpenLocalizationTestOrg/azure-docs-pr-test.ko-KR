---
title: "hello 변경 aaaWorking Azure Cosmos DB에서 지원 피드 | Microsoft Docs"
description: "사용 하 여 Azure Cosmos DB 문서에 피드 지원 tootrack 변경 사항을 변경 하 고 트리거와 마찬가지로 이벤트 기반 처리와 캐시 및 분석 시스템을 최신 상태로 유지를 수행 합니다."
keywords: "변경 피드"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Cosmos DB Azure의에서 hello 변경 피드 지원 팀과 작업
[Azure Cosmos DB](../cosmos-db/introduction.md)는 빠르고 유연성 있는, 전역적으로 복제된 데이터베이스 서비스로 읽기 및 쓰기에 대해 한 자릿수 밀리초인 예측 가능한 대기 시간 동안 대량의 트랜잭션 및 운영 데이터를 저장하는 데 사용됩니다. 따라서 IoT, 게임, 소매 및 운영 로깅 응용 프로그램에 적합합니다. 이러한 응용 프로그램에서 일반적인 디자인 패턴 tootrack 변경 내용을 tooAzure Cosmos DB 데이터 및 구체화 된 뷰를 업데이트, 이러한 변경 내용에 따라 특정 이벤트에서 실시간 분석, 보관 데이터 toocold 저장소 및 알림을 전송할 수행 됩니다. hello **변경 피드 지원** Azure Cosmos DB에서 사용 하면 toobuild 효율적이 고 확장 가능한 솔루션 각 이러한 패턴에 대 한 합니다.

지원 피드 변경으로 인해 Azure Cosmos DB 문서 수정 된 hello 순서로 프로그램 Azure Cosmos DB 컬렉션 내에서 정렬 된 목록을 제공 합니다. 이 피드 hello 컬렉션 내에서 toodata 수정에 대 한 사용된 toolisten 수 및와 같은 작업을 수행할 수 있습니다.

* 문서를 삽입 하거나 수정할 때 호출 tooan API 트리거
* 업데이트에 대한 실시간(스트림) 처리 수행
* 캐시, 검색 엔진 또는 데이터 웨어하우스와 데이터 동기화

Azure Cosmos DB의 변경 내용이 유지되면 비동기적으로 처리되고 병렬 처리를 위해 한 명 이상의 소비자에게 분산될 수 있습니다. 변경 피드를 사용 하는 방법으로 toobuild 확장 가능한 실시간 응용 프로그램에 대 한 Api hello를 살펴 보겠습니다. 이 문서 toowork Azure Cosmos DB와 함께 피드 및 hello DocumentDB API을 변경 하는 방법을 보여 줍니다. 

![Azure Cosmos DB 변경을 사용 하 여 피드 toopower 실시간 분석 및 이벤트 기반 컴퓨팅 시나리오](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> 지원 피드 변경에만 제공 됩니다 hello DocumentDB API 시킵니다. Graph API hello 및 테이블 API 현재 지원 되지 않습니다.

## <a name="use-cases-and-scenarios"></a>사용 사례 및 시나리오
변경 피드는 많은 양의 쓰기와 큰 데이터 집합의 효율적인 처리를 허용 하 고 변경 된 내용을 대체 tooquerying 전체 데이터 집합 tooidentify를 제공 합니다. 예를 들어 hello 작업을 효율적으로 다음을 수행할 수 있습니다.

* Azure Cosmos DB에 저장된 데이터를 사용하여 캐시, 검색 인덱스 또는 데이터 웨어하우스를 업데이트합니다.
* 응용 프로그램 수준 데이터 계층화 및 보관 구현, 즉, Azure Cosmos DB에서 "핫 데이터를" 저장 하 고 너무 "콜드 데이터 를" age[Azure Blob 저장소](../storage/common/storage-introduction.md) 또는 [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md)합니다.
* [Apache Hadoop](run-hadoop-with-hdinsight.md)를 사용하여 데이터에 대한 Batch 분석을 구현합니다.
* Azure Cosmos DB를 사용하여 [Azure의 람다 파이프라인](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)을 구현합니다. Azure Cosmos DB는 수집 및 쿼리를 모두 처리할 수 있는 확장성이 뛰어난 데이터베이스 솔루션을 제공하고 TCO가 낮은 람다 아키텍처를 구현합니다. 
* 0 가동 중지 시간이 마이그레이션 tooanother Azure Cosmos DB 계정과 다른 파티션 구성표를 수행 합니다.

**수집 및 쿼리에 Azure Cosmos DB를 사용하는 람다 파이프라인:**

![수집 및 쿼리에 대한 Azure Cosmos DB 기반 람다 파이프라인](./media/change-feed/lambda.png)

Azure Cosmos DB tooreceive를 사용 하 여 하 고 장치, 센서, 인프라 및 응용 프로그램에서 이벤트 데이터를 저장 하 고 이러한 이벤트를 처리 수와 실시간 [Azure 스트림 분석](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), 또는 [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md)합니다. 

내에서 프로그램 [서버가 없는](http://azure.com/serverless) 웹 및 모바일 앱 푸시 알림 tootheir 장치 를사용하여보내는같은특정작업변경내용tooyour고객프로필,기본설정또는위치tootrigger같은추적이벤트수있습니다[Azure 함수](../azure-functions/functions-bindings-documentdb.md) 또는 [응용 프로그램 서비스](https://azure.microsoft.com/services/app-service/)합니다. Azure Cosmos DB toobuild 게임을 사용 하는 경우 예를 들어 변경 피드 tooimplement 실시간 순위표 완료 게임에서 점수에 따라 사용할 수 있습니다.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Azure Cosmos DB에서 변경 피드의 작동 방식
Azure Cosmos DB hello 기능 tooincrementally 읽기 업데이트를 수행 해도 tooan Azure Cosmos DB 컬렉션을 제공 합니다. 이 변경 피드 hello 다음과 같은 속성에 있습니다.

* 변경 내용이 Azure Cosmos DB에서 지속되면 비동기적으로 처리될 수 있습니다.
* 컬렉션 내에서 변경 내용을 toodocuments hello 변경 피드 즉시 제공 됩니다.
* 각 변경 tooa 문서 hello 변경 피드에 정확히 한 번만 표시 하 고 클라이언트 검사점 논리를 관리 합니다. hello 변경 피드 프로세서 라이브러리 자동 검사점을 설정 하 고 "최소 한 번" 의미 체계를 제공 합니다.
* 지정된 된 문서에 대 한 유일한 hello 가장 최근의 변경 hello 변경 로그에 포함 됩니다. 중간 변경 내용을 사용할 수 없습니다.
* hello 변경 피드 내 각 파티션 키 값 수정 순서를 기준으로 정렬 됩니다. 파티션 키 값에 보장된 순서가 없습니다.
* 특정 시점에서 변경 내용을 동기화할 수 있습니다. 즉, 변경 내용을 사용할 수 있는 고정 데이터 보존 기간이 없습니다.
* 변경 내용은 파티션 키 범위에서 사용할 수 있습니다. 이 기능을 동시에 여러 소비자/서버에서 처리 하는 광범위 한 모음 toobe의 변경 내용을 사용 합니다.
* 여러 개의 변경 피드를 동시에 hello에 동일한 응용 프로그램 요청 수 수집 합니다.

Azure Cosmos DB의 변경 피드는 모든 계정에 기본적으로 사용됩니다. 사용할 수 있습니다 프로그램 [프로 비전 된 처리량](request-units.md) 쓰기 지역 또는에 [영역을 읽을](distribute-data-globally.md) hello에서 tooread Azure Cosmos DB에서 다른 작업에서와 마찬가지로 피드를 변경 합니다. hello 변경 피드에 삽입 및 toodocuments hello 컬렉션 내에서 실행 한 업데이트 작업이 포함 됩니다. 삭제 대신 문서 내에서 "soft-delete" 플래그를 설정하여 삭제를 캡처할 수 있습니다. 또는 hello 통해 문서에 대 한 유한 만료 기간을 설정할 수 [TTL 기능](time-to-live.md)예: 24 시간 및 사용 하 여 hello 값에 대 한 해당 속성의 toocapture 삭제 합니다. 이 솔루션을 hello TTL 만료 기간 보다 짧은 시간 간격 내 tooprocess 변경 내용이 있습니다. hello 변경 피드 hello 문서 컬렉션 내에서 각 파티션 키 범위에 사용할 수 있으며 따라서 병렬 처리에 대 한 하나 이상의 소비자에서 배포할 수 있습니다. 

![Azure Cosmos DB 변경 피드의 분산 처리](./media/change-feed/changefeedvisual.png)

클라이언트 코드에서 변경 피드를 구현하는 방법에는 몇 가지 옵션이 있습니다. 다음 tooimplement이 hello Azure Cosmos DB REST API를 사용 하 여 변경 공급 hello 하 고 DocumentDB Sdk hello 하는 방법을 설명 하는 즉시 hello 섹션입니다. 그러나.NET 응용 프로그램에 사용할 수 있는 권장 hello 새 [변경 피드 프로세서 라이브러리](#change-feed-processor) hello에서 이벤트를 처리 파티션 간에 읽기 변경 사항을 간소화 하 고에서 작업 하는 여러 스레드가 피드 변경 병렬 처리 합니다. 

## <a id="rest-apis"></a>REST API 및 DocumentDB Sdk hello 사용
Azure Cosmos DB에서는 **컬렉션**이라는 저장소 및 처리량의 탄력적인 컨테이너를 제공합니다. 확장성 및 성능을 위해 [파티션 키](partition-data.md)를 사용하여 컬렉션 내의 데이터를 논리적으로 그룹화합니다. Azure Cosmos DB에서는 ID(읽기/가져오기), 쿼리 및 읽기-피드(검색) 기준 조회를 포함하여 이 데이터에 액세스하기 위한 다양한 API를 제공합니다. hello 변경 피드 얻을 수 있습니다 두 개의 새 요청 헤더 toohello DocumentDB를 채워 `ReadDocumentFeed` API를 파티션 키 범위에서 동시에 처리할 수 있습니다.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
ReadDocumentFeed의 작동 방식에 대해 간략하게 살펴보겠습니다. Azure Cosmos DB 지원 문서 hello 통해 컬렉션 내에서 피드를 읽는 `ReadDocumentFeed` API입니다. 예를 들어 hello 다음 요청 페이지를 반환 hello 구조로 문서 `serverlogs` 컬렉션입니다. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Hello를 사용 하 여 결과 제한 될 수 있습니다 `x-ms-max-item-count` 머리글과 읽기와 hello 요청을 다시 제출 하 여 다시 시작할 수는 `x-ms-continuation` hello 이전 응답에서 헤더를 반환 합니다. 단일 클라이언트에서 수행되는 경우, `ReadDocumentFeed`는 전체 파티션의 결과를 순차적으로 반복합니다. 

**문서 피드의 순차적 읽기**

지원 되는 hello 중 하나를 사용 하 여 문서의 hello 피드를 검색할 수도 있습니다 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)합니다. 예를 들어 hello를 조각과 방법을 따르는 toouse hello [ReadDocumentFeedAsync 메서드](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .net에서 합니다.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>ReadDocumentFeed의 분산 실행
테라바이트 이상의 데이터를 포함하거나 대량의 업데이트를 수집하는 컬렉션의 경우, 단일 클라이언트 컴퓨터에서 읽기 피드를 순차적으로 실행하면 실용적이지 않습니다. 순서 toosupport 이러한 빅 데이터 시나리오, Azure Cosmos DB 제공 Api toodistribute `ReadDocumentFeed` 여러 클라이언트 판독기/소비자를 넘어선 투명 하 게 호출 합니다. 

**분산 읽기 문서 피드**

증분 변경, Azure Cosmos DB tooprovide 확장성이 높은 처리 hello 변경 피드 파티션 키의 범위에 따라 API는 확장 모델을 지원 합니다.

* `ReadPartitionKeyRanges` 호출을 수행하는 컬렉션에 대한 파티션 키 범위의 목록을 가져올 수 있습니다. 
* 각 파티션 키 범위에 대해 수행할 수 있습니다는 `ReadDocumentFeed` 범위 내에서 파티션 키를 사용 하 여 tooread 문서.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>컬렉션에 대한 파티션 키 범위 검색
요청 hello 여 hello 파티션 키 범위를 검색할 수 있습니다 `pkranges` 컬렉션 내의 리소스입니다. 예를 들어 hello 다음 요청 hello의 목록을 검색 hello에 대 한 파티션 키 범위 `serverlogs` 컬렉션:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

이 요청 hello 다음 hello 파티션 키 범위에 대 한 메타 데이터를 포함 하는 응답을 반환 합니다.

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**키 범위 속성을 파티션**: 다음 표에 hello에 hello 메타 데이터 속성을 포함 하는 각 파티션 키 범위:

<table>
    <tr>
        <th>헤더 이름</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>hello 파티션 키 범위에 대 한 hello ID입니다. 각 컬렉션 내에서 안정적이고 고유한 ID입니다.</p>
            <p>파티션 키 범위 하 여 hello tooread 변경 내용을 호출 다음에 사용 되어야 합니다.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>hello 파티션 키 범위에 대 한 hello 최대 파티션 키 해시 값입니다. 내부에 사용합니다.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>hello 파티션 키 범위에 대 한 hello 최소 파티션 키 해시 값입니다. 내부에 사용합니다.</td>
    </tr>       
</table>

지원 되는 hello 중 하나를 사용 하 여 수행할 수 있습니다 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)합니다. 예를 들어 hello 다음 코드 조각에서는.net에서 tooretrieve 파티션 키 범위 하는 방법을 hello를 사용 하 여 [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) 메서드.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

선택적 설정 hello 하 여 파티션 키 범위 당 문서를 검색할 수 있도록 azure Cosmos DB `x-ms-documentdb-partitionkeyrangeid` 헤더입니다. 

### <a name="performing-an-incremental-readdocumentfeed"></a>증분 ReadDocumentFeed 수행
ReadDocumentFeed는 시나리오/의 Azure Cosmos DB 컬렉션의 변경 내용 증분 처리에 대 한 작업을 수행 하는 hello를 지원 합니다.

* 모든 읽기 컬렉션 만들기에서 hello부터 toodocuments 즉, 변경합니다.
* 모든 읽기 사용자가 지정한 시간 이후에 현재 시간 또는 변경 내용을 toofuture 업데이트 toodocuments를 변경 합니다.
* 모든 읽기 hello 컬렉션 (ETag)의 논리적 버전에서 toodocuments를 변경합니다. 소비자 기반 증분 피드 읽기 요청에서 ETag를 반환 하는 hello로 검사점을 수 있습니다.

hello 변경 내용에는 삽입 및 업데이트 toodocuments를 포함 합니다. toocapture 삭제 되 면 문서, 내에서 "소프트 삭제" 속성을 사용 하거나 hello를 사용 하 여 [기본 제공 TTL 속성](time-to-live.md) toosignal hello에 보류 중인 삭제 피드를 변경 합니다.

다음 테이블 목록 hello hello [요청](/rest/api/documentdb/common-documentdb-rest-request-headers.md) 및 [응답 헤더](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed 작업에 대 한 합니다.

**증분 ReadDocumentFeed에 대한 요청 헤더**:

<table>
    <tr>
        <th>헤더 이름</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>설정 해야 너무 "증분 피드" 그렇지 않으면 생략 하거나</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>머리글이 없음: (컬렉션 생성)를 시작 하는 hello에서 모든 변경 내용을 반환</p>
            <p>"*": hello 컬렉션 내에서 모든 새 변경 내용을 toodata 반환</p>         
            <p>&lt;etag&gt;: 경우 ETag tooa 컬렉션 설정, 해당 논리 타임 스탬프 이후 모든 변경 내용을 반환</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 시간 형식: If-None-Match가 지정된 경우 무시합니다.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>데이터를 읽기 위한 hello 파티션 키 범위 ID입니다.</td>
    </tr>
</table>

**증분 ReadDocumentFeed에 대한 응답 헤더**:

<table> <tr>
        <th>헤더 이름</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>hello 논리적 시퀀스 번호 (LSN) hello 응답에서 반환 된 마지막 문서입니다.</p>
            <p>증분 ReadDocumentFeed는 If-None-Match에서 이 값을 다시 제출하여 다시 시작할 수 있습니다.</p>
        </td>
    </tr>
</table>

다음 샘플 요청 tooreturn은 hello 논리 버전/ETag에서 컬렉션의 모든 증분 변경 내용을 `28535` 키 범위를 분할 하 고 = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

변경 내용은 hello 파티션 키 범위 내에서 각 파티션 키 값에서 시간으로 정렬 됩니다. 파티션 키 값에 보장된 순서가 없습니다. 단일 페이지에 포함할 수 있는 것 보다 많은 결과가 있으면 hello로 hello 요청을 다시 제출 하 여 hello 결과의 다음 페이지를 읽을 수 있습니다 `If-None-Match` 값 같은 toohello 헤더 `etag` hello 이전 응답에서 합니다. 여러 문서 삽입 되거나 저장된 프로시저 또는 트리거 내에서 트랜잭션 방식으로 업데이트 된 경우 모두 반환 됩니다 hello 내에서 동일한 응답 페이지.

> [!NOTE]
> 변경 피드를 사용 더 많은 항목에 지정 된 버전과 페이지에 반환 될 수 있습니다 `x-ms-max-item-count` 삽입 되거나 업데이트 저장된 프로시저 내의 여러 문서의 경우 hello 또는 트리거. 

Hello.NET SDK (1.17.0)를 사용할 때는 hello 필드 설정 `StartTime` 에 `ChangeFeedOptions` 이후 변경 toodirectly 반환 문서 `StartTime` 를 호출할 때 `CreateDocumentChangeFeedQuery`합니다. 지정 하 여 `If-Modified-Since` hello REST API를 사용 하 여 요청은 문서를 반환 하지 hello 자체 하지만 대신 hello 연속 토큰 또는 `etag` hello 응답 헤더에 있습니다. 시간, hello continuation 토큰을 지정 하는 수정 된 hello tooreturn hello 문서 `etag` hello 다음 요청에 사용 해야 합니다 `If-None-Match` tooreturn hello 실제 문서. 

.NET SDK hello 제공 hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) 및 [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) 도우미 클래스가 tooaccess 변경한 tooa 컬렉션입니다. hello 다음 코드 조각은 변경 내역을 보여 tooretrieve 모든 단일 클라이언트에서.NET SDK hello를 사용 하 여 hello부터에서 합니다.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
Hello 다음 코드 조각은 변경 내역을 보여 tooprocess 실시간 및 hello 변경 사용 하 여 Azure Cosmos DB와 함께 지원 피드 및 hello 함수 앞에 있습니다. hello 첫 번째 호출이 hello 컬렉션의 모든 hello 문서를 반환 하 고 hello 둘째만 hello hello 마지막 검사점 이후 생성 된 만든 두 문서

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

클라이언트 쪽 논리 tooselectively 프로세스 이벤트를 사용 하 여 hello 변경 공급을 필터링 할 수도 있습니다. 예를 들어 다음은 장치 센서의 온도 변경 이벤트에만 클라이언트 쪽 LINQ tooprocess를 사용 하는 조각입니다.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>변경 피드 프로세서 라이브러리
두 번째 방법은 toouse hello [Azure Cosmos DB 변경 피드 프로세서 라이브러리](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)를 쉽게 이벤트 여러 소비자에서 피드는 변경 내용으로 인해 처리를 배포 하면 도움이 될 수 있는 합니다. hello 라이브러리는 변경 판독기 hello.NET 플랫폼에서 피드를 구축 하기 위한 훌륭한입니다. Hello에 포함 된 hello 메서드를 통해 hello 프로세서 피드 교환 라이브러리를 사용 하 여 단순화 하는 일부 워크플로 다른 Cosmos DB Sdk를 포함 합니다. 

* 데이터가 여러 파티션에 저장되어 있는 경우, 변경 피드에서 업데이트 풀링
* 이동 하거나 컬렉션을 하나 tooanother에서 데이터 복제
* 업데이트 toodata가 트리거하는 작업 및 변경 피드의 병렬 실행 

Hello Cosmos Sdk의에서 Api hello를 사용 하 여 정확한 액세스 toochange 파티션마다에서 업데이트 피드 제공 하며, hello 프로세서 피드 교환 라이브러리를 사용 하 여 변경 내용을 읽는 파티션과 병렬로 작동 하는 여러 스레드 간에 간단해 집니다. 수동으로 각 컨테이너에서 변경 내용을 읽는 각 파티션에 대 한 연속 토큰을 저장 하는 대신 hello 프로세서 피드 교환 임대 메커니즘을 사용 하 여 파티션 간에 읽기 변경 내용을 자동으로 관리 합니다.

hello 라이브러리는 NuGet 패키지로 사용할 수 있는: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) Github로 소스 코드와 [샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)합니다. 

### <a name="understanding-change-feed-processor-library"></a>변경 피드 프로세서 라이브러리의 이해 

네 가지 주요 요소가 hello 프로세서 피드 교환 구현의: hello 컬렉션, hello 임대 컬렉션, hello 프로세서 호스트 및 hello 소비자를 모니터링 합니다. 

**모니터링 대상된 컬렉션:** 모니터링 hello 컬렉션이 hello 데이터는 hello에서 변경 피드가 생성 합니다. 모든 삽입 및 변경 내용을 모니터링 toohello 컬렉션 hello 컬렉션의 변경 피드 hello에에서 반영 됩니다. 

**임대 수집:** hello 임대 컬렉션 좌표 여러 작업자 간에 피드 hello 변경 처리 합니다. 별도 컬렉션은 사용 되는 toostore hello 임대 파티션당 1 개씩 사용 합니다. 유리 toostore hello로 다른 계정에이 임대 수집 쓰기 지역 자세히 toowhere hello 변경 피드 프로세서가 실행 중인 경우 임대 개체 특성을 다음 hello를 포함 되어 있습니다. 
* 소유자: hello 임대를 소유 하는 hello 호스트를 지정 합니다.
* 특정 파티션에 대 한 피드 hello 변경에 hello 위치 (연속 토큰)를 지정 하는 연속 작업:
* 타임 스탬프: 임대 업데이트 된 시간입니다. hello 타임 스탬프 hello 임대가 만료 된 것으로 간주 됩니다 여부를 사용 하는 toocheck 될 수 있습니다 

**프로세서 호스트:** 각 호스트 호스트의 다른 인스턴스를 개수에 활성 임대가 기준으로 파티션을 tooprocess 개수를 결정 합니다. 
1.  호스트 시작 되 면 모든 호스트에 걸쳐 임대 toobalance hello 작업 부하를 획득 합니다. 호스트는 임대가 활성 상태로 유지되도록 주기적으로 임대를 갱신합니다. 
2.  호스트 검사점 hello 마지막 연속 토큰 tooits 임대 각 읽기에 대 한 합니다. tooensure 동시성 안전 호스트 각 임대 업데이트에 대 한 hello ETag를 확인합니다. 다른 검사점 전략도 지원됩니다.  
3.  종료, 모든 임대를 해제 하는 호스트 않고 유지 hello 연속 정보 나중 hello 저장 된 검사점에서 읽기를 다시 시작할 수 있도록 합니다. 

이 이번에 hello 호스트 수가 파티션 (임대) hello 수보다 클 수 없습니다.

**소비자가:** 소비자나 작업자는 각 호스트에 의해 시작 된 처리 피드 hello 변경을 수행 하는 스레드입니다. 각 프로세서 호스트에는 여러 소비자가 있을 수 있습니다. 각 소비자가 읽는 hello 변경 피드 hello에서 tooand 할당 된 파티션 변경의 해당 호스트에 알립니다 및 만료 된 임대 합니다.

toofurther 변경 피드 프로세서의 이러한 4 개의 요소를 함께 작동을 hello 다이어그램을 다음의 예제를 살펴보겠습니다. hello는 컬렉션 저장소 문서를 모니터링 하 고 hello 파티션 키로 hello "city"를 사용 합니다. 파란색 hello 파티션 포함 "E" hello "city" 필드를 사용 하 여 문서에 표시 됩니다. 각각 4 hello 파티션을 병렬로 읽는 두 소비자와 함께 두 호스트 가지가 있습니다. hello 화살표 hello의 특정 지점에서 읽는 hello 소비자 변경 피드를 표시 합니다. Hello 첫 번째 파티션에 hello 어두운 파란색 hello 연한 파랑은 hello 변경 피드에 변경 내용을 이미 파악 하는 hello 읽지 않은 변경 내용을 나타냅니다. hello 호스트 hello 임대 컬렉션 toostore "연속" 값 tookeep 트랙의 각 소비자에 대 한 위치를 읽는 현재 hello 사용 합니다. 

![프로세서 호스트 피드 hello Azure Cosmos DB 변경 사용](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>변경 피드 프로세서 라이브러리 사용 
다음 단원을 hello toouse 소스 컬렉션 tooa 대상 컬렉션에서 변경 내용 복제의 hello 컨텍스트에서 변경 내용 피드 처리기 라이브러리 hello 하는 방법을 설명 합니다. 여기서 hello 소스 컬렉션은 변경 피드 프로세서에서 모니터링 하는 hello 컬렉션입니다. 

**설치 하 고 hello 변경 피드 프로세서 NuGet 패키지를 포함 합니다.** 

변경 피드 프로세서 NuGet 패키지를 설치하기 전에 먼저 다음을 설치합니다. 
* Microsoft.Azure.DocumentDB, 버전 1.13.1 이상 
* Newtonsoft.Json, 9.0.1 버전 이상 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 설치 및 참조로 포함합니다.

**모니터링되는 컬렉션, 임대 및 대상 컬렉션 만들기** 

순서 toouse hello 프로세서 라이브러리 피드 변경, hello 임대 컬렉션 hello 프로세서 호스트를 실행 하기 전에 만든 toobe 제공 되어야 합니다. 다시 임대 컬렉션 변경 피드 프로세서에서 실행 되 고 쓰기 지역 자세히 toowhere hello로 다른 계정에 저장 하는 것이 좋습니다. 이 예에서 데이터 이동 toocreate hello 대상 컬렉션 hello 프로세서 피드 교환 호스트를 실행 하기 전에 필요 합니다. Hello 샘플 코드에서 지속적으로 모니터링 하는 도우미 메서드 toocreate hello 이라고 임대 및 존재 하지 않을 경우 대상 컬렉션입니다. 

> [!WARNING]
> 컬렉션을 만드는 영향을 줍니다 가격의 Azure Cosmos DB와 함께 응용 프로그램 toocommunicate hello에 대 한 처리량을 예약 하는. 자세한 내용은 hello를 방문 하세요 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*프로세서 호스트 만들기*

hello `ChangeFeedProcessorHost` 클래스는 검사점 설정 및 파티션 임대 관리 기능도 제공 하는 이벤트 프로세서 구현을 스레드로부터 안전한, 다중 프로세스, 안전한 런타임 환경을 제공 합니다. toouse hello `ChangeFeedProcessorHost` 클래스를 구현할 수 있습니다 `IChangeFeedObserver`합니다. 이 인터페이스는 세 가지 메서드가 포함합니다.

* `OpenAsync`: 이 함수는 변경 피드 관찰자를 열 때 호출됩니다. 소비자/관찰자를 열 때 수정 된 tooperform 특정 작업을 수 있습니다.  
* `CloseAsync`: 이 함수는 변경 피드 관찰자를 종료할 때 호출됩니다. 소비자/관찰자를 닫으면 수정 된 tooperform 특정 작업을 수 있습니다.  
* `ProcessChangesAsync`: 이 함수는 변경 피드에서 문서의 새로운 변경 내용을 사용할 수 있을 때 호출됩니다. 수정 된 tooperform 모든 피드 변경 업데이트할 때 특정 작업을 수 있습니다.  

Hello 인터페이스 구현 예제에서는 `IChangeFeedObserver` hello를 통해 `DocumentFeedObserver` 클래스입니다. 여기에서 hello `ProcessChangesAsync` upserts (업데이트) 변경 내용으로 인해 문서 피드 hello 대상 컬렉션으로 작동 합니다. 이 예제는 데이터 집합의 순서 toochange hello 파티션 키의 컬렉션을 하나 tooanother에서 데이터를 이동 하는 데 유용 합니다. 

*실행 중인 hello 프로세서 호스트*

이벤트 처리를 시작하기 전에, 변경 피드 옵션 및 변경 피드 호스트 옵션을 모두 사용자 지정할 수 있습니다. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
다음 표에서 hello에 지정할 수 있는 hello 특정 필드 요약 되어 있습니다. 

**변경 피드 옵션**:
<table>
    <tr>
        <th>속성 이름</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Hello 항목 toobe hello Azure Cosmos DB 데이터베이스 서비스의에서 hello 열거 작업에서 반환 된 최대 수를 가져오거나 설정 합니다.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Hello Azure Cosmos DB 데이터베이스 서비스에서 hello 현재 요청에 대 한 hello 파티션 키 범위 id를 가져오거나 설정 합니다.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Hello Azure Cosmos DB 데이터베이스 서비스에서 hello 요청 continuation 토큰을 가져오거나 설정 합니다.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>세션 일관성 hello Azure Cosmos DB 데이터베이스 서비스에에서 사용 하기 위해 hello 세션 토큰을 가져오거나 설정 합니다.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Hello Azure Cosmos DB 데이터베이스 서비스에서 피드 변경 (true) 시작 하 고 hello 또는 현재 (false)에서 시작할지 여부를 나타내는 값을 가져오거나 설정 합니다. 기본적으로 현재(false)부터 시작합니다.</td>
    </tr>
</table>

**변경 피드 호스트 옵션**:
<table>
    <tr>
        <th>속성 이름</th>
        <th>형식</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>hello ChangeFeedEventHost 인스턴스에서 현재 보유 하는 파티션에 대 한 모든 임대에 대 한 hello 간격입니다.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>파티션에 균등 하 게 알려진된 호스트 인스턴스에서 여부를 태스크 toocompute 오프 간격 tookick을 hello 합니다.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>hello 간격은 hello에 대 한 파티션을 나타내는 임대를 임대를 가져옵니다. 이 간격을 hello 임대 갱신 하지 않으면 만료 되어 및 hello 파티션의 소유권 tooanother ChangeFeedEventHost 인스턴스를 이동 합니다.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>모든 현재 변경 내용을 종료 후 hello hello에 새 변경 내용에 대 한 파티션을 폴링 간격 피드입니다.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>hello 주파수 toocheckpoint 임대 합니다.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>hello hello 호스트에 대 한 최소 파티션 수입니다.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>hello 파티션 hello 호스트의 최대 수를 사용할 수 있습니다.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Bool</td>
        <td>여부에서 hello 시작 hello 호스트의 모든 기존 임대 삭제 하 고 hello 호스트는 처음부터 다시 시작 해야 합니다.</td>
    </tr>
</table>


toostart 이벤트 처리를 인스턴스화할 `ChangeFeedProcessorHost`, Azure Cosmos DB 컬렉션에 대 한 hello 적절 한 매개 변수를 제공 합니다. 그런 다음 호출 `RegisterObserverAsync` tooregister 프로그램 `IChangeFeedObserver` hello 런타임 (이 예제의 DocumentFeedObserver) 구현 합니다. 이 시점에서 hello 호스트 tooacquire 모든 파티션 키 범위 "과 대" 알고리즘을 사용 하 여 hello Azure Cosmos DB 컬렉션에 대 한 임 대권을 시도 합니다. 이러한 임대는 지정된 시간 프레임 동안 지속되며 갱신되어야 합니다. 새 노드로 작업자 인스턴스는이 경우 온라인 상태로, 임대를 예약을 배치 하 고 시간이 지남에 따라 hello 부하 이동 노드 간 각 호스트 시도 tooacquire 임대가 더 합니다. 

Hello 샘플 코드를 사용 하 여 팩터리 클래스 (DocumentFeedObserverFactory.cs) toocreate 관찰자 및 hello `RegistObserverFactoryAsync` tooregister hello observer입니다. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
시간이 지남에 따라 평형이 설정됩니다. 이 동적 기능을 사용 하면 수직 확장 및 축소 모두에 대 한 자동 크기 조정 적용 toobe tooconsumers CPU 기반 합니다. 변경 내용을 처리할 수 있는 것 보다 빠른 속도로 Azure Cosmos DB에서 사용할 수 있는 경우 소비자에 대 한 hello CPU 증가 작업자 인스턴스 수에 사용 되는 toocause 자동으로 조정할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* Hello 시도 [Azure Cosmos DB 변경 GitHub에서 코드 샘플 피드](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Hello로 코딩을 시작 해 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md) 또는 hello [REST API](/rest/api/documentdb/)합니다.
