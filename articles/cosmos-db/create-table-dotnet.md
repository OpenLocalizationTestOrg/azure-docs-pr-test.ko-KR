---
title: "사용 하 여 Azure Cosmos DB.NET 응용 프로그램 aaaBuild 테이블 API hello | Microsoft Docs"
description: ".NET을 사용하여 Azure Cosmos DB의 Table API 시작"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a>Azure Cosmos DB: hello 테이블 API를 사용 하 여.NET 응용 프로그램 빌드

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작에서는 방법을 toocreate Azure Cosmos DB 계정을 한 hello Azure 포털을 사용 하 여 해당 계정 내에서 테이블을 만듭니다. 그런 다음 코드 tooinsert, update 및 delete 엔터티를 작성 하 고 새 hello를 사용 하 여 일부 쿼리를 실행 합니다 [Windows Azure 저장소 프리미엄 테이블](https://aka.ms/premiumtablenuget) 에서 NuGet 패키지 (미리 보기). 이 라이브러리에 hello 동일한 클래스와 메서드 시그니처에 hello 공용으로 [Windows Azure 저장소 SDK](https://www.nuget.org/packages/WindowsAzure.Storage), 하지만 또한 hello를 사용 하 여 hello 기능 tooconnect tooAzure Cosmos DB 계정을 [테이블 API](table-introduction.md) (미리 보기). 

## <a name="prerequisites"></a>필수 조건

설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다. 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>테이블 추가

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>샘플 데이터 추가

이제 데이터 탐색기 (미리 보기)를 사용 하 여 데이터 tooyour 새 테이블을 추가할 수 있습니다.

1. 데이터 탐색기에서 **sample-table**, **엔터티**를 클릭한 다음 **엔터티 추가**를 클릭합니다.

   ![Hello Azure 포털에서에서 데이터 탐색기에서 새 엔터티 만들기](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. 이제 데이터 toohello PartitionKey 값 상자 및 RowKey 값 상자에 추가 하 고 클릭 **엔터티 추가**합니다.

   ![설정 hello 파티션 키와 새 엔터티의 행 키](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    있습니다 수 이제 더 많은 엔터티 tooyour 테이블 추가, 엔터티를 편집 하거나 데이터 탐색기에서 데이터를 쿼리 합니다. 데이터 탐색기 처리량의 크기를 조정 하 고 저장된 프로시저, 사용자 정의 함수 및 트리거 tooyour 테이블을 추가할 수 있는 이기도 합니다.

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 보겠습니다 테이블 앱 github hello 연결 문자열을 설정 하 고 실행을 복제 합니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. 그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello Program.cs 파일을 찾을 수입니다. 

* hello CloudTableClient 초기화 됩니다.

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* 새 테이블이 존재하지 않는 경우 만들어집니다.

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* 새 테이블 컨테이너가 만들어집니다. 이 코드와 매우 유사 tooregular Azure 테이블 저장소 SDK 확인할 수 있습니다. 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 앱 tooAzure Cosmos DB 서로 연결할 수 있도록 hello 연결 문자열 정보 업데이트. 

1. Visual Studio에서 hello app.config 파일을 엽니다. 

2. Hello에 [Azure 포털](http://portal.azure.com/)hello에 Azure Cosmos DB 왼쪽 탐색 메뉴를 마우스 오른쪽 클릭 **연결 문자열**합니다. 그런 다음 hello 새 창에서 hello 연결 문자열에 대 한 hello 복사 단추를 클릭 합니다. 

    ![표시 및 연결 문자열 창 hello hello 끝점 및 계정 키를 복사](./media/create-table-dotnet/keys.png)

3. Hello PremiumStorageConnectionString의 hello 값으로 hello 값을 hello app.config 파일에 붙여 넣습니다. 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    Hello StandardStorageConnectionString 그대로 둘 수 있습니다.

이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 

## <a name="run-hello-web-app"></a>Hello 웹 앱 실행

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **PremiumTableGetStarted** 프로젝트에서 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다. 

2. Hello NuGet에서에서 **찾아보기** 상자에서 입력 *WindowsAzure.Storage PremiumTable*합니다.

3. Hello 확인 **시험판 포함** 상자입니다. 

4. Hello 결과 통해 설치 hello **WindowsAzure.Storage PremiumTable** 라이브러리입니다. 모든 종속성 뿐 아니라 hello 미리 보기 패키지 Azure Cosmos DB 테이블 API가 설치 됩니다. Azure 테이블 저장소에서 사용 하는 hello Windows Azure 저장소 패키지 보다 다른 NuGet 패키지 인지 note 합니다. 

5. CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.

    hello 콘솔 창에는 추가, 검색, 쿼리, 대체 및 중인 hello 테이블에서 삭제 된 hello 데이터가 표시 됩니다. Hello 스크립트가 완료 되 면 아무 키 tooclose hello 콘솔 창 키를 누릅니다. 
    
    ![Hello 빠른 시작의 콘솔 출력](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. Hello toosee 정당한 주석 줄 188 208 삭제 되지 않습니다 있으므로 program.cs에 있는 데이터 탐색기에서 새 엔터티를 원하는 경우 다음 hello 샘플 다시 실행 합니다. 

    이제 다시 할 수 있습니다 tooData 탐색기 클릭 **새로 고침**, hello 확장 **사람** 테이블 마우스 클릭 **엔터티**, 한 다음이 새 데이터를 사용 합니다. 

    ![데이터 탐색기의 새 엔터티](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제: 

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 toocreate Azure Cosmos DB 계정 hello 데이터 탐색기를 사용 하 여 테이블을 만듭니다 하 고 응용 프로그램을 실행 하는 방법을 배웠습니다.  이제 hello 테이블 API를 사용 하 여 데이터를 쿼리할 수 있습니다.  

> [!div class="nextstepaction"]
> [Hello 테이블 API를 사용 하 여 쿼리](tutorial-query-table.md)

