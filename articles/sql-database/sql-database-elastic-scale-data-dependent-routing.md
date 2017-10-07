---
title: "Azure SQL 데이터베이스 라우팅 종속 aaaData | Microsoft Docs"
description: "어떻게 toouse hello 데이터 종속 라우팅, Azure SQL 데이터베이스에서 분할 된 데이터베이스의 기능에 대 한.NET 응용 프로그램에서 ShardMapManager 클래스"
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
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="f9b40-103">데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="f9b40-103">Data dependent routing</span></span>
<span data-ttu-id="f9b40-104">**데이터 종속 라우팅** 쿼리 tooroute hello 요청 tooan 적절 한 데이터베이스의 hello 기능 toouse hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-104">**Data dependent routing** is hello ability toouse hello data in a query tooroute hello request tooan appropriate database.</span></span> <span data-ttu-id="f9b40-105">이러한 방식은 분할된 데이터베이스에서 작업할 때의 기본 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="f9b40-106">특히 hello 분할 키 일부가 아닌 경우 hello 쿼리의 hello 요청 컨텍스트는 사용 되는 tooroute hello 요청 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-106">hello request context may also be used tooroute hello request, especially if hello sharding key is not part of hello query.</span></span> <span data-ttu-id="f9b40-107">각 특정 쿼리 또는 데이터 종속 라우팅을 사용 하 여 응용 프로그램에서 트랜잭션 제한 tooaccessing 요청당 단일 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-107">Each specific query or transaction in an application using data dependent routing is restricted tooaccessing a single database per request.</span></span> <span data-ttu-id="f9b40-108">Hello Azure SQL 데이터베이스 탄력적 도구에 대 한 hello를 사용 하 여 수행 됩니다이 라우팅은  **[ShardMapManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  ADO.NET 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-108">For hello Azure SQL Database Elastic tools, this routing is accomplished with hello **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="f9b40-109">다양 한 연결 문자열 또는 연결 된 hello 분할 환경에서 데이터의 다른 조각 DB 위치 hello 응용 프로그램에 tootrack 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-109">hello application does not need tootrack various connection strings or DB locations associated with different slices of data in hello sharded environment.</span></span> <span data-ttu-id="f9b40-110">대신, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) 열립니다 연결 toohello 올바른 데이터베이스 필요할 때 hello 데이터를 기반으로 분할 맵은 hello 및 hello hello 응용 프로그램의 요청의 hello 대상인 hello 분할 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-110">Instead, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections toohello correct databases when needed, based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello application’s request.</span></span> <span data-ttu-id="f9b40-111">hello 키는 일반적으로 hello *customer_id*, *tenant_id*, *date_key*, 또는 hello 데이터베이스 요청의 기본 매개 변수는 다른 특정 식별자)입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-111">hello key is typically hello *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of hello database request).</span></span> 

