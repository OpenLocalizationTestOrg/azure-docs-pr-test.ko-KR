---
title: "Java 사용 하 여 Azure Cosmos DB 그래프 데이터베이스 aaaCreate | Microsoft Docs"
description: "Java Gremlin를 사용 하 여 Azure Cosmos DB에서 tooconnect tooand 쿼리 그래프 데이터를 사용 하는 샘플 코드를 표시 합니다."
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
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java를 사용 하 여 그래프 데이터베이스를 만들고 Azure 포털 hello

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작으로 그래프를 만듭니다 포털 Azure tools for Azure Cosmos DB hello 사용 하 여 데이터베이스입니다. 이 퀵 스타트의 표시 tooquickly hello OS를 사용 하 여 그래프 데이터베이스를 사용 하 여 Java 콘솔 응용 프로그램을 만드는 방법을 [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) 드라이버입니다. 이 빠른 시작의 hello 지침 Java 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다. 이 빠른 시작을 작성 하 고 수정 hello UI 또는 프로그래밍 방식으로, 기본 설정을 중 더 작은 값의 그래프 리소스를 살펴봅니다. 

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

그래프 데이터베이스를 만들 수 있습니다, 전에 toocreate Gremlin (그래프) 데이터베이스 계정을 Azure Cosmos DB와 함께 필요 합니다.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>그래프 추가

이제 Azure 포털 toocreate 그래프 데이터베이스 hello에 hello 데이터 탐색기 도구를 사용할 수 있습니다. 

