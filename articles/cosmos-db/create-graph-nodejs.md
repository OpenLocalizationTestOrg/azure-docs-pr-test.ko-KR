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
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Graph API를 사용하여 Node.js 응용 프로그램 빌드

Cosmos DB azure는 Microsoft에서 전역으로 분산 하는 hello 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 문서 hello Azure 포털을 사용 하 여 Azure Cosmos DB toocreate Graph API (미리 보기), 데이터베이스 및 그래프에 대 한 고려 하는 방법을 보여줍니다. 그런 다음 빌드 및 실행 하 여 콘솔 응용 프로그램 hello 오픈 소스를 사용 하 여 [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) 드라이버입니다.  

> [!NOTE]
> hello npm 모듈 `gremlin-secure` 의 수정된 된 버전은 `gremlin` SSL 및 Azure Cosmos DB를 사용 하 여 연결 하는 데 필요한 SASL 지 원하는 모듈입니다. 소스 코드는 [GitHub](https://github.com/CosmosDB/gremlin-javascript)에서 사용할 수 있습니다.
>

## <a name="prerequisites"></a>필수 조건

이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.
* [Node.js](https://nodejs.org/en/) 버전 v0.10.29 이상
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>그래프 추가

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 GitHub에서 복제는 Graph API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: Git Bash Git 터미널 윈도우를 열고 변경 (통해 `cd` 명령) tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Visual Studio에서 hello 솔루션 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello `app.js` 파일과 있습니다 hello 다음 줄의 코드를 찾을 수 있습니다. 

* hello Gremlin 클라이언트가 만들어집니다.

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

  hello 구성은 모두 `config.js`는 hello 다음 섹션에서에서 편집 합니다.

* Hello로 실행 되는 일련의 Gremlin 단계 `client.execute` 메서드.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

1. 열기 hello config.js 파일입니다. 

2. Config.js의 hello로 hello config.endpoint 키를 입력 **Gremlin URI** hello에서 값 **개요** hello Azure 포털의 페이지입니다. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-graph-nodejs/gremlin-uri.png)

   경우 hello **Gremlin URI** hello에서 hello 값을 생성할 수 있습니다, 값이 비어 **키** hello를 사용 하 여 hello 포털에서 페이지 **URI** 값, https://, 제거 및 변경 toographs 설명합니다.

   hello Gremlin 끝점만 hello 호스트 이름 이어야 hello 프로토콜/포트 번호 없이 같은 `mygraphdb.graphs.azure.com` (하지 `https://mygraphdb.graphs.azure.com` 또는 `mygraphdb.graphs.azure.com:433`).

3. Config.js에서 hello 사용 하 여 hello config.primaryKey 값을 입력 **기본 키** hello에서 값 **키** hello Azure 포털의 페이지입니다. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Azure 포털 키 블레이드 hello](./media/create-graph-nodejs/keys.png)

4. Hello 데이터베이스 이름과 config.database 및 config.collection hello 값에 대 한 그래프 (컨테이너) 이름을 입력 합니다. 

완성된 config.js 파일은 다음과 같은 모양입니다.

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Hello 콘솔 앱 실행

1. 터미널 윈도우를 열고 변경 (통해 `cd` 명령) hello 프로젝트에 포함 된 hello package.json 파일에 대 한 toohello 설치 디렉터리입니다.  

2. 실행 `npm install` tooinstall hello npm 모듈을 포함 하는 데 필요한 `gremlin-secure`합니다.

3. 실행 `node app.js` 터미널 toostart에 응용 프로그램 노드.

## <a name="browse-with-data-explorer"></a>데이터 탐색기 검색

이제 Azure 포털 tooview hello에 탐색기 tooData 돌아가서, 쿼리, 수정 하 고 수 작업 하는 새 그래프 데이터입니다.

데이터 탐색기에서 새 데이터베이스 hello hello에 나타납니다 **그래프** 창. Hello 컬렉션 hello 데이터베이스를 확장 한 다음 클릭 **그래프**합니다.

hello hello 샘플 응용 프로그램에 의해 생성 된 데이터는 hello 내에서 다음 창 hello **그래프** 를 클릭할 때 탭 **필터 적용**합니다.

완료 시도 `g.V()` 와 `.has('firstName', 'Thomas')` tootest hello 필터입니다. Hello 값은 대/소문자 구분 note 마십시오.

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>리소스 정리

이 앱을 사용 하 여 toocontinue 하지 않으려는 경우 hello 다음을 수행 하 여이 문서에서 만든 모든 리소스를 삭제 합니다. 

1. Hello hello 왼쪽된 탐색 메뉴에서 Azure 포털에서에서 클릭 **리소스 그룹**, 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 리소스 toobe 삭제의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 Azure Cosmos DB 계정 toocreate 데이터 탐색기를 사용 하 여 그래프를 만듭니다 하 고 응용 프로그램을 실행 하는 방법 배웠습니다. 이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다. 

> [!div class="nextstepaction"]
> [Gremlin을 사용하여 쿼리](tutorial-query-graph.md)
