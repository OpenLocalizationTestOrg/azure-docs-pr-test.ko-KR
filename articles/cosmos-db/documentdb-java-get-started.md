---
title: "NoSQL 자습서:Azure Cosmos DB Java SDK용 DocumentDB API | Microsoft Docs"
description: "Azure Cosmos DB용 DocumentDB API를 사용하여 온라인 데이터베이스 및 Java 콘솔 응용 프로그램을 만드는 NoSQL 자습서입니다. Azure DocumentDB는 JSON에 대한 NoSQL 데이터베이스입니다."
keywords: "NoSQL 자습서, 온라인 데이터베이스, Java 콘솔 응용 프로그램"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="f0c2c-105">NoSQL 자습서: DocumentDB API Java 콘솔 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="f0c2c-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0c2c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f0c2c-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f0c2c-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f0c2c-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f0c2c-108">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="f0c2c-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f0c2c-109">Node.JS</span><span class="sxs-lookup"><span data-stu-id="f0c2c-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f0c2c-110">Java</span><span class="sxs-lookup"><span data-stu-id="f0c2c-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f0c2c-111">C++</span><span class="sxs-lookup"><span data-stu-id="f0c2c-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f0c2c-112">Azure Cosmos DB Java SDK용 DocumentDB API에 대한 NoSQL 자습서를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="f0c2c-113">이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f0c2c-114">다음 항목에 대해서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-114">We cover:</span></span>

* <span data-ttu-id="f0c2c-115">Azure Cosmos DB 계정 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="f0c2c-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="f0c2c-116">Visual Studio 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="f0c2c-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="f0c2c-117">온라인 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-117">Creating an online database</span></span>
* <span data-ttu-id="f0c2c-118">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-118">Creating a collection</span></span>
* <span data-ttu-id="f0c2c-119">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-119">Creating JSON documents</span></span>
* <span data-ttu-id="f0c2c-120">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="f0c2c-120">Querying the collection</span></span>
* <span data-ttu-id="f0c2c-121">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-121">Creating JSON documents</span></span>
* <span data-ttu-id="f0c2c-122">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="f0c2c-122">Querying the collection</span></span>
* <span data-ttu-id="f0c2c-123">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-123">Replacing a document</span></span>
* <span data-ttu-id="f0c2c-124">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="f0c2c-124">Deleting a document</span></span>
* <span data-ttu-id="f0c2c-125">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="f0c2c-125">Deleting the database</span></span>

<span data-ttu-id="f0c2c-126">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0c2c-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0c2c-127">Prerequisites</span></span>
<span data-ttu-id="f0c2c-128">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-128">Make sure you have the following:</span></span>

