---
title: "Azure Cosmos DB: Java 사용 하 여 콘솔 응용 프로그램을 빌드하고 MongoDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용할 수는 Java 코드 샘플 hello Azure Cosmos DB MongoDB API를 표시."
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
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java와 함께 MongoDB API 콘솔 응용 프로그램을 빌드하고 hello Azure 포털

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다. 그런 다음 빌드하고 hello를 기반으로 하는 콘솔 응용 프로그램 배포 [MongoDB Java 드라이버](https://docs.mongodb.com/ecosystem/drivers/java/)합니다. 

## <a name="prerequisites"></a>필수 조건

* 이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.
   * JDK 1.7+(JDK가 없는 경우 `apt-get install default-jdk` 실행)
   * Maven(Maven이 없는 경우 `apt-get install maven` 실행)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>컬렉션 추가

새 사용자 데이터베이스 이름을 **db**로 지정하고 새로운 컬렉션 이름을 **coll**로 지정합니다.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 github에서 복제는 MongoDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. 그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello `Program.cs` 파일을 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스를 찾을 수 있습니다. 

* hello DocumentClient 초기화 됩니다.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* 새 데이터베이스 및 컬렉션이 만들어집니다.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* `MongoCollection.insertOne`을 사용하여 일부 문서가 삽입됩니다.

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* `MongoCollection.find`을 사용하여 일부 쿼리가 수행됩니다.

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Hello 계정에서에서 선택 **빠른 시작**, Java을 선택 하 고 hello 연결 문자열 tooyour 클립보드에 복사

2. 열기 hello `Program.java` 파일, hello 인수 toohello MongoClientURI 생성자 hello 연결 문자열로 대체 합니다. 이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 
    
## <a name="run-hello-console-app"></a>Hello 콘솔 앱 실행

1. 실행 `mvn package` 터미널 tooinstall에 필수 npm 모듈

2. 실행 `mvn exec:java -D exec.mainClass=GetStarted.Program` 터미널 toostart에서 Java 응용 프로그램입니다.

이제 사용할 수 있습니다 [Robomongo](mongodb-robomongo.md) / [Studio 3t 이상](mongodb-mongochef.md) tooquery, 수정 하 고이 새 데이터를 사용 합니다.

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 하 고 콘솔 응용 프로그램을 실행 하는 방법 배웠습니다. 이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB로 MongoDB 데이터 가져오기](mongodb-migrate.md)


