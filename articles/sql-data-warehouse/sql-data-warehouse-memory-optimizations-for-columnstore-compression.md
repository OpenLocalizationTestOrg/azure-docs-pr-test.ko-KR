---
title: "Azure sql에서 aaaImprove columnstore 인덱스 성능 | Microsoft Docs"
description: "메모리 요구 사항을 줄이거나 각 행 그룹에 columnstore 인덱스를 압축 하는 행의 hello toomaximize hello 수를 사용 가능한 메모리를 늘리십시오."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>columnstore의 행 그룹 품질 최대화

행 그룹 품질 hello 행 그룹의 행 수가 결정 됩니다. 메모리 요구 사항을 줄이거나 각 행 그룹에 columnstore 인덱스를 압축 하는 행의 hello toomaximize hello 수를 사용 가능한 메모리를 늘리십시오.  Columnstore 인덱스에 대 한 이러한 방법 tooimprove 압축 비율과 쿼리 성능을 사용 합니다.

## <a name="why-hello-rowgroup-size-matters"></a>Hello 행 그룹 크기 중요 한 이유
개별 행 그룹의 열 세그먼트를 검색 하 여 한 테이블을 검색 하는 columnstore 인덱스, 하므로 쿼리 성능이 향상 hello 각 행 그룹의 행 수를 극대화 됩니다. 행 그룹이 많은 수의 행 데이터 압축으로, 디스크에서 작은 데이터 tooread 향상 됩니다.

행 그룹 에 대한 자세한 내용은 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.

## <a name="target-size-for-rowgroups"></a>행 그룹의 대상 크기
최고의 쿼리 성능을 위해 hello 목적은 toomaximize hello 수가 행 그룹당 최대 columnstore 인덱스의 행입니다. 행 그룹은 최대 1,048,576개의 행을 포함할 수 있습니다. 덮어쓰려면 toonot hello 최대 행 그룹당 최대 행 수가 있어야 합니다. Columnstore 인덱스는 행 그룹에 100,000개 이상의 행이 있을 때 적절한 성능을 달성합니다.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>압축 중에 행 그룹을 잘라낼 수 있음

대량 로드 또는 columnstore 인덱스 다시 작성 하는 동안 때로는 없는 각 행 그룹에 대해 지정 된 행을 hello 모두 만큼 충분 한 메모리 사용 가능한 toocompress 합니다. 메모리 압박이 있는 경우 columnstore 인덱스는 hello columnstore로 압축 성공할 수 있도록 hello 행 그룹 크기를 자릅니다. 

각 행 그룹에 메모리가 부족 하 여 toocompress 적어도 10, 000 행 되는 경우 SQL 데이터 웨어하우스 오류가 발생 합니다.

대량 로드에 대한 자세한 내용은 [클러스터형 columnstore 인덱스로 대량 로드](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)를 참조하세요.

## <a name="how-toomonitor-rowgroup-quality"></a>어떻게 toomonitor rowgroup 품질

Trimming가 있을 경우 잘라내기 rowgroup 및 hello 이유의 행 수 등 유용한 정보를 노출 하는 DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) 있습니다. 행 그룹 트리밍에 편리한 방법 tooquery로 보기를 수행 하는 hello이 DMV tooget 정보를 만들 수 있습니다.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

