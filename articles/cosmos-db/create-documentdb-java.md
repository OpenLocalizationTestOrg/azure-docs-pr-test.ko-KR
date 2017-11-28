---
title: "Java 사용 하 여 Azure Cosmos DB 문서 데이터베이스 aaaCreate | Microsoft Docs | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용할 수는 Java 코드 샘플 hello Azure Cosmos DB DocumentDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="8533f-103">Azure Cosmos DB: Java를 사용 하 여 문서 데이터베이스를 만들고 Azure 포털 hello</span><span class="sxs-lookup"><span data-stu-id="8533f-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="8533f-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8533f-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="8533f-106">이 퀵 스타트의 문서 만듭니다 포털 Azure tools for Azure Cosmos DB hello 사용 하 여 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="8533f-107">이 퀵 스타트의 표시 tooquickly hello를 사용 하 여 Java 콘솔 응용 프로그램을 만드는 방법을 [DocumentDB Java API](documentdb-sdk-java.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="8533f-108">이 빠른 시작의 hello 지침 Java 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="8533f-109">이 빠른 시작을 완료 하 여 만들고 수정 hello UI 또는 프로그래밍 방식으로, 기본 설정을 더 문서 데이터베이스 리소스에 잘 알고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8533f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8533f-110">Prerequisites</span></span>

