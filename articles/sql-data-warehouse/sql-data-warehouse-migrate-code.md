---
title: "aaaMigrate SQL 코드 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "솔루션 개발을 위한 SQL 코드 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="1e56f-103">SQL 코드 tooSQL 데이터 웨어하우스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1e56f-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="1e56f-104">이 문서에서는 시켜야 합니다 toomake 다른 데이터베이스 tooSQL 데이터 웨어하우스에서에서 코드를 마이그레이션할 때 코드 변경 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="1e56f-105">일부 SQL 데이터 웨어하우스 기능 분산 방식에서 디자인 된 toowork 멤버인 성능은 크게 개선 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="1e56f-106">그러나 toomaintain 성능 및 확장성 일부 기능은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="1e56f-107">일반적인 T-SQL 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1e56f-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="1e56f-108">다음 목록 hello SQL 데이터 웨어하우스를 지원 하지 않는 hello 가장 일반적인 기능을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="1e56f-109">hello 링크를 이동 하면 hello 지원 되지 않는 기능에 대 한 tooworkarounds 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="1e56f-110">[업데이트 시 ANSI 조인][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="1e56f-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="1e56f-111">[삭제 시 ANSI 조인][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="1e56f-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="1e56f-112">[병합 문][merge statement]</span><span class="sxs-lookup"><span data-stu-id="1e56f-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="1e56f-113">데이터베이스 간 조인</span><span class="sxs-lookup"><span data-stu-id="1e56f-113">cross-database joins</span></span>
* <span data-ttu-id="1e56f-114">[커서][cursors]</span><span class="sxs-lookup"><span data-stu-id="1e56f-114">[cursors][cursors]</span></span>
* <span data-ttu-id="1e56f-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="1e56f-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="1e56f-116">output 절</span><span class="sxs-lookup"><span data-stu-id="1e56f-116">output clause</span></span>
* <span data-ttu-id="1e56f-117">인라인 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="1e56f-117">inline user-defined functions</span></span>
* <span data-ttu-id="1e56f-118">다중 문 함수</span><span class="sxs-lookup"><span data-stu-id="1e56f-118">multi-statement functions</span></span>
* [<span data-ttu-id="1e56f-119">공통 테이블 식</span><span class="sxs-lookup"><span data-stu-id="1e56f-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="1e56f-120">[재귀 공통 테이블 식(CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="1e56f-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="1e56f-121">CLR 함수 및 프로시저</span><span class="sxs-lookup"><span data-stu-id="1e56f-121">CLR functions and procedures</span></span>
* <span data-ttu-id="1e56f-122">$partition 함수</span><span class="sxs-lookup"><span data-stu-id="1e56f-122">$partition function</span></span>
* <span data-ttu-id="1e56f-123">테이블 변수</span><span class="sxs-lookup"><span data-stu-id="1e56f-123">table variables</span></span>
* <span data-ttu-id="1e56f-124">테이블 값 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1e56f-124">table value parameters</span></span>
* <span data-ttu-id="1e56f-125">분산된 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="1e56f-125">distributed transactions</span></span>
* <span data-ttu-id="1e56f-126">커밋 / 롤백 작업</span><span class="sxs-lookup"><span data-stu-id="1e56f-126">commit / rollback work</span></span>
* <span data-ttu-id="1e56f-127">트랜잭션 저장</span><span class="sxs-lookup"><span data-stu-id="1e56f-127">save transaction</span></span>
* <span data-ttu-id="1e56f-128">실행 컨텍스트 (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="1e56f-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="1e56f-129">[롤업/큐브/그룹화 집합 옵션을 사용하는 GROUP BY 절][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="1e56f-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="1e56f-130">[8을 초과한 중첩 수준][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="1e56f-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="1e56f-131">[뷰를 통한 업데이트][updating through views]</span><span class="sxs-lookup"><span data-stu-id="1e56f-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="1e56f-132">[변수 할당에 대한 select 사용][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="1e56f-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="1e56f-133">[동적 SQL 문자열에 대한 MAX 데이터 형식 없음][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="1e56f-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="1e56f-134">다행히 대부분의 이러한 제한을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="1e56f-135">앞서 설명 된 hello 관련 개발 문서에 설명이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="1e56f-136">지원되는 CTE 기능</span><span class="sxs-lookup"><span data-stu-id="1e56f-136">Supported CTE features</span></span>
<span data-ttu-id="1e56f-137">CTE(공용 테이블 식)는 SQL 데이터 웨어하우스에서 부분적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="1e56f-138">같은 CTE 기능 hello는 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="1e56f-139">SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="1e56f-140">CREATE VIEW 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="1e56f-141">(CTAS)CREATE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="1e56f-142">(CRTAS)CREATE REMOTE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="1e56f-143">(CETAS)CREATE EXTERNAL TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="1e56f-144">CTE로부터 원격 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="1e56f-145">CTE로부터 외부 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="1e56f-146">CTE에 여러 개의 CTE 쿼리 정의를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="1e56f-147">CTE 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1e56f-147">CTE Limitations</span></span>
<span data-ttu-id="1e56f-148">공용 테이블 식은 SQL 데이터 웨어하우스에서 다음을 포함하여 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="1e56f-149">CTE는 단일 SELECT 문 뒤에 와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="1e56f-150">INSERT, UPDATE, DELETE 및 MERGE 문은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="1e56f-151">참조 tooitself (재귀 공통 테이블 식)를 포함 하는 공통 테이블 식은 지원 되지 않습니다 (아래 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="1e56f-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="1e56f-152">CTE에 둘 이상의 WITH 절을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="1e56f-153">예를 들어 CTE_query_definition에 하위 쿼리가 포함된 경우 해당 하위 쿼리에는 다른 CTE를 정의하는 중첩된 WITH 절을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="1e56f-154">TOP 절을 지정 하는 경우 ORDER BY 절을 제외 하 고 hello CTE_query_definition에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="1e56f-155">일괄 처리의 일부로 문에서 CTE가 사용 하는 경우 세미콜론으로 전의 hello 문 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="1e56f-156">Cte hello가 작동 하는 sp_prepare에서 준비 된 문을 사용할 경우 동일한 방식으로 PDW에서 다른 SELECT 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="1e56f-157">그러나 Cte CETAS sp_prepare에서 준비의 일환으로 사용 되 면 hello 동작 SQL Server와 다른 PDW 문 sp_prepare에 대 한 바인딩을 구현 하는 hello 방식으로 인해 연기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="1e56f-158">선택 CTE는 CTE에 존재 하지 않는 잘못 된 열을 사용 하는 참조, hello sp_prepare hello 오류를 검색 하지 않고 통과 합니다 하지만 대신 hello 오류가 sp_execute 하는 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="1e56f-159">재귀 CTE</span><span class="sxs-lookup"><span data-stu-id="1e56f-159">Recursive CTEs</span></span>
<span data-ttu-id="1e56f-160">재귀 CTE는 SQL 데이터 웨어하우스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="1e56f-161">재귀적 CTE의 hello 마이그레이션 다소 복잡할 수 있으며 hello 최상의 프로세스는 toobreak 여러 단계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="1e56f-162">일반적으로 루프를 사용 하 고 hello 재귀 중간 쿼리를 반복 하는 대로 임시 테이블을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="1e56f-163">Hello 임시 테이블은 채워진 후에 단일 결과 집합으로 다음 hello 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="1e56f-164">유사한 방법을 사용 하는 toosolve 되었습니다 `GROUP BY WITH CUBE` hello에 [롤업 절에 의해 그룹 / 큐브 / 그룹화 집합 옵션이] [ group by clause with rollup / cube / grouping sets options] 문서.</span><span class="sxs-lookup"><span data-stu-id="1e56f-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="1e56f-165">지원되지 않는 시스템 함수</span><span class="sxs-lookup"><span data-stu-id="1e56f-165">Unsupported system functions</span></span>
<span data-ttu-id="1e56f-166">지원하지 않는 일부 시스템 함수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="1e56f-167">Hello 주요 경우가 일반적으로 데이터 웨어하우징에 사용 되는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="1e56f-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="1e56f-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="1e56f-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="1e56f-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="1e56f-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="1e56f-170">@@IDENTITY()</span></span>
* <span data-ttu-id="1e56f-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="1e56f-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="1e56f-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="1e56f-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="1e56f-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="1e56f-173">ERROR_LINE()</span></span>

<span data-ttu-id="1e56f-174">이러한 문제 중 일부는 해결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="1e56f-175">@@ROWCOUNT 해결 방법</span><span class="sxs-lookup"><span data-stu-id="1e56f-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="1e56f-176">@에 대 한 지원 부족 주위 toowork@ROWCOUNT, sys.dm_pdw_request_steps에서 hello 마지막 행 개수를 검색 하 고 다음 실행 하는 저장된 프로시저를 만들 `EXEC LastRowCount` DML 문 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e56f-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="1e56f-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e56f-177">Next steps</span></span>
<span data-ttu-id="1e56f-178">지원되는 모든 T-SQL 문의 전체 목록은 [Transact-SQL 항목][Transact-SQL topics]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e56f-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
