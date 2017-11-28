---
title: "Azure SQL 데이터베이스 아웃 aaaScale | Microsoft Docs"
description: "어떻게 toouse hello ShardMapManager, 탄력적 데이터베이스 클라이언트 라이브러리"
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
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="f844e-103">Hello shard map manager와 함께 데이터베이스 확장</span><span class="sxs-lookup"><span data-stu-id="f844e-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="f844e-104">SQL Azure에서 데이터베이스 확장 tooeasily shard map manager를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="f844e-105">hello shard map manager는 분할 집합의 모든 분할 영역 (데이터베이스)에 대 한 전역 매핑 정보를 유지 하는 특별 한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="f844e-106">hello 메타 데이터를 통해 응용 프로그램 tooconnect toohello 올바른 데이터베이스의 hello hello 값에 따라 **분할 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="f844e-107">Hello 집합의 모든 분할 hello 로컬 분할 데이터를 추적 하는 지도 포함 하는 또한 (라고 **shardlet**).</span><span class="sxs-lookup"><span data-stu-id="f844e-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![분할된 데이터베이스 맵 관리](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="f844e-109">이러한 맵은 생성 하는 방법을 이해 하는 것은 필수 tooshard 맵 관리 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="f844e-110">이 작업은 수행 hello를 사용 하 여 [ShardMapManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)hello에 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) toomanage 분할 영역에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="f844e-111">분할된 데이터베이스 맵 및 분할된 데이터베이스 매핑</span><span class="sxs-lookup"><span data-stu-id="f844e-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="f844e-112">각 분할에 대 한 분할 맵 toocreate hello 종류를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="f844e-113">hello 데이터베이스 아키텍처에 따라 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="f844e-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="f844e-114">데이터베이스당 단일 테넌트</span><span class="sxs-lookup"><span data-stu-id="f844e-114">Single tenant per database</span></span>  
2. <span data-ttu-id="f844e-115">데이터베이스당 다중 테넌트(두 가지 형식):</span><span class="sxs-lookup"><span data-stu-id="f844e-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="f844e-116">목록 매핑</span><span class="sxs-lookup"><span data-stu-id="f844e-116">List mapping</span></span>
   2. <span data-ttu-id="f844e-117">범위 매핑</span><span class="sxs-lookup"><span data-stu-id="f844e-117">Range mapping</span></span>

<span data-ttu-id="f844e-118">단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="f844e-119">테 넌 트 당 하나의 데이터베이스만 hello 단일 테 넌 트 모델을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="f844e-120">관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![목록 매핑][1]

