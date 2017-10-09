---
title: "aaaMonitor Dmv를 사용 하 여 작업 | Microsoft Docs"
description: "자세한 내용은 방법 toomonitor Dmv를 사용 하 여 작업 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a>DMV를 사용하여 작업 모니터링
이 문서에서는 설명 방법을 toouse 동적 관리 뷰 (Dmv) toomonitor 작업 하 고 Azure SQL 데이터 웨어하우스에 쿼리 실행을 조사 합니다.

## <a name="permissions"></a>권한
tooquery hello Dmv이 문서에서는 VIEW DATABASE STATE 또는 CONTROL 권한이 있어야 합니다. 일반적으로 훨씬 제한적 이므로 VIEW DATABASE STATE를 부여 하는 것에 기본 설정 hello 권한입니다.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>연결 모니터링
모든 로그인 tooSQL 데이터 웨어하우스 너무 로깅됩니다[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions]합니다.  이 DMV hello가 포함 되어 마지막 10, 000 로그인 합니다.  hello session_id hello 기본 키 이며 각 새 로그온에 대해 순차적으로 할당 됩니다.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>쿼리 실행 모니터링
SQL 데이터 웨어하우스에서 실행 되는 모든 쿼리는 너무 로깅됩니다[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests]합니다.  이 DMV hello가 포함 되어 실행 되는 10, 000 쿼리 지속 합니다.  고유 하 게 hello request_id는 각 쿼리를 식별 하 고 hello이이 DMV에 대 한 기본 키가 있습니다.  hello request_id 각 쿼리에 대해 순차적으로 할당 되 고이 쿼리 id는 QID 접두사로  이 DMV에서 지정된 session_id를 쿼리하면 지정된 로그온에 대한 모든 쿼리가 표시됩니다.

> [!NOTE]
> 저장 프로시저는 여러 요청 ID를 사용합니다.  요청 ID는 순차적으로 할당됩니다. 
> 
> 

다음은 단계 toofollow tooinvestigate 쿼리 실행 계획 및 특정 쿼리에 대 한 시간입니다.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>1 단계: tooinvestigate 원하는 hello 쿼리를 식별 합니다.
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

쿼리 결과 앞에 오는 hello에서 **참고 hello 요청 ID** 싶다는 의사를 tooinvestigate hello 쿼리 합니다.

Hello에 대 한 쿼리 **Suspended** tooconcurrency 제한 인해 대기 중인 상태입니다. 이러한 쿼리 UserConcurrencyResourceType 유형의으로 hello sys.dm_pdw_waits 대기 쿼리에도 나타납니다. 동시성 제한에 대한 자세한 내용은 [동시성 및 워크로드 관리][Concurrency and workload management]를 참조하세요. 쿼리는 개체 잠금 등의 기타 이유로 인해 대기 상태일 수도 있습니다.  쿼리가 리소스를 대기 중인 경우 이 문서 뒷부분의 [리소스를 대기 중인 쿼리 조사][Investigating queries waiting for resources]를 참조하세요.

hello sys.dm_pdw_exec_requests 테이블을 사용 하 여 쿼리의 toosimplify hello 조회 [레이블] [ LABEL] tooassign 주석 tooyour 쿼리 hello sys.dm_pdw_exec_requests 보기에서 조회할 수 있습니다.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>2 단계: hello 쿼리 계획을 조사
Hello 요청 ID tooretrieve hello의 분산된 SQL (DSQL)에서 쿼리 계획을 사용 하 여 [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps]합니다.

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

DSQL 계획 예상 보다 오래 걸리면, 복잡 한 계획을 여러 DSQL 단계 나 한 단계로 너무 오래 걸리면 hello 원인이 될 수 있습니다.  여러 개의 이동 작업을 사용 하 여 많은 단계 hello 계획을 사용 하는 경우에 최적화 프로그램 테이블 분포 tooreduce 데이터를 이동 하는 것이 좋습니다. hello [배포 테이블] [ Table distribution] 문서에서는 데이터 쿼리 toosolve 이동된 해야 하 고 몇 가지 배포 전략 toominimize 데이터 이동에 설명 하는 이유 설명 합니다.

tooinvestigate 자세한 내용은 한 번에 대 한 hello *operation_type* hello 장기 실행 쿼리 단계 및 참고 hello 열 **단계 인덱스**:

