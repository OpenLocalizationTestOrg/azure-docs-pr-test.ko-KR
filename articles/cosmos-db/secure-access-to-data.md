---
title: "aaaLearn toosecure toodata Azure Cosmos DB에서 액세스 하는 방법 | Microsoft Docs"
description: "마스터 키, 읽기 전용 키, 사용자 및 권한을 포함해서 Azure Cosmos DB의 액세스 제어 개념에 대해 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>액세스 tooAzure Cosmos DB 데이터 보안
이 문서에 저장 된 액세스 toodata 보안 설정의 개요를 제공 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)합니다.

Azure Cosmos DB는 두 가지 유형의 키 tooauthenticate 사용자를 사용 하 여 및 tooits 데이터 액세스와 리소스를 제공 합니다. 

|키 유형|리소스|
|---|---|
|[마스터 키](#master-keys) |데이터베이스 계정, 데이터베이스, 사용자, 사용 권한을 비롯한 관리 리소스에 사용됩니다.|
|[리소스 토큰](#resource-tokens)|컬렉션, 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF를 비롯한 응용 프로그램 리소스에 사용됩니다.|

<a id="master-keys"></a>

## <a name="master-keys"></a>마스터 키 

마스터 키 hello 데이터베이스 계정에 대 한 액세스 toohello hello 관리 리소스를 모두 제공합니다. 마스터 키:  
- 액세스 tooaccounts, 데이터베이스, 사용자 및 사용 권한을 제공 합니다. 
- 사용 되는 tooprovide 세부적인 액세스 toocollections 및 문서 수 없습니다.
- Hello 계정 만드는 동안 생성 됩니다.
- 언제든지 다시 생성할 수 있습니다.

각 계정은 두 개의 마스터 키(주 키와 보조 키)로 구성됩니다. hello 이중 키의 목적은 다시 생성 하거나 연속 액세스 tooyour 계정 및 데이터를 제공 합니다. 키를 롤포워드할 수 있도록 합니다. 

Hello Cosmos DB 계정에 대 한 추가 toohello 두 마스터 키에 두 개의 읽기 전용 키가 있습니다. 이러한 읽기 전용 키를 사용 하 여 hello 계정에 읽기 작업만 허용 합니다. 읽기 전용 키 액세스 tooread 사용 권한 리소스 제공 하지 않습니다.

주, 보조 읽기 전용 및 읽기 / 쓰기 마스터 키를 검색할 수 hello Azure 포털을 사용 하 여 다시 합니다. 자세한 내용은 [액세스 키 보기, 복사 및 다시 생성](manage-account.md#keys)을 참조하세요.

![Hello NoSQL 데이터베이스 보안을 보여 주는-Azure 포털에서에서 액세스 제어 (IAM)](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

마스터 키 순환의 hello 과정은 간단 합니다. Azure 포털 tooretrieve toohello 사용자의 보조 키를 이동 하 한 다음 기본 키를 응용 프로그램의 보조 키로 대체 한 다음 hello hello Azure 포털의에서 기본 키를 회전 합니다.

![Azure 포털-NoSQL 데이터베이스 보안을 보여 주는 hello에 마스터 키 회전](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>코드 샘플 toouse 마스터 키

hello 다음 코드 예제에서는 어떻게 toouse Cosmos DB는 DocumentClient tooinstantiate 끝점 및 마스터 키를 계정 하 고 데이터베이스를 만듭니다. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>리소스 토큰

리소스 토큰 toohello 응용 프로그램 리소스 데이터베이스 내에서 액세스를 제공합니다. 리소스 토큰:
- 액세스 toospecific 컬렉션, 파티션 키, 문서, 첨부 파일, 저장된 프로시저, 트리거 및 Udf를 제공 합니다.
- 될 때 생성 되는 [사용자](#users) 부여 [권한을](#permissions) tooa 특정 리소스입니다.
- POST, GET 또는 PUT 호출로 권한 리소스가 작동할 때 다시 생성됩니다.
- Hello 사용자, 리소스 및 사용 권한에 대 한 구체적으로 생성 된 해시 리소스 토큰을 사용 합니다.
- 시간은 사용자 지정 가능한 유효 기간으로 제한됩니다. hello 기본 유효한 timespan 1 시간입니다. 그러나 토큰 수명 지정할 수 있습니다. 명시적으로 tooa 최대 5 시간을 합니다.
- Hello 마스터 키 아웃 안전한 대체 toogiving를 제공 합니다. 
- 클라이언트 tooread, 쓰기 및 삭제 계정의 리소스에 hello Cosmos DB toohello 권한이 부여 된에 따라 사용 하도록 설정 합니다.

리소스 토큰을 사용 하 여 (만들어서 Cosmos DB 사용자 및 사용 권한) 하려는 경우 Cosmos db에서 tooprovide 액세스 tooresources 계정 tooa 클라이언트 hello 마스터 키로 신뢰할 수 없습니다.  

Cosmos DB 리소스 토큰이 클라이언트 tooread, 쓰기 및 삭제 리소스 중 하나는 마스터 필요 없이 및 toohello 사용 권한을 부여 하지에 따라 Cosmos DB 계정에 있도록 안전한 대체 방법을 제공 하거나만 키를 읽을 합니다.

다음은 그에 따라 리소스 토큰 수 수 요청, 생성 및 tooclients 배달 일반적인 디자인 패턴이입니다.

1. 중간 계층 서비스는 모바일 응용 프로그램 tooshare 사용자 사진 tooserve를 설정 합니다. 
2. hello 중간 계층 서비스는 hello Cosmos DB 계정의 hello 마스터 키를가지고 있습니다.
3. hello 사진 앱은 최종 사용자의 모바일 장치에 설치 됩니다. 
4. 로그인에 hello 사진 앱 hello 사용자 hello 중간 계층 서비스와의 hello id를 설정 합니다. 이 메커니즘 identity 설정의 toohello 응용 프로그램을 순수 하 게은입니다.
5. Hello id가 설정 되 면 hello 중간 계층 서비스는 hello id에 따라 권한을 요청 합니다.
6. hello 중간 계층 서비스는 리소스 토큰 백 toohello phone 앱을 보냅니다.
7. hello 전화 앱에 의해 정의 hello 리소스 토큰 hello 리소스 토큰에서 허용 하는 hello 간격에 대 한 hello 권한을 toouse hello 리소스 토큰 toodirectly 리소스 액세스 Cosmos DB 계속할 수 있습니다. 
8. Hello 리소스 토큰이 만료 되 면 후속 요청 401 권한이 없음된 예외가 수신 됩니다.  이 시점에서 hello 전화 앱 hello id를 다시 설정 하 고 새 리소스 토큰을 요청 합니다.

    ![Azure Cosmos DB 리소스 토큰 워크플로](./media/secure-access-to-data/resourcekeyworkflow.png)

리소스 토큰 생성 및 관리 hello 네이티브 Cosmos DB 클라이언트 라이브러리;에 의해 처리 됩니다. 그러나 REST를 사용 하는 경우 hello 요청/인증 헤더를 구성 해야 합니다. REST에 대 한 인증 헤더를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [Cosmos DB 리소스에 대 한 액세스 제어](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) 또는 hello [우리의 Sdk에 대 한 소스 코드](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js)합니다.

Toogenerate 또는 broker 리소스 토큰을 사용 하는 중간 계층 서비스의 예를 참조 hello [ResourceTokenBroker 앱](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers)합니다.

<a id="users"></a>

## <a name="users"></a>사용자
Cosmos DB 사용자는 Cosmos DB 데이터베이스와 연결됩니다.  각 데이터베이스는 0개 이상의 Cosmos DB 사용자를 포함할 수 있습니다.  코드 샘플에서 보여 주는 방법을 다음 hello toocreate Cosmos DB 사용자 리소스입니다.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> 각 Cosmos DB 사용자가 사용 되는 tooretrieve hello 목록이 될 수 있는 PermissionsLink 속성 [권한을](#permissions) hello 사용자와 연결 합니다.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>권한
Cosmos DB 권한 리소스는 Cosmos DB 사용자와 연결됩니다.  각 사용자는 0개 이상의 Cosmos DB 권한을 포함할 수 있습니다.  사용 권한 리소스 hello 사용자 요구 tooaccess 하려고 할 때 특정 응용 프로그램 리소스를 액세스 tooa 보안 토큰을 제공 합니다.
권한 리소스에서 제공될 수 있는 사용 가능한 액세스 수준은 다음 두 가지입니다.

* All: hello 사용자에 게 모든 권한을 hello 리소스에 있습니다.
* 읽기: hello 사용자 hello 리소스의 hello 내용을 읽을 수만 있지만 쓰기, 업데이트 또는 hello 리소스에 대 한 delete 작업을 수행할 수 없습니다.

> [!NOTE]
> 순서 toorun Cosmos DB에서에서 저장된 프로시저 hello 사용자 권한이 있어야 hello 모든 저장된 프로시저를 실행 합니다는 hello에 hello 컬렉션에.
> 
> 

### <a name="code-sample-toocreate-permission"></a>코드 샘플 toocreate 권한

hello 다음 보여 주는 코드 예제 toocreate 사용 권한 리소스 읽기 hello 사용 권한 리소스의 리소스 토큰 hello 방법과 hello 사용 권한을 hello로 연결할 [사용자](#users) 위에서 만든 합니다.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

지정한 다음 hello 사용 권한 컬렉션, 문서 및 첨부 파일 리소스에 대 한 사용자 컬렉션에 대 한 파티션 키를 포함 해야 하는 경우 추가 toohello ResourceLink에에서 ResourcePartitionKey hello 합니다.

### <a name="code-sample-tooread-permissions-for-user"></a>사용자에 대 한 코드 샘플 tooread 권한

Cosmos DB 사용할 수 있도록 사용 권한, tooeasily 특정 사용자와 연결 된 모든 사용 권한 리소스를 가져와서 각 사용자 개체에 대 한 피드입니다.  hello 다음 코드 조각 방법을 보여 줍니다 tooretrieve hello 사용 권한, 위에서 만든 hello 사용자와 관련 된 사용 권한 목록을 구성할 새 DocumentClient hello 사용자를 대신 하 여 인스턴스화합니다.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>다음 단계
* Cosmos DB 데이터베이스 보안에 대해 자세히 toolearn 참조 [Cosmos DB: 데이터베이스 보안](database-security.md)합니다.
* 마스터 및 읽기 전용 키를 관리 하는 방법에 대 한 toolearn 참조 [어떻게 toomanage Azure Cosmos DB 계정](manage-account.md#keys)합니다.
* tooconstruct Azure Cosmos DB 권한 부여 토큰을 확인 하려면 어떻게 해야 toolearn [Azure Cosmos DB 리소스에 대 한 액세스 제어](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)합니다.
