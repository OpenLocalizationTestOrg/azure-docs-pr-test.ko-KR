---
title: "Dapper와 aaaUsing 탄력적 데이터베이스 클라이언트 라이브러리 | Microsoft Docs"
description: "Dapper과 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a><span data-ttu-id="1fd69-103">Dapper과 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="1fd69-103">Using elastic database client library with Dapper</span></span>
<span data-ttu-id="1fd69-104">이 문서는 Dapper toobuild 응용 프로그램에 의존 하지만 tooembrace을 할 수도 있는 개발자를 위한 [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md) 데이터 계층 분할 tooscale 아웃을 구현 하는 toocreate 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-104">This document is for developers that rely on Dapper toobuild applications, but also want tooembrace [elastic database tooling](sql-database-elastic-scale-introduction.md) toocreate applications that implement sharding tooscale-out their data tier.</span></span>  <span data-ttu-id="1fd69-105">이 문서는 탄력적 데이터베이스 도구와 함께 필요한 toointegrate Dapper 기반 응용 프로그램의 hello 변경 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-105">This document illustrates hello changes in Dapper-based applications that are necessary toointegrate with elastic database tools.</span></span> <span data-ttu-id="1fd69-106">Hello 탄력적 데이터베이스 분할 관리 및 데이터에 종속 된 구성에 집중은 Dapper와 라우팅입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-106">Our focus is on composing hello elastic database shard management and data dependent routing with Dapper.</span></span> 

