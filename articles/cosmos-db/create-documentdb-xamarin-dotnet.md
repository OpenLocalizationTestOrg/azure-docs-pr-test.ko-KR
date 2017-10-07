---
title: "Azure Cosmos DB: Xamarin 및 Facebook 인증으로 웹앱 작성 | Microsoft Docs"
description: "Tooconnect tooand에서는.NET 코드 샘플은 Azure Cosmos DB 쿼리를 표시."
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: .NET, Xamarin 및 Facebook 인증으로 웹앱 작성

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다. 그런 다음 빌드 하 고 hello 기반으로 할 일 목록 웹 앱을 배포 합니다 [DocumentDB.NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), 연산자 및 hello Azure Cosmos DB 권한 부여 엔진입니다. hello 할 일 목록 웹 앱 Facebook 인증을 사용 하 여 사용자가 toologin 수 있도록 하는 사용자 단위 데이터 패턴을 구현 하 고 자신의 toodo 항목을 관리 합니다.

## <a name="prerequisites"></a>필수 조건

설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다. 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>컬렉션 추가

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 github에서 복제는 DocumentDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다. 얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다. 

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Visual Studio에서 hello samples/xamarin/UserItems/xamarin.forms 폴더에서 다음 hello DocumentDBTodo.sln 파일을 엽니다. 

## <a name="review-hello-code"></a>Hello 코드 검토

hello 코드 hello Xamarin 폴더에 포함 되어 있습니다.

* Xamarin 앱. hello 앱 UserItems 라는 분할 된 컬렉션에 hello 사용자의 할 일 항목을 저장 합니다.
* 리소스 토큰 broker API. 간단한 ASP.NET 웹 API toobroker Azure Cosmos DB 리소스 toohello hello 앱의 사용자는 로그인 토큰입니다. 리소스 토큰은 사용자의 데이터에 기록 하는 hello 액세스 toohello 함께 hello 응용 프로그램을 제공 하는 수명이 짧은 액세스 토큰입니다.

아래 hello 다이어그램 hello 인증 및 데이터 흐름을 보여 줍니다.

* hello UserItems 컬렉션 hello 파티션 키를 사용 하 여 만든 ' / userid'. 지정 된 컬렉션에 대 한 파티션 키 하면 Azure Cosmos DB tooscale 무한 hello 사용자와 항목 수로 증가 합니다.
* hello Xamarin 앱에 Facebook 자격 증명으로 사용자가 toologin을 수 있습니다.
* hello Xamarin 앱에서 Facebook 액세스 토큰 tooauthenticate ResourceTokenBroker API 사용
* hello 리소스 토큰 브로커 API 앱 서비스 인증 기능을 사용 하는 hello 요청을 인증 하 고 hello 인증 된 사용자의 파티션 키를 공유 하는 읽기/쓰기 액세스 tooall 문서와 함께 Azure Cosmos DB 리소스 토큰을 요청 합니다.
* 리소스 토큰 브로커 hello 리소스 토큰 toohello 클라이언트 응용 프로그램을 반환합니다.
* hello 앱 hello 리소스 토큰을 사용 하 여 hello 사용자의 할 일 항목에 액세스 합니다.

![샘플 데이터를 사용한 Todo 앱](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다. Hello 다음 단계에서 hello Web.config 파일로 hello 화면 toocopy hello URI의 hello 오른쪽에서 복사 단추 hello와 기본 키를 사용 합니다.

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-xamarin-dotnet/keys.png)

2. Visual Studio 2017에 hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker 폴더에 hello Web.config 파일을 엽니다. 

3. Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게 hello hello accountUrl web.config에서의 값입니다. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. 그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello hello accountKey Web.congif에서의 값입니다. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다. 

## <a name="build-and-deploy-hello-web-app"></a>빌드 및 hello 웹 응용 프로그램 배포

1. Hello Azure 포털, 한 앱 서비스 웹 사이트 toohost hello 리소스 토큰 브로커를 API를 만듭니다.
2. Azure 포털 hello에 hello 리소스 토큰 브로커 API 웹 사이트의 hello 응용 프로그램 설정 블레이드를 엽니다. 앱 설정에 따라 hello를 입력 합니다.

    * accountUrl-hello Azure Cosmos DB 계정 키 탭에서 hello Azure Cosmos DB 계정 URL입니다.
    * accountKey-Azure Cosmos DB 계정 키 탭 hello에서에서 hello Azure Cosmos DB 계정 마스터 키입니다.
    * 사용자가 만든 데이터베이스와 컬렉션의 databaseId 및 collectionId

3. Hello ResourceTokenBroker 솔루션 tooyour 만든 웹 사이트를 게시 합니다.

4. Hello Xamarin 프로젝트를 열고 tooTodoItemManager.cs 이동 합니다. Hello 리소스 토큰 브로커 웹 사이트에 대 한 hello 기본 https url로 resourceTokenBrokerURL 뿐만 아니라 accountURL, collectionId, databaseId에 대 한 hello 값을 입력 합니다.

5. 전체 hello [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Facebook 로그인](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) 자습서 toosetup Facebook 인증 hello ResourceTokenBroker 웹 사이트 및 구성 합니다.

    Hello Xamarin 앱을 실행 합니다.

## <a name="review-slas-in-hello-azure-portal"></a>Sla hello Azure 포털에서에서 검토 하 고

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제: 

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 다음 방금 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 toocreate Azure Cosmos DB 계정을 hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 및 빌드 및 Xamarin 앱을 배포 방법을 배웠습니다. 이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB로 데이터 가져오기](import-data.md)
