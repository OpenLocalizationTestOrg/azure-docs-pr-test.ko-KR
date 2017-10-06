---
title: "Azure Cosmos DB: Python 사용 하 여 앱을 빌드하고 DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하면 Python 코드 샘플은 hello Azure Cosmos DB DocumentDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Azure Cosmos DB: python DocumentDB API 앱을 빌드하고 hello Azure 포털

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다. 그런 다음 작성 하 고 hello를 기반으로 하 여 콘솔 응용 프로그램을 실행할 [DocumentDB Python API](documentdb-sdk-python.md)합니다.

## <a name="prerequisites"></a>필수 조건

* 이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.
    * [Visual Studio 2015](http://www.visualstudio.com/) 이상.
    * [GitHub](http://microsoft.github.io/PTVS/)에서 Visual Studio용 Python 도구. 이 자습서에서는 Python Tools for VS 2015를 사용합니다.
    * [python.org](https://www.python.org/downloads/release/python-2712/)의 Python 2.7

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>컬렉션 추가

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 github에서 복제는 DocumentDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello DocumentDBGetStarted.py 파일을 찾을 수입니다. 


* hello DocumentClient 초기화 됩니다.

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* 새 데이터베이스가 만들어집니다.

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* 새 컬렉션이 만들어집니다.

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* 일부 문서가 만들어집니다.

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* SQL을 사용하여 쿼리가 수행됩니다.

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다. Hello에 hello 화면 toocopy hello URI의 오른쪽 hello와 기본 키에서 hello 복사 단추를 사용 한다고 `DocumentDBGetStarted.py` hello 다음 단계에는 파일입니다.

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. 열린 hello `DocumentDBGetStarted.py` 파일입니다. 

3. Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게에 hello 끝점 키의 값을 hello `DocumentDBGetStarted.py`합니다. 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. 그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello 값 hello `config.MASTERKEY` 에서 `DocumentDBGetStarted.py`합니다. 이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>Hello 앱 실행
1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기**현재 Python 환경 hello를 선택한 다음 마우스 오른쪽 단추로 클릭 합니다.

2. Python 패키지 설치를 선택하고 **pydocumentdb**를 입력합니다.

3. F5 toorun hello 응용 프로그램을 실행 합니다. 앱이 브라우저에 표시됩니다. 

이제 다시 tooData 탐색기 및 쿼리를 참조, 수정 돌아가서이 새 데이터를 사용 합니다. 

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 하 고 응용 프로그램을 실행 하는 방법 배웠습니다. 이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다. 

> [!div class="nextstepaction"]
> [DocumentDB API hello에 대 한 Azure Cosmos DB로 데이터 가져오기](import-data.md)


