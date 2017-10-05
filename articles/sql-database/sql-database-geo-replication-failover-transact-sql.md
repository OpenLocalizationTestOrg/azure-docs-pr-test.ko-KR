---
title: "TSQL:Azure SQL Database에 대한 장애 조치(failover) 시작 | Microsoft Docs"
description: "Transact-SQL을 사용하여 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치 시작"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 459941d2c82e5d4ef62beab4ccf775ab8f5efce4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="25ecd-103">Transact-SQL로 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치 시작</span><span class="sxs-lookup"><span data-stu-id="25ecd-103">Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="25ecd-104">이 문서에서는 Transact-SQL을 사용하여 보조 SQL 데이터베이스로 장애 조치(failover)를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-104">This article shows you how to initiate failover to a secondary SQL Database using Transact-SQL.</span></span> <span data-ttu-id="25ecd-105">지역에서 복제를 구성하려면 [Azure SQL Database에 대한 지역에서 복제 구성](sql-database-geo-replication-transact-sql.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-105">To configure geo-replication, see [Configure geo-replication for Azure SQL Database](sql-database-geo-replication-transact-sql.md).</span></span>

<span data-ttu-id="25ecd-106">장애 조치를 시작하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-106">To initiate failover, you need the following:</span></span>

* <span data-ttu-id="25ecd-107">주 서버에서 DBManager로 로그인</span><span class="sxs-lookup"><span data-stu-id="25ecd-107">A login that is DBManager on the primary</span></span>
* <span data-ttu-id="25ecd-108">지역에서 복제할 로컬 데이터베이스의 db_ownership 보유</span><span class="sxs-lookup"><span data-stu-id="25ecd-108">Have db_ownership of the local database that you will geo-replicate</span></span>
* <span data-ttu-id="25ecd-109">지역에서 복제를 구성하는 파트너 서버의 DBManager</span><span class="sxs-lookup"><span data-stu-id="25ecd-109">Be DBManager on the partner server(s) to which you will configure geo-replication</span></span>
* <span data-ttu-id="25ecd-110">최신 버전의 SSMS(SQL Server Management Studio)</span><span class="sxs-lookup"><span data-stu-id="25ecd-110">Newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25ecd-111">Microsoft Azure 및 SQL 데이터베이스에 대한 업데이트와 동기화 상태를 유지하려면 항상 최신 버전의 Management Studio를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-111">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="25ecd-112">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="25ecd-112">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-to-become-the-new-primary"></a><span data-ttu-id="25ecd-113">새 주 데이터베이스가 되도록 보조 데이터베이스를 승격하는 계획된 장애 조치 시작</span><span class="sxs-lookup"><span data-stu-id="25ecd-113">Initiate a planned failover promoting a secondary database to become the new primary</span></span>
<span data-ttu-id="25ecd-114">**ALTER DATABASE** 문을 사용하여 기존 주가 보조가 되도록 강등시키는 계획된 방식으로 보조 데이터베이스가 새로운 주 데이터베이스가 되도록 승격할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-114">You can use the **ALTER DATABASE** statement to promote a secondary database to become the new primary database in a planned fashion, demoting the existing primary to become a secondary.</span></span> <span data-ttu-id="25ecd-115">이 문은 승격되는 지역에서 복제된 보조 데이터베이스가 상주하는 Azure SQL 데이터베이스 논리 서버의 마스터 데이터베이스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-115">This statement is executed on the master database on the Azure SQL Database logical server in which the geo-replicated secondary database that is being promoted resides.</span></span> <span data-ttu-id="25ecd-116">이 기능은 DR 훈련 중과 같은 계획된 장애 조치에 대해 설계되었으며 주 데이터베이스는 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-116">This functionality is designed for planned failover, such as during the DR drills, and requires that the primary database be available.</span></span>

<span data-ttu-id="25ecd-117">명령은 다음 워크플로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-117">The command performs the following workflow:</span></span>

1. <span data-ttu-id="25ecd-118">복제를 보조 데이터베이스로 플러시될 모든 미해결 트랜잭션을 초래하고 모든 새 트랜잭션을 차단하는 동기 모드로 일시적으로 전환</span><span class="sxs-lookup"><span data-stu-id="25ecd-118">Temporarily switches replication to synchronous mode, causing all outstanding transactions to be flushed to the secondary and blocking all new transactions;</span></span>
2. <span data-ttu-id="25ecd-119">지역에서 복제 파트너 관계에서 두 데이터베이스의 역할을 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-119">Switches the roles of the two databases in the geo-replication partnership.</span></span>  

