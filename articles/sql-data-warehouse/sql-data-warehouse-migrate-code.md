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
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>SQL 코드 tooSQL 데이터 웨어하우스 마이그레이션
이 문서에서는 시켜야 합니다 toomake 다른 데이터베이스 tooSQL 데이터 웨어하우스에서에서 코드를 마이그레이션할 때 코드 변경 내용을 설명 합니다. 일부 SQL 데이터 웨어하우스 기능 분산 방식에서 디자인 된 toowork 멤버인 성능은 크게 개선 수 있습니다. 그러나 toomaintain 성능 및 확장성 일부 기능은 사용할 수 없습니다.

## <a name="common-t-sql-limitations"></a>일반적인 T-SQL 제한 사항
다음 목록 hello SQL 데이터 웨어하우스를 지원 하지 않는 hello 가장 일반적인 기능을 요약 합니다. hello 링크를 이동 하면 hello 지원 되지 않는 기능에 대 한 tooworkarounds 있습니다.

* [업데이트 시 ANSI 조인][ANSI joins on updates]
* [삭제 시 ANSI 조인][ANSI joins on deletes]
* [병합 문][merge statement]
* 데이터베이스 간 조인
* [커서][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* output 절
* 인라인 사용자 정의 함수
* 다중 문 함수
* [공통 테이블 식](#Common-table-expressions)
* [재귀 공통 테이블 식(CTE)](#Recursive-common-table-expressions-(CTE)
* CLR 함수 및 프로시저
* $partition 함수
* 테이블 변수
* 테이블 값 매개 변수
* 분산된 트랜잭션
* 커밋 / 롤백 작업
* 트랜잭션 저장
* 실행 컨텍스트 (EXECUTE AS)
* [롤업/큐브/그룹화 집합 옵션을 사용하는 GROUP BY 절][group by clause with rollup / cube / grouping sets options]
* [8을 초과한 중첩 수준][nesting levels beyond 8]
* [뷰를 통한 업데이트][updating through views]
* [변수 할당에 대한 select 사용][use of select for variable assignment]
* [동적 SQL 문자열에 대한 MAX 데이터 형식 없음][no MAX data type for dynamic SQL strings]

다행히 대부분의 이러한 제한을 해결할 수 있습니다. 앞서 설명 된 hello 관련 개발 문서에 설명이 제공 됩니다.

## <a name="supported-cte-features"></a>지원되는 CTE 기능
CTE(공용 테이블 식)는 SQL 데이터 웨어하우스에서 부분적으로 지원됩니다.  같은 CTE 기능 hello는 현재 지원 됩니다.

* SELECT 문에서 CTE를 지정할 수 있습니다.
* CREATE VIEW 문에서 CTE를 지정할 수 있습니다.
* (CTAS)CREATE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.
* (CRTAS)CREATE REMOTE TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.
* (CETAS)CREATE EXTERNAL TABLE AS SELECT 문에서 CTE를 지정할 수 있습니다.
* CTE로부터 원격 테이블을 참조할 수 있습니다.
* CTE로부터 외부 테이블을 참조할 수 있습니다.
* CTE에 여러 개의 CTE 쿼리 정의를 정의할 수 있습니다.

## <a name="cte-limitations"></a>CTE 제한 사항
공용 테이블 식은 SQL 데이터 웨어하우스에서 다음을 포함하여 몇 가지 제한 사항이 있습니다.

* CTE는 단일 SELECT 문 뒤에 와야 합니다. INSERT, UPDATE, DELETE 및 MERGE 문은 지원되지 않습니다.
* 참조 tooitself (재귀 공통 테이블 식)를 포함 하는 공통 테이블 식은 지원 되지 않습니다 (아래 섹션 참조).
* CTE에 둘 이상의 WITH 절을 지정할 수 없습니다. 예를 들어 CTE_query_definition에 하위 쿼리가 포함된 경우 해당 하위 쿼리에는 다른 CTE를 정의하는 중첩된 WITH 절을 포함할 수 없습니다.
* TOP 절을 지정 하는 경우 ORDER BY 절을 제외 하 고 hello CTE_query_definition에 사용할 수 없습니다.
* 일괄 처리의 일부로 문에서 CTE가 사용 하는 경우 세미콜론으로 전의 hello 문 따라야 합니다.
* Cte hello가 작동 하는 sp_prepare에서 준비 된 문을 사용할 경우 동일한 방식으로 PDW에서 다른 SELECT 문의 합니다. 그러나 Cte CETAS sp_prepare에서 준비의 일환으로 사용 되 면 hello 동작 SQL Server와 다른 PDW 문 sp_prepare에 대 한 바인딩을 구현 하는 hello 방식으로 인해 연기할 수 있습니다. 선택 CTE는 CTE에 존재 하지 않는 잘못 된 열을 사용 하는 참조, hello sp_prepare hello 오류를 검색 하지 않고 통과 합니다 하지만 대신 hello 오류가 sp_execute 하는 동안 발생 합니다.

## <a name="recursive-ctes"></a>재귀 CTE
재귀 CTE는 SQL 데이터 웨어하우스에서 지원되지 않습니다.  재귀적 CTE의 hello 마이그레이션 다소 복잡할 수 있으며 hello 최상의 프로세스는 toobreak 여러 단계에 있습니다. 일반적으로 루프를 사용 하 고 hello 재귀 중간 쿼리를 반복 하는 대로 임시 테이블을 채울 수 있습니다. Hello 임시 테이블은 채워진 후에 단일 결과 집합으로 다음 hello 데이터를 반환할 수 있습니다. 유사한 방법을 사용 하는 toosolve 되었습니다 `GROUP BY WITH CUBE` hello에 [롤업 절에 의해 그룹 / 큐브 / 그룹화 집합 옵션이] [ group by clause with rollup / cube / grouping sets options] 문서.

## <a name="unsupported-system-functions"></a>지원되지 않는 시스템 함수
지원하지 않는 일부 시스템 함수도 있습니다. Hello 주요 경우가 일반적으로 데이터 웨어하우징에 사용 되는 다음과 같습니다.

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

이러한 문제 중 일부는 해결될 수 있습니다.

## <a name="rowcount-workaround"></a>@@ROWCOUNT 해결 방법
@에 대 한 지원 부족 주위 toowork@ROWCOUNT, sys.dm_pdw_request_steps에서 hello 마지막 행 개수를 검색 하 고 다음 실행 하는 저장된 프로시저를 만들 `EXEC LastRowCount` DML 문 다음 합니다.

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

## <a name="next-steps"></a>다음 단계
지원되는 모든 T-SQL 문의 전체 목록은 [Transact-SQL 항목][Transact-SQL topics]을 참조하세요.

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
