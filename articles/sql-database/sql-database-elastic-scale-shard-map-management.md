---
title: "Azure SQL Database 규모 확장 | Microsoft Docs"
description: "ShardMapManager 및 .NET용 탄력적 데이터베이스를 사용하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="fe9d9-103">분할된 데이터베이스 맵 관리자를 사용하여 데이터베이스 확장</span><span class="sxs-lookup"><span data-stu-id="fe9d9-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="fe9d9-104">SQL Azure에서 데이터베이스를 쉽게 확장하려면 분할된 데이터베이스 맵 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="fe9d9-105">분할된 데이터베이스 맵 관리자는 분할된 데이터베이스 집합에서 모든 분할된 데이터베이스(데이터베이스)에 대한 전역 매핑 정보를 유지 관리하는 특수한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="fe9d9-106">메타데이터를 사용하면 응용 프로그램을 **분할 키**의 값에 따라 올바른 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="fe9d9-107">또한 집합에 있는 모든 분할된 데이터베이스는 로컬 분할된 데이터베이스 데이터를 추적하는 맵을 포함합니다( **shardlet**라고도 함).</span><span class="sxs-lookup"><span data-stu-id="fe9d9-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![분할된 데이터베이스 맵 관리](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="fe9d9-109">분할된 데이터베이스 맵 관리를 위해서는 이 맵의 구성을 이해하는 것이 필수적입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="fe9d9-110">[Elastic Database 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)에 있는 [ShardMapManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)를 사용하여 분할된 데이터베이스 맵을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="fe9d9-111">분할된 데이터베이스 맵 및 분할된 데이터베이스 매핑</span><span class="sxs-lookup"><span data-stu-id="fe9d9-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="fe9d9-112">각 분할된 데이터베이스에 만들 분할된 데이터베이스 맵의 종류를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="fe9d9-113">데이터베이스 아키텍처에 따라 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="fe9d9-114">데이터베이스당 단일 테넌트</span><span class="sxs-lookup"><span data-stu-id="fe9d9-114">Single tenant per database</span></span>  
2. <span data-ttu-id="fe9d9-115">데이터베이스당 다중 테넌트(두 가지 형식):</span><span class="sxs-lookup"><span data-stu-id="fe9d9-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="fe9d9-116">목록 매핑</span><span class="sxs-lookup"><span data-stu-id="fe9d9-116">List mapping</span></span>
   2. <span data-ttu-id="fe9d9-117">범위 매핑</span><span class="sxs-lookup"><span data-stu-id="fe9d9-117">Range mapping</span></span>

<span data-ttu-id="fe9d9-118">단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="fe9d9-119">단일 테넌트 모델은 테넌트당 하나의 데이터베이스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="fe9d9-120">관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![목록 매핑][1]

