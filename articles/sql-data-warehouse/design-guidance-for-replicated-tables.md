---
title: "복제 된 테이블-Azure SQL 데이터 웨어하우스에 대 한 aaaDesign 가이드 | Microsoft Docs"
description: "Azure SQL Data Warehouse 스키마로 복제 테이블을 디자인하기 위한 권장 사항입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse에서 복제 테이블 사용에 대한 디자인 지침
이 문서는 SQL Data Warehouse 스키마로 복제 테이블을 디자인하기 위한 권장 사항을 제공합니다. 이러한 권장 사항을 tooimprove 쿼리 성능을 사용 하 여 데이터 이동 및 쿼리 복잡성을 줄여 합니다.

> [!NOTE]
> hello 복제 테이블 기능은 현재 공개 미리 보기 중입니다. 일부 동작은 주체 toochange는.
> 

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 SQL Data Warehouse의 데이터 배포 및 데이터 이동 개념에 익숙하다고 가정합니다.  자세한 내용은 [분산 데이터](sql-data-warehouse-distributed-data.md)를 참조하세요. 

테이블 디자인의 일환으로, 데이터 및 hello 데이터를 쿼리 하는 방법에 대 한 가능한 한을 이해 합니다.  예를 들어 다음 질문을 고려합니다.

- 향 테이블인 hello?   
- Hello 테이블은 얼마나 자주 새로?   
- 데이터 웨어하우스에 팩트 및 차원 테이블이 있나요?   

## <a name="what-is-a-replicated-table"></a>복제 테이블이란?
복제 된 테이블에는 각 계산 노드가에 액세스할 수 있는 hello 테이블의 전체 복사본입니다. 테이블을 복제 하기 전에 조인 또는 집계를 계산 노드 간에 hello 필요 tootransfer 데이터를 제거 합니다. Hello 테이블에 복사본을 여러 개 있으므로 hello 테이블 크기는 2GB 미만 압축 하는 경우 복제 된 테이블 가장 효과적입니다.

hello 다음 다이어그램에서는 각 계산 노드에 액세스할 수 있는 복제 테이블 SQL 데이터 웨어하우스 hello 복제 된 테이블에는 각 계산 노드에 대해 배포 데이터베이스를 완벽 하 게 복사 tooa은. 

![복제 테이블](media/guidance-for-using-replicated-tables/replicated-table.png "복제 테이블")  

복제 테이블은 별모양 스키마의 작은 차원 테이블에 효과적입니다. 차원 테이블에는 일반적으로 불가능 toostore 있도록 크기의 개와 여러 복사본을 유지 관리 합니다. 차원에는 고객 이름 및 주소, 제품 세부 정보와 같이 느리게 변하는 설명 데이터가 저장됩니다. 느린 hello 데이터의 특성을 변경 하는 hello 안내 hello 복제 된 테이블의 toofewer 다시 작성 합니다. 

복제 테이블 사용을 고려하는 것이 좋은 경우:

