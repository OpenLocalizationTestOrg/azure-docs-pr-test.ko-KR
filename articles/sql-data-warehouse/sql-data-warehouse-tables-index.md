---
title: "SQL 데이터 웨어하우스에 aaaIndexing 테이블 | Microsoft Azure"
description: "Azure SQL 데이터 웨어하우스에서 테이블 인덱싱 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 테이블 인덱싱
> [!div class="op_single_selector"]
> * [개요][Overview]
> * [데이터 형식][Data Types]
> * [배포][Distribute]
> * [인덱스][Index]
> * [파티션][Partition]
> * [통계][Statistics]
> * [임시][Temporary]
> 
> 

SQL Data Warehouse는 [클러스터형 columnstore 인덱스][clustered columnstore indexes], [클러스터형 인덱스 및 비클러스터형 인덱스][clustered indexes and nonclustered indexes]를 비롯한 몇 가지 인덱싱 옵션을 제공합니다.  또한 [힙][heap]이라고도 하는 비인덱스 옵션도 제공합니다.  이 문서에서는 각 인덱스 유형에 hello 이점에 설명으로 toogetting hello 인덱스에서 대부분의 성능 팁입니다. 참조 [create 테이블 구문] [ create table syntax] 방법에 대 한 세부 toocreate SQL 데이터 웨어하우스의 테이블입니다.

## <a name="clustered-columnstore-indexes"></a>클러스터형 columnstore 인덱스
기본적으로 SQL 데이터 웨어하우스는 테이블에 대해 인덱스 옵션이 지정되지 않은 경우 클러스터형 columnstore 인덱스를 만듭니다. 클러스터형된 columnstore 테이블을 모두 hello 가장 높은 수준으로 데이터 압축 hello 전반적으로 최적의 쿼리 성능을 제공합니다.  클러스터형된 columnstore 테이블에 클러스터형된 인덱스나 힙 테이블을 보다 성능이 뛰어나지만 일반적으로 및 대형 테이블에 대 한 hello 최선의 선택은 일반적으로 합니다.  이러한 이유로, 클러스터형된 columnstore는 가장 좋은 장소 toostart hello 방법을 모를 때 tooindex 테이블입니다.  

클러스터형된 columnstore 테이블 toocreate hello WITH 절에서 클러스터형 COLUMNSTORE 인덱스를 지정 하거나 hello WITH 절을 생략할 하기만 하면:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

다음과 같은 일부 시나리오에서는 클러스터형 columnstore를 사용하는 것이 적합하지 않을 수 있습니다.

* Columnstore 테이블이 varchar(max), nvarchar(max) 및 varbinary(max)를 지원하지 않습니다.  대신 힙 또는 클러스터형 인덱스를 고려합니다.
* Columnstore 테이블이 임시 데이터에 대해 덜 효율적일 수 있습니다.  힙 및 임시 테이블을 고려합니다.
* 1억개 미만의 행이 있는 작은 테이블.  힙 테이블을 고려합니다.

## <a name="heap-tables"></a>힙 테이블
일시적으로 SQL 데이터 웨어하우스에 대 한 데이터는 방문는 힙 테이블을 사용 하면 전체 프로세스를 더 빠르게 hello 알 수 있습니다.  즉 로드 tooheaps 보다 더 빠른 tooindex 테이블 및 일부 경우 hello 후속 읽기 캐시에서 수행 될 수 있습니다.  로드 하는 경우 데이터만 toostage hello 테이블 tooheap 테이블을 로드 하는 많은 변형을 실행 하기 전에 됩니다 hello 데이터 tooa 로드 보다 훨씬 빠르게 클러스터형 columnstore 테이블. 또한 데이터 tooa 로드 [임시 테이블] [ Temporary] 테이블 toopermanent 저장소를 로드할 때 보다 훨씬 빠르게 로드 됩니다.  

1억개 행 미만을 포함하는 작은 조회 테이블의 경우 힙 테이블을 사용하는 것이 더 나은 경우도 많습니다.  클러스터 columnstore 테이블 100 백만 개 이상의 행 되 면 tooachieve 최적의 압축을 시작 합니다.

