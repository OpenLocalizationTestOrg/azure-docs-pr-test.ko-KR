---
title: "보존 정책 사용 하 여 임시 테이블에서 한 aaaManage 기록 데이터 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 임시 보존 정책 tookeep 기록 데이터 제어 합니다."
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
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="67b74-103">재방문 주기 정책 사용하여 Temporal Tables에서 과거 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="67b74-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="67b74-104">임시 테이블은 특히 과거 데이터를 장기간 보관할 경우 일반 테이블 보다 데이터베이스 크기를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="67b74-105">따라서, 기록 데이터에 대 한 보존 정책 계획 및 모든 임시 테이블의 hello 수명 주기 관리의 중요 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="67b74-106">Azure SQL Database의 임시 테이블은 이 작업을 수행하는 데 유용한 사용하기 쉬운 재방문 주기 메커니즘과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="67b74-107">임시 기록 보존 toocreate 유연한 에이징 정책은 사용자가 hello 개별 테이블 수준에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="67b74-108">임시 보존이 적용 하는 것은 간단: 하나의 매개 변수 toobe 테이블 스키마를 만들거나 변경 하는 동안 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="67b74-109">재방문 주기 정책을 정의하고 나면 Azure SQL Database는 자동 데이터 정리에 적합한 과거 행이 있는지 정기적으로 확인하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="67b74-110">일치 하는 행 식별 하 고 hello 기록 테이블에서 해당 제거 예약 되 고 hello 시스템에서 실행 하는 hello 백그라운드 작업에서 투명 하 게 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="67b74-111">Hello 기록 테이블의 행에 대 한 나이 조건은 SYSTEM_TIME 기간 종료를 나타내는 hello 열에 따라 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="67b74-112">보존 기간 등 설정 된 경우 toosix 정리에 대 한 적격 테이블 행 hello 다음 조건을 충족 하는 월:</span><span class="sxs-lookup"><span data-stu-id="67b74-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="67b74-113">앞 예제는 hello, 것으로 가정 하는 **ValidTo** toohello SYSTEM_TIME 기간 종료 열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="67b74-114">어떻게 tooconfigure 보존 정책을?</span><span class="sxs-lookup"><span data-stu-id="67b74-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="67b74-115">임시 테이블에 대 한 보존 정책을 구성 하기 전에 먼저 임시 기록 보존 설정 되어 있는지 확인 *hello 데이터베이스 수준에서*합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="67b74-116">플래그 데이터베이스 **is_temporal_history_retention_enabled** 기본적으로 집합 tooON 이지만 사용자가 ALTER DATABASE 문을 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="67b74-117">자동으로 후 tooOFF 집합은 또한 [지정 시간 복원](sql-database-recovery-using-backups.md) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="67b74-118">프로그램 데이터베이스에 대 한 임시 기록 보존 정리 tooenable hello 문 다음 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="67b74-119">**is_temporal_history_retention_enabled**이 OFF가 되더라도 임시 테이블에 대한 재방문 주기는 구성할 수 있지만 그 경우 오래된 행에 대한 자동 정리는 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="67b74-120">보존 정책은 hello HISTORY_RETENTION_PERIOD 매개 변수 값을 지정 하 여 테이블을 만들 때 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="67b74-121">Azure SQL 데이터베이스를 통해 toospecify 보존 기간이 다른 시간 단위를 사용 하 여: 일, 주, 월 및 연도입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="67b74-122">HISTORY_RETENTION_PERIOD가 생략되면 재방문 주기를 INFINITE로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="67b74-123">또한 INFINITE 키워드를 명시적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="67b74-124">일부 시나리오에서는 테이블을 만든 후 tooconfigure 보존을 할 수 있습니다 또는 toochange 이전에 구성 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="67b74-125">이 경우 ALTER TABLE 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="67b74-126">SYSTEM_VERSIONING tooOFF 설정 *유지 하지 않습니다* 보존 기간 값입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="67b74-127">HISTORY_RETENTION_PERIOD 없이 SYSTEM_VERSIONING tooON 설정에 지정 된 명시적으로 결과 hello 무한 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="67b74-128">tooreview hello 보존 정책의 현재 상태를 사용 하 여 hello 다음 쿼리 개별 테이블에 대 한 보존 기간이 hello 데이터베이스 수준에서 해당 조인 임시 보존 사용 플래그:</span><span class="sxs-lookup"><span data-stu-id="67b74-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="67b74-129">SQL Database가 오래된 행을 삭제하는 방법은?</span><span class="sxs-lookup"><span data-stu-id="67b74-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="67b74-130">hello 정리 프로세스는 hello 기록 테이블의 hello 인덱스 레이아웃에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="67b74-131">것이 중요 한 toonotice 하 *유한 보존 정책을 구성한를 포함할 수 있습니다 (B-트리 또는 columnstore) 클러스터형된 인덱스를 가진 기록 테이블*합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="67b74-132">백그라운드 작업을 한정 된 보존 기간으로 모든 임시 테이블에 대 한 오래 된 데이터 정리 tooperform 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="67b74-133">Hello 클러스터형된 rowstore (btree) 인덱스에 대 한 정리 논리 데이터베이스 로그와 I/O 하위 시스템에 대 한 압력을 최소화 합니다. 더 작은 청크 (위쪽 too10K)의 오래 된 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="67b74-134">정리 논리를 활용 하지만 B-트리 인덱스, 보존 기간을 모뎀과 보장할 수 없는 보다 오래 된 hello 행에 대 한 삭제의 순서를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="67b74-135">따라서 *응용 프로그램에서 정리 순서 hello에 모든 종속성을 사용 하지 않는*합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="67b74-136">hello hello clustered columnstore에 대 한 정리 작업을 제거 전체 [행 그룹](https://msdn.microsoft.com/library/gg492088.aspx) 한 번에 (일반적으로 포함 되어 각 행의 1 백만), 높은 속도로 기록 데이터가 생성 되는 경우에 특히 매우 효율적인를 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![클러스터형 columnstore 재방문 주기](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="67b74-138">클러스터형 columnstore 인덱스는 뛰어난 데이터 압축 및 효율적인 재방문 주기 정리를 자랑하기 때문에 워크로드가 빠른 시간 내에 대량의 과거 데이터를 생성하는 시나리오인 경우 완벽한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="67b74-139">해당 패턴은 변경 내용 추적 및 감사, 추세 분석 또는 IoT 데이터 수집에 대해 [임시 테이블을 사용하는 집약적 트랜잭션 처리 워크로드](https://msdn.microsoft.com/library/mt631669.aspx)에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="67b74-140">인덱스 고려 사항</span><span class="sxs-lookup"><span data-stu-id="67b74-140">Index considerations</span></span>
<span data-ttu-id="67b74-141">rowstore 클러스터형된 인덱스가 있는 테이블에 대 한 hello 정리 태스크는 인덱스 toostart hello 열 해당 hello 종료가 SYSTEM_TIME 기간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="67b74-142">이러한 인덱스가 없는 경우 한정된 재방문 주기 기간을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="67b74-143">*Msg 13765, 수준 16, 상태 1 <br> </br> temporalstagetestdb.dbo.WebsiteUserInfo' 시스템 버전 임시 테이블'에서 실패 유한 보존 기간 설정 hello 기록 테이블 ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' 필요한 클러스터형된 인덱스가 포함 되지 않습니다. 클러스터형된 columnstore 또는 SYSTEM_TIME 끝과 일치 하는 hello 열으로 시작 하는 B-트리 인덱스를 만드는 것이 좋습니다 hello 기록 테이블에서 기간입니다.*</span><span class="sxs-lookup"><span data-stu-id="67b74-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="67b74-144">이미 Azure SQL 데이터베이스에서 만든 기본 기록 테이블 hello toonotice에 보존 정책에 대 한 호환 되는 인덱스는 클러스터형 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="67b74-145">한정 된 보존 기간 설정 된 테이블에서 해당 인덱스 tooremove를 시도 하면 다음 오류가 hello로 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="67b74-146">*Msg 13766, 수준 16, 상태 1 <br> </br> 오래 된 데이터의 자동 정리에 사용 되는 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' hello 클러스터형된 인덱스를 삭제할 수 없습니다. 이 인덱스 toodrop 필요한 경우 hello 해당 시스템 버전 임시 테이블에서 설정 HISTORY_RETENTION_PERIOD tooINFINITE를 것이 좋습니다.*</span><span class="sxs-lookup"><span data-stu-id="67b74-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="67b74-147">오름차순 (hello end 기간 열에 순서 대로)는 항상 hello hello SYSTEM_ 독점적으로 hello 기록 테이블을 채울 때 hello에 기록 행이 삽입 hello 클러스터형된 columnstore 인덱스에는 정리 최적으로 작동 VERSIONIOING 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="67b74-148">기간 열 (수도 있음 hello 경우 기존 기록 데이터를 마이그레이션하는 경우)의 끝으로 hello 기록 테이블의 행은 정렬 되지 다시 만들어야 tooachieve 최적 정렬 제대로 되 B-트리 rowstore 인덱스를 기반으로 클러스터형된 columnstore 인덱스 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="67b74-149">정렬 자연스럽 게 hello 시스템 버전 관리 작업에 의해 적용 된 hello 행 그룹에 변경 될 수 있으므로 hello 유한 보존 기간으로 hello 기록 테이블에서 클러스터형된 columnstore 인덱스를 다시 작성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="67b74-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="67b74-150">Hello 기록 테이블에서 클러스터형된 columnstore 인덱스 toorebuild 필요한 않은 경우 일반 데이터 정리에 필요한 hello 행 그룹의 순서를 유지 하면서 규격 B-트리 인덱스를 기반으로 다시 생성 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="67b74-151">hello 보장된 데이터 순서 없이 열 인덱스 클러스터링 기존 기록 테이블을 임시 테이블을 만들면 같은 방법을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="67b74-152">한정 된 보존 기간을 hello 클러스터형된 columnstore 인덱스가 있는 hello 기록 테이블에 대해 구성 된 경우 해당 테이블에 추가 비클러스터형 btree 인덱스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="67b74-153">다음 오류가 hello로 문 위의 시도 tooexecute는 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="67b74-154">*Msg 13772, Level 16, State 1 <br></br> 임시 기록 테이블인 'WebsiteUserInfoHistory'에는 한정된 재방문 주기 기간 및 클러스터형 columnstore 인덱스가 정의되어 있기 때문에 비클러스터형 인덱스를 생성할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="67b74-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="67b74-155">재방문 주기 정책을 사용한 테이블 쿼리</span><span class="sxs-lookup"><span data-stu-id="67b74-155">Querying tables with retention policy</span></span>
<span data-ttu-id="67b74-156">Hello 임시 테이블에서 모든 쿼리가 자동으로 hello 정리 작업에서 오래 된 행을 삭제할 수 하기 때문에 무한 보존 정책, tooavoid 예측할 수 없는 결과 일치 하지 않는 결과 비교 하는 기록 행을 필터링 *시간 및 특정 시점 임의의 순서가*합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="67b74-157">hello 다음 다음과 같은 순서로 hello 쿼리 계획에 대 한 단순 쿼리</span><span class="sxs-lookup"><span data-stu-id="67b74-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="67b74-158">tooend 기간 열 (ValidTo)의 hello (강조 표시) hello 기록 테이블에서 데이터 Clustered Index Scan 연산자에 적용 하는 hello 쿼리 계획에 추가 필터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="67b74-159">이 예는 한 달 재방문 주기 기간이 WebsiteUserInfo 테이블에 설정되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![재방문 주기 쿼리 필터](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="67b74-161">그러나 기록 테이블을 직접 쿼리한다면 지정된 재방문 주기 기간보다 오래된 행을 볼 수도 있을테지만 쿼리 결과가 반복되리라는 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="67b74-162">hello 다음 다음과 같은 순서로 hello 쿼리에 대 한 쿼리 실행 계획 hello 기록 테이블에 추가 필터를 적용 하지 않고</span><span class="sxs-lookup"><span data-stu-id="67b74-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![재방문 주기 필터를 사용하지 않은 기록 쿼리](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="67b74-164">일관되지 않거나 예측할 수 없는 결과가 나올 수도 있기 때문에 재방문 주기 기간을 초과하여 기록 테이블을 읽는 비즈니스 논리에 의존하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="67b74-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="67b74-165">임시 테이블에 있는 데이터를 분석하려면 FOR SYSTEM_TIME 절을 사용한 임시 쿼리를 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="67b74-166">특정 시점 복원 고려 사항</span><span class="sxs-lookup"><span data-stu-id="67b74-166">Point in time restore considerations</span></span>
<span data-ttu-id="67b74-167">하 여 새 데이터베이스를 만들 때 [기존 데이터베이스 tooa 특정 지정 시간으로 복원](sql-database-recovery-using-backups.md), 있기 임시 보존 hello 데이터베이스 수준에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="67b74-168">(**is_temporal_history_retention_enabled** 플래그가 설정 tooOFF).</span><span class="sxs-lookup"><span data-stu-id="67b74-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="67b74-169">이 기능을 통해 tooexamine tooquery 도달 하기 전에 행 오래 된 하는 관계 없이 복원 시 모든 기록 행은 제거 하면 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="67b74-170">도 사용할 수 있습니다*구성 된 보존 기간 이후에도 기록 데이터를 검사*합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="67b74-171">임시 테이블의 재방문 주기가 1 MONTH로 지정되었다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="67b74-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="67b74-172">Premium 서비스 계층에서 데이터베이스를 만든 경우에 hello 과거 인하면에서 too35 일을 hello 데이터베이스 상태와 데이터베이스 복사본 수 toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="67b74-173">효과적으로 수 있게 해 주는 사용자 들 두 일이 넘으면 hello 기록 테이블을 직접 쿼리하여 tooanalyze 기록 행.</span><span class="sxs-lookup"><span data-stu-id="67b74-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="67b74-174">Tooactivate 임시 보존 정리 하려는 경우 hello Transact SQL 문 지정 시간 복원은 후 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="67b74-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67b74-175">Next steps</span></span>
<span data-ttu-id="67b74-176">응용 프로그램에서 임시 테이블 toouse 체크 아웃 방법을 toolearn [Azure SQL 데이터베이스에서 임시 테이블 시작](sql-database-temporal-tables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="67b74-177">방문 Channel 9 toohear는 [실제 고객 구현 임시 성공 스토리](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) 및 조사식은 [임시 데모 라이브](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)합니다.</span><span class="sxs-lookup"><span data-stu-id="67b74-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="67b74-178">Temporal Tables에 관한 자세한 내용은 [MSDN 설명서](https://msdn.microsoft.com/library/dn935015.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67b74-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

