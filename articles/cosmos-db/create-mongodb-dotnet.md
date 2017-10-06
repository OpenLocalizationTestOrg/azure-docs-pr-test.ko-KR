---
title: "Azure Cosmos DB:.net 웹 앱을 빌드하고 MongoDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하면.NET 코드 예제는 hello Azure Cosmos DB MongoDB API를 표시."
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB:.net MongoDB API 웹 앱을 빌드하고 hello Azure 포털

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다. 그런 다음 빌드하고 hello에 작성 하는 작업 목록 웹 앱을 배포할 [MongoDB.NET 드라이버](https://docs.mongodb.com/ecosystem/drivers/csharp/)합니다. 

## <a name="prerequisites"></a>필수 조건

설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다. 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 github에서 복제는 MongoDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. 그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello **Dal.cs** hello 파일 **DAL** directory를 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스를 찾을 수 있습니다. 

* Hello Mongo 클라이언트를 초기화 합니다.

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* Hello 데이터베이스 및 hello 컬렉션을 검색 합니다.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* 모든 문서를 검색합니다.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **연결 문자열**, 클릭 하 고 **읽기-쓰기 키**합니다. Hello 다음 단계에서 hello Dal.cs 파일로 hello hello 화면 toocopy hello 사용자 이름 오른쪽에 hello 복사 단추, 암호 및 호스트를 사용 합니다.

2. 열기 hello **Dal.cs** hello에 대 한 파일 **DAL** 디렉터리입니다. 

3. 복사 프로그램 **사용자 이름** hello 포털 (hello 복사 단추 사용)에서 값을 하 게 hello 값 hello **사용자 이름** 에 프로그램 **Dal.cs** 파일입니다. 

4. 다음 복사 프로그램 **호스트** hello 포털에서 값을 하 게 hello 값 hello **호스트** 에 프로그램 **Dal.cs** 파일입니다. 

5. 마지막 복사 프로그램 **암호** hello 포털에서 값을 하 게 hello 값 hello **암호** 에 프로그램 **Dal.cs** 파일입니다. 

이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 
    
## <a name="run-hello-web-app"></a>Hello 웹 앱 실행

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다. 

2. Hello NuGet에서에서 **찾아보기** 상자에서 입력 *MongoDB.Driver*합니다.

3. Hello 결과 통해 설치 hello **MongoDB.Driver** 라이브러리입니다. Hello MongoDB.Driver 패키지 뿐만 아니라 모든 종속성을 설치합니다.

4. CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다. 앱이 브라우저에 표시됩니다. 

5. 클릭 **만들기** 에 브라우저 hello 하 고 작업 목록 앱에서 몇 가지 새 작업을 만듭니다.

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 퀵 스타트의 어떻게 toocreate Azure Cosmos DB 계정 및 사용 하 여 웹 응용 프로그램 실행 hello API MongoDB에 대 한 배웠습니다. 이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다. 

> [!div class="nextstepaction"]
> [Hello MongoDB API에 대 한 Azure Cosmos DB로 데이터 가져오기](mongodb-migrate.md)

