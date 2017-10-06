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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java를 사용 하 여 문서 데이터베이스를 만들고 Azure 포털 hello

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 퀵 스타트의 문서 만듭니다 포털 Azure tools for Azure Cosmos DB hello 사용 하 여 데이터베이스입니다. 이 퀵 스타트의 표시 tooquickly hello를 사용 하 여 Java 콘솔 응용 프로그램을 만드는 방법을 [DocumentDB Java API](documentdb-sdk-java.md)합니다. 이 빠른 시작의 hello 지침 Java 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다. 이 빠른 시작을 완료 하 여 만들고 수정 hello UI 또는 프로그래밍 방식으로, 기본 설정을 더 문서 데이터베이스 리소스에 잘 알고 수 있습니다.

## <a name="prerequisites"></a>필수 조건

* [JDK(Java Development Kit) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Ubuntu, 실행 `apt-get install default-jdk` tooinstall hello JDK.
    * Hello JDK 설치 되어 있는지 tooset hello JAVA_HOME 환경 변수 toopoint toohello 폴더 수 있습니다.
* [Maven](http://maven.apache.org/) 이진 아카이브 [다운로드](http://maven.apache.org/download.cgi) 및 [설치](http://maven.apache.org/install.html)
    * Ubuntu, 실행할 수 있습니다 `apt-get install maven` tooinstall Maven 합니다.
* [Git](https://www.git-scm.com/)
    * Ubuntu, 실행할 수 있습니다 `sudo apt-get install git` tooinstall Git 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

문서 데이터베이스를 만들기 전에 Azure Cosmos db (DocumentDB) SQL 데이터베이스 계정 toocreate를 해야 합니다.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>컬렉션 추가

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>샘플 데이터 추가

이제 데이터 탐색기를 사용 하 여 데이터 tooyour 새 컬렉션을 추가할 수 있습니다.

1. 데이터 탐색기 hello 새 데이터베이스 hello 모음 창에 표시 됩니다. Hello 확장 **작업** hello 확장 하 고, 데이터베이스 **항목** 컬렉션 클릭 **문서**, 클릭 하 고 **새 문서**합니다. 

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 문서 만들기](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. 이제 다음 구조 hello로 문서 toohello 컬렉션을 추가 합니다.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Hello json toohello 추가 하면 **문서** 탭을 클릭 **저장**합니다.

    ![Json 데이터에 복사한 hello Azure 포털에서에서 데이터 탐색기에서 저장 클릭](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  만들기 및 저장 한 더 많은 문서 hello에 대 한 고유한 값을 삽입할 `id` 속성 및 기타 속성을 원하는 대로 hello 변경 합니다. Azure Cosmos DB가 데이터에 어떠한 스키마도 적용하지 않으므로 새 문서는 사용자가 원하는 어떠한 구조든 가질 수 있습니다.

     Hello를 클릭 하 여 데이터의 데이터 탐색기 tooretrieve 쿼리 사용 하 여 이제 수 **필터 편집** 및 **필터 적용** 단추입니다. 기본적으로 데이터 탐색기 사용 `SELECT * FROM c` tooretrieve hello 컬렉션에서 모든 문서에 해당 tooa 다른 변경할 수 [SQL 쿼리](documentdb-sql-query.md)와 같은 `SELECT * FROM c ORDER BY c._ts DESC`, 내림차순으로 정렬 하는 모든 hello 문서 기반 tooreturn 타임 스탬프입니다. 
 
     데이터 탐색기 toocreate 저장 프로시저, Udf 및 트리거 tooperform 서버 쪽 비즈니스 논리도을 사용할 수도 있습니다 눈금 처리량으로 합니다. 데이터 탐색기의 hello 프로그래밍 방식으로 기본 제공 데이터 액세스 Api, hello에서 사용할 수 있는 모든 아니라 hello Azure 포털에에서 쉽게 액세스할 수 있도록 tooyour 데이터를 제공 합니다.

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 코드로 tooworking 전환 해 보겠습니다. GitHub hello 연결 문자열을 설정 하 고 실행에서 DocumentDB API 앱을 복제할 보겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `CD` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello `Program.java` hello \src\GetStarted 폴더에서 파일 및 리소스를 만드는 hello Azure Cosmos DB이 코드이 줄을 찾습니다. 

* hello `DocumentClient` 초기화 됩니다.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* 새 데이터베이스가 만들어집니다.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* 새 컬렉션이 만들어집니다.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* 일부 문서가 만들어집니다.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* JSON을 통해 SQL 쿼리가 수행됩니다.

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

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다. 이렇게 하면 응용 프로그램 toocommunicate 호스팅된 데이터베이스와 함께 활성화 됩니다.

1. Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다. Hello에 hello 화면 toocopy hello URI의 오른쪽 hello와 기본 키에서 hello 복사 단추를 사용 한다고 `Program.java` hello 다음 단계에는 파일입니다.

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. Hello open에서 `Program.java` 파일 (hello 복사 단추 사용) 하는 hello 포털에서 URI 값을 복사 하 고 쉽게에 hello 끝점 toohello DocumentClient 생성자의 값을 hello `Program.java`합니다. 

    `"https://FILLME.documents.azure.com"`

4. 그런 다음 hello 포털에서 기본 키 값을 복사 하 고 있으므로 "FILLME" 위에 붙여넣을 hello hello DocumentClient 생성자의 두 번째 매개 변수입니다. 이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 
    
## <a name="run-hello-app"></a>Hello 앱 실행

1. Hello git 터미널 창에서 `cd` toohello azure-cosmos-db-documentdb-java-getting-started 폴더입니다.

2. Hello git 터미널 창에서 입력 `mvn package` tooinstall hello Java 패키지가 필요 합니다.

3. Hello git 터미널 창에서 실행 `mvn exec:java -D exec.mainClass=GetStarted.Program` 에 hello 터미널 윈도우 toostart Java 응용 프로그램입니다.

    Hello 터미널 창에서 데이터베이스를 만들 FamilyDB hello 알림과 toopress 키 toocontinue 받게 됩니다. 키 toocreate hello 데이터베이스를 누르고 전환 하는 데이터 탐색기 toohello FamilyDB 데이터베이스 포함 되어 있음을 표시 됩니다. Toopress는 키 toocreate hello 컬렉션 및 hello 문서를 계속 하 고 쿼리를 수행 합니다. Hello 프로젝트 완료 되 면 hello 리소스 계정에서 삭제 됩니다. 

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 퀵 스타트의 어떻게 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 hello 데이터 탐색기를 사용 하 여 이동 하 고 앱 toodo 실행 hello 똑같은 프로그래밍 방식으로 배웠습니다. 이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB로 데이터 가져오기](import-data.md)


