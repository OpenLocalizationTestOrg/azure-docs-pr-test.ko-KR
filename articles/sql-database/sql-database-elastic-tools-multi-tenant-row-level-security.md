---
title: "탄력적 데이터베이스 도구와 행 수준 보안 aaaMulti 테 넌 트 응용 프로그램"
description: "어떻게 toouse 탄력적 데이터베이스 도구와 함께 행 수준 보안 toobuild와 Azure SQL 데이터베이스를 지 원하는 다중 테 넌 트 분할 영역에 확장성이 높은 데이터 계층 응용 프로그램에 대해 알아봅니다."
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
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="1df9b-103">탄력적 데이터베이스 도구 및 행 수준 보안을 제공하는 다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1df9b-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="1df9b-104">[탄력적 데이터베이스 도구](sql-database-elastic-scale-get-started.md) 및 [행 수준 보안 (RLS)](https://msdn.microsoft.com/library/dn765131) 강력한 유연 하 게 하 고 효율적으로 확장할 다중 테 넌 트 응용 프로그램을 Azure SQL 데이터베이스의 데이터 계층 hello에 대 한 기능 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="1df9b-105">자세한 내용은 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1df9b-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="1df9b-106">이 문서에서는 설명 방법을 toouse 이러한 기술 함께 toobuild로 지 원하는 다중 테 넌 트 분할 영역을 사용 하 여 확장성이 높은 데이터 계층 응용 프로그램을 **ADO.NET SqlClient** 및/또는 **EntityFramework**.</span><span class="sxs-lookup"><span data-stu-id="1df9b-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="1df9b-107">**탄력적 데이터베이스 도구** 아웃 Azure 서비스 템플릿과.NET 라이브러리 집합을 사용 하는 업계 표준 분할 관행을 통해 응용 프로그램의 hello 데이터 계층 개발자 tooscale 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="1df9b-108">자동화 하 고 다양 한 일반적으로 분할 될 때까지 연관 된 hello 인프라 작업을 간소화를 통해 hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 분할 된 데이터베이스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="1df9b-109">**행 수준 보안** hello 같은 보안 정책을 toofilter 쿼리 실행 toohello 테 넌 트에 속하지 않는 행을 사용 하 여 데이터베이스에서 여러 테 넌 트에 대 한 개발자 toostore 데이터 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="1df9b-110">Hello 데이터베이스 내부에서 RLS로 액세스 논리를 중앙 집중화 대신 hello 응용 프로그램에서 유지 관리를 단순화 하 고 응용 프로그램의 코드 베이스 hello 오류 위험을 줄어듭니다 보다 커집니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="1df9b-111">이 사용 하 여 함께 기능, 응용 프로그램에 다중 테 넌 트에서 hello에 동일 데이터를 저장 하 여 비용 절감 및 효율성 향상에서 얻을 수 분할 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="1df9b-112">Hello 동시 여전히 응용 프로그램에 hello 유연성 toooffer isolated, 다중 테 넌 트 분할 영역 테 넌 트 간에 같은 리소스 배포를 보장 하지 않지만 이후 더 엄격한 성능 보장 해야 하는 "프리미엄" 테 넌 트에 대 한 단일 테 넌 트 분할 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="1df9b-113">즉, 탄력적 데이터베이스 클라이언트 라이브러리를 hello [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) Api 해당 분할 키 (일반적으로 "TenantId")가 포함 된 테 넌 트 toohello 올바른 분할 데이터베이스를 자동으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="1df9b-114">연결 되 면 테 넌 트의 TenantId를 포함 하는 행만 액세스할 수 있도록 hello 데이터베이스 내에서 RLS 보안 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="1df9b-115">모든 테이블에 속하는 tooeach 테 넌 트 행 TenantId 열 tooindicate 포함을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![앱 아키텍처 블로그][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="1df9b-117">Hello 샘플 프로젝트를 다운로드</span><span class="sxs-lookup"><span data-stu-id="1df9b-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1df9b-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1df9b-118">Prerequisites</span></span>
* <span data-ttu-id="1df9b-119">Visual Studio 2012 이상 사용</span><span class="sxs-lookup"><span data-stu-id="1df9b-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="1df9b-120">Azure SQL 데이터베이스 3개 생성</span><span class="sxs-lookup"><span data-stu-id="1df9b-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="1df9b-121">샘플 프로젝트 다운로드: [Azure SQL을 위한 탄력적 DB 도구 - 다중 테넌트 분할된 데이터베이스](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="1df9b-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="1df9b-122">Hello 시작 부분에서 데이터베이스에 대 한 hello 정보를 입력 **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="1df9b-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="1df9b-123">이 프로젝트 하나에 설명 된 hello 확장 [엔터티 프레임 워크 통합-Azure sql 탄력적 DB 도구](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) 다중 테 넌 트 분할 데이터베이스에 대 한 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="1df9b-124">4 명의 테 넌 트 및 hello 위의 다이어그램에에서 나타난 것 처럼 두 개의 다중 테 넌 트 분할 데이터베이스와 함께 블로그 및 게시물을 만들기 위한 간단한 콘솔 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="1df9b-125">빌드하고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-125">Build and run hello application.</span></span> <span data-ttu-id="1df9b-126">Hello 탄력적 데이터베이스 도구 shard map manager 및 다음 테스트 실행된 hello를 부트스트랩 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="1df9b-127">Entity Framework 및 LINQ를 사용하여 새 블로그를 만든 후 각 테넌트에 대한 모든 블로그 표시</span><span class="sxs-lookup"><span data-stu-id="1df9b-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="1df9b-128">ADO.NET SqlClient를 사용하여 특정 테넌트에 대한 모든 블로그 표시</span><span class="sxs-lookup"><span data-stu-id="1df9b-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="1df9b-129">오류가 발생 하는 hello 잘못 된 테 넌 트 tooverify에 대 한 블로그 tooinsert를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1df9b-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="1df9b-130">RLS hello 분할 데이터베이스에서 아직 활성화 되지 않은 때문에 이러한 테스트 각각의 작업에서 문제가 발견 되는 공지: 테 넌 트 수 toosee 블로그 toothem, 속해 있지 않은 되며 hello 응용 프로그램이 블로그 hello 잘못 된 테 넌 트에 대 한 삽입에서 차단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="1df9b-131">hello이 문서의 나머지 부분에 설명 방법을 tooresolve 이러한 문제를 적용 하 여 테 넌 트 RLS로 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="1df9b-132">두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-132">There are two steps:</span></span> 

1. <span data-ttu-id="1df9b-133">**응용 프로그램 계층**: hello 응용 프로그램 코드를 수정 tooalways 집합 연결을 연 후 SESSION_CONTEXT hello에 현재 TenantId hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="1df9b-134">hello 샘플 프로젝트에 이미이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="1df9b-135">**데이터 계층**: 각 분할 데이터베이스 toofilter SESSION_CONTEXT에 저장 된 hello TenantId 기준으로 행에에서는 RLS 보안 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="1df9b-136">필요 toodo 분할 데이터베이스 각각에 대해, 그렇지 않으면 다중 테 넌 트 분할 영역에 행 필터링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="1df9b-137">1 단계) 응용 프로그램 계층: SESSION_CONTEXT hello에 있는 tenantid가 설정</span><span class="sxs-lookup"><span data-stu-id="1df9b-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="1df9b-138">RLS 보안 정책을 행을 필터링 할 수 있도록 어떤 TenantId 해당 연결을 사용 하는 hello 탄력적 데이터베이스 클라이언트 라이브러리의 데이터 종속 라우팅 Api hello 응용 프로그램 계속 사용 하 여 연결 tooa 분할 데이터베이스 tootell hello 데이터베이스가 필요한 후 속하는 tooother 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="1df9b-139">이 정보는 권장된 방법을 toopass hello toostore hello hello에는 해당 연결에 대 한 현재 TenantId [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="1df9b-140">(참고: 또는 사용할 수 있습니다 [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), 하지만 SESSION_CONTEXT는 편이 더 나은지 있기 때문에 보다 쉽게 toouse, 기본적으로 NULL을 반환 합니다. 키-값 쌍을 지원 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1df9b-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="1df9b-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1df9b-141">Entity Framework</span></span>
<span data-ttu-id="1df9b-142">Entity Framework를 사용 하 여 응용 프로그램에 대 한 hello는 가장 쉬운 방법은 tooset hello에 설명 된 hello ElasticScaleContext 재정의 내 SESSION_CONTEXT [데이터 종속 라우팅 EF DbContext를 사용 하 여](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="1df9b-143">데이터 종속 라우팅을 통해 중개 hello 연결을 반환 하기 전에 만들기 하 고 해당 연결에 대해 지정 된 hello SESSION_CONTEXT toohello shardingkey에서 'TenantId'를 설정 하는 SqlCommand를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="1df9b-144">이 이렇게 하면 toowrite 코드 tooset hello SESSION_CONTEXT 되 면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

<span data-ttu-id="1df9b-145">이제 SESSION_CONTEXT hello로 자동으로 설정 된 hello ElasticScaleContext가 호출 될 때마다 TenantId를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="1df9b-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="1df9b-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="1df9b-147">주위 ShardMap.OpenConnectionForKey() 'TenantId' hello SESSION_CONTEXT toohello에서 자동으로 설정 하는 래퍼 함수를 반환 하기 전에 TenantId 수정 응용 프로그램을 사용 하 여 ADO.NET SqlClient hello 권장 방법은 toocreate에 대 한는 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="1df9b-148">SESSION_CONTEXT 항상 설정 된 tooensure만 열어야이 래퍼 함수를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="1df9b-149">2단계) 데이터 계층: 행 수준 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1df9b-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="1df9b-150">보안 정책 toofilter hello 각 테 넌 트에 액세스할 수는 행 만들기</span><span class="sxs-lookup"><span data-stu-id="1df9b-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="1df9b-151">Hello 응용 프로그램은와 SESSION_CONTEXT를 설정 하는 했으므로 hello 현재 TenantId를 쿼리 하기 전에 RLS 보안 정책 수 쿼리를 필터링 하 고 다른 TenantId이 있는 행을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="1df9b-152">RLS는 T-SQL에서 구현: hello 액세스 논리를 정의 하는 사용자 정의 함수 및 보안 정책 함수 tooany 개수의 테이블을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="1df9b-153">이 프로젝트에 대 한 hello 함수는 단순히 확인 hello 아니라 응용 프로그램 (다른 SQL 사용자)는 연결 된 toohello 데이터베이스 'TenantId' hello SESSION_CONTEXT에에서 저장 된 해당 hello hello 지정된 된 행의 TenantId와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="1df9b-154">필터 조건자를 사용 하면 SELECT, UPDATE 및 DELETE 쿼리의; hello 필터를 통해 이러한 조건을 toopass를 만족 하는 행 및는 block 조건자는 INSERTed 또는 UPDATEd 없도록 이러한 조건을 위반 하는 행 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="1df9b-155">SESSION_CONTEXT 설정 되지 않은 경우 NULL이 고 행이 없는 삽입 표시 되거나 수 toobe 됩니다 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="1df9b-156">tooenable RLS 실행 하거나 Visual Studio (SSDT), SSMS를 사용 하 여 모든 분할 영역에서 다음 T-SQL hello 또는 hello 프로젝트에 포함 된 PowerShell 스크립트를 환영 (사용 하는 경우 또는 [탄력적 데이터베이스 작업](sql-database-elastic-jobs-overview.md), tooautomate 실행을 사용할 수 있습니다 이 T-SQL의 모든 분할 영역에):</span><span class="sxs-lookup"><span data-stu-id="1df9b-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="1df9b-157">수백 개에서 tooadd hello 조건자를 필요로 하는 보다 복잡 한 프로젝트에 대 한 스키마의 모든 테이블에 조건자를 추가 하는 보안 정책을 자동으로 생성 하는 도우미 저장 프로시저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="1df9b-158">참조 [행 수준 보안 적용 tooall 테이블-도우미 스크립트 (블로그)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="1df9b-159">이제 hello 샘플 응용 프로그램을 다시 실행 하는 경우 테 넌 트가 됩니다 수 toosee toothem 속하는 행만 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="1df9b-160">또한 hello 응용 프로그램 hello 한 현재 연결 된 toohello 분할 데이터베이스 이외의 tootenants 속하는 행을 삽입할 수 없습니다 및 표시 되는 행 toohave 다른 TenantId를 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="1df9b-161">Hello 응용 프로그램을 toodo 하거나 가져오려고 한 DbUpdateException 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="1df9b-162">나중에 새 테이블을 추가 하는 경우 단순히 ALTER hello 보안 정책 및 hello 새 테이블에서 필터 조건자와 차단 조건자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="1df9b-163">기본 추가 제약 조건 tooautomatically TenantId 삽입에 대 한 채우기</span><span class="sxs-lookup"><span data-stu-id="1df9b-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="1df9b-164">기본값을 넣을 수 있습니다 각 테이블 tooautomatically에 제약 조건을 채울 hello로 TenantId hello 현재 행을 삽입할 때 SESSION_CONTEXT에 저장 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="1df9b-165">예:</span><span class="sxs-lookup"><span data-stu-id="1df9b-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="1df9b-166">이제 hello 응용 프로그램 행을 삽입할 때 toospecify는 TenantId를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="1df9b-167">Entity Framework 프로젝트에 대 한 기본 제약 조건을 사용 하면 EF 데이터 모델에 hello TenantId 열을 포함 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="1df9b-168">Entity Framework 쿼리는 자동으로 hello 기본 제약 조건 T-SQL에서 만든 SESSION_CONTEXT를 사용 하는 재정의 하는 기본값을 제공 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="1df9b-169">toouse default 제약 조건 hello로 샘플 프로젝트, 예를 들어, TenantId DataClasses.cs (및 hello 패키지 관리자 콘솔에서에서 실행된 Add-migration)에서 제거 해야 하 고 필드 hello를 사용 하 여 T-SQL tooensure hello 데이터베이스 테이블에만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="1df9b-170">그러면 데이터 삽입 시 EF에서 잘못된 기본값을 자동으로 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="1df9b-171">(선택 사항) 모든 행 "superuser" tooaccess을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1df9b-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="1df9b-172">일부 응용 프로그램 간의 모든 분할 영역에 있는 모든 테 넌 트 또는 테 넌 트 행 데이터베이스 간에 이동와 관련 된 분할 된 데이터베이스에서 분할/병합 작업 tooperform 보고가 순서 tooenable의 예를 들어, 모든 행에 액세스할 수 있는 "superuser" toocreate를 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="1df9b-173">tooenable이 각 분할 데이터베이스에서 새 SQL 사용자 (이 예제의 "superuser")을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="1df9b-174">그런 다음이 사용자 tooaccess 모든 행을 허용 하는 새 조건자 함수를 사용 하 여 hello 보안 정책 변경:</span><span class="sxs-lookup"><span data-stu-id="1df9b-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="1df9b-175">유지 관리</span><span class="sxs-lookup"><span data-stu-id="1df9b-175">Maintenance</span></span>
* <span data-ttu-id="1df9b-176">**새 분할 영역이 추가**: 새로운 모든 분할 영역에 hello T-SQL 스크립트 tooenable RLS를 실행 해야, 그렇지 않으면 이러한 분할 된이 데이터베이스에 대 한 쿼리는 필터링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="1df9b-177">**새 테이블을 추가**: 필터를 추가 하 고 새 테이블을 만들 때마다 모든 분할 영역에 보안 정책을 조건자 toohello를 차단 해야, 그렇지 않으면 hello 새 테이블에 대 한 쿼리는 필터링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="1df9b-178">자동화할 수 있습니다는 DDL 트리거를 사용 하 여에 설명 된 대로 [행 수준 보안 적용 자동으로 toonewly 테이블을 만들지 (블로그)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="1df9b-179">요약</span><span class="sxs-lookup"><span data-stu-id="1df9b-179">Summary</span></span>
<span data-ttu-id="1df9b-180">탄력적 데이터베이스 도구 및 행 수준 보안이 사용 되는 함께 tooscale 다중 테 넌 트 및 단일 테 넌 트 모두 분할 된 데이터베이스를 지 원하는 데이터 계층 응용 프로그램의 초과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="1df9b-181">다중 테 넌 트 분할만 포함 되도록 사용된 toostore 데이터 보다 효율적으로 (특히에서 많은 수의 테 넌 트가 있는 경우 데이터의 행을 몇 개만), 단일 테 넌 트 분할 된 데이터베이스는 보다 엄격한 성능 및 격리에 사용 되는 toosupport premium 테 넌 트 수 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="1df9b-182">자세한 내용은 [행 수준 보안 참조](https://msdn.microsoft.com/library/dn765131)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1df9b-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1df9b-183">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1df9b-183">Additional resources</span></span>
* [<span data-ttu-id="1df9b-184">Azure 탄력적 풀이란?</span><span class="sxs-lookup"><span data-stu-id="1df9b-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="1df9b-185">Azure SQL 데이터베이스를 사용하여 확장</span><span class="sxs-lookup"><span data-stu-id="1df9b-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="1df9b-186">Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="1df9b-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="1df9b-187">Azure AD 및 OpenID Connect를 사용하여 다중 테넌트 앱에서 인증</span><span class="sxs-lookup"><span data-stu-id="1df9b-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="1df9b-188">Tailspin 설문 조사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1df9b-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="1df9b-189">질문 및 기능 요청</span><span class="sxs-lookup"><span data-stu-id="1df9b-189">Questions and Feature Requests</span></span>
<span data-ttu-id="1df9b-190">질문에 게 연락 하세요 hello에 toous [SQL 데이터베이스 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) 기능 요청에 대 한 하십시오 추가할 toohello [SQL 데이터베이스 피드백 포럼](https://feedback.azure.com/forums/217321-sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df9b-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


