---
title: "Azure SQL 데이터베이스를 사용 하 여 동적 관리 뷰 aaaMonitoring | Microsoft Docs"
description: "자세한 내용은 방법 toodetect 동적 관리 뷰 toomonitor Microsoft Azure SQL 데이터베이스를 사용 하 여 일반적인 성능 문제를 진단 하 고 있습니다."
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="51343-103">동적 관리 뷰를 사용하여 Azure SQL 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="51343-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="51343-104">Microsoft Azure SQL 데이터베이스 사용 동적 관리의 하위 집합 뷰에 toodiagnose 성능 문제 또는 장기 실행 쿼리, 리소스 병목 상태, 부실한 쿼리 계획 등에 의해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="51343-105">이 항목에서는 방법을 설명 toodetect 동적 관리 뷰를 사용 하 여 일반적인 성능 문제.</span><span class="sxs-lookup"><span data-stu-id="51343-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="51343-106">SQL 데이터베이스는 세 가지 범주의 동적 관리 뷰를 부분적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="51343-107">데이터베이스 관련 동적 관리 뷰.</span><span class="sxs-lookup"><span data-stu-id="51343-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="51343-108">실행 관련 동적 관리 뷰.</span><span class="sxs-lookup"><span data-stu-id="51343-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="51343-109">트랜잭션 관련 동적 관리 뷰</span><span class="sxs-lookup"><span data-stu-id="51343-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="51343-110">동적 관리 뷰에 대한 자세한 내용은 SQL Server 온라인 설명서의 [동적 관리 뷰 및 함수(Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51343-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="51343-111">권한</span><span class="sxs-lookup"><span data-stu-id="51343-111">Permissions</span></span>
<span data-ttu-id="51343-112">SQL 데이터베이스에서 동적 관리 뷰를 쿼리하려면 **VIEW DATABASE STATE** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="51343-113">hello **VIEW DATABASE STATE** 권한 hello 현재 데이터베이스 내의 모든 개체에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="51343-114">toogrant hello **VIEW DATABASE STATE** 권한 tooa 특정 데이터베이스 사용자, hello 다음 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="51343-115">온-프레미스 SQL 서버의 인스턴스에서 동적 관리 뷰는 서버 상태 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="51343-116">SQL 데이터베이스에서는 현재의 논리 데이터베이스에 관한 정보만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="51343-117">데이터베이스 크기 계산</span><span class="sxs-lookup"><span data-stu-id="51343-117">Calculating database size</span></span>
<span data-ttu-id="51343-118">hello 다음 쿼리를 반환 합니다 (메가바이트)에서 데이터베이스의 hello 크기.</span><span class="sxs-lookup"><span data-stu-id="51343-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="51343-119">hello 다음 쿼리 hello 크기 반환 메가바이트 단위로 개별 개체의 데이터베이스에서:</span><span class="sxs-lookup"><span data-stu-id="51343-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="51343-120">연결 모니터링</span><span class="sxs-lookup"><span data-stu-id="51343-120">Monitoring connections</span></span>
<span data-ttu-id="51343-121">Hello를 사용할 수 있습니다 [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) hello 설정 된 연결 tooa 특정 Azure SQL 데이터베이스 서버 및 각 연결의 hello 세부 정보에 대 한 tooretrieve 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="51343-122">또한 hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) 뷰는 모든 활성 사용자 연결과 내부 태스크에 대 한 정보를 검색할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="51343-123">hello 다음 쿼리는 검색 hello 현재 연결에 대 한 정보:</span><span class="sxs-lookup"><span data-stu-id="51343-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="51343-124">Hello를 실행할 때 **sys.dm_exec_requests** 및 **sys.dm_exec_sessions 뷰**하는 경우 **VIEW DATABASE STATE** 권한을 hello 데이터베이스에 실행 중인 모든 표시 hello 데이터베이스;에 대 한 세션 그렇지 않으면 표시만 hello 현재 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="51343-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="51343-125">쿼리 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="51343-125">Monitoring query performance</span></span>
<span data-ttu-id="51343-126">느린 속도로 또는 장시간 실행하는 쿼리는 많은 양의 시스템 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="51343-127">이 섹션에서는 방법을 toouse 동적 관리 뷰 toodetect 몇 가지 일반적인 쿼리 성능 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51343-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="51343-128">문제 해결을 위해는 오래 되었지만 여전히 도움이 참조는 hello [SQL Server 2008의 성능 문제 해결](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet에서 문서.</span><span class="sxs-lookup"><span data-stu-id="51343-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="51343-129">최상위 N개 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="51343-129">Finding top N queries</span></span>
<span data-ttu-id="51343-130">hello 다음 예제에서는 반환 hello 상위 5 개 쿼리에 평균 CPU 시간을 기준으로 하는 방법에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="51343-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="51343-131">이 예에서는 논리적으로 동일한 쿼리를 누적 리소스 소비량 그룹화 되도록 tootheir 쿼리 해시에 따라 hello 쿼리를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="51343-132">차단된 쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="51343-132">Monitoring blocked queries</span></span>
<span data-ttu-id="51343-133">저속 또는 장기 실행 쿼리 tooexcessive 리소스 소비에 기여 하 고 차단 된 쿼리에 따른 hello 결과 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="51343-134">hello 차단 hello 원인을 잘못 된 응용 프로그램 디자인, 잘못 된 쿼리 계획, 유용한 인덱스 부족 hello 및 등을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="51343-135">Azure SQL 데이터베이스의 hello sys.dm_tran_locks 보기 tooget hello 현재 잠금 작업에 대 한 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="51343-136">예제 코드는 SQL Server 온라인 설명서의 [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51343-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="51343-137">쿼리 계획 모니터링</span><span class="sxs-lookup"><span data-stu-id="51343-137">Monitoring query plans</span></span>
<span data-ttu-id="51343-138">또한 비효율적인 쿼리 계획 때문에 CPU 사용량이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51343-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="51343-139">hello 다음 예제에서는 hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) toodetermine hello 가장 많은 누적 CPU를 사용 하는 쿼리를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="51343-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="51343-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="51343-140">See also</span></span>
[<span data-ttu-id="51343-141">소개 tooSQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="51343-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

