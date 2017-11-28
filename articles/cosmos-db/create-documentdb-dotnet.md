---
title: "Azure Cosmos DB:.net 웹 앱을 빌드하고 DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하면.NET 코드 예제는 hello Azure Cosmos DB DocumentDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="dc8d0-103">Azure Cosmos DB:.net DocumentDB API 웹 앱을 빌드하고 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="dc8d0-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="dc8d0-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="dc8d0-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="dc8d0-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="dc8d0-107">그런 다음 빌드하고 hello에 작성 하는 할 일 목록 웹 앱을 배포 [DocumentDB.NET API](documentdb-sdk-dotnet.md)hello 스크린 샷 뒤에 나타난 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![샘플 데이터를 사용한 Todo 앱](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="dc8d0-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dc8d0-109">Prerequisites</span></span>

<span data-ttu-id="dc8d0-110">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="dc8d0-111">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="dc8d0-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="dc8d0-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="dc8d0-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="dc8d0-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="dc8d0-114">샘플 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="dc8d0-114">Add sample data</span></span>

<span data-ttu-id="dc8d0-115">이제 데이터 탐색기를 사용 하 여 데이터 tooyour 새 컬렉션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="dc8d0-116">데이터 탐색기 hello 새 데이터베이스 hello 모음 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="dc8d0-117">Hello 확장 **작업** hello 확장 하 고, 데이터베이스 **항목** 컬렉션 클릭 **문서**, 클릭 하 고 **새 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 문서 만들기](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="dc8d0-119">이제 다음 구조 hello로 문서 toohello 컬렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="dc8d0-120">Hello json toohello 추가 하면 **문서** 탭을 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Json 데이터에 복사한 hello Azure 포털에서에서 데이터 탐색기에서 저장 클릭](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="dc8d0-122">만들기 및 저장 한 더 많은 문서 hello에 대 한 고유한 값을 삽입할 `id` 속성 및 기타 속성을 원하는 대로 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="dc8d0-123">Azure Cosmos DB가 데이터에 어떠한 스키마도 적용하지 않으므로 새 문서는 사용자가 원하는 어떠한 구조든 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="dc8d0-124">이제 데이터 데이터 탐색기 tooretrieve에서 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="dc8d0-125">기본적으로 데이터 탐색기 사용 `SELECT * FROM c` tooretrieve hello 컬렉션에서 모든 문서에 해당 tooa 다른 변경할 수 [SQL 쿼리](documentdb-sql-query.md)와 같은 `SELECT * FROM c ORDER BY c._ts DESC`, 내림차순으로 정렬 하는 모든 hello 문서 기반 tooreturn 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="dc8d0-126">데이터 탐색기 toocreate 저장 프로시저, Udf 및 트리거 tooperform 서버 쪽 비즈니스 논리도을 사용할 수도 있습니다 눈금 처리량으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="dc8d0-127">데이터 탐색기의 hello 프로그래밍 방식으로 기본 제공 데이터 액세스 Api, hello에서 사용할 수 있는 모든 아니라 hello Azure 포털에에서 쉽게 액세스할 수 있도록 tooyour 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="dc8d0-128">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="dc8d0-128">Clone hello sample application</span></span>

<span data-ttu-id="dc8d0-129">이제 코드로 tooworking 전환 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="dc8d0-130">GitHub hello 연결 문자열을 설정 하 고 실행에서 DocumentDB API 앱을 복제할 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="dc8d0-131">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="dc8d0-132">예: git bash git 터미널 윈도우를 열고 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="dc8d0-133">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="dc8d0-134">그런 다음 Visual Studio에서 hello todo 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="dc8d0-135">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="dc8d0-135">Review hello code</span></span>

<span data-ttu-id="dc8d0-136">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="dc8d0-137">다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello DocumentDBRepository.cs 파일을 찾을 수입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="dc8d0-138">hello DocumentClient 73 줄에 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="dc8d0-139">88번 줄에서 새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="dc8d0-140">107번 줄에서 새 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="dc8d0-141">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="dc8d0-141">Update your connection string</span></span>

<span data-ttu-id="dc8d0-142">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="dc8d0-143">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="dc8d0-144">Hello 다음 단계에서 hello web.config 파일로 hello 화면 toocopy hello URI의 hello 오른쪽에서 복사 단추 hello와 기본 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="dc8d0-146">Visual Studio 2017 hello web.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="dc8d0-147">Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게 hello web.config에 hello 끝점 키의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="dc8d0-148">그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello hello authKey web.config에서의 값입니다. 이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="dc8d0-149">Hello 웹 앱 실행</span><span class="sxs-lookup"><span data-stu-id="dc8d0-149">Run hello web app</span></span>
1. <span data-ttu-id="dc8d0-150">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="dc8d0-151">Hello NuGet에서에서 **찾아보기** 상자에서 입력 *DocumentDB*합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="dc8d0-152">Hello 결과 통해 설치 hello **Microsoft.Azure.DocumentDB** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="dc8d0-153">Hello Microsoft.Azure.DocumentDB 패키지 뿐만 아니라 모든 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="dc8d0-154">CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="dc8d0-155">앱이 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="dc8d0-156">클릭 **새로 만들기** 브라우저 hello와 할 일 앱에서 몇 가지 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![샘플 데이터를 사용한 Todo 앱](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="dc8d0-158">이제 다시 tooData 탐색기 및 쿼리를 참조, 수정 돌아가서이 새 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="dc8d0-159">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="dc8d0-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="dc8d0-160">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="dc8d0-160">Clean up resources</span></span>

<span data-ttu-id="dc8d0-161">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="dc8d0-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="dc8d0-162">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="dc8d0-163">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc8d0-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc8d0-164">Next steps</span></span>

<span data-ttu-id="dc8d0-165">이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 하 고 웹 응용 프로그램을 실행 하는 방법 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="dc8d0-166">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc8d0-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc8d0-167">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="dc8d0-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


