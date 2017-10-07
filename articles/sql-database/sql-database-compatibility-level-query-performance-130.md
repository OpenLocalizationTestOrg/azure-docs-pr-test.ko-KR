---
title: "aaaDatabase 호환성 수준 130-Azure SQL 데이터베이스 | Microsoft Docs"
description: "이 문서에서는 호환성 수준 130에서 Azure SQL 데이터베이스를 실행 하 고 hello 새 쿼리 최적화 프로그램의 hello 혜택을 활용 하 여 hello 이점을 탐색 하 고 쿼리 프로세서 기능. Hello 가능한 부작용 hello 기존 SQL 응용 프로그램에 대 한 hello 쿼리 성능에 해결합니다."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능
Azure SQL 데이터베이스 실행 투명 하 게 수백, 수천 데이터베이스의 여러 다른 호환성 수준에서 유지 하 고 모든 고객에 대 한 hello 이전 버전과 호환성 toohello Microsoft SQL Server의 해당 버전을 보장 하기!

이 문서에서는 호환성 수준 130에서 Azure SQL 데이터베이스를 실행 하 고 hello 새 쿼리 최적화 프로그램의 hello 혜택을 활용 하 여 hello 이점을 탐색 하 고 쿼리 프로세서 기능. Hello 가능한 부작용 hello 기존 SQL 응용 프로그램에 대 한 hello 쿼리 성능에 해결합니다.

기록의 알림으로 SQL 버전 toodefault 호환성 수준의 hello 맞춤은 다음과 같습니다.

* 100: SQL Server 2008 및 Azure SQL 데이터베이스 V11.
* 110: SQL Server 2012 및 Azure SQL 데이터베이스 V11.
* 120: SQL Server 2014 및 Azure SQL 데이터베이스 V12.
* 130: SQL Server 2016 및 Azure SQL 데이터베이스 V12.

> [!IMPORTANT]
> 부터는 **mid-2016 년 6 월**, Azure SQL 데이터베이스 hello 기본 호환성 수준 130에 대 한 120 대신 됩니다 **새로 만든** 데이터베이스.
> 
> 2016년 6월 중순 전에 만든 데이터베이스는 영향을 받지 *않고* , 현재 호환성 수준(100, 110, 또는 120)을 유지하게 됩니다. Azure SQL 데이터베이스 버전 V11 tooV12에서에서 마이그레이션된 데이터베이스 호환성 수준이 100 또는 110 갖습니다. 
> 

## <a name="about-compatibility-level-130"></a>호환성 수준 130에 대한 정보
첫째, 데이터베이스의 tooknow hello 현재 호환성 수준을 원한다 면 hello Transact SQL 문 다음을 실행 합니다.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


이러한 변경 전에 toolevel 130에 대 한 발생 **새로** 보겠습니다이 변경은 란 모두에 대 한 몇 가지 기본적인 쿼리 예를 통해 검토 하 고 여기에서 얻을 수 누구나 어떻게 참조 데이터베이스를 만든 합니다.

관계형 데이터베이스에서 쿼리 처리 매우 복잡할 수 있으며 toolots 컴퓨터 과학, 수학 toounderstand hello 고유 설계 선택 및 동작을 일으킬 수 있습니다. 이 문서에서는 hello 콘텐츠 의도적으로 단순화 된 tooensure는 최소 기술 배경 지식이 있는 모든 사용자 수 hello 호환성 수준 변경이 미치는 hello 영향을 이해 하 고 응용 프로그램에 이점을 얻을 수 있습니다 어떻게 결정 했습니다.

