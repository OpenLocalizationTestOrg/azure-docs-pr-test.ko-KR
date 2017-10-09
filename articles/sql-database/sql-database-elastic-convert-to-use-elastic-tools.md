---
title: "tooscale 아웃 데이터베이스 aaaMigrate 기존 | Microsoft Docs"
description: "Shard map manager 만들어 분할 된 데이터베이스 toouse 탄력적 데이터베이스 도구 변환"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="4fc53-103">기존 데이터베이스 tooscale 아웃 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4fc53-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="4fc53-104">Azure SQL 데이터베이스 데이터베이스 도구를 사용 하 여 기존 확장 분할 된 데이터베이스를 쉽게 관리할 (hello 같은 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="4fc53-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="4fc53-105">먼저 기존 데이터베이스 toouse hello 집합을 변환 해야 [shard map manager](sql-database-elastic-scale-shard-map-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="4fc53-106">개요</span><span class="sxs-lookup"><span data-stu-id="4fc53-106">Overview</span></span>
<span data-ttu-id="4fc53-107">toomigrate 기존 분할 된 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="4fc53-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="4fc53-108">Hello 준비 [shard map manager 데이터베이스](sql-database-elastic-scale-shard-map-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="4fc53-109">Hello 분할 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-109">Create hello shard map.</span></span>
3. <span data-ttu-id="4fc53-110">Hello 개별 분할 된 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="4fc53-111">매핑 toohello 분할 맵을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="4fc53-112">이러한 기술은 두 hello를 사용 하 여 구현할 수 있습니다 [.NET Framework 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), 있거나 hello PowerShell 스크립트에 [Azure SQL DB-탄력적 데이터베이스 도구 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="4fc53-113">여기에 hello 예제는 hello PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="4fc53-114">ShardMapManager hello에 대 한 자세한 내용은 참조 [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="4fc53-115">Hello 탄력적 데이터베이스 도구 개요를 참조 하십시오. [탄력적 데이터베이스 기능 개요](sql-database-elastic-scale-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="4fc53-116">Hello shard map manager 데이터베이스를 준비</span><span class="sxs-lookup"><span data-stu-id="4fc53-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="4fc53-117">hello shard map manager는 hello 데이터 toomanage 수평 확장 된 데이터베이스를 포함 하는 특별 한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="4fc53-118">기존 데이터베이스를 사용하거나 새 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="4fc53-119">참고는 동일한 분할 영역으로 데이터베이스는 데이터베이스 역할을 하는 shard map manager hello 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="4fc53-120">PowerShell 스크립트 hello 데이터베이스가 만들어지지 않습니다 hello 드립니다 note도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="4fc53-121">1단계: 분할된 데이터베이스 맵 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc53-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="4fc53-122">tooretrieve hello shard map manager</span><span class="sxs-lookup"><span data-stu-id="4fc53-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="4fc53-123">를 만든 후이 cmdlet과 hello shard map manager을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="4fc53-124">Toouse hello ShardMapManager 개체 할 때마다이 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="4fc53-125">2 단계: hello 분할 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc53-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="4fc53-126">분할 맵 toocreate hello 종류를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="4fc53-127">hello 데이터베이스 아키텍처에 따라 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="4fc53-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="4fc53-128">데이터베이스 마다 단일 테 넌 트 (말해서 참조 hello [용어집](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="4fc53-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="4fc53-129">데이터베이스당 다중 테넌트(두 가지 형식):</span><span class="sxs-lookup"><span data-stu-id="4fc53-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="4fc53-130">목록 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-130">List mapping</span></span>
   2. <span data-ttu-id="4fc53-131">범위 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-131">Range mapping</span></span>

<span data-ttu-id="4fc53-132">단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="4fc53-133">테 넌 트 당 하나의 데이터베이스만 hello 단일 테 넌 트 모델을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="4fc53-134">관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![목록 매핑][1]

<span data-ttu-id="4fc53-136">hello 다중 테 넌 트 모델 할당 하는 여러 테 넌 트 tooa 단일 데이터베이스 (및 여러 데이터베이스에 걸쳐 테 넌 트의 그룹을 배포할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="4fc53-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="4fc53-137">각 테 넌 트 toohave 작은 데이터 요구를 예상 하는 경우이 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="4fc53-138">이 모델을 사용 하 여 테 넌 트 tooa 데이터베이스 범위 할당 **범위 매핑**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![범위 매핑][2]

<span data-ttu-id="4fc53-140">사용 하 여 다중 테 넌 트 데이터베이스 모델을 구현할 수 있습니다는 *목록 매핑* tooassign 여러 테 넌 트 tooa 단일 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="4fc53-141">예를 들어 d b 1은 1에서 5, 테 넌 트 id에 대 한 정보를 사용 하는 toostore DB2 7 테 넌 트 및 테 넌 트 10에 대 한 데이터를 저장 하며</span><span class="sxs-lookup"><span data-stu-id="4fc53-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![단일 DB의 다중 테넌트][3] 

<span data-ttu-id="4fc53-143">**다음 옵션 중 하나를 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="4fc53-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="4fc53-144">옵션1: 목록 매핑에 대한 분할된 데이터베이스 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc53-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="4fc53-145">Hello ShardMapManager 개체를 사용 하 여 분할 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="4fc53-146">옵션 2: 범위 매핑에 대한 분할된 데이터베이스 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="4fc53-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="4fc53-147">해당 tooutilize이 매핑 패턴에 유의 테 넌 트 id 값이 필요한 toobe 연속 범위 며 hello 범위에 허용 가능한 toohave 간격이 hello 데이터베이스를 만들 때 단순히 hello 범위를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="4fc53-148">옵션 3: 단일 데이터베이스의 목록 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="4fc53-149">2단계 옵션 1과 같이 이 패턴을 설정할 때도 목록 맵을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="4fc53-150">3단계: 개별 분할된 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="4fc53-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="4fc53-151">각 분할 (데이터베이스) toohello shard map 관리자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="4fc53-152">이 매핑 정보를 저장 하기 위한 hello 개별 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="4fc53-153">각각의 분할된 데이터베이스에서 이 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="4fc53-154">4단계: 매핑 추가</span><span class="sxs-lookup"><span data-stu-id="4fc53-154">Step 4: Add mappings</span></span>
<span data-ttu-id="4fc53-155">매핑 hello 추가 만든 분할 영역 맵의 hello 종류에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="4fc53-156">목록 맵을 만든 경우 목록 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="4fc53-157">범위 맵을 만든 경우 범위 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="4fc53-158">옵션 1: 목록 매핑에 대 한 hello 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="4fc53-159">각 테 넌 트에 대 한 목록 매핑을 추가 하 여 hello 데이터를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fc53-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="4fc53-160">옵션 2: 범위 매핑에 대 한 hello 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="4fc53-161">모든 hello 테 넌 트 id 범위-데이터베이스 연결에 대 한 hello 범위 매핑을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="4fc53-162">4 단계 옵션 3: 단일 데이터베이스에서 여러 테 넌 트에 대 한 hello 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="4fc53-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="4fc53-163">각 테 넌 트에 대 한 추가 ListMapping hello 실행 (위의 1, 옵션).</span><span class="sxs-lookup"><span data-stu-id="4fc53-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="4fc53-164">Hello 매핑을 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="4fc53-164">Checking hello mappings</span></span>
<span data-ttu-id="4fc53-165">다음 명령을 사용 하 여 hello 기존 분할 영역 및 연결 된 hello 매핑을 대 한 정보를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="4fc53-166">요약</span><span class="sxs-lookup"><span data-stu-id="4fc53-166">Summary</span></span>
<span data-ttu-id="4fc53-167">Hello 설치를 완료 한 후 toouse hello 탄력적 데이터베이스 클라이언트 라이브러리를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="4fc53-168">또한 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 [다중 분할된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fc53-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fc53-169">Next steps</span></span>
<span data-ttu-id="4fc53-170">Hello PowerShell 스크립트에서 가져와서 [Azure SQL DB 탄력적 데이터베이스 도구 sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="4fc53-171">hello 도구가 GitHub에도 있는: [Azure/탄력적인-db-도구](https://github.com/Azure/elastic-db-tools)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="4fc53-172">다중 테 넌 트 모델 tooa 단일 테 넌 트 모델에서 분할 / 병합 도구 toomove 데이터 tooor hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="4fc53-173">[분할 병합 도구](sql-database-elastic-scale-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fc53-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fc53-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4fc53-174">Additional resources</span></span>
<span data-ttu-id="4fc53-175">다중 테넌트 SaaS(software-as-a-service) 데이터베이스 응용 프로그램의 일반적인 데이터 아키텍처 패턴에 대한 정보는 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fc53-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="4fc53-176">질문 및 기능 요청</span><span class="sxs-lookup"><span data-stu-id="4fc53-176">Questions and Feature Requests</span></span>
<span data-ttu-id="4fc53-177">질문에 게 연락 하세요 hello에 toous [SQL 데이터베이스 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) 기능 요청에 대 한 하십시오 추가할 toohello [SQL 데이터베이스 피드백 포럼](https://feedback.azure.com/forums/217321-sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc53-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

