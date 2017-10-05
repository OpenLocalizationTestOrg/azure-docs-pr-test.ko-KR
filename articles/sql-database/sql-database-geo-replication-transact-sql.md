---
title: "Transact-SQL로 Azure SQL Database에 대한 지역에서 복제 구성 | Microsoft Docs"
description: "Transact-SQL을 사용하여 Azure SQL Database에 대한 지역에서 복제 구성"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: e5011c1c67e051616d53621b72e46ba894ca3c02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="59f4b-103">TRANSACT-SQL로 Azure SQL Database에 대한 활성 지역 복제 구성</span><span class="sxs-lookup"><span data-stu-id="59f4b-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="59f4b-104">이 문서에서는 Transact-SQL을 사용하여 Azure SQL Database에 대한 활성 지역 복제를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-104">This article shows you how to configure active geo-replication for an Azure SQL Database with Transact-SQL.</span></span>

<span data-ttu-id="59f4b-105">Transact-SQL을 사용하여 장애 조치(Failover)를 시작하려면 [Transact-SQL로 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치(Failover) 시작](sql-database-geo-replication-failover-transact-sql.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-105">To initiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span></span>

> [!NOTE]
> <span data-ttu-id="59f4b-106">재해 복구를 위해 활성 지역 복제(읽을 수 있는 보조)를 사용하는 경우 자동 및 투명한 장애 조치를 수행할 수 있도록 응용 프로그램 내의 모든 데이터베이스에 대해 장애 조치 그룹을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-106">When you use active geo-replication (readable secondaries) for disaster recovery you should configure a failover group for all databases within an application to enable automatic and transparent failover.</span></span> <span data-ttu-id="59f4b-107">이 기능은 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-107">This feature is in preview.</span></span> <span data-ttu-id="59f4b-108">자세한 내용은 [자동 장애 조치 그룹 및 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-108">For more information see [Auto-failover groups and geo-replication](sql-database-geo-replication-overview.md).</span></span>
> 
> 

<span data-ttu-id="59f4b-109">Transact-SQL을 사용하여 활성 지역 복제를 구성하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-109">To configure active geo-replication using Transact-SQL, you need the following:</span></span>

* <span data-ttu-id="59f4b-110">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="59f4b-110">An Azure subscription</span></span>
* <span data-ttu-id="59f4b-111">논리 Azure SQL Database 서버 <MyLocalServer> 및 SQL 데이터베이스 <MyDB> - 복제하려는 주 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-111">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - The primary database that you want to replicate</span></span>
* <span data-ttu-id="59f4b-112">하나 이상의 논리 Azure SQL Database 서버 <MySecondaryServer(n)> - 보조 데이터베이스를 만드는 파트너 서버가 될 논리 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-112">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - The logical servers that will be the partner servers in which you will create secondary databases</span></span>
* <span data-ttu-id="59f4b-113">주 서버에서 DBManager로 로그인</span><span class="sxs-lookup"><span data-stu-id="59f4b-113">A login that is DBManager on the primary</span></span>
* <span data-ttu-id="59f4b-114">지역에서 복제할 로컬 데이터베이스의 db_ownership 보유</span><span class="sxs-lookup"><span data-stu-id="59f4b-114">Have db_ownership of the local database that you will geo-replicate</span></span>
* <span data-ttu-id="59f4b-115">지역에서 복제를 구성하는 파트너 서버의 DBManager</span><span class="sxs-lookup"><span data-stu-id="59f4b-115">Be DBManager on the partner server(s) to which you will configure geo-replication</span></span>
* <span data-ttu-id="59f4b-116">최신 버전의 SSMS(SQL Server Management Studio)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-116">The newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59f4b-117">Microsoft Azure 및 SQL 데이터베이스에 대한 업데이트와 동기화 상태를 유지하려면 항상 최신 버전의 Management Studio를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-117">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="59f4b-118">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="59f4b-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

## <a name="add-secondary-database"></a><span data-ttu-id="59f4b-119">보조 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="59f4b-119">Add secondary database</span></span>
<span data-ttu-id="59f4b-120">**ALTER DATABASE** 문을 사용하여 파트너 서버에서 지역에서 복제된 보조 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-120">You can use the **ALTER DATABASE** statement to create a geo-replicated secondary database on a partner server.</span></span> <span data-ttu-id="59f4b-121">복제할 데이터베이스를 포함하는 서버의 마스터 데이터베이스에서 이 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-121">You execute this statement on the master database of the server containing the database to be replicated.</span></span> <span data-ttu-id="59f4b-122">지역에서 복제된 데이터베이스("주 데이터베이스")는 복제되는 데이터베이스와 동일한 이름을 가지며 기본적으로 주 데이터베이스와 동일한 서비스 수준을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-122">The geo-replicated database (the "primary database") will have the same name as the database being replicated and will, by default, have the same service level as the primary database.</span></span> <span data-ttu-id="59f4b-123">보조 데이터베이스는 읽을 수 있거나 읽을 수 없을 수 있으며 단일 데이터베이스 또는 탄력적 풀에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-123">The secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span></span> <span data-ttu-id="59f4b-124">자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="59f4b-125">보조 데이터베이스가 만들어지고 시드된 후 데이터는 주 데이터베이스에서 비동기적으로 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-125">After the secondary database is created and seeded, data will begin replicating asynchronously from the primary database.</span></span> <span data-ttu-id="59f4b-126">다음 단계에서는 Management Studio를 사용하여 지역에서 복제를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-126">The steps below describe how to configure geo-replication using Management Studio.</span></span> <span data-ttu-id="59f4b-127">단일 데이터베이스 또는 탄력적 풀로 읽을 수 없는 및 읽을 수 있는 보조를 만드는 단계가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-127">Steps to create non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span></span>

> [!NOTE]
> <span data-ttu-id="59f4b-128">데이터베이스가 주 데이터베이스와 같은 이름으로 지정된 파트너 서버에 있는 경우 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-128">If a database exists on the specified partner server with the same name as the primary database the command will fail.</span></span>
> 

### <a name="add-readable-secondary-single-database"></a><span data-ttu-id="59f4b-129">읽을 수 있는 보조(단일 데이터베이스) 추가</span><span class="sxs-lookup"><span data-stu-id="59f4b-129">Add readable secondary (single database)</span></span>
<span data-ttu-id="59f4b-130">단일 데이터베이스로 읽을 수 있는 보조를 만들려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-130">Use the following steps to create a readable secondary as a single database.</span></span>

1. <span data-ttu-id="59f4b-131">Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-131">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="59f4b-132">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-132">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="59f4b-133">다음 **ALTER DATABASE** 문을 사용하여 로컬 데이터베이스를 지역에서 복제 주 데이터베이스(보조 서버의 읽을 수 있는 보조 데이터베이스와 함께)로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-133">Use the following **ALTER DATABASE** statement to make a local database into a geo-replication primary with a readable secondary database on a secondary server.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. <span data-ttu-id="59f4b-134">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-134">Click **Execute** to run the query.</span></span>

### <a name="add-readable-secondary-elastic-pool"></a><span data-ttu-id="59f4b-135">읽을 수 있는 보조(탄력적 풀) 추가</span><span class="sxs-lookup"><span data-stu-id="59f4b-135">Add readable secondary (elastic pool)</span></span>
<span data-ttu-id="59f4b-136">탄력적 풀에서 읽을 수 있는 보조를 만들려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-136">Use the following steps to create a readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="59f4b-137">Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-137">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="59f4b-138">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-138">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="59f4b-139">다음 **ALTER DATABASE** 문을 사용하여 로컬 데이터베이스를 지역에서 복제 주 데이터베이스(탄력적 풀에 포함된 보조 서버의 읽을 수 있는 보조 데이터베이스와 함께)로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-139">Use the following **ALTER DATABASE** statement to make a local database into a geo-replication primary with a readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. <span data-ttu-id="59f4b-140">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-140">Click **Execute** to run the query.</span></span>

## <a name="remove-secondary-database"></a><span data-ttu-id="59f4b-141">보조 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="59f4b-141">Remove secondary database</span></span>
<span data-ttu-id="59f4b-142">**ALTER DATABASE** 문을 사용하여 보조 데이터베이스와 주 데이터베이스 간의 복제 파트너 관계를 영구적으로 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-142">You can use the **ALTER DATABASE** statement to permanently terminate the replication partnership between a secondary database and its primary.</span></span> <span data-ttu-id="59f4b-143">이 문은 주 데이터베이스가 상주하는 마스터 데이터베이스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-143">This statement is executed on the master database on which the primary database resides.</span></span> <span data-ttu-id="59f4b-144">관계가 종료된 후 보조 데이터베이스는 일반 읽기-쓰기 데이터베이스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-144">After the relationship termination, the secondary database becomes a regular read-write database.</span></span> <span data-ttu-id="59f4b-145">보조 데이터베이스에 대한 연결이 끊어진 경우 명령이 성공하지만 연결이 복원된 후 보조는 읽기-쓰기가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-145">If the connectivity to secondary database is broken the command succeeds but the secondary will become read-write after connectivity is restored.</span></span> <span data-ttu-id="59f4b-146">자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-146">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="59f4b-147">지역에서 복제 파트너 관계에서 지역에서 복제된 보조 데이터베이스를 제거하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-147">Use the following steps to remove geo-replicated secondary from a geo-replication partnership.</span></span>

1. <span data-ttu-id="59f4b-148">Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-148">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="59f4b-149">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-149">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="59f4b-150">다음 **ALTER DATABASE** 문을 사용하여 지역에서 복제된 보조 데이터베이스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-150">Use the following **ALTER DATABASE** statement to remove a geo-replicated secondary.</span></span>
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. <span data-ttu-id="59f4b-151">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-151">Click **Execute** to run the query.</span></span>

## <a name="monitor-active-geo-replication-configuration-and-health"></a><span data-ttu-id="59f4b-152">활성 지역 복제 구성 및 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="59f4b-152">Monitor active geo-replication configuration and health</span></span>

<span data-ttu-id="59f4b-153">모니터링 작업에는 지역에서 복제 구성의 모니터링 및 데이터 복제 상태 모니터링이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-153">Monitoring tasks include monitoring of the geo-replication configuration and monitoring data replication health.</span></span>  <span data-ttu-id="59f4b-154">마스터 데이터베이스의 **sys.dm_geo_replication_links** 동적 관리 뷰를 사용하여 Azure SQL Database 논리 서버의 각 데이터베이스에 대한 모든 기존 복제 링크에 대한 정보를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-154">You can use the **sys.dm_geo_replication_links** dynamic management view in the master database to return information about all exiting replication links for each database on the Azure SQL Database logical server.</span></span> <span data-ttu-id="59f4b-155">이 뷰는 주 및 보조 데이터베이스 간의 각 복제 링크에 대한 행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-155">This view contains a row for each of the replication link between primary and secondary databases.</span></span> <span data-ttu-id="59f4b-156">**sys.dm_replication_status** 동적 관리 뷰를 사용하여 현재 복제 링크에 참여하는 각 Azure SQL Database에 대한 행을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-156">You can use the **sys.dm_replication_link_status** dynamic management view to return a row for each Azure SQL Database that is currently engaged in a replication replication link.</span></span> <span data-ttu-id="59f4b-157">주 및 보조 데이터베이스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-157">This includes both primary and secondary databases.</span></span> <span data-ttu-id="59f4b-158">지정된 주 데이터베이스에 두 개 이상의 연속 복제 링크가 있는 경우 이 테이블은 각 관계에 대한 행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-158">If more than one continuous replication link exists for a given primary database, this table contains a row for each of the relationships.</span></span> <span data-ttu-id="59f4b-159">논리 마스터를 포함한 모든 데이터베이스에 뷰가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-159">The view is created in all databases, including the logical master.</span></span> <span data-ttu-id="59f4b-160">그러나 논리 마스터에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-160">However, querying this view in the logical master returns an empty set.</span></span> <span data-ttu-id="59f4b-161">**sys.dm_operation_status** 동적 관리 뷰를 사용하여 복제 링크의 상태를 포함하는 모든 데이터베이스 작업에 대한 상태를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-161">You can use the **sys.dm_operation_status** dynamic management view to show the status for all database operations including the status of the replication links.</span></span> <span data-ttu-id="59f4b-162">자세한 내용은 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 및 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-162">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span></span>

<span data-ttu-id="59f4b-163">활성 지역 복제 파트너 관계를 모니터링하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-163">Use the following steps to monitor an active geo-replication partnership.</span></span>

1. <span data-ttu-id="59f4b-164">Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-164">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="59f4b-165">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-165">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="59f4b-166">지역에서 복제 링크와 함께 모든 데이터베이스를 표시하려면 다음 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-166">Use the following statement to show all databases with geo-replication links.</span></span>
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. <span data-ttu-id="59f4b-167">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-167">Click **Execute** to run the query.</span></span>
5. <span data-ttu-id="59f4b-168">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **MyDB**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-168">Open the Databases folder, expand the **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span></span>
6. <span data-ttu-id="59f4b-169">다음 문을 사용하여 복제 지연 및 MyDB의 보조 데이터베이스의 마지막 복제 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-169">Use the following statement to show the replication lags and last replication time of my secondary databases of MyDB.</span></span>
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. <span data-ttu-id="59f4b-170">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-170">Click **Execute** to run the query.</span></span>
8. <span data-ttu-id="59f4b-171">다음 문을 사용하여 데이터베이스 MyDB와 연결되는 가장 최근의 지역에서 복제 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-171">Use the following statement to show the most recent geo-replication operations associated with database MyDB.</span></span>
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. <span data-ttu-id="59f4b-172">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f4b-172">Click **Execute** to run the query.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59f4b-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59f4b-173">Next steps</span></span>
* <span data-ttu-id="59f4b-174">장애 조치 그룹과 활성 지역 복제에 대한 자세한 내용은 [장애 조치 그룹](sql-database-geo-replication-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f4b-174">To learn more about failover groups and active geo-replication, see - [Failover groups](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="59f4b-175">비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="59f4b-175">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>