toocreate 힙 테이블을 힙 hello WITH 절에 지정:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>클러스터형 및 비클러스터형 인덱스
클러스터형된 인덱스는 단일 행 toobe 신속 하 게 검색 해야 할 때 클러스터 된 columnstore 테이블 보다 성능이 뛰어나지만 수 있습니다.  여기서는 단일 또는 매우 적고 행 조회는 극단적인 속도와 필요한 tooperformance 쿼리에 대 한 클러스터 인덱스 또는 비클러스터형 보조 인덱스를 고려 합니다.  hello 단점은 toousing 클러스터형된 인덱스는 hello 클러스터형된 인덱스 열에서 매우 선택적인 필터를 사용 하는 쿼리만 이점을 얻을 수입니다.  비클러스터형 인덱스 수는 다른 열에 대 한 tooimprove 필터 tooother 열을 추가 했습니다.  그러나 tooa 테이블 추가 된 각 인덱스 공간과 처리 시간 tooloads 모두 추가 합니다.

단순히 toocreate 클러스터형된 인덱스 테이블을 hello WITH 절에서 클러스터형 인덱스를 지정 합니다.

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd에 테이블의 비클러스터형 인덱스 구문 다음 hello를 사용 하면 됩니다.

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>클러스터형 columnstore 인덱스 최적화
클러스터형 columnstore 테이블은 데이터가 세그먼트로 구성됩니다.  Columnstore 테이블에 중요 한 tooachieving 최적의 쿼리 성능을 높은 세그먼트 양질의입니다.  세그먼트 품질 hello 압축 된 행 그룹의 행 수로 측정할 수 있습니다.  세그먼트 품질은 적어도 100k 압축 된 행 마다 행 그룹 및 hello 처리당 행 수가 행 그룹 접근 방식 1048576 행, 즉 hello 행 그룹에 포함 될 수 있습니다 대부분의 행으로 성능을 얻을 수 있는 최적의입니다.

보기 아래의 hello를 작성 및 사용 되는 시스템 toocompute hello에서 행 마다 평균 행 그룹 및 모든 최적 클러스터 columnstore 인덱스를 식별 합니다.  이 뷰의 마지막 열 hello 인덱스 toorebuild 사용된 될 수 있는 SQL 문으로 생성 됩니다.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Hello 뷰를 만든 했으므로이으로 쿼리를 실행 tooidentify 테이블 행 그룹에 100, 000 행 미만입니다.  물론, 자세한 최적의 세그먼트 품질에 대 한 원하는 경우 100, 000의 tooincrease hello 임계값을 할 수 있습니다. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Hello 쿼리를 실행 한 toolook hello 데이터에서 시작 하 고 결과 분석할 수 있습니다. 이 표에서 행 그룹 분석에 대 한 어떤 toolook를 설명합니다.