- 디스크 hello 테이블 크기는 2GB 미만인, hello 행 개수에 관계 없이 합니다. 테이블의 toofind hello 크기 hello를 사용할 수 있습니다 [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) 명령: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`합니다. 
- hello 테이블 데이터를 이동 해야 하는 조인에 사용 됩니다. 예를 들어 해시 distributed 테이블에 대 한 조인을 hello 조인 열은 동일한 배포 열 hello 하지 하는 경우 데이터 이동이 필요 합니다. Hello 해시 distributed 테이블 중 하나의 값이 작으면 복제 된 테이블을 고려 합니다. 라운드 로빈 테이블에 조인하려면 데이터 이동이 필요합니다. 대부분의 경우 라운드 로빈 테이블 대신 복제 테이블을 사용하는 것이 좋습니다. 


복제 된 테이블 tooa distributed 기존 변환 하는 것이 좋습니다. 하면 테이블:

- 쿼리 계획을 사용 하 여 hello 데이터 tooall hello 계산 노드를 브로드캐스트하는 데이터 이동 작업. hello BroadcastMoveOperation 상당히 소모 되며 쿼리 성능이 느려집니다. 사용 하 여 쿼리 계획에서 데이터 이동 작업 tooview [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)합니다.
 
복제 된 테이블 hello 최고의 쿼리 성능을 얻을 수 없는 경우:

- hello 테이블에는 빈번한 삽입, 업데이트 및 삭제 작업입니다. 이러한 데이터 조작 언어 (DML) 작업 hello 복제 된 테이블의 다시 작성을 해야합니다. 다시 빌드가 빈번하면 성능을 저하시킬 수 있습니다.
- 데이터 웨어하우스 hello 자주 크기가 조정 됩니다. Hello 수가 계산 노드를 다시 발생 하는 변경 데이터 웨어하우스를 확장 합니다.
- hello 테이블에 많은 수의 열, 하지만 데이터 작업에는 일반적으로 적은 수의 열만 액세스 합니다. Hello 전체 테이블을 복제 하는 대신이 시나리오에서 보다 효과적인 toohash 수도 hello 테이블을 배포 하 고 다음 자주 액세스 하는 hello 열에 인덱스를 만듭니다. 필요한 경우에 쿼리 데이터 이동, SQL 데이터 웨어하우스만 hello에 대 한 이동 데이터 열을 요청 합니다. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>단순 쿼리 조건자로 복제 테이블 사용
Toodistribute 선택 하거나 테이블을 복제 하기 전에 hello 유형의 쿼리 toorun hello 테이블에 대 한 계획에 대해 생각 합니다. 가능하면,

- 같음 또는 같지 않음과 같은 단순 쿼리 조건자를 사용한 쿼리에는 복제 테이블을 사용합니다.
- LIKE 또는 NOT LIKE와 같은 복잡한 쿼리 조건자를 사용한 쿼리에는 분산 테이블을 사용합니다.

CPU 사용량이 많은 쿼리 hello 작업 모든 hello 계산 노드 배포 된 경우 가장 잘 수행 합니다. 예를 들어 테이블의 각 행에서 계산을 실행하는 쿼리는 복제 테이블에 비해 분산 테이블에서 성능이 더 높습니다. 복제 된 테이블, 각 계산 노드에 전체에 저장 되므로 모든 계산 노드에서 복제 된 테이블에 대 한 CPU 사용량이 많은 쿼리 hello 전체 테이블에 대해 실행 됩니다. hello 추가 계산 성능이 느려질 수 있습니다 쿼리 합니다.

예를 들어 이 쿼리에는 복잡한 조건자가 있습니다.  이 쿼리는 공급자가 복제 테이블이 아니라 분산 테이블일 때 실행 속도가 빨라집니다. 이 예제에서 공급자는 해시 분산 또는 라운드 로빈 분산 테이블일 수 있습니다.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>기존 라운드 로빈 테이블 tooreplicated 테이블 변환
라운드 로빈 테이블이 이미 있는 경우 권장 변환한 tooreplicated 테이블이이 문서에 설명 된 조건으로 충족 하는 경우. 복제 된 테이블 데이터 이동에 대 한 hello 필요 하지 않으므로 라운드 로빈 테이블에 대해 성능을 향상 시킬.  라운드 로빈 테이블은 조인을 위해 데이터 이동이 항상 필요합니다. 

이 예에서는 [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory 테이블 tooa 복제 된 테이블입니다. 이 예제는 DimSalesTerritory가 해시 분산이거나 라운드 로빈이거나 상관없이 작동합니다.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>라운드 로빈 대비 복제에 대한 쿼리 성능 예제 

복제 된 테이블 hello 전체 테이블은 각 계산 노드가 이미 있으므로 데이터 이동을 조인에 대 한 필요 하지 않습니다. Hello 차원 테이블은 라운드 로빈 배포, 조인 전체 tooeach 계산 노드에 hello 차원 테이블에 복사 합니다. toomove hello 데이터 hello 쿼리 계획 BroadcastMoveOperation 이라는 작업을 포함 합니다. 이런 유형의 데이터 이동 작업은 쿼리 성능을 저하시키며 복제 테이블을 사용하면 필요가 없어집니다. tooview 쿼리 계획 단계를 사용 하 여 hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) 시스템 카탈로그 뷰. 

예를 들어 hello AdventureWorks 스키마에 대해 다음 쿼리를 hello ` FactInternetSales` 테이블은 해시 분산 합니다. hello `DimDate` 및 `DimSalesTerritory` 테이블은 작은 차원 테이블입니다. 이 쿼리 북미 지역에 2004 회계 연도 대 한 hello 총 판매액을 반환합니다.
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
`DimDate` 및 `DimSalesTerritory`를 라운드 로빈 테이블로 다시 만들었습니다. 결과적으로, hello 쿼리는 여러 브로드캐스트 이동 작업에 쿼리 계획을 따르는 hello 없다고 표시 됩니다. 
 
![라운드 로빈 쿼리 계획](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

다시 생성 `DimDate` 및 `DimSalesTerritory` 로 복제 된 테이블을과 hello 쿼리를 다시 실행 합니다. hello 결과 쿼리 계획은 훨씬 더 짧은 하 고 있는 모든 브로드캐스트되지 이동 합니다.

![복제된 쿼리 계획](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>복제 테이블 수정에 대한 성능 고려 사항
SQL 데이터 웨어하우스 hello 테이블의 마스터 버전을 유지 하 여 복제 된 테이블을 구현 합니다. 각 계산 노드에 대해 hello 마스터 버전 tooone 배포 데이터베이스를 복사합니다. 변경 내용이 있을 때 SQL 데이터 웨어하우스는 먼저 hello 마스터 테이블을 업데이트 합니다. 각 계산 노드에 대해 hello 테이블 다시 빌드할이 필요합니다. Hello 테이블 tooeach 계산 노드를 복사 하 고 hello 인덱스 다시 작성 한 다음 복제 된 테이블 다시 빌드에 포함 되어 있습니다.

다시 빌드가 필요한 경우:
- 데이터가 로드되었거나 수정된 후
- hello 데이터 웨어하우스는 크기 조정 된 tooa 다른 DWU 설정
- 테이블 정의가 업데이트된 후

다시 빌드가 필요하지 않은 경우:
- 작업 일시 중지 후
- 작업 일시 다시 시작 후

데이터 수정 된 후에 즉시 hello 다시 발생 하지 않습니다. Hello rebuild 대신 트리거되는 hello 처음으로 쿼리는 hello 테이블에서 선택 합니다.  Hello 테이블에서 초기 select 문의 hello 단계 toorebuild hello에 대 한 복제 된 테이블은 수 있습니다.  Hello rebuild hello 쿼리 내에서 완료 되 면 hello 영향 toohello 초기 select 문의 hello 테이블의 hello 크기에 따라 중요 한 수. 있습니다  여러 복제 된 테이블에는 다시 작성 해야 하는 관련 된, 각 복사본 hello 문 내에서 단계로 순차적으로 빌드됩니다.  hello hello 다시 작성 하는 동안 데이터 일관성 toomaintain hello 테이블에서 사용 하는 배타적 잠금이 테이블을 복제 합니다.  hello 잠금 hello 다시 작성 hello 기간에 대 한 모든 액세스 toohello 테이블을 방지합니다. 

### <a name="use-indexes-conservatively"></a>신중하게 인덱스 사용
기본적인 인덱싱 tooreplicated 테이블을 적용합니다. SQL 데이터 웨어하우스 hello 다시 작성의 일부로 각 복제 테이블 인덱스를 다시 작성합니다. Hello 인덱스 다시 작성의 hello 비용을 능가 하는 hello 성능 향상에 도움이 되는 경우에 인덱스를 사용 합니다.  
 
### <a name="batch-data-loads"></a>일괄 처리 데이터 로드
복제 된 테이블에 데이터를 로드할 때 로드를 함께 일괄 처리 하 여 toominimize 다시 작성 하십시오. Select 문을 실행 하기 전에 모든 hello 일괄 처리 로드를 수행 합니다.

예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하고 4개의 다시 빌드를 호출합니다. 

- 원본 1에서 로드.
- Select 문이 다시 빌드 1을 호출.
- 원본 2에서 로드.
- Select 문이 다시 빌드 2를 호출.
- 원본 3에서 로드.
- Select 문이 다시 빌드 3을 호출.
- 원본 4에서 로드.
- Select 문이 다시 빌드 4를 호출.

예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하지만 다시 빌드를 1개만 호출합니다.

- 원본 1에서 로드.
- 원본 2에서 로드.
- 원본 3에서 로드.
- 원본 4에서 로드.
- Select 문이 다시 빌드를 호출.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>일괄 처리 로드 후 복제 테이블 다시 빌드
tooensure 일관성 있는 쿼리 실행 시간, 일괄 처리 로드 후 hello 복제 된 테이블의 새로 고침을 강제 적용 하면 두는 것이 좋습니다. 그렇지 않으면 첫 번째 쿼리에서 hello hello 인덱스 다시 작성을 포함 하는 hello 테이블 toorefresh 기다려야 합니다. Hello 크기 및 영향을 받는 복제 된 테이블의 수에 따라 hello 성능에 미치는 영향 중요할 수 있습니다.  

이 쿼리에서 hello를 사용 하 여 [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello 수정 되었지만 다시 작성 하지 않은 테이블을 복제 합니다.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce 다시 작성, hello 문 hello 출력 앞의 각 테이블에서 다음을 실행 합니다. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>다음 단계 
toocreate 복제 된 테이블을 사용 하 여 이러한 문 중 하나:

- [CREATE TABLE(Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT(Azure SQL Data Warehouse](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

분산 테이블에 대한 개요는 [분산 테이블](sql-data-warehouse-tables-distribute.md)을 참조하세요.



