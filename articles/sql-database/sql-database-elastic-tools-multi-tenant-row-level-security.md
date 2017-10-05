---
title: "탄력적 데이터베이스 도구 및 행 수준 보안을 제공하는 다중 테넌트 응용 프로그램"
description: "탄력적 데이터베이스 도구와 행 수준 보안을 함께 사용하여 다중 테넌트 분할된 데이터베이스를 지원하고 Azure SQL 데이터베이스의 데이터 계층을 유연하게 확장할 수 있는 응용 프로그램 구축 방법에 대해 알아보세요."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="30deb-103">탄력적 데이터베이스 도구 및 행 수준 보안을 제공하는 다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30deb-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="30deb-104">[탄력적 데이터베이스 도구](sql-database-elastic-scale-get-started.md) 및 [RLS(행 수준 보안)](https://msdn.microsoft.com/library/dn765131)는 Azure SQL Database로 다중 테넌트 응용 프로그램의 데이터를 유연하고 효율적으로 확장할 수 있는 강력한 기능 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="30deb-105">자세한 내용은 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30deb-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="30deb-106">이 문서에서는 이러한 기술을 함께 사용하여 **ADO.NET SqlClient** 및/또는 **Entity Framework**를 통해 다중 테넌트 분할된 데이터베이스를 지원하는 우수한 확장성의 응용 프로그램을 구축하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="30deb-107">**탄력적 데이터베이스 도구** 를 사용하면 개발자는 .NET 라이브러리 및 Azure 서비스 템플릿 집합을 사용하는 산업 표준 분할 관행을 통해 응용 프로그램의 데이터 계층을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="30deb-108">탄력적 데이터베이스 클라이언트 라이브러리를 사용하여 분할된 데이터베이스를 관리하면 일반적으로 분할과 관련된 여러 인프라 작업을 자동화 및 간소화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="30deb-109">**행 수준 보안** 을 사용하면 개발자는 쿼리를 실행하는 테넌트에 속하지 않은 행을 필터링하는 보안 정책을 사용하여 여러 테넌트의 데이터를 같은 데이터베이스에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="30deb-110">액세스 논리를 응용 프로그램이 아닌 데이터베이스 내부에 중앙 집중화하면 코드 베이스가 성장하기 때문에 응용 프로그램의 유지 관리가 간소화되고 오류 위험이 완화됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="30deb-111">이러한 기능을 함께 사용하면 여러 테넌트의 데이터를 같은 분할된 데이터베이스에 저장하여 응용 프로그램의 비용을 절감하고 효율성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="30deb-112">또한 다중 테넌트 분할된 데이터베이스는 테넌트 간에 리소스가 균등하게 분산된다는 보장이 없기 때문에 보다 엄격한 성능 보장을 필요로 하는 "프리미엄" 테넌트를 위해 격리된 단일 테넌트 분할된 데이터베이스를 제공하는 응용 프로그램의 유연성은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="30deb-113">간단히 말해서 탄력적 데이터베이스 클라이언트 라이브러리의 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) API는 테넌트를 해당 분할 키(일반적으로 "TenantId")가 포함된 올바른 분할된 데이터베이스에 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="30deb-114">데이터베이스에 연결되면 데이터베이스의 RLS 보안 정책에 따라 테넌트는 해당 TenantId가 포함된 행에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="30deb-115">모든 테이블에는 각 테넌트에 속한 행을 나타내는 TenantId 열이 포함되어 있는 것으로 추정됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![앱 아키텍처 블로그][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="30deb-117">샘플 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="30deb-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="30deb-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30deb-118">Prerequisites</span></span>
* <span data-ttu-id="30deb-119">Visual Studio 2012 이상 사용</span><span class="sxs-lookup"><span data-stu-id="30deb-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="30deb-120">Azure SQL 데이터베이스 3개 생성</span><span class="sxs-lookup"><span data-stu-id="30deb-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="30deb-121">샘플 프로젝트 다운로드: [Azure SQL을 위한 탄력적 DB 도구 - 다중 테넌트 분할된 데이터베이스](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="30deb-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="30deb-122">**Program.cs**</span><span class="sxs-lookup"><span data-stu-id="30deb-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="30deb-123">이 프로젝트는 [Azure SQL을 위한 탄력적 DB 도구 - Entity Framework 통합](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) 에서 설명한 프로젝트에 다중 테넌트 분할된 데이터베이스에 대한 지원을 추가하는 확장 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="30deb-124">위의 다이어그램에서 볼 수 있듯이 테넌트 네 명과 다중 테넌트 분할 데이터베이스 두 개를 사용하여 블로그 및 게시물을 만드는 간단한 콘솔 응용 프로그램을 구축하는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="30deb-125">응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-125">Build and run the application.</span></span> <span data-ttu-id="30deb-126">그러면 탄력적 데이터베이스 도구의 분할된 데이터베이스 맵 관리자가 부트스트랩되고 다음 테스트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="30deb-127">Entity Framework 및 LINQ를 사용하여 새 블로그를 만든 후 각 테넌트에 대한 모든 블로그 표시</span><span class="sxs-lookup"><span data-stu-id="30deb-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="30deb-128">ADO.NET SqlClient를 사용하여 특정 테넌트에 대한 모든 블로그 표시</span><span class="sxs-lookup"><span data-stu-id="30deb-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="30deb-129">잘못된 테넌트에 대한 블로그 삽입을 시도하여 오류가 throw되는지 확인</span><span class="sxs-lookup"><span data-stu-id="30deb-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="30deb-130">분할된 데이터베이스에서 아직 RLS를 설정하지 않았기 때문에 각 테스트에서 다음 문제가 발생합니다. 테넌트가 자신에게 속하지 않은 블로그를 볼 수 있으며 응용 프로그램에서 잘못된 테넌트에 대한 블로그를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="30deb-131">이 문서의 나머지 부분에서는 RLS로 테넌트를 강제 격리하여 이러한 문제를 해결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="30deb-132">두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-132">There are two steps:</span></span> 

1. <span data-ttu-id="30deb-133">**응용 프로그램 계층**: 연결을 연 후 응용 프로그램 코드를 수정하여 SESSION_CONTEXT에서 현재 TenantId를 항상 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="30deb-134">샘플 프로젝트는 이 작업이 이미 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="30deb-135">**데이터 계층**: 각 분할된 데이터베이스에서 SESSION_CONTEXT에 저장된 TenantId에 따라 행을 필터링하는 RLS 보안 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="30deb-136">분할된 데이터베이스 각각에 대해 이 작업을 수행해야 합니다. 그렇지 않으면 다중 테넌트 분할된 데이터베이스의 행이 필터링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="30deb-137">1단계) 응용 프로그램 계층: SESSION_CONTEXT에서 TenantId 설정</span><span class="sxs-lookup"><span data-stu-id="30deb-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="30deb-138">탄력적 데이터베이스 클라이언트 라이브러리의 데이터 종속 라우팅 API를 사용하여 분할된 데이터베이스에 연결된 후에도 RLS 보안 정책에서 다른 테넌트에 속한 행을 필터링할 수 있도록 응용 프로그램에서는 어떤 TenantId가 해당 연결을 사용하고 있는지 데이터베이스에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="30deb-139">이 정보를 전달하는 권장 방법은 [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx)에서 해당 연결의 현재 TenantId를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="30deb-140">(참고: [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx)도 사용할 수 있지만 사용하기 쉬우며 기본적으로 NULL을 반환하고 키-값 쌍을 지원하는 SESSION_CONTEXT가 더 나은 옵션입니다.)</span><span class="sxs-lookup"><span data-stu-id="30deb-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="30deb-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="30deb-141">Entity Framework</span></span>
<span data-ttu-id="30deb-142">Entity Framework를 사용하는 응용 프로그램의 경우 가장 간단한 방법은 [EF DbContext를 사용하는 데이터 종속 라우팅](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext)에 설명된 ElasticScaleContext 재정의 내에서 SESSION_CONTEXT를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="30deb-143">데이터 종속 라우팅을 통해 조정된 연결을 반환하기 전에 SESSION_CONTEXT의 'TenantId'를 해당 연결에 대해 지정된 shardingKey로 설정하는 SqlCommand를 만들어서 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="30deb-144">이 방법을 사용하면 SESSION_CONTEXT를 설정하는 코드를 한 번만 작성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="30deb-145">이제 ElasticScaleContext가 호출될 때마다 SESSION_CONTEXT는 자동으로 지정된 TenantId로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="30deb-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="30deb-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="30deb-147">ADO.NET SqlClient를 사용하는 응용 프로그램에 권장되는 방법은 ShardMap.OpenConnectionForKey() 주위에 래퍼 함수를 생성하는 것입니다. ShardMap.OpenConnectionForKey()는 연결이 반환되기 전에 SESSION_CONTEXT의 'TenantId'를 올바른 Tenantld로 자동적으로 설정해줍니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="30deb-148">SESSION_CONTEXT가 항상 설정되도록 하기 위해 이 래퍼 함수를 사용해서만 연결을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="30deb-149">2단계) 데이터 계층: 행 수준 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="30deb-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="30deb-150">각 테넌트가 액세스할 수 있는 행을 필터링하는 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="30deb-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="30deb-151">응용 프로그램에서 SESSION_CONTEXT를 현재 TenantId로 설정한 후 쿼리하므로 RLS 보안 정책에서 쿼리를 필터링하고 TenantId가 다른 행을 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="30deb-152">RLS는 T-SQL에서 구현됩니다. 사용자 정의 함수에서 액세스 논리를 정의하고, 보안 정책에서 이 함수를 모든 테이블에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="30deb-153">이 프로젝트의 경우 이 함수는 다른 SQL 사용자가 아닌 응용 프로그램이 데이터베이스에 연결되었는지, SESSION_CONTEXT에 저장된 'TenantId'가 지정된 행의 TenantId와 일치하는지만 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="30deb-154">필터 조건자는 이러한 조건을 충족하는 행이 SELECT, UPDATE 및 DELETE 쿼리에 대한 필터를 통과하도록 하며 차단 조건자는 이러한 조건을 위반하는 행이 INSERT 또는 UPDATE되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="30deb-155">SESSION_CONTEXT가 설정되지 않은 경우 NULL을 반환하고 행이 표시되지 않거나 삽입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="30deb-156">RLS를 사용하려면 Visual Studio(SSDT), SSMS 또는 프로젝트에 포함된 PowerShell 스크립트 중 하나를 사용하여 모든 분할된 데이터베이스에서 다음 T-SQL을 실행합니다. 또는 [Elastic Database Jobs](sql-database-elastic-jobs-overview.md)를 사용하는 경우 모든 분할된 데이터베이스에서 이 T-SQL을 자동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="30deb-157">수백 개의 테이블에서 조건자를 추가해야 하는 복잡한 프로젝트의 경우 자동으로 보안 정책을 생성하여 스키마의 모든 테이블에 조건자를 추가하는 도우미 저장 프로시저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="30deb-158">[모든 테이블에 행 수준 보안 적용 – 도우미 스크립트(블로그)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30deb-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="30deb-159">이제 샘플 응용 프로그램을 다시 실행하면 각 테넌트는 자신에게 속한 행만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="30deb-160">또한 응용 프로그램에서는 현재 분할된 데이터베이스에 연결된 테넌트 이외의 다른 테넌트에 속한 행을 삽입할 수 없으며 표시되는 행을 다른 TenantId를 포함하도록 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="30deb-161">응용 프로그램에서 두 작업을 시도하면 DbUpdateException이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="30deb-162">나중에 새 테이블을 추가하는 경우 보안 정책을 변경하고 새 테이블에 필터 및 차단 조건자를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="30deb-163">삽입 시 TenantId를 자동으로 채우도록 기본 제약 조건 추가</span><span class="sxs-lookup"><span data-stu-id="30deb-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="30deb-164">행을 삽입할 때 자동으로 SESSION_CONTEXT에 현재 저장된 값으로 TenantId를 채우도록 각 테이블에 기본 제약 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="30deb-165">예:</span><span class="sxs-lookup"><span data-stu-id="30deb-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="30deb-166">이제 행을 삽입할 때 응용 프로그램에서 TenantId를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="30deb-167">Entity Framework 프로젝트에 기본 제약 조건을 사용하는 경우 EF 데이터 모델에 TenantId 열을 포함하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="30deb-168">Entity Framework 쿼리에서 자동으로 기본값을 제공하는데, 이 기본값은 T-SQL에서 만든 SESSION_CONTEXT를 사용하는 기본 제약 조건을 재정의하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="30deb-169">예를 들어 샘플 프로젝트에서 기본 제약 조건을 사용하려면 DataClasses.cs에서 TenantId를 제거하고(그리고 패키지 관리자 콘솔에서 Add-Migration을 실행하고) 데이터베이스 테이블에만 필드가 있도록 T-SQL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="30deb-170">그러면 데이터 삽입 시 EF에서 잘못된 기본값을 자동으로 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="30deb-171">(선택 사항) 모든 행에 액세스 하려면 "superuser"를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="30deb-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="30deb-172">예를 들면 일부 응용 프로그램은  모든shard안의 모든 tenant가 보고할 수 있게 하거나 데이터베이스간의 이동 테넌트 행에 관련된 shard에서 분할/합병 작업을 수행하기 위해 모든 행에 액세스할 수 있는 “SuperUser”생성을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="30deb-173">이 기능을 사용 하려면 각 분할 데이터베이스에서 새 SQL 사용자 (이 예에서 "superuser")를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="30deb-174">그런 다음 사용자를 모든 행에 액세스할 수 있도록 하는 새 조건자 함수를 사용하여 보안 정책을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="30deb-175">유지 관리</span><span class="sxs-lookup"><span data-stu-id="30deb-175">Maintenance</span></span>
* <span data-ttu-id="30deb-176">**새로운 분할된 데이터베이스 추가**: T-SQL 스크립트를 실행하여 모든 새로운 분할된 데이터베이스에서 RLS를 설정해야 합니다. 그렇지 않으면 분할된 데이터베이스에 대한 쿼리가 필터링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="30deb-177">**새 테이블 추가**: 새 테이블을 만들 때마다 모든 분할된 데이터베이스의 보안 정책에 필터 및 차단 조건자를 추가해야 합니다. 그렇지 않으면 새 테이블에 대한 쿼리가 필터링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="30deb-178">[새로 만든 테이블에 자동으로 행 수준 보안 적용(블로그)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx)에 설명된 것처럼 DDL 트리거를 사용하여 이 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="30deb-179">요약</span><span class="sxs-lookup"><span data-stu-id="30deb-179">Summary</span></span>
<span data-ttu-id="30deb-180">탄력적 데이터베이스 도구와 행 수준 보안을 함께 사용하면 다중 테넌트 및 단일 테넌트 분할된 데이터베이스를 모두 지원하여 응용 프로그램의 데이터 계층을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="30deb-181">다중 테넌트 분할된 데이터베이스를 사용하여 데이터를 보다 효율적으로 저장할 수 있고(특히 테넌트 수는 많은데 데이터 행은 적은 경우), 단일 테넌트 분할된 데이터베이스를 사용하여 성능 및 격리 요구 사항이 엄격한 프리미엄 테넌트를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30deb-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="30deb-182">자세한 내용은 [행 수준 보안 참조](https://msdn.microsoft.com/library/dn765131)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30deb-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="30deb-183">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="30deb-183">Additional resources</span></span>
* [<span data-ttu-id="30deb-184">Azure 탄력적 풀이란?</span><span class="sxs-lookup"><span data-stu-id="30deb-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="30deb-185">Azure SQL 데이터베이스를 사용하여 확장</span><span class="sxs-lookup"><span data-stu-id="30deb-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="30deb-186">Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="30deb-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="30deb-187">Azure AD 및 OpenID Connect를 사용하여 다중 테넌트 앱에서 인증</span><span class="sxs-lookup"><span data-stu-id="30deb-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="30deb-188">Tailspin 설문 조사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30deb-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="30deb-189">질문 및 기능 요청</span><span class="sxs-lookup"><span data-stu-id="30deb-189">Questions and Feature Requests</span></span>
<span data-ttu-id="30deb-190">의문 사항이 있으면 [SQL Database 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)에 문의하고, 기능에 대한 요청이 있는 경우 해당 기능을 [SQL Database 사용자 의견 포럼](https://feedback.azure.com/forums/217321-sql-database/)에 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="30deb-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


