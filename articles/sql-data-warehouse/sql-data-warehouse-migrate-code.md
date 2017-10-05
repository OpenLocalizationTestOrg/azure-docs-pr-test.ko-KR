---
title: "SQL Data Warehouse에 SQL 코드 마이그레이션| Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스로 SQL 코드를 마이그레이션하기 위한 팁"
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
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="2894c-103">SQL 데이터 웨어하우스에 SQL 코드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2894c-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="2894c-104">이 문서는 다른 데이터베이스에서 SQL Data Warehouse로 코드를 마이그레이션하는 경우 수행해야 하는 코드 변경 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="2894c-105">일부 SQL 데이터 웨어하우스 기능은 원래 분산 방식으로 작동하도록 디자인되었기 때문에 크게 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="2894c-106">그러나 성능 및 확장을 유지하려면 일부 기능은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="2894c-107">일반적인 T-SQL 제한 사항</span><span class="sxs-lookup"><span data-stu-id="2894c-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="2894c-108">다음 목록에서는 SQL Data Warehouse에서 지원하지 않는 가장 일반적인 기능을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="2894c-109">링크를 따라 이동하면 지원되지 않는 기능에 대한 대안을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="2894c-110">[업데이트 시 ANSI 조인][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="2894c-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="2894c-111">[삭제 시 ANSI 조인][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="2894c-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="2894c-112">[병합 문][merge statement]</span><span class="sxs-lookup"><span data-stu-id="2894c-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="2894c-113">데이터베이스 간 조인</span><span class="sxs-lookup"><span data-stu-id="2894c-113">cross-database joins</span></span>
* <span data-ttu-id="2894c-114">[커서][cursors]</span><span class="sxs-lookup"><span data-stu-id="2894c-114">[cursors][cursors]</span></span>
* <span data-ttu-id="2894c-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="2894c-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="2894c-116">output 절</span><span class="sxs-lookup"><span data-stu-id="2894c-116">output clause</span></span>
* <span data-ttu-id="2894c-117">인라인 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="2894c-117">inline user-defined functions</span></span>
* <span data-ttu-id="2894c-118">다중 문 함수</span><span class="sxs-lookup"><span data-stu-id="2894c-118">multi-statement functions</span></span>
* [<span data-ttu-id="2894c-119">공통 테이블 식</span><span class="sxs-lookup"><span data-stu-id="2894c-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="2894c-120">[재귀 공통 테이블 식(CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="2894c-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="2894c-121">CLR 함수 및 프로시저</span><span class="sxs-lookup"><span data-stu-id="2894c-121">CLR functions and procedures</span></span>
* <span data-ttu-id="2894c-122">$partition 함수</span><span class="sxs-lookup"><span data-stu-id="2894c-122">$partition function</span></span>
* <span data-ttu-id="2894c-123">테이블 변수</span><span class="sxs-lookup"><span data-stu-id="2894c-123">table variables</span></span>
* <span data-ttu-id="2894c-124">테이블 값 매개 변수</span><span class="sxs-lookup"><span data-stu-id="2894c-124">table value parameters</span></span>
* <span data-ttu-id="2894c-125">분산된 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="2894c-125">distributed transactions</span></span>
* <span data-ttu-id="2894c-126">커밋 / 롤백 작업</span><span class="sxs-lookup"><span data-stu-id="2894c-126">commit / rollback work</span></span>
* <span data-ttu-id="2894c-127">트랜잭션 저장</span><span class="sxs-lookup"><span data-stu-id="2894c-127">save transaction</span></span>
* <span data-ttu-id="2894c-128">실행 컨텍스트 (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="2894c-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="2894c-129">[롤업/큐브/그룹화 집합 옵션을 사용하는 GROUP BY 절][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="2894c-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="2894c-130">[8을 초과한 중첩 수준][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="2894c-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="2894c-131">[뷰를 통한 업데이트][updating through views]</span><span class="sxs-lookup"><span data-stu-id="2894c-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="2894c-132">[변수 할당에 대한 select 사용][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="2894c-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="2894c-133">[동적 SQL 문자열에 대한 MAX 데이터 형식 없음][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="2894c-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="2894c-134">다행히 대부분의 이러한 제한을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="2894c-135">위에서 언급한 개발 관련 문서에 대한 설명이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="2894c-136">지원되는 CTE 기능</span><span class="sxs-lookup"><span data-stu-id="2894c-136">Supported CTE features</span></span>
<span data-ttu-id="2894c-137">CTE(공용 테이블 식)는 SQL 데이터 웨어하우스에서 부분적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="2894c-138">현재 지원되는 CTE 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="2894c-139">SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="2894c-140">CREATE VIEW 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="2894c-141">(CTAS)CREATE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="2894c-142">(CRTAS)CREATE REMOTE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="2894c-143">(CETAS)CREATE EXTERNAL TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="2894c-144">CTE로부터 원격 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="2894c-145">CTE로부터 외부 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="2894c-146">CTE에 여러 개의 CTE 쿼리 정의를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="2894c-147">CTE 제한 사항</span><span class="sxs-lookup"><span data-stu-id="2894c-147">CTE Limitations</span></span>
<span data-ttu-id="2894c-148">공용 테이블 식은 SQL 데이터 웨어하우스에서 다음을 포함하여 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="2894c-149">CTE는 단일 SELECT 문 뒤에 와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="2894c-150">INSERT, UPDATE, DELETE 및 MERGE 문은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="2894c-151">자체에 대한 참조를 포함하는 공통 테이블 식(재귀 공통 테이블 식)은 지원되지 않습니다(아래 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="2894c-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="2894c-152">CTE에 둘 이상의 WITH 절을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="2894c-153">예를 들어 CTE_query_definition에 하위 쿼리가 포함된 경우 해당 하위 쿼리에는 다른 CTE를 정의하는 중첩된 WITH 절을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="2894c-154">TOP 절이 지정된 경우를 제외하고 ORDER BY 절은 CTE_query_definition에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="2894c-155">일괄 처리의 일부인 문에서 CTE가 사용되는 경우 그 전의 문 뒤에 세미콜론이 와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="2894c-156">Sp_prepare에 의해 준비된 문에서 사용할 경우 CTE는 PDW에서 다른 SELECT 문과 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="2894c-157">그러나 sp_prepare를 통해 준비된 CETAS의 일부로 CTE를 사용할 경우 sp_prepare에 대해 구현되는 바인딩 방식이 다르기 때문에 동작이 SQL Server 및 다른 PDW와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="2894c-158">CTE를 참조하는 SELECT 문이 CTE에 없는 잘못된 열을 사용할 경우 오류를 감지하지 않고 sp_prepare를 통과합니다. 대신 sp_execute 동안 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="2894c-159">재귀 CTE</span><span class="sxs-lookup"><span data-stu-id="2894c-159">Recursive CTEs</span></span>
<span data-ttu-id="2894c-160">재귀 CTE는 SQL 데이터 웨어하우스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="2894c-161">재귀 CTE의 마이그레이션은 복잡할 수 있지만 가장 좋은 프로세스는 여러 단계로 분할하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="2894c-162">재귀 중간 쿼리를 반복할 때 일반적으로 루프를 사용하여 임시 테이블을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="2894c-163">임시 테이블을 채우고 나면 데이터를 단일 결과 집합으로 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="2894c-164">[롤업/큐브/그룹화 집합 옵션을 사용하는 GROUP BY 절][group by clause with rollup / cube / grouping sets options] 문서에서 `GROUP BY WITH CUBE`를 해결하는 데 사용한 것과 비슷한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="2894c-165">지원되지 않는 시스템 함수</span><span class="sxs-lookup"><span data-stu-id="2894c-165">Unsupported system functions</span></span>
<span data-ttu-id="2894c-166">지원하지 않는 일부 시스템 함수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="2894c-167">일반적으로 데이터 웨어하우징에서 사용될 수 있는 일부 기본 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="2894c-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="2894c-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="2894c-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="2894c-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="2894c-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="2894c-170">@@IDENTITY()</span></span>
* <span data-ttu-id="2894c-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="2894c-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="2894c-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="2894c-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="2894c-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="2894c-173">ERROR_LINE()</span></span>

<span data-ttu-id="2894c-174">이러한 문제 중 일부는 해결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="2894c-175">@@ROWCOUNT 해결 방법</span><span class="sxs-lookup"><span data-stu-id="2894c-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="2894c-176">@@ROWCOUNT에 대한 지원 부족 문제를 해결하려면 sys.dm_pdw_request_steps에서 마지막 행 수를 검색한 후 DML 문 다음에 `EXEC LastRowCount`를 실행하는 저장 절차를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2894c-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2894c-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2894c-177">Next steps</span></span>
<span data-ttu-id="2894c-178">지원되는 모든 T-SQL 문의 전체 목록은 [Transact-SQL 항목][Transact-SQL topics]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2894c-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
