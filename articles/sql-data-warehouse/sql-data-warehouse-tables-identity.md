---
title: "ID를 사용 하 여 서로게이트 키 aaaCreate | Microsoft Docs"
description: "테이블에 toouse IDENTITY toocreate 서로게이트 키 하는 방법에 대해 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>IDENTITY를 사용하여 서로게이트 키 만들기
> [!div class="op_single_selector"]
> * [개요][Overview]
> * [데이터 형식][Data Types]
> * [배포][Distribute]
> * [인덱스][Index]
> * [파티션][Partition]
> * [통계][Statistics]
> * [임시][Temporary]
> * [ID][Identity]
> 
> 

많은 데이터 모델러는 데이터 웨어하우스 모델을 디자인할 때 해당 테이블에 toocreate 서로게이트 키 같은입니다. 사용할 수 있습니다 hello IDENTITY 속성 tooachieve이이 목표 간단 하 고 효과적으로 로드 성능에 영향을 주지 않고. 

## <a name="get-started-with-identity"></a>IDENTITY 시작
테이블은 유사한 toohello 문 다음 구문을 사용 하 여 hello 테이블을 처음 만들 때 hello IDENTITY 속성이 있는 것으로 정의할 수 있습니다.

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

사용할 수 있습니다 `INSERT..SELECT` toopopulate hello 테이블입니다.

## <a name="behavior"></a>동작
hello IDENTITY 속성으로 설계 된 tooscale 로드 성능에 영향을 주지 않고 hello 데이터 웨어하우스의 모든 hello 분포 값은입니다. 따라서 ID의 hello 구현 이러한 목표를 달성과 관련 방향입니다. 이 섹션에서는 hello 갖는 요약 hello 구현 toohelp의 올바르게 이해 하 보다 완전 하 게 합니다.  

### <a name="allocation-of-values"></a>값 할당
hello IDENTITY 속성에는 SQL Server 및 Azure SQL 데이터베이스의 hello 동작을 반영 하는 hello 순서는 hello 서로게이트 값에 할당 된, 가능성이 보장 되지 않습니다. 그러나 Azure SQL 데이터 웨어하우스의 보장 hello 없을 경우 더 많이 듭니다. 

다음 예제는 hello이를 보여 줍니다.

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

앞 예제는 hello에서 두 개의 행 배포 1에에서 연결 합니다. 열에서 hello 서로게이트 값이 1에 대 한 hello 첫 번째 행은 `C1`, hello 두 번째 행에 61의 hello 서로게이트 값 및 합니다. Hello IDENTITY 속성에 의해 생성 된 두이 값을 합니다. 그러나 hello 값의 hello 할당 인접 하지 않습니다. 이 동작은 의도된 것입니다.

### <a name="skewed-data"></a>불균형 데이터 
hello 데이터 형식에 대 한 값의 hello 범위 hello 배포판을 균등 하 게 분산 되어 있습니다. 분산된 테이블이 일치 하지 않는 데이터에서 발생 하는 경우 사용할 수 있는 toohello datatype을 중간 소진 될 수 있습니다. 값의 범위를 hello 합니다. 예를 들어 모든 hello 데이터는 단일 분포에서 끝난 경우 효과적으로 hello 테이블에 한 hello hello 데이터 형식이 값 액세스 tooonly sixtieth 하나 있습니다. 이러한 이유로 hello IDENTITY 속성은 제한 된 너무`INT` 및 `BIGINT` 데이터 형식에 합니다.

### <a name="selectinto"></a>SELECT..INTO
기존 ID 열을 새 테이블로 선택 하면 hello 다음 조건 중 하나는 경우에 hello 새 열 hello IDENTITY 속성을 상속 합니다.
- hello SELECT 문에 조인이 포함 되어 있습니다.
- UNION을 사용하여 여러 SELECT 문이 조인됩니다.
- hello ID 열에는 한 번 이상 hello 선택 목록에 나열 됩니다.
- hello ID 열이 식의 일부입니다.
    
이러한 조건 중 하나라도 true 이면 hello 열 hello IDENTITY 속성을 상속 하는 대신 NULL이 아닌 생성 됩니다.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
만들 테이블 AS 선택 (CTAS에는) 다음과 같은 SQL Server 동작 선택에 대 한 설명 하는 hello... 합니다. 그러나 Hello의 hello 열 정의에 IDENTITY 속성을 지정할 수 없습니다 `CREATE TABLE` hello 문의 일부로 합니다. 또한 hello에 hello IDENTITY 함수를 사용할 수 없습니다 `SELECT` hello CTAS에 포함 합니다. 테이블 toopopulate 해야 toouse `CREATE TABLE` toodefine hello 테이블 뒤 `INSERT..SELECT` toopopulate 것입니다.

