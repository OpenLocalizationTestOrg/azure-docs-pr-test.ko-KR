---
title: "shard map manager에 대 한 aaaPerformance 카운터"
description: "ShardMapManager 클래스 및 데이터 종속 라우팅 성능 카운터"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a><span data-ttu-id="09b8f-103">분할된 맵 관리자에 대한 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="09b8f-103">Performance counters for shard map manager</span></span>
<span data-ttu-id="09b8f-104">성능을 hello를 캡처할 수 있습니다는 [shard map manager](sql-database-elastic-scale-shard-map-management.md)사용 하는 경우에 특히 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-104">You can capture hello performance of a [shard map manager](sql-database-elastic-scale-shard-map-management.md), especially when using [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="09b8f-105">카운터는 hello Microsoft.Azure.SqlDatabase.ElasticScale.Client 클래스의 메서드를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-105">Counters are created with methods of hello Microsoft.Azure.SqlDatabase.ElasticScale.Client class.</span></span>  

<span data-ttu-id="09b8f-106">카운터를 사용 하는 tootrack hello 성능을 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-106">Counters are used tootrack hello performance of [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) operations.</span></span> <span data-ttu-id="09b8f-107">이러한 카운터는 성능 모니터 hello hello "탄력적 데이터베이스:: 분할 관리" 범주 아래에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-107">These counters are accessible in hello Performance Monitor, under hello "Elastic Database: Shard Management" category.</span></span>

<span data-ttu-id="09b8f-108">**Hello 최신 버전에 대 한:** 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-108">**For hello latest version:** Go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="09b8f-109">참고 항목 [는 app toouse hello 최신 탄력적 데이터베이스 클라이언트 라이브러리를 업그레이드](sql-database-elastic-scale-upgrade-client-library.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-109">See also [Upgrade an app toouse hello latest elastic database client library](sql-database-elastic-scale-upgrade-client-library.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09b8f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="09b8f-110">Prerequisites</span></span>
* <span data-ttu-id="09b8f-111">toocreate hello 성능 범주 및 카운터를 hello 사용자 hello 로컬의 일부 여야 합니다. **관리자** hello 응용 프로그램을 호스트 하는 hello 컴퓨터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-111">toocreate hello performance category and counters, hello user must be a part of hello local **Administrators** group on hello machine hosting hello application.</span></span>  
* <span data-ttu-id="09b8f-112">hello 사용자 두 hello의 구성원 이어야 합니다., toocreate 성능 카운터 인스턴스 및 hello 카운터 업데이트 **관리자** 또는 **성능 모니터 사용자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-112">toocreate a performance counter instance and update hello counters, hello user must be a member of either hello **Administrators** or **Performance Monitor Users** group.</span></span> 

## <a name="create-performance-category-and-counters"></a><span data-ttu-id="09b8f-113">성능 범주 및 카운터 만들기</span><span class="sxs-lookup"><span data-stu-id="09b8f-113">Create performance category and counters</span></span>
<span data-ttu-id="09b8f-114">hello의 hello CreatePeformanceCategoryAndCounters 메서드를 호출 하는 toocreate hello 카운터 [ShardMapManagmentFactory 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-114">toocreate hello counters, call hello CreatePeformanceCategoryAndCounters method of hello [ShardMapManagmentFactory class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx).</span></span> <span data-ttu-id="09b8f-115">관리자만 hello 메서드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-115">Only an administrator can execute hello method:</span></span> 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

<span data-ttu-id="09b8f-116">사용할 수도 있습니다 [이](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell 스크립트 tooexecute hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="09b8f-116">You can also use [this](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell script tooexecute hello method.</span></span> <span data-ttu-id="09b8f-117">hello 메서드는 다음 성능 카운터 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-117">hello method creates hello following performance counters:</span></span>  

* <span data-ttu-id="09b8f-118">**매핑 캐시**: hello 분할 맵에 대 한 캐시 된 매핑 수입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-118">**Cached mappings**: Number of mappings cached for hello shard map.</span></span>
* <span data-ttu-id="09b8f-119">**DDR 작업/초**: hello 분할 맵에 대 한 데이터 종속 라우팅 작업 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-119">**DDR operations/sec**: Rate of data dependent routing operations for hello shard map.</span></span> <span data-ttu-id="09b8f-120">이 카운터는 호출할 때 업데이트 됩니다 너무[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 연결 성공 toohello 대상 분할 영역에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-120">This counter is  updated when a call too[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) results in a successful connection toohello destination shard.</span></span> 
* <span data-ttu-id="09b8f-121">**조회 캐시 적중/sec 매핑**: hello shard map의 매핑에 대 한 성공적인 캐시 조회 작업 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-121">**Mapping lookup cache hits/sec**: Rate of successful cache lookup operations for mappings in hello shard map.</span></span> 
* <span data-ttu-id="09b8f-122">**조회 캐시 누락 수/초 매핑**: hello shard map의 매핑에 대 한 실패 한 캐시 조회 작업 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-122">**Mapping lookup cache misses/sec**: Rate of failed cache lookup operations for mappings in hello shard map.</span></span>
* <span data-ttu-id="09b8f-123">**매핑에서에서 추가 되거나 업데이트 캐시/sec**: 속도 매핑이 추가 되 고 또는 분할 맵 hello에 대 한 업데이트에서 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-123">**Mappings added or updated in cache/sec**: Rate at which mappings are being added or updated in cache for hello shard map.</span></span> 
* <span data-ttu-id="09b8f-124">**캐시/sec에서 매핑을 제거**: hello 분할 맵에 대 한 캐시에서 매핑을 제거 되 고 있는 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-124">**Mappings removed from cache/sec**: Rate at which mappings are being removed from cache for hello shard map.</span></span> 

<span data-ttu-id="09b8f-125">성능 카운터는 프로세스마다 각각의 캐시된 분할 맵에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-125">Performance counters are created for each cached shard map per process.</span></span>  

## <a name="notes"></a><span data-ttu-id="09b8f-126">참고 사항</span><span class="sxs-lookup"><span data-stu-id="09b8f-126">Notes</span></span>
<span data-ttu-id="09b8f-127">hello 다음 이벤트를 트리거할 hello 성능 카운터의 hello 만들기:</span><span class="sxs-lookup"><span data-stu-id="09b8f-127">hello following events trigger hello creation of hello performance counters:</span></span>  

* <span data-ttu-id="09b8f-128">Hello의 초기화 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 와 [즉시 로드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)hello ShardMapManager 모든 분할 맵에 포함 된 경우.</span><span class="sxs-lookup"><span data-stu-id="09b8f-128">Initialization of hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) with [eager loading](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), if hello ShardMapManager contains any shard maps.</span></span> <span data-ttu-id="09b8f-129">여기에 hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) 및 hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="09b8f-129">These include hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) and hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) methods.</span></span>
* <span data-ttu-id="09b8f-130">분할된 맵의 성공적인 조회([GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 또는 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx) 사용).</span><span class="sxs-lookup"><span data-stu-id="09b8f-130">Successful lookup of a shard map (using [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) or [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)).</span></span> 
* <span data-ttu-id="09b8f-131">CreateShardMap()을 사용한 분할된 맵의 성공적인 조회.</span><span class="sxs-lookup"><span data-stu-id="09b8f-131">Successful creation of shard map using CreateShardMap().</span></span>

