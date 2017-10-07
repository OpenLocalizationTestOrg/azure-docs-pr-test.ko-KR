---
title: "Azure Cosmos DB: hello.NET에서 Graph API를 사용 하 여 개발 | Microsoft Docs"
description: "자세한 방법을 toodevelop.NET을 사용 하 여 Azure Cosmos DB DocumentDB api"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: hello.NET에서 Graph API를 사용 하 여 개발
Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 자습서에서는 하 고 사용 하 여 Azure Cosmos DB 계정을 toocreate hello Azure 포털 방법 설명 toocreate 그래프 데이터베이스 및 컨테이너. hello 만듭니다 간단한 소셜 네트워크 hello를 사용 하 여 4 명의 사람과 [Graph API](graph-sdk-dotnet.md) (미리 보기) 트래버스하 고 Gremlin를 사용 하 여 hello 그래프를 쿼리 합니다.

이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * Azure Cosmos DB 계정 만들기 
> * 그래프 데이터베이스 및 컨테이너 만들기
> * 꼭 짓 점 및 가장자리 too.NET 개체 serialize
> * 꼭짓점 및 가장자리 추가
> * Gremlin를 사용 하 여 쿼리 hello 그래프

## <a name="graphs-in-azure-cosmos-db"></a>Azure Cosmos DB의 그래프
Azure Cosmos DB toocreate, 업데이트 및 hello를 사용 하 여 쿼리 그래프를 사용할 수 있습니다 [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) 라이브러리입니다. 단일 확장 메서드를 제공 하는 hello Microsoft.Azure.Graph 라이브러리 `CreateGremlinQuery<T>` hello 위에 `DocumentClient` tooexecute Gremlin 쿼리 클래스입니다.

Gremlin은 쓰기 작업(DML)과 쿼리 및 순회 작업을 지원하는 함수형 프로그래밍 언어입니다. 이 문서 tooget에 몇 가지 예가 Gremlin와 시작 프로그램 다룹니다. Azure Cosmos DB에서 사용할 수 있는 Gremlin 기능에 대한 자세한 연습은 [Gremlin 쿼리](gremlin-support.md)를 참조하세요. 

## <a name="prerequisites"></a>필수 조건
Hello 다음 항목이 있는지 확인 하십시오.

* 활성 Azure 계정. 계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다. 
    * Hello 또는 사용할 수 있습니다 [Azure DocumentDB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>데이터베이스 계정 만들기

Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.  

> [!TIP]
> * Azure Cosmos DB 계정이 이미 있나요? 이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)
> * Azure DocumentDB 계정이 있나요? 따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.  
> * Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다. 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Visual Studio 솔루션 설치
1. 컴퓨터에서 **Visual Studio**를 엽니다.
2. Hello에 **파일** 메뉴 선택 **새로**를 선택한 후 **프로젝트**합니다.
3. Hello에 **새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **콘솔 응용 프로그램 (.NET Framework)**프로젝트 이름을 지정 하 고 클릭 한 다음, **확인**합니다.
4. Hello에 **솔루션 탐색기**을 Visual Studio 솔루션에서 사용 중인 새 콘솔 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...**
5. Hello에 **NuGet** 탭을 클릭 **찾아보기**, 유형과 **Microsoft.Azure.Graphs** hello 검색 상자 및 확인란 hello **시험판 버전포함**.
6. Hello 결과 내 찾을 **Microsoft.Azure.Graphs** 클릭 **설치**합니다.
   
   클릭 하 여 변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 가져오면 **확인**합니다. 라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.
   
    hello `Microsoft.Azure.Graphs` 단일 확장 메서드를 제공 하는 라이브러리 `CreateGremlinQuery<T>` Gremlin 작업을 실행 하기 위한 합니다. Gremlin은 쓰기 작업(DML)과 쿼리 및 순회 작업을 지원하는 함수형 프로그래밍 언어입니다. 이 문서 tooget에 몇 가지 예가 Gremlin와 시작 프로그램 다룹니다. [Gremlin 쿼리](gremlin-support.md)에는 Azure Cosmos DB의 Gremlin 기능에 대한 자세한 연습이 있습니다.

## <a id="add-references"></a>앱 연결