## <a name="explicitly-insert-values-into-an-identity-column"></a>IDENTITY 열에 값을 명시적으로 삽입 
SQL Data Warehouse는 `SET IDENTITY_INSERT <your table> ON|OFF` 구문을 지원합니다. Hello ID 열에 값이 구문 tooexplicitly 삽입을 사용할 수 있습니다.

많은 데이터 모델러 toouse 미리 정의 된 음수 값을 특정 해당 차원에 있는 행 처럼 합니다. 예-1 hello 또는 "알 수 없는 멤버" 행입니다. 

다음 스크립트 hello tooexplicitly SET IDENTITY_INSERT를 사용 하 여이 행을 추가 하는 방법을 보여 줍니다.

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>IDENTITY가 있는 테이블에 데이터 로드

hello IDENTITY 속성의 hello 존재 일부 영향 tooyour 데이터 로드 코드를 있습니다. 이 섹션에서는 IDENTITY를 사용하여 테이블로 데이터를 로드하는 몇 가지 기본 패턴을 강조 표시합니다. 

### <a name="load-data-with-polybase"></a>PolyBase를 사용하여 데이터 로드
tooload 데이터를 테이블에 ID를 사용 하 여 서로게이트 키를 생성 하 고 hello 테이블 만들기 및 다음 INSERT를 사용 하 여... SELECT 또는 INSERT... 값 tooperform hello 로드 합니다.

hello 다음 예제에서는 하이라이트 hello 기본 패턴:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> 가능한 toouse 없으면 `CREATE TABLE AS SELECT` 현재 ID 열이 있는 테이블에 데이터를 로드 하는 경우.
> 

Hello 대량 복사 프로그램 (BCP) 도구를 사용 하 여 데이터 로드에 대 한 자세한 내용은 다음 문서는 hello 참조:

- [PolyBase로 로드하기][]
- [PolyBase 모범 사례][]

### <a name="load-data-with-bcp"></a>BCP를 사용하여 데이터 로드
BCP는 명령줄 도구를 SQL 데이터 웨어하우스에 tooload 데이터를 사용할 수 있습니다. 해당 매개 변수 중 하나 (-E) ID 열이 있는 테이블에 데이터를 로드할 때 컨트롤 hello BCP의 동작입니다. 

-E를 지정 하는 경우 ID를 가진 hello hello 열에 대 한 입력된 파일에 보관 hello 값이 유지 됩니다. -E가 *하지* 지정 하면이 열의 hello 값은 무시 됩니다. Hello id 열을 지정 하지 않은 경우 hello 데이터가 정상적으로 로드 됩니다. hello 값 hello 속성의 toohello 증가 및 시드 정책에 따라 생성 됩니다.

BCP를 사용 하 여 데이터를 로드에 대 한 자세한 내용은 다음 문서는 hello 참조:

- [BCP로 로드하기][]
- [MSDN의 BCP][]

## <a name="catalog-views"></a>카탈로그 뷰
SQL 데이터 웨어하우스 지원 hello `sys.identity_columns` 카탈로그 뷰에 있습니다. 이 보기에 사용 되는 tooidentify hello IDENTITY 속성이 있는 열 수 있습니다.

hello 데이터베이스 스키마를 더 잘 이해 toohelp,이 예제에서는 어떻게 toointegrate `sys.identity_columns` 다른 시스템 카탈로그 뷰와:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>제한 사항
다음 시나리오는 hello에 hello IDENTITY 속성을 사용할 수 없습니다.
- Hello 열 데이터 형식이 인 하지 정수나 BIGINT
- Hello 열이 hello 배포 키도
- Hello 테이블은 외부 테이블 

hello 관련된 함수를 다음 SQL 데이터 웨어하우스에서 지원 되지 않습니다.

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>작업

이 섹션에는 몇 가지 샘플 코드에서는 ID 열을 사용 하 여 작업할 때 tooperform 일반적인 작업을 사용할 수 있습니다.

> [!NOTE] 
> 열 C1는 작업을 수행 하는 모든 hello에 hello IDENTITY입니다.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>테이블에 할당 된 hello 가장 높은 값을 찾을
사용 하 여 hello `MAX()` toodetermine hello 가장 높은 값 분산된 테이블에 할당 된 함수:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Hello IDENTITY 속성에 대 한 hello 초기값 및 증가값을 찾기
다음 쿼리에서 hello를 사용 하 여 테이블에 대 한 hello 카탈로그 뷰 toodiscover hello identity 초기값 및 증가값 구성 값을 사용할 수 있습니다. 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>다음 단계

* 참조 테이블의 경우 개발에 대 한 더 toolearn [테이블 개요][Overview], [데이터 형식이 테이블][Data Types], [테이블배포] [ Distribute], [테이블 인덱스][Index], [테이블 분할][Partition], 및 [ 임시 테이블][Temporary]합니다. 
* 모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[BCP로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[PolyBase로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase 모범 사례]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[MSDN의 BCP]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