<span data-ttu-id="09b8f-132">hello 성능 카운터에서 분할 맵은 hello 및 매핑을 수행 하는 모든 캐시 작업에 의해 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-132">hello performance counters will be updated by all cache operations performed on hello shard map and mappings.</span></span> <span data-ttu-id="09b8f-133">성공적으로 hello 분할 맵은 DeleteShardMap () reults hello 성능 카운터 인스턴스 삭제에 사용 하 여 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-133">Successful removal of hello shard map using DeleteShardMap()reults in deletion of hello performance counters instance.</span></span>  

## <a name="best-practices"></a><span data-ttu-id="09b8f-134">모범 사례</span><span class="sxs-lookup"><span data-stu-id="09b8f-134">Best practices</span></span>
* <span data-ttu-id="09b8f-135">Hello ShardMapManager 개체를 만들기 전에 hello 성능 범주 및 카운터의 생성을 한 번만 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-135">Creation of hello performance category and counters should be performed only once before hello creation of ShardMapManager object.</span></span> <span data-ttu-id="09b8f-136">Hello 명령 실행할 때마다 CreatePerformanceCategoryAndCounters() 지웁니다 (모든 인스턴스에서 보고 하는 데이터 손실) hello 이전 카운터 하 고 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-136">Every execution of hello command CreatePerformanceCategoryAndCounters() clears hello previous counters (losing data reported by all instances) and creates new ones.</span></span>  
* <span data-ttu-id="09b8f-137">성능 카운터 인스턴스는 프로세스 마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-137">Performance counter instances are created per process.</span></span> <span data-ttu-id="09b8f-138">모든 응용 프로그램 충돌 또는 hello 캐시에서 분할 맵은 제거 hello 성능 카운터 인스턴스 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09b8f-138">Any application crash or removal of a shard map from hello cache will result in deletion of hello performance counters instances.</span></span>  

### <a name="see-also"></a><span data-ttu-id="09b8f-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="09b8f-139">See also</span></span>
[<span data-ttu-id="09b8f-140">탄력적 데이터베이스 기능 개요</span><span class="sxs-lookup"><span data-stu-id="09b8f-140">Elastic Database features overview</span></span>](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

