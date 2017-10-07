---
title: "사용 하 여 Azure Cosmos DB.NET 응용 프로그램 aaaBuild hello Graph API | Microsoft Docs"
description: "Tooconnect tooand에서는.NET 코드 샘플은 Azure Cosmos DB 쿼리를 표시."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: hello Graph API를 사용 하 여.NET 응용 프로그램 빌드

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 toocreate Azure Cosmos DB 계정, 데이터베이스 및 그래프 (컨테이너)를 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다. 그런 다음 작성 하 고 hello를 기반으로 하 여 콘솔 응용 프로그램을 실행할 [Graph API](graph-sdk-dotnet.md) (미리 보기).  

## <a name="prerequisites"></a>필수 조건

설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다. 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>그래프 추가

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 github에서 복제는 Graph API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. 그런 다음 Visual Studio 및 열기 hello 솔루션 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello Program.cs 파일을 찾을 수입니다. 

* hello DocumentClient 초기화 됩니다. Hello 미리 보기에서 hello Azure Cosmos DB 클라이언트에서 그래프 확장 API를 추가 했습니다. 제작 하는 독립 실행형 그래프 클라이언트 hello Azure Cosmos DB 클라이언트 및 리소스에서 분리 합니다.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* 새 데이터베이스가 만들어집니다.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* 새 그래프가 만들어집니다.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Hello를 사용 하 여 일련의 Gremlin 단계 실행 `CreateGremlinQuery` 메서드.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Visual Studio 2017 hello App.config 파일을 엽니다. 

2. Hello Azure Cosmos DB 계정에 Azure 포털에서에서 클릭 **키** 왼쪽 탐색 hello에 있습니다. 

    ![표시 및 hello hello 키 페이지에서 Azure 포털에서에서 기본 키를 복사](./media/create-graph-dotnet/keys.png)

3. 복사 프로그램 **URI** hello 포털에서 값을 하 게 hello App.config에 hello 끝점 키의 값입니다. Hello 스크린 샷 toocopy hello 값 앞에 표시 된 대로 hello 복사 단추를 사용할 수 있습니다.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. 복사 프로그램 **기본 키** hello 포털에서 값을 하 게 App.config에 hello AuthKey 키의 값을 hello 다음 변경 내용을 저장 합니다. 

    `<add key="AuthKey" value="FILLME" />`

이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 

## <a name="run-hello-console-app"></a>Hello 콘솔 앱 실행

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **GraphGetStarted** 프로젝트에서 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다. 

2. Hello NuGet에서에서 **찾아보기** 상자에서 입력 *Microsoft.Azure.Graphs* hello를 확인 하 고 **시험판 포함** 상자. 

3. Hello 결과 통해 설치 hello **Microsoft.Azure.Graphs** 라이브러리입니다. Hello Azure Cosmos DB 그래프 확장 라이브러리 패키지 및 모든 종속성을 설치 합니다.

    클릭 하 여 변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 가져오면 **확인**합니다. 라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.

4. CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.

   hello 정점 및 가장자리 toohello 그래프 추가 되 고 hello 콘솔 창에 표시 됩니다. Hello 스크립트가 완료 되 면 ENTER 키를 누릅니다 tooclose hello 콘솔 창에 두 번입니다. 

## <a name="browse-using-hello-data-explorer"></a>Hello 데이터 탐색기를 사용 하 여 찾아보기

이제 다시 hello Azure 포털에서에서 tooData 탐색기 및 찾아보기 돌아가서 새 그래프 데이터를 쿼리 합니다.

1. 데이터 탐색기에서 새 데이터베이스 hello hello 그래프 창에 나타납니다. **graphdb**, **graphcollz**를 확장하고 **그래프**를 클릭합니다.

2. Hello 클릭 **필터 적용** 단추 toouse hello 기본 tooview hello 그래프에 있는 모든 hello verticies를 쿼리 합니다. hello 샘플 응용 프로그램에서 생성 된 hello 데이터 hello 그래프 창에 표시 됩니다.

    Hello 그래프를 축소 수, hello 그래프 표시 공간 확장, 추가 verticies 추가 한 hello에 verticies 화면으로 이동할 수 있습니다.

    ![Hello Azure 포털에서에서 데이터 탐색기에서 hello 그래프 보기](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제: 

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 그래프를 만듭니다 하 고 응용 프로그램을 실행 하는 방법 배웠습니다. 이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다. 

> [!div class="nextstepaction"]
> [Gremlin을 사용하여 쿼리](tutorial-query-graph.md)

