---
title: "SQL 데이터 웨어하우스에 aaaTransactions | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 트랜잭션 구현을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 트랜잭션
와 마찬가지로, SQL 데이터 웨어하우스 트랜잭션을 hello 데이터 웨어하우스 작업의 일환으로 지원 합니다. 그러나 SQL 데이터 웨어하우스의 tooensure hello 성능은 비교 tooSQL 서버 일부 기능을 제한 하는 규모에 유지 됩니다. Hello 차이점을 설명 하는이 문서 및 목록 hello 다른 합니다. 

## <a name="transaction-isolation-levels"></a>트랜잭션 격리 수준
SQL 데이터 웨어하우스는 ACID 트랜잭션을 구현합니다. 그러나 hello hello 트랜잭션 지원의 격리는 너무 제한`READ UNCOMMITTED` 변경할 수 없습니다. 다양 한 문제가이 경우 데이터의 tooprevent 더티 읽기 코딩 방법 구현할 수 있습니다. hello 가장 인기 있는 메서드 및 활용 하 여 모두 CTAS에는 테이블 파티션 전환 (종종 라고도 함 슬라이딩 창 패턴 hello) tooprevent 사용자가 여전히 준비 중인 데이터를 쿼리 합니다. 뷰 미리 hello 데이터를 필터링 하는 일반적인 접근 방법 이기도 합니다.  

## <a name="transaction-size"></a>트랜잭션 크기
단일 데이터 수정 트랜잭션은 크기가 제한됩니다. 오늘 "배포" 당 hello 제한이 적용 됩니다. 따라서 hello 제한 hello 배포 수로 곱하여 hello 총 할당을 계산할 수 있습니다. tooapproximate hello 최대 행 개수 hello 트랜잭션에서 각 행의 총 크기 hello hello 배포 cap을 나눕니다. 가변 길이 열에 대 한 hello 최대 크기를 사용 하는 대신 수행 된 평균 열 길이 보십시오.

Hello 아래 hello 테이블에 다음과 같은 가정은 적용 했습니다.

* 균일한 데이터 분포가 발생했습니다. 
* hello 평균 행 길이 250 바이트

| [DWU][DWU] | 배포당 용량(GiB) | 배포 수 | 최대 트랜잭션 크기(GiB) | 배포 당 행 수 | 트랜잭션당 최대 행 수 |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4,000,000 |240,000,000 |
| DW200 |1.5 |60 |90 |6,000,000 |360,000,000 |
| DW300 |2.25 |60 |135 |9,000,000 |540,000,000 |
| DW400 |3 |60 |180 |12,000,000 |720,000,000 |
| DW500 |3.75 |60 |225 |15,000,000 |900,000,000 |
| DW600 |4.5. |60 |270 |18,000,000 |1,080,000,000 |
| DW1000 |7.5 |60 |450 |30,000,000 |1,800,000,000 |
| DW1200 |9 |60 |540 |36,000,000 |2,160,000,000 |
| DW1500 |11.25 |60 |675 |45,000,000 |2,700,000,000 |
| DW2000 |15 |60 |900 |60,000,000 |3,600,000,000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

트랜잭션 또는 작업 마다 hello 트랜잭션 크기 제한이 적용 됩니다. 모든 동시 트랜잭션에서 적용되지는 않습니다. 따라서 각 트랜잭션에이 데이터 toohello 로그이 정도의 toowrite 허용 합니다. 

toooptimize hello toohello 로그에 기록 된 데이터 양을 최소화 하 고 toohello를 참조 하십시오 [트랜잭션을 모범 사례] [ Transactions best practices] 문서.

> [!WARNING]
> 해시에 대 한 트랜잭션 크기를 수행할 수 있습니다 또는 ROUND_ROBIN distributed 테이블의 hello 확산 되는 위치 데이터를 환영 최대 hello 짝수 이면 합니다. Hello 트랜잭션 쓰는 경우 데이터는 왜곡 된 방식에서 toohello 분포 hello 제한 이면 가능성이 toobe 이전 toohello 최대 트랜잭션 크기에 도달 합니다.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>트랜잭션 상태
SQL 데이터 웨어하우스는 hello XACT_STATE 함수 tooreport hello 값-2를 사용 하 여 실패 한 트랜잭션을 사용 합니다. 즉, hello 트랜잭션이 실패 하 고만 롤백에 대 한 표시