* [<span data-ttu-id="8533f-111">JDK(Java Development Kit) 1.7+</span><span class="sxs-lookup"><span data-stu-id="8533f-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="8533f-112">Ubuntu, 실행 `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="8533f-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="8533f-113">Hello JDK 설치 되어 있는지 tooset hello JAVA_HOME 환경 변수 toopoint toohello 폴더 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="8533f-114">[Maven](http://maven.apache.org/) 이진 아카이브 [다운로드](http://maven.apache.org/download.cgi) 및 [설치](http://maven.apache.org/install.html)</span><span class="sxs-lookup"><span data-stu-id="8533f-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="8533f-115">Ubuntu, 실행할 수 있습니다 `apt-get install maven` tooinstall Maven 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="8533f-116">Git</span><span class="sxs-lookup"><span data-stu-id="8533f-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="8533f-117">Ubuntu, 실행할 수 있습니다 `sudo apt-get install git` tooinstall Git 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="8533f-118">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="8533f-118">Create a database account</span></span>

<span data-ttu-id="8533f-119">문서 데이터베이스를 만들기 전에 Azure Cosmos db (DocumentDB) SQL 데이터베이스 계정 toocreate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="8533f-120">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="8533f-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="8533f-121">샘플 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="8533f-121">Add sample data</span></span>

<span data-ttu-id="8533f-122">이제 데이터 탐색기를 사용 하 여 데이터 tooyour 새 컬렉션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="8533f-123">데이터 탐색기 hello 새 데이터베이스 hello 모음 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="8533f-124">Hello 확장 **작업** hello 확장 하 고, 데이터베이스 **항목** 컬렉션 클릭 **문서**, 클릭 하 고 **새 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 문서 만들기](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="8533f-126">이제 다음 구조 hello로 문서 toohello 컬렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="8533f-127">Hello json toohello 추가 하면 **문서** 탭을 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Json 데이터에 복사한 hello Azure 포털에서에서 데이터 탐색기에서 저장 클릭](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="8533f-129">만들기 및 저장 한 더 많은 문서 hello에 대 한 고유한 값을 삽입할 `id` 속성 및 기타 속성을 원하는 대로 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="8533f-130">Azure Cosmos DB가 데이터에 어떠한 스키마도 적용하지 않으므로 새 문서는 사용자가 원하는 어떠한 구조든 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="8533f-131">Hello를 클릭 하 여 데이터의 데이터 탐색기 tooretrieve 쿼리 사용 하 여 이제 수 **필터 편집** 및 **필터 적용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="8533f-132">기본적으로 데이터 탐색기 사용 `SELECT * FROM c` tooretrieve hello 컬렉션에서 모든 문서에 해당 tooa 다른 변경할 수 [SQL 쿼리](documentdb-sql-query.md)와 같은 `SELECT * FROM c ORDER BY c._ts DESC`, 내림차순으로 정렬 하는 모든 hello 문서 기반 tooreturn 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="8533f-133">데이터 탐색기 toocreate 저장 프로시저, Udf 및 트리거 tooperform 서버 쪽 비즈니스 논리도을 사용할 수도 있습니다 눈금 처리량으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="8533f-134">데이터 탐색기의 hello 프로그래밍 방식으로 기본 제공 데이터 액세스 Api, hello에서 사용할 수 있는 모든 아니라 hello Azure 포털에에서 쉽게 액세스할 수 있도록 tooyour 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="8533f-135">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="8533f-135">Clone hello sample application</span></span>

<span data-ttu-id="8533f-136">이제 코드로 tooworking 전환 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="8533f-137">GitHub hello 연결 문자열을 설정 하 고 실행에서 DocumentDB API 앱을 복제할 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="8533f-138">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="8533f-139">예: git bash git 터미널 윈도우를 열고 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="8533f-140">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="8533f-141">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="8533f-141">Review hello code</span></span>

<span data-ttu-id="8533f-142">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="8533f-143">열기 hello `Program.java` hello \src\GetStarted 폴더에서 파일 및 리소스를 만드는 hello Azure Cosmos DB이 코드이 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="8533f-144">hello `DocumentClient` 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="8533f-145">새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="8533f-146">새 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="8533f-147">일부 문서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="8533f-148">JSON을 통해 SQL 쿼리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="8533f-149">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="8533f-149">Update your connection string</span></span>

<span data-ttu-id="8533f-150">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="8533f-151">이렇게 하면 응용 프로그램 toocommunicate 호스팅된 데이터베이스와 함께 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="8533f-152">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="8533f-153">Hello에 hello 화면 toocopy hello URI의 오른쪽 hello와 기본 키에서 hello 복사 단추를 사용 한다고 `Program.java` hello 다음 단계에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="8533f-155">Hello open에서 `Program.java` 파일 (hello 복사 단추 사용) 하는 hello 포털에서 URI 값을 복사 하 고 쉽게에 hello 끝점 toohello DocumentClient 생성자의 값을 hello `Program.java`합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="8533f-156">그런 다음 hello 포털에서 기본 키 값을 복사 하 고 있으므로 "FILLME" 위에 붙여넣을 hello hello DocumentClient 생성자의 두 번째 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="8533f-157">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="8533f-158">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="8533f-158">Run hello app</span></span>

1. <span data-ttu-id="8533f-159">Hello git 터미널 창에서 `cd` toohello azure-cosmos-db-documentdb-java-getting-started 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="8533f-160">Hello git 터미널 창에서 입력 `mvn package` tooinstall hello Java 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="8533f-161">Hello git 터미널 창에서 실행 `mvn exec:java -D exec.mainClass=GetStarted.Program` 에 hello 터미널 윈도우 toostart Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="8533f-162">Hello 터미널 창에서 데이터베이스를 만들 FamilyDB hello 알림과 toopress 키 toocontinue 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="8533f-163">키 toocreate hello 데이터베이스를 누르고 전환 하는 데이터 탐색기 toohello FamilyDB 데이터베이스 포함 되어 있음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="8533f-164">Toopress는 키 toocreate hello 컬렉션 및 hello 문서를 계속 하 고 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="8533f-165">Hello 프로젝트 완료 되 면 hello 리소스 계정에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="8533f-167">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="8533f-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8533f-168">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="8533f-168">Clean up resources</span></span>

<span data-ttu-id="8533f-169">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="8533f-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="8533f-170">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="8533f-171">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8533f-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8533f-172">Next steps</span></span>

<span data-ttu-id="8533f-173">이 퀵 스타트의 어떻게 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 hello 데이터 탐색기를 사용 하 여 이동 하 고 앱 toodo 실행 hello 똑같은 프로그래밍 방식으로 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="8533f-174">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8533f-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8533f-175">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="8533f-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


