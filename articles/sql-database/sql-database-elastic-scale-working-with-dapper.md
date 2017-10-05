---
title: "Dapper와 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용 | Microsoft Docs"
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
ms.openlocfilehash: f0efd37a39c1a60eee7b47304483c27727ca8833
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a><span data-ttu-id="33d1e-103">Dapper과 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="33d1e-103">Using elastic database client library with Dapper</span></span>
<span data-ttu-id="33d1e-104">이 문서는 Dapper에 의존하여 응용 프로그램을 만들 개발자를 위한 것이지만, 구현 분할 확장 데이터 계층 응용 프로그램을 생성하기 위해 [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md) 를 수용하고 싶은 개발자들도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-104">This document is for developers that rely on Dapper to build applications, but also want to embrace [elastic database tooling](sql-database-elastic-scale-introduction.md) to create applications that implement sharding to scale-out their data tier.</span></span>  <span data-ttu-id="33d1e-105">이 문서에서는 탄력적 데이터베이스 도구와 통합하기 위해 Dapper 기반 응용 프로그램에서 수행해야 하는 변경에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-105">This document illustrates the changes in Dapper-based applications that are necessary to integrate with elastic database tools.</span></span> <span data-ttu-id="33d1e-106">여기서는 Dapper를 사용하여 탄력적 데이터베이스의 분할된 데이터베이스 관리 및 데이터 종속 라우팅을 작성하는 방법에 대해 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-106">Our focus is on composing the elastic database shard management and data dependent routing with Dapper.</span></span> 

