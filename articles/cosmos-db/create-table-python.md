---
title: "빠른 시작: 테이블 API와 Python - Azure Cosmos DB | Microsoft Docs"
description: "이 빠른 시작은 Azure Portal 및 Python과 함께 Azure Cosmos DB 테이블 API를 사용하여 응용 프로그램을 만드는 방법을 보여 줍니다."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: quickstart
ms.date: 11/16/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 56c52aef2dda899a7f7ce90a26068897781773da
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="quickstart-build-a-table-api-app-with-python-and-azure-cosmos-db"></a>빠른 시작: Python 및 Azure Cosmos DB를 사용하여 테이블 API 응용 프로그램 빌드

이 빠른 시작은 GitHub에서 예제를 복제하여 앱을 빌드하기 위해 Python과 Azure Cosmos DB [테이블 API](table-introduction.md)를 사용하는 방법을 보여 줍니다. 또한 Azure Cosmos DB 계정을 만드는 방법 및 데이터 탐색기를 사용하여 웹 기반 Azure Portal에 테이블과 엔터티를 만드는 방법도 보여줍니다.

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. Azure Cosmos DB의 핵심인 전역 배포 및 수평 크기 조정 기능의 이점을 모두 활용하여 문서, 키/값, 전체 열 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

또한,

* Visual Studio 2017이 아직 설치되지 않은 경우 **체험판** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)을 다운로드하고 사용할 수 있습니다. Visual Studio를 설정하는 동안 **Azure 개발**을 사용할 수 있는지 확인합니다.
* [GitHub](http://microsoft.github.io/PTVS/)에서 Visual Studio용 Python 도구. 이 자습서에서는 Python Tools for VS 2015를 사용합니다.
* [python.org](https://www.python.org/downloads/release/python-2712/)의 Python 2.7

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

> [!IMPORTANT] 
> 일반 공급 Table API SDK를 사용하려면 새 Table API 계정을 만들어야 합니다. 미리 보기 중에 만들어진 Table API 계정은 일반 공급 SDK에서 지원되지 않습니다.
>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>테이블 추가

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>샘플 데이터 추가

이제 데이터 탐색기를 사용하여 새 테이블에 데이터를 추가할 수 있습니다.

1. 데이터 탐색기에서 **sample-table**, **엔터티**를 클릭한 다음 **엔터티 추가**를 클릭합니다.

   ![Azure Portal의 데이터 탐색기에서 새 엔터티 만들기](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. 이제 PartitionKey 값 상자 및 RowKey 값 상자에 데이터를 추가하고 **엔터티 추가**를 클릭합니다.

   ![새 엔터티에 대한 분할 키와 행 키 설정](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    이제 테이블에 더 많은 엔터티를 추가하고 엔터티를 편집하거나 데이터 탐색기에서 데이터를 쿼리할 수 있습니다. 데이터 탐색기에서는 처리량을 확장하고 테이블에 저장된 프로시저, 사용자 정의 함수 및 트리거를 추가할 수 있습니다.

## <a name="clone-the-sample-application"></a>샘플 응용 프로그램 복제

이제 github에서 Table 앱을 복제하고 연결 문자열을 설정한 다음 실행해 보겠습니다. 프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다. 

1. Git Bash와 같은 Git 터미널 창을 열고, `cd` 명령을 사용하여 샘플 앱을 설치할 폴더를 변경합니다. 

    ```bash
    cd "C:\git-samples"
    ```

2. 다음 명령을 실행하여 샘플 리포지토리를 복제합니다. 이 명령은 컴퓨터에서 샘플 앱의 복사본을 만듭니다. 

    ```bash
    git clone https://github.com/Azure-Samples/storage-python-getting-started.git
    ```

3. 그런 다음 Visual Studio에서 솔루션을 엽니다. 

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 Azure Portal로 다시 이동하여 연결 문자열 정보를 가져와서 앱에 복사합니다. 이를 통해 앱이 호스팅된 데이터베이스와 통신할 수 있게 됩니다. 

1. [Azure Portal](http://portal.azure.com/)에서 **연결 문자열**을 클릭합니다. 

    ![연결 문자열 창에서 연결 문자열 보기 및 복사](./media/create-table-python/connection-string.png)

2. 오른쪽에 있는 단추를 사용하여 계정 이름을 복사합니다.

3. config.py 파일을 열고 포털의 계정 이름을 19번째 줄의 STORAGE_ACCOUNT_NAME 값에 붙여넣습니다.

4. 포털로 돌아가서 기본 키를 복사합니다.

5. 포털의 기본 키를 20번째 줄의 STORAGE_ACCOUNT_KEY 값에 붙여넣습니다.

3. config.py 파일을 저장합니다.

## <a name="run-the-app"></a>앱 실행

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 현재 Python 환경을 선택한 후 마우스 오른쪽 단추로 클릭합니다.

2. Python 패키지 설치를 선택하고 **azure-storage-table**에 입력합니다.

3. F5를 눌러 응용 프로그램을 실행합니다. 앱이 브라우저에 표시됩니다. 

이제 데이터 탐색기로 돌아가서 이 새 데이터를 쿼리 및 수정하고 작업에 사용할 수 있습니다. 

## <a name="review-slas-in-the-azure-portal"></a>Azure Portal에서 SLA 검토

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 테이블을 만들고, 앱을 실행하는 방법을 알아보았습니다.  이제 테이블 API를 사용하여 데이터를 쿼리할 수 있습니다.  

> [!div class="nextstepaction"]
> [Table API로 테이블 데이터 가져오기](table-import.md)