| 열 | 어떻게 toouse이이 데이터 |
| --- | --- |
| [table_partition_count] |Hello 테이블이 분할 되어 있다면 toosee 높은 열린 행 그룹 수를 기대할 수 있습니다. Hello 배포의 각 파티션에 이론적에서 가지기 관련 된 열린 행 그룹. 분석할 때 이 점을 고려해야 합니다. 작은 테이블을 파티션으로 분할 되어이 압축을 향상 시킬 때 모두를 분할 하는 hello를 제거 하 여 최적화할 수 있습니다. |
| [row_count_total] |Hello 테이블에 대 한 총 행 수입니다. 예를 들어 hello 압축 상태에이 값 toocalculate 비율의 행을 사용할 수 있습니다. |
| [row_count_per_distribution_MAX] |모든 행 균등 하 게 분산 하는 경우이 값은 hello 대상 수가 배포 당 행 수입니다. 이 값 hello compressed_rowgroup_count과 비교 합니다. |
| [COMPRESSED_rowgroup_rows] |Columnstore 형식 hello 테이블에 대 한 행의 총 수입니다. |
| [COMPRESSED_rowgroup_rows_AVG] |Hello 평균 행 수의 행 그룹에 대 한 행 보다 작은 hello 최대 # 크게 이면 CTAS에는 사용을 고려 합니다 또는 ALTER INDEX REBUILD toorecompress hello 데이터 |
| [COMPRESSED_rowgroup_count] |columnstore 형식인 행 그룹의 수. 이 숫자는 관계 toohello 테이블에서 높은 경우 hello columnstore 밀도 낮은 표시기입니다. |
| [COMPRESSED_rowgroup_rows_DELETED] |행이 columnstore 형식으로 논리적으로 삭제됩니다. Hello 번호가 높은 상대 tootable 크기 이면 hello 파티션을 다시 만드는 것이 물리적으로 제거 하는 대로 hello 인덱스를 다시 작성 하십시오. |
| [COMPRESSED_rowgroup_rows_MIN] |Hello 평균 및 최대 열 toounderstand hello 값의 범위와 함께에서이 프로그램 columnstore에서 hello 행 그룹에 대 한 사용 합니다. Hello 로드 임계값 (파티션 정렬 분포 102400)를 통해 적은 수 최적화는 hello 데이터 로드에서 사용할 수 있는 제안 |
| [COMPRESSED_rowgroup_rows_MAX] |위와 동일합니다. |
| [OPEN_rowgroup_count] |열려 있는 행 그룹은 정상입니다. 테이블 분산당(60) 행 그룹이 하나 열려 있다고 예상하는 것이 합리적일 것입니다. 이 숫자가 과도하게 높으면 여러 파티션에 데이터를 로드한다는 뜻입니다. 분할 전략 toomake 사운드 인지 확인 hello |
| [OPEN_rowgroup_rows] |각 행 그룹은 최대 1,048,576개 행을 포함할 수 있습니다. 이 값 toosee 채워진 정도 사용 하 여 hello 열린 행 그룹은 현재 |
| [OPEN_rowgroup_rows_MIN] |그룹을 엽니다. 데이터가 유출 되는이 행 그룹으로 나머지 행에 대해 이전 로드 하는 hello 또는 hello 테이블에 로드 trickle 되 고 임을 나타냅니다. 사용 하 여 hello MIN, MAX, AVG 열 toosee 열린 행 그룹에 데이터의 양을 채도 됩니다. 작은 테이블에 대 한 모든 hello 데이터의 100% 수 있습니다! 이 경우 ALTER INDEX REBUILD tooforce 데이터 toocolumnstore를 hello 합니다. |
| [OPEN_rowgroup_rows_MAX] |위와 동일합니다. |
| [OPEN_rowgroup_rows_AVG] |위와 동일합니다. |
| [CLOSED_rowgroup_rows] |온전성 검사 방법으로 hello 닫힌 행 그룹 행을 확인 합니다. |
| [CLOSED_rowgroup_count] |닫힌된 행 그룹이 hello 수는 전혀 표시 되는 낮은 수 있습니다. 닫힌된 행 그룹이 hello ALTER INDEX를 사용 하 여 변환 된 toocompressed rowg roups 될 수 있습니다... REORGANISE 명령을 사용하여 닫힌 행 그룹을 압축된 행 그룹으로 변환할 수 있습니다. 그러나 일반적으로는 이 작업이 필요하지 않습니다. 닫힌된 그룹은 hello 배경 "tuple mover" 프로세스에 의해 자동으로 변환 된 toocolumnstore 행 그룹. |
| [CLOSED_rowgroup_rows_MIN] |닫힌 행 그룹의 채우기 속도가 매우 높아야 합니다. 닫힌된 행 그룹에 대 한 채우기 비율 hello 낮으면 hello columnstore의 추가 분석이 필요 합니다. |
| [CLOSED_rowgroup_rows_MAX] |위와 동일합니다. |
| [CLOSED_rowgroup_rows_AVG] |위와 동일합니다. |
| [Rebuild_Index_SQL] |테이블에 대 한 SQL toorebuild columnstore 인덱스 |

## <a name="causes-of-poor-columnstore-index-quality"></a>columnstore 인덱스 품질 저하의 원인
불량 세그먼트 품질을 테이블을 식별 하면 tooidentify hello 근본 원인을 싶을 것입니다.  다음은 세그먼트 품질 저하의 일반적인 몇 가지 원인입니다.

1. 인덱스를 작성했을 때 메모리 부족
2. 많은 양의 DML 작업
3. 작거나 지속적인 로드 작업
4. 너무 많은 파티션

이러한 요소 지정 하면 columnstore 인덱스 toohave 크게 행 그룹당 1 백만 행 최적의 hello 보다 작은.  압축 된 행 그룹 대신 행 toogo toohello 델타 행 그룹을 일으킬 수도 있습니다. 

### <a name="memory-pressure-when-index-was-built"></a>인덱스를 작성했을 때 메모리 부족
hello 행의 직접적인 관련된은 toohello 너비가 하 고 사용 가능한 tooprocess hello 행 그룹 메모리 양을 hello 하는 행 압축 된 행 그룹당 hello 수입니다.  행의 메모리 사용량이 toocolumnstore 테이블 기록 되 고, columnstore 세그먼트 품질이 저하 될 수 있습니다.  따라서 hello 최상의 방법 tooyour columnstore 인덱스 테이블 액세스 tooas 최대한 많은 메모리를 작성 하는 toogive hello 세션입니다.  메모리 할당 DWU hello 양의 사용자 테이블의 각 행에 hello 데이터에 따라 tooyour 시스템을 할당 했는지 및 동시성 hello 양을 슬롯이 있습니다 오른쪽 hello에 대 한 hello 지침 toohello를 제공할 수 메모리와 동시성 기능 손실을 절충 이므로 데이터 tooyour 테이블을 작성 하는 세션입니다.  모범 사례로, DW1000를 사용 하는 이상 DW400 tooDW600 및 mediumrc를 사용 중인 경우 명 largerc 이하의 xlargerc DW300를 사용 하는 경우로 시작 하는 것이 좋습니다.