* <span data-ttu-id="f0c2c-129">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-129">An active Azure account.</span></span> <span data-ttu-id="f0c2c-130">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="f0c2c-131">또는 이 자습서에 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="f0c2c-132">Git</span><span class="sxs-lookup"><span data-stu-id="f0c2c-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="f0c2c-133">[JDK(Java Development Kit) 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="f0c2c-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="f0c2c-134">[Maven](http://maven.apache.org/download.cgi)</span><span class="sxs-lookup"><span data-stu-id="f0c2c-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f0c2c-135">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f0c2c-136">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f0c2c-137">사용하려는 계정이 이미 있는 경우 [GitHub 프로젝트 복제](#GitClone)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="f0c2c-138">Azure Cosmos DB 에뮬레이터를 사용할 경우 [Azure Cosmos DB 에뮬레이터](local-emulator.md)의 단계에 따라 에뮬레이터를 설정하고 [GitHub 프로젝트 복제](#GitClone)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f0c2c-139"><a id="GitClone"></a>2단계: GitHub 프로젝트 복제</span><span class="sxs-lookup"><span data-stu-id="f0c2c-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="f0c2c-140">[Azure Cosmos DB 및 Java 시작](https://github.com/Azure-Samples/documentdb-java-getting-started)의 경우 GitHub 리포지토리를 복제하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="f0c2c-141">예를 들어 로컬 디렉터리에서 다음을 실행하여 샘플 프로젝트를 로컬로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="f0c2c-142">디렉터리에는 프로젝트의 `pom.xml` 및 `Program.java`을 비롯한 Java 소스 코드를 포함하는 `src` 폴더를 포함합니다. 여기서는 Azure Cosmos DB를 사용하여 문서 만들기 및 컬렉션 내에서 데이터 쿼리와 같은 단순한 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="f0c2c-143">`pom.xml`은 [Maven의 DocumentDB Java SDK](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb)에 대한 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="f0c2c-144"><a id="Connect"></a>3단계: Azure Cosmos DB 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="f0c2c-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="f0c2c-145">다음으로 [Azure Portal](https://portal.azure.com)로 다시 이동하여 끝점과 기본 마스터 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="f0c2c-146">Azure Cosmos DB 끝점과 기본 키는 응용 프로그램에서 연결할 위치를 식별하고 Azure Cosmos DB에서 응용 프로그램의 연결을 신뢰하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="f0c2c-147">Azure Portal에서 Azure Cosmos DB 계정으로 이동한 다음 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="f0c2c-148">포털에서 URI를 복사하고 Program.java 파일의 `https://FILLME.documents.azure.com`에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="f0c2c-149">그런 다음 포털에서 기본 키를 복사하고 `FILLME`에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Java 콘솔 응용 프로그램을 만들기 위해 NoSQL 자습서에서 사용하는 Azure Portal의 스크린샷입니다.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="f0c2c-152">4단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-152">Step 4: Create a database</span></span>
<span data-ttu-id="f0c2c-153">**DocumentClient** 클래스의 [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) 메서드를 사용하여 Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="f0c2c-154">데이터베이스는 여러 컬렉션으로 분할된 JSON 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="f0c2c-155"><a id="CreateColl"></a>5단계: 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f0c2c-156">**createCollection**은 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="f0c2c-157">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="f0c2c-158">**DocumentClient** 클래스의 [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) 메서드를 사용하여 [컬렉션](documentdb-resources.md#collections)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="f0c2c-159">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="f0c2c-160"><a id="CreateDoc"></a>6단계: JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="f0c2c-161">**DocumentClient** 클래스의 [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) 메서드를 사용하여 [문서](documentdb-resources.md#documents)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="f0c2c-162">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f0c2c-163">이제 하나 이상의 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-163">We can now insert one or more documents.</span></span> <span data-ttu-id="f0c2c-164">데이터베이스에 저장하려는 데이터가 이미 있는 경우 Azure Cosmos DB의 [데이터 마이그레이션 도구](import-data.md)를 사용하여 데이터를 데이터베이스로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![NoSQL에서 Java 콘솔 응용 프로그램을 만들기 위해 사용한 계정, 데이터베이스, 컬렉션 및 문서 간의 계층 관계를 보여 주는 다이어그램](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="f0c2c-166"><a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="f0c2c-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f0c2c-167">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="f0c2c-168">다음 샘플 코드에서는 [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) 메서드와 함께 SQL 구문을 사용하여 Azure Cosmos DB의 문서를 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="f0c2c-169"><a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f0c2c-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="f0c2c-170">Azure Cosmos DB는 [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) 메서드를 사용하여 JSON 문서를 업데이트하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="f0c2c-171"><a id="DeleteDocument"></a>9단계: JSON 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="f0c2c-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="f0c2c-172">마찬가지로, Azure Cosmos DB는 [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) 메서드를 사용하여 JSON 문서를 삭제하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="f0c2c-173"><a id="DeleteDatabase"></a>10단계: 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="f0c2c-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="f0c2c-174">만든 데이터베이스를 삭제하면 데이터베이스와 모든 하위 리소스(컬렉션, 문서 등)가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="f0c2c-175"><a id="Run"></a>11단계: Java 콘솔 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="f0c2c-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="f0c2c-176">콘솔에서 응용 프로그램을 실행하려면 프로젝트 폴더로 이동하고 Maven을 사용하여 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="f0c2c-177">`mvn package`를 실행하면 Maven에서 최신 Azure Cosmos DB 라이브러리를 다운로드하고 `GetStarted-0.0.1-SNAPSHOT.jar`을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="f0c2c-178">그 후에 다음을 실행하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="f0c2c-179">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-179">Congratulations!</span></span> <span data-ttu-id="f0c2c-180">이 NoSQL 자습서를 완료했으며 실행되는 Java 콘솔 응용 프로그램이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c2c-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0c2c-181">Next steps</span></span>
* <span data-ttu-id="f0c2c-182">Java 웹앱 자습서가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="f0c2c-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="f0c2c-183">[Azure Cosmos DB를 사용하여 Java로 웹 응용 프로그램 빌드](documentdb-java-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="f0c2c-184">[Azure Cosmos DB 계정 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f0c2c-185">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f0c2c-186">[Azure Cosmos DB 설명서](https://azure.microsoft.com/documentation/services/documentdb/) 페이지의 개발 섹션에서 프로그래밍 모델에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0c2c-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
