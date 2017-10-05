---
title: "탄력적 데이터베이스 클라이언트 라이브러리에 대한 자격 증명 관리 | Microsoft Docs"
description: "탄력적 데이터베이스 확장 앱에 대해 올바른 수준의 자격 증명(관리자부터 읽기 전용까지)을 설정하는 방법입니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 46908be2846062a0520d21e06db3091a4d711b0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="credentials-used-to-access-the-elastic-database-client-library"></a><span data-ttu-id="3949b-103">탄력적 데이터베이스 클라이언트 라이브러리 액세스에 사용되는 자격 증명</span><span class="sxs-lookup"><span data-stu-id="3949b-103">Credentials used to access the Elastic Database client library</span></span>
<span data-ttu-id="3949b-104">[Elastic Database 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)는 세 가지 다른 종류의 자격 증명을 사용하여 [분할된 데이터베이스 맵 관리자](sql-database-elastic-scale-shard-map-management.md)에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-104">The [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials to access the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="3949b-105">필요에 따라서 가능한 한 액세스 수준이 가장 낮은 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-105">Depending on the need, use the credential with  the lowest level of access possible.</span></span>

* <span data-ttu-id="3949b-106">**관리 자격 증명**: 분할된 데이터베이스 맵 관리자를 만들고 조작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="3949b-107">( [용어집](sql-database-elastic-scale-glossary.md)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="3949b-107">(See the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="3949b-108">**액세스 자격 증명**: 분할된 데이터베이스에 대한 정보를 얻기 위해 기존의 분할된 데이터베이스 맵 관리자에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-108">**Access credentials**: to access an existing shard map manager to obtain information about shards.</span></span>
* <span data-ttu-id="3949b-109">**연결 자격 증명**: 분할된 데이터베이스에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-109">**Connection credentials**: to connect to shards.</span></span> 

<span data-ttu-id="3949b-110">[Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3949b-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="3949b-111">관리 자격 증명 정보</span><span class="sxs-lookup"><span data-stu-id="3949b-111">About management credentials</span></span>
<span data-ttu-id="3949b-112">관리 자격 증명은 분할된 데이터베이스 맵을 조작하는 응용 프로그램에 대한 [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 개체를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-112">Management credentials are used to create a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="3949b-113">예를 들어 [Elastic Database 도구를 사용하여 분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md) 및 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요. 탄력적인 크기의 클라이언트 라이브러리 사용자는 SQL 사용자 및 SQL 로그인을 만들고 각각에 대해 글로벌 분할된 데이터베이스 맵 데이터베이스는 물론 모든 분할된 데이터베이스 맵에 대한 읽기/쓰기 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) The user of the elastic scale client library creates the SQL users and SQL logins and makes sure each is granted the read/write permissions on the global shard map database and all shard databases as well.</span></span> <span data-ttu-id="3949b-114">이러한 자격 증명은 분할된 데이터베이스 맵에 대한 변경을 수행할 때 전역 분할된 데이터베이스 맵 및 로컬 분할된 데이터베이스 맵을 유지 관리 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-114">These credentials are used to maintain the global shard map and the local shard maps when changes to the shard map are performed.</span></span> <span data-ttu-id="3949b-115">예를 들어 관리 자격 증명을 사용하여 분할된 데이터베이스 맵 관리자 개체를 만듭니다([**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx) 사용).</span><span class="sxs-lookup"><span data-stu-id="3949b-115">For instance, use the management credentials to create the shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="3949b-116">**smmAdminConnectionString** 변수는 관리 자격 증명을 포함하는 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-116">The variable **smmAdminConnectionString** is a connection string that contains the management credentials.</span></span> <span data-ttu-id="3949b-117">사용자 ID와 암호는 분할된 데이터베이스 맵 데이터베이스와 개별 분할된 데이터베이스에 대한 읽기/쓰기 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-117">The user ID and password provides read/write access to both shard map database and individual shards.</span></span> <span data-ttu-id="3949b-118">또한 관리 연결 문자열은 전역 분할된 데이터베이스 맵 데이터베이스를 식별하는 서버 이름과 데이터베이스 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-118">The management connection string also includes the server name and database name to identify the global shard map database.</span></span> <span data-ttu-id="3949b-119">다음은 해당 용도를 위한 일반적인 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="3949b-120">형식의 값을 사용 하지 마십시오 "username@server"-대신 "username" 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-120">Do not use values in the form of "username@server"—instead just use the "username" value.</span></span>  <span data-ttu-id="3949b-121">자격 증명은 분할된 데이터베이스 맵 관리자 데이터베이스와 각기 다른 서버에 있을 수 있는 개별 분할된 데이터베이스에 대해 모두 작동해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-121">This is because credentials must work against both the shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="3949b-122">액세스 자격 증명</span><span class="sxs-lookup"><span data-stu-id="3949b-122">Access credentials</span></span>
<span data-ttu-id="3949b-123">분할된 데이터베이스 맵을 관리하지 않는 응용 프로그램에 분할된 데이터베이스 맵 관리자를 만드는 경우, 글로벌 분할된 데이터베이스 맵에 대해 읽기 전용 권한이 있는 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on the global shard map.</span></span> <span data-ttu-id="3949b-124">이러한 자격 증명으로 글로벌 분할된 데이터베이스 맵에서 검색한 정보는 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 에 사용되며, 클라이언트의 분할된 데이터베이스 맵 캐시를 채우는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-124">The information retrieved from the global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and to populate the shard map cache on the client.</span></span> <span data-ttu-id="3949b-125">자격 증명은 위에 표시된 것처럼 **GetSqlShardMapManager** 에 대한 동일한 호출 패턴을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-125">The credentials are provided through the same call pattern to **GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="3949b-126">**관리자가 아닌** 사용자를 대신하여 이 액세스에 대한 서로 다른 자격 증명의 사용을 반영하기 위해 **smmReadOnlyConnectionString**을 사용합니다. 이러한 자격 증명은 전역 분할된 데이터베이스 맵에 대한 쓰기 권한을 제공하지 않아야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-126">Note the use of the **smmReadOnlyConnectionString** to reflect the use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on the global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="3949b-127">연결 자격 증명</span><span class="sxs-lookup"><span data-stu-id="3949b-127">Connection credentials</span></span>
<span data-ttu-id="3949b-128">[**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 메서드를 사용하여 분할 키와 연결된 분할된 데이터베이스에 액세스할 때 추가 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-128">Additional credentials are needed when using the [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method to access a shard associated with a sharding key.</span></span> <span data-ttu-id="3949b-129">이러한 자격 증명은 분할된 데이터베이스에 있는 로컬 분할된 데이터베이스 맵 테이블에 대한 읽기 전용 액세스 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-129">These credentials need to provide permissions for read-only access to the local shard map tables residing on the shard.</span></span> <span data-ttu-id="3949b-130">이 권한은 분할된 데이터베이스의 데이터 종속 라우팅에 대한 연결 유효성 검사를 수행하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-130">This is needed to perform connection validation for data-dependent routing on the shard.</span></span> <span data-ttu-id="3949b-131">이 코드 조각은 데이터 종속 라우팅의 컨텍스트에서 데이터 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-131">This code snippet allows data access in the context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="3949b-132">이 예제에서 **smmUserConnectionString** 에는 사용자 자격 증명의 연결 문자열이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-132">In this example, **smmUserConnectionString** holds the connection string for the user credentials.</span></span> <span data-ttu-id="3949b-133">Azure SQL DB의 경우 사용자 자격 증명에 대한 일반적인 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="3949b-134">관리자 자격 증명에서와 마찬가지로 수행 하지 값의 형태로 "username@server"입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-134">As with the admin credentials, do not values in the form of "username@server".</span></span> <span data-ttu-id="3949b-135">대신 "username"만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-135">Instead, just use "username".</span></span>  <span data-ttu-id="3949b-136">또한 서버 이름과 데이터베이스 이름은 연결 문자열에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-136">Also note that the connection string does not contain a server name and database name.</span></span> <span data-ttu-id="3949b-137">**OpenConnectionForKey** 호출은 키에 따라 올바른 분할된 데이터베이스로 연결을 자동으로 지정하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-137">That is because the **OpenConnectionForKey** call will automatically direct the connection to the correct shard based on the key.</span></span> <span data-ttu-id="3949b-138">따라서 데이터베이스 이름과 서버 이름이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3949b-138">Hence, the database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3949b-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3949b-139">See also</span></span>
[<span data-ttu-id="3949b-140">Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리</span><span class="sxs-lookup"><span data-stu-id="3949b-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="3949b-141">SQL 데이터베이스 보안 설정</span><span class="sxs-lookup"><span data-stu-id="3949b-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="3949b-142">탄력적 데이터베이스 작업 시작</span><span class="sxs-lookup"><span data-stu-id="3949b-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