### <a name="high-volume-of-dml-operations"></a>많은 양의 DML 작업
업데이트 하 고 행을 삭제 하는 DML 작업에서 대량의 hello columnstore에 비효율성을 제공할 수 있습니다. Hello 대부분 행 그룹의 hello 행의 수정 된 경우 특히 유용 합니다.

* 삭제 된 것으로 hello 행을 표시만 논리적으로 압축 된 행 그룹에서 행을 삭제 합니다. hello 행 hello 파티션 또는 테이블 다시 빌드될 때까지 hello 압축 된 행 그룹에 남아 있습니다.
* 델타 행 그룹 이라고 하는 hello 행 tootooan 내부 rowstore 테이블에 추가 행을 삽입 합니다. hello 삽입 행 hello 델타 행 그룹 꽉 찼으며 된 것으로 전에 변환 된 toocolumnstore 되지 않습니다. 행 그룹 hello 1048576 행의 최대 용량에 도달 닫힙니다. 
* Columnstore 형식에서 행을 업데이트하면 논리적 삭제 후 삽입으로 처리됩니다. hello 삽입 행 hello 델타 저장소에 저장할 수 있습니다.

일괄 처리 업데이트 하 고 파티션 정렬 된 배포 toohello columnstore 서식을 지정 하는 직접 쓰여질 행 수가 102, 400 hello 대량 임계값을 초과 하는 작업을 삽입 합니다. 그러나는 균등 한 분포가 라고 가정할 경우 해야 toobe 6.144 백만 개 이상의 행이이 toooccur에 대 한 단일 작업을 수정 합니다. Hello 지정 된 파티션의 행 수 분포를 정렬 하는 경우는 102400 미만 hello 행 toohello 델타 저장소 이동 하 고 계속 유지 됩니다 때까지 충분 한 행을 삽입 또는 수정 된 tooclose hello 행 그룹 또는 hello 인덱스 다시 작성 되었습니다.

### <a name="small-or-trickle-load-operations"></a>작거나 지속적인 로드 작업
SQL 데이터 웨어하우스로 유입되는 작은 부하는 지속적인 부하라고도 합니다. 일반적으로 데이터 수집 되 고 된 hello 시스템에 의해 거의 상수 스트림을 나타냅니다. 그러나 근처의이 스트림은 행의 볼륨 연속 hello 특히 크지 않습니다. 대개 hello 데이터를 직접 로드 toocolumnstore 형식에 필요한 hello 임계값 보다 훨씬 큽니다.

이러한 상황에서는 종종 더 나은 tooland hello 데이터 먼저 Azure blob 저장소에 사용 되며 이전 tooloading를 누적 하도록 합니다. 이 기술을 *마이크로 일괄 처리*라고 합니다.

### <a name="too-many-partitions"></a>너무 많은 파티션
또 다른 사항은 tooconsider 클러스터형된 columnstore 테이블에서 분할의 hello 영향입니다.  분할 전에 미리 SQL 데이터 웨어하우스는 데이터를 60개의 데이터베이스로 나눕니다.  분할을 수행하면 데이터가 좀 더 세분화됩니다.  데이터를 분할할 경우 tooconsider 원하는 **각** 파티션은 클러스터형된 columnstore 인덱스에서 toohave 적어도 1 백만 행 toobenefit를 필요로 합니다.  테이블 파티션 수가 100 개라도 분할할 경우 테이블에 클러스터형된 columnstore 인덱스에서 행 toobenefit toohave 6 십억 이상 필요 합니다 (60 분포 * 파티션 수가 100 개라도 * 1 백만 행). 100 파티션 테이블 6 십억 행이 없는 경우 hello 파티션 수를 줄이거나 힙 테이블을 대신 사용 하는 것이 좋습니다.

