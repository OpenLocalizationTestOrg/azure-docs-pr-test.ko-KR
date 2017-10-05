---
title: "재방문 주기 정책 사용하여 Temporal Tables에서 과거 데이터 관리 | Microsoft Docs"
description: "임시 재방문 주기 정책을 사용하여 과거 데이터를 제어하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 8975d7a7d39114b2758d64a4df9f992cba6bf561
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="c966f-103">재방문 주기 정책 사용하여 Temporal Tables에서 과거 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="c966f-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="c966f-104">임시 테이블은 특히 과거 데이터를 장기간 보관할 경우 일반 테이블 보다 데이터베이스 크기를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="c966f-105">따라서 과거 데이터에 대한 재방문 주기 정책은 모든 임시 테이블의 수명 주기를 계획하고 관리하는 데 있어서 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="c966f-106">Azure SQL Database의 임시 테이블은 이 작업을 수행하는 데 유용한 사용하기 쉬운 재방문 주기 메커니즘과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="c966f-107">임시 과거 재방문 주기는 사용자가 유연한 에이징 정책을 만들 수 있도록 개별 테이블 수준에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="c966f-108">임시 재방문 주기를 적용하는 것은 간단합니다. 테이블 만들기 또는 스키마 변경 동안 하나의 매개 변수만 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="c966f-109">재방문 주기 정책을 정의하고 나면 Azure SQL Database는 자동 데이터 정리에 적합한 과거 행이 있는지 정기적으로 확인하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="c966f-110">일치하는 행 식별 및 기록 테이블에서 제거는 시스템에서 예약하고 실행하는 백그라운드 작업에서 투명하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="c966f-111">기록 테이블 행에 대한 Age 조건은 SYSTEM_TIME 기간의 종료를 나타내는 열을 기준으로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="c966f-112">예를 들어 재방문 주기 기간이 6개월로 설정된 경우 정리에 적합한 테이블 행은 다음 조건을 만족합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="c966f-113">앞의 예에서는 **ValidTo** 행이 SYSTEM_TIME 기간의 끝에 해당한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="c966f-114">재방문 주기 정책을 구성하는 방법?</span><span class="sxs-lookup"><span data-stu-id="c966f-114">How to configure retention policy?</span></span>
<span data-ttu-id="c966f-115">임시 테이블에 대한 재방문 주기 정책을 구성하기 전에 먼저 임시 기록 재방문 주기를 *데이터베이스 수준에서* 사용하도록 설정할지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="c966f-116">데이터베이스 플래그 **is_temporal_history_retention_enabled**는 기본적으로 ON에 설정되어 있지만 사용자가 ALTER DATABASE 문을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="c966f-117">또한 이 플래그는 [특정 시점 복원](sql-database-recovery-using-backups.md) 작업 후에 자동적으로 OFF로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="c966f-118">데이터베이스에 대한 임시 기록 재방문 주기를 사용하도록 설정하려면 다음 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="c966f-119">**is_temporal_history_retention_enabled**이 OFF가 되더라도 임시 테이블에 대한 재방문 주기는 구성할 수 있지만 그 경우 오래된 행에 대한 자동 정리는 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="c966f-120">재방문 주기 정책은 HISTORY_RETENTION_PERIOD 매개 변수에 대한 값을 지정하여 테이블을 만들 때 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="c966f-121">Azure SQL Database를 통해 다른 시간 단위인 DAYS, WEEKS, MONTHS, YEARS를 사용하여 재방문 주기 기간을 지정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="c966f-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="c966f-122">HISTORY_RETENTION_PERIOD가 생략되면 재방문 주기를 INFINITE로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="c966f-123">또한 INFINITE 키워드를 명시적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="c966f-124">일부 시나리오에서는 테이블을 만든 후 재방문 주기를 구성하거나 앞서 구성된 값을 변경해도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="c966f-125">이 경우 ALTER TABLE 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="c966f-126">SYSTEM_VERSIONING을 OFF로 설정하면 재방문 주기 기간 값을 *유지하지 않습니다*.</span><span class="sxs-lookup"><span data-stu-id="c966f-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="c966f-127">HISTORY_RETENTION_PERIOD를 명시적으로 지정하지 않고 SYSTEM_VERSIONING을 ON으로 설정하면 재방문 주기 기간이 INFINITE가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="c966f-128">재방문 주기 정책의 현재 상태를 살펴보려면 임시 재방문 주기 사용 플래그를 데이터베이스 수준에서 개별 테이블에 대한 재방문 주기 기간과 조인하는 다음 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="c966f-129">SQL Database가 오래된 행을 삭제하는 방법은?</span><span class="sxs-lookup"><span data-stu-id="c966f-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="c966f-130">정리 프로세스는 기록 테이블의 인덱스 레이아웃에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="c966f-131">*클러스터형 인덱스(B-트리 또는 columnstore)가 있는 기록 테이블만이 유한한 재방문 주기 정책을 구성할 수 있다*는 점에 유의해야 합니다</span><span class="sxs-lookup"><span data-stu-id="c966f-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="c966f-132">한정된 재방문 주기 기간을 가진 모든 임시 테이블에 대해 오래된 데이터 정리를 수행하는 백그라운드 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="c966f-133">rowstore(B-트리) 클러스터형 인덱스에 대한 정리 논리를 사용해 오래된 행을 더 작은 청크(최대 10K)로 삭제하여 데이터베이스 로그 및 I/O 하위 시스템에 대한 압력을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="c966f-134">정리 논리는 필수인 B-트리 인덱스를 활용하지만, 재방문 주기 기간보다 오래된 행의 삭제 순서는 확고히 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="c966f-135">따라서 *응용 프로그램의 정리 순서에 의존하지 않도록 합니다*.</span><span class="sxs-lookup"><span data-stu-id="c966f-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="c966f-136">클러스터형 columnstore에 대한 정리 작업은 전체 [행 그룹](https://msdn.microsoft.com/library/gg492088.aspx)(일반적으로 한 그룹에 백만 행 포함)을 한 번에 제거하여 매우 효율적이며 특히 과거 데이터가 고속으로 생성된 경우에 더욱 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![클러스터형 columnstore 재방문 주기](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="c966f-138">클러스터형 columnstore 인덱스는 뛰어난 데이터 압축 및 효율적인 재방문 주기 정리를 자랑하기 때문에 워크로드가 빠른 시간 내에 대량의 과거 데이터를 생성하는 시나리오인 경우 완벽한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="c966f-139">해당 패턴은 변경 내용 추적 및 감사, 추세 분석 또는 IoT 데이터 수집에 대해 [임시 테이블을 사용하는 집약적 트랜잭션 처리 워크로드](https://msdn.microsoft.com/library/mt631669.aspx)에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="c966f-140">인덱스 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c966f-140">Index considerations</span></span>
<span data-ttu-id="c966f-141">Rowstore 클러스터형 인덱스가 있는 테이블에 대한 정리 작업은 SYSTEM_TIME 기간의 끝에 해당하는 열로 시작하는 인덱스를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="c966f-142">이러한 인덱스가 없는 경우 한정된 재방문 주기 기간을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="c966f-143">*Msg 13765, Level 16, State 1 <br></br> 한정된 재방문 주기 기간 설정은 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' 기록 테이블에 필수 클러스터형 인덱스가 없기 때문에 'temporalstagetestdb.dbo.WebsiteUserInfo’ 시스템 버전 임시 테이블에서 실패했습니다. 기록 테이블에 SYSTEM_TIME의 끝 부분과 일치하는 열로 시작하는 클러스터형 columnstore 또는 B-트리 인덱스를 만드는 것이 좋습니다.*</span><span class="sxs-lookup"><span data-stu-id="c966f-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="c966f-144">Azure SQL Database에서 만든 기본 기록 테이블에 재방문 주기 정책과 호환되는 클러스터형 인덱스가 이미 있는지 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="c966f-145">재방문 주기 기간이 한정된 테이블에서 해당 인덱스를 제거하려 하면 다음 오류와 함께 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="c966f-146">*Msg 13766, Level 16, State 1 <br></br> 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' 클러스터형 인덱스가 오래된 데이터의 자동 정리를 위해 사용되고 있으므로 삭제할 수 없습니다. 이 인덱스를 삭제해야 할 경우 해당 시스템 버전 임시 테이블에서 HISTORY_RETENTION_PERIOD를 INFINITE로 설정하는 것이 좋습니다.*</span><span class="sxs-lookup"><span data-stu-id="c966f-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="c966f-147">클러스터형 columnstore 인덱스 상의 정리는 기록 행이 오름차순(기간 열 끝의 순서로 정렬됨)으로 삽입된 경우 최적으로 작동합니다. 특히 기록 테이블이 SYSTEM_VERSIONIOING 메커니즘에 의해 단독으로 채워질 때 항상 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="c966f-148">기록 테이블의 행이 기간 열(기존 과거 데이터를 마이그레이션한 경우에 해당될 수 있음)의 끝을 기준으로 정렬되지 경우, 최적의 성능을 얻으려면 제대로 정렬된 B-트리 rowstore 인덱스 위에 클러스터형 columnstore 인덱스를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="c966f-149">시스템 버전 관리 작업에 의해 기본적으로 적용되는 행 그룹의 순서가 변경될 수 있으므로 한정된 재방문 주기를 사용하여 기록 테이블에 클러스터형 columnstore 인덱스를 다시 작성하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c966f-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="c966f-150">기록 테이블의 클러스터형 columnstore 인덱스를 다시 작성해야 할 경우 호환성 B-트리 인덱스의 상단에 재생성하여 정기적인 데이터 정리를 위해 필요한 행 그룹의 순서를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="c966f-151">데이터 순서가 보장되지 않은 클러스터형 열 인덱스를 가진 기존 기록 테이블로 임시 테이블을 만들면 동일한 방법을 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="c966f-152">클러스터형 columnstore 인덱스가 있는 기록 테이블에 대해 재방문 주기 기간을 한정되게 구성한다면 해당 테이블에 추가로 비클러스터형 B-트리 인덱스를 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="c966f-153">위의 문을 실행하면 다음 오류와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="c966f-154">*Msg 13772, Level 16, State 1 <br></br> 임시 기록 테이블인 'WebsiteUserInfoHistory'에는 한정된 재방문 주기 기간 및 클러스터형 columnstore 인덱스가 정의되어 있기 때문에 비클러스터형 인덱스를 생성할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="c966f-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="c966f-155">재방문 주기 정책을 사용한 테이블 쿼리</span><span class="sxs-lookup"><span data-stu-id="c966f-155">Querying tables with retention policy</span></span>
<span data-ttu-id="c966f-156">임시 테이블에 대한 모든 쿼리는 오래된 행이 정리 작업에 의해 자동으로 *언제든지 임의의 순서로* 삭제될 수 있기 때문에 예측할 수 없고 일관되지 않은 결과를 방지하기 위해 유한한 재방문 주기 정책과 일치하는 기록 행을 자동으로 걸러냅니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="c966f-157">다음 그림은 간단한 쿼리에 대한 쿼리 계획을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="c966f-158">쿼리 계획에는 기록 테이블(강조 표시)에 있는 Clustered Index Scan 연산자의 기간 열 (ValidTo) 끝에 적용 되는 추가 필터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="c966f-159">이 예는 한 달 재방문 주기 기간이 WebsiteUserInfo 테이블에 설정되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![재방문 주기 쿼리 필터](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="c966f-161">그러나 기록 테이블을 직접 쿼리한다면 지정된 재방문 주기 기간보다 오래된 행을 볼 수도 있을테지만 쿼리 결과가 반복되리라는 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="c966f-162">다음 그림은 추가 필터를 적용하지 않고 기록 테이블에 대한 쿼리 계획 실행을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![재방문 주기 필터를 사용하지 않은 기록 쿼리](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="c966f-164">일관되지 않거나 예측할 수 없는 결과가 나올 수도 있기 때문에 재방문 주기 기간을 초과하여 기록 테이블을 읽는 비즈니스 논리에 의존하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c966f-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="c966f-165">임시 테이블에 있는 데이터를 분석하려면 FOR SYSTEM_TIME 절을 사용한 임시 쿼리를 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="c966f-166">특정 시점 복원 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c966f-166">Point in time restore considerations</span></span>
<span data-ttu-id="c966f-167">[기존 데이터베이스를 특정 시점으로 복원](sql-database-recovery-using-backups.md)하여 새 데이터베이스를 만들 때 데이터베이스 수준에서 비활성화된 임시 재방문 주기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="c966f-168">(**is_temporal_history_retention_enabled** 플래그 OFF로 설정).</span><span class="sxs-lookup"><span data-stu-id="c966f-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="c966f-169">이 기능을 사용하면 쿼리하기도 전에 오래된 행이 삭제되는 것에 대한 걱정 없이 복원 시 모든 기록 행을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="c966f-170">*구성된 재방문 주기를 초과하여 과거 데이터를 검사*하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="c966f-171">임시 테이블의 재방문 주기가 1 MONTH로 지정되었다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="c966f-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="c966f-172">데이터베이스가 프리미엄 서비스 계층에서 만들어진 경우 데이타베이스 상태를 35일 이전으로 돌려 데이터베이스 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="c966f-173">이를 통해 실질적으로 기록 테이블을 직접 쿼리하여 최대 65일 전까지의 기록 행을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="c966f-174">임시 재방문 주기 정리를 활성화하고자 한다면 특정 시점 복원을 한 후 다음 TRANSACT-SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="c966f-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c966f-175">Next steps</span></span>
<span data-ttu-id="c966f-176">응용 프로그램에서 Temporal Tables을 사용하는 방법을 알아보려면 [Azure SQL Database의 임시 테이블 시작](sql-database-temporal-tables.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c966f-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="c966f-177">Channel 9을 방문하여 [실제 고객 임시 구현 성공 사례](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions)를 듣고 [라이브 임시 데모](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)를 시청합니다.</span><span class="sxs-lookup"><span data-stu-id="c966f-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="c966f-178">Temporal Tables에 관한 자세한 내용은 [MSDN 설명서](https://msdn.microsoft.com/library/dn935015.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c966f-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

