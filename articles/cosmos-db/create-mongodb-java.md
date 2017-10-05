---
title: "Azure Cosmos DB: Java 및 MongoDB API에서 콘솔 앱 작성 | Microsoft Docs"
description: "Azure Cosmos DB MongoDB API에 연결 및 쿼리하는 데 사용할 수 있는 Java 코드 샘플을 제시합니다."
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="263d4-103">Azure Cosmos DB: Java 및 Azure Portal에서 MongoDB API 콘솔 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="263d4-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="263d4-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="263d4-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="263d4-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="263d4-107">그런 다음, [MongoDB Java 드라이버](https://docs.mongodb.com/ecosystem/drivers/java/)에서 작성한 콘솔 앱을 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="263d4-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="263d4-108">Prerequisites</span></span>

* <span data-ttu-id="263d4-109">이 샘플을 실행하기 전에 다음 필수 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="263d4-110">JDK 1.7+(JDK가 없는 경우 `apt-get install default-jdk` 실행)</span><span class="sxs-lookup"><span data-stu-id="263d4-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="263d4-111">Maven(Maven이 없는 경우 `apt-get install maven` 실행)</span><span class="sxs-lookup"><span data-stu-id="263d4-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="263d4-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="263d4-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="263d4-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="263d4-113">Add a collection</span></span>

<span data-ttu-id="263d4-114">새 사용자 데이터베이스 이름을 **db**로 지정하고 새로운 컬렉션 이름을 **coll**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="263d4-115">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="263d4-115">Clone the sample application</span></span>

<span data-ttu-id="263d4-116">이제 GitHub에서 MongoDB API 앱을 복제하고 연결 문자열을 설정한 다음 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="263d4-117">프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="263d4-118">git bash와 같은 git 터미널 창을 열고 `cd`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="263d4-119">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="263d4-120">그런 다음 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="263d4-121">코드 검토</span><span class="sxs-lookup"><span data-stu-id="263d4-121">Review the code</span></span>

<span data-ttu-id="263d4-122">앱에서 어떤 상황이 발생하고 있는지 빠르게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="263d4-123">`Program.cs` 파일을 열어 보면 이들 코드 줄에서 Azure Cosmos DB 리소스를 만드는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="263d4-124">DocumentClient가 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="263d4-125">새 데이터베이스 및 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="263d4-126">`MongoCollection.insertOne`을 사용하여 일부 문서가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="263d4-127">`MongoCollection.find`을 사용하여 일부 쿼리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="263d4-128">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="263d4-128">Update your connection string</span></span>

<span data-ttu-id="263d4-129">이제 Azure Portal로 다시 이동하여 연결 문자열 정보를 가져와서 앱에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="263d4-130">계정에서 **빠른 시작**을 선택하고 Java를 선택한 다음 연결 문자열을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="263d4-131">`Program.java` 파일을 열고 MongoClientURI 생성자에 대한 인수를 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="263d4-132">이제 Azure Cosmos DB와 통신하는 데 필요한 모든 정보로 앱이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="263d4-133">콘솔 앱 실행</span><span class="sxs-lookup"><span data-stu-id="263d4-133">Run the console app</span></span>

1. <span data-ttu-id="263d4-134">터미널에서 `mvn package`를 실행하여 필요한 npm 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="263d4-135">터미널에서 `mvn exec:java -D exec.mainClass=GetStarted.Program`을 실행하여 Java 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="263d4-136">이제 [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md)를 사용하여 이 새 데이터를 쿼리, 수정 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="263d4-137">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="263d4-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="263d4-138">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="263d4-138">Clean up resources</span></span>

<span data-ttu-id="263d4-139">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="263d4-140">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="263d4-141">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="263d4-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="263d4-142">Next steps</span></span>

<span data-ttu-id="263d4-143">이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 컬렉션을 만들고, 콘솔 앱을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="263d4-144">이제 사용자의 Cosmos DB 계정에 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="263d4-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="263d4-145">Azure Cosmos DB로 MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="263d4-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