<span data-ttu-id="33d1e-107">**샘플 코드**: [Azure SQL 데이터베이스-Dapper 통합에 대한 탄력적 데이터베이스 도구](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span><span class="sxs-lookup"><span data-stu-id="33d1e-107">**Sample Code**: [Elastic database tools for Azure SQL Database - Dapper integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span></span>

<span data-ttu-id="33d1e-108">**Dapper**와 **DapperExtensions**는 Azure SQL Database의 탄력적 데이터베이스 클라이언트와 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-108">Integrating **Dapper** and **DapperExtensions** with the elastic database client library for Azure SQL Database is easy.</span></span> <span data-ttu-id="33d1e-109">응용 프로그램에서는 새로운 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체를 만들고 열 때 [클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/dn765902.aspx)의 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출을 사용하도록 변경하여 데이터 종속 라우팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-109">Your applications can use data dependent routing by changing the creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects to use the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call from the [client library](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span></span> <span data-ttu-id="33d1e-110">이 경우 응용 프로그램에서 새 연결을 만들고 열 때만 해당 호출을 사용하도록 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-110">This limits changes in your application to only where new connections are created and opened.</span></span> 

## <a name="dapper-overview"></a><span data-ttu-id="33d1e-111">Dapper 개요</span><span class="sxs-lookup"><span data-stu-id="33d1e-111">Dapper overview</span></span>
<span data-ttu-id="33d1e-112">**Dapper** 는 개체 관계형 매퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-112">**Dapper** is an object-relational mapper.</span></span> <span data-ttu-id="33d1e-113">응용 프로그램의 .NET 개체와 관계형 데이터베이스를 서로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-113">It maps .NET objects from your application to a relational database (and vice versa).</span></span> <span data-ttu-id="33d1e-114">샘플 코드의 첫 부분에서는 탄력적 데이터베이스 클라이언트 라이브러리를 Dapper 기반 응용 프로그램과 통합할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-114">The first part of the sample code illustrates how you can integrate the elastic database client library with Dapper-based applications.</span></span> <span data-ttu-id="33d1e-115">그리고 두 번째 부분에서는 Dapper와 DapperExtensions를 통합하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-115">The second part of the sample code illustrates how to integrate when using both Dapper and DapperExtensions.</span></span>  

<span data-ttu-id="33d1e-116">Dapper의 매퍼 기능은 데이터베이스 쿼리 또는 실행을 위해 T-SQL 문을 전송하는 과정을 간소화하는 확장 메서드를 데이터베이스 연결에 대해 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-116">The mapper functionality in Dapper provides extension methods on database connections that simplify submitting T-SQL statements for execution or querying the database.</span></span> <span data-ttu-id="33d1e-117">예를 들어 Dapper를 사용하면 **Execute** 호출을 위한 SQL 문의 매개 변수와 .NET 개체 간 매핑을 쉽게 수행하거나 Dapper에서 **Query** 호출을 사용하여 SQL 쿼리의 결과를 .NET 개체에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-117">For instance, Dapper makes it easy to map between your .NET objects and the parameters of SQL statements for **Execute** calls, or to consume the results of your SQL queries into .NET objects using **Query** calls from Dapper.</span></span> 

<span data-ttu-id="33d1e-118">DapperExtensions를 사용할 때는 더 이상 SQL 문을 입력하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-118">When using DapperExtensions, you no longer need to provide the SQL statements.</span></span> <span data-ttu-id="33d1e-119">데이터베이스 연결에 대해 **GetList**, **Insert** 등의 확장 메서드를 사용하는 경우 SQL 문이 백그라운드에서 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-119">Extensions methods such as **GetList** or **Insert** over the database connection create the SQL statements behind the scenes.</span></span>

<span data-ttu-id="33d1e-120">Dapper 및 DapperExtensions를 사용할 때 또 다른 이점은 응용 프로그램의 데이터베이스 연결 작성을 제어한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-120">Another benefit of Dapper and also DapperExtensions is that the application controls the creation of the database connection.</span></span> <span data-ttu-id="33d1e-121">따라서 데이터베이스에 대한 shardlet 매핑을 기준으로 데이터베이스 연결을 조정하는 탄력적 데이터베이스 클라이언트 라이브러리와 상호 작용이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-121">This helps interact with the elastic database client library which brokers database connections based on the mapping of shardlets to databases.</span></span>

<span data-ttu-id="33d1e-122">Dapper 어셈블리를 확인하려면 [Dapper.net](http://www.nuget.org/packages/Dapper/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33d1e-122">To get the Dapper assemblies, see [Dapper dot net](http://www.nuget.org/packages/Dapper/).</span></span> <span data-ttu-id="33d1e-123">Dapper 확장은 [DapperExtensions](http://www.nuget.org/packages/DapperExtensions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33d1e-123">For the Dapper extensions, see [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span></span>

## <a name="a-quick-look-at-the-elastic-database-client-library"></a><span data-ttu-id="33d1e-124">탄력적 데이터베이스 클라이언트 라이브러리를 간단히 살펴보기</span><span class="sxs-lookup"><span data-stu-id="33d1e-124">A quick Look at the elastic database client library</span></span>
<span data-ttu-id="33d1e-125">탄력적 데이터베이스 클라이언트 라이브러리를 사용하면 *shardlets*라는 응용 프로그램 데이터 파티션을 정의하여 데이터베이스에 매핑한 다음 *분할 키*로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-125">With the elastic database client library, you define partitions of your application data called *shardlets* , map them to databases, and identify them by *sharding keys*.</span></span> <span data-ttu-id="33d1e-126">데이터베이스는 필요한 수만큼 포함할 수 있으며 이러한 데이터베이스에 대해 shardlet을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-126">You can have as many databases as you need and distribute your shardlets across these databases.</span></span> <span data-ttu-id="33d1e-127">라이브러리의 API에서 제공하는 분할된 데이터베이스 맵을 통해 데이터베이스에 대한 분할 키 값의 매핑이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-127">The mapping of sharding key values to the databases is stored by a shard map provided by the library’s APIs.</span></span> <span data-ttu-id="33d1e-128">이 기능을 **분할된 데이터베이스 맵 관리**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-128">This capability is called **shard map management**.</span></span> <span data-ttu-id="33d1e-129">분할된 데이터베이스 맵은 분할 키를 전송하는 요청에 대한 데이터베이스 연결의 브로커 역할도 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-129">The shard map also serves as the broker of database connections for requests that carry a sharding key.</span></span> <span data-ttu-id="33d1e-130">이 기능을 **데이터 종속 라우팅**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-130">This capability is referred to as **data dependent routing**.</span></span>

![분할된 데이터베이스 맵과 데이터 종속 라우팅][1]

<span data-ttu-id="33d1e-132">분할된 데이터베이스 맵 관리자는 동시 shardlet 관리 작업이 수행될 때 데이터베이스에서 발생할 수 있는 shardlet 데이터 뷰 불일치 현상을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-132">The shard map manager protects users from inconsistent views into shardlet data that can occur when concurrent shardlet management operations are happening on the databases.</span></span> <span data-ttu-id="33d1e-133">이를 위해, 분할된 데이터베이스 맵이 라이브러리내의 기존 응용 프로그램용 데이터베이스 연결을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-133">To do so, the shard maps broker the database connections for an application built with the library.</span></span> <span data-ttu-id="33d1e-134">분할된 데이터베이스 관리 작업 수행 시 shardlet이 영향을 받을 수 있는 경우 분할된 데이터베이스 맵 기능은 데이터베이스 연결을 자동으로 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-134">When shard management operations could impact the shardlet, this allows the shard map functionality to automatically kill a database connection.</span></span> 

<span data-ttu-id="33d1e-135">따라서 Dapper에 대한 연결을 만드는 기존 방식을 사용하는 대신 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn824099.aspx)메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-135">Instead of using the traditional way to create connections for Dapper, we need to use the [OpenConnectionForKey method](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span></span> <span data-ttu-id="33d1e-136">이 메서드를 사용하면 분할된 데이터베이스 간을 데이터가 이동할 때 모든 유효성 검사가 수행되며 연결이 제대로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-136">This ensures that all the validation takes place and connections are managed properly when any data moves between shards.</span></span>

### <a name="requirements-for-dapper-integration"></a><span data-ttu-id="33d1e-137">Dapper 통합을 위한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="33d1e-137">Requirements for Dapper integration</span></span>
<span data-ttu-id="33d1e-138">탄력적 데이터베이스 클라이언트 라이브러리와 Dapper API를 모두 사용할 때는 다음 속성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-138">When working with both the elastic database client library and the Dapper APIs, we want to retain the following properties:</span></span>

* <span data-ttu-id="33d1e-139">**규모 확장**: 응용 프로그램의 용량 요구 사항에 따라 분할된 응용 프로그램의 데이터 계층에서 데이터베이스를 필요한 만큼 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-139">**Scaleout**: We want to add or remove databases from the data tier of the sharded application as necessary for the capacity demands of the application.</span></span> 
* <span data-ttu-id="33d1e-140">**일관성**: 응용 프로그램은 분할을 사용하여 규모 확장되므로 데이터 종속 라우팅을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-140">**Consistency**: Since our application is scaled out using sharding, we need to perform data dependent routing.</span></span> <span data-ttu-id="33d1e-141">이를 위해 라이브러리의 데이터 종속 라우팅 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-141">We want to use the Data dependent routing capabilities of the library to do so.</span></span> <span data-ttu-id="33d1e-142">특히 손상이나 잘못된 쿼리 결과를 방지하기 위해 분할된 데이터베이스 맵을 통해 조정되는 연결에서 보장하는 유효성 검사 및 일관성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-142">In particular, we want to retain the validation and consistency guarantees provided by connections that are brokered through the shard map manager in order to avoid corruption or wrong query results.</span></span> <span data-ttu-id="33d1e-143">이렇게 하면 예를 들어 지정된 shardlet이 분할/병합 API를 사용하여 현재 다른 분할된 데이터베이스로 이동되어 있는 경우 해당 shardlet에 대한 연결이 거부되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-143">This ensures that connections to a given shardlet are rejected or stopped if (for instance) the shardlet is currently moved to a different shard using Split/Merge APIs.</span></span>
* <span data-ttu-id="33d1e-144">**개체 매핑**: 응용 프로그램의 클래스와 기본 데이터베이스 구조 간 변환을 수행하기 위해 Dapper에서 제공하는 편리한 매핑 기능을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-144">**Object Mapping**: We want to retain the convenience of the mappings provided by Dapper to translate between classes in the application and the underlying database structures.</span></span> 

<span data-ttu-id="33d1e-145">다음 섹션에서는 **Dapper** 및 **DapperExtensions**를 기반으로 하는 응용 프로그램에 대한 이러한 요구 사항 관련 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-145">The following section provides guidance for these requirements for applications based on **Dapper** and **DapperExtensions**.</span></span>

## <a name="technical-guidance"></a><span data-ttu-id="33d1e-146">기술 지침</span><span class="sxs-lookup"><span data-stu-id="33d1e-146">Technical Guidance</span></span>
### <a name="data-dependent-routing-with-dapper"></a><span data-ttu-id="33d1e-147">Dapper를 사용한 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="33d1e-147">Data dependent routing with Dapper</span></span>
<span data-ttu-id="33d1e-148">Dapper를 사용하는 경우 대개 응용 프로그램에서 기본 데이터베이스에 대한 연결을 만들고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-148">With Dapper, the application is typically responsible for creating and opening the connections to the underlying database.</span></span> <span data-ttu-id="33d1e-149">Dapper는 T 형식 .NET 컬렉션으로 쿼리 결과를 반환합니다(응용 프로그램에서 T 형식을 지정함). Dapper는 T-SQL 결과 행에서 T 형식 개체로의 매핑을 수행합니다. 마찬가지로 Dapper는 .NET 개체를 DML(데이터 조작 언어) 문의 SQL 값이나 매개 변수로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-149">Given a type T by the application, Dapper returns query results as .NET collections of type T. Dapper performs the mapping from the T-SQL result rows to the objects of type T. Similarly, Dapper maps .NET objects into SQL values or parameters for data manipulation language (DML) statements.</span></span> <span data-ttu-id="33d1e-150">Dapper는 ADO.NET SQL 클라이언트 라이브러리의 일반 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체에 대한 확장 메서드를 통해 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-150">Dapper offers this functionality via extension methods on the regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object from the ADO .NET SQL Client libraries.</span></span> <span data-ttu-id="33d1e-151">DDR용 탄력적인 확장 API에서 반환하는 SQL 연결도 일반 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-151">The SQL connection returned by the Elastic Scale APIs for DDR are also regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects.</span></span> <span data-ttu-id="33d1e-152">따라서 클라이언트 라이브러리의 DDR API에서 반환하는 형식은 단순 SQL 클라이언트 연결이기도 하므로 이 형식에 대해 Dapper 확장을 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-152">This allows us to directly use Dapper extensions over the type returned by the client library’s DDR API, as it is also a simple SQL Client connection.</span></span>

<span data-ttu-id="33d1e-153">이와 같이 확인된 정보를 통해 탄력적 데이터베이스 클라이언트 라이브러리에서 조정하는 연결을 Dapper에 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-153">These observations make it straightforward to use connections brokered by the elastic database client library for Dapper.</span></span>

<span data-ttu-id="33d1e-154">함께 제공되는 샘플에 포함된 이 코드 예제에서는 연결을 올바르게 분할된 데이터베이스로 조정하기 위해 응용 프로그램에서 라이브러리에 분할 키를 제공하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-154">This code example (from the accompanying sample) illustrates the approach where the sharding key is provided by the application to the library to broker the connection to the right shard.</span></span>   

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

<span data-ttu-id="33d1e-155">[OpenConnectionForKey API](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출에서 SQL 클라이언트 연결의 기본 만들기 및 열기가 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-155">The call to the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API replaces the default creation and opening of a SQL Client connection.</span></span> <span data-ttu-id="33d1e-156">[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출은 데이터 종속 라우팅에 필요한 다음과 같은 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-156">The [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call takes the arguments that are required for data dependent routing:</span></span> 

* <span data-ttu-id="33d1e-157">데이터 종속 라우팅 인터페이스에 액세스하는 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="33d1e-157">The shard map to access the data dependent routing interfaces</span></span>
* <span data-ttu-id="33d1e-158">shardlet을 식별하는 분할 키</span><span class="sxs-lookup"><span data-stu-id="33d1e-158">The sharding key to identify the shardlet</span></span>
* <span data-ttu-id="33d1e-159">분할된 데이터베이스에 연결하기 위한 자격 증명(사용자 이름 및 암호)</span><span class="sxs-lookup"><span data-stu-id="33d1e-159">The credentials (user name and password) to connect to the shard</span></span>

<span data-ttu-id="33d1e-160">분할된 데이터베이스 맵 개체는 지정된 분할 키용 shardlet을 포함하는 분할된 데이터베이스에 대한 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-160">The shard map object creates a connection to the shard that holds the shardlet for the given sharding key.</span></span> <span data-ttu-id="33d1e-161">또한 탄력적 데이터베이스 클라이언트 API는 일관성을 보장하기 위해 연결에 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-161">The elastic database client APIs also tag the connection to implement its consistency guarantees.</span></span> <span data-ttu-id="33d1e-162">[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출에서는 일반 SQL 클라이언트 연결 개체를 반환하므로 Dapper에서 후속 **Execute** 확장 메서드를 호출할 때는 표준 Dapper 방식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-162">Since the call to [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) returns a regular SQL Client connection object, the subsequent call to the **Execute** extension method from Dapper follows the standard Dapper practice.</span></span>

<span data-ttu-id="33d1e-163">쿼리는 거의 비슷한 방식으로 작동합니다. 즉, 먼저 탄력적인 확장 API에서 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)를 사용하여 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-163">Queries work very much the same way - you first open the connection using [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) from the client API.</span></span> <span data-ttu-id="33d1e-164">그런 다음 일반 Dapper 확장 메서드를 사용하여 SQL 쿼리 결과를 .NET 개체에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-164">Then you use the regular Dapper extension methods to map the results of your SQL query into .NET objects:</span></span>

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

<span data-ttu-id="33d1e-165">DDR 연결이 포함된 **using** 블록에서는 블록 내의 모든 데이터베이스 작업 범위가 tenantId1이 저장된 분할된 데이터베이스 하나로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-165">Note that the **using** block with the DDR connection scopes all database operations within the block to the one shard where tenantId1 is kept.</span></span> <span data-ttu-id="33d1e-166">이 쿼리는 현재 분할된 데이터베이스에 저장되어 있는 블로그만 반환하며 다른 분할된 데이터베이스에 저장된 블로그는 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-166">The query only returns blogs stored on the current shard, but not the ones stored on any other shards.</span></span> 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a><span data-ttu-id="33d1e-167">Dapper 및 DapperExtensions를 사용한 데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="33d1e-167">Data dependent routing with Dapper and DapperExtensions</span></span>
<span data-ttu-id="33d1e-168">Dapper에는 데이터베이스 응용 프로그램을 개발할 때 데이터베이스에서 추가적인 편의 기능과 추상화를 제공할 수 있는 추가 확장 에코시스템이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-168">Dapper comes with an ecosystem of additional extensions that can provide further convenience and abstraction from the database when developing database applications.</span></span> <span data-ttu-id="33d1e-169">이러한 기능의 한 가지 예가 DapperExtensions입니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-169">DapperExtensions is an example.</span></span> 

<span data-ttu-id="33d1e-170">응용 프로그램에서 DapperExtensions를 사용하더라도 데이터베이스 연결 작성 및 관리 방식은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-170">Using DapperExtensions in your application does not change how database connections are created and managed.</span></span> <span data-ttu-id="33d1e-171">즉, 응용 프로그램이 계속 연결을 열며 확장 메서드에는 일반 SQL 클라이언트 연결 개체가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-171">It is still the application’s responsibility to open connections, and regular SQL Client connection objects are expected by the extension methods.</span></span> <span data-ttu-id="33d1e-172">위에서 설명한 것처럼 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-172">We can rely on the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) as outlined above.</span></span> <span data-ttu-id="33d1e-173">다음의 코드 샘플에 나와 있는 것처럼 변경되는 부분은 더 이상 T-SQL 문을 작성할 필요가 없다는 것뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-173">As the following code samples show, the only change is that we do no longer have to write the T-SQL statements:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

<span data-ttu-id="33d1e-174">쿼리의 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-174">And here is the code sample for the query:</span></span> 

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

### <a name="handling-transient-faults"></a><span data-ttu-id="33d1e-175">일시적인 오류 처리</span><span class="sxs-lookup"><span data-stu-id="33d1e-175">Handling transient faults</span></span>
<span data-ttu-id="33d1e-176">Microsoft Patterns & Practices 팀은 응용 프로그램 개발자들이 클라우드에서 실행 시에 일반적으로 발생하는 일시적인 오류 상황을 완화할 수 있도록 [일시적인 오류 처리 응용 프로그램 블록](http://msdn.microsoft.com/library/hh680934.aspx)을 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-176">The Microsoft Patterns & Practices team published the [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) to help application developers mitigate common transient fault conditions encountered when running in the cloud.</span></span> <span data-ttu-id="33d1e-177">더 자세한 정보는 [인내, 모든 승리의 비밀: 일시적인 오류 처리 응용 프로그램 블록 사용](http://msdn.microsoft.com/library/dn440719.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33d1e-177">For more information, see [Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).</span></span>

<span data-ttu-id="33d1e-178">코드 샘플에서는 일시적인 오류 라이브러리를 사용하여 일시적인 오류를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-178">The code sample relies on the transient fault library to protect against transient faults.</span></span> 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

<span data-ttu-id="33d1e-179">위 코드의 **SqlDatabaseUtils.SqlRetryPolicy**는 다시 시도 횟수가 10이고 다시 시도 간의 대기 시간이 5초인 **SqlDatabaseTransientErrorDetectionStrategy**로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-179">**SqlDatabaseUtils.SqlRetryPolicy** in the code above is defined as a **SqlDatabaseTransientErrorDetectionStrategy** with a retry count of 10, and 5 seconds wait time between retries.</span></span> <span data-ttu-id="33d1e-180">트랜잭션을 사용하는 경우에는 일시적인 오류 발생 시 다시 시도 범위를 트랜잭션 시작 위치로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-180">If you are using transactions, make sure that your retry scope goes back to the beginning of the transaction in the case of a transient fault.</span></span>

## <a name="limitations"></a><span data-ttu-id="33d1e-181">제한 사항</span><span class="sxs-lookup"><span data-stu-id="33d1e-181">Limitations</span></span>
<span data-ttu-id="33d1e-182">이 문서에서 설명하는 접근 방식에는 몇 가지 제한 사항이 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-182">The approaches outlined in this document entail a couple of limitations:</span></span>

* <span data-ttu-id="33d1e-183">이 문서의 샘플 코드에서는 분할된 데이터베이스 간에 스키마를 관리하는 방법을 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-183">The sample code for this document does not demonstrate how to manage schema across shards.</span></span>
* <span data-ttu-id="33d1e-184">요청이 있는 경우 모든 데이터베이스 처리가 요청에서 제공된 분할 키로 식별되는 단일 분할된 데이터베이스에 포함된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-184">Given a request, we assume that all its database processing is contained within a single shard as identified by the sharding key provided by the request.</span></span> <span data-ttu-id="33d1e-185">그러나 분할 키를 제공할 수 없는 등의 경우도 있으므로 이 가정이 항상 적용되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-185">However, this assumption does not always hold, for example, when it is not possible to make a sharding key available.</span></span> <span data-ttu-id="33d1e-186">이를 해결하려면 탄력적 데이터베이스 클라이언트 라이브러리가 [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-186">To address this, the elastic database client library includes the [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span></span> <span data-ttu-id="33d1e-187">이 클래스는 여러 분할된 데이터베이스에 대한 쿼리를 위해 연결 추상화를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-187">The class implements a connection abstraction for querying over several shards.</span></span> <span data-ttu-id="33d1e-188">MultiShardQuery와 Dapper를 함께 사용하는 방법에 대해서는 이 문서에서 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-188">Using MultiShardQuery in combination with Dapper is beyond the scope of this document.</span></span>

## <a name="conclusion"></a><span data-ttu-id="33d1e-189">결론</span><span class="sxs-lookup"><span data-stu-id="33d1e-189">Conclusion</span></span>
<span data-ttu-id="33d1e-190">Dapper 및 DapperExtensions를 사용하는 응용 프로그램에서는 Azure SQL 데이터베이스의 탄력적 데이터베이스 도구를 쉽게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-190">Applications using Dapper and DapperExtensions can easily benefit from elastic database tools for Azure SQL Database.</span></span> <span data-ttu-id="33d1e-191">이 문서에서 대략적으로 설명한 단계를 수행하면 이러한 응용 프로그램은 새로운 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체를 만들고 열 때 탄력적 데이터베이스 클라이언트 라이브러리의 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출을 사용하도록 변경하여 도구의 데이터 종속 라우팅 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-191">Through the steps outlined in this document, those applications can use the tool's capability for data dependent routing by changing the creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects to use the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call of the elastic database client library.</span></span> <span data-ttu-id="33d1e-192">이 경우 응용 프로그램에서 새 연결을 만들고 여는 위치에서만 해당 호출을 사용하도록 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33d1e-192">This limits the application changes required to those places where new connections are created and opened.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