<span data-ttu-id="f844e-122">hello 다중 테 넌 트 모델 할당 하는 여러 테 넌 트 tooa 단일 데이터베이스 (및 여러 데이터베이스에 걸쳐 테 넌 트의 그룹을 배포할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="f844e-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="f844e-123">각 테 넌 트 toohave 작은 데이터 요구를 예상 하는 경우이 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="f844e-124">이 모델을 사용 하 여 테 넌 트 tooa 데이터베이스 범위 할당 **범위 매핑**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![범위 매핑][2]

<span data-ttu-id="f844e-126">사용 하 여 다중 테 넌 트 데이터베이스 모델을 구현할 수 있습니다는 *목록 매핑* tooassign 여러 테 넌 트 tooa 단일 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="f844e-127">예를 들어 d b 1은 1에서 5, 테 넌 트 id에 대 한 정보를 사용 하는 toostore DB2 7 테 넌 트 및 테 넌 트 10에 대 한 데이터를 저장 하며</span><span class="sxs-lookup"><span data-stu-id="f844e-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![단일 DB의 다중 테넌트][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="f844e-129">분할 키에 대해 지원되는 .Net 형식</span><span class="sxs-lookup"><span data-stu-id="f844e-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="f844e-130">탄력적인 크기 조정 지원 hello 다음.Net Framework 형식을 분할 키로:</span><span class="sxs-lookup"><span data-stu-id="f844e-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="f844e-131">정수</span><span class="sxs-lookup"><span data-stu-id="f844e-131">integer</span></span>
* <span data-ttu-id="f844e-132">long</span><span class="sxs-lookup"><span data-stu-id="f844e-132">long</span></span>
* <span data-ttu-id="f844e-133">GUID</span><span class="sxs-lookup"><span data-stu-id="f844e-133">guid</span></span>
* <span data-ttu-id="f844e-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="f844e-134">byte[]</span></span>  
* <span data-ttu-id="f844e-135">datetime</span><span class="sxs-lookup"><span data-stu-id="f844e-135">datetime</span></span>
* <span data-ttu-id="f844e-136">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f844e-136">timespan</span></span>
* <span data-ttu-id="f844e-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f844e-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="f844e-138">목록 및 범위 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="f844e-138">List and range shard maps</span></span>
<span data-ttu-id="f844e-139">분할된 데이터베이스 맵은 **개별 분할 키 값의 목록**이나 **분할 키 값의 범위**를 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="f844e-140">목록 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="f844e-140">List shard maps</span></span>
<span data-ttu-id="f844e-141">**분할 된 데이터베이스** 포함 **shardlet** 와 분할 맵에 의해 shardlet tooshards의 hello 매핑을 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="f844e-142">A **목록 분할 맵은** hello 개별 키 식별 하는 값 hello shardlet 및 분할 된 데이터베이스로 제공 하는 hello 데이터베이스 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="f844e-143">**매핑을 나열 합니다.** 은 명시적 및 서로 다른 키 값에 매핑된 toohello 수 같은 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="f844e-144">예를 들어 키 1 tooDatabase A 매핑하고 3, 6 키 값이 2. 데이터베이스 참조</span><span class="sxs-lookup"><span data-stu-id="f844e-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="f844e-145">키</span><span class="sxs-lookup"><span data-stu-id="f844e-145">Key</span></span> | <span data-ttu-id="f844e-146">분할된 데이터베이스 위치</span><span class="sxs-lookup"><span data-stu-id="f844e-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="f844e-147">1</span><span class="sxs-lookup"><span data-stu-id="f844e-147">1</span></span> |<span data-ttu-id="f844e-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="f844e-148">Database_A</span></span> |
| <span data-ttu-id="f844e-149">3</span><span class="sxs-lookup"><span data-stu-id="f844e-149">3</span></span> |<span data-ttu-id="f844e-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="f844e-150">Database_B</span></span> |
| <span data-ttu-id="f844e-151">4</span><span class="sxs-lookup"><span data-stu-id="f844e-151">4</span></span> |<span data-ttu-id="f844e-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="f844e-152">Database_C</span></span> |
| <span data-ttu-id="f844e-153">6</span><span class="sxs-lookup"><span data-stu-id="f844e-153">6</span></span> |<span data-ttu-id="f844e-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="f844e-154">Database_B</span></span> |
| <span data-ttu-id="f844e-155">...</span><span class="sxs-lookup"><span data-stu-id="f844e-155">...</span></span> |<span data-ttu-id="f844e-156">...</span><span class="sxs-lookup"><span data-stu-id="f844e-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="f844e-157">범위 분할된 데이터베이스 맵</span><span class="sxs-lookup"><span data-stu-id="f844e-157">Range shard maps</span></span>
<span data-ttu-id="f844e-158">에 **범위 분할 맵은**, hello 키 범위를 쌍으로 설명 **[낮은 값, 높은 가치의)** 여기서 hello *낮은 값* hello 범위 및 hello hello최소키*귀중* hello 범위 보다 높으며 hello 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="f844e-159">예를 들어 **[0, 100)**에는 0 이상 100 미만의 모든 정수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="f844e-160">범위 수 지점 toohello 데이터베이스를 동일 하 고 범위를 서로 분리 된 여러 지원 됩니다 (예: [100,200) 및 [400,600) 두 지점 tooDatabase C 아래의 hello 예에서.)</span><span class="sxs-lookup"><span data-stu-id="f844e-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="f844e-161">키</span><span class="sxs-lookup"><span data-stu-id="f844e-161">Key</span></span> | <span data-ttu-id="f844e-162">분할된 데이터베이스 위치</span><span class="sxs-lookup"><span data-stu-id="f844e-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="f844e-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="f844e-163">[1,50)</span></span> |<span data-ttu-id="f844e-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="f844e-164">Database_A</span></span> |
| <span data-ttu-id="f844e-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="f844e-165">[50,100)</span></span> |<span data-ttu-id="f844e-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="f844e-166">Database_B</span></span> |
| <span data-ttu-id="f844e-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="f844e-167">[100,200)</span></span> |<span data-ttu-id="f844e-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="f844e-168">Database_C</span></span> |
| <span data-ttu-id="f844e-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="f844e-169">[400,600)</span></span> |<span data-ttu-id="f844e-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="f844e-170">Database_C</span></span> |
| <span data-ttu-id="f844e-171">...</span><span class="sxs-lookup"><span data-stu-id="f844e-171">...</span></span> |<span data-ttu-id="f844e-172">...</span><span class="sxs-lookup"><span data-stu-id="f844e-172">...</span></span> |

<span data-ttu-id="f844e-173">위에 표시 된 hello 테이블 각각의의 개념적 예는 **ShardMap** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="f844e-174">각 행에는 개인의 간단한 예는 **PointMapping** (예: 목록 분할 맵은 hello) 또는 **RangeMapping** (hello 범위 분할 맵은)에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="f844e-175">분할된 데이터베이스 맵 관리자</span><span class="sxs-lookup"><span data-stu-id="f844e-175">Shard map manager</span></span>
<span data-ttu-id="f844e-176">Hello 클라이언트 라이브러리를 hello shard map manager는 분할 영역 맵의의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="f844e-177">데이터를 관리 하는 hello는 **ShardMapManager** 다음 세 위치에 유지 되는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="f844e-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="f844e-178">**전역 분할 맵 GSM ()**: 모든 분할 영역 맵 및 매핑을 대 한 hello 리포지토리로 데이터베이스 tooserve를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="f844e-179">특수 테이블 및 저장된 프로시저 toomanage hello 정보를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="f844e-180">이 일반적으로 작은 데이터베이스 액세스 lightly 넣고 hello 응용 프로그램의 다른 요구에 따라 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="f844e-181">hello 테이블은 라는 특수 한 스키마 **__ShardManagement**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="f844e-182">**로컬 분할 맵 (LSM)**: 여러 개의 작은 테이블 및 분할 맵 정보 특정 toothat 분할 관리를 포함 하는 특별 한 저장된 프로시저는 분할 된 데이터베이스는 toobe 수정 toocontain를 지정 하는 모든 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="f844e-183">이 정보 hello GSM의 hello 정보와 중복 이며 hello 응용 프로그램 캐시 toovalidate 분할 맵 정보 없이 GSM; hello에 대 한 모든 부하가 허용 합니다. hello 응용 프로그램 캐시 된 매핑을 여전히 유효한 경우 LSM toodetermine hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="f844e-184">hello 테이블 각 분할에 LSM가 hello 스키마에도 해당 toohello **__ShardManagement**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="f844e-185">**Application cache**: **ShardMapManager** 개체에 액세스하는 각 응용 프로그램 인스턴스는 해당 매핑의 로컬 메모리 내 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="f844e-186">이 캐시는 최근에 검색된 라우팅 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="f844e-187">ShardMapManager 생성</span><span class="sxs-lookup"><span data-stu-id="f844e-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="f844e-188">**ShardMapManager** 개체는 [팩터리](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 패턴을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="f844e-189">hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  hello 형식의 메서드는 자격 증명 (hello 서버 이름 및 hello GSM을 보유 하는 데이터베이스 이름 포함)는  **ConnectionString** 의 인스턴스를 반환 하는 **ShardMapManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="f844e-190">**주의 사항:** hello **ShardMapManager** 는 응용 프로그램에 대 한 hello 초기화 코드 내에서 응용 프로그램 도메인당 한 번만 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="f844e-191">만들 인스턴스의 ShardMapManager hello에 동일한 appdomain hello 응용 프로그램의 CPU 사용률이 향상 된 메모리에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="f844e-192">**ShardMapManager** 는 분할된 데이터베이스 맵을 개수와 관계없이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="f844e-193">많은 응용 프로그램의 경우 단일 분할된 데이터베이스 맵으로 충분할 수 있지만 서로 다른 스키마에 대해서 또는 고유성을 위해서는 서로 다른 데이터베이스 집합이 사용되며 이러한 경우 다중 분할된 데이터베이스 맵을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="f844e-194">이 코드에서는 응용 프로그램이 하면 기존의 tooopen **ShardMapManager** hello로 [TryGetSqlShardMapManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="f844e-195">경우는 Global를 나타내는 개체 **ShardMapManager** hello 클라이언트 라이브러리가 만들어 있습니다 hello를 사용 하 여, GSM ()는 그렇지 않습니다 아직 hello 데이터베이스 내부 존재 [CreateSqlShardMapManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
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
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="f844e-196">대신 Powershell toocreate 새 Shard Map Manager를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="f844e-197">[여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="f844e-198">RangeShardMap 또는 ListShardMap 가져오기</span><span class="sxs-lookup"><span data-stu-id="f844e-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="f844e-199">Hello를 얻을 수는 shard map manager를 만든 후 [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) 또는 [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello를 사용 하 여 [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), 또는 hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="f844e-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="f844e-200">분할된 데이터베이스 맵 관리 자격 증명</span><span class="sxs-lookup"><span data-stu-id="f844e-200">Shard map administration credentials</span></span>
<span data-ttu-id="f844e-201">관리 및 분할 맵에 조작 하는 응용 프로그램은 hello 분할 맵을 tooroute 연결을 사용 하는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="f844e-202">tooadminister 분할 맵 (추가 또는 분할 된 데이터베이스, 분할 영역 맵의 분할 매핑 등 변경) hello 인스턴스화해야 **ShardMapManager** 를 사용 하 여 **권한이 있는 자격 증명 읽기/쓰기 권한 모두 hello GSM 데이터베이스 및 각 분할 영역으로 사용 되는 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="f844e-203">hello 자격 증명 허용 해야 두 hello의 hello 테이블에 대 한 쓰기 GSM 및 LSM 분할 맵 정보를 입력 하거나도 새 분할 영역에 LSM 테이블을 만들 때와 수정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="f844e-204">참조 [tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하는 자격 증명](sql-database-elastic-scale-manage-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="f844e-205">영향을 받는 메타데이터만</span><span class="sxs-lookup"><span data-stu-id="f844e-205">Only metadata affected</span></span>
<span data-ttu-id="f844e-206">Hello를 변경 하거나 채우는 사용 되는 메서드의 **ShardMapManager** 데이터 자체 hello 분할 영역에 저장 된 hello 사용자 데이터를 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="f844e-207">와 같은 예를 들어 메서드 **CreateShard**, **DeleteShard**, **UpdateMapping**등 hello shard map 메타 데이터만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="f844e-208">제거 하지 않습니다, 추가 또는 hello 분할 영역에 포함 된 사용자 데이터를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="f844e-209">대신, 이러한 메서드는 사용 되는 디자인 된 toobe 별도 작업와 함께에서 하면 toocreate 수행 실제 데이터베이스를 제거 또는 이동 하는 분할 환경 tooanother toorebalance 하나의 분할 영역에서에서 행.</span><span class="sxs-lookup"><span data-stu-id="f844e-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="f844e-210">(hello **분할 / 병합** 탄력적 데이터베이스 도구에 포함 된 도구에서 분할 된 데이터베이스 간에 실제 데이터 이동을 오케스트레이션 함께 이러한 Api를 활용 합니다.) 참조 [hello 탄력적 데이터베이스 분할 / 병합 도구를 사용 하 여 크기 조정](sql-database-elastic-scale-overview-split-and-merge.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="f844e-211">분할된 데이터베이스 맵 채우기 예제</span><span class="sxs-lookup"><span data-stu-id="f844e-211">Populating a shard map example</span></span>
<span data-ttu-id="f844e-212">시퀀스 작업 toopopulate 특정 분할 맵은의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="f844e-213">hello 코드는 다음이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="f844e-214">새로운 분할된 데이터베이스 맵이 분할된 데이터베이스 맵 관리자 내에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="f844e-215">두 개의 서로 다른 분할 영역에 대 한 메타 데이터 hello toohello 분할 맵을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="f844e-216">다양 한 키 범위 매핑 추가 되 고 hello hello shard map의 전체 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="f844e-217">hello 코드 hello 메서드 오류가 발생 한 경우 다시 실행할 수 있도록 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="f844e-218">분할 영역이 있는지 여부를 테스트 하는 각 요청 또는 toocreate 시도 하기 전에 매핑이 이미 존재 하기.</span><span class="sxs-lookup"><span data-stu-id="f844e-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="f844e-219">hello이 코드에서는 데이터베이스 라는 **sample_shard_0**, **sample_shard_1** 및 **sample_shard_2** 문자열에서참조하는hello서버에이미만들어져**shardServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

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

            // List hello shards and mappings 
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

<span data-ttu-id="f844e-220">PowerShell을 사용 하 여는 대신 스크립트 tooachieve hello 처럼 같은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="f844e-221">사용할 수 있는 일부 hello 샘플 PowerShell 예에서는 [여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="f844e-222">분할 영역 맵의 채워지고 나면 hello 지도와 toowork 조정 또는 데이터 액세스 응용 프로그램 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="f844e-223">채우기 hello 지도 조작 하거나까지 다시 발생 하지 않아도 **지도 레이아웃** toochange 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="f844e-224">데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="f844e-224">Data dependent routing</span></span>
<span data-ttu-id="f844e-225">hello shard map manager 데이터베이스 연결 tooperform hello 응용 프로그램별 데이터 작업을 수행 해야 하는 응용 프로그램에 가장 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="f844e-226">이러한 연결 hello 올바른 데이터베이스와 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="f844e-227">이를 **데이터 종속 라우팅**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="f844e-228">이러한 응용 프로그램에 대 한 hello GSM 데이터베이스에 대 한 읽기 전용 권한이 있는 자격 증명을 사용 하 여 hello 공장에서 shard map manager 개체를 인스턴스화하십시오.</span><span class="sxs-lookup"><span data-stu-id="f844e-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="f844e-229">이후 연결에 대 한 개별 요청 toohello 적절 한 분할 데이터베이스를 연결 하기 위해 필요한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="f844e-230">이러한 응용 프로그램 (사용 하 여 **ShardMapManager** 읽기 전용 자격 증명으로 연) न ी द toohello 지방 지도나 매핑.</span><span class="sxs-lookup"><span data-stu-id="f844e-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="f844e-231">이러한 요구 사항을 위해, 앞서 설명한 대로 더 높은 권한의 자격 증명을 제공하는 PowerShell 스크립트 또는 관리별 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="f844e-232">참조 [tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하는 자격 증명](sql-database-elastic-scale-manage-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="f844e-233">자세한 내용은 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f844e-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="f844e-234">분할된 데이터베이스 맵 수정</span><span class="sxs-lookup"><span data-stu-id="f844e-234">Modifying a shard map</span></span>
<span data-ttu-id="f844e-235">분할된 데이터베이스 맵은 여러 방법으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="f844e-236">Hello 분할 된 데이터베이스 및 해당 매핑을 설명 하는 hello 메타 데이터를 수정 하는 모든 메서드를 다음 hello 하지만 hello 분할 영역 내에서 데이터를 실제로 수정 하지도 만들거나 하거나 hello 실제 데이터베이스 삭제지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="f844e-237">Hello에 대 한 작업 아래에서 설명 하는 hello 분할 맵은 일부 toobe 또는 데이터를 실제로 이동 하는 추가 하 고 분할 된 데이터베이스 역할을 수행 하는 데이터베이스를 제거 하는 관리 작업을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="f844e-238">이러한 메서드는 함께 수정에 사용할 수 있는 hello 빌딩 블록으로 분할 된 데이터베이스 환경에서 데이터의 전체 분포 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="f844e-239">분할 된 데이터베이스 tooadd 또는 제거: 사용 하 여  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  및  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  hello의 [Shardmap 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="f844e-240">hello 서버 및 데이터베이스 hello 대상 분할 영역을 나타내는 이미 존재 해야 이러한 작업 tooexecute 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="f844e-241">이러한 메서드 hello 데이터베이스 자체를 hello shard map의 메타 데이터에 대해서만에 영향을 받지를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="f844e-242">toocreate / 제거를 점 또는 범위는 매핑된 toohello 분할: 사용 하 여  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  hello의 [RangeShardMapping 클래스](https://msdn.microsoft.com/library/azure/dn807318.aspx), 및  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  의 hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="f844e-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="f844e-243">많은 다양 한 지점 또는 범위에는 매핑된 toohello 수 동일한 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="f844e-244">이러한 메서드는 메타데이터에만 영향을 주며, 분할된 데이터베이스에 이미 존재하는 데이터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="f844e-245">데이터와 일치 하는 순서 toobe에 hello 데이터베이스에서 제거 toobe 필요 **DeleteMapping** 작업을 해야 tooperform 이러한 작업이 개별적으로 하지만 이러한 방법을 사용 하 여 함께에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="f844e-246">toosplit 기존 범위를 두 개 또는 하나에 인접 한 범위 병합: 사용 하 여  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  및  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="f844e-247">분할 및 병합 작업을 **hello 분할 toowhich 키 값이 매핑되는 변경 하지 마십시오**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="f844e-248">분할의 두 부분으로 기존 범위를 중단 되지만 매핑된 toohello로 둘 다 동일한 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="f844e-249">매핑된 toohello 이미 있는 인접 한 두 범위에서 작동 하는 병합 단일 범위로 통합 하는 동일한 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="f844e-250">hello 점 또는 분할 간 범위 자체의 이동 필요를 사용 하 여 조정 toobe **UpdateMapping** 함께 실제 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="f844e-251">Hello를 사용할 수 있습니다 **분할/병합** 이동이 필요한 경우 탄력적 데이터베이스의 일부인 서비스 도구 toocoordinate 분할 맵을 변경 내용 데이터 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="f844e-252">toore 맵 (또는 이동) 개별 포인트 또는 범위 toodifferent 조각을: 사용 하 여  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="f844e-253">데이터와 일치 하는 순서 toobe에 하나의 분할 tooanother에서 이동 toobe 할 수 있으므로 **UpdateMapping** 작업을 해야 tooperform 해당 이동 별도로 하지만 이러한 방법을 사용 하 여 함께에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="f844e-254">온라인 및 오프 라인 tootake 매핑: 사용 하 여  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  및  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello의 온라인 상태는 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="f844e-255">**UpdateMapping** 및 **DeleteMapping**을 비롯하여 매핑이 "오프라인" 상태인 경우에만 분할된 데이터베이스 매핑에 대한 특정 작업이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="f844e-256">매핑이 오프라인 상태이면 해당 매핑에 포함된 특정 키를 기반으로 하는 데이터 종속 요청이 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="f844e-257">또한 범위 먼저 오프 라인 상태인 경우 모든 연결에 대 한 영향을 받는 toohello 분할 영역 변경 되는 범위에 대해 쿼리에 대 한 순서 tooprevent 일치 하지 않거나 불완전 한 결과에 자동으로 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="f844e-258">매핑은.Net에서 변경할 수 없는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="f844e-259">모든 매핑을 변경 하는 hello 메서드 위의 코드에서 모든 참조 toothem도 무효화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="f844e-260">toomake 새 매핑을 변경 하는 hello 메서드의 모든 매핑의 상태를 변경 하는 작업의 더 쉽게 tooperform 시퀀스를 반환 하는 it 작업에 연결 될 수 있으므로 매핑 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f844e-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="f844e-261">예를 들어 기존 25 hello 키가 포함 된 shardmap sm에서 매핑을 toodelete, 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="f844e-262">분할된 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="f844e-262">Adding a shard</span></span>
<span data-ttu-id="f844e-263">응용 프로그램 종종 필요한 toosimply 새로운 키 또는 키 범위에서 예상 되는 새 분할 영역이 toohandle 데이터 대 한 추가 분할 맵은 이미 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="f844e-264">예를 들어 테 넌 트 ID에 따라 분할 응용 프로그램 tooprovision 새로운 분할 새 테 넌 트에 대 한 하거나 데이터 분할 매월 새로운 분할 hello 새로운 달이 시작 하기 전에 사용자를 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="f844e-265">Hello 새로운 키 값의 범위로 되어 있지 않은 경우 기존 매핑을 및 데이터 이동 없이 필요한 것이 매우 간단한 tooadd hello 새 분할 영역 및 hello 새 키 또는 범위 toothat 분할 영역을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="f844e-266">새로운 분할된 데이터베이스를 추가하는 방법에 대한 자세한 내용은 [새로운 분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f844e-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="f844e-267">그러나 데이터를 이동 해야 하는 시나리오에 대 한 hello 분할 / 병합 도구가 hello 필요한 분할 맵 업데이트와 함께에서 분할 영역 간에 필요한 tooorchestrate hello 데이터를 이동을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f844e-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="f844e-268">사용 하 여에 대 한 내용은 분할 / 병합 yool hello, 참조 [분할 / 병합의 개요](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="f844e-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