* OnOperation, RemoteOperation, ReturnOperation 등의 **SQL 작업**에 대해 3a단계를 진행합니다.
* ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation 등의 **데이터 이동 작업**에 대해 3b단계를 진행합니다.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>3a 단계: hello 배포 데이터베이스에서 SQL 조사
Hello 요청 ID와 hello 단계 인덱스 tooretrieve 세부 정보를 사용 하 여 [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], 모든 hello hello 쿼리 단계의 실행 정보가 포함 된 데이터베이스를 배포 합니다.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Hello 쿼리 단계가 실행 되는 경우 [상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] hello hello 단계에서 특정 실행에 대 한 SQL Server 계획 캐시에서에서 사용 되는 tooretrieve hello SQL Server 예상된 계획 수 배포 합니다.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>3b 단계: 조사 hello 배포 데이터베이스에서 데이터 이동
Hello 요청 ID 및 단계 인덱스 tooretrieve 정보에서 각 배포에서 실행 되는 데이터 이동 단계에 대 한 hello를 사용 하 여 [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers]합니다.

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Hello 확인 *total_elapsed_time* 열 toosee 특정 분포 데이터 이동에 대 한 다른 항목 보다 시간이 많이 소요 되는 경우.
* Hello 장기 실행 배포용 hello 확인 *rows_processed* 열 toosee hello 해당 배포에서 이동 하는 행 수가 다른 항목 보다 훨씬 큰 경우. 이동되는 행 수가 훨씬 많으면 기본 데이터가 기울어진 것일 수 있습니다.

Hello 쿼리가 실행 중인 경우 [상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] hello 현재 특정 내에서 SQL 단계를 실행 하는 hello에 대 한 SQL Server 계획 캐시에서에서 사용 되는 tooretrieve hello SQL Server 예상된 계획 수 배포 합니다.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>대기 중인 쿼리 모니터링
쿼리에 진행 되지 않습니다는 리소스에 대 한 대기 하 고 있으므로 발견 한 경우에 대 한 쿼리를 기다리고 hello 리소스를 모두 표시 하는 쿼리 다음과 같습니다.

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

Hello 쿼리가 다른 쿼리에서 리소스에 적극적으로 대기 중인 경우 hello 상태가 됩니다 **AcquireResources**합니다.  Hello 쿼리에 모든 필수 hello 리소스 경우 hello 상태가 됩니다 **Granted**합니다.

## <a name="monitor-tempdb"></a>tempdb 모니터링
높은 tempdb 사용 hello 근본 원인을 메모리가 부족 한 문제 및 성능 저하 될 수 있습니다. 데이터 기울기 또는 낮은 품질로 rowgroup을 사용할 및 hello 적절 한 조치를 수행 하는 경우 먼저 확인 하십시오. tempdb가 쿼리 실행 중 한계에 도달한 것을 발견한 경우 데이터 웨어하우스를 확장하는 것이 좋습니다. hello 다음 설명 방법을 각 노드에 대 한 쿼리당 tooidentify tempdb 사용 합니다. 

Hello 다음 sys.dm_pdw_sql_requests 보기 tooassociate hello 적합 한 노드 id를 만듭니다. Tooleverage 있습니다 다른 통과 Dmv를 사용 되 고 sys.dm_pdw_sql_requests 해당 테이블에 조인 합니다.

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
다음 쿼리 toomonitor tempdb hello를 실행 합니다.

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a>메모리 모니터링

메모리 성능 저하 및 메모리가 부족 한 문제 hello 근본 원인이 될 수 있습니다. 데이터 기울기 또는 낮은 품질로 rowgroup을 사용할 및 hello 적절 한 조치를 수행 하는 경우 먼저 확인 하십시오. SQL Server 메모리 사용량이 쿼리 실행 중 한계에 도달한 것을 발견한 경우 데이터 웨어하우스를 확장하는 것이 좋습니다.

다음 쿼리에서 hello 노드당 SQL Server 메모리 사용량 및 메모리 부족을 반환 합니다. 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a>트랜잭션 로그 크기 모니터링
hello 다음 쿼리는 반환 hello 트랜잭션 로그 크기에 각 배포 합니다. 데이터 기울기 또는 낮은 품질로 rowgroup을 사용할 및 hello 적절 한 조치를 수행 하는 경우 확인 하십시오. 160GB에 도달 하는 hello 로그 파일 중 하나 하는 경우에 인스턴스를 확장 하거나 트랜잭션 크기를 제한 해야 합니다. 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a>트랜잭션 로그 롤백 모니터링
쿼리는 실패 하거나 시간이 오래 tooproceed 라인으로 전환를 확인 하 고 있는 모든 트랜잭션을 롤백하는 경우를 모니터링할 수 있습니다.
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a>다음 단계
DMV에 대한 자세한 내용은 [시스템 뷰][System views]를 참조하세요.
모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse best practices]를 참조하세요.

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