<span data-ttu-id="25ecd-120">이 순서는 두 데이터베이스가 역할이 전환되기 전에 동기화됨을 보장하므로 데이터 손실이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-120">This sequence guarantees that the two databases are synchronized before the roles switch and therefore no data loss will occur.</span></span> <span data-ttu-id="25ecd-121">역할이 전환되는 동안 두 데이터베이스를 모두 사용할 수 없는 (0-25초의 순서로) 짧은 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-121">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="25ecd-122">주 데이터베이스에 여러 개의 보조 데이터베이스가 있는 경우 이 명령을 사용하면 새로운 주 데이터베이스에 연결할 다른 보조 데이터베이스가 자동으로 다시 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-122">If the primary database has multiple secondary databases, the command will automatically reconfigure the other secondaries to connect to the new primary.</span></span>  <span data-ttu-id="25ecd-123">전체 작업은 정상적인 상황에서 완료하는데 1분 미만이 걸려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-123">The entire operation should take less than a minute to complete under normal circumstances.</span></span> <span data-ttu-id="25ecd-124">자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="25ecd-125">계획된 장애 조치를 시작하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-125">Use the following steps to initiate a planned failover.</span></span>

1. <span data-ttu-id="25ecd-126">Management Studio에서 지역에서 복제된 보조 데이터베이스가 상주하는 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-126">In Management Studio, connect to the Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="25ecd-127">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-127">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="25ecd-128">보조 데이터베이스를 주 역할로 전환하려면 다음 **ALTER DATABASE** 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-128">Use the following **ALTER DATABASE** statement to switch the secondary database to the primary role.</span></span>
   
        ALTER DATABASE <MyDB> FAILOVER;
4. <span data-ttu-id="25ecd-129">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-129">Click **Execute** to run the query.</span></span>

> [!NOTE]
> <span data-ttu-id="25ecd-130">드문 경우로 작업을 완료할 수 없으며 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-130">In rare cases, it is possible that the operation cannot complete and may appear stuck.</span></span> <span data-ttu-id="25ecd-131">이 경우 사용자는 강제 장애 조치 명령을 실행하고 데이터 손실을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-131">In this case, the user can execute the force failover command and accept data loss.</span></span>
> 
> 

## <a name="initiate-an-unplanned-failover-from-the-primary-database-to-the-secondary-database"></a><span data-ttu-id="25ecd-132">주 데이터베이스에서 보조 데이터베이스로 계획되지 않은 장애 조치 시작</span><span class="sxs-lookup"><span data-stu-id="25ecd-132">Initiate an unplanned failover from the primary database to the secondary database</span></span>
<span data-ttu-id="25ecd-133">**ALTER DATABASE** 문을 사용하여 주 데이터베이스를 더 이상 사용할 수 없는 경우에, 계획되지 않은 방식으로 보조 데이터베이스가 새로운 주 데이터베이스가 되도록 수준을 올리고, 기존의 주 데이터베이스가 보조 데이터베이스가 되도록 강제로 수준을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-133">You can use the **ALTER DATABASE** statement to promote a secondary database to become the new primary database in an unplanned fashion, forcing the demotion of the existing primary to become a secondary at a time when the primary database is no longer available.</span></span> <span data-ttu-id="25ecd-134">이 문은 승격되는 지역에서 복제된 보조 데이터베이스가 상주하는 Azure SQL 데이터베이스 논리 서버의 마스터 데이터베이스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-134">This statement is executed on the master database on the Azure SQL Database logical server in which the geo-replicated secondary database that is being promoted resides.</span></span>

<span data-ttu-id="25ecd-135">이 기능은 데이터베이스의 가용성 복원이 중요하고 일부 데이터 손실이 허용되는 경우 재해 복구를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-135">This functionality is designed for disaster recovery when restoring availability of the database is critical and some data loss is acceptable.</span></span> <span data-ttu-id="25ecd-136">강제 장애 조치가 호출되면 지정된 보조 데이터베이스는 즉시 주 데이터베이스가 되며 쓰기 트랜잭션 승인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-136">When forced failover is invoked, the specified secondary database immediately becomes the primary database and begins accepting write transactions.</span></span> <span data-ttu-id="25ecd-137">기존 주 데이터베이스가 이 새 주 데이터베이스와 다시 연결할 수 있는 즉시 기존 주 데이터베이스에서 증분 백업이 수행되고 이어서 이전 주 데이터베이스는 새 주 데이터베이스에 대한 보조 데이터베이스로 만들어지며 이는 단순히 새 주의 복제본 동기화입니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-137">As soon as the original primary database is able to reconnect with this new primary database, an incremental backup is taken on the original primary database and the old primary database is made into a secondary database for the new primary database; subsequently, it is merely a synchronizing replica of the new primary.</span></span>

