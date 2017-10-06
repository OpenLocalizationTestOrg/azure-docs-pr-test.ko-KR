---
title: "Azure Cosmos DB: Node.js 사용 하 여 앱을 빌드하고 DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하는 Node.js 코드 샘플 hello Azure Cosmos DB DocumentDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="eb14c-103">Azure Cosmos DB: Node.js와 함께 DocumentDB API 앱을 빌드하고 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="eb14c-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="eb14c-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="eb14c-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="eb14c-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="eb14c-107">그런 다음 작성 하 고 hello를 기반으로 하 여 콘솔 응용 프로그램을 실행할 [DocumentDB Node.js API](documentdb-sdk-node.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb14c-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eb14c-108">Prerequisites</span></span>

* <span data-ttu-id="eb14c-109">이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="eb14c-110">[Node.js](https://nodejs.org/en/) 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="eb14c-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="eb14c-111">Git</span><span class="sxs-lookup"><span data-stu-id="eb14c-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="eb14c-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="eb14c-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="eb14c-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="eb14c-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="eb14c-114">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="eb14c-114">Clone hello sample application</span></span>

<span data-ttu-id="eb14c-115">이제 github에서 복제는 DocumentDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="eb14c-116">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="eb14c-117">예: git bash git 터미널 윈도우를 열고 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="eb14c-118">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="eb14c-119">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="eb14c-119">Review hello code</span></span>

<span data-ttu-id="eb14c-120">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="eb14c-121">열기 hello `app.js` 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="eb14c-122">hello `documentClient` 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="eb14c-123">새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb14c-124">새 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb14c-125">일부 문서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb14c-126">JSON을 통해 SQL 쿼리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="eb14c-127">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb14c-127">Update your connection string</span></span>

<span data-ttu-id="eb14c-128">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="eb14c-129">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="eb14c-130">Hello에 hello 화면 toocopy hello URI의 오른쪽 hello와 기본 키에서 hello 복사 단추를 사용 한다고 `config.js` hello 다음 단계에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="eb14c-132">열린 hello `config.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="eb14c-133">Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게에 hello 끝점 키의 값을 hello `config.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="eb14c-134">그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello 값 hello `config.primaryKey` 에서 `config.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="eb14c-135">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="eb14c-136">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="eb14c-136">Run hello app</span></span>
1. <span data-ttu-id="eb14c-137">실행 `npm install` 터미널 tooinstall에 필수 npm 모듈</span><span class="sxs-lookup"><span data-stu-id="eb14c-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="eb14c-138">실행 `node app.js` 터미널 toostart에 응용 프로그램 노드.</span><span class="sxs-lookup"><span data-stu-id="eb14c-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="eb14c-139">이제 다시 tooData 탐색기 및 쿼리를 참조, 수정 돌아가서이 새 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="eb14c-140">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="eb14c-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="eb14c-141">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="eb14c-141">Clean up resources</span></span>

<span data-ttu-id="eb14c-142">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="eb14c-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="eb14c-143">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="eb14c-144">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb14c-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb14c-145">Next steps</span></span>

<span data-ttu-id="eb14c-146">이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 하 고 응용 프로그램을 실행 하는 방법 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="eb14c-147">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb14c-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb14c-148">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="eb14c-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