hello trim_reason_desc hello rowgroup 잘린 있는지 여부를 알려 줍니다 (trim_reason_desc = 잘리지 했습니다 및 행 그룹은 최적의 품질 NO_TRIM 함축). hello 트림 다음과 같은 이유로 다음과 같이 나타냅니다. hello 행 그룹의 중간 트리밍
- BULKLOAD: 트림이 이유는 hello 부하에 대 한 행의 들어오는 일괄 처리 hello 보다 작거나 1 백만 행이 때 사용 됩니다. hello 델타 저장소로 것과 반대로 tooinserting) (으로 삽입 되는 100, 000 행 보다 큰 있지만 집합 hello 트림 이유 tooBULKLOAD 경우 hello 엔진은 압축 된 행 그룹을 만듭니다. 이 시나리오에서는 더 많은 행에 일괄 처리 부하 창 tooaccumulate 증가 하는 것이 좋습니다. 또한 상태가 아닙니다 너무 세분화 행 그룹 파티션 경계에 걸쳐 있을 수 하 여 파티션 구성표 tooensure 다시 평가 합니다.
- MEMORY_LIMITATION: hello 엔진에 의해 toocreate 행 그룹 1 백만 행, 일정량의 작업 중인 메모리에 필요 합니다. 사용 가능한 메모리의 세션을 로드 하는 hello hello 작업 중인 메모리 필요한 것 보다 작은 경우 행 그룹 잘립니다 중간 가져옵니다. 다음 섹션 hello tooestimate 메모리 필요 하 고 더 많은 메모리를 할당 하는 방법을 설명 합니다.
- DICTIONARY_SIZE: 이 자르기 이유는 너비 및/또는 높이 값이 큰 카디널리티 문자열이 포함된 문자열 열이 하나 이상 있어서 행 그룹이 잘렸음을 나타냅니다. hello 사전 크기는 MB 메모리 및이 한도 도달 hello 행 그룹이 압축 된 제한 too16입니다. 이 경우를 실행 하는 않는 경우 hello 문제가 있는 열을 별도 테이블로 분리 하는 것이 좋습니다.

## <a name="how-tooestimate-memory-requirements"></a>어떻게 tooestimate 메모리 요구 사항

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

hello 필요한 메모리를 최대 toocompress 한 행 그룹은 대략

- 72MB +
- \#행 \* \#열 \* 8바이트 +
- \#행 \* \#short-string-columns \* 32바이트 +
- 압축 사전인 경우 \#long-string-columns \* 16MB

여기서 short-string-columns는 32바이트 이하의 문자열 데이터 형식을 사용하고 long-string-columns는 32바이트를 초과하는 문자열 데이터 형식을 사용합니다.

긴 문자열은 텍스트 압축용으로 고안된 압축 방법으로 압축됩니다. 이 압축 방법을 사용 하 여 한 *사전* toostore 텍스트 패턴입니다. hello 사전의 최대 크기는 16MB입니다. Hello 행 그룹의 각 긴 문자열 열에 대 한 사전이 하나만 있습니다.

columnstore 메모리 요구 사항에 대한 자세한 내용은 [Azure SQL Data Warehouse 확장: 구성 및 지침](https://myignite.microsoft.com/videos/14822) 비디오를 참조하세요.

## <a name="ways-tooreduce-memory-requirements"></a>같은 방법으로 tooreduce 메모리 요구 사항

Hello 기술을 tooreduce hello 메모리 요구 사항을 준수 rowgroup을 columnstore 인덱스에 압축 하는 데 사용 합니다.

### <a name="use-fewer-columns"></a>적은 수의 열 사용
가능 하면 열이 적은 hello 테이블을 디자인 합니다. Hello columnstore에 compressed 임을 hello columnstore 인덱스 각 열 세그먼트를 개별적으로 압축 합니다. 따라서 hello toocompress 행 그룹 hello 수 열 증가으로 증가 하는 메모리 요구 사항입니다.


### <a name="use-fewer-string-columns"></a>적은 수의 문자열 열 사용
문자열 데이터 형식의 열에는 숫자 및 날짜 데이터 형식보다 더 많은 메모리가 필요합니다. tooreduce 메모리 요구 사항을 팩트 테이블에서 문자열 열을 제거 하 고 더 작은 차원 테이블에 삽입 하는 것이 좋습니다.

문자열 압축을 위한 추가 메모리 요구 사항:

- Too32 문자를 문자열 데이터 형식 값 당 32 바이트의 추가 필요할 수 있습니다.
- 32자를 초과하는 문자열 데이터 형식은 사전 방법을 사용하여 압축됩니다.  Hello 행 그룹의 각 열은 tooan 추가 16MB toobuild hello 사전을 요구할 수 있습니다.

### <a name="avoid-over-partitioning"></a>오버 분할 방지

Columnstore 인덱스는 파티션당 행 그룹을 하나 이상 만듭니다. SQL 데이터 웨어하우스, 파티션 수가 hello hello 데이터를 배포 하 고 각 배포는 분할 되므로 신속 하 게를 증가 합니다. Hello 테이블에 너무 많은 분할 경우 있을 수 있습니다 하지 충분 한 행 toofill hello 행 그룹. 행의 hello 부족 압축 하는 동안 메모리 부족을 만들지 않습니다 되지만 hello columnstore 최고의 쿼리 성능의 얻을 toorowgroups 유발 합니다.

또 다른 이유 tooavoid 과도 하 게 분할은 분할된 된 테이블에서 columnstore 인덱스로 행을 로드 하는 오버 헤드를 메모리가입니다. 로드 하는 동안 파티션 수는 각 파티션에 충분 한 행 toobe 압축 될 때까지 메모리에 보관 되는 hello 들어오는 행을 받을 수 있습니다. 너무 많은 파티션이 있으면 메모리 부족이 발생합니다.

### <a name="simplify-hello-load-query"></a>쿼리를 로드 하는 hello를 간소화 합니다.

hello 데이터베이스에 대 한 모든 hello 연산자 hello 쿼리 간에 쿼리 메모리 부여 hello를 공유합니다. 쿼리 로드에 복잡 한 정렬 및 조인이 있는 경우 압축에 대해 사용할 수 있는 hello 메모리 감소 됩니다.

Hello 쿼리 로드에 대해서만 hello 부하 쿼리 toofocus를 디자인 합니다. Hello 데이터에 대 한 toorun 변형 해야 할 경우 실행할 쿼리를 로드 하는 hello와 별도로 합니다. 예를 들어 단계 hello 데이터 힙 테이블에 hello 변환을 실행 하 고 hello columnstore 인덱스로 테이블을 준비 하는 hello를 로드 합니다. 먼저 hello 데이터를 로드할 수도 있고 hello MPP 시스템 tootransform hello 데이터를 사용 하 여 합니다.

### <a name="adjust-maxdop"></a>MAXDOP 조정

각 배포 배포 당 사용 가능한 CPU 코어를 하나 이상 없을 경우 병렬로 hello columnstore에 행 그룹을 압축 합니다. hello parallelism toomemory 압력과 rowgroup 트리밍 될 수 있는 추가 메모리 리소스를 필요 합니다.

tooreduce 메모리가 중, 각 배포 내에서 직렬 모드로 hello MAXDOP 쿼리 힌트 tooforce hello 부하 작업 toorun를 사용할 수 있습니다.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>같은 방법으로 tooallocate 더 많은 메모리

DWU 크기와 hello 사용자 리소스 클래스 메모리 크기는 사용자 쿼리를 실행할 수를 결정 합니다. tooincrease hello 메모리 Dwu hello 수를 증가 하거나 hello 리소스 클래스를 높일 수 있습니다 쿼리 로드에 대 한 권한을 부여 합니다.

- tooincrease hello dwu로, 참조 [성능 확장 방법을?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- 쿼리의 경우 toochange hello 리소스 클래스 참조 [사용자 리소스 클래스 예제 변경](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)합니다.

예를 들어 DWU 100에 hello smallrc 리소스 클래스에서 사용자 צ ְ ײ 100MB 메모리의 각 배포에 대 한 합니다. Hello 세부 정보를 참조 하십시오. [SQL 데이터 웨어하우스의 동시성](sql-data-warehouse-develop-concurrency.md)합니다.

700MB 메모리 tooget 고품질 행 그룹 크기의 필요 하다 고 판단 가정 합니다. 이러한 예제 충분 한 메모리가 있는 hello 부하 쿼리를 실행 하는 방법을 보여 줍니다.

- DWU 1000 및 mediumrc를 사용하면 메모리 부여는 800MB입니다.
- DWU 600 및 largerc를 사용하면 메모리 부여는 800MB입니다.


## <a name="next-steps"></a>다음 단계

toofind hello를 참조 하는 방법으로 tooimprove 성능이 SQL 데이터 웨어하우스에 [성능 개요](sql-data-warehouse-overview-manage-user-queries.md)합니다.

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
