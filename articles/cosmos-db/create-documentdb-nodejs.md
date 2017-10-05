---
title: "Azure Cosmos DB: Node.js 및 DocumentDB API에서 앱 작성 | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API에 연결 및 쿼리하는 데 사용할 수 있는 Node.js 코드 샘플을 제시합니다."
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
ms.openlocfilehash: 26e3548bf6aacbc60c4c46a5cc88749ca14cec01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="0e8c3-103">Azure Cosmos DB: Node.js 및 Azure Portal에서 DocumentDB API 앱 작성</span><span class="sxs-lookup"><span data-stu-id="0e8c3-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and the Azure portal</span></span>

<span data-ttu-id="0e8c3-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0e8c3-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0e8c3-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="0e8c3-107">그런 다음, [DocumentDB Node.js API](documentdb-sdk-node.md)에서 작성한 콘솔 앱을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-107">You then build and run a console app built on the [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e8c3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e8c3-108">Prerequisites</span></span>

* <span data-ttu-id="0e8c3-109">이 샘플을 실행하기 전에 다음 필수 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="0e8c3-110">[Node.js](https://nodejs.org/en/) 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="0e8c3-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="0e8c3-111">Git</span><span class="sxs-lookup"><span data-stu-id="0e8c3-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="0e8c3-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0e8c3-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="0e8c3-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="0e8c3-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="0e8c3-114">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="0e8c3-114">Clone the sample application</span></span>

<span data-ttu-id="0e8c3-115">이제 github에서 DocumentDB API 앱을 복제하고 연결 문자열을 설정한 후 실행해 보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="0e8c3-116">프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-116">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="0e8c3-117">git bash와 같은 git 터미널 창을 열고 `CD`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-117">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="0e8c3-118">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="0e8c3-119">코드 검토</span><span class="sxs-lookup"><span data-stu-id="0e8c3-119">Review the code</span></span>

<span data-ttu-id="0e8c3-120">앱에서 어떤 일이 일어나는지 빠르게 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="0e8c3-121">`app.js` 파일을 열어 보면 이들 코드 줄에서 Azure Cosmos DB 리소스를 만드는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-121">Open the `app.js` file and you find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="0e8c3-122">`documentClient`가 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-122">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="0e8c3-123">새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="0e8c3-124">새 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="0e8c3-125">일부 문서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="0e8c3-126">JSON을 통해 SQL 쿼리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="0e8c3-127">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="0e8c3-127">Update your connection string</span></span>

<span data-ttu-id="0e8c3-128">이제 Azure Portal로 다시 이동하여 연결 문자열 정보를 가져와서 앱에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-128">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="0e8c3-129">[Azure Portal](http://portal.azure.com/)의 Azure Cosmos DB 계정에서 왼쪽 탐색 영역의 **키**를 클릭한 다음 **읽기-쓰기 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-129">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="0e8c3-130">다음 단계에서 화면 오른쪽의 복사 단추를 사용하여 URI 및 기본 키를 `config.js` 파일에 복사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-130">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![Azure Portal에서 선택 키 보기 및 복사, 키 블레이드](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="0e8c3-132">`config.js` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-132">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="0e8c3-133">포털에서 URI 값을 복사(복사 단추 사용)한 후 이 값을 `config.js`의 끝점 키 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-133">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="0e8c3-134">그 다음, 포털에서 사용자의 기본 키 값을 복사한 후 `config.js`의 `config.primaryKey` 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-134">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="0e8c3-135">이제 Azure Cosmos DB와 통신하는 데 필요한 모든 정보로 앱이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-135">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="0e8c3-136">앱 실행</span><span class="sxs-lookup"><span data-stu-id="0e8c3-136">Run the app</span></span>
1. <span data-ttu-id="0e8c3-137">터미널에서 `npm install`를 실행하여 필요한 npm 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-137">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="0e8c3-138">터미널에서 `node app.js`을 실행하여 노드 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-138">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="0e8c3-139">이제 데이터 탐색기로 돌아가서 이 새 데이터를 쿼리 및 수정하고 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-139">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="0e8c3-140">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="0e8c3-140">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="0e8c3-141">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="0e8c3-141">Clean up resources</span></span>

<span data-ttu-id="0e8c3-142">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-142">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="0e8c3-143">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-143">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="0e8c3-144">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-144">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e8c3-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e8c3-145">Next steps</span></span>

<span data-ttu-id="0e8c3-146">이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 컬렉션을 만들고, 앱을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-146">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="0e8c3-147">이제 사용자의 Cosmos DB 계정에 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e8c3-147">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e8c3-148">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e8c3-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


