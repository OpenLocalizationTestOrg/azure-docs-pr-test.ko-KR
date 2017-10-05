---
title: "복구 관리자를 사용하여 분할된 데이터베이스 맵 문제 해결 | Microsoft Docs"
description: "RecoveryManager 클래스를 사용하여 분할된 데이터베이스 맵의 문제 해결"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: e60e2295484873ea15d52108b7d619319a57827f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-recoverymanager-class-to-fix-shard-map-problems"></a><span data-ttu-id="981ba-103">RecoveryManager 클래스를 사용하여 분할된 데이터베이스 맵 문제 해결</span><span class="sxs-lookup"><span data-stu-id="981ba-103">Using the RecoveryManager class to fix shard map problems</span></span>
<span data-ttu-id="981ba-104">[RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) 클래스는 분할된 데이터베이스 환경에서 ADO.Net 응용 프로그램이 GSM(전역 분할된 데이터베이스 맵)과 LSM(로컬 분할된 데이터베이스 맵) 간의 모든 불일치를 쉽게 감지하고 수정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-104">The [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) class provides ADO.Net applications the ability to easily detect and correct any inconsistencies between the global shard map (GSM) and the local shard map (LSM) in a sharded database environment.</span></span> 

<span data-ttu-id="981ba-105">GSM 및 LSM은 분할된 데이터베이스 환경에서 각 데이터베이스의 매핑을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-105">The GSM and LSM track the mapping of each database in a sharded environment.</span></span> <span data-ttu-id="981ba-106">경우에 따라 GSM과 LSM 사이에서 중단이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-106">Occasionally, a break occurs between the GSM and the LSM.</span></span> <span data-ttu-id="981ba-107">이 경우 RecoveryManager 클래스를 사용하여 중단을 검색하고 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-107">In that case, use the RecoveryManager class to detect and repair the break.</span></span>

<span data-ttu-id="981ba-108">RecoveryManager 클래스는 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-108">The RecoveryManager class is part of the [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> 

![분할된 맵][1]