응용 프로그램에 이 두 상수와 *client* 변수를 추가합니다. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Toohello 돌아가 다음으로, [Azure 포털](https://portal.azure.com) tooretrieve 끝점 URL 및 기본 키입니다. hello 끝점 URL 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다. 

에 Azure 포털 hello, tooyour Azure Cosmos DB 계정 탐색, 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다. 

Hello 포털에서 hello URI를 복사 하 고 붙여넣어 `Endpoint` 위의 hello 끝점 속성에 있습니다. 그런 다음 복사본 hello 포털에서 기본 키를 hello 및 hello에 붙여 `AuthKey` 위의 속성입니다. 

! [Hello Azure 포털의 스크린 샷 hello 자습서 toocreate 하 여 C# 응용 프로그램을 사용 합니다. 키 단추에 강조 표시 된 hello Azure Cosmos DB 탐색 및 hello URI 및 기본 키 값에 강조 표시 된 hello 키 블레이드에서 Azure Cosmos DB 계정 hello 표시] [키] 
 
## <a id="instantiate"></a>Hello DocumentClient 인스턴스화합니다 
다음으로 hello의 새 인스턴스를 만듭니다 **DocumentClient**합니다.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>데이터베이스 만들기 

이제 Azure Cosmos DB 만들 [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) 메서드 또는 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello 방식의  **DocumentClient** hello에서 클래스 [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)합니다.  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>그래프 만들기 

다음으로 hello를 사용 하 여 hello를 사용 하 여 그래프의 컨테이너를 만들 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) 메서드 또는 [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello 방식의 **DocumentClient**  클래스입니다. 컬렉션은 그래프 엔터티의 컨테이너입니다. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>꼭 짓 점 및 가장자리 too.NET 개체 serialize
Azure Cosmos DB hello를 사용 하 여 [GraphSON 통신 형식](gremlin-support.md), 꼭 짓 점, 모서리 및 속성에 대 한 JSON 스키마를 정의 하는 합니다. 이렇게 하면 코드에서 작업할 수 있습니다 있는.NET 개체로 GraphSON tooserialize/역직렬화 및 hello Cosmos DB AZURE.NET SDK를 종속성으로 JSON.NET 포함 됩니다.

예를 들어 4명의 사람으로 구성된 포함된 간단한 소셜 네트워크로 작업해 보겠습니다. 방법을 살펴볼 toocreate `Person` 꼭지점 추가 `Knows` 다음 사이의 관계를 쿼리하고 hello 그래프 toofind "친한 친구의 친구" 관계를 트래버스 합니다. 

hello `Microsoft.Azure.Graphs.Elements` 네임 스페이스를 제공 `Vertex`, `Edge`, `Property` 및 `VertexProperty` GraphSON 응답 toowell 정의.NET 개체를 역직렬화 하는 동안에 대 한 클래스입니다.

## <a name="run-gremlin-using-creategremlinquery"></a>CreateGremlinQuery를 사용하여 Gremlin 실행
Gremlin은 SQL과 마찬가지로 읽기, 쓰기 및 쿼리 작업을 지원합니다. 예를 들어 hello 다음 코드 조각에서는 toocreate 꼭지점, 가장자리를 사용 하 여 몇 가지 샘플 쿼리를 수행 하는 방법 `CreateGremlinQuery<T>`, 비동기적으로 사용 하 여 이러한 결과 반복 하 고 `ExecuteNextAsync` 및 ' HasMoreResults 합니다.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>꼭짓점 및 가장자리 추가

Hello Gremlin 문을 자세히 hello 섹션 앞에 표시 된 것을 살펴보겠습니다. 먼저 Gremlin의 `addV` 메서드를 사용하는 몇 가지 꼭짓점이 있습니다. 예를 들어 hello 다음 조각에서는 "Person" 형식의 "Thomas Andersen" 꼭지점 이름, 성, 이름 및 보존 기간에 대 한 속성을 사용 합니다.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

그런 다음 Gremlin의 `addE` 메서드를 사용하여 이 꼭짓점 사이에 몇 개의 가장자리를 만듭니다. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Gremlin의 `properties` 단계를 사용하여 기존 꼭짓점을 업데이트할 수 있습니다. Hello 호출 tooexecute hello를 통해 쿼리를 건너뛰고 `HasMoreResults` 및 `ExecuteNextAsync` hello 나머지 hello 예제에 대 한 합니다.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Gremlin의 `drop` 단계를 사용하여 가장자리와 꼭짓점을 제거할 수 있습니다. 다음은 조각 보여 주는 방법을 toodelete 꼭 짓 점 및 가장자리입니다. 참고의 hello 모두 삭제를 수행 하는 꼭 짓 점 삭제 가장자리에 연결 합니다.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>쿼리 hello 그래프

Gremlin을 사용하여 쿼리와 순회도 수행할 수 있습니다. 예를 들어 다음 코드 조각 hello toocount hello 그래프에 꼭 짓 점 수가 hello 하는 방법을 보여 줍니다.

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Gremlin의를 사용 하 여 필터를 수행할 수 있습니다 `has` 및 `hasLabel` 둘을 결합 하 여 단계를 사용 하 여 `and`, `or`, 및 `not` toobuild 보다 복잡 한 필터:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Hello를 사용 하 여 hello 쿼리 결과에서 특정 속성을 프로젝션 할 수 `values` 단계:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

지금까지 모든 데이터베이스에서 작동하는 쿼리 연산자만 보았습니다. Toonavigate toorelated 가장자리과 꼭지점 필요한 경우 그래프를 신속 하 고 통과 작업에 대 한 효율적인 있습니다. Thomas의 친구들을 모두 찾아 보겠습니다. Gremlin의를 사용 하 여 수행 `outE` Thomas에서 모든 hello 송신 가장자리 toofind 시작한 다음 Gremlin의를 사용 하 여 해당 가장자리부터 꼭지점에 toohello 통과 `inV` 단계:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

hello 다음 쿼리는 두 가지 홉 toofind 수행 Thomas' "친구의 친구"를 호출 하 여 모든 `outE` 및 `inV` 두 배입니다. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

더 복잡 한 쿼리를 작성 하 고 Gremlin를 비롯 한 혼합 필터를 사용 하 여 반복을 수행 하는 식, hello를 사용 하 여 강력한 그래프 순회 논리 구현 `loop` 단계 및 hello를 사용 하 여 구현 조건부 탐색 `choose` 단계입니다. [Gremlin 지원](gremlin-support.md)에서 수행할 수 있는 작업에 대해 자세히 알아보세요!

이것으로 끝이며, 이 Azure Cosmos DB 자습서를 완료했습니다! 

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이이 앱을 하는 경우 단계 toodelete hello Azure 포털에서에서이 자습서에서 만든 모든 리소스를 수행 하는 hello를 사용 합니다.  

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * Azure Cosmos DB 계정 만들기 
> * 그래프 데이터베이스 및 컨테이너 만들기
> * 직렬화 된 꼭 짓 점 및 가장자리 too.NET 개체
> * 꼭짓점 및 가장자리 추가
> * Gremlin를 사용 하 여 쿼리 된 hello 그래프

이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다. 

> [!div class="nextstepaction"]
> [Gremlin을 사용하여 쿼리](tutorial-query-graph.md)
