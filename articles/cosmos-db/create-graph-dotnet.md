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
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a><span data-ttu-id="35d09-103">Azure Cosmos DB: hello Graph API를 사용 하 여.NET 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="35d09-103">Azure Cosmos DB: Build a .NET application using hello Graph API</span></span>

<span data-ttu-id="35d09-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="35d09-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="35d09-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 데이터베이스 및 그래프 (컨테이너)를 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal.</span></span> <span data-ttu-id="35d09-107">그런 다음 작성 하 고 hello를 기반으로 하 여 콘솔 응용 프로그램을 실행할 [Graph API](graph-sdk-dotnet.md) (미리 보기).</span><span class="sxs-lookup"><span data-stu-id="35d09-107">You then build and run a console app built on hello [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="35d09-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="35d09-108">Prerequisites</span></span>

<span data-ttu-id="35d09-109">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="35d09-110">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="35d09-111">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="35d09-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="35d09-112">그래프 추가</span><span class="sxs-lookup"><span data-stu-id="35d09-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="35d09-113">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="35d09-113">Clone hello sample application</span></span>

<span data-ttu-id="35d09-114">이제 github에서 복제는 Graph API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-114">Now let's clone a Graph API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="35d09-115">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-115">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="35d09-116">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-116">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="35d09-117">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-117">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="35d09-118">그런 다음 Visual Studio 및 열기 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-118">Then open Visual Studio and open hello solution file.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="35d09-119">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="35d09-119">Review hello code</span></span>

<span data-ttu-id="35d09-120">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="35d09-121">다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello Program.cs 파일을 찾을 수입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-121">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="35d09-122">hello DocumentClient 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-122">hello DocumentClient is initialized.</span></span> <span data-ttu-id="35d09-123">Hello 미리 보기에서 hello Azure Cosmos DB 클라이언트에서 그래프 확장 API를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-123">In hello preview, we added a graph extension API on hello Azure Cosmos DB client.</span></span> <span data-ttu-id="35d09-124">제작 하는 독립 실행형 그래프 클라이언트 hello Azure Cosmos DB 클라이언트 및 리소스에서 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-124">We are working on a standalone graph client decoupled from hello Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="35d09-125">새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="35d09-126">새 그래프가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="35d09-127">Hello를 사용 하 여 일련의 Gremlin 단계 실행 `CreateGremlinQuery` 메서드.</span><span class="sxs-lookup"><span data-stu-id="35d09-127">A series of Gremlin steps are executed using hello `CreateGremlinQuery` method.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="35d09-128">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="35d09-128">Update your connection string</span></span>

<span data-ttu-id="35d09-129">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="35d09-130">Visual Studio 2017 hello App.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-130">In Visual Studio 2017, open hello App.config file.</span></span> 

2. <span data-ttu-id="35d09-131">Hello Azure Cosmos DB 계정에 Azure 포털에서에서 클릭 **키** 왼쪽 탐색 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-131">In hello Azure portal, in your Azure Cosmos DB account, click **Keys** in hello left navigation.</span></span> 

    ![표시 및 hello hello 키 페이지에서 Azure 포털에서에서 기본 키를 복사](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="35d09-133">복사 프로그램 **URI** hello 포털에서 값을 하 게 hello App.config에 hello 끝점 키의 값입니다. Hello 스크린 샷 toocopy hello 값 앞에 표시 된 대로 hello 복사 단추를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-133">Copy your **URI** value from hello portal and make it hello value of hello Endpoint key in App.config. You can use hello copy button as shown in hello preceding screenshot toocopy hello value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="35d09-134">복사 프로그램 **기본 키** hello 포털에서 값을 하 게 App.config에 hello AuthKey 키의 값을 hello 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-134">Copy your **PRIMARY KEY** value from hello portal, and make it hello value of hello AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="35d09-135">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-console-app"></a><span data-ttu-id="35d09-136">Hello 콘솔 앱 실행</span><span class="sxs-lookup"><span data-stu-id="35d09-136">Run hello console app</span></span>

1. <span data-ttu-id="35d09-137">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **GraphGetStarted** 프로젝트에서 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-137">In Visual Studio, right-click on hello **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="35d09-138">Hello NuGet에서에서 **찾아보기** 상자에서 입력 *Microsoft.Azure.Graphs* hello를 확인 하 고 **시험판 포함** 상자.</span><span class="sxs-lookup"><span data-stu-id="35d09-138">In hello NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check hello **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="35d09-139">Hello 결과 통해 설치 hello **Microsoft.Azure.Graphs** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-139">From hello results, install hello **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="35d09-140">Hello Azure Cosmos DB 그래프 확장 라이브러리 패키지 및 모든 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-140">This installs hello Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="35d09-141">클릭 하 여 변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 가져오면 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="35d09-142">라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-142">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="35d09-143">CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-143">Click CTRL + F5 toorun hello application.</span></span>

   <span data-ttu-id="35d09-144">hello 정점 및 가장자리 toohello 그래프 추가 되 고 hello 콘솔 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-144">hello console window displays hello vertexes and edges being added toohello graph.</span></span> <span data-ttu-id="35d09-145">Hello 스크립트가 완료 되 면 ENTER 키를 누릅니다 tooclose hello 콘솔 창에 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-145">When hello script completes, press ENTER twice tooclose hello console window.</span></span> 

## <a name="browse-using-hello-data-explorer"></a><span data-ttu-id="35d09-146">Hello 데이터 탐색기를 사용 하 여 찾아보기</span><span class="sxs-lookup"><span data-stu-id="35d09-146">Browse using hello Data Explorer</span></span>

<span data-ttu-id="35d09-147">이제 다시 hello Azure 포털에서에서 tooData 탐색기 및 찾아보기 돌아가서 새 그래프 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-147">You can now go back tooData Explorer in hello Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="35d09-148">데이터 탐색기에서 새 데이터베이스 hello hello 그래프 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-148">In Data Explorer, hello new database appears in hello Graphs pane.</span></span> <span data-ttu-id="35d09-149">**graphdb**, **graphcollz**를 확장하고 **그래프**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-149">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="35d09-150">Hello 클릭 **필터 적용** 단추 toouse hello 기본 tooview hello 그래프에 있는 모든 hello verticies를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-150">Click hello **Apply Filter** button toouse hello default query tooview all hello verticies in hello graph.</span></span> <span data-ttu-id="35d09-151">hello 샘플 응용 프로그램에서 생성 된 hello 데이터 hello 그래프 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-151">hello data generated by hello sample app is displayed in hello Graphs pane.</span></span>

    <span data-ttu-id="35d09-152">Hello 그래프를 축소 수, hello 그래프 표시 공간 확장, 추가 verticies 추가 한 hello에 verticies 화면으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-152">You can zoom in and out of hello graph, you can expand hello graph display space, add additional verticies, and move verticies on hello display surface.</span></span>

    ![Hello Azure 포털에서에서 데이터 탐색기에서 hello 그래프 보기](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="35d09-154">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="35d09-154">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="35d09-155">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="35d09-155">Clean up resources</span></span>

<span data-ttu-id="35d09-156">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="35d09-156">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="35d09-157">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-157">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="35d09-158">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-158">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35d09-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35d09-159">Next steps</span></span>

<span data-ttu-id="35d09-160">이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 그래프를 만듭니다 하 고 응용 프로그램을 실행 하는 방법 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-160">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="35d09-161">이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d09-161">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="35d09-162">Gremlin을 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="35d09-162">Query using Gremlin</span></span>](tutorial-query-graph.md)

