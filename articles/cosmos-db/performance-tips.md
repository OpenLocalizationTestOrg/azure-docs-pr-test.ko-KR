---
title: "aaaPerformance 팁-Azure Cosmos DB NoSQL | Microsoft Docs"
description: "클라이언트 구성 옵션 tooimprove Azure Cosmos DB 데이터베이스 성능에 알아봅니다"
keywords: "tooimprove 데이터베이스 성능"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Azure Cosmos DB에 대한 성능 팁
Azure Cosmos DB는 보장된 대기 시간 및 처리량으로 매끄럽게 크기가 조정되는 빠르고 유연한 분산 데이터베이스입니다. Toomake 주요 아키텍처 변경 하거나 복잡 한 코드 tooscale Cosmos DB와 함께 데이터베이스를 작성 하지 않으면 합니다. 규모를 확장 및 축소하는 것은 단일 API 호출 또는 [SDK 메서드 호출](set-throughput.md#set-throughput-sdk)을 수행하는 것만큼 쉽습니다. 그러나 Cosmos DB를 통해 액세스 하기 때문에 네트워크 호출 있습니다 tooachieve 성능을 최적화할 수 있게 하는 클라이언트 쪽 최적화 됩니다.

"내 데이터베이스 성능을 향상시키는 방법"을 물으면 hello 다음 옵션을 고려 합니다.

## <a name="networking"></a>네트워킹
<a id="direct-connection"></a>

1. **연결 정책: 직접 연결 모드 사용**

    클라이언트가 tooCosmos DB를 연결 하는 방법을 관찰 된 클라이언트 쪽 지연 시간의 측면에서 특히 성능에 중요 한 이점이 있습니다. 두 가지 주요 구성 설정은 클라이언트 연결 정책 – hello 연결을 구성 하는 데 사용할 수 있는 *모드* 및 hello [연결 *프로토콜*](#connection-protocol)합니다.  hello 두 개의 사용 가능한 모드는 같습니다.

   1. 게이트웨이 모드(기본값)
   2. 직접 모드

      게이트웨이 모드 SDK는 모든 플랫폼에서 지원 되며 구성 hello 기본값이 됩니다.  엄격한 방화벽 제한 사항이 있는 응용 프로그램이 회사 네트워크 내에서 실행 되 면 게이트웨이 모드 이므로 hello 적합 하 고 hello 표준 HTTPS 포트 및 단일 끝점을 사용 하 여입니다. 성능 균형 hello, 인데 게이트웨이 모드 과정이 포함 되어 있음을 추가 네트워크 홉 될 때마다 데이터를 읽거나 tooCosmos DB 기록 합니다. 이 때문에 직접 모드 toofewer 네트워크 홉 인해 더 나은 성능을 제공합니다.
<a id="use-tcp"></a>
2. **연결 정책을: hello TCP 프로토콜을 사용 하 여**

    직접 모드를 사용하는 경우 다음과 같이 두 가지 프로토콜 옵션을 사용할 수 있습니다.

   * TCP
   * HTTPS

     Cosmos DB는 HTTPS를 통해 단순한 개방형 RESTful 프로그래밍 모델을 제공합니다. 또한 피어 채널의 통신 모델에는 또한 RESTful 이며 hello.NET 클라이언트 SDK 통해 사용할 수 있는 효율적인 TCP 프로토콜을 제공 합니다. 직접 TCP 및 HTTPS는 모두 초기 인증 및 암호화 트래픽에 SSL을 사용합니다. 최상의 성능을 위해 가능 하면 hello TCP 프로토콜을 사용 합니다.

     게이트웨이 모드 TCP를 사용 하는 경우 TCP 포트 443 hello Cosmos DB 포트 이며 10255 hello MongoDB API 포트입니다. Tooensure hello 포트가 필요 하면 추가 toohello 게이트웨이 포트의 직접 모드에서 TCP를 사용 하는 경우 10000과 20000 사이의 범위는 Cosmos DB 동적 TCP 포트를 사용 하기 때문에 열려 있습니다. 이러한 포트가 열려 있으며 toouse TCP 시도, 503 서비스를 사용할 수 없는 오류가 발생 합니다.

     연결 모드 hello hello hello ConnectionPolicy 매개 변수를 사용 하 여 hello DocumentClient 인스턴스 생성 중 구성 됩니다. 직접 모드를 사용 하는 경우 hello 프로토콜 hello ConnectionPolicy 매개 변수 내에서 설정할 수도 있습니다.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    TCP 게이트웨이 모드를 사용 하는 경우에 직접 모드에서 지원 됩니다, 때문에 다음 hello HTTPS 프로토콜은 항상 게이트웨이 hello로 toocommunicate 및 hello 프로토콜 값에서에서 사용할 hello ConnectionPolicy는 무시 됩니다.

    ![그림의 hello Azure Cosmos DB 연결 정책](./media/performance-tips/connection-policy.png)

3. **첫 번째 요청에서 OpenAsync tooavoid 시작 대기 시간이 호출 합니다.**

    기본적으로 hello 첫 번째 요청에 toofetch hello 주소 라우팅 테이블에 있기 때문에 더 높은 대기 시간이 있습니다. tooavoid hello에이 시작 대기 시간이 먼저 요청, 초기화 하는 동안 한 번 OpenAsync() 다음과 같이 호출 해야 합니다.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **성능을 위해 동일한 Azure 지역에 클라이언트 배치**

    때 가능한 위치 Cosmos DB를 호출 하는 모든 응용 프로그램 hello와 동일한 지역 hello Cosmos DB 데이터베이스입니다. 대략적인 비교 tooCosmos DB hello 1-2 밀리초, 하지만 서쪽 hello 및의 hello 미국 동부 지역 간의 hello 대기 시간 내에 완료 동일한 지역 내에서 호출 하 여 > 50ms 합니다. 이 대기는 hello 클라이언트 toohello Azure 데이터 센터 경계에서 전달 하는 hello 요청을 수행한 hello 경로 따라 요청 toorequest에서 가능성이 달라질 수 있습니다. 가장 낮은 대기 시간을 최소화 hello hello 호출 되도록 하 여 이루어집니다. 응용 프로그램은 hello hello와 같은 Azure 지역 Cosmos DB 끝점을 프로 비전 합니다. 사용 가능한 영역 목록은 [Azure 지역](https://azure.microsoft.com/regions/#services)을 참조하세요.

    ![그림의 hello Azure Cosmos DB 연결 정책](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **스레드/작업의 수 늘리기**

    Hello 네트워크를 통해 호출 tooAzure Cosmos DB 하므로 hello 클라이언트 응용 프로그램 요청 간에 대기 시간이 거의 줄이도록 toovary hello 병렬 처리 수준 요청을 할 수 있습니다. 예를 들어 사용 중인 경우. NET의 [작업 병렬 라이브러리](https://msdn.microsoft.com//library/dd460717.aspx), hello 순서 대로 읽기 또는 tooCosmos DB 쓰기 작업 단위: 100의 작성 합니다.

## <a name="sdk-usage"></a>SDK 사용
1. **설치 hello 최신 SDK**

    Cosmos DB Sdk hello 끊임 향상 된 tooprovide hello 최상의 성능이 없이 합니다. Hello 참조 [Cosmos DB SDK](documentdb-sdk-dotnet.md) 페이지 toodetermine 최신 SDK hello 및 향상 기능을 살펴봅니다.
2. **Singleton Cosmos DB 클라이언트를 사용 하 여 응용 프로그램의 수명 hello에 대 한**

    각 DocumentClient 인스턴스는 스레드로부터 안전하고 직접 모드에서 작동하는 경우 효율적인 연결 관리와 주소 캐싱을 수행합니다. tooallow 효율적인 연결 관리 및 DocumentClient 하 여 더 나은 성능을 hello 응용 프로그램의 hello 수명에 대 한 toouse AppDomain 당 DocumentClient의 단일 인스턴스를 권장 합니다.

   <a id="max-connection"></a>
3. **Gateway 모드를 사용하는 경우 호스트당 System.Net MaxConnections 늘리기**

    Cosmos DB 요청 게이트웨이 모드를 사용 하는 경우 HTTPS/REST를 통해 수행 되므로 및 호스트 이름 또는 IP 주소 당 toohello 발전 하 여 기본 연결 제한 됩니다. Hello 클라이언트 라이브러리를 사용할 수 여러 동시 연결 tooCosmos DB 있도록 tooset hello MaxConnections tooa 더 높은 값 (100-1000) 할 수 있습니다. .NET SDK 1.8.0 hello와 위의 hello에 대 한 기본값 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) 은 50과 toochange hello 값, hello를 설정할 수 있습니다 [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa 더 큰 값입니다.   
4. **분할된 컬렉션에 대한 병렬 쿼리 튜닝**

     DocumentDB.NET SDK 버전 1.9.0 이상과 tooquery 동시에 분할 된 컬렉션을 사용 하는 병렬 쿼리를 지원 (참조 [hello Sdk 작업](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) 및 관련 hello [코드 샘플](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) 에 대 한 추가 정보). 병렬 쿼리 디자인 된 tooimprove 쿼리 대기 시간 및 처리량 직렬 그 반대인 위에 합니다. 두 개의 매개 변수를 제공 하는 병렬 쿼리는 사용자가 튜닝할 수 toocustom 맞춤 요구 사항 (a) MaxDegreeOfParallelism:, parallel 및 (b) MaxBufferedItemCount toocontrol hello 최대 다음 파티션 수를 쿼리할 수 있습니다: toocontrol hello 수 사전 인출 된 결과입니다.

    (a) ***MaxDegreeOfParallelism 튜닝\:*** 여러 파티션을 병렬로 쿼리하여 병렬 쿼리가 작동합니다. 그러나는 개별 분할 된 수집에서 데이터를 존중 toohello 쿼리로 직렬로 가져오지 않습니다. 따라서 파티션 설정 hello MaxDegreeOfParallelism toohello 수 확률이 hello 최대 달성 대부분 고성능 쿼리 hello, 다른 모든 시스템 조건 계속 제공 hello 동일 합니다. 파티션 수가 hello를 모르는 경우 hello MaxDegreeOfParallelism tooa 높은 수를 설정할 수 있습니다 및 hello 시스템 MaxDegreeOfParallelism hello 대로 hello 최소 (파티션, 사용자가 제공한 입력 수)를 선택 합니다.

    것이 중요 한 toonote hello 데이터가 존중 toohello 쿼리와 함께 모든 파티션에 균등 하 게 된 경우 쿼리 생성 hello에 대 한 최상의 혜택을 병렬화 하 합니다. Hello 컬렉션 분할 방식 전체 또는 대부분의 쿼리에서 반환 된 hello 데이터는 몇 가지 파티션 (최악의 경우에서 하나의 파티션)에 집중 다음 hello 쿼리의 hello 성능을 해당 파티션에 의해 병목 현상이 발생은 분할 됩니다.

    (b) ***튜닝 MaxBufferedItemCount\: *** hello 클라이언트에서 결과의 hello 현재 일괄 처리를 처리 하는 동안 병렬 쿼리는 디자인 된 toopre 인출 결과입니다. hello 프리페치 쿼리 전체 대기 시간 개선 사항에는 데 도움이 됩니다. MaxBufferedItemCount 미리 인출한 결과 hello 매개 변수 toolimit hello 수입니다. 반환 된 결과 (또는 더 큰 값)의 수를 프리페치 하는 hello 쿼리 tooreceive 최대 활용 허용 toohello 예상 MaxBufferedItemCount를 설정 합니다.

    미리 반입 works hello hello MaxDegreeOfParallelism의 방식으로 상관 없이 동일 하 고 모든 파티션으로부터의 hello 데이터에 대 한 단일 버퍼가 note 합니다.  
5. **서버 쪽 GC 켜기**

    일부 경우에 가비지 수집의 hello 빈도 줄이는 데 도움이 됩니다. .NET에서는 설정 [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue 합니다.
6. **RetryAfter 간격으로 백오프 구현**

    성능 테스트 중에는 작은 비율의 요청이 제한될 때까지 로드를 늘려야 합니다. 제한 하 여 hello 클라이언트 응용 프로그램 hello 서버에 지정 된 다시 시도 간격에 대 한 스로틀에 백오프를 해야 합니다. 최소한의 다시 시도 작업 사이의 대기 시간을 소비 하는 확인 hello 백오프를 유지 합니다. 다시 시도 정책 지원 버전 1.8.0 이상에 포함 되는지 hello DocumentDB의 [.NET](documentdb-sdk-dotnet.md) 및 [Java](documentdb-sdk-java.md), 1.9.0 버전 이상의 hello [Node.js](documentdb-sdk-node.md) 및 [ Python](documentdb-sdk-python.md), 지원 되는 모든 버전의 hello 및 [.NET Core](documentdb-sdk-dotnet-core.md) Sdk입니다. 자세한 내용은 [예약된 처리량 제한 초과](request-units.md#RequestRateTooLarge) 및 [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx)를 참조하세요.
7. **클라이언트 워크로드 규모 확장**

    처리량이 높은 수준에서 테스트 하는 경우 (> 50,000 000RU/s), hello 클라이언트 응용 프로그램 CPU, 네트워크 사용률에 toohello 컴퓨터 제한 인해 hello 병목 상태가 될 수 있습니다. 이 시점에 도달 하면 여러 서버에서 클라이언트 응용 프로그램을 확장 하 여 toopush hello Cosmos DB 계정 추가 계속할 수 있습니다.
8. **짧은 읽기 대기 시간 동안 문서 URI 캐시**

    캐시 문서 hello 최상의 읽기 성능을 위해 가능 하면 Uri입니다.
   <a id="tune-page-size"></a>
9. **성능 향상을 위해 쿼리/read 피드에 대 한 hello 페이지 크기를 조정**

    대량 수행를 읽을 때 읽기 피드 (예를 들어 ReadDocumentFeedAsync) 기능을 사용 하 여 문서 또는 DocumentDB SQL 쿼리를 실행 하는 경우 hello 결과 집합이 너무 큰 경우 분할 된 형태로 hello 결과가 반환 됩니다. 기본적으로, 100개의 항목 또는 1MB 단위(둘 중 먼저 도달하는 단위)로 결과가 반환됩니다.

    tooreduce hello 수가 네트워크 필요한 왕복 tooretrieve 적용 가능한 모든 결과, x-ms-최대-항목-수 요청 헤더 tooup too1000를 사용 하 여 hello 페이지 크기를 늘릴 수 있습니다. 해야 하는 경우 toodisplay 몇 가지 결과만에서 예를 들어 사용자 인터페이스 또는 응용 프로그램 API만 10을 반환 하는 경우 한 번으로 인해, 읽기 및 쿼리를 위해 사용 된 hello 페이지 크기 too10 tooreduce hello 처리량을 줄일 수 있습니다.

    Hello 페이지 크기를 설정할 수도 있습니다 사용할 수 있는 Cosmos DB Sdk hello를 사용 하 여 합니다.  예:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **스레드/작업의 수 늘리기**

    참조 [스레드/작업의 수를 늘릴](#increase-threads) hello 네트워킹 섹션에에서 있습니다.

11. **64비트 호스트 처리 사용**

    DocumentDB SDK hello DocumentDB.NET SDK 1.11.4 버전을 사용 하는 경우와 위의 32 비트 호스트 프로세스에서 작동 합니다. 하지만 파티션 간 쿼리를 사용하는 경우 성능 향상을 위해 64비트 호스트를 처리하는 것이 좋습니다. hello 다음 종류의 응용 프로그램을 hello 기본값으로 처리 하므로 순서 toochange too64 비트는 응용 프로그램의 hello 형식을 기반으로 이러한 단계를 수행 하는 32 비트 호스트에는

    - 실행 가능한 응용 프로그램에 대 한 이렇게 hello 선택을 취소 하 여 **32 비트 선호** hello에 대 한 옵션 **프로젝트 속성** 창의 hello에 **빌드** 탭 합니다.

    - VSTest 테스트 프로젝트를 기반으로 이렇게 선택 하 여 **테스트**->**테스트 설정**->**기본 프로세서 아키텍처: X64로**, hello에서 **Visual Studio 테스트** 메뉴 옵션입니다.

    - 로컬 배포 된 ASP.NET 웹 응용 프로그램의 경우 이렇게 hello를 확인 하 여 **웹 사이트 및 프로젝트에 대 한 사용 하 여 hello 64 비트 버전의 IIS Express**아래 **도구** ->  **옵션**->**프로젝트 및 솔루션**->**웹 프로젝트**합니다.

    - ASP.NET 웹 응용 프로그램의 Azure에 배포 된 경우 이렇게 hello를 선택 하 여 **64 비트 플랫폼** hello에 **응용 프로그램 설정** hello Azure 포털에 있습니다.

## <a name="indexing-policy"></a>인덱싱 정책
1. **더 빠른 피크 시간 수집 속도에 대한 지연 인덱싱 사용**

    Cosmos DB는 인덱싱 정책 사용할 수 있는 toochoose hello 문서에 자동으로 인덱싱 컬렉션 toobe 하려는 경우 – hello 모음 수준에서 toospecify를 – 있습니다.  또한 동기(일관성)와 비동기(지연) 인덱스 업데이트 중에서 선택할 수 있습니다. 기본적으로 hello 인덱스는 각 삽입, 교체, 또는 문서 toohello 컬렉션의 삭제에 동기적으로 업데이트 됩니다. 동기적으로 모드 활성화 hello 쿼리 toohonor hello 동일 [일관성 수준이](consistency-levels.md) hello과 같은 문서 hello 인덱스에 대 한 지연 너무 "따라잡을" 없이 읽습니다.

    Lazy 인덱싱을 고려 될 수 있습니다, 버스트에서 데이터를 작성 하는 시나리오 및 tooamortize hello 필요한 작업 tooindex 콘텐츠 더 긴 기간 동안 합니다. Lazy 인덱싱을 또한 있습니다 toouse 프로그램 처리량을 효과적으로 프로 비전 및 serve 쓰기 요청을 사용량이 많은 시간에 최소 대기 시간으로 합니다. 그러나 중요 한 toonote, lazy 인덱싱을 사용 하도록 설정한 경우 쿼리 결과 결국 hello Cosmos DB 계정에 구성 된 hello 일관성 수준에 관계 없이 일관성 있는 경우

    따라서 일관 된 인덱싱 모드 (IndexingPolicy.IndexingMode tooConsistent 설정 됨) hello 가장 높은 요청 단위 충전 인덱싱 모드 (IndexingPolicy.IndexingMode tooLazy 설정 됨) 및 없음 인덱싱 Lazy 하는 동안 쓰기를 발생 시킵니다 (IndexingPolicy.Automatic 설정 됨 tooFalse) 쓰기의 hello 시간에 인덱싱 비용이 0이 있어야 합니다.
2. **더 빠른 쓰기에 대한 인덱싱에서 사용하지 않는 경로 제외**

    Cosmos DB의 인덱싱 정책 경로 tooinclude 문서화 되지 않았거나 인덱싱 경로 (IndexingPolicy.IncludedPaths 및 IndexingPolicy.ExcludedPaths)를 활용 하 여 인덱싱에서 제외 toospecify가 있습니다. 쓰기 성능 및 시나리오는 hello에 쿼리 패턴이 미리 확인 된, 인덱싱 비용 직접은 높이고 인덱스 저장 공간 인덱스는 고유 경로의 toohello 수 상관 관계가 지정 된 hello 인덱싱 경로 사용 하 여 제공할 수 있습니다.  예를 들어 코드 다음 hello 방법을 tooexclude hello의 전체 섹션에 설명 (규칙 하위 하위 트리) hello를 사용 하 여 인덱싱에서 "*" 와일드 카드입니다.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    자세한 내용은 [Azure Cosmos DB 인덱싱 정책](indexing-policies.md)을 참조하세요.

## <a name="throughput"></a>처리량
<a id="measure-rus"></a>

1. **낮은 요청 단위/초 사용량 측정 및 튜닝**

    Cosmos DB는 다양 한 Udf, 저장된 프로시저 및 트리거 – 모든 운영 데이터베이스 컬렉션 내에서 hello 문서에서 관계형 및 계층적 쿼리를 포함 한 데이터베이스 작업을 제공 합니다. 이러한 각 작업와 관련 된 hello 비용 hello CPU, IO 및 메모리 필요한 toocomplete hello 작업에 따라 다릅니다. 에 대해 생각 하 고 하드웨어 리소스를 관리 하는 대신 생각할 수 있습니다는 요청 단위 (RU) 리소스 필요한 tooperform hello에 대 한 단일 측정값으로 다양 한 데이터베이스 작업 및 서비스 응용 프로그램 요청 합니다.

    [요청 단위](request-units.md) hello 구매한 용량 단위 수에 따라 각 데이터베이스 계정에 대 한 프로 비전 됩니다. 요청 단위 소비는 초당 비율로 평가됩니다. Hello 프로 비전 된 요청 단위를 초과 하는 응용 프로그램에는 hello 속도 hello 예약된 hello 계정에 대 한 수준 아래로 떨어질 때까지 계정으로 제한 됩니다에 대 한 비율입니다. 응용 프로그램에 더 높은 처리량 수준이 필요한 경우 추가 용량 단위를 구매할 수 있습니다.

    hello 복잡 한 쿼리 요청 단위의 수는 작업에 대 한 사용 되는 영향을 줍니다. 조건자의 hello 개수, hello 조건자, Udf 수 및 모든 영향을 줄의 hello 비용 hello 원본 데이터 집합의 hello 크기의 특성 작업을 쿼리 합니다.

    모든 작업의 toomeasure hello 오버 헤드 (만들기, 업데이트 또는 삭제), hello ms 요청 무료 x 헤더를 검사 (또는 RequestCharge 속성 ResourceResponse에 해당 하는 환영<T> 또는 FeedResponse<T> hello.NET SDK에에서) toomeasure 이러한 작업을 사용한 요청 단위 hello 수입니다.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    hello이 헤더에 반환 된 요청 충전은 프로 비전 된 처리량의 소수 부분 (즉, 2000 RUs / 초)입니다. 예를 들어 hello 앞의 쿼리를 반환할 경우 1000 1KB 문서 hello 연산의 hello 비용은 1000입니다. 따라서 1 초 이내에 hello 서버에서는 이러한 두 개의 요청 후속 요청을 제한 하기 전에 부여 합니다. 자세한 내용은 참조 [요청 단위](request-units.md) 및 hello [요청 단위 계산기](https://www.documentdb.com/capacityplanner)합니다.
<a id="429"></a>
2. **너무 큰 속도 제한/요청 속도 처리**

    계정에 대 한 tooexceed hello 예약 된 처리량을 시도 하면 hello 서버에서 성능 저하 없이 및가 사용 되지 않지만 예약 hello 수준 벗어났다고 처리 용량 hello 서버 hello RequestRateTooLarge (HTTP 상태 코드 429) 요청 하 고 반환 hello x-ms-다시 시도-후-ms을 나타내는 헤더 hello 양의 시간 (밀리초), 사용자 hello hello 요청을 다시 시도 하기 전에 대기 해야이 미리 종료 됩니다.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    hello Sdk 모두 암시적으로이 응답을 catch, hello 서버에 지정 된 retry-after 헤더, 준수 및 hello 요청을 다시 시도 합니다. 계정 여러 클라이언트에서 동시에 액세스 하는, 하지 않는 한 hello 다음 재시도 성공 합니다.

    누적 hello 요청 속도 위에서 일관 되 게 작동 하는 여러 명의 클라이언트를 설정한 경우 hello 기본 다시 시도 횟수 현재 집합 too9 hello 클라이언트에서 내부적으로 요구 사항을 충족 하지 않을 수 있습니다. 이 경우 hello 클라이언트에서 상태 코드 429 toohello 응용 프로그램과 함께 DocumentClientException throw 합니다. hello ConnectionPolicy 인스턴스에서 설정 hello RetryOptions 여 hello 기본 다시 시도 횟수를 변경할 수 있습니다. 기본적으로 상태 코드 429 DocumentClientException hello hello 요청 hello 요청 속도 위에 toooperate 계속 되 면 누적 대기 시간이 30 초 후 반환 됩니다. 가 경우에 현재 재시도 횟수 hello hello 최대 재시도 횟수 보다 작으면이 발생, hello 기본 9 또는 사용자 정의 값의 수입니다.

    Hello 자동화 된 다시 시도 동작을 사용 하면 tooimprove 복원 력 및 유용성 hello에 대 한 대부분의 응용 프로그램, 특히 측정 하는 경우 대기 시간 성능 벤치 마크를 수행할 때 했지만 수행할 수 합니다.  hello 클라이언트 관찰 된 대기 시간 hello 실험 hello 서버 제한에 도달 하면 hello 클라이언트 SDK toosilently 다시 시도 하는 경우 스파이크 됩니다. tooavoid 대기 시간 성능 실험 하는 동안 각 작업에서 반환 된 측정값 hello 충전 갑작스럽게 증가 하 고 요청 hello 예약된 요청 속도 아래 작동 하는지 확인 합니다. 자세한 내용은 [요청 단위](request-units.md)를 참조하세요.
3. **처리량을 높이기 위해 문서 크기를 줄이도록 설계**

    hello 요청 효율적인 (즉, 요청 처리 비용)이 지정된 된 작업은 직접 toohello hello 문서 크기를 상호 연결 합니다. 큰 문서에서 작업하는 경우 작은 문서 작업에 비해 비용이 많이 듭니다.

## <a name="next-steps"></a>다음 단계
샘플 응용 프로그램 사용 tooevaluate Cosmos DB 몇 개의 클라이언트 컴퓨터에서 성능 시나리오를 참조 하십시오. [성능 및 확장 Cosmos DB와 함께 테스트](performance-testing.md)합니다.

또한 toolearn 규모 및 고성능을 위해 응용 프로그램 디자인에 대해 자세히 확인할 [Partitioning 및 Azure Cosmos DB에 크기 조정](partition-data.md)합니다.