<span data-ttu-id="f9b40-112">자세한 내용은 [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx)(데이터 종속 라우팅을 사용하여 SQL Server 크기 조정)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9b40-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-hello-client-library"></a><span data-ttu-id="f9b40-113">Hello 클라이언트 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="f9b40-113">Download hello client library</span></span>
<span data-ttu-id="f9b40-114">tooget hello 클래스인 설치 hello [탄력적 데이터베이스 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-114">tooget hello class, install hello [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="f9b40-115">데이터 종속 라우팅 응용 프로그램에서 ShardMapManager 사용</span><span class="sxs-lookup"><span data-stu-id="f9b40-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="f9b40-116">응용 프로그램 hello 인스턴스화해야 **ShardMapManager** hello 팩터리 호출을 사용 하 여 초기화 하는 동안  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-116">Applications should instantiate hello **ShardMapManager** during initialization, using hello factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="f9b40-117">이 예제에서는 **ShardMapManager** 및 포함하는 특정 **ShardMap**이 모두 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="f9b40-118">이 예제에서는 GetSqlShardMapManager hello 및 [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="f9b40-118">This example shows hello GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a><span data-ttu-id="f9b40-119">가능한 가장 낮은 권한 자격 증명을 사용 하 여 hello 분할 맵은 가져오기 위한</span><span class="sxs-lookup"><span data-stu-id="f9b40-119">Use lowest privilege credentials possible for getting hello shard map</span></span>
<span data-ttu-id="f9b40-120">응용 프로그램 하지 hello 분할 맵 자체를 조작 하 고, 경우 hello 자격 증명 hello 팩터리 메서드에 사용 되는 읽기 전용만 대해 권한이 있어야 hello **글로벌 분할 맵은** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-120">If an application is not manipulating hello shard map itself, hello credentials used in hello factory method should have just read-only permissions on hello **Global Shard Map** database.</span></span> <span data-ttu-id="f9b40-121">이러한 자격 증명은 사용 된 자격 증명 tooopen 연결 toohello shard map 관리자 일반적으로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-121">These credentials are typically different from credentials used tooopen connections toohello shard map manager.</span></span> <span data-ttu-id="f9b40-122">참고 항목 [tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하는 자격 증명](sql-database-elastic-scale-manage-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-122">See also [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-hello-openconnectionforkey-method"></a><span data-ttu-id="f9b40-123">Hello OpenConnectionForKey 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-123">Call hello OpenConnectionForKey method</span></span>
<span data-ttu-id="f9b40-124">hello  **[ShardMap.OpenConnectionForKey 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  ADO.Net 연결을 발급 하는 hello hello 값에 따라 명령을 toohello 적절 한 데이터베이스에 대 한 준비 반환 **키**매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-124">hello **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands toohello appropriate database based on hello value of hello **key** parameter.</span></span> <span data-ttu-id="f9b40-125">분할 정보 hello 하 여 hello 응용 프로그램에 캐시 된 **ShardMapManager**이러한 요청 hello에 대 한 데이터베이스를 검색 하는 일반적으로 포함 하지 않으므로 **글로벌 분할 맵은** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-125">Shard information is cached in hello application by hello **ShardMapManager**, so these requests do not typically involve a database lookup against hello **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="f9b40-126">hello **키** 매개 변수는 hello 분할 맵 toodetermine hello 적절 한 데이터베이스에 조회 키로 hello 요청에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-126">hello **key** parameter is used as a lookup key into hello shard map toodetermine hello appropriate database for hello request.</span></span> 
* <span data-ttu-id="f9b40-127">hello **connectionString** 는 사용 되는 toopass hello 필요한 연결에 대 한 유일한 hello 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-127">hello **connectionString** is used toopass only hello user credentials for hello desired connection.</span></span> <span data-ttu-id="f9b40-128">데이터베이스 이름 또는 서버 이름이 없습니다 여기에 포함 *connectionString* hello 데이터베이스와 서버 hello를 사용 하 여 hello 메서드는 확인 하므로 **ShardMap**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-128">No database name or server name are included in this *connectionString* since hello method will determine hello database and server using hello **ShardMap**.</span></span> 
* <span data-ttu-id="f9b40-129">hello  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  설정할지 너무**ConnectionOptions.Validate** 경우 분할 영역에 매핑합니다 환경 변경 될 수 있으며 행으로 tooother 데이터베이스를 이동할 수는 분할 또는 병합 작업의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-129">hello **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set too**ConnectionOptions.Validate** if an environment where shard maps may change and rows may move tooother databases as a result of split or merge operations.</span></span> <span data-ttu-id="f9b40-130">여기에 대 한 간단한 쿼리 toohello 로컬 분할 맵을 hello 연결 하기 전에 hello 대상 데이터베이스 (하지 toohello 글로벌 shard map)에 toohello 응용 프로그램 배달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-130">This involves a brief query toohello local shard map on hello target database (not toohello global shard map) before hello connection is delivered toohello application.</span></span> 

<span data-ttu-id="f9b40-131">로컬 분할 맵은 hello에 대 한 hello 유효성 검사 (hello 캐시 잘못 되었음을 나타냄)에 실패 hello Shard Map Manager hello 글로벌 shard map tooobtain hello 새 올바른 값을 쿼리 합니다 hello 조회에 대 한 hello 캐시를 업데이트 하 고 가져오고 hello를 반환 합니다. 적절 한 데이터베이스 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-131">If hello validation against hello local shard map fails (indicating that hello cache is incorrect), hello Shard Map Manager will query hello global shard map tooobtain hello new correct value for hello lookup, update hello cache, and obtain and return hello appropriate database connection.</span></span> 

<span data-ttu-id="f9b40-132">**ConnectionOptions.None** 은 응용 프로그램이 온라인 상태이며 분할된 데이터베이스 매핑 변경이 필요하지 않는 경우에만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="f9b40-133">이 경우 캐시 hello 값 tooalways 잘못 되어 hello 추가 왕복 유효성 검사 호출 toohello 대상 데이터베이스를 안전 하 게 건너뛸 수 있는으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-133">In that case, hello cached values can be assumed tooalways be correct, and hello extra round-trip validation call toohello target database can be safely skipped.</span></span> <span data-ttu-id="f9b40-134">이렇게 하면 데이터베이스 트래픽이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-134">That reduces database traffic.</span></span> <span data-ttu-id="f9b40-135">hello **connectionOptions** 는 분할 변경 작업이 필요 여부 일정 기간 동안이 아닌 구성 파일 tooindicate에 값을 통해 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-135">hello **connectionOptions** may also be set via a value in a configuration file tooindicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="f9b40-136">이 예에서는 정수 키의 hello 값 **CustomerID**를 사용 하 여 한 **ShardMap** 라는 개체 **customerShardMap**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-136">This example uses hello value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
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

<span data-ttu-id="f9b40-137">hello **OpenConnectionForKey** 메서드가 새 이미 공개 연결 toohello 올바른 데이터베이스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-137">hello **OpenConnectionForKey** method returns a new already-open connection toohello correct database.</span></span> <span data-ttu-id="f9b40-138">이러한 방식으로 활용되는 연결은 ADO.Net 연결 풀링을 완벽하게 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="f9b40-139">한 번에 하나의 분할 하 여 트랜잭션 및 요청을 충족 될 수,으로이 이미 ADO.Net을 사용 하 여 응용 프로그램에서 필요한 hello만 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-139">As long as transactions and requests can be satisfied by one shard at a time, this should be hello only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="f9b40-140">hello  **[OpenConnectionForKeyAsync 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  응용 프로그램에서 사용 하 여 ADO.Net의 비동기 프로그래밍 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-140">hello **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="f9b40-141">해당 동작은 hello 데이터 종속 라우팅 ADO에 해당 합니다. Net의  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  메서드.</span><span class="sxs-lookup"><span data-stu-id="f9b40-141">Its behavior is hello data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="f9b40-142">일시적인 오류 처리와 통합</span><span class="sxs-lookup"><span data-stu-id="f9b40-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="f9b40-143">Hello 클라우드에서 데이터 액세스 응용 프로그램 개발에 가장 좋은 방법은 tooensure hello 작업 오류를 throw 하기 전에 여러 번 재시도 하 고 일시적인 오류 hello 앱에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-143">A best practice in developing data access applications in hello cloud is tooensure that transient faults are caught by hello app, and that hello operations are retried several times before throwing an error.</span></span> <span data-ttu-id="f9b40-144">클라우드 응용 프로그램에 대한 일시적인 오류 처리는 [일시적인 오류 처리](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="f9b40-145">일시적인 오류 처리는 hello 데이터 종속 라우팅 패턴으로 자연스럽 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-145">Transient fault handling can coexist naturally with hello Data Dependent Routing pattern.</span></span> <span data-ttu-id="f9b40-146">hello 주요 요구 사항은 되 hello를 포함 하 여 tooretry hello 전체 데이터 액세스 요청 **를 사용 하 여** hello 데이터 종속 라우팅 연결을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-146">hello key requirement is tooretry hello entire data access request including hello **using** block that obtained hello data-dependent routing connection.</span></span> <span data-ttu-id="f9b40-147">위의 hello 예제 (강조 표시 된 변경 참고) 다음과 같이 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-147">hello example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="f9b40-148">예제 - 일시적인 오류 처리를 사용하는 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="f9b40-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
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


<span data-ttu-id="f9b40-149">필요한 tooimplement 일시적인 오류 처리는 패키지는 hello 탄력적 데이터베이스에 대 한 샘플 응용 프로그램을 빌드할 때 자동으로 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-149">Packages necessary tooimplement transient fault handling are downloaded automatically when you build hello elastic database sample application.</span></span> <span data-ttu-id="f9b40-150">[엔터프라이즈 라이브러리 - 일시적인 오류 처리 응용 프로그램 블록](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)에서도 패키지가 별도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="f9b40-151">버전 6.0 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f9b40-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="f9b40-152">트랜잭션 일관성</span><span class="sxs-lookup"><span data-stu-id="f9b40-152">Transactional consistency</span></span>
<span data-ttu-id="f9b40-153">트랜잭션 속성은 모든 작업에 대 한 로컬 tooa 분할 영역에 대 한 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-153">Transactional properties are guaranteed for all operations local tooa shard.</span></span> <span data-ttu-id="f9b40-154">예를 들어 트랜잭션 데이터 종속 라우팅을 통해 제출 된 hello 연결에 대 한 hello 대상 분할의 hello 범위 내에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-154">For example, transactions submitted through data-dependent routing execute within hello scope of hello target shard for hello connection.</span></span> <span data-ttu-id="f9b40-155">이때 트랜잭션으로 여러 연결을 등록하기 위한 기능은 제공되지 않으므로 분할된 데이터베이스 간에 수행되는 작업에 대한 트랜잭션은 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9b40-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b40-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9b40-156">Next steps</span></span>
<span data-ttu-id="f9b40-157">toodetach 분할 또는 분할 tooreattach 참조 [hello RecoveryManager 클래스 toofix 분할 맵 문제를 사용 하 여](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="f9b40-157">toodetach a shard, or tooreattach a shard, see [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

