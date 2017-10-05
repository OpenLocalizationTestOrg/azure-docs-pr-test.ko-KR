---
title: "Azure Cosmos DB에서 데이터에 대한 액세스를 보호하는 방법 | Microsoft Docs"
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="4f4fb-103">Azure Cosmos DB 데이터에 대한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="4f4fb-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="4f4fb-104">이 문서에서는 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)에 저장된 데이터에 대한 액세스를 보호하는 방법을 개괄적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="4f4fb-105">Azure Cosmos DB는 두 가지 유형의 키를 사용하여 사용자를 인증하고 해당 데이터 및 리소스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="4f4fb-106">키 유형</span><span class="sxs-lookup"><span data-stu-id="4f4fb-106">Key type</span></span>|<span data-ttu-id="4f4fb-107">리소스</span><span class="sxs-lookup"><span data-stu-id="4f4fb-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="4f4fb-108">마스터 키</span><span class="sxs-lookup"><span data-stu-id="4f4fb-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="4f4fb-109">데이터베이스 계정, 데이터베이스, 사용자, 사용 권한을 비롯한 관리 리소스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="4f4fb-110">리소스 토큰</span><span class="sxs-lookup"><span data-stu-id="4f4fb-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="4f4fb-111">컬렉션, 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF를 비롯한 응용 프로그램 리소스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="4f4fb-112">마스터 키</span><span class="sxs-lookup"><span data-stu-id="4f4fb-112">Master keys</span></span> 