<span data-ttu-id="fe9d9-122">다중 테넌트 모델은 단일 데이터베이스에 여러 테넌트를 할당합니다(또한 테넌트 그룹을 여러 데이터베이스에 배포할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="fe9d9-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="fe9d9-123">각 테넌트에 데이터 요구가 적다고 예상되는 경우 이 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="fe9d9-124">이 모델에서 **범위 매핑**을 사용하여 데이터베이스에 테넌트의 범위를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![범위 매핑][2]

<span data-ttu-id="fe9d9-126">또는 다중 테넌트를 단일 데이터베이스에 할당하는 *목록 매핑* 을 사용하여 다중 테넌트 데이터베이스 모델을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="fe9d9-127">예를 들어 DB1은 테넌트 ID 1과 5에 대한 정보를 저장하는 데 사용하고 DB2는 테넌트 7과 테넌트 10의 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![단일 DB의 다중 테넌트][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="fe9d9-129">분할 키에 대해 지원되는 .Net 형식</span><span class="sxs-lookup"><span data-stu-id="fe9d9-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="fe9d9-130">탄력적인 확장은 분할 키로 다음의 .NET Framework 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="fe9d9-131">정수</span><span class="sxs-lookup"><span data-stu-id="fe9d9-131">integer</span></span>
* <span data-ttu-id="fe9d9-132">long</span><span class="sxs-lookup"><span data-stu-id="fe9d9-132">long</span></span>
* <span data-ttu-id="fe9d9-133">GUID</span><span class="sxs-lookup"><span data-stu-id="fe9d9-133">guid</span></span>
* <span data-ttu-id="fe9d9-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="fe9d9-134">byte[]</span></span>  
* <span data-ttu-id="fe9d9-135">datetime</span><span class="sxs-lookup"><span data-stu-id="fe9d9-135">datetime</span></span>
* <span data-ttu-id="fe9d9-136">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fe9d9-136">timespan</span></span>
* <span data-ttu-id="fe9d9-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fe9d9-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="fe9d9-138">목록 및 범위 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="fe9d9-138">List and range shard maps</span></span>
<span data-ttu-id="fe9d9-139">분할된 데이터베이스 맵은 **개별 분할 키 값의 목록**이나 **분할 키 값의 범위**를 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="fe9d9-140">목록 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="fe9d9-140">List shard maps</span></span>
<span data-ttu-id="fe9d9-141">**분할된 데이터베이스**에는 **shardlet**이 포함되며, 분할된 데이터베이스에 대한 shardlet 매핑은 분할된 데이터베이스 맵을 통해 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="fe9d9-142">**목록 분할된 데이터베이스 맵** 은 shardlet을 식별하는 개별 키 값과 분할된 데이터베이스로 사용되는 데이터베이스 간의 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="fe9d9-143">**목록 매핑** 은 동일한 데이터베이스에 매핑될 수 있는 명시적이고 서로 다른 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="fe9d9-144">예를 들어 키 1은 데이터베이스 A에 매핑되고 키 값 3과 6은 모두 데이터베이스 B를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="fe9d9-145">키</span><span class="sxs-lookup"><span data-stu-id="fe9d9-145">Key</span></span> | <span data-ttu-id="fe9d9-146">분할된 데이터베이스 위치</span><span class="sxs-lookup"><span data-stu-id="fe9d9-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="fe9d9-147">1</span><span class="sxs-lookup"><span data-stu-id="fe9d9-147">1</span></span> |<span data-ttu-id="fe9d9-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="fe9d9-148">Database_A</span></span> |
| <span data-ttu-id="fe9d9-149">3</span><span class="sxs-lookup"><span data-stu-id="fe9d9-149">3</span></span> |<span data-ttu-id="fe9d9-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="fe9d9-150">Database_B</span></span> |
| <span data-ttu-id="fe9d9-151">4</span><span class="sxs-lookup"><span data-stu-id="fe9d9-151">4</span></span> |<span data-ttu-id="fe9d9-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="fe9d9-152">Database_C</span></span> |
| <span data-ttu-id="fe9d9-153">6</span><span class="sxs-lookup"><span data-stu-id="fe9d9-153">6</span></span> |<span data-ttu-id="fe9d9-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="fe9d9-154">Database_B</span></span> |
| <span data-ttu-id="fe9d9-155">...</span><span class="sxs-lookup"><span data-stu-id="fe9d9-155">...</span></span> |<span data-ttu-id="fe9d9-156">...</span><span class="sxs-lookup"><span data-stu-id="fe9d9-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="fe9d9-157">범위 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="fe9d9-157">Range shard maps</span></span>
<span data-ttu-id="fe9d9-158">**범위 분할된 데이터베이스 맵**에서 키 범위는 한 쌍 **[낮은 값, 높은 값)**으로 기술됩니다. 여기서 *낮은 값*은 범위에서 최소 키이고 *높은 값*은 범위보다 높은 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="fe9d9-159">예를 들어 **[0, 100)**에는 0 이상 100 미만의 모든 정수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="fe9d9-160">여러 범위가 동일한 데이터베이스를 가리킬 수 있으며 연결되지 않은 범위도 지원됩니다. 예를 들어 아래 예제에서 [100, 200) 및 400, 600)은 모두 데이터베이스 C를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="fe9d9-161">키</span><span class="sxs-lookup"><span data-stu-id="fe9d9-161">Key</span></span> | <span data-ttu-id="fe9d9-162">분할된 데이터베이스 위치</span><span class="sxs-lookup"><span data-stu-id="fe9d9-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="fe9d9-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="fe9d9-163">[1,50)</span></span> |<span data-ttu-id="fe9d9-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="fe9d9-164">Database_A</span></span> |
| <span data-ttu-id="fe9d9-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="fe9d9-165">[50,100)</span></span> |<span data-ttu-id="fe9d9-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="fe9d9-166">Database_B</span></span> |
| <span data-ttu-id="fe9d9-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="fe9d9-167">[100,200)</span></span> |<span data-ttu-id="fe9d9-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="fe9d9-168">Database_C</span></span> |
| <span data-ttu-id="fe9d9-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="fe9d9-169">[400,600)</span></span> |<span data-ttu-id="fe9d9-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="fe9d9-170">Database_C</span></span> |
| <span data-ttu-id="fe9d9-171">...</span><span class="sxs-lookup"><span data-stu-id="fe9d9-171">...</span></span> |<span data-ttu-id="fe9d9-172">...</span><span class="sxs-lookup"><span data-stu-id="fe9d9-172">...</span></span> |

<span data-ttu-id="fe9d9-173">위에 나와 있는 각 테이블은 **ShardMap** 개체의 개념적 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="fe9d9-174">각 행은 개별 **PointMapping**(목록 분할된 데이터베이스 맵의 경우) 또는 **RangeMapping**(범위 분할된 데이터베이스 맵의 경우) 개체에 대한 단순한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="fe9d9-175">분할된 데이터베이스 맵 관리자</span><span class="sxs-lookup"><span data-stu-id="fe9d9-175">Shard map manager</span></span>
<span data-ttu-id="fe9d9-176">클라이언트 라이브러리에서 분할된 데이터베이스 맵 관리자는 분할된 데이터베이스 맵의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="fe9d9-177">**ShardMapManager** 인스턴스를 통해 관리되는 데이터는 다음 세 개 위치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="fe9d9-178">**GSM(전역 분할된 데이터베이스 맵)**: 해당 분할된 데이터베이스 맵 및 매핑 모두에 대한 리포지토리 역할을 할 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="fe9d9-179">정보를 관리할 특수 테이블 및 저장된 프로시저는 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="fe9d9-180">일반적으로 작은 데이터베이스이며 손쉽게 액세스할 수 있지만 응용 프로그램의 다른 요구 사항에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="fe9d9-181">테이블은 **__ShardManagement**라는 특수한 스키마에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="fe9d9-182">**LSM(로컬 분할된 데이터베이스 맵)**: 분할된 데이터베이스로 지정하는 모든 데이터베이스는 해당 분할된 데이터베이스와 관련된 분할된 데이터베이스 맵 정보를 포함하고 유지하는 여러 개의 작은 테이블 및 특수 저장 프로시저를 포함하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="fe9d9-183">이 정보는 GSM의 정보와 중복되지만 그렇기 때문에 응용 프로그램에서 GSM에 어떤 부하도 주지 않으면서 캐시된 분할된 데이터베이스 맵 정보의 유효성을 검사할 수 있습니다. 응용 프로그램은 LSM을 사용하여 캐시된 매핑이 여전히 유효한지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="fe9d9-184">각 분할된 데이터베이스의 LSM에 해당하는 테이블은 **__ShardManagement** 스키마에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="fe9d9-185">**Application cache**: **ShardMapManager** 개체에 액세스하는 각 응용 프로그램 인스턴스는 해당 매핑의 로컬 메모리 내 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="fe9d9-186">이 캐시는 최근에 검색된 라우팅 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="fe9d9-187">ShardMapManager 생성</span><span class="sxs-lookup"><span data-stu-id="fe9d9-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="fe9d9-188">**ShardMapManager** 개체는 [팩터리](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 패턴을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="fe9d9-189">**[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** 메서드는 **ConnectionString** 형식으로 자격 증명(GSM이 저장되는 데이터베이스 이름과 서버 이름 포함)을 가져오고 **ShardMapManager** 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="fe9d9-190">**참고:** **ShardMapManager**는 응용 프로그램용 초기화 코드 내에서 앱 도메인별로 한 번만 인스턴스화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="fe9d9-191">동일한 AppDomain에서 ShardMapManager의 추가 인스턴스를 만들면 응용 프로그램의 메모리와 CPU 사용률이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="fe9d9-192">**ShardMapManager** 는 분할된 데이터베이스 맵을 개수와 관계없이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="fe9d9-193">많은 응용 프로그램의 경우 단일 분할된 데이터베이스 맵으로 충분할 수 있지만 서로 다른 스키마에 대해서 또는 고유성을 위해서는 서로 다른 데이터베이스 집합이 사용되며 이러한 경우 다중 분할된 데이터베이스 맵을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="fe9d9-194">이 코드에서는 응용 프로그램이 **TryGetSqlShardMapManager 메서드** 를 사용하여 기존 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)를 열려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="fe9d9-195">GSM(전역 **ShardMapManager** )을 나타내는 개체가 아직 데이터베이스에 없는 경우 클라이언트 라이브러리에서 [CreateSqlShardMapManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)를 사용하여 해당 개체를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="fe9d9-196">대신 Powershell을 사용하여 새 분할된 데이터베이스 맵 관리자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="fe9d9-197">[여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="fe9d9-198">RangeShardMap 또는 ListShardMap 가져오기</span><span class="sxs-lookup"><span data-stu-id="fe9d9-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="fe9d9-199">분할된 데이터베이스 맵 관리자를 만든 후 [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) 또는 [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 메서드를 사용하여 [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) 또는 [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx)을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="fe9d9-200">분할된 데이터베이스 맵 관리 자격 증명</span><span class="sxs-lookup"><span data-stu-id="fe9d9-200">Shard map administration credentials</span></span>
<span data-ttu-id="fe9d9-201">분할된 데이터베이스 맵을 관리하고 조작하는 응용 프로그램은 분할된 데이터베이스 맵을 사용하여 연결을 라우트하는 응용 프로그램과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="fe9d9-202">분할된 데이터베이스, 분할된 데이터베이스 맵, 분할된 데이터베이스 매핑 등을 추가/변경하는 등 분할된 데이터베이스 맵을 관리하려는 경우 **ShardMapManager**를 인스턴스화해야 하며, 이때 **GSM 데이터베이스 및 분할된 데이터베이스로 사용되는 각 데이터베이스 모두에 대해 읽기/쓰기 권한이 있는 자격 증명**을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="fe9d9-203">이 자격 증명은 분할된 데이터베이스 맵 정보를 입력하거나 변경할 뿐만 아니라 새로운 분할된 데이터베이스에 LSM 테이블을 생성할 때 GSM 및 LSM에서 테이블에 쓸 수 있도록 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="fe9d9-204">[탄력적 데이터베이스 클라이언트 라이브러리에 액세스하는 데 사용되는 자격 증명](sql-database-elastic-scale-manage-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="fe9d9-205">영향을 받는 메타데이터만</span><span class="sxs-lookup"><span data-stu-id="fe9d9-205">Only metadata affected</span></span>
<span data-ttu-id="fe9d9-206">**ShardMapManager** 데이터를 채우거나 변경하는 데 사용되는 메서드는 분할된 데이터베이스 자체에 저장된 사용자 데이터를 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="fe9d9-207">예를 들어 **CreateShard**, **DeleteShard**, **UpdateMapping** 등의 메서드는 분할된 데이터베이스 맵 메타데이터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="fe9d9-208">분할된 데이터베이스에 포함된 사용자 데이터를 제거, 추가 또는 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="fe9d9-209">대신, 이러한 메서드는 실제 데이터베이스를 생성 또는 제거하기 위해 수행하는 개별 작업 또는 분할된 환경을 리밸런스하기 위해 분할된 데이터베이스 간에 행을 이동하는 개별 작업과 함께 사용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="fe9d9-210">탄력적 데이터베이스 도구에 포함된 **분할-병합** 도구는 분할된 데이터베이스 간의 실제 데이터 이동을 조정하면서 이러한 API를 사용합니다. [Elastic Database 분할/병합 도구를 사용하여 확장하기](sql-database-elastic-scale-overview-split-and-merge.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="fe9d9-211">분할된 데이터베이스 맵 채우기 예제</span><span class="sxs-lookup"><span data-stu-id="fe9d9-211">Populating a shard map example</span></span>
<span data-ttu-id="fe9d9-212">특정 분할된 데이터베이스 맵을 채우는 작업의 예제 시퀀스는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="fe9d9-213">이 코드는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="fe9d9-214">새로운 분할된 데이터베이스 맵이 분할된 데이터베이스 맵 관리자 내에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="fe9d9-215">서로 다른 두 개의 분할된 데이터베이스용 메타데이터가 분할된 데이터베이스 맵에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="fe9d9-216">다양한 키 범위 매핑이 추가되고 분할된 데이터베이스 맵의 전체 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="fe9d9-217">오류가 발생하면 메서드를 다시 실행할 수 있도록 코드가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="fe9d9-218">각 요청은 분할된 데이터베이스 또는 매핑을 만들기 전에 해당 항목이 이미 존재하는지 여부를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="fe9d9-219">코드에서는 **sample_shard_0**, **sample_shard_1** 및 **sample_shard_2**라는 데이터베이스가 **shardServer** 문자열로 참조되는 서버에 이미 생성되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List the shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="fe9d9-220">또는 PowerShell 스크립트를 사용하여 동일한 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="fe9d9-221">[여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 일부 샘플 PowerShell 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="fe9d9-222">분할된 데이터베이스 맵이 채워진 후에는 해당 맵에 대한 작업을 수행하도록 데이터 액세스 응용 프로그램을 생성하거나 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="fe9d9-223">**맵 레이아웃** 을 변경해야 할 때까지는 맵을 다시 채우거나 조작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="fe9d9-224">데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="fe9d9-224">Data dependent routing</span></span>
<span data-ttu-id="fe9d9-225">분할된 데이터베이스 맵 관리자는 앱별 작업을 수행하기 위해 데이터베이스 연결이 필요한 응용 프로그램에서 대부분 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="fe9d9-226">이러한 연결은 올바른 데이터베이스와 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="fe9d9-227">이를 **데이터 종속 라우팅**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="fe9d9-228">이러한 응용 프로그램의 경우 GSM 데이터베이스에 대한 읽기 전용 액세스 권한이 있는 자격 증명을 사용하여 팩터리의 분할된 데이터베이스 맵 관리자 개체를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="fe9d9-229">이후 연결에 대한 개별 요청은 적합한 분할된 데이터베이스에 연결하는 데 필요한 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="fe9d9-230">읽기 전용 자격 증명으로 열린 **ShardMapManager** 를 사용하는 이러한 응용 프로그램은 맵 또는 매핑을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="fe9d9-231">이러한 요구 사항을 위해, 앞서 설명한 대로 더 높은 권한의 자격 증명을 제공하는 PowerShell 스크립트 또는 관리별 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="fe9d9-232">[탄력적 데이터베이스 클라이언트 라이브러리에 액세스하는 데 사용되는 자격 증명](sql-database-elastic-scale-manage-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="fe9d9-233">자세한 내용은 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="fe9d9-234">분할된 데이터베이스 맵 수정</span><span class="sxs-lookup"><span data-stu-id="fe9d9-234">Modifying a shard map</span></span>
<span data-ttu-id="fe9d9-235">분할된 데이터베이스 맵은 여러 방법으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="fe9d9-236">다음 메서드 모두가 분할된 데이터베이스 및 해당 매핑을 기술하는 메타데이터를 수정하지만 분할된 데이터베이스 내에서 데이터를 실제로 수정하지 않으며 실제 데이터베이스를 만들거나 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="fe9d9-237">아래에서 설명하는 분할된 데이터베이스 맵에 대한 일부 작업은 데이터를 실제로 이동하거나 분할된 데이터베이스로 사용되는 데이터베이스를 추가 및 제거하는 관리 작업으로 조정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="fe9d9-238">이러한 메서드는 분할된 데이터베이스 환경에서 데이터의 전반적인 분산을 수정하기 위해 사용할 수 있는 구성 요소로 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="fe9d9-239">분할된 데이터베이스를 추가하거나 제거하려면 [Shardmap 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)의 **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** 및 **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="fe9d9-240">이러한 작업을 실행하려면 대상 분할된 데이터베이스를 나타내는 서버 및 데이터베이스가 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="fe9d9-241">이러한 메서드는 데이터베이스 자체가 아닌 분할된 데이터베이스 맵의 메타데이터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="fe9d9-242">분할된 데이터베이스에 매핑되는 지점 또는 범위를 만들거나 제거하려면 [RangeShardMapping 클래스](https://msdn.microsoft.com/library/azure/dn807318.aspx)의 **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** 및 [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)의 **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="fe9d9-243">여러 많은 지점 또는 범위를 동일한 분할된 데이터베이스에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="fe9d9-244">이러한 메서드는 메타데이터에만 영향을 주며, 분할된 데이터베이스에 이미 존재하는 데이터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="fe9d9-245">**DeleteMapping** 작업과의 일관성을 위해 데이터베이스에서 데이터를 제거해야 하는 경우 이러한 메서드를 사용하면서 해당 작업을 개별적으로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="fe9d9-246">기존 범위를 둘로 분할하거나 인접한 범위를 하나로 병합하려면 **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** 및 **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="fe9d9-247">분할 및 병합 작업에서는 **키 값이 매핑되는 분할된 데이터베이스가 변경되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="fe9d9-248">분할은 기존 범위를 두 부분으로 나누지만 둘 다를 동일한 분할된 데이터베이스에 매핑된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="fe9d9-249">병합은 동일한 분할된 데이터베이스에 이미 매핑되어 있는 인접한 두 범위에 대해 작동하여 단일 범위로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="fe9d9-250">분할된 데이터베이스 간에 지점 또는 범위 자체를 이동할 때는 실제 데이터를 이동함과 동시에 **UpdateMapping** 을 사용하여 이동을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="fe9d9-251">탄력적 데이터베이스 도구의 일부인 **분할/병합** 서비스를 사용하여 이동이 필요할 때 데이터 이동에 맞춰 분할된 데이터베이스 맵 변경을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="fe9d9-252">개별 지점 또는 범위를 여러 분할된 데이터베이스로 다시 매핑하거나 이동하려면 **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**의 값에 따라 올바른 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="fe9d9-253">**UpdateMapping** 작업과의 일관성을 유지하기 위해 분할된 데이터베이스 간에 데이터를 이동해야 할 수 있으므로, 이러한 메서드를 사용하면서 이동을 개별적으로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="fe9d9-254">매핑을 온라인 및 오프라인으로 설정하려면 **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** 및 **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**을 사용하여 매핑의 온라인 상태를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="fe9d9-255">**UpdateMapping** 및 **DeleteMapping**을 비롯하여 매핑이 "오프라인" 상태인 경우에만 분할된 데이터베이스 매핑에 대한 특정 작업이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="fe9d9-256">매핑이 오프라인 상태이면 해당 매핑에 포함된 특정 키를 기반으로 하는 데이터 종속 요청이 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="fe9d9-257">또한 범위가 먼저 오프라인으로 전환되면 변경 중인 범위에 대해 전송된 쿼리 결과가 불일치하거나 불완전해지지 않도록 영향 받는 분할된 데이터베이스에 대한 모든 연결이 자동으로 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="fe9d9-258">매핑은.Net에서 변경할 수 없는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="fe9d9-259">매핑을 변경하는 위의 모든 메서드는 사용자의 코드 안의 메서드의 모든 참조를 무효화합니다</span><span class="sxs-lookup"><span data-stu-id="fe9d9-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="fe9d9-260">쉽게 매핑의 상태를 변경 하는 작업의 시퀀스를 수행 하려면 모든 매핑을 변경 하는 메서드의 반환 새 매핑 참조를 작업을 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="fe9d9-261">예를 들면, key25가 포함된 shardmap sm의 기존 매핑을 삭제하려면 다음을 실행합니다:</span><span class="sxs-lookup"><span data-stu-id="fe9d9-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="fe9d9-262">분할된 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="fe9d9-262">Adding a shard</span></span>
<span data-ttu-id="fe9d9-263">이미 존재하는 분할된 데이터베이스 맵의 경우 응용 프로그램은 대개 새 키 또는 키 범위에서 예상되는 데이터를 처리할 새로운 분할된 데이터베이스를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="fe9d9-264">예를 들어 테넌트 ID를 기준으로 분할된 응용 프로그램이 새로운 테넌트에 대한 새로운 분할된 데이터베이스를 프로비전해야 할 수 있습니다. 또는 월별로 분할된 데이터의 경우 새로운 달이 시작되기 전에 새로운 분할된 데이터베이스를 프로비전해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="fe9d9-265">키 값의 새로운 범위가 기존 매핑에 속하지 않으며 데이터를 이동할 필요가 없는 경우에는 단지 새로운 분할된 데이터베이스를 추가하고 새 키 또는 범위를 해당 분할된 데이터베이스에 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="fe9d9-266">새로운 분할된 데이터베이스를 추가하는 방법에 대한 자세한 내용은 [새로운 분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="fe9d9-267">그러나 데이터 이동이 필요한 시나리오에서는, 필요한 분할된 데이터베이스 맵 업데이트와 함께 분할된 데이터베이스 간의 데이터 이동을 조정하기 위해 분할/병합 도구가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9d9-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="fe9d9-268">분할-병합 도구 사용에 대한 자세한 내용은 [분할-병합 개요](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="fe9d9-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
