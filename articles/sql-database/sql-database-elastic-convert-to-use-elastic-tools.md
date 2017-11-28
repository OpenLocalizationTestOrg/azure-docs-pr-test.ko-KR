---
title: "확장하기 위해 기존 데이터베이스 마이그레이션 | Microsoft Docs"
description: "분할된 데이터베이스 맵 관리자를 만들어 탄력적 데이터베이스 도구를 사용하기 위해 분할된 데이터베이스 변환"
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
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="b32f5-103">확장하기 위해 기존 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b32f5-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="b32f5-104">Azure SQL 데이터베이스 데이터베이스 도구(예: [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md))를 사용하여 기존의 확장된 분할된 데이터베이스를 쉽게 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="b32f5-105">기존의 데이터베이스 집합을 먼저 변환하여 [분할된 데이터베이스 맵 관리자](sql-database-elastic-scale-shard-map-management.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="b32f5-106">개요</span><span class="sxs-lookup"><span data-stu-id="b32f5-106">Overview</span></span>
<span data-ttu-id="b32f5-107">기존의 분할된 데이터베이스를 마이그레이션하려면:</span><span class="sxs-lookup"><span data-stu-id="b32f5-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="b32f5-108">[분할된 데이터베이스 맵 관리자 데이터베이스](sql-database-elastic-scale-shard-map-management.md)를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="b32f5-109">분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-109">Create the shard map.</span></span>
3. <span data-ttu-id="b32f5-110">개별 분할된 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="b32f5-111">분할된 데이터베이스 맵에 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="b32f5-112">이러한 기술은 [.NET Framework 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) 또는 [Azure SQL DB - Elastic Database 도구 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 있는 PowerShell 스크립트 중 하나를 사용하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="b32f5-113">여기에 있는 예제에서는 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="b32f5-114">ShardMapManager에 대한 자세한 내용은 [분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b32f5-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="b32f5-115">탄력적 데이터베이스 도구에 대한 개요는 [탄력적 데이터베이스 기능 개요](sql-database-elastic-scale-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b32f5-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="b32f5-116">분할된 데이터베이스 맵 관리자 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="b32f5-117">분할된 데이터베이스 맵 관리자는 확장된 데이터베이스를 관리하는 데이터를 포함하는 특별한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="b32f5-118">기존 데이터베이스를 사용하거나 새 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="b32f5-119">분할된 데이터베이스 맵 관리자의 역할을 하는 데이터베이스는 분할된 데이터베이스와 같은 데이터베이스가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="b32f5-120">또한 PowerShell 스크립트는 데이터베이스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="b32f5-121">1단계: 분할된 데이터베이스 맵 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="b32f5-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="b32f5-122">분할된 데이터베이스 맵 관리자를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="b32f5-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="b32f5-123">만든 후 이 cmdlet을 사용하여 분할된 데이터베이스 맵 관리자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="b32f5-124">이 단계는 ShardMapManager 개체를 사용해야 할 때마다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="b32f5-125">2단계: 분할된 데이터베이스 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="b32f5-125">Step 2: create the shard map</span></span>
<span data-ttu-id="b32f5-126">만들 분할된 데이터베이스 맵의 종류를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="b32f5-127">데이터베이스 아키텍처에 따라 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="b32f5-128">데이터베이스당 단일 테넌트(용어는 [용어집](sql-database-elastic-scale-glossary.md)참조.)</span><span class="sxs-lookup"><span data-stu-id="b32f5-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="b32f5-129">데이터베이스당 다중 테넌트(두 가지 형식):</span><span class="sxs-lookup"><span data-stu-id="b32f5-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="b32f5-130">목록 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-130">List mapping</span></span>
   2. <span data-ttu-id="b32f5-131">범위 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-131">Range mapping</span></span>

<span data-ttu-id="b32f5-132">단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="b32f5-133">단일 테넌트 모델은 테넌트당 하나의 데이터베이스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="b32f5-134">관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![목록 매핑][1]

<span data-ttu-id="b32f5-136">다중 테넌트 모델은 단일 데이터베이스에 여러 테넌트를 할당합니다(또한 테넌트 그룹을 여러 데이터베이스에 배포할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b32f5-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="b32f5-137">각 테넌트에 데이터 요구가 적다고 예상되는 경우 이 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="b32f5-138">이 모델에서 **범위 매핑**을 사용하여 데이터베이스에 테넌트의 범위를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![범위 매핑][2]

<span data-ttu-id="b32f5-140">또는 다중 테넌트를 단일 데이터베이스에 할당하는 *목록 매핑* 을 사용하여 다중 테넌트 데이터베이스 모델을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="b32f5-141">예를 들어 DB1은 테넌트 ID 1과 5에 대한 정보를 저장하는 데 사용하고 DB2는 테넌트 7과 테넌트 10의 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![단일 DB의 다중 테넌트][3] 

<span data-ttu-id="b32f5-143">**다음 옵션 중 하나를 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="b32f5-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="b32f5-144">옵션1: 목록 매핑에 대한 분할된 데이터베이스 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="b32f5-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="b32f5-145">ShardMapManager 개체를 사용하여 분할된 데이터베이스 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="b32f5-146">옵션 2: 범위 매핑에 대한 분할된 데이터베이스 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="b32f5-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="b32f5-147">이 매핑 패턴을 활용하려면 테넌트 ID 값이 연속 범위여야 합니다. 또한 데이터베이스를 만들 때 범위를 간단히 건너뛰어 범위에 갭이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="b32f5-148">옵션 3: 단일 데이터베이스의 목록 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="b32f5-149">2단계 옵션 1과 같이 이 패턴을 설정할 때도 목록 맵을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="b32f5-150">3단계: 개별 분할된 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="b32f5-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="b32f5-151">각각의 분할된 데이터베이스를 분할된 데이터베이스 맵 관리자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="b32f5-152">이는 매핑 정보를 저장하기 위한 개별 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="b32f5-153">각각의 분할된 데이터베이스에서 이 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="b32f5-154">4단계: 매핑 추가</span><span class="sxs-lookup"><span data-stu-id="b32f5-154">Step 4: Add mappings</span></span>
<span data-ttu-id="b32f5-155">매핑 추가는 만든 분할된 데이터베이스 맵의 종류에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="b32f5-156">목록 맵을 만든 경우 목록 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="b32f5-157">범위 맵을 만든 경우 범위 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="b32f5-158">옵션 1: 목록 매핑을 위한 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="b32f5-159">각 테넌트에 대한 목록 매핑을 추가하여 데이터를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="b32f5-160">옵션 2: 범위 매핑을 위한 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="b32f5-161">모든 테넌트 ID 범위에 대한 범위 매핑 추가 - 데이터베이스 연결:</span><span class="sxs-lookup"><span data-stu-id="b32f5-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="b32f5-162">4단계 옵션 3: 단일 데이터베이스에서 다중 테넌트에 대한 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="b32f5-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="b32f5-163">각 테넌트에 대해 ListMapping 추가를 실행합니다(위의 옵션 1).</span><span class="sxs-lookup"><span data-stu-id="b32f5-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="b32f5-164">매핑 확인</span><span class="sxs-lookup"><span data-stu-id="b32f5-164">Checking the mappings</span></span>
<span data-ttu-id="b32f5-165">기존의 분할된 데이터베이스와 이와 연결된 매핑에 대한 정보는 다음 명령을 사용하여 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="b32f5-166">요약</span><span class="sxs-lookup"><span data-stu-id="b32f5-166">Summary</span></span>
<span data-ttu-id="b32f5-167">설치를 완료한 후에는 탄력적 데이터베이스 클라이언트 라이브러리를 사용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="b32f5-168">또한 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 [다중 분할된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b32f5-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b32f5-169">Next steps</span></span>
<span data-ttu-id="b32f5-170">[Azure SQL DB-탄력적 데이터베이스 도구 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에서 PowerShell 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="b32f5-171">도구는 GitHub( [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools))에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="b32f5-172">분할/병합 도구를 사용하여 데이터를 다중 테넌트 모델에서 단일 테넌트 모델로 또는 반대로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b32f5-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="b32f5-173">[분할 병합 도구](sql-database-elastic-scale-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b32f5-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b32f5-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b32f5-174">Additional resources</span></span>
<span data-ttu-id="b32f5-175">다중 테넌트 SaaS(software-as-a-service) 데이터베이스 응용 프로그램의 일반적인 데이터 아키텍처 패턴에 대한 정보는 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b32f5-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="b32f5-176">질문 및 기능 요청</span><span class="sxs-lookup"><span data-stu-id="b32f5-176">Questions and Feature Requests</span></span>
<span data-ttu-id="b32f5-177">의문 사항이 있으면 [SQL Database 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)에 문의하고, 기능에 대한 요청이 있는 경우 해당 기능을 [SQL Database 사용자 의견 포럼](https://feedback.azure.com/forums/217321-sql-database/)에 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="b32f5-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