1. Hello hello 왼쪽된 탐색 메뉴에서 Azure 포털에서에서 클릭 **데이터 탐색기 (미리 보기)**합니다. 
2. Hello에 **데이터 탐색기 (미리 보기)** 블레이드에서 클릭 **새 그래프**, hello 다음 정보를 사용 하 여 hello 페이지를 채웁니다.

    ![Hello Azure 포털에서에서 데이터 탐색기](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    설정|제안 값|설명
    ---|---|---
    데이터베이스 ID|sample-database|새 데이터베이스에 대 한 hello ID입니다. 데이터베이스 이름은 1~255자 사이여야 하며 `/ \ # ?` 또는 후행 공백을 포함할 수 없습니다.
    그래프 ID|sample-graph|새 그래프에 대 한 hello ID입니다. 그래프 이름에는 hello 요구 사항 데이터베이스 id로 문자 동일 합니다.
    저장소 용량| 10 GB|Hello 기본값을 그대로 둡니다. 이 hello 데이터베이스의 저장 용량 hello입니다.
    처리량|400RU|Hello 기본값을 그대로 둡니다. 확장할 수 있습니다 hello 처리량 나중 tooreduce 대기 시간 하려는 경우.
    파티션 키|비워 둠|이 빠른 시작의 hello 용도로 hello 파티션 키를 비워 둡니다.

3. Hello 양식에 입력, 클릭 **확인**합니다.

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 보겠습니다 hello 연결 문자열을 설정 하 고 실행 github에서 그래프 응용 프로그램을 복제 합니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello `Program.java` hello \src\GetStarted 폴더에서 파일을 다음 코드이 줄을 찾습니다. 

* hello Gremlin `Client` hello 구성에서 초기화 `src/remote.yaml`합니다.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Hello를 사용 하 여 일련의 Gremlin 단계 실행 `client.submit` 메서드.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

1. 열기 hello src/remote.yaml 파일입니다. 

3. 입력 프로그램 *호스트*, *username*, 및 *암호* hello src/remote.yaml 파일의 값입니다. hello 설정 hello 나머지 toobe 변경할 필요는 없습니다.

    설정|제안 값|설명
    ---|---|---
    호스트|[***.graphs.azure.com]|Hello 스크린 샷을 다음이 표를 참조 하십시오. 이 값은 hello Gremlin URI 값 hello hello 후행 대괄호에서 Azure 포털의 hello 개요 페이지에서: 443 / 제거 합니다.<br><br>Https:// 제거한 문서 toographs 변경 hello 후행 제거 하 여 hello URI 값을 사용 하 여 hello 키 탭에서이 값을 검색할 수도 있습니다: 443 / 합니다.
    사용자 이름|/dbs/sample-database/colls/sample-graph|hello 폼의 리소스 hello `/dbs/<db>/colls/<coll>` 여기서 `<db>` 은 기존 데이터베이스 이름 및 `<coll>` 은 기존 컬렉션 이름입니다.
    암호|*기본 마스터 키*|Hello 두 번째 스크린 샷을 다음이 표를 참조 하십시오. 이 값은 사용자 기본 키를 hello hello 기본 키 상자에 Azure 포털의 hello 키 페이지에서 검색할 수 있습니다. Hello 값 hello 복사 단추를 사용 하 여 hello hello 상자 오른쪽에 복사 합니다.

    Hello 호스트 값에 대 한 hello 복사 **Gremlin URI** hello에서 값 **개요** 페이지. 가 비어 있으면 hello 호스트 행 hello hello 키 블레이드에서 hello Gremlin URI를 만드는 방법에 대해 테이블 앞에 있는 hello 지침을 참조 합니다.
![Hello Azure 포털에서에서 hello 개요 페이지에서 보기 및 복사 hello Gremlin URI 값](./media/create-graph-java/gremlin-uri.png)

    암호 값 hello에 대 한 hello 복사 **기본 키** hello에서 **키** 블레이드: ![hello Azure 포털에서에서 기본 키의 키 보기 및 복사 페이지](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Hello 콘솔 앱 실행

1. Hello git 터미널 창에서 `cd` toohello azure-cosmos-db-graph-java-getting-started 폴더입니다.

2. Hello git 터미널 창에서 입력 `mvn package` tooinstall hello Java 패키지가 필요 합니다.

3. Hello git 터미널 창에서 실행 `mvn exec:java -D exec.mainClass=GetStarted.Program` 에 hello 터미널 윈도우 toostart Java 응용 프로그램입니다.

hello 터미널 창 hello 꼭지점 toohello 그래프 추가 되 고 표시 됩니다. Hello 프로그램 완료 되 면 인터넷 브라우저에서 뒤로 toohello Azure 포털을 전환 합니다. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>샘플 데이터 검토 및 추가

이제 tooData 탐색기 이전 단계로 이동 하 고 hello 꼭지점 toohello 그래프를 추가 하 고 다른 데이터 요소를 추가 합니다. 확인할 수 있습니다.

1. 데이터 탐색기에서 hello **샘플 데이터베이스**/**샘플 그래프**, 클릭 **그래프**, 클릭 하 고 **필터 적용**. 

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 문서 만들기](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. Hello에 **결과** 목록에서 새 사용자 hello toohello 그래프를 추가 합니다. 선택 **ben** 그가 연결 toorobin 표시 되는지 확인 합니다. Hello 꼭지점 hello 그래프 탐색기 내에서 이동, 확대 / 축소 있고 hello 그래프 탐색기 화면의 hello 크기를 확장 합니다. 

   ![Hello Azure 포털에서에서 데이터 탐색기에서 hello 그래프에서 새 꼭지점](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Hello 데이터 탐색기를 사용 하 여 몇 가지 새로운 사용자가 toohello 그래프를 추가 해 보겠습니다. Hello 클릭 **새 꼭지점** 단추 tooadd 데이터 tooyour 그래프입니다.

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 문서 만들기](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. 레이블을 입력 *사람* hello 다음 키를 toocreate hello 첫 번째 꼭 짓 점 hello 그래프에서 값을 입력 합니다. 그래프의 각 person에 대해 고유한 속성을 만들 수 있습니다. 만 hello id 키가 필요 합니다.

    key|값|메모
    ----|----|----
    id|ashley|hello hello 꼭지점에 대 한 고유 식별자입니다. ID를 지정하지 않으면 사용자에 대해 하나 생성됩니다.
    gender|female| 
    tech | java | 

    > [!NOTE]
    > 이 빠른 시작에서는 파티션되지 않은 컬렉션을 만듭니다. 그러나 hello 컬렉션 생성 하는 동안 파티션 키를 지정 하 여 분할 된 컬렉션을 만들면 다음 해야 tooinclude hello 파티션 키에서 각 새 꼭지점 키로 합니다. 

5. **확인**을 클릭합니다. 화면 toosee tooexpand를 할 수 있습니다 **확인** hello hello 화면 아래쪽에 있습니다.

6. **새 꼭짓점**을 다시 클릭하고 새로운 추가 사용자를 추가합니다. 레이블을 입력 *사람* hello 다음을 입력 한 다음 키와 값:

    key|값|메모
    ----|----|----
    id|rakesh|hello hello 꼭지점에 대 한 고유 식별자입니다. ID를 지정하지 않으면 사용자에 대해 하나 생성됩니다.
    gender|male| 
    school|MIT| 

7. **확인**을 클릭합니다. 

8. 클릭 **필터 적용** 이며 기본값은 hello `g.V()` 필터입니다. 이제 모든 hello 사용자 hello에 표시 **결과** 목록입니다. 더 많은 데이터를 추가 하면 결과 필터 toolimit를 사용할 수 있습니다. 기본적으로 데이터 탐색기 사용 `g.V()` tooretrieve는 그래프에 있는 모든 꼭 짓 점에 해당 tooa 다른 변경할 수 [그래프 쿼리](tutorial-query-graph.md)와 같은 `g.V().count()`, tooreturn JSON 형식의 hello 그래프의 모든 hello 꼭 짓 점 개수입니다.

9. 이제 rakesh 및 ashley를 연결할 수 있습니다. 확인 **일부 터** hello에서 선택한 **결과** 다음 너무 hello 편집 단추를 클릭 한 다음 목록**대상** 오른쪽 아래에 있습니다. 창 toosee hello toowiden를 할 수 있습니다 **속성** 영역입니다.

   ![그래프의 한 꼭 짓 점에 hello 대상 변경](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. Hello에 **대상** 상자에 입력 *rakesh*, 및 hello **가장자리 레이블** 상자에 입력 *알고*, hello 확인란을 클릭 하 고 합니다.

   ![데이터 탐색기에서 ashley와 rakesh 사이의 연결을 추가합니다.](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. 이제 템플릿을 선택할 **rakesh** hello 결과 목록에서 단위 및 rakesh 연결 되어 있는지를 참조 하십시오. 

   ![데이터 탐색기에서 연결된 두 꼭짓점](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    데이터 탐색기 toocreate 저장 프로시저, Udf 및 트리거 tooperform 서버 쪽 비즈니스 논리도을 사용할 수도 있습니다 눈금 처리량으로 합니다. 데이터 탐색기의 hello 프로그래밍 방식으로 기본 제공 데이터 액세스 Api, hello에서 사용할 수 있는 모든 아니라 hello Azure 포털에에서 쉽게 액세스할 수 있도록 tooyour 데이터를 제공 합니다.



## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제: 

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 그래프를 만듭니다 하 고 응용 프로그램을 실행 하는 방법 배웠습니다. 이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다. 

> [!div class="nextstepaction"]
> [Gremlin을 사용하여 쿼리](tutorial-query-graph.md)