<span data-ttu-id="1fd69-107">**샘플 코드**: [Azure SQL 데이터베이스-Dapper 통합에 대한 탄력적 데이터베이스 도구](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span><span class="sxs-lookup"><span data-stu-id="1fd69-107">**Sample Code**: [Elastic database tools for Azure SQL Database - Dapper integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span></span>

<span data-ttu-id="1fd69-108">통합 **Dapper** 및 **DapperExtensions** hello로 Azure SQL 데이터베이스 탄력적 데이터베이스 클라이언트 라이브러리 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-108">Integrating **Dapper** and **DapperExtensions** with hello elastic database client library for Azure SQL Database is easy.</span></span> <span data-ttu-id="1fd69-109">응용 프로그램 데이터 종속 라우팅 hello 만들기를 변경 하 고 새로운를 열 여 צ ְ ײ [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello에서 호출 [클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/dn765902.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-109">Your applications can use data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call from hello [client library](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span></span> <span data-ttu-id="1fd69-110">새 연결이 만들어지고 열려 있는 프로그램 응용 프로그램 tooonly의 변경 내용을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-110">This limits changes in your application tooonly where new connections are created and opened.</span></span> 

## <a name="dapper-overview"></a><span data-ttu-id="1fd69-111">Dapper 개요</span><span class="sxs-lookup"><span data-stu-id="1fd69-111">Dapper overview</span></span>
<span data-ttu-id="1fd69-112">**Dapper** 는 개체 관계형 매퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-112">**Dapper** is an object-relational mapper.</span></span> <span data-ttu-id="1fd69-113">.NET 개체 응용 프로그램 tooa 관계형 데이터베이스에서 (또는 그 반대로) 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-113">It maps .NET objects from your application tooa relational database (and vice versa).</span></span> <span data-ttu-id="1fd69-114">hello 예제 코드의 첫 번째 부분 hello Dapper 기반 응용 프로그램과 함께 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통합 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-114">hello first part of hello sample code illustrates how you can integrate hello elastic database client library with Dapper-based applications.</span></span> <span data-ttu-id="1fd69-115">hello hello 예제 코드의 두 번째 부분에서는 어떻게 toointegrate Dapper와 DapperExtensions 둘 다 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1fd69-115">hello second part of hello sample code illustrates how toointegrate when using both Dapper and DapperExtensions.</span></span>  

<span data-ttu-id="1fd69-116">Dapper hello 매퍼 기능은 제출 하는 중 T-SQL 문을 실행 하거나 hello 데이터베이스 쿼리를 단순화 하는 데이터베이스 연결에 확장 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-116">hello mapper functionality in Dapper provides extension methods on database connections that simplify submitting T-SQL statements for execution or querying hello database.</span></span> <span data-ttu-id="1fd69-117">예를 들어, Dapper를 사용 하면.NET 개체 및에 대 한 SQL 문의 hello 매개 변수 간의 쉽게 toomap **Execute** 호출 또는 SQL 쿼리를 사용 하 여.NET 개체로 tooconsume hello 결과 **쿼리**Dapper에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-117">For instance, Dapper makes it easy toomap between your .NET objects and hello parameters of SQL statements for **Execute** calls, or tooconsume hello results of your SQL queries into .NET objects using **Query** calls from Dapper.</span></span> 

<span data-ttu-id="1fd69-118">DapperExtensions을 사용할 경우 tooprovide hello SQL 문을 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-118">When using DapperExtensions, you no longer need tooprovide hello SQL statements.</span></span> <span data-ttu-id="1fd69-119">와 같은 확장 메서드 **GetList** 또는 **삽입** hello 데이터베이스 연결을 통해 hello SQL 문을 만드는 hello 내부적입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-119">Extensions methods such as **GetList** or **Insert** over hello database connection create hello SQL statements behind hello scenes.</span></span>

<span data-ttu-id="1fd69-120">Dapper와 DapperExtensions 또 다른 이점은 응용 프로그램 컨트롤의 hello hello hello 데이터베이스 연결 만들기는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-120">Another benefit of Dapper and also DapperExtensions is that hello application controls hello creation of hello database connection.</span></span> <span data-ttu-id="1fd69-121">이렇게 하면 브로커 데이터베이스 shardlet toodatabases의 hello 매핑을 기반으로 연결 하는 hello 탄력적 데이터베이스 클라이언트 라이브러리와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-121">This helps interact with hello elastic database client library which brokers database connections based on hello mapping of shardlets toodatabases.</span></span>

<span data-ttu-id="1fd69-122">tooget hello Dapper 어셈블리 참조 [net Dapper 점](http://www.nuget.org/packages/Dapper/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-122">tooget hello Dapper assemblies, see [Dapper dot net](http://www.nuget.org/packages/Dapper/).</span></span> <span data-ttu-id="1fd69-123">Hello Dapper 확장에 대 한 참조 [DapperExtensions](http://www.nuget.org/packages/DapperExtensions)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-123">For hello Dapper extensions, see [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span></span>

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a><span data-ttu-id="1fd69-124">Hello 탄력적 데이터베이스 클라이언트 라이브러리 개요</span><span class="sxs-lookup"><span data-stu-id="1fd69-124">A quick Look at hello elastic database client library</span></span>
<span data-ttu-id="1fd69-125">Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하면 호출 응용 프로그램 데이터의 파티션을 정의할 *shardlet* 매핑하십시오 toodatabases, 및 식별 하 여 *분할 키*합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-125">With hello elastic database client library, you define partitions of your application data called *shardlets* , map them toodatabases, and identify them by *sharding keys*.</span></span> <span data-ttu-id="1fd69-126">데이터베이스는 필요한 수만큼 포함할 수 있으며 이러한 데이터베이스에 대해 shardlet을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-126">You can have as many databases as you need and distribute your shardlets across these databases.</span></span> <span data-ttu-id="1fd69-127">분할 키 값 toohello 데이터베이스의 hello 매핑 hello 라이브러리의 Api에서 제공 하는 분할 맵을로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-127">hello mapping of sharding key values toohello databases is stored by a shard map provided by hello library’s APIs.</span></span> <span data-ttu-id="1fd69-128">이 기능을 **분할된 데이터베이스 맵 관리**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-128">This capability is called **shard map management**.</span></span> <span data-ttu-id="1fd69-129">분할 키를 전송 하는 요청에 대 한 데이터베이스 연결의 hello 브로커로 hello 분할 맵은 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-129">hello shard map also serves as hello broker of database connections for requests that carry a sharding key.</span></span> <span data-ttu-id="1fd69-130">이 기능은 참조 tooas **데이터 종속 라우팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-130">This capability is referred tooas **data dependent routing**.</span></span>

![분할된 데이터베이스 맵과 데이터 종속 라우팅][1]

<span data-ttu-id="1fd69-132">hello shard map manager hello 데이터베이스에서 shardlet 동시 관리 작업 중인 경우 발생할 수 있는 shardlet 데이터에 일관성이 없는 뷰에서 사용자가 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-132">hello shard map manager protects users from inconsistent views into shardlet data that can occur when concurrent shardlet management operations are happening on hello databases.</span></span> <span data-ttu-id="1fd69-133">따라서 toodo hello 라이브러리를 사용 하 여 빌드한 응용 프로그램에 대 한 분할 맵을 브로커 hello 데이터베이스 연결을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-133">toodo so, hello shard maps broker hello database connections for an application built with hello library.</span></span> <span data-ttu-id="1fd69-134">분할 관리 작업 hello shardlet에 영향을 줄 수, 하는 경우 이렇게 하면 hello 분할 맵 기능 tooautomatically kill 데이터베이스 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-134">When shard management operations could impact hello shardlet, this allows hello shard map functionality tooautomatically kill a database connection.</span></span> 

<span data-ttu-id="1fd69-135">Toouse hello Dapper에 대 한 hello 전통적인 방법 toocreate 연결을 사용 하는 대신 필요 [OpenConnectionForKey 메서드](http://msdn.microsoft.com/library/azure/dn824099.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-135">Instead of using hello traditional way toocreate connections for Dapper, we need toouse hello [OpenConnectionForKey method](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span></span> <span data-ttu-id="1fd69-136">이렇게 하면 모든 hello 유효성 검사를 수행 하 고 분할 된 데이터베이스 간에 데이터를 이동할 때 연결을 올바르게 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-136">This ensures that all hello validation takes place and connections are managed properly when any data moves between shards.</span></span>

### <a name="requirements-for-dapper-integration"></a><span data-ttu-id="1fd69-137">Dapper 통합을 위한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1fd69-137">Requirements for Dapper integration</span></span>
<span data-ttu-id="1fd69-138">Hello 탄력적 데이터베이스 클라이언트 라이브러리와 hello Dapper Api를 사용할 때는 다음과 같은 속성 tooretain hello 원하는:</span><span class="sxs-lookup"><span data-stu-id="1fd69-138">When working with both hello elastic database client library and hello Dapper APIs, we want tooretain hello following properties:</span></span>

* <span data-ttu-id="1fd69-139">**확장**: tooadd 또는 hello 분할 응용 프로그램의 용량 요구 hello에 대 한 필요에 따라 hello 응용 프로그램의 hello 데이터 계층에서 데이터베이스를 제거 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-139">**Scaleout**: We want tooadd or remove databases from hello data tier of hello sharded application as necessary for hello capacity demands of hello application.</span></span> 
* <span data-ttu-id="1fd69-140">**일관성**: 응용 프로그램은 분할을 사용 하 여 확장할 이후 tooperform 데이터 종속 라우팅 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-140">**Consistency**: Since our application is scaled out using sharding, we need tooperform data dependent routing.</span></span> <span data-ttu-id="1fd69-141">따라서 toouse hello 데이터 종속 라우팅 기능을 hello 라이브러리 toodo 하려고합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-141">We want toouse hello Data dependent routing capabilities of hello library toodo so.</span></span> <span data-ttu-id="1fd69-142">특히, 원하는 tooretain hello 유효성 검사 하 고 일관성 순서 tooavoid 손상이 나 잘못 된 쿼리 결과의 hello shard map 관리자를 통해 조정 된 연결에서 제공 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-142">In particular, we want tooretain hello validation and consistency guarantees provided by connections that are brokered through hello shard map manager in order tooavoid corruption or wrong query results.</span></span> <span data-ttu-id="1fd69-143">이렇게 하면 해당 연결 tooa shardlet을 지정 된 거부 또는 (예를 들어) hello shardlet은 분할/병합 Api를 사용 하 여 현재 이동된 tooa 다른 분할 하는 경우 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-143">This ensures that connections tooa given shardlet are rejected or stopped if (for instance) hello shardlet is currently moved tooa different shard using Split/Merge APIs.</span></span>
* <span data-ttu-id="1fd69-144">**개체의 매핑**: Dapper tootranslate hello 응용 프로그램의 클래스 및 기본 데이터베이스 구조 hello 사이 제공 하는 hello 매핑의 tooretain hello 편의 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-144">**Object Mapping**: We want tooretain hello convenience of hello mappings provided by Dapper tootranslate between classes in hello application and hello underlying database structures.</span></span> 

<span data-ttu-id="1fd69-145">hello 다음 섹션에서는 이러한 요구 사항 기반으로 하는 응용 프로그램에 대 한 지침 **Dapper** 및 **DapperExtensions**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-145">hello following section provides guidance for these requirements for applications based on **Dapper** and **DapperExtensions**.</span></span>

## <a name="technical-guidance"></a><span data-ttu-id="1fd69-146">기술 지침</span><span class="sxs-lookup"><span data-stu-id="1fd69-146">Technical Guidance</span></span>
### <a name="data-dependent-routing-with-dapper"></a><span data-ttu-id="1fd69-147">Dapper를 사용한 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="1fd69-147">Data dependent routing with Dapper</span></span>
<span data-ttu-id="1fd69-148">Dapper와 hello 응용 프로그램은 일반적으로 만들고 hello 연결 toohello 기본 데이터베이스 열에 대 한 책임 지.</span><span class="sxs-lookup"><span data-stu-id="1fd69-148">With Dapper, hello application is typically responsible for creating and opening hello connections toohello underlying database.</span></span> <span data-ttu-id="1fd69-149">T 형식이 hello 응용 프로그램에 제공한, Dapper 쿼리 결과 반환 화 Dapper 유형의.NET 컬렉션에서 화 유형의 hello T-SQL 결과 행 toohello 개체 hello 매핑을 수행 마찬가지로, Dapper SQL 값 또는 데이터 조작 언어 (DML) 문에 대 한 매개 변수를.NET 개체를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-149">Given a type T by hello application, Dapper returns query results as .NET collections of type T. Dapper performs hello mapping from hello T-SQL result rows toohello objects of type T. Similarly, Dapper maps .NET objects into SQL values or parameters for data manipulation language (DML) statements.</span></span> <span data-ttu-id="1fd69-150">일반 hello에 대 한 확장 메서드를 통해이 기능을 제공 하는 Dapper [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello ADO.NET SQL 클라이언트 라이브러리에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-150">Dapper offers this functionality via extension methods on hello regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object from hello ADO .NET SQL Client libraries.</span></span> <span data-ttu-id="1fd69-151">탄력적인 확장 Api hello DDR이 반환한 SQL 연결 hello 일반도 있습니다. [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-151">hello SQL connection returned by hello Elastic Scale APIs for DDR are also regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects.</span></span> <span data-ttu-id="1fd69-152">이 통해 toodirectly 사용 Dapper 확장 hello 클라이언트 라이브러리의 DDR API에서 반환 하는 hello 형식에 대해 간단한 SQL 클라이언트 연결은도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-152">This allows us toodirectly use Dapper extensions over hello type returned by hello client library’s DDR API, as it is also a simple SQL Client connection.</span></span>

<span data-ttu-id="1fd69-153">이러한 결과이 따르면 Dapper에 대 한 hello 탄력적 데이터베이스 클라이언트 라이브러리에서 조정 된 간단한 toouse 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-153">These observations make it straightforward toouse connections brokered by hello elastic database client library for Dapper.</span></span>

<span data-ttu-id="1fd69-154">이 코드 예제 (샘플 약관과 hello)에 hello 응용 프로그램 toohello 라이브러리 toobroker hello 연결 toohello 오른쪽 분할 hello 분할 키가 제공한 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-154">This code example (from hello accompanying sample) illustrates hello approach where hello sharding key is provided by hello application toohello library toobroker hello connection toohello right shard.</span></span>   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

<span data-ttu-id="1fd69-155">hello 호출 toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API hello 기본 만들기 및 SQL 클라이언트 연결 열기를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-155">hello call toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API replaces hello default creation and opening of a SQL Client connection.</span></span> <span data-ttu-id="1fd69-156">hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출 데이터 종속 라우팅에 필요한 hello 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-156">hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call takes hello arguments that are required for data dependent routing:</span></span> 

* <span data-ttu-id="1fd69-157">hello shard map tooaccess hello 데이터 종속 라우팅 인터페이스</span><span class="sxs-lookup"><span data-stu-id="1fd69-157">hello shard map tooaccess hello data dependent routing interfaces</span></span>
* <span data-ttu-id="1fd69-158">hello 분할 키 tooidentify hello shardlet</span><span class="sxs-lookup"><span data-stu-id="1fd69-158">hello sharding key tooidentify hello shardlet</span></span>
* <span data-ttu-id="1fd69-159">hello 자격 증명 (사용자 이름 및 암호) tooconnect toohello 분할</span><span class="sxs-lookup"><span data-stu-id="1fd69-159">hello credentials (user name and password) tooconnect toohello shard</span></span>

<span data-ttu-id="1fd69-160">hello shard map 개체 분할 키를 제공 하는 hello에 대 한 hello shardlet을 보유 하는 연결 toohello 분할 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-160">hello shard map object creates a connection toohello shard that holds hello shardlet for hello given sharding key.</span></span> <span data-ttu-id="1fd69-161">hello 탄력적 데이터베이스 클라이언트 Api에는 또한 일관성을 보장 하는 hello 연결 tooimplement을 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-161">hello elastic database client APIs also tag hello connection tooimplement its consistency guarantees.</span></span> <span data-ttu-id="1fd69-162">Hello 이후 호출을 통해서도[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 일반 SQL 클라이언트 연결 개체를 후속 호출 toohello hello 반환 **Execute** Dapper 다음과에서 확장 메서드는 표준 Dapper hello 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-162">Since hello call too[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) returns a regular SQL Client connection object, hello subsequent call toohello **Execute** extension method from Dapper follows hello standard Dapper practice.</span></span>

<span data-ttu-id="1fd69-163">쿼리 작업 거의 동일한 hello 방법-처음 열면 사용 하 여 hello 연결 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 클라이언트 API에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-163">Queries work very much hello same way - you first open hello connection using [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) from hello client API.</span></span> <span data-ttu-id="1fd69-164">다음 SQL 쿼리 hello 정규 Dapper 확장 메서드 toomap hello 결과 사용 하 여.NET 개체로:</span><span class="sxs-lookup"><span data-stu-id="1fd69-164">Then you use hello regular Dapper extension methods toomap hello results of your SQL query into .NET objects:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

<span data-ttu-id="1fd69-165">해당 hello 참고 **를 사용 하 여** hello DDR 연결 범위가 hello 블록 toohello 하나의 분할 tenantId1 보관할 내의 모든 데이터베이스 작업을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-165">Note that hello **using** block with hello DDR connection scopes all database operations within hello block toohello one shard where tenantId1 is kept.</span></span> <span data-ttu-id="1fd69-166">hello 쿼리는 hello 현재 분할 하지만 다른 분할 영역에 저장 된 hello 하지에 저장 된 블로그만 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-166">hello query only returns blogs stored on hello current shard, but not hello ones stored on any other shards.</span></span> 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a><span data-ttu-id="1fd69-167">Dapper 및 DapperExtensions를 사용한 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="1fd69-167">Data dependent routing with Dapper and DapperExtensions</span></span>
<span data-ttu-id="1fd69-168">Dapper는 데이터베이스 응용 프로그램을 개발 하는 경우 추가 편 및 hello 데이터베이스에서 추상화를 제공할 수 있는 추가 확장 프로그램 에코 시스템 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-168">Dapper comes with an ecosystem of additional extensions that can provide further convenience and abstraction from hello database when developing database applications.</span></span> <span data-ttu-id="1fd69-169">이러한 기능의 한 가지 예가 DapperExtensions입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-169">DapperExtensions is an example.</span></span> 

<span data-ttu-id="1fd69-170">응용 프로그램에서 DapperExtensions를 사용하더라도 데이터베이스 연결 작성 및 관리 방식은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-170">Using DapperExtensions in your application does not change how database connections are created and managed.</span></span> <span data-ttu-id="1fd69-171">Hello 응용 프로그램의 책임 tooopen 연결에는 여전히와 일반 SQL 클라이언트 연결 개체는 hello 확장명 메서드에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-171">It is still hello application’s responsibility tooopen connections, and regular SQL Client connection objects are expected by hello extension methods.</span></span> <span data-ttu-id="1fd69-172">Hello에 의존 수 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 위에서 설명한 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-172">We can rely on hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) as outlined above.</span></span> <span data-ttu-id="1fd69-173">다음 코드 예제 표시, hello로는 더 이상 것 toowrite hello T-SQL 문을으로 hello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-173">As hello following code samples show, hello only change is that we do no longer have toowrite hello T-SQL statements:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

<span data-ttu-id="1fd69-174">및 다음은 hello 쿼리에 대 한 hello 코드 샘플:</span><span class="sxs-lookup"><span data-stu-id="1fd69-174">And here is hello code sample for hello query:</span></span> 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a><span data-ttu-id="1fd69-175">일시적인 오류 처리</span><span class="sxs-lookup"><span data-stu-id="1fd69-175">Handling transient faults</span></span>
<span data-ttu-id="1fd69-176">hello Microsoft Patterns & Practices 팀 게시 된 hello [일시적인 오류 처리 응용 프로그램 블록](http://msdn.microsoft.com/library/hh680934.aspx) toohelp 응용 프로그램 개발자가 hello 클라우드에서 실행 하는 경우에 발생 한 일반적인 일시적인 오류 상황을 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-176">hello Microsoft Patterns & Practices team published hello [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) toohelp application developers mitigate common transient fault conditions encountered when running in hello cloud.</span></span> <span data-ttu-id="1fd69-177">자세한 내용은 참조 [해냈다, 암호의 모든의 전리품이 야: hello 일시적인 오류 처리 응용 프로그램 블록을 사용 하 여](http://msdn.microsoft.com/library/dn440719.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-177">For more information, see [Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).</span></span>

<span data-ttu-id="1fd69-178">hello 코드 예제는 hello 일시적인 오류 라이브러리 tooprotect 일시적 오류에 대해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-178">hello code sample relies on hello transient fault library tooprotect against transient faults.</span></span> 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

<span data-ttu-id="1fd69-179">**SqlDatabaseUtils.SqlRetryPolicy** 로 정의 된 hello 위의 코드는 **SqlDatabaseTransientErrorDetectionStrategy** 10 및 5 초 동안 다시 시도 횟수를 시도 간 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-179">**SqlDatabaseUtils.SqlRetryPolicy** in hello code above is defined as a **SqlDatabaseTransientErrorDetectionStrategy** with a retry count of 10, and 5 seconds wait time between retries.</span></span> <span data-ttu-id="1fd69-180">트랜잭션을 사용 하는 경우 다시 시도 범위 toohello 돌아갑니다 있는지 확인의 일시적인 오류의 경우 hello hello 트랜잭션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-180">If you are using transactions, make sure that your retry scope goes back toohello beginning of hello transaction in hello case of a transient fault.</span></span>

## <a name="limitations"></a><span data-ttu-id="1fd69-181">제한 사항</span><span class="sxs-lookup"><span data-stu-id="1fd69-181">Limitations</span></span>
<span data-ttu-id="1fd69-182">이 문서에 설명 된 hello 접근 방식에 몇 가지 제한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-182">hello approaches outlined in this document entail a couple of limitations:</span></span>

* <span data-ttu-id="1fd69-183">이 문서에 대 한 hello 샘플 코드를 보여 주지 않습니다 방법을 분할 영역 간에 toomanage 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-183">hello sample code for this document does not demonstrate how toomanage schema across shards.</span></span>
* <span data-ttu-id="1fd69-184">요청 제공을 hello 요청에서 제공 하는 hello 분할 키로 식별 되는 모든 데이터베이스 처리 단일 분할 영역에 포함 된 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-184">Given a request, we assume that all its database processing is contained within a single shard as identified by hello sharding key provided by hello request.</span></span> <span data-ttu-id="1fd69-185">그러나이 가정을 유지 하지 않으면 항상, 예를 들어 가능한 toomake 분할 키를 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="1fd69-185">However, this assumption does not always hold, for example, when it is not possible toomake a sharding key available.</span></span> <span data-ttu-id="1fd69-186">tooaddress이,이 hello 탄력적 데이터베이스 클라이언트 라이브러리 포함 hello [MultiShardQuery 클래스](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-186">tooaddress this, hello elastic database client library includes hello [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span></span> <span data-ttu-id="1fd69-187">hello 클래스에는 여러 분할 된 데이터베이스를 쿼리 하기 위한 연결 추상화를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-187">hello class implements a connection abstraction for querying over several shards.</span></span> <span data-ttu-id="1fd69-188">MultiShardQuery Dapper와 함께에서 사용 하 여이 설명서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-188">Using MultiShardQuery in combination with Dapper is beyond hello scope of this document.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1fd69-189">결론</span><span class="sxs-lookup"><span data-stu-id="1fd69-189">Conclusion</span></span>
<span data-ttu-id="1fd69-190">Dapper 및 DapperExtensions를 사용하는 응용 프로그램에서는 Azure SQL 데이터베이스의 탄력적 데이터베이스 도구를 쉽게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-190">Applications using Dapper and DapperExtensions can easily benefit from elastic database tools for Azure SQL Database.</span></span> <span data-ttu-id="1fd69-191">이 문서에 설명 된 hello 단계를 통해 해당 응용 프로그램에 사용할 수 hello 도구 기능 변경 hello 작성 및 열기를 새로운 라우팅을 종속 데이터 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체 toouse hello [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 탄력적 데이터베이스 클라이언트 라이브러리를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-191">Through hello steps outlined in this document, those applications can use hello tool's capability for data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call of hello elastic database client library.</span></span> <span data-ttu-id="1fd69-192">새 연결이 만들어지고 열려 있는 hello 응용 프로그램 변경 내용이 필요한 toothose 위치를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd69-192">This limits hello application changes required toothose places where new connections are created and opened.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
