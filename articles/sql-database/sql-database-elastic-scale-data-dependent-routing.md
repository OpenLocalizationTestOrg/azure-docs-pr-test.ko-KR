---
title: "Azure SQL Database를 사용한 데이터 종속 라우팅 | Microsoft Docs"
description: "Azure SQL Database의 분할된 데이터베이스 기능인 데이터 종속 라우팅을 위해 .NET 앱에서 ShardMapManager 클래스를 사용하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="7e936-103">데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="7e936-103">Data dependent routing</span></span>
<span data-ttu-id="7e936-104">**데이터 종속 라우팅** 은 쿼리에서 데이터를 사용하여 적절한 데이터베이스로 요청을 라우트하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="7e936-105">이러한 방식은 분할된 데이터베이스에서 작업할 때의 기본 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="7e936-106">요청 컨텍스트는 특히 분할 키가 쿼리의 일부가 아닌 경우 요청을 라우트하는 데 사용될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="7e936-107">데이터 종속 라우팅을 사용하는 응용 프로그램의 구체적인 각 쿼리 또는 트랜잭션은 요청당 단일 데이터베이스에 대한 액세스로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="7e936-108">Azure SQL Database 탄력적 도구의 경우 이 라우팅은 ADO.NET 응용 프로그램의 **[ShardMapManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**와 함께 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="7e936-109">응용 프로그램에서는 다양한 연결 문자열 또는 분할된 환경의 여러 데이터 조각과 연결된 DB 위치를 추적하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="7e936-110">대신 [분할된 데이터베이스 맵 관리자](sql-database-elastic-scale-shard-map-management.md) 에서 필요한 경우 분할된 데이터베이스 맵의 데이터 및 응용 프로그램의 요청 대상인 분할 키의 값에 따라 올바른 데이터베이스에 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="7e936-111">이 키는 일반적으로 *customer_id*, *tenant_id*, *date_key* 또는 데이터베이스 요청의 기본 매개 변수인 다른 특정 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="7e936-112">자세한 내용은 [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx)(데이터 종속 라우팅을 사용하여 SQL Server 크기 조정)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e936-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="7e936-113">클라이언트 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="7e936-113">Download the client library</span></span>
<span data-ttu-id="7e936-114">클래스를 가져오려면 [탄력적 데이터베이스 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="7e936-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="7e936-115">데이터 종속 라우팅 응용 프로그램에서 ShardMapManager 사용</span><span class="sxs-lookup"><span data-stu-id="7e936-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="7e936-116">응용 프로그램은 초기화 중 팩터리 호출 **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**를 사용하여 **ShardMapManager**를 인스턴스화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="7e936-117">이 예제에서는 **ShardMapManager** 및 포함하는 특정 **ShardMap**이 모두 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="7e936-118">이 예제에서는 GetSqlShardMapManager 및 [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="7e936-119">가능한 가장 낮은 권한 자격 증명을 사용하여 분할된 데이터베이스 맵 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e936-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="7e936-120">응용 프로그램에서 분할된 데이터베이스 맵 자체를 조작하지 않는 경우 팩터리 메서드에서 사용되는 자격 증명은 **전역 분할된 데이터베이스 맵** 데이터베이스에서 읽기 전용 권한만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="7e936-121">이러한 자격 증명을 분할된 데이터베이스 맵 관리자에 대한 연결을 여는데 사용되는 자격 증명과는 일반적으로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="7e936-122">또는 [탄력적 데이터베이스 클라이언트 라이브러리 액세스에 사용되는 자격 증명](sql-database-elastic-scale-manage-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e936-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="7e936-123">OpenConnectionForKey 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="7e936-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="7e936-124">**[ShardMap.OpenConnectionForKey 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**는 **key** 매개 변수 값을 기반으로 적합한 데이터베이스에 명령을 실행할 수 있는 ADO.Net 연결을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="7e936-125">분할된 데이터베이스 정보는 **ShardMapManager**를 통해 응용 프로그램에 캐시되므로, 이러한 요청 시에는 일반적으로 **전역 분할된 데이터베이스 맵**에 대한 데이터베이스 조회를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="7e936-126">**key** 매개 변수는 요청에 대한 적합한 데이터베이스를 결정하는 분할된 데이터베이스 맵의 조회 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="7e936-127">**connectionString** 은 원하는 연결에 대한 사용자 자격 증명만 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="7e936-128">메서드에서 *ShardMap* 을 사용하여 데이터베이스 및 서버를 결정하므로 데이터베이스 이름 또는 서버 이름은 이 **connectionString**에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="7e936-129">분할된 데이터베이스 맵이 변경되고 분할 또는 병합 작업의 결과로 행이 다른 데이터베이스로 이동될 수 있는 환경에서는 **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**를 **ConnectionOptions.Validate**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="7e936-130">이는 연결이 응용 프로그램에 전달되기 전 대상 데이터베이스의 로컬 분할된 데이터베이스 맵(전역의 분할된 데이터베이스 맵이 아님)에 대한 간략한 쿼리와 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="7e936-131">로컬 분할된 데이터베이스 맵에 대한 유효성 검사가 실패하면(캐시가 올바르지 않음을 나타냄) 분할된 데이터베이스 맵 관리자가 조회를 위한 올바른 새 값을 가져오고, 캐시를 업데이트하고, 적절한 데이터베이스 연결을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="7e936-132">**ConnectionOptions.None** 은 응용 프로그램이 온라인 상태이며 분할된 데이터베이스 매핑 변경이 필요하지 않는 경우에만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="7e936-133">이 경우 캐시된 값은 항상 올바른 것으로 간주되며, 대상 데이터베이스에 대한 추가 왕복 유효성 검사 호출을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="7e936-134">이렇게 하면 데이터베이스 트래픽이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-134">That reduces database traffic.</span></span> <span data-ttu-id="7e936-135">**connectionOptions** 는 구성 파일의 값을 통해 특정 기간 동안 분할 변경이 필요한지 여부를 나타내도록 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="7e936-136">이 예제에서는 **customerShardMap**이라는 **ShardMap** 개체를 사용하는 정수 키 **CustomerID** 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="7e936-137">**OpenConnectionForKey** 메서드는 이미 열려 있는 새 연결을 올바른 데이터베이스에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="7e936-138">이러한 방식으로 활용되는 연결은 ADO.Net 연결 풀링을 완벽하게 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="7e936-139">트랜잭션 및 요청을 한 번에 하나의 분할된 데이터베이스를 통해 충족할 수 있다면 이미 ADO.Net을 사용하는 응용 프로그램에서는 이 수정만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="7e936-140">응용 프로그램에서 ADO.Net과 함께 비동기 프로그래밍을 사용하는 경우 **[OpenConnectionForKeyAsync 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="7e936-141">이 메서드의 동작은 ADO.Net의 **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** 메서드에 해당하는 데이터 종속 라우팅입니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="7e936-142">일시적인 오류 처리와 통합</span><span class="sxs-lookup"><span data-stu-id="7e936-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="7e936-143">클라우드에서 데이터 액세스 응용 프로그램을 개발할 경우 일시적인 오류는 앱을 통해 catch하고 오류를 throw하기 전에 작업이 여러 번 다시 시도되는지 확인하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="7e936-144">클라우드 응용 프로그램에 대한 일시적인 오류 처리는 [일시적인 오류 처리](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="7e936-145">일시적인 오류 처리는 데이터 종속 라우팅 패턴과 함께 자연스럽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="7e936-146">주요 요구 사항은 데이터 종속 라우팅 연결을 가져온 **using** 블록을 포함하여 전체 데이터 액세스 요청을 다시 시도하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="7e936-147">위의 예제를 다음과 같이 다시 작성할 수 있습니다(강조 표시된 변경 참조).</span><span class="sxs-lookup"><span data-stu-id="7e936-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="7e936-148">예제 - 일시적인 오류 처리를 사용하는 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="7e936-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="7e936-149">일시적인 오류 처리를 구현하는 데 필요한 패키지는 탄력적 데이터베이스 샘플 응용 프로그램을 빌드할 때 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="7e936-150">[엔터프라이즈 라이브러리 - 일시적인 오류 처리 응용 프로그램 블록](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)에서도 패키지가 별도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="7e936-151">버전 6.0 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="7e936-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="7e936-152">트랜잭션 일관성</span><span class="sxs-lookup"><span data-stu-id="7e936-152">Transactional consistency</span></span>
<span data-ttu-id="7e936-153">트랜잭션 속성은 분할된 데이터베이스에 로컬인 모든 작업에 대해 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="7e936-154">예를 들어 데이터 종속 라우팅을 통해 제출된 트랜잭션은 연결의 대상인 분할된 데이터베이스 범위 내에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="7e936-155">이때 트랜잭션으로 여러 연결을 등록하기 위한 기능은 제공되지 않으므로 분할된 데이터베이스 간에 수행되는 작업에 대한 트랜잭션은 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e936-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e936-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e936-156">Next steps</span></span>
<span data-ttu-id="7e936-157">분할된 데이터베이스를 분리하거나 다시 연결하려면 [RecoveryManager 클래스를 사용하여 분할된 데이터베이스 맵 문제 해결](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="7e936-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