<span data-ttu-id="981ba-110">용어 정의는 [탄력적 데이터베이스 도구 용어집](sql-database-elastic-scale-glossary.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-110">For term definitions, see [Elastic Database tools glossary](sql-database-elastic-scale-glossary.md).</span></span> <span data-ttu-id="981ba-111">분할된 데이터베이스 솔루션에서 데이터를 관리하는 데 **ShardMapManager** 가 어떻게 사용되는지 이해하려면 [분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-111">To understand how the **ShardMapManager** is used to manage data in a sharded solution, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span>

## <a name="why-use-the-recovery-manager"></a><span data-ttu-id="981ba-112">복구 관리자를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="981ba-112">Why use the recovery manager?</span></span>
<span data-ttu-id="981ba-113">분할된 데이터베이스 환경에서는 데이터베이스당 한 개의 테넌트가 있고 서버당 여러 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-113">In a sharded database environment, there is one tenant per database, and many databases per server.</span></span> <span data-ttu-id="981ba-114">또한 환경에 여러 서버가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-114">There can also be many servers in the environment.</span></span> <span data-ttu-id="981ba-115">분할된 데이터베이스 맵에서 각 데이터베이스를 매핑하므로 올바른 서버 및 데이터베이스로 호출을 라우트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-115">Each database is mapped in the shard map, so calls can be routed to the correct server and database.</span></span> <span data-ttu-id="981ba-116">데이터베이스는 **분할 키**에 따라 추적되며 각 분할된 데이터베이스에는 **키 값 범위**가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-116">Databases are tracked according to a **sharding key**, and each shard is assigned a **range of key values**.</span></span> <span data-ttu-id="981ba-117">예를 들어 분할 키는 "D"에서 "F"까지의 고객 이름을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-117">For example, a sharding key may represent the customer names from "D" to "F."</span></span> <span data-ttu-id="981ba-118">모든 분할된 데이터베이스의 매핑(즉, 데이터베이스) 및 매핑 범위는 **GSM(전역 분할된 데이터베이스 맵)**에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-118">The mapping of all shards (aka databases) and their mapping ranges are contained in the **global shard map (GSM)**.</span></span> <span data-ttu-id="981ba-119">각 데이터베이스에도 분할된 데이터베이스에 포함된 범위 맵이 포함되며 이를 **LSM(로컬 분할된 데이터베이스 맵)**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-119">Each database also contains a map of the ranges contained on the shard that is known as the **local shard map (LSM)**.</span></span> <span data-ttu-id="981ba-120">앱이 분할된 데이터베이스에 연결될 때 빠른 검색을 위해 매핑이 앱과 함께 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-120">When an app connects to a shard, the mapping is cached with the app for quick retrieval.</span></span> <span data-ttu-id="981ba-121">LSM은 캐시된 데이터의 유효성을 검사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-121">The LSM is used to validate cached data.</span></span> 

<span data-ttu-id="981ba-122">GSM 및 LSM이 동기화되지 않는 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-122">The GSM and LSM may become out of sync for the following reasons:</span></span>

1. <span data-ttu-id="981ba-123">범위가 더 이상 사용되지 않는 분할된 데이터베이스가 삭제되거나 분할된 데이터베이스의 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-123">The deletion of a shard whose range is believed to no longer be in use, or renaming of a shard.</span></span> <span data-ttu-id="981ba-124">**분리되어 분할된 매핑**에서 분할된 데이터베이스 결과 삭제.</span><span class="sxs-lookup"><span data-stu-id="981ba-124">Deleting a shard results in an **orphaned shard mapping**.</span></span> <span data-ttu-id="981ba-125">마찬가지로 이름이 바뀐 데이터베이스도 분리되어 분할된 데이터베이스 매핑을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-125">Similarly, a renamed database can cause an orphaned shard mapping.</span></span> <span data-ttu-id="981ba-126">변경 의도에 따라 분할된 데이터베이스를 제거하거나 분할된 데이터베이스 위치를 업데이트할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-126">Depending on the intent of the change, the shard may need to be removed or the shard location needs to be updated.</span></span> <span data-ttu-id="981ba-127">삭제된 데이터베이스를 복구하려면 [삭제된 데이터베이스 복구](sql-database-recovery-using-backups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-127">To recover a deleted database, see [Restore a deleted database](sql-database-recovery-using-backups.md).</span></span>
2. <span data-ttu-id="981ba-128">지역 장애 조치(failover) 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-128">A geo-failover event occurs.</span></span> <span data-ttu-id="981ba-129">계속하려면 분할된 데이터베이스 맵의 모든 분할된 데이터베이스에 대해 서버 이름과 응용 프로그램에 있는 분할된 데이터베이스 맵 관리자의 데이터베이스 이름을 업데이트한 다음 분할된 데이터베이스 매핑 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-129">To continue, one must update the server name, and database name of shard map manager in the application and then update the shard mapping details for all shards in a shard map.</span></span> <span data-ttu-id="981ba-130">지역 장애 조치의 경우 이러한 복구 논리는 장애 조치 워크플로 내에서 자동화됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-130">If there is a geo-failover, such recovery logic should be automated within the failover workflow.</span></span> <span data-ttu-id="981ba-131">복구 작업을 자동화하면 지역 지원 데이터베이스에 대해 원활한 관리 효율성을 제공하며 사람이 직접 작업하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-131">Automating recovery actions enables a frictionless manageability for geo-enabled databases and avoids manual human actions.</span></span> <span data-ttu-id="981ba-132">데이터 센터 중단 시 데이터베이스를 복구하는 옵션에 대해 알아보려면 [비즈니스 연속성](sql-database-business-continuity.md) 및 [재해 복구](sql-database-disaster-recovery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-132">To learn about options to recover a database if there is a data center outage, see [Business Continuity](sql-database-business-continuity.md) and [Disaster Recovery](sql-database-disaster-recovery.md).</span></span>
3. <span data-ttu-id="981ba-133">분할된 데이터베이스 또는 ShardMapManager 데이터베이스는 이전 시점으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-133">Either a shard or the ShardMapManager database is restored to an earlier point-in time.</span></span> <span data-ttu-id="981ba-134">백업을 사용하여 시간 복구 지점에 대해 알아보려면 [백업을 사용하여 복구](sql-database-recovery-using-backups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-134">To learn about point in time recovery using backups, see [Recovery using backups](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="981ba-135">Azure SQL Database Elastic Database 도구, 지역 복제 및 복원에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-135">For more information about Azure SQL Database Elastic Database tools, geo-replication and Restore, see the following:</span></span> 

* [<span data-ttu-id="981ba-136">개요: SQL 데이터베이스의 클라우드 무중단 업무 방식 및 데이터베이스 재해 복구</span><span class="sxs-lookup"><span data-stu-id="981ba-136">Overview: Cloud business continuity and database disaster recovery with SQL Database</span></span>](sql-database-business-continuity.md) 
* [<span data-ttu-id="981ba-137">탄력적 데이터베이스 도구 시작하기</span><span class="sxs-lookup"><span data-stu-id="981ba-137">Get started with elastic database tools</span></span>](sql-database-elastic-scale-get-started.md)  
* [<span data-ttu-id="981ba-138">ShardMap 관리</span><span class="sxs-lookup"><span data-stu-id="981ba-138">ShardMap Management</span></span>](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a><span data-ttu-id="981ba-139">ShardMapManager에서 RecoveryManager 검색</span><span class="sxs-lookup"><span data-stu-id="981ba-139">Retrieving RecoveryManager from a ShardMapManager</span></span>
<span data-ttu-id="981ba-140">첫 번째 단계는 RecoveryManager 인스턴스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-140">The first step is to create a RecoveryManager instance.</span></span> <span data-ttu-id="981ba-141">[GetRecoveryManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx)는 현재 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 인스턴스에 대한 복구 관리자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-141">The [GetRecoveryManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) returns the recovery manager for the current [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instance.</span></span> <span data-ttu-id="981ba-142">분할된 데이터베이스 맵의 모든 불일치를 해결하려면 먼저 특정 분할된 데이터베이스 맵에 대한 RecoveryManager를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-142">To address any inconsistencies in the shard map, you must first retrieve the RecoveryManager for the particular shard map.</span></span> 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

<span data-ttu-id="981ba-143">이 예에서는 RecoveryManager가 ShardMapManager에서 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-143">In this example, the RecoveryManager is initialized from the ShardMapManager.</span></span> <span data-ttu-id="981ba-144">ShardMap이 포함된 ShardMapManager도 이미 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-144">The ShardMapManager containing a ShardMap is also already initialized.</span></span> 

<span data-ttu-id="981ba-145">이 응용 프로그램 코드는 분할된 데이터베이스 맵 자체를 조작하므로 팩터리 메서드에 사용된 자격 증명(위의 예제에서는, smmConnectionString)은 연결 문자열에서 참조하는 GSM 데이터베이스에 대한 읽기-쓰기 권한이 있는 자격 증명이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-145">Since this application code manipulates the shard map itself, the credentials used in the factory method (in the preceding example, smmConnectionString) should be credentials that have read-write permissions on the GSM database referenced by the connection string.</span></span> <span data-ttu-id="981ba-146">일반적으로 이러한 자격 증명은 데이터 종속 라우팅에 대한 연결을 여는 데 사용되는 자격 증명과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-146">These credentials are typically different from credentials used to open connections for data-dependent routing.</span></span> <span data-ttu-id="981ba-147">자세한 내용은 [탄력적 데이터베이스 클라이언트에 자격 증명 사용](sql-database-elastic-scale-manage-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-147">For more information, see [Using credentials in the elastic database client](sql-database-elastic-scale-manage-credentials.md).</span></span>

## <a name="removing-a-shard-from-the-shardmap-after-a-shard-is-deleted"></a><span data-ttu-id="981ba-148">분할된 데이터베이스를 삭제한 후 ShardMap에서 분할된 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="981ba-148">Removing a shard from the ShardMap after a shard is deleted</span></span>
<span data-ttu-id="981ba-149">[DetachShard 메서드](https://msdn.microsoft.com/library/azure/dn842083.aspx) 는 분할된 데이터베이스 맵에서 지정된 분할된 데이터베이스를 분리하고 여기에 연결된 매핑을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-149">The [DetachShard method](https://msdn.microsoft.com/library/azure/dn842083.aspx) detaches the given shard from the shard map and deletes mappings associated with the shard.</span></span>  

* <span data-ttu-id="981ba-150">위치 매개 변수는 분할된 데이터베이스 위치, 특히 분리 중인 분할된 데이터베이스의 서버 이름 및 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-150">The location parameter is the shard location, specifically server name and database name, of the shard being detached.</span></span> 
* <span data-ttu-id="981ba-151">shardMapName 매개 변수는 분할된 데이터베이스 맵 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-151">The shardMapName parameter is the shard map name.</span></span> <span data-ttu-id="981ba-152">여러 분할된 데이터베이스 맵을 동일한 분할된 데이터베이스 맵 관리자가 관리하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-152">This is only required when multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="981ba-153">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-153">Optional.</span></span> 


> [!IMPORTANT]
> <span data-ttu-id="981ba-154">업데이트되는 매핑의 범위가 비어 있는 것이 확실한 경우에만 이 기술을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-154">Use this technique only if you are certain that the range for the updated mapping is empty.</span></span> <span data-ttu-id="981ba-155">위의 방법에서는 이동하는 범위에서 데이터를 확인하지 않으므로 코드에 검사를 포함하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-155">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>
>

<span data-ttu-id="981ba-156">이 예제에서는 분할된 데이터베이스 맵에서 분할된 데이터베이스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-156">This example removes shards from the shard map.</span></span> 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

<span data-ttu-id="981ba-157">분할된 데이터베이스 맵에 분할된 데이터베이스를 삭제하기 전에 GSM에서의 분할된 데이터베이스 위치가 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-157">The shard map reflects the shard location in the GSM before the deletion of the shard.</span></span> <span data-ttu-id="981ba-158">분할된 데이터베이스는 삭제되었기 때문에 의도적인 것으로 간주되며 분할 키 범위는 더 이상 사용 중이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-158">Because the shard was deleted, it is assumed this was intentional, and the sharding key range is no longer in use.</span></span> <span data-ttu-id="981ba-159">그렇지 않은 경우 특정 시점 복원을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-159">If not, you can execute point-in time restore.</span></span> <span data-ttu-id="981ba-160">이전 시점에서 분할된 데이터베이스를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-160">to recover the shard from an earlier point-in-time.</span></span> <span data-ttu-id="981ba-161">(이 경우, 다음 섹션을 검토하여 분할된 데이터베이스의 불일치를 감지하세요.) 복구하려면 [특정 시점 복구](sql-database-recovery-using-backups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="981ba-161">(In that case, review the following section to detect shard inconsistencies.) To recover, see [Point in time recovery](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="981ba-162">데이터베이스 삭제를 의도적인 것으로 가정하므로 최종 관리 정리 작업은 분할된 데이터베이스 맵 관리자에서 분할된 데이터베이스에 대한 항목을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-162">Since it is assumed the database deletion was intentional, the final administrative cleanup action is to delete the entry to the shard in the shard map manager.</span></span> <span data-ttu-id="981ba-163">이렇게 하면 응용 프로그램에서 예기치 않은 범위에 정보를 실수록 기록하는 일을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-163">This prevents the application from inadvertently writing information to a range that is not expected.</span></span>

## <a name="to-detect-mapping-differences"></a><span data-ttu-id="981ba-164">매핑 차이를 감지하려면</span><span class="sxs-lookup"><span data-stu-id="981ba-164">To detect mapping differences</span></span>
<span data-ttu-id="981ba-165">[DetectMappingDifferences 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) 는 원본으로 분할된 데이터베이스 맵(로컬 또는 전역) 중 하나를 선택하여 반환하고 두 분할된 데이터베이스 맵(GSM 및 LSM)에서 매핑을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-165">The [DetectMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) selects and returns one of the shard maps (either local or global) as the source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* <span data-ttu-id="981ba-166">*위치* 는 서버 이름과 데이터베이스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-166">The *location* specifies the server name and database name.</span></span> 
* <span data-ttu-id="981ba-167">*shardMapName* 매개 변수는 분할된 데이터베이스 맵 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-167">The *shardMapName* parameter is the shard map name.</span></span> <span data-ttu-id="981ba-168">여러 분할된 데이터베이스 맵을 동일한 분할된 데이터베이스 맵 관리자가 관리하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-168">This is only required if multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="981ba-169">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-169">Optional.</span></span> 

## <a name="to-resolve-mapping-differences"></a><span data-ttu-id="981ba-170">매핑 차이를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="981ba-170">To resolve mapping differences</span></span>
<span data-ttu-id="981ba-171">[ResolveMappingDifferences 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) 는 원본으로 분할된 데이터베이스 맵(로컬 또는 전역) 중 하나를 선택하고 두 분할된 데이터베이스 맵(GSM 및 LSM)에서 매핑을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-171">The [ResolveMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) selects one of the shard maps (either local or global) as the source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* <span data-ttu-id="981ba-172">*RecoveryToken* 매개 변수는 특정 분할된 데이터베이스에 대한 GSM 및 LSM 간의 매핑에서 차이를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-172">The *RecoveryToken* parameter enumerates the differences in the mappings between the GSM and the LSM for the specific shard.</span></span> 
* <span data-ttu-id="981ba-173">[MappingDifferenceResolution 열거](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) 는 분할된 데이터베이스 매핑 간 차이를 해결하기 위한 메서드를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-173">The [MappingDifferenceResolution enumeration](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) is used to indicate the method for resolving the difference between the shard mappings.</span></span> 
* <span data-ttu-id="981ba-174">**MappingDifferenceResolution.KeepShardMapping**은 LSM이 정확한 매핑을 포함하므로 분할된 데이터베이스의 매핑이 사용되는 경우에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-174">**MappingDifferenceResolution.KeepShardMapping** is recommended that when the LSM contains the accurate mapping and therefore the mapping in the shard should be used.</span></span> <span data-ttu-id="981ba-175">이 방법은 장애 조치 시 일반적인 사례입니다. 이제 분할된 데이터베이스는 새 서버에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-175">This is typically the case if there is a failover: the shard now resides on a new server.</span></span> <span data-ttu-id="981ba-176">분할된 데이터베이스는 GSM에서 먼저 제거되므로(RecoveryManager.DetachShard 메서드 사용) GSM에 매핑이 더 이상 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-176">Since the shard must first be removed from the GSM (using the RecoveryManager.DetachShard method), a mapping no longer exists on the GSM.</span></span> <span data-ttu-id="981ba-177">따라서 분할된 매핑을 다시 설정하기 위해 LSM을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-177">Therefore, the LSM must be used to re-establish the shard mapping.</span></span>

## <a name="attach-a-shard-to-the-shardmap-after-a-shard-is-restored"></a><span data-ttu-id="981ba-178">분할된 데이터베이스를 복원한 후 ShardMap에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-178">Attach a shard to the ShardMap after a shard is restored</span></span>
<span data-ttu-id="981ba-179">[AttachShard 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) 는 지정된 분할된 데이터베이스를 분할된 데이터베이스 맵에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-179">The [AttachShard method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) attaches the given shard to the shard map.</span></span> <span data-ttu-id="981ba-180">그런 다음 분할된 데이터베이스 맵의 불일치를 감지하고 분할된 데이터베이스 복원의 해당 지점에서 분할된 데이터베이스와 일치하도록 매핑을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-180">It then detects any shard map inconsistencies and updates the mappings to match the shard at the point of the shard restoration.</span></span> <span data-ttu-id="981ba-181">특정 시점 복원의 기본값은 타임스탬프가 추가된 새 데이터베이스이므로 데이터베이스가 원래 데이터베이스 이름(분할된 데이터베이스가 복원되기 이전)을 반영하도록 이름이 변경되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-181">It is assumed that the database is also renamed to reflect the original database name (before the shard was restored), since the point-in time restoration defaults to a new database appended with the timestamp.</span></span> 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* <span data-ttu-id="981ba-182">*location* 매개 변수는 분리 중인 분할된 데이터베이스의 서버 이름 및 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-182">The *location* parameter is the server name and database name, of the shard being attached.</span></span> 
* <span data-ttu-id="981ba-183">*shardMapName* 매개 변수는 분할된 데이터베이스 맵 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-183">The *shardMapName* parameter is the shard map name.</span></span> <span data-ttu-id="981ba-184">여러 분할된 데이터베이스 맵을 동일한 분할된 데이터베이스 맵 관리자가 관리하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-184">This is only required when multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="981ba-185">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-185">Optional.</span></span> 

<span data-ttu-id="981ba-186">이 예제는 분할된 데이터베이스를 최근 이전 시점에서 복원된 분할된 데이터베이스 맵에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-186">This example adds a shard to the shard map that has been recently restored from an earlier point-in time.</span></span> <span data-ttu-id="981ba-187">분할된 데이터베이스(즉, LSM에서 분할된 데이터베이스에 대한 매핑)를 복원한 후에는 GSM에서 분할된 데이터베이스 항목과 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-187">Since the shard (namely the mapping for the shard in the LSM) has been restored, it is potentially inconsistent with the shard entry in the GSM.</span></span> <span data-ttu-id="981ba-188">이 예제 코드 외부에서 분할된 데이터베이스가 복원되었고 데이터베이스의 원래 이름으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-188">Outside of this example code, the shard was restored and renamed to the original name of the database.</span></span> <span data-ttu-id="981ba-189">복원된 후에는 LSM에서의 매핑이 신뢰할 수 있는 매핑으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-189">Since it was restored, it is assumed the mapping in the LSM is the trusted mapping.</span></span> 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-the-shards"></a><span data-ttu-id="981ba-190">분할된 데이터베이스의 지역 장애 조치(복원) 후 분할된 데이터베이스 위치 업데이트</span><span class="sxs-lookup"><span data-stu-id="981ba-190">Updating shard locations after a geo-failover (restore) of the shards</span></span>
<span data-ttu-id="981ba-191">지역 장애 조치 시, 보조 데이터베이스가 쓸 수 있는 상태가 되고 새로운 주 데이터베이스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-191">If there is a geo-failover, the secondary database is made write accessible and becomes the new primary database.</span></span> <span data-ttu-id="981ba-192">서버와 잠재적으로 데이터베이스의 이름(구성에 따라 다름)은 원래 주 데이터베이스와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-192">The name of the server, and potentially the database (depending on your configuration), may be different from the original primary.</span></span> <span data-ttu-id="981ba-193">따라서 GSM 및 LSM에서 분할된 데이터베이스에 대한 매핑 항목을 고정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-193">Therefore the mapping entries for the shard in the GSM and LSM must be fixed.</span></span> <span data-ttu-id="981ba-194">마찬가지로, 데이터베이스가 다른 이름 또는 위치로 복원되거나 이전 시점으로 복원되면 분할된 데이터베이스 맵에서 불일치가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-194">Similarly, if the database is restored to a different name or location, or to an earlier point in time, this might cause inconsistencies in the shard maps.</span></span> <span data-ttu-id="981ba-195">분할된 데이터베이스 맵 관리자가 올바른 데이터베이스에 대해 열려 있는 연결의 배포를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-195">The Shard Map Manager handles the distribution of open connections to the correct database.</span></span> <span data-ttu-id="981ba-196">배포는 분할된 맵의 데이터와 응용 프로그램의 요청 대상인 분할 키의 값을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-196">Distribution is based on the data in the shard map and the value of the sharding key that is the target of the applications request.</span></span> <span data-ttu-id="981ba-197">지역 장애 조치 후 이 정보를 정확한 서버 이름, 데이터베이스 이름 및 복구된 데이터베이스의 분할된 데이터베이스 매핑으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-197">After a geo-failover, this information must be updated with the accurate server name, database name and shard mapping of the recovered database.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="981ba-198">모범 사례</span><span class="sxs-lookup"><span data-stu-id="981ba-198">Best practices</span></span>
<span data-ttu-id="981ba-199">지역 장애 조치(failover) 및 복구는 의도적으로 Azure SQL 데이터베이스 무중단 업무 방식 기능 중 하나를 활용하는 응용 프로그램의 클라우드 관리자가 일반적으로 관리하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-199">Geo-failover and recovery are operations typically managed by a cloud administrator of the application intentionally utilizing one of Azure SQL Databases business continuity features.</span></span> <span data-ttu-id="981ba-200">비즈니스 연속성 계획에는 비즈니스 작업을 중단 없이 계속할 수 있도록 보장해주는 프로세스, 절차 및 측정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-200">Business continuity planning requires processes, procedures, and measures to ensure that business operations can continue without interruption.</span></span> <span data-ttu-id="981ba-201">이 워크플로 내에서 RecoveryManager 클래스의 일부로 제공되는 메서드를 사용하여 수행되는 복구 작업에 따라 GSM 및 LSM이 최신 상태로 유지되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-201">The methods available as part of the RecoveryManager class should be used within this work flow to ensure the GSM and LSM are kept up-to-date based on the recovery action taken.</span></span> <span data-ttu-id="981ba-202">장애 조치 이벤트 후 GSM 및 LSM이 정확한 정보를 반영하도록 제대로 보장하는 5가지 기본 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-202">There are five basic steps to properly ensuring the GSM and LSM reflect the accurate information after a failover event.</span></span> <span data-ttu-id="981ba-203">이러한 단계를 실행할 응용 프로그램 코드를 기존 도구 및 워크플로에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-203">The application code to execute these steps can be integrated into existing tools and workflow.</span></span> 

1. <span data-ttu-id="981ba-204">ShardMapManager에서 RecoveryManager를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-204">Retrieve the RecoveryManager from the ShardMapManager.</span></span> 
2. <span data-ttu-id="981ba-205">분할된 데이터베이스 맵에서 이전 분할된 데이터베이스를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-205">Detach the old shard from the shard map.</span></span>
3. <span data-ttu-id="981ba-206">새 분할된 데이터베이스 위치를 포함하여 새 분할된 데이터베이스를 분할된 데이터베이스 맵에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-206">Attach the new shard to the shard map, including the new shard location.</span></span>
4. <span data-ttu-id="981ba-207">GSM 및 LSM 간의 매핑에서 불일치를 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-207">Detect inconsistencies in the mapping between the GSM and LSM.</span></span> 
5. <span data-ttu-id="981ba-208">LSM을 신뢰하여 GSM 및 LSM 간의 차이를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-208">Resolve differences between the GSM and the LSM, trusting the LSM.</span></span> 

<span data-ttu-id="981ba-209">이 예제에서는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-209">This example performs the following steps:</span></span>

1. <span data-ttu-id="981ba-210">장애 조치 이벤트 이전에, 분할된 데이터베이스 위치를 반영하는 분할된 데이터베이스 맵에서 분할된 데이터베이스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-210">Removes shards from the Shard Map that reflect shard locations before the failover event.</span></span>
2. <span data-ttu-id="981ba-211">분할된 데이터베이스를 새 분할된 데이터베이스 위치를 반영하는 분할된 데이터베이스 맵에 연결합니다("Configuration.SecondaryServer" 매개 변수는 새로운 서버 이름이지만 동일한 데이터베이스 이름입니다).</span><span class="sxs-lookup"><span data-stu-id="981ba-211">Attaches shards to the Shard Map reflecting the new shard locations (the parameter "Configuration.SecondaryServer" is the new server name but the same database name).</span></span>
3. <span data-ttu-id="981ba-212">각 분할된 데이터베이스에 대해 GSM 및 LSM 간의 매핑 차이를 감지하여 복구 토큰을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-212">Retrieves the recovery tokens by detecting mapping differences between the GSM and the LSM for each shard.</span></span> 
4. <span data-ttu-id="981ba-213">각 분할된 데이터베이스의 LSM에서 매핑을 신뢰하여 불일치를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="981ba-213">Resolves the inconsistencies by trusting the mapping from the LSM of each shard.</span></span> 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