> [!NOTE]
> -2의 실패 한 트랜잭션 나타내는 다른 동작이 tooSQL 서버 hello XACT_STATE 함수 toodenote로 hello를 사용 합니다. SQL Server hello 값-1 toorepresent 커밋할 트랜잭션이 사용합니다. SQL Server toobe로 커밋할 표시 없이 트랜잭션 내에서는 몇 가지 오류를 허용할 수 있습니다. 예를 들어 `SELECT 1/0` 은 오류를 발생시키지만 커밋할 수 없는 상태로 트랜잭션을 강제 적용하지 않습니다. 또한 SQL Server는 hello 커밋할 트랜잭션에서 읽기를 허용합니다. 그러나 SQL 데이터 웨어하우스는 이를 허용하지 않습니다. Hello-2 상태가 자동으로 전환 됩니다 및 수 toomake 됩니다 SQL 데이터 웨어하우스 트랜잭션 내부에서 오류가 발생 하는 경우 모든 추가 문을 때까지 선택 hello 문을 롤백 되었습니다. 따라서 중요 한 toocheck XACT_STATE 때 사용 하는 경우 응용 프로그램 코드 toosee toomake 코드를 수정 해야 할 수는 버전이 있습니다.
> 
> 

예를 들어 SQL Server에서 다음과 같은 트랜잭션이 나타날 수 있습니다.

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

위에 있기 때문에 코드를 그대로 둔 hello 다음과 같은 오류 메시지가 발생 합니다.

메시지 111233, 수준 16, 상태 1, 줄 1 111233; 현재 트랜잭션이 중단 및 보류 중인 변경 내용이 롤백 되었다는 hello 합니다. 원인: 롤백 전용 상태의 트랜잭션은 DDL, DML 또는 SELECT 문 이전에 명시적으로 롤백되지 않았습니다.

Hello 오류 * 함수 hello 출력 하지 발생 하기도 합니다.

SQL 데이터 웨어하우스 hello 코드 toobe 약간 변경 해야 합니다.

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

hello 동작을 따릅니다 이제 필요 합니다. hello 트랜잭션에서 hello 오류는 관리 하 고 hello 오류 * 함수 예상 대로 값을 제공 합니다.

변경 된 모든는 해당 hello `ROLLBACK` hello의 트랜잭션 이전의 toohappen hello hello에 대 한 hello 오류 정보의 읽을 `CATCH` 블록입니다.

## <a name="errorline-function"></a>Error_Line() 함수
SQL 데이터 웨어하우스 구현 하거나 hello error_line () 함수를 지원 하지 않는 주목할 만한 이기도 합니다. Tooremove 해야는 코드에서이 있는 경우 그 toobe SQL 데이터 웨어하우스를 준수 합니다. 레이블을 사용 하 여 쿼리 코드에서 대신 tooimplement 이와 동일한 기능입니다. Toohello를 참조 하십시오 [레이블] [ LABEL] 이 기능에 대 한 자세한 내용은 문서입니다.

## <a name="using-throw-and-raiserror"></a>THROW 및 RAISERROR 사용
THROW는 hello SQL 데이터 웨어하우스의 예외를 발생 시키기 위한 최신 구현 하지만 RAISERROR도 지원 합니다. 주의 기울여야 toohowever 가치가 있는 몇 가지 차이점이 있습니다.

* 사용자 정의 오류 메시지 번호 100000 150000 범위 THROW에 대 한 hello에 있을 수 없습니다.
* RAISERROR 오류 메시지는 50,000으로 고정됩니다.
* sys.messages 사용은 지원되지 않습니다.

## <a name="limitiations"></a>제한 사항
SQL 데이터 웨어하우스 tootransactions와 관련 된 몇 가지 제한에는.

다음과 같습니다.

* 분산된 트랜잭션이 없습니다
* 중첩된 트랜잭션이 허용되지 않습니다.
* 저장 점수를 사용할 수 없습니다.
* 명명된 트랜잭션이 없습니다.
* 표시된 트랜잭션이 없습니다.
* 사용자 정의 트랜잭션 내에 `CREATE TABLE` 과 같은 DDL 지원은 없습니다.

## <a name="next-steps"></a>다음 단계
트랜잭션을 최적화에 대 한 더 toolearn 참조 [트랜잭션을 모범 사례][Transactions best practices]합니다.  기타 SQL 데이터 웨어하우스 모범 사례에 대 한 toolearn 참조 [SQL 데이터 웨어하우스 모범 사례][SQL Data Warehouse best practices]합니다.

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