Hello 호환성 수준을 130 hello 테이블에는 개요 죠.  [ALTER DATABASE 호환성 수준(Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)에서 자세한 내용을 볼 수 있지만, 여기에 간략한 요약을 제공합니다.

* hello Insert select 문의 삽입 작업 다중 스레드 수 또는 병렬 계획을 가질 수 있습니다 하지만 전에이 작업이 단일 스레드입니다.
* 메모리 액세스에 최적화된 테이블 및 테이블 변수 쿼리가, 이전에는 단일 스레드 작업이었지만, 이제 병렬 계획을 가질 수 있습니다.
* 메모리 액세스에 최적화된 테이블에 대한 통계를 이제 샘플링하고 자동으로 업데이트할 수 있습니다. 자세한 내용은 [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) (데이터베이스 엔진의 새로운 기능: 메모리 내 OLTP)를 참조하세요.
* 배치 모드 및 행 모드가 열 저장소 인덱스와 함께 변경됩니다.
  * 열 저장소 인덱스를 통한 테이블 정렬이 이제 배치 모드로 수행됩니다.
  * 기간 이동 집계가 이제 배치 모드(예: TSQL LAG/LEAD 문)로 진행됩니다.
  * 여러 개의 다른 절을 포함하는 열 저장소 테이블에 대한 쿼리가 배치 모드에서 수행됩니다.
  * 직렬 계획 또는 DOP=1 하에서 실행되는 쿼리도 배치 모드로 실행됩니다.
* 마지막으로, 호환성 수준이 120 되지만 그룹 정책 실행에 낮은 호환성 수준 (100 또는 110)에 대 한 카디널리티 추정 개선 실제로 들어오는, hello 이동 toocompatibility 수준 130 또한 나타납니다 이러한 향상 된이 기능 및 이러한 수도 있습니다. 응용 프로그램의 hello 쿼리 성능을 활용 합니다.

## <a name="practicing-compatibility-level-130"></a>호환성 수준 130 연습
첫 번째 살펴보겠습니다 일부 테이블, 인덱스 및 생성 된 난수 데이터 toopractice 이러한 새로운 기능 중 일부입니다. Azure SQL 데이터베이스 또는 SQL Server 2016 hello TSQL 스크립트 예제를 실행할 수 있습니다. 그러나 Azure SQL 데이터베이스를 만들 때 최소한 두 가지 다중 스레드 코어 tooallow hello 최소 P2 필요 하기 때문에 데이터베이스에서 선택 하 고 따라서 이러한 기능을 활용 있는지 확인 합니다.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


이제 호환성 수준 130으로 들어오는 hello 쿼리 처리 기능 모양 toosome 죠.

## <a name="parallel-insert"></a>병렬 삽입
Hello 호환성 수준 120 및 130, 다중 스레드 모델 (130) 및 단일 스레드 모델 (120)에서 각각 hello 삽입 작업을 실행 하는 삽입 작업을 실행 아래 hello TSQL 문을 실행 합니다.

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Hello hello 실제 쿼리 계획을 그래픽 표현 또는 해당 XML 콘텐츠를 요청 하 여 재생에 함수는 어떤 카디널리티 추정을 확인할 수 있습니다. 그림 1에 hello 계획-side-by-side를 살펴보면 130에서 120 tooparallel에서 직렬에서 전환 되는 열 저장소 삽입 실행 해당 hello를 명확 하 게 볼 수 있습니다. 실제로 병렬은 이제 반복기 실행 hello hello 팩트를 보여 주기 위해 두 개의 병렬 화살표를 표시 하는 hello 130 계획에 hello 반복기 아이콘의 hello 변경을 note 또한 합니다. 연결 된 toohello hello 데이터베이스에 있는 코어 수가 hello 병렬 실행 성능이 향상; INSERT 작업 toocomplete 큰 경우 100 배 이상 빠릅니다 tooa를 상황에 따라!

*그림 1: 호환성 수준이 130 직렬 tooparallel에서 변경 작업을 삽입 합니다.*

![그림 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>직렬 배치 모드
마찬가지로 데이터의 행을 처리할 때 toocompatibility 수준 130 이동 일괄 처리 모드를 사용 합니다. 첫째, 배치 모드 작업은 열 저장소 인덱스가 있어야만 가능합니다. 둘째, 일괄 처리 일반적으로 ~ 900 행을 나타내는 멀티 코어 CPU, 메모리 처리량에 대 한 액세스에 최적화 된 코드 논리를 사용 하 고 직접 활용 하 여 hello hello 가능 하면 Columnstore의 압축 된 데이터. 이러한 상황에서는 SQL Server 2016 처리할 수 ~ 900 행 한 번에 hello 시 1 개 행 대신 있으며이 인해 hello hello 작업의 전체적인 오버 헤드 비용 이제 공유 hello 전체 일괄 처리에 의해, hello 전체 행으로 비용을 감소. 이 공유 작업과 기본적으로 hello 열 저장소 압축 결합 양을 hello 대기 작업과 관련된 된 선택 일괄 처리 모드를 줄입니다. 모드에서 일괄 처리와 hello 열 저장소에 대 한 자세한 정보를 찾을 수 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)합니다.

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


아래 표시로 hello 쿼리 계획--함께 숫자 2 관찰 하 여 볼 수 있습니다 hello 처리 모드가 hello 호환성 수준으로 변경 하 고이 인해 두 호환성 수준에서 hello 쿼리 실행을 완전히 때 수 있다는 것을 알합니다 행 비교 모드 (86%) toohello 일괄 처리 모드 (14%)이 2 일괄 처리 된 대부분의 hello 처리 시간이 소비 됩니다. Hello 데이터 집합을 증가 hello 혜택 증가 합니다.

*그림 2: 호환성 수준 130 사용 하 여 직렬 toobatch 모드에서 변경 작업을 선택 합니다.*

![그림 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>배치 모드에서 정렬 실행
행 모드 (호환성 수준 120) toobatch 모드 (호환성 수준 130)에서 위의 비슷한 toohello 수 있지만, 적용 된 tooa 정렬 작업 hello 전환을 속도가 빨라집니다 hello hello hello에 대 한 정렬 작업의 몇 가지 이유로 합니다.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


표시-side-by-side 그림 3에, hello 정렬 작업이 행 모드에서의 비용, hello 일괄 처리 모드에만 hello 비용 (각각 81% 및 hello 정렬 자체에 56%)의 %19 나타냅니다 hello 81%를 나타내는 볼 수 있습니다.

*그림 3: 정렬 작업에서 행 toobatch 모드 호환성 수준 130으로 변경합니다.*

![그림 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

물론, 이러한 샘플만 포함 수만 개의 행을 되 고이 nothing 요즘 대부분의 SQL 서버에서 사용할 수 있는 hello 데이터를 볼 때. 방금 대신 수백만 행에 대해 이러한 프로젝트를 마우스 용 hello 특성 워크 로드의 보류 중인 매일 실행의 몇 분 정도에 나타날 수 있습니다.

## <a name="cardinality-estimation-ce-improvements"></a>카디널리티 예측(CE) 향상
SQL Server 2014에 도입 된, 모든 데이터베이스 호환성 수준 120 이상에서 실행 하면 새 카디널리티 추정 기능 hello 사용 합니다. 기본적으로, 카디널리티 추정 hello 논리가 사용 toodetermine SQL server는 예상된 비용을 기반으로 쿼리를 실행 하는 방법입니다. hello 추정 해당 쿼리에 관련 된 개체와 관련 된 통계의 입력을 사용 하 여 계산 됩니다. 실제로, 상위 수준에서 카디널리티 추정 기능은 hello 값, 고유 값 수의 분포 hello에 대 한 정보와 함께 행 수가 예상치와 중복 된 개수에 포함 된 hello 테이블과 hello 쿼리에서 참조 되는 개체입니다. 이러한 예상치를 잘못 된, 나타났다 toounnecessary 디스크 I/O tooinsufficient 메모리 부여 (예:: TempDB spill) 인해 발생할 수 있습니다 또는 tooa 선택 직렬 계획의 실행을 통해 병렬 계획 실행, tooname 몇 가지 있습니다. 결론을 잘못 된 예측 tooan 편이성 hello 쿼리 실행의 전반적인 성능이 저하 됩니다. Hello에 다른 쪽 보다 잘 예측 더 정확 하 게 예측, 잠재 고객 toobetter 쿼리 실행!

앞서 언급 했 듯이 쿼리 최적화와 예상치는 복잡 한 것 이지만 쿼리 계획 및 카디널리티 평가기에 대 한 자세한 toolearn 하려는 경우 toohello 문서에서 참조할 수 있습니다 [hello SQL Server 2014로 Your 쿼리 계획을 최적화 카디널리티 평가기](https://msdn.microsoft.com/library/dn673537.aspx) 심층 분석에 대 한 합니다.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>현재 어떤 카디널리티 예측을 사용하고 있습니까?
쿼리를 사용 중인 카디널리티 예측 해 보겠습니다 방금 hello 쿼리 사용 샘플 아래 toodetermine 합니다. 호환성 수준 110에서 암시 hello 이전 카디널리티 예측 함수의 hello 사용이 첫 번째 예제를 실행 하는 참고 합니다.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


실행이 완료 되 면 hello XML 링크를 클릭 하 고 아래와 같이 hello 첫 번째 반복기의 hello 속성을 보고 합니다. Hello 메모 속성 이름인 호출 CardinalityEstimationModelVersion 현재 70에 설정 됩니다. 데이터베이스 호환성 수준이 hello toohello SQL Server 7.0 버전 (설정 110으로 위의 hello TSQL 문을에 표시)을 설정 하지만 hello 값 70 단순히 hello 레거시 카디널리티 추정 기능 나타내는 SQL부터 사용할 수 있음 의미 하지 않습니다. 서버 7.0, SQL Server 2014 (와 함께 제공 되는 호환성 수준 120) 될 때까지 어느 주요 수정 버전이 없어야 합니다.

*그림 4: hello CardinalityEstimationModelVersion too70은 설정 하는 호환성 수준이 110 이하로 사용 하는 경우.*

![그림 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Hello 호환성 수준 too130 변경 하 고 LEGACY_CARDINALITY_ESTIMATION 설정으로 tooON hello를 사용 하 여 hello 새 카디널리티 예측 함수의 hello 사용을 비활성화할 수 또는 [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). 이 수 정확 하 게 hello 카디널리티 추정 함수의 관점에서 110을 사용 하 여 호환성 수준을 처리 하는 hello 최신 쿼리를 사용 하는 동안과 동일 합니다. 이렇게 hello 새 쿼리 처리 hello 최신 호환성 수준 (즉, 일괄 처리 모드)가 기능을 활용 하지만 필요한 경우 이전 카디널리티 추정 기능 hello 하면서 사용 수 있습니다.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Toohello 호환성 수준 120 또는 130을 이동 하기만 하면 hello 새 카디널리티 예측 기능을 사용 하도록 설정 합니다. 이 경우 CardinalityEstimationModelVersion hello 기본 설정 됩니다 적절 하 게 too120 또는 아래 보이지 130입니다.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*그림 5: hello CardinalityEstimationModelVersion too130은 설정 하는 호환성 수준이 130 사용 하는 경우.*

![그림 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Witnessing hello 카디널리티 추정 차이점
이제 확인해 보겠습니다 약간 더 복잡 일부 조건자를 사용 하는 WHERE 절로 INNER JOIN 관련 된 쿼리를 살펴 보겠습니다 hello 행 개수 예측이 hello 이전 카디널리티 추정 함수에서 먼저.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


이 쿼리를 효과적으로 실행 hello 이전 카디널리티 예측 기능을 사용 하 여 hello 행 예상 194,284 행을 주장 하는 동안 200,704 행 반환 됩니다. 물론, 전에 언급 한 것 처럼 이러한 행 개수 결과 다릅니다 얼마나 자주 실행 hello 이전 샘플 각 실행에서 반복 해 서 다시 hello 예제 테이블을 채우는. 물론, 쿼리에서 hello 조건자 hello 실제 추정 hello 테이블 모양, 데이터 콘텐츠 및 어떻게이 데이터 실제로 서로 상호 연결 하는 것 외에 영향이 제공 됩니다.

*그림 6: hello 행 개수 예측이 꺼져 194,284 또는 6000 행에서 예상 되는 hello 200,704 행 있습니다.*

![그림 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Hello에 동일한 방식으로 보겠습니다 이제 hello 같은 hello 새 카디널리티 추정 기능으로 쿼리를 실행 합니다.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Hello 아래를 살펴보면 이제 보면 해당 hello 행 예상 값 이며 202,877, 또는 훨씬 더 가깝기 때문 이전 카디널리티 추정 hello 보다 더 높은 됩니다.

*그림 7: hello 행 개수 예측이 이제 202,877 194,284 대신.*

![그림 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

실제로 hello 결과 집합은 200,704 행 (하지만 얼마나 자주 않은 쿼리를 실행할 hello hello의 이전 예제를 따라 해당 내용을 모두 않지만 무엇 보다도 TSQL hello hello rand () 문을 사용 하 여, 때문에 반환 하는 hello 실제 값 달라질 수 있습니다 하나 실행된 toohello에서 옆). 따라서이 특정 예제의 hello 새 카디널리티 추정 않으면 202,877 더 가깝습니다 too200, 704, 194,284 보다 이므로 hello 행 수를 예측에 더 효율적으로! Last, WHERE 절 조건자 tooequality hello를 변경 하는 경우 (보다는 ">" 예를 들어), hello 이전 및 새 카디널리티 함수 간의 hello 예측을 훨씬 더 서로 다르게 만들 수이 하, 일치 항목의 수에 따라 가져올 수 있습니다.

물론, 이 경우, 실제 카운트에서 최대 6000개의 행이 해제되면 상황에 따라서 많은 데이터를 나타내지 않습니다. 이제이 toomillions 행의 여러 테이블 및 더 복잡 한 쿼리를 통해 행과 열 및 hello 예상 시간에 수백만 개의 행을 날 수 있고 따라서 실행 계획 또는 메모리가 부족 하 여 요청 권한을 부여 앞에 오는 잘못 선택 하는 데 접속 hello의 위험을 hello tooTempDB spill 및 하므로 더 많은 I/O는 훨씬 더 높은입니다.

Hello 기회를 설정한 경우이 비교 가장 일반적인 쿼리 및 데이터 집합, 연습 및 얼마나 hello 이전 및 새 예측 중 일부에 영향을 일부만 될 수 오프 hello 현실에서 수를 늘리거나 일부는 다른 하는 것 동안 자신에 대 한 참조 자세히 toohello 실제 행 hello 결과 집합에 실제로 반환 된를 계산 합니다. 해당 내용을 모두 쿼리, hello Azure SQL 데이터베이스 특징, hello 특성 및 데이터 집합 및 hello 통계에 대 한 사용 가능한의 hello 크기의 hello 셰이프의 따라 달라 집니다. Azure SQL 데이터베이스 인스턴스, hello 쿼리 최적화 프로그램은 toobuild 방금 만든 지식을 다시 사용 통계 hello 이전 쿼리는 구성 대신 처음부터 실행 됩니다. 따라서 hello 예측은 매우 컨텍스트 및 거의 특정 tooevery 서버 및 응용 프로그램 상황 합니다. 에 중요 한 측면 tookeep입니다.

## <a name="some-considerations-tootake-into-account"></a>계정에 몇 가지 고려 사항 tootake
대부분의 작업은 프로덕션 환경에 대 한 호환성 수준을 hello를 채택 하기 전에 hello 호환성 수준 130에서에서 이익을 얻을, 3 옵션은 기본적으로 있습니다.

1. Toocompatibility 수준 130을 이동한 항목 성능을 확인 합니다. 일부 재발을 확인 하는 경우 하는 것 설정 hello 호환성 수준 뒤로 tooits 원래 수준 또는 130을 유지 하 고만 hello 카디널리티 추정 백 toohello 레거시 모드를 역방향 (위에서 설명한 대로이 단독 수 hello 문제 해결).
2. 미세 조정을 진행 중인 tooproduction 하기 전에 hello 성능 평가 비슷한 프로덕션 부하에서 기존 응용 프로그램을 철저히 테스트 합니다. 문제가 발생 하면 위와 동일한 항상 toohello 원래 호환성 수준으로 다시 이동 하거나 hello 카디널리티 추정 백 toohello 레거시 모드를 반대로 생각해 합니다.
3. 마지막 옵션 및 hello 가장 최근의 방식으로 tooaddress tooleverage hello 쿼리 저장소는 질문 이러한 있습니다. 이것이 현재 권장되는 옵션입니다. tooassist hello 분석 쿼리의 호환성 수준 120 또는 아래 130, 대 수 없습니다 좋습니다 toouse 쿼리 저장소 부족 합니다. 쿼리 저장소는 hello Azure SQL 데이터베이스 v 12의 최신 버전으로 사용할 수 있으며 기능은 toohelp 쿼리 성능 문제 해결을 있습니다. Hello 쿼리 저장소를 수집 하 고 모든 쿼리에 대 한 기록 세부 정보를 나타내는 데이터베이스에 대 한 항공 데이터 레코더 라고 생각 됩니다. 이 크게 hello 시간 toodiagnose를 줄임으로써 성능 법정 단순화 및 문제를 해결 합니다. 자세한 내용은 [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(쿼리 저장소: 데이터베이스에 대한 블랙박스)를 참조하세요.

Hello 이미 호환성 수준 120 이하로 실행 되는 데이터베이스 집합이 있고 toomove 계획 하는 경우 상위 수준에서 그 중 일부를 too130, 워크 로드 될 새 데이터베이스를 자동으로 프로 비전 곧 될 기본 too130 설정한, 하십시오 다음과 같이 hello:

* 프로덕션 환경에서 새로운 호환성 수준 toohello를 변경 하기 전에 쿼리 저장소를 사용 하도록 설정 합니다. 너무 참조할 수[hello 데이터베이스 호환성 모드와 사용 하 여 hello 쿼리 저장소를 변경](https://msdn.microsoft.com/library/bb895281.aspx) 자세한 정보에 대 한 합니다.
* 다음으로 대표 데이터 및 쿼리 프로덕션 환경과 유사한 환경 및 발생 하는 hello 성능을 비교 하 고 쿼리 저장소에서 보고를 사용 하 여 모든 중요 한 워크 로드를 테스트 합니다. 일부 회귀가 발생 하는 경우를 식별할 수 있습니다 쿼리 저장소 hello로 회귀 된 쿼리를 hello 및 hello 계획 쿼리 저장소에서 옵션을 사용 하 여 (고정 계획 aka). 이 경우 명확 hello 호환성 수준 130 그대로 적용 했으며 hello 쿼리 저장소에서 제시한 대로 hello 이전 쿼리 계획을 사용 합니다.
* 만으로도 마지막 수단으로 hello 호환성 수준 130에서 중요 한 toochanges 않는 tooleverage 새로운 기능 및 Azure SQL 데이터베이스 (SQL Server 2016을 실행 중임)의 기능을 사용할 경우 고려할 수 강제 다시 hello 호환성 수준 ALTER DATABASE 문을 사용 하 여 워크 로드에 맞는 toohello 수준입니다. 먼저, 수 있지만 130을 사용 하지 않는 기본적으로 남아 있는 경우 이전 SQL Server 버전의 hello 기능 수준에서 때문에 옵션 고정 hello 쿼리 저장소 계획은 가장 좋은 방법입니다.
* 여러 데이터베이스를 확장 하는 다중 테 넌 트 응용 프로그램의 경우 필요한 tooupdate hello; 모든 데이터베이스에서 사용자 데이터베이스 tooensure 일관 된 호환성 수준이의 논리를 프로 비전 수 있습니다. 이전 구문과 새로 프로 비전 된 것입니다. 응용 프로그램 워크 로드 성능에는 일부 데이터베이스는 서로 다른 호환성 수준에서 실행 되는 중요 한 toohello 팩트 될 수 있으며 따라서 모든 데이터베이스에서 호환성 수준 일관성 필요할 수 tooprovide hello 동일한 순서 tooyour 고객 hello 보드에서 모두 발생 합니다. Note는 필수적, 실제로 hello 호환성 수준에 따라 응용 프로그램의 적용 하는 방법에 따라 다릅니다.
* 마지막으로, hello 카디널리티 추정에 대 한 프로덕션 환경에서 계속 진행 하기 전에 hello 호환성 수준 변경이 마찬가지로 응용 프로그램에서 활용 하는 경우 tootest hello 새 조건 toodetermine에서 프로덕션 작업에 권장 hello 카디널리티 추정 개선 되었습니다.

## <a name="conclusion"></a>결론
Azure SQL 데이터베이스를 사용 하 여 모든 SQL Server 2016 향상 기능에서 toobenefit 명확 하 게 향상 시킬 수 있습니다 쿼리 실행 합니다. 얘기한 그대로 입니다. 물론, 새 기능과 마찬가지로 적절 한 평가 해야 toodetermine hello 조건은 정확 하 게 데이터베이스 작업 중인 hello 가장 잘 작동 합니다. 경험 대부분 작업 부하 예상된 tooat 이상 투명 하 게 실행 호환성 수준 130, 함수 및 새 카디널리티 예측을 처리 하는 새 쿼리를 활용 하면서 보여 줍니다. 적절 한 기한을 진행 하 고 다시 말하면 실제적으로, 몇 가지 예외는 항상 성실은 중요 한 평가 toodetermine 얼마나 이러한 향상 기능에서 얻을 수 있습니다. 이며이 작업을 수행 하에 큰 도움이 hello 쿼리 저장소를 다시 지정할 수 있습니다!

SQL Azure 진화 함에 따라 hello에 호환성 수준이 140 이후 기대할 수 있습니다. 적절한 시기가 되면, 현재 호환성 수준 130을 통해 가능해 지는 것들을 여기에서 간략하게 설명했듯이, 미래의 호환성 수준 140을 통해 가능해지는 것들에 관해 간략하게 설명할 예정입니다.

지금은 콘텐트가, 2016 년 6 월부터 Azure SQL 데이터베이스에서에서 변경 됩니다. hello 기본 호환성 수준 120 too130 새로 만든된 데이터베이스에 대 한 합니다. 잊지 마세요!

## <a name="references"></a>참조
* [데이터베이스 엔진의 새로운 기능](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [블로그: 쿼리 저장소: 데이터베이스에 대한 블랙박스, 작성자: Borko Novakovic, 2016년 6월 8일](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [ALTER DATABASE 호환성 수준(Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)
* [Azure SQL 데이터베이스 V12에 대한 호환성 수준 130](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [쿼리 계획을 여를 최적화 하 여 hello SQL Server 2014 카디널리티 평가기](https://msdn.microsoft.com/library/dn673537.aspx)
* [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)
* [블로그: Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능, 작성자: Alain Lissoir, 2016년 5월 6일](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