<span data-ttu-id="25ecd-138">그러나 특정 시점 복원은 보조 데이터베이스에서 지원되지 않으므로 강제 장애 조치가 발생하기 전에 새 주 데이터베이스에 복제되지 않은 이전 주 데이터베이스에 커밋된 데이터를 복구하고자 할 경우 사용자는 손실된 데이터를 복구하도록 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-138">However, because Point In Time Restore is not supported on the secondary databases, if the user wishes to recover data committed to the old primary database that had not been replicated to the new primary database before the forced failover occurred, the user will need to engage support to recover this lost data.</span></span>

<span data-ttu-id="25ecd-139">주 데이터베이스에 여러 개의 보조 데이터베이스가 있는 경우 이 명령을 사용하면 새로운 주 데이터베이스에 연결할 다른 보조 데이터베이스가 자동으로 다시 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-139">If the primary database has multiple secondary databases, the command will automatically reconfigure the other secondaries to connect to the new primary.</span></span>

<span data-ttu-id="25ecd-140">계획되지 않은 장애 조치를 시작하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-140">Use the following steps to initiate an unplanned failover.</span></span>

1. <span data-ttu-id="25ecd-141">Management Studio에서 지역에서 복제된 보조 데이터베이스가 상주하는 Azure SQL 데이터베이스 논리 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-141">In Management Studio, connect to the Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="25ecd-142">데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-142">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="25ecd-143">보조 데이터베이스를 주 역할로 전환하려면 다음 **ALTER DATABASE** 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-143">Use the following **ALTER DATABASE** statement to switch the secondary database to the primary role.</span></span>
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. <span data-ttu-id="25ecd-144">**실행** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-144">Click **Execute** to run the query.</span></span>

> [!NOTE]
> <span data-ttu-id="25ecd-145">주 및 보조가 모두 온라인일 때 명령이 실행되는 경우 데이터 동기화 없이 이전 주는 즉시 새 보조가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-145">If the command is issued when both primary and secondary are online the old primary will become the new secondary immediately without data synchronization.</span></span> <span data-ttu-id="25ecd-146">주 데이터베이스가 명령이 실행될 때 트랜잭션을 커밋하면 일부 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-146">If the primary is committing transactions when the command is issued some data loss may occur.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="25ecd-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25ecd-147">Next steps</span></span>
* <span data-ttu-id="25ecd-148">장애 조치(failover) 후에는 새로운 주 데이터베이스에서 서버 및 데이터베이스의 인증 요구 사항이 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25ecd-148">After failover, ensure the authentication requirements for your server and database are configured on the new primary.</span></span> <span data-ttu-id="25ecd-149">자세한 내용은 [재해 복구 후의 SQL Database 보안](sql-database-geo-replication-security-config.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-149">For details, see [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="25ecd-150">사전 및 사후 복구 단계를 비롯한 활성 지역 복제를 사용하고 재해 복구 훈련을 수행하여 재해 후에 복구하는 방법을 알아보려면 [재해 복구](sql-database-disaster-recovery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-150">To learn recovering after a disaster using active geo-replication, including pre-recovery and post-recovery steps and performing a disaster recovery drill, see [Disaster Recovery](sql-database-disaster-recovery.md)</span></span>
* <span data-ttu-id="25ecd-151">활성 지역 복제에 대한 Sasha Nosov의 블로그 게시물은 [새로운 지역에서 복제 기능에 대한 주요 내용](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-151">For a Sasha Nosov blog post about active geo-replication, see [Spotlight on new geo-replication capabilities](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)</span></span>
* <span data-ttu-id="25ecd-152">활성 지역 복제를 사용하여 클라우드 응용 프로그램을 설계하는 방법에 대한 자세한 내용은 [지역에서 복제를 사용하여 무중단 업무 방식에 사용 가능하도록 클라우드 응용 프로그램 설계](sql-database-designing-cloud-solutions-for-disaster-recovery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-152">For information about designing cloud applications to use active geo-replication, see [Designing cloud applications for business continuity using geo-replication](sql-database-designing-cloud-solutions-for-disaster-recovery.md)</span></span>
* <span data-ttu-id="25ecd-153">탄력적 풀의 활성 지역 복제 사용에 대한 자세한 내용은 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-153">For information about using active geo-replication with elastic pools, see [Elastic Pool disaster recovery strategies](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).</span></span>
* <span data-ttu-id="25ecd-154">무중단 업무 방식에 대한 개략적 정보는 [무중단 업무 방식 개요](sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25ecd-154">For an overview of business continuity, see [Business Continuity Overview](sql-database-business-continuity.md)</span></span>

