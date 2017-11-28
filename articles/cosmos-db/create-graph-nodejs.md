---
title: "Graph API를 사용 하 여 Azure Cosmos DB Node.js 응용 프로그램 aaaBuild | Microsoft Docs"
description: "Tooconnect tooand에서는 Node.js 코드 샘플은 Azure Cosmos DB 쿼리를 표시."
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="96872-103">Azure Cosmos DB: Graph API를 사용하여 Node.js 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="96872-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="96872-104">Cosmos DB azure는 Microsoft에서 전역으로 분산 하는 hello 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="96872-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="96872-106">이 빠른 시작 문서 hello Azure 포털을 사용 하 여 Azure Cosmos DB toocreate Graph API (미리 보기), 데이터베이스 및 그래프에 대 한 고려 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="96872-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="96872-107">그런 다음 빌드 및 실행 하 여 콘솔 응용 프로그램 hello 오픈 소스를 사용 하 여 [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="96872-108">hello npm 모듈 `gremlin-secure` 의 수정된 된 버전은 `gremlin` SSL 및 Azure Cosmos DB를 사용 하 여 연결 하는 데 필요한 SASL 지 원하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="96872-109">소스 코드는 [GitHub](https://github.com/CosmosDB/gremlin-javascript)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="96872-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="96872-110">Prerequisites</span></span>

<span data-ttu-id="96872-111">이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="96872-112">[Node.js](https://nodejs.org/en/) 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="96872-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="96872-113">Git</span><span class="sxs-lookup"><span data-stu-id="96872-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="96872-114">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="96872-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="96872-115">그래프 추가</span><span class="sxs-lookup"><span data-stu-id="96872-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="96872-116">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="96872-116">Clone hello sample application</span></span>

<span data-ttu-id="96872-117">이제 GitHub에서 복제는 Graph API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="96872-118">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96872-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="96872-119">예: Git Bash Git 터미널 윈도우를 열고 변경 (통해 `cd` 명령) tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="96872-120">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="96872-121">Visual Studio에서 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96872-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="96872-122">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="96872-122">Review hello code</span></span>

<span data-ttu-id="96872-123">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="96872-124">열기 hello `app.js` 파일과 있습니다 hello 다음 줄의 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="96872-125">hello Gremlin 클라이언트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="96872-125">hello Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="96872-126">hello 구성은 모두 `config.js`는 hello 다음 섹션에서에서 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="96872-127">Hello로 실행 되는 일련의 Gremlin 단계 `client.execute` 메서드.</span><span class="sxs-lookup"><span data-stu-id="96872-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="96872-128">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="96872-128">Update your connection string</span></span>

1. <span data-ttu-id="96872-129">열기 hello config.js 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="96872-130">Config.js의 hello로 hello config.endpoint 키를 입력 **Gremlin URI** hello에서 값 **개요** hello Azure 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="96872-132">경우 hello **Gremlin URI** hello에서 hello 값을 생성할 수 있습니다, 값이 비어 **키** hello를 사용 하 여 hello 포털에서 페이지 **URI** 값, https://, 제거 및 변경 toographs 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="96872-133">hello Gremlin 끝점만 hello 호스트 이름 이어야 hello 프로토콜/포트 번호 없이 같은 `mygraphdb.graphs.azure.com` (하지 `https://mygraphdb.graphs.azure.com` 또는 `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="96872-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="96872-134">Config.js에서 hello 사용 하 여 hello config.primaryKey 값을 입력 **기본 키** hello에서 값 **키** hello Azure 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Azure 포털 키 블레이드 hello](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="96872-136">Hello 데이터베이스 이름과 config.database 및 config.collection hello 값에 대 한 그래프 (컨테이너) 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="96872-137">완성된 config.js 파일은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="96872-138">Hello 콘솔 앱 실행</span><span class="sxs-lookup"><span data-stu-id="96872-138">Run hello console app</span></span>

1. <span data-ttu-id="96872-139">터미널 윈도우를 열고 변경 (통해 `cd` 명령) hello 프로젝트에 포함 된 hello package.json 파일에 대 한 toohello 설치 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="96872-140">실행 `npm install` tooinstall hello npm 모듈을 포함 하는 데 필요한 `gremlin-secure`합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="96872-141">실행 `node app.js` 터미널 toostart에 응용 프로그램 노드.</span><span class="sxs-lookup"><span data-stu-id="96872-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="96872-142">데이터 탐색기 검색</span><span class="sxs-lookup"><span data-stu-id="96872-142">Browse with Data Explorer</span></span>

<span data-ttu-id="96872-143">이제 Azure 포털 tooview hello에 탐색기 tooData 돌아가서, 쿼리, 수정 하 고 수 작업 하는 새 그래프 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="96872-144">데이터 탐색기에서 새 데이터베이스 hello hello에 나타납니다 **그래프** 창.</span><span class="sxs-lookup"><span data-stu-id="96872-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="96872-145">Hello 컬렉션 hello 데이터베이스를 확장 한 다음 클릭 **그래프**합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="96872-146">hello hello 샘플 응용 프로그램에 의해 생성 된 데이터는 hello 내에서 다음 창 hello **그래프** 를 클릭할 때 탭 **필터 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="96872-147">완료 시도 `g.V()` 와 `.has('firstName', 'Thomas')` tootest hello 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="96872-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="96872-148">Hello 값은 대/소문자 구분 note 마십시오.</span><span class="sxs-lookup"><span data-stu-id="96872-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="96872-149">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="96872-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="96872-150">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="96872-150">Clean up your resources</span></span>

<span data-ttu-id="96872-151">이 앱을 사용 하 여 toocontinue 하지 않으려는 경우 hello 다음을 수행 하 여이 문서에서 만든 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="96872-152">Hello hello 왼쪽된 탐색 메뉴에서 Azure 포털에서에서 클릭 **리소스 그룹**, 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="96872-153">리소스 그룹 페이지에서 클릭 **삭제**hello 리소스 toobe 삭제의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="96872-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96872-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96872-154">Next steps</span></span>

<span data-ttu-id="96872-155">이 문서에서는 Azure Cosmos DB 계정 toocreate 데이터 탐색기를 사용 하 여 그래프를 만듭니다 하 고 응용 프로그램을 실행 하는 방법 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="96872-156">이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96872-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="96872-157">Gremlin을 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="96872-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