테이블 데이터 로드 한 후, 단계 tooidentify 아래 hello 따르고 최적 클러스터 columnstore 인덱스가 있는 테이블을 다시 작성 합니다.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Tooimprove 세그먼트 품질 인덱스를 다시 작성
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>1 단계: 식별 하거나 hello 오른쪽 리소스 클래스를 사용 하는 사용자 만들기
빠르게 tooimmediately 세그먼트 품질을 향상 시킬는 toorebuild hello 인덱스입니다.  hello SQL 보기 위에 hello에서 반환 되는 ALTER INDEX REBUILD 문을 사용 하는 toorebuild 될 수 있는 인덱스를 반환 합니다.  인덱스를 다시 작성할 때 인덱스를 다시 빌드할 수 있는 충분 한 메모리 내 toohello 세션을 할당 해야 합니다.  toodo 권한을 toorebuild hello에 인덱스가이 테이블 toohello 권장 되는 최소 사용자의이, 증가 hello 리소스 클래스입니다.  먼저 toodo를 필요 hello 시스템에 사용자를 만들지 않은 경우 hello 데이터베이스 소유자 사용자의 hello 리소스 클래스를 변경할 수 없습니다.  hello 최소값 권장은 xlargerc DW300를 사용 하는 경우 이하의 largerc DW1000를 사용 하는 이상 DW400 tooDW600 및 mediumrc를 사용 중인 경우입니다.

다음 방법의 예로 tooallocate 클래스에 따라 리소스를 늘려 더 많은 메모리 tooa 사용자입니다.  리소스 클래스 이며 어떻게 toocreate 새 사용자 수에 hello에 대 한 자세한 내용은 [동시성 및 작업 관리] [ Concurrency] 문서.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>2단계: 더 높은 리소스 클래스 사용자를 사용하여 클러스터형 columnstore 인덱스 다시 작성
사용자로 로그온 hello 1 단계에서 (예: LoadUser)는 더 높은 리소스 클래스를 사용 하 여 되 고 hello ALTER INDEX 문을 실행 합니다.  이 사용자가 ALTER 사용 권한 toohello 표 hello 인덱스 다시 작성 될 위치에 있어야 합니다.  이러한 예와 toorebuild hello 전체 columnstore 인덱스는 방법 또는 자동 저장 방식 toorebuild 단일 분할 합니다. 대형 테이블에는 한 번에 하나의 파티션 더 실용적 toorebuild 인덱스

또는 hello 인덱스를 다시 작성 하는 대신 복사 하면 hello tooa 새 테이블 사용 하 여 테이블 [CTAS][CTAS]합니다.  어떤 방식이 적합할까요? 데이터 양이 많은 경우 일반적으로 [CTAS][CTAS]가 [ALTER INDEX][ALTER INDEX]보다 빠릅니다. 데이터를 더 작은 볼륨에 대 한 [ALTER INDEX] [ ALTER INDEX] 쉽게 toouse 이며 hello 테이블 아웃 tooswap 필요 하지 않습니다.  참조 **CTAS 및 파티션 전환을 사용 하 여 인덱스를 다시 작성** 아래 toorebuild CTAS에는 사용 하 여 인덱스 하는 방법에 대 한 자세한 내용은 합니다.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

SQL 데이터 웨어하우스에서 인덱스를 다시 작성하는 작업은 오프라인 작업입니다.  인덱스 다시 작성 하는 방법에 대 한 자세한 내용은 hello ALTER INDEX REBUILD 섹션을 참조 하십시오. [Columnstore 인덱스 조각 모음] [ Columnstore Indexes Defragmentation] 및 hello 구문 항목 [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>3단계: 클러스터형 columnstore 세그먼트 품질이 향상되었는지 확인
Poor로 테이블을 식별 하는 hello 쿼리를 다시 실행 품질을 분할 하 고 세그먼트 품질이 향상 않은 확인 합니다.  세그먼트 품질이 개선 되지 않았습니다 hello 행 테이블에는 매우 굵게 수 있습니다.  인덱스를 다시 작성할 때 더 높은 리소스 클래스 또는 DWU를 사용하는 것이 좋습니다.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>CTAS 및 파티션 전환을 사용하여 인덱스 다시 빌드
이 예에서는 [CTAS에] [ CTAS] 및 파티션 toorebuild 테이블 파티션을 전환 합니다. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

사용 하 여 파티션을 다시 작성에 대 한 자세한 내용은 `CTAS`, hello 참조 [파티션] [ Partition] 문서.

## <a name="next-steps"></a>다음 단계
toolearn에 hello 문서를 더 참조 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블배포] [ Distribute], [테이블 분할][Partition], [테이블 통계를 유지 관리] [ Statistics] 및 [ 임시 테이블][Temporary]합니다.  모범 사례에 대해 자세히 toolearn 참조 [SQL 데이터 웨어하우스 모범 사례][SQL Data Warehouse Best Practices]합니다.

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
