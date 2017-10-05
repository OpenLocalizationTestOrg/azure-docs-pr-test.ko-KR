---
title: "분할된 맵 관리자에 대한 성능 카운터"
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
ms.openlocfilehash: 60bb26fe6833998137ede71b363d5d40479a4c60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-counters-for-shard-map-manager"></a><span data-ttu-id="06be8-103">분할된 맵 관리자에 대한 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="06be8-103">Performance counters for shard map manager</span></span>
<span data-ttu-id="06be8-104">[분할된 맵 관리자](sql-database-elastic-scale-shard-map-management.md)에 대한 성능은 특히, [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 사용하는 경우에 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-104">You can capture the performance of a [shard map manager](sql-database-elastic-scale-shard-map-management.md), especially when using [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="06be8-105">카운터는 Microsoft.Azure.SqlDatabase.ElasticScale.Client 클래스의 메서드를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-105">Counters are created with methods of the Microsoft.Azure.SqlDatabase.ElasticScale.Client class.</span></span>  

<span data-ttu-id="06be8-106">카운터는 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 작업의 성능을 추적하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-106">Counters are used to track the performance of [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) operations.</span></span> <span data-ttu-id="06be8-107">이러한 카운터는 “탄력적 데이터베이스: 분할된 관리" 범주 아래 성능 모니터에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-107">These counters are accessible in the Performance Monitor, under the "Elastic Database: Shard Management" category.</span></span>

<span data-ttu-id="06be8-108">**최신 버전은**[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-108">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="06be8-109">참고 항목: [최신 탄력적 데이터베이스 클라이언트 라이브러리를 사용하도록 앱 업그레이드](sql-database-elastic-scale-upgrade-client-library.md).</span><span class="sxs-lookup"><span data-stu-id="06be8-109">See also [Upgrade an app to use the latest elastic database client library](sql-database-elastic-scale-upgrade-client-library.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06be8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06be8-110">Prerequisites</span></span>
* <span data-ttu-id="06be8-111">성능 범주 및 카운터를 만들려면, 응용 프로그램을 호스트하는 컴퓨터의 로컬 **관리자** 그룹에 사용자가 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-111">To create the performance category and counters, the user must be a part of the local **Administrators** group on the machine hosting the application.</span></span>  
* <span data-ttu-id="06be8-112">성능 카운터 인스턴스를 만들고 카운터를 업데이트하려면, **관리자** 또는 **성능 모니터 사용자** 그룹에 사용자가 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-112">To create a performance counter instance and update the counters, the user must be a member of either the **Administrators** or **Performance Monitor Users** group.</span></span> 

## <a name="create-performance-category-and-counters"></a><span data-ttu-id="06be8-113">성능 범주 및 카운터 만들기</span><span class="sxs-lookup"><span data-stu-id="06be8-113">Create performance category and counters</span></span>
<span data-ttu-id="06be8-114">카운터를 만들려면 [ShardMapManagmentFactory 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)의 CreatePeformanceCategoryAndCounters 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-114">To create the counters, call the CreatePeformanceCategoryAndCounters method of the [ShardMapManagmentFactory class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx).</span></span> <span data-ttu-id="06be8-115">관리자만 메서드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-115">Only an administrator can execute the method:</span></span> 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

<span data-ttu-id="06be8-116">[이](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell 스크립트를 사용하여 메서드를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-116">You can also use [this](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell script to execute the method.</span></span> <span data-ttu-id="06be8-117">메서드는 다음과 같은 성능 카운터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-117">The method creates the following performance counters:</span></span>  

* <span data-ttu-id="06be8-118">**캐시된 매핑**: 분할된 맵에 대해 캐시된 매핑의 수.</span><span class="sxs-lookup"><span data-stu-id="06be8-118">**Cached mappings**: Number of mappings cached for the shard map.</span></span>
* <span data-ttu-id="06be8-119">**DDR 작업/초**: 분할된 맵에 대한 데이터 종속 라우팅 작업의 속도.</span><span class="sxs-lookup"><span data-stu-id="06be8-119">**DDR operations/sec**: Rate of data dependent routing operations for the shard map.</span></span> <span data-ttu-id="06be8-120">이 카운터는 [OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)에 대한 호출이 대상 분할에 대한 성공적인 연결로 이어지면 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-120">This counter is  updated when a call to [OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) results in a successful connection to the destination shard.</span></span> 
* <span data-ttu-id="06be8-121">**매핑 조회 캐시 적중/초**: 분할된 맵의 매핑에 대한 성공적인 캐시 조회 작업의 속도.</span><span class="sxs-lookup"><span data-stu-id="06be8-121">**Mapping lookup cache hits/sec**: Rate of successful cache lookup operations for mappings in the shard map.</span></span> 
* <span data-ttu-id="06be8-122">**매핑 조회 캐시 누락/초**: 분할된 맵의 매핑에 대해 실패한 캐시 조회 작업의 속도.</span><span class="sxs-lookup"><span data-stu-id="06be8-122">**Mapping lookup cache misses/sec**: Rate of failed cache lookup operations for mappings in the shard map.</span></span>
* <span data-ttu-id="06be8-123">**캐시에 추가되거나 업데이트된 매핑/초**: 분할된 맵에 대해 캐시에 매핑이 추가되거나 업데이트된 속도.</span><span class="sxs-lookup"><span data-stu-id="06be8-123">**Mappings added or updated in cache/sec**: Rate at which mappings are being added or updated in cache for the shard map.</span></span> 
* <span data-ttu-id="06be8-124">**캐시에서 제거된 매핑/초**: 분할된 맵에 대해 캐시에서 매핑이 제거되는 속도.</span><span class="sxs-lookup"><span data-stu-id="06be8-124">**Mappings removed from cache/sec**: Rate at which mappings are being removed from cache for the shard map.</span></span> 

<span data-ttu-id="06be8-125">성능 카운터는 프로세스마다 각각의 캐시된 분할 맵에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-125">Performance counters are created for each cached shard map per process.</span></span>  

## <a name="notes"></a><span data-ttu-id="06be8-126">참고 사항</span><span class="sxs-lookup"><span data-stu-id="06be8-126">Notes</span></span>
<span data-ttu-id="06be8-127">다음 이벤트는 성능 카운터 생성을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-127">The following events trigger the creation of the performance counters:</span></span>  

* <span data-ttu-id="06be8-128">ShardMapManager에 분할된 맵이 포함된 경우, [즉시 로드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)를 통한 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx) 초기화.</span><span class="sxs-lookup"><span data-stu-id="06be8-128">Initialization of the [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) with [eager loading](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), if the ShardMapManager contains any shard maps.</span></span> <span data-ttu-id="06be8-129">여기에는 [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) 및 [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) 메서드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-129">These include the [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) and the [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) methods.</span></span>
* <span data-ttu-id="06be8-130">분할된 맵의 성공적인 조회([GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 또는 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx) 사용).</span><span class="sxs-lookup"><span data-stu-id="06be8-130">Successful lookup of a shard map (using [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) or [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)).</span></span> 
* <span data-ttu-id="06be8-131">CreateShardMap()을 사용한 분할된 맵의 성공적인 조회.</span><span class="sxs-lookup"><span data-stu-id="06be8-131">Successful creation of shard map using CreateShardMap().</span></span>

<span data-ttu-id="06be8-132">성능 카운터는 분할된 맵과 매핑에 수행되는 모든 캐시 작업에 의해 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-132">The performance counters will be updated by all cache operations performed on the shard map and mappings.</span></span> <span data-ttu-id="06be8-133">DeleteShardMap()을 사용한 분할된 맵의 성공적인 제거는 성능 카운터 인스턴스의 삭제로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-133">Successful removal of the shard map using DeleteShardMap()reults in deletion of the performance counters instance.</span></span>  

## <a name="best-practices"></a><span data-ttu-id="06be8-134">모범 사례</span><span class="sxs-lookup"><span data-stu-id="06be8-134">Best practices</span></span>
* <span data-ttu-id="06be8-135">성능 범주 및 카운터 생성은 ShardMapManager 개체를 만들기 전에 한 번만 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-135">Creation of the performance category and counters should be performed only once before the creation of ShardMapManager object.</span></span> <span data-ttu-id="06be8-136">CreatePerformanceCategoryAndCounters() 명령을 실행할 때마다 이전 카운터가 지워지고(모든 인스턴스에 의해 보고된 데이터 손실) 새 카운터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-136">Every execution of the command CreatePerformanceCategoryAndCounters() clears the previous counters (losing data reported by all instances) and creates new ones.</span></span>  
* <span data-ttu-id="06be8-137">성능 카운터 인스턴스는 프로세스 마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-137">Performance counter instances are created per process.</span></span> <span data-ttu-id="06be8-138">응용 프로그램 작동이 중단되거나 분할된 맵이 캐시에서 제거되면 성능 카운터 인스턴스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="06be8-138">Any application crash or removal of a shard map from the cache will result in deletion of the performance counters instances.</span></span>  

### <a name="see-also"></a><span data-ttu-id="06be8-139">참고 항목: </span><span class="sxs-lookup"><span data-stu-id="06be8-139">See also</span></span>
[<span data-ttu-id="06be8-140">탄력적 데이터베이스 기능 개요</span><span class="sxs-lookup"><span data-stu-id="06be8-140">Elastic Database features overview</span></span>](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

