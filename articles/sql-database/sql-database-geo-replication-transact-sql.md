---
title: "Transact SQL와 Azure SQL 데이터베이스의 지역 간 복제 aaaConfigure | Microsoft Docs"
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
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="07df4-103">TRANSACT-SQL로 Azure SQL Database에 대한 활성 지역 복제 구성</span><span class="sxs-lookup"><span data-stu-id="07df4-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="07df4-104">이 문서에서는 어떻게 tooconfigure 활성 지리적 복제는 Azure SQL 데이터베이스 TRANSACT-SQL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-104">This article shows you how tooconfigure active geo-replication for an Azure SQL Database with Transact-SQL.</span></span>

<span data-ttu-id="07df4-105">TRANSACT-SQL을 사용 하 여 tooinitiate 장애 조치 참조 [TRANSACT-SQL와 Azure SQL 데이터베이스에 대 한 계획 되거나 계획 되지 않은 장애 조치의 시작](sql-database-geo-replication-failover-transact-sql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-105">tooinitiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span></span>

> [!NOTE]
> <span data-ttu-id="07df4-106">재해 복구용 활성 지리적 복제 (읽기 가능한 보조 복제본)를 사용 하는 경우 응용 프로그램 tooenable 자동 및 투명 장애 내의 모든 데이터베이스에 대 한 장애 조치 그룹을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-106">When you use active geo-replication (readable secondaries) for disaster recovery you should configure a failover group for all databases within an application tooenable automatic and transparent failover.</span></span> <span data-ttu-id="07df4-107">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-107">This feature is in preview.</span></span> <span data-ttu-id="07df4-108">자세한 내용은 [자동 장애 조치 그룹 및 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07df4-108">For more information see [Auto-failover groups and geo-replication](sql-database-geo-replication-overview.md).</span></span>
> 
> 

<span data-ttu-id="07df4-109">tooconfigure 활성 지리적 복제 hello 다음 필요한 TRANSACT-SQL을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="07df4-109">tooconfigure active geo-replication using Transact-SQL, you need hello following:</span></span>

* <span data-ttu-id="07df4-110">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="07df4-110">An Azure subscription</span></span>
* <span data-ttu-id="07df4-111">Azure SQL 데이터베이스 논리 서버 <MyLocalServer> 및 SQL 데이터베이스 <MyDB> -tooreplicate 원하는 hello 주 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="07df4-111">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - hello primary database that you want tooreplicate</span></span>
* <span data-ttu-id="07df4-112">하나 이상의 논리 Azure SQL 데이터베이스 서버 < MySecondaryServer(n)-> 보조 데이터베이스에서는 hello 파트너 서버 될 hello 논리 서버</span><span class="sxs-lookup"><span data-stu-id="07df4-112">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - hello logical servers that will be hello partner servers in which you will create secondary databases</span></span>
* <span data-ttu-id="07df4-113">기본 hello DBManager 켜져 있는 로그인</span><span class="sxs-lookup"><span data-stu-id="07df4-113">A login that is DBManager on hello primary</span></span>
* <span data-ttu-id="07df4-114">지역 간 복제 한다는 hello 로컬 데이터베이스의 db_ownership이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-114">Have db_ownership of hello local database that you will geo-replicate</span></span>
* <span data-ttu-id="07df4-115">Hello 파트너 서버 toowhich DBManager 켜야 지리적 복제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-115">Be DBManager on hello partner server(s) toowhich you will configure geo-replication</span></span>
* <span data-ttu-id="07df4-116">hello 최신 버전 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="07df4-116">hello newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07df4-117">항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-117">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="07df4-118">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="07df4-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

## <a name="add-secondary-database"></a><span data-ttu-id="07df4-119">보조 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="07df4-119">Add secondary database</span></span>
<span data-ttu-id="07df4-120">Hello를 사용할 수 있습니다 **ALTER DATABASE** 문 toocreate 파트너 서버에서 보조 데이터베이스 지리적으로 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-120">You can use hello **ALTER DATABASE** statement toocreate a geo-replicated secondary database on a partner server.</span></span> <span data-ttu-id="07df4-121">Hello 서버 포함 hello 데이터베이스 toobe 복제의 hello master 데이터베이스에서이 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-121">You execute this statement on hello master database of hello server containing hello database toobe replicated.</span></span> <span data-ttu-id="07df4-122">hello 지리적으로 복제 된 데이터베이스 (hello "기본 데이터베이스")에 적용 됩니다 hello 데이터베이스 복제 되 고 기본적으로이 hello로 이름과 같은 이름을 hello hello 주 데이터베이스와 같은 서비스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-122">hello geo-replicated database (hello "primary database") will have hello same name as hello database being replicated and will, by default, have hello same service level as hello primary database.</span></span> <span data-ttu-id="07df4-123">hello 보조 데이터베이스 읽기 가능 인지 또는 읽을 수 없는 수와 단일 데이터베이스가 될 수 있습니다 또는 탄력적인 풀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-123">hello secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span></span> <span data-ttu-id="07df4-124">자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07df4-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="07df4-125">Hello 보조 데이터베이스를 만들고 시드 된 후 데이터 hello 주 데이터베이스에서 비동기적으로 복제를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-125">After hello secondary database is created and seeded, data will begin replicating asynchronously from hello primary database.</span></span> <span data-ttu-id="07df4-126">다음 hello 단계에서는 어떻게 tooconfigure 지리적 복제 Management Studio를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-126">hello steps below describe how tooconfigure geo-replication using Management Studio.</span></span> <span data-ttu-id="07df4-127">단계 toocreate 읽을 수 없는 및 읽기 가능한 보조 복제본을 단일 데이터베이스 또는 탄력적 풀에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-127">Steps toocreate non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span></span>

> [!NOTE]
> <span data-ttu-id="07df4-128">데이터베이스가 기본 hello 이름이 hello로 지정 된 파트너 서버 hello에 있는 데이터베이스 hello 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-128">If a database exists on hello specified partner server with hello same name as hello primary database hello command will fail.</span></span>
> 

### <a name="add-readable-secondary-single-database"></a><span data-ttu-id="07df4-129">읽을 수 있는 보조(단일 데이터베이스) 추가</span><span class="sxs-lookup"><span data-stu-id="07df4-129">Add readable secondary (single database)</span></span>
<span data-ttu-id="07df4-130">다음 단계를 단일 데이터베이스로 읽기 가능한 보조 toocreate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-130">Use hello following steps toocreate a readable secondary as a single database.</span></span>

1. <span data-ttu-id="07df4-131">Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-131">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="07df4-132">Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-132">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="07df4-133">Hello 다음을 사용 하 여 **ALTER DATABASE** 문 toomake 보조 서버에서 읽기 가능한 보조 데이터베이스와 지역 복제 주에 로컬 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-133">Use hello following **ALTER DATABASE** statement toomake a local database into a geo-replication primary with a readable secondary database on a secondary server.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. <span data-ttu-id="07df4-134">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-134">Click **Execute** toorun hello query.</span></span>

### <a name="add-readable-secondary-elastic-pool"></a><span data-ttu-id="07df4-135">읽을 수 있는 보조(탄력적 풀) 추가</span><span class="sxs-lookup"><span data-stu-id="07df4-135">Add readable secondary (elastic pool)</span></span>
<span data-ttu-id="07df4-136">다음 단계 toocreate 탄력적 풀의 읽기 가능한 보조 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-136">Use hello following steps toocreate a readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="07df4-137">Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-137">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="07df4-138">Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-138">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="07df4-139">Hello 다음을 사용 하 여 **ALTER DATABASE** 문 toomake 탄력적 풀의 보조 서버에서 읽기 가능한 보조 데이터베이스와 지역 복제 주에 로컬 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-139">Use hello following **ALTER DATABASE** statement toomake a local database into a geo-replication primary with a readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. <span data-ttu-id="07df4-140">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-140">Click **Execute** toorun hello query.</span></span>

## <a name="remove-secondary-database"></a><span data-ttu-id="07df4-141">보조 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="07df4-141">Remove secondary database</span></span>
<span data-ttu-id="07df4-142">Hello를 사용할 수 있습니다 **ALTER DATABASE** 문을 toopermanently 보조 데이터베이스와 주 도메인 컨트롤러 간의 hello 복제 파트너 관계를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-142">You can use hello **ALTER DATABASE** statement toopermanently terminate hello replication partnership between a secondary database and its primary.</span></span> <span data-ttu-id="07df4-143">이 문은 주 데이터베이스가 있는 어떤 hello에 hello master 데이터베이스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-143">This statement is executed on hello master database on which hello primary database resides.</span></span> <span data-ttu-id="07df4-144">Hello 관계 종료 후 hello 보조 데이터베이스 일반 읽기 / 쓰기 데이터베이스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-144">After hello relationship termination, hello secondary database becomes a regular read-write database.</span></span> <span data-ttu-id="07df4-145">Hello 연결 toosecondary 데이터베이스 중단 된 hello 명령이 성공 수 있지만 연결이 복원 된 후 보조 hello 읽기 / 쓰기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-145">If hello connectivity toosecondary database is broken hello command succeeds but hello secondary will become read-write after connectivity is restored.</span></span> <span data-ttu-id="07df4-146">자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07df4-146">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="07df4-147">지리적 복제 파트너 관계에서 단계 tooremove 지리적 복제 보조를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-147">Use hello following steps tooremove geo-replicated secondary from a geo-replication partnership.</span></span>

1. <span data-ttu-id="07df4-148">Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-148">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="07df4-149">Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-149">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="07df4-150">Hello 다음을 사용 하 여 **ALTER DATABASE** 문 tooremove 지리적 복제 보조 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-150">Use hello following **ALTER DATABASE** statement tooremove a geo-replicated secondary.</span></span>
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. <span data-ttu-id="07df4-151">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-151">Click **Execute** toorun hello query.</span></span>

## <a name="monitor-active-geo-replication-configuration-and-health"></a><span data-ttu-id="07df4-152">활성 지역 복제 구성 및 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="07df4-152">Monitor active geo-replication configuration and health</span></span>

<span data-ttu-id="07df4-153">모니터링 작업 hello 지리적 복제 구성의 모니터링 및 데이터 복제 상태 모니터링에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-153">Monitoring tasks include monitoring of hello geo-replication configuration and monitoring data replication health.</span></span>  <span data-ttu-id="07df4-154">Hello를 사용할 수 있습니다 **sys.dm_geo_replication_links** hello Azure SQL 데이터베이스 논리 서버에 hello master 데이터베이스 tooreturn 정보 각 데이터베이스에 대 한 모든 기존 복제 링크에 대 한 동적 관리 뷰.</span><span class="sxs-lookup"><span data-stu-id="07df4-154">You can use hello **sys.dm_geo_replication_links** dynamic management view in hello master database tooreturn information about all exiting replication links for each database on hello Azure SQL Database logical server.</span></span> <span data-ttu-id="07df4-155">이 보기는 각 주 데이터베이스와 보조 데이터베이스 간의 복제 링크 hello에 대 한 한 행을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-155">This view contains a row for each of hello replication link between primary and secondary databases.</span></span> <span data-ttu-id="07df4-156">Hello를 사용할 수 있습니다 **sys.dm_replication_link_status** 동적 관리 뷰를 tooreturn 행 복제 복제 링크에 현재 참여 하는 각 Azure SQL 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-156">You can use hello **sys.dm_replication_link_status** dynamic management view tooreturn a row for each Azure SQL Database that is currently engaged in a replication replication link.</span></span> <span data-ttu-id="07df4-157">주 및 보조 데이터베이스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-157">This includes both primary and secondary databases.</span></span> <span data-ttu-id="07df4-158">지정된 된 주 데이터베이스에 대 한 연속 복제 링크를 두 개 이상 있는 경우이 테이블 각 hello 관계의 한 행을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-158">If more than one continuous replication link exists for a given primary database, this table contains a row for each of hello relationships.</span></span> <span data-ttu-id="07df4-159">hello 뷰가 hello 논리 master를 포함 하는 모든 데이터베이스에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-159">hello view is created in all databases, including hello logical master.</span></span> <span data-ttu-id="07df4-160">그러나 hello 논리 master에서이 뷰를 쿼리하면 빈 집합이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-160">However, querying this view in hello logical master returns an empty set.</span></span> <span data-ttu-id="07df4-161">Hello를 사용할 수 있습니다 **sys.dm_operation_status** hello 복제 링크의 hello 상태를 포함 하 여 작업 한 모든 데이터베이스에 대 한 동적 관리 tooshow hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-161">You can use hello **sys.dm_operation_status** dynamic management view tooshow hello status for all database operations including hello status of hello replication links.</span></span> <span data-ttu-id="07df4-162">자세한 내용은 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 및 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07df4-162">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span></span>

<span data-ttu-id="07df4-163">다음 단계 toomonitor 활성 지리적 복제 파트너 관계 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-163">Use hello following steps toomonitor an active geo-replication partnership.</span></span>

1. <span data-ttu-id="07df4-164">Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-164">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="07df4-165">Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-165">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="07df4-166">지리적 복제 링크가 있는 hello 문을 tooshow 다음 모든 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-166">Use hello following statement tooshow all databases with geo-replication links.</span></span>
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. <span data-ttu-id="07df4-167">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-167">Click **Execute** toorun hello query.</span></span>
5. <span data-ttu-id="07df4-168">Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **MyDB**, 클릭 하 고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-168">Open hello Databases folder, expand hello **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span></span>
6. <span data-ttu-id="07df4-169">다음 문은 tooshow hello 복제 사용 하 여 hello 만큼 이전 성과 MyDB의 보조 데이터베이스의 복제 시간.</span><span class="sxs-lookup"><span data-stu-id="07df4-169">Use hello following statement tooshow hello replication lags and last replication time of my secondary databases of MyDB.</span></span>
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. <span data-ttu-id="07df4-170">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-170">Click **Execute** toorun hello query.</span></span>
8. <span data-ttu-id="07df4-171">문을 tooshow hello 가장 최근의 지리적 복제 작업 MyDB 데이터베이스와 관련 된 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-171">Use hello following statement tooshow hello most recent geo-replication operations associated with database MyDB.</span></span>
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. <span data-ttu-id="07df4-172">클릭 **Execute** toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07df4-172">Click **Execute** toorun hello query.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07df4-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07df4-173">Next steps</span></span>
* <span data-ttu-id="07df4-174">장애 조치 그룹 및 활성 지리적 복제에 대해 자세히 toolearn 참조- [장애 조치 그룹](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="07df4-174">toolearn more about failover groups and active geo-replication, see - [Failover groups](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="07df4-175">비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="07df4-175">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>

