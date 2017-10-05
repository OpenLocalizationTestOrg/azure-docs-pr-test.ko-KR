---
title: "동적 관리 뷰를 사용하여 Azure SQL Database 모니터링 | Microsoft Docs"
description: "동적 관리 뷰를 사용하여 Microsoft Azure SQL 데이터베이스를 모니터링하여 일반적인 성능 문제를 감지 및 진단하는 방법에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="baf43-103">동적 관리 뷰를 사용하여 Azure SQL 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="baf43-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="baf43-104">Microsoft Azure SQL 데이터베이스를 사용하여 차단되거나 오래 실행된 쿼리, 리소스 병목 현상, 잘못된 쿼리 계획 등에 의해 야기될 수 있는 동적 관리 뷰의 하위 집합에서 성능 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="baf43-105">이 항목에서는 동적 관리 뷰를 사용하여 일반적인 성능 문제를 감지하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="baf43-106">SQL 데이터베이스는 세 가지 범주의 동적 관리 뷰를 부분적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="baf43-107">데이터베이스 관련 동적 관리 뷰.</span><span class="sxs-lookup"><span data-stu-id="baf43-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="baf43-108">실행 관련 동적 관리 뷰.</span><span class="sxs-lookup"><span data-stu-id="baf43-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="baf43-109">트랜잭션 관련 동적 관리 뷰</span><span class="sxs-lookup"><span data-stu-id="baf43-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="baf43-110">동적 관리 뷰에 대한 자세한 내용은 SQL Server 온라인 설명서의 [동적 관리 뷰 및 함수(Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="baf43-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="baf43-111">권한</span><span class="sxs-lookup"><span data-stu-id="baf43-111">Permissions</span></span>
<span data-ttu-id="baf43-112">SQL 데이터베이스에서 동적 관리 뷰를 쿼리하려면 **VIEW DATABASE STATE** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="baf43-113">**VIEW DATABASE STATE** 권한은 현재 데이터베이스 내의 모든 개체에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="baf43-114">특정 데이터베이스 사용자에게 **VIEW DATABASE STATE** 권한을 부여하려면 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="baf43-115">온-프레미스 SQL 서버의 인스턴스에서 동적 관리 뷰는 서버 상태 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="baf43-116">SQL 데이터베이스에서는 현재의 논리 데이터베이스에 관한 정보만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="baf43-117">데이터베이스 크기 계산</span><span class="sxs-lookup"><span data-stu-id="baf43-117">Calculating database size</span></span>
<span data-ttu-id="baf43-118">다음 쿼리는 데이터베이스 크기(MB)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="baf43-119">다음 쿼리는 데이터베이스의 개별 개체 크기(MB)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="baf43-120">연결 모니터링</span><span class="sxs-lookup"><span data-stu-id="baf43-120">Monitoring connections</span></span>
<span data-ttu-id="baf43-121">[sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) 뷰를 사용하여 특정 Azure SQL Database 서버에 설정된 연결에 관한 정보 및 각 연결의 세부 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="baf43-122">또한 [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) 뷰는 모든 활성 사용자 연결 및 내부 작업에 대한 정보를 검색할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="baf43-123">다음 쿼리는 현재 연결에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="baf43-124">**sys.dm_exec_requests** 및 **sys.dm_exec_sessions views**를 실행하는 경우, 데이터베이스에 대한 **VIEW DATABASE STATE** 권한을 가지고 있으면 데이터베이스에 대한 모든 실행 세션이 표시되며, 그렇지 않으면 현재 세션만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="baf43-125">쿼리 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="baf43-125">Monitoring query performance</span></span>
<span data-ttu-id="baf43-126">느린 속도로 또는 장시간 실행하는 쿼리는 많은 양의 시스템 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="baf43-127">이 섹션에서는 동적 관리 뷰를 사용하여 몇 가지 일반적인 쿼리 성능 문제를 감지하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="baf43-128">오래 되었지만 여전히 유익한 문제 해결 참고 자료는 Microsoft Technet의 [SQL Server 2008의 성능 문제해결](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="baf43-129">최상위 N개 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="baf43-129">Finding top N queries</span></span>
<span data-ttu-id="baf43-130">다음 예제는 평균 CPU 시간별로 상위 5개의 쿼리에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="baf43-131">이 예제는 쿼리 해시에 따라 쿼리를 집계하므로 논리적으로 동일한 쿼리는 해당 누적 리소스 소비량에 따라 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="baf43-132">차단된 쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="baf43-132">Monitoring blocked queries</span></span>
<span data-ttu-id="baf43-133">느린 속도로 또는 장시간 실행하는 쿼리는 과도한 리소스 소비에 기여하고 차단된 쿼리에 따른 결과일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="baf43-134">차단의 원인으로 부실한 응용 프로그램 디자인, 잘못된 쿼리 계획, 유용한 인덱스 부족 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="baf43-135">sys.dm_tran_locks 뷰를 사용하여 Azure SQL 데이터베이스의 현재 잠금 작업에 관한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="baf43-136">예제 코드는 SQL Server 온라인 설명서의 [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="baf43-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="baf43-137">쿼리 계획 모니터링</span><span class="sxs-lookup"><span data-stu-id="baf43-137">Monitoring query plans</span></span>
<span data-ttu-id="baf43-138">또한 비효율적인 쿼리 계획 때문에 CPU 사용량이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="baf43-139">다음 예제에서는 [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) 뷰를 사용하여 가장 많은 누적 CPU를 사용하는 쿼리를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="baf43-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="baf43-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="baf43-140">See also</span></span>
[<span data-ttu-id="baf43-141">SQL 데이터베이스 소개</span><span class="sxs-lookup"><span data-stu-id="baf43-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