<span data-ttu-id="4f4fb-113">마스터 키는 데이터베이스 계정에 대한 모든 관리 리소스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="4f4fb-114">마스터 키:</span><span class="sxs-lookup"><span data-stu-id="4f4fb-114">Master keys:</span></span>  
- <span data-ttu-id="4f4fb-115">계정, 데이터베이스, 사용자 및 사용 권한에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="4f4fb-116">컬렉션 및 문서에 대한 세분화된 액세스를 제공하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="4f4fb-117">계정 생성 중에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="4f4fb-118">언제든지 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="4f4fb-119">각 계정은 두 개의 마스터 키(주 키와 보조 키)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="4f4fb-120">이중 키를 사용하는 목적은 키를 다시 생성하거나 롤링하여 계정 및 데이터에 지속적인 액세스를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="4f4fb-121">Cosmos DB 계정에 대한 두 개의 마스터 키 외에도 두 개의 읽기 전용 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="4f4fb-122">이러한 읽기 전용 키는 계정에 대한 읽기 작업만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="4f4fb-123">읽기 전용 키는 읽기 권한 리소스에 대한 액세스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="4f4fb-124">Azure Portal을 사용하여 주, 보조, 읽기 전용 및 읽기-쓰기 마스터 키를 검색 및 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="4f4fb-125">자세한 내용은 [액세스 키 보기, 복사 및 다시 생성](manage-account.md#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Azure Portal에서 액세스 제어(IAM) - NoSQL 데이터베이스 보안 설명](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="4f4fb-127">마스터 키를 회전하는 프로세스는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="4f4fb-128">Azure Portal로 이동하여 보조 키를 검색한 후 응용 프로그램에서 주 키를 보조 키로 바꾼 다음 Azure Portal에서 주 키를 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Azure Portal에서 마스터 키 회전 - NoSQL 데이터베이스 보안 설명](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="4f4fb-130">마스터 키를 사용할 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="4f4fb-130">Code sample to use a master key</span></span>

<span data-ttu-id="4f4fb-131">다음 코드 샘플에서는 Cosmos DB 계정 끝점 및 마스터 키를 사용해서 DocumentClient를 인스턴스화하고 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="4f4fb-132">리소스 토큰</span><span class="sxs-lookup"><span data-stu-id="4f4fb-132">Resource tokens</span></span>

<span data-ttu-id="4f4fb-133">리소스 토큰은 데이터베이스 내에서 응용 프로그램 리소스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="4f4fb-134">리소스 토큰:</span><span class="sxs-lookup"><span data-stu-id="4f4fb-134">Resource tokens:</span></span>
- <span data-ttu-id="4f4fb-135">특정 컬렉션, 파티션 키, 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="4f4fb-136">[사용자](#users)에게 특정 리소스에 대한 [사용 권한](#permissions)이 부여된 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="4f4fb-137">POST, GET 또는 PUT 호출로 권한 리소스가 작동할 때 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="4f4fb-138">사용자, 리소스 및 사용 권한을 위해 특별히 구성된 해시 리소스 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="4f4fb-139">시간은 사용자 지정 가능한 유효 기간으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="4f4fb-140">기본 유효 기간은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="4f4fb-141">하지만 토큰 수명은 최대 5시간까지 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="4f4fb-142">마스터 키를 전달하기 위한 안전한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="4f4fb-143">Cosmos DB 계정에서 클라이언트가 부여된 권한에 따라 리소스를 읽고 쓰고 삭제할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="4f4fb-144">Cosmos DB 계정에 있는 리소스에 대한 액세스 권한을 마스터 키로 신뢰할 수 없는 클라이언트에 제공하려는 경우 Cosmos DB 사용자 및 권한을 만들어서 리소스 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="4f4fb-145">Cosmos DB 리소스 토큰은 사용자가 부여한 권한에 따라 마스터 또는 읽기 전용 키에 대한 요구 없이 Cosmos DB 계정에서 클라이언트가 리소스를 읽고, 쓰고, 삭제할 수 있게 해주는 안전한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="4f4fb-146">다음은 리소스 토큰을 요청, 생성 및 클라이언트에 제공할 수 있는 일반적인 디자인 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="4f4fb-147">중간 계층 서비스는 모바일 응용 프로그램이 사용자 사진을 공유하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="4f4fb-148">중간 계층 서비스는 Cosmos DB 계정의 마스터 키를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="4f4fb-149">사진 앱은 최종 사용자 모바일 장치에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="4f4fb-150">로그인하면 사진 앱이 중간 계층 서비스를 사용해서 사용자의 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="4f4fb-151">ID 설정 방식은 순전히 응용 프로그램에 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="4f4fb-152">ID가 설정된 다음에는 중간 계층 서비스 요청 권한이 ID를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="4f4fb-153">중간 계층 서비스는 리소스 토큰을 다시 전화 앱으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="4f4fb-154">전화 앱은 계속 리소스 토큰을 사용해서 리소스의 토큰으로 정의된 권한을 사용하여 리소스 토큰에서 허용하는 간격으로 Cosmos DB 리소스에 직접 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="4f4fb-155">리소스 토큰이 만료되면 후속 요청은 401 허가되지 않은 예외를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="4f4fb-156">이 지점에서는 전화 앱이 ID 를 다시 설정하고 새로운 리소스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Azure Cosmos DB 리소스 토큰 워크플로](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="4f4fb-158">리소스 토큰 생성 및 관리는 네이티브 Cosmos DB 클라이언트 라이브러리에서 처리하지만 REST를 사용하는 경우 요청/인증 헤더를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="4f4fb-159">REST에 대한 인증 헤더를 만드는 방법에 대한 자세한 내용은 [Cosmos DB 리소스에 대한 액세스 제어](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) 또는 [SDK에 대한 소스 코드](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="4f4fb-160">리소스 토큰을 생성하거나 broker하는 데 사용되는 중간 계층 서비스의 예는 [ResourceTokenBroker 앱](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="4f4fb-161">사용자</span><span class="sxs-lookup"><span data-stu-id="4f4fb-161">Users</span></span>
<span data-ttu-id="4f4fb-162">Cosmos DB 사용자는 Cosmos DB 데이터베이스와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="4f4fb-163">각 데이터베이스는 0개 이상의 Cosmos DB 사용자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="4f4fb-164">다음 코드 샘플에서는 Cosmos DB 사용자 리소스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="4f4fb-165">각 Cosmos DB 사용자에게는 해당 사용자와 관련된 [권한](#permissions) 목록을 검색하기 위해 사용할 수 있는 PermissionsLink 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="4f4fb-166">권한</span><span class="sxs-lookup"><span data-stu-id="4f4fb-166">Permissions</span></span>
<span data-ttu-id="4f4fb-167">Cosmos DB 권한 리소스는 Cosmos DB 사용자와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="4f4fb-168">각 사용자는 0개 이상의 Cosmos DB 권한을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="4f4fb-169">권한 리소스는 사용자가 특정 응용 프로그램 리소스에 액세스하려고 시도할 때 필요한 보안 토큰에 대한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="4f4fb-170">권한 리소스에서 제공될 수 있는 사용 가능한 액세스 수준은 다음 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="4f4fb-171">전체: 사용자가 리소스에 대한 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="4f4fb-172">읽기: 사용자가 리소스 내용을 읽을 수만 있고 리소스에 대해 쓰기, 업데이트 또는 삭제 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="4f4fb-173">Cosmos DB 저장 프로시저를 실행하려면 사용자에게 저장 프로시저가 실행되는 컬렉션에 대한 모든 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="4f4fb-174">사용 권한을 만드는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="4f4fb-174">Code sample to create permission</span></span>

<span data-ttu-id="4f4fb-175">다음 코드 샘플은 권한 리소스를 만들고, 권한 리소스의 리소스 토큰을 읽고, 위에서 생성된 [사용자](#users)와 사용 권한을 연결시키는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="4f4fb-176">컬렉션에 파티션 키를 지정한 다음 컬렉션에 대한 권한을 지정한 경우 문서 및 첨부 파일 리소스는 ResourceLink 외에도 ResourcePartitionKey를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="4f4fb-177">사용자에 대한 권한을 읽는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="4f4fb-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="4f4fb-178">특정 사용자와 관련된 모든 권한 리소스를 쉽게 가져오기 위해, Cosmos DB는 각 사용자 개체에 대해 권한 피드를 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="4f4fb-179">다음 코드 조각은 위에서 생성된 사용자와 연관된 권한을 검색하고, 권한 목록을 생성하고, 사용자를 대신해서 새 DocumentClient를 인스턴스화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4f4fb-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f4fb-180">Next steps</span></span>
* <span data-ttu-id="4f4fb-181">Cosmos DB 데이터베이스 보안에 대한 자세한 내용은 [Cosmos DB: 데이터베이스 보안](database-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="4f4fb-182">마스터 키와 읽기 전용 키를 관리하는 방법에 대한 자세한 내용은 [Azure Cosmos DB 계정을 관리하는 방법](manage-account.md#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="4f4fb-183">Azure Cosmos DB 권한 부여 토큰을 생성하는 방법에 대한 자세한 내용은 [Azure Cosmos DB 리소스에 대한 액세스 제어](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f4fb-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
