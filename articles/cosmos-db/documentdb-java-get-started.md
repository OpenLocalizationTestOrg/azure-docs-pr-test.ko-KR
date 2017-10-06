---
title: "NoSQL 자습서:Azure Cosmos DB Java SDK용 DocumentDB API | Microsoft Docs"
description: "NoSQL 하는 자습서는 Azure Cosmos DB에 대 한 hello DocumentDB API를 사용 하 여 콘솔 응용 프로그램 Java와 온라인 데이터베이스를 만듭니다. Azure DocumentDB는 JSON에 대한 NoSQL 데이터베이스입니다."
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
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>NoSQL 자습서: DocumentDB API Java 콘솔 응용 프로그램 빌드
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB용 Node.js](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Azure Cosmos DB Java SDK에 대 한 hello DocumentDB API에 대 한 toohello NoSQL 자습서를 시작! 이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.

다음 항목에 대해서 다룹니다.

* 만들기 및 tooan Azure Cosmos DB 계정 연결
* Visual Studio 솔루션 구성
* 온라인 데이터베이스 만들기
* 컬렉션 만들기
* JSON 문서 만들기
* Hello 컬렉션 쿼리
* JSON 문서 만들기
* Hello 컬렉션 쿼리
* 문서 바꾸기
* 문서 삭제
* Hello 데이터베이스 삭제

이제 시작하겠습니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음 항목이 있는지 확인 합니다.

* 활성 Azure 계정. 계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다. Hello 또는 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.
* [Git](https://git-scm.com/downloads)
* [JDK(Java Development Kit) 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven](http://maven.apache.org/download.cgi)

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1단계: Azure Cosmos DB 계정 만들기
Azure Cosmos DB 계정을 만들어 보겠습니다. Toouse 원하는 계정을 이미 있는 경우 건너뛰어도 너무[복제 hello GitHub 프로젝트](#GitClone)합니다. Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따라 [Azure Cosmos DB 에뮬레이터](local-emulator.md) tooset hello 에뮬레이터 및 너무 건너 뛸[복제 hello GitHub 프로젝트](#GitClone)합니다.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>2 단계: 복제 hello GitHub 프로젝트
에 대 한 hello GitHub 리포지토리를 복제 하 여 시작할 수 있습니다 [Azure Cosmos DB 및 Java 시작](https://github.com/Azure-Samples/documentdb-java-getting-started)합니다. 예를 들어 로컬 디렉터리에서 hello 다음 tooretrieve hello 샘플 프로젝트를 로컬로 실행 합니다.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

hello 디렉터리에는 `pom.xml` hello 프로젝트에 대 한 및 `src` 포함 하 여 Java 소스 코드에 포함 된 폴더 `Program.java` 는 문서 만들기 및 쿼리 내에서 데이터와 같은 Azure Cosmos DB와 함께 간단한 작업을 어떻게 수행는 컬렉션입니다. hello `pom.xml` hello에 대 한 종속성을 포함 [Maven에서 DocumentDB Java SDK](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb)합니다.

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>3 단계: tooan Cosmos DB Azure 계정을 연결 하세요.
Toohello 돌아가 다음으로, [Azure 포털](https://portal.azure.com) tooretrieve 끝점 및 기본 마스터 키입니다. hello Azure Cosmos DB 끝점 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다.

에 Azure 포털 hello, tooyour Azure Cosmos DB 계정을 탐색 한 다음 클릭 **키**합니다. Hello 포털에서 hello URI를 복사 하 고 붙여 넣습니다 `https://FILLME.documents.azure.com` hello Program.java 파일에 있습니다. 그러면 복사본 hello 포털에서 기본 키를 hello에 붙여 넣습니다 `FILLME`합니다.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Azure 포털 hello NoSQL 자습서 toocreate Java 콘솔 응용 프로그램에서 사용 하는 hello 스크린 샷 계정에 강조 표시 하는 hello 활성 허브 hello 키 단추가 hello Azure Cosmos DB 계정 블레이드에서 강조 표시 및 hello URI, 기본 키 및 보조 키 값에 강조 표시 된 hello 키 블레이드에서 Azure Cosmos DB를 보여 줍니다.][keys]

## <a name="step-4-create-a-database"></a>4단계: 데이터베이스 만들기
Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 만들 수 [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) hello 방식의 **DocumentClient** 클래스입니다. 데이터베이스는 컬렉션에 분할 된 JSON 문서 저장소의 hello 논리적 컨테이너입니다.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>5단계: 컬렉션 만들기
> [!WARNING]
> **createCollection**은 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.
> 
> 

A [컬렉션](documentdb-resources.md#collections) hello를 사용 하 여 만들 수 [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) hello 방식의 **DocumentClient** 클래스입니다. 컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>6단계: JSON 문서 만들기
A [문서](documentdb-resources.md#documents) hello를 사용 하 여 만들 수 [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) hello 방식의 **DocumentClient** 클래스입니다. 문서는 사용자 정의(임의) JSON 콘텐츠입니다. 이제 하나 이상의 문서를 삽입할 수 있습니다. 원하는 toostore 데이터베이스의 데이터를 이미 있는 경우 Azure Cosmos DB를 사용할 수 있습니다 [데이터 마이그레이션 도구](import-data.md) tooimport hello 데이터를 데이터베이스에 있습니다.

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

![Hello 계정과 hello 온라인 데이터베이스, hello 컬렉션 hello NoSQL 자습서 toocreate Java 콘솔 응용 프로그램에서 사용 하는 hello 문서 간의 hello 계층 관계를 보여 주는 다이어그램](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리
Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.  다음 샘플 코드 hello tooquery Azure Cosmos DB에서 설명 하는 방법을 SQL 구문을 사용 하 여 hello로 [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) 메서드.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기
Azure Cosmos DB 지원 hello를 사용 하 여 업데이트 JSON 문서 [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) 메서드.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>9단계: JSON 문서 삭제
마찬가지로, Azure Cosmos DB 지원 hello를 사용 하 여 JSON 문서를 삭제 하는 중 [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) 메서드.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>10 단계: hello 데이터베이스를 삭제 합니다.
삭제 만든 hello 데이터베이스 hello 데이터베이스와 모든 자식 리소스 (컬렉션, 문서 등)를 제거합니다.

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>11단계: Java 콘솔 응용 프로그램 모두 함께 실행
hello 콘솔에서 toorun hello 응용 프로그램 toohello 프로젝트 폴더와 컴파일 Maven을 사용 하 여 이동 합니다.
    
    mvn package

실행 `mvn package` Maven에서 hello 최신 Azure Cosmos DB 라이브러리를 다운로드 하 고 생성 `GetStarted-0.0.1-SNAPSHOT.jar`합니다. 그런 다음 실행 하 여 hello 앱을 실행 합니다.

    mvn exec:java -D exec.mainClass=GetStarted.Program

축하합니다. 이 NoSQL 자습서를 완료했으며 실행되는 Java 콘솔 응용 프로그램이 생겼습니다.

## <a name="next-steps"></a>다음 단계
* Java 웹앱 자습서가 필요한가요? [Azure Cosmos DB를 사용하여 Java로 웹 응용 프로그램 빌드](documentdb-java-application.md)를 참조하세요.
* 너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정을 모니터링](monitor-accounts.md)합니다.
* Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.
* Hello hello의 개발 섹션에서에서 hello 프로그래밍 모델에 대 한 자세한 [Azure Cosmos DB 설명서 페이지](https://azure.microsoft.com/documentation/services/documentdb/)합니다.

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
