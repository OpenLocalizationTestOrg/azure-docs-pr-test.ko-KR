---
title: "aaaManage 계산 능력이 Azure SQL 데이터 웨어하우스에 (개요) | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스의 성능 확장 기능입니다. Dwu로 조정 하 여 수평 확장 또는 일시 중지 하 고 계산 리소스 toosave 비용이 다시 시작 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Azure SQL 데이터 웨어하우스의 계산 능력 관리(개요)
> [!div class="op_single_selector"]
> * [개요](sql-data-warehouse-manage-compute-overview.md)
> * [포털](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST (영문)](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

SQL 데이터 웨어하우스의 hello 아키텍처는 저장소 및 계산의 경우, 각 tooscale를 독립적으로 허용 구분 합니다. 따라서 계산 크기 조정 된 toomeet 성능 요구가 hello 양의 데이터와 무관 수 있습니다. 이 아키텍처의 자연스러운 결과는 계산 및 저장소에 대한 [청구][billed]가 분리되어 있다는 것입니다. 

이 개요에서는 설명 작동 하는 SQL 데이터 웨어하우스 및 일시 중지, 다시 시작할 때 및 SQL 데이터 웨어하우스의 확장 기능 tooutilize hello 하는 방법을 어떻게 확장 합니다. Hello 참조 [데이터 웨어하우스 단위 (Dwu)] [ data warehouse units (DWUs)] 페이지 toolearn Dwu와 성능 관계입니다. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>SQL Data Warehouse에서 계산 관리 작업이 작동하는 방법
SQL 데이터 웨어하우스에 대 한 hello 아키텍처 제어 노드로, 노드 및 hello 저장소 계층 60 분포에 분산을 계산 합니다. 

SQL 데이터 웨어하우스에 일반 활성 세션 중에 시스템의 헤드 노드 hello 메타 데이터를 관리 하 고 hello 분산 쿼리 최적화 프로그램을 포함 합니다. 이 헤드 노드 아래에는 계산 노드와 저장소 계층이 있습니다. DWU 400의 경우 시스템에 헤드 노드, 4 개의 계산 노드 및 hello 저장소 계층에서 60 배포로 구성 된 하나의 합니다. 

소수 자릿수를 진행 하거나 작업을 일시 중지 hello 시스템 먼저 모든 수신 쿼리를 중지 및 롤백됩니다 트랜잭션을 tooensure 일관 된 상태입니다. 크기 조정 작업의 경우 이 트랜잭션 롤백을 완료한 후에만 크기 조정이 수행됩니다. 스케일 업 작업에 대 한 hello 시스템 규정 extra 원하는 계산 노드 수를 hello 하 고 hello 계산 노드 toohello 저장소 계층을 다시 연결을 시작 합니다. 축소 작업에 대 한 hello 불필요 한 노드 해제 되 고 나머지 계산 노드 hello 다시 toohello 적절 한 개수의 배포 첨부 합니다. 일시 중지 작업에 대 한 모든 계산 노드 해제 되 고 시스템 다양 한 메타 데이터 작업 tooleave 안정 된 상태가 최종 시스템 될 예정입니다.

| DWU  | 계산 노드 수 \# | 노드당 배포 수 \# |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

hello 계산을 관리 하기 위한 세 가지 주요 기능은 다음과 같습니다.

1. 일시 중지
2. 다시 시작
3. 확장

이러한 각 작업 몇 분 toocomplete를 걸릴 수 있습니다. 자동 크기 조정/일시 중지/재개 됩니다 tooimplement 논리 tooensure 특정 작업이 다른 작업을 진행 하기 전에 완료 된 수도 있습니다. 

다양 한 끝점을 통해 hello 데이터베이스 상태를 확인 하는 중 이러한 작업의 구현 자동화 toocorrectly 허용 됩니다. hello 포털은는 작업과 hello 데이터베이스 현재 상태가 완료 될 때 알림을 제공 되었지만 상태를 프로그래밍 방식으로 검사에 대 한 허용 하지 않습니다. 

>  [!NOTE]
>
>  모든 끝점에 대한 계산 관리 기능은 존재하지 않습니다.
>
>  

|              | 일시 중지/다시 시작 | 확장 | 데이터베이스 상태 확인 |
| ------------ | ------------ | ----- | -------------------- |
| Azure 포털 | 예          | 예   | **아니요**               |
| PowerShell   | 예          | 예   | 예                  |
| REST API     | 예          | 예   | 예                  |
| T-SQL        | **아니요**       | 예   | 예                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>계산 조정

SQL Data Warehouse의 성능은 CPU, 메모리 및 I/O 대역폭과 같은 계산 리소스를 추상화한 측정값인 [DWU(데이터 웨어하우스 단위)][data warehouse units (DWUs)]로 측정됩니다. 시스템 성능 tooscale 하려는 사용자는 이렇게 하려면 다양 한 방법을 통해와 같은 hello 포털과 T-SQL, REST Api를 통해 합니다. 

### <a name="how-do-i-scale-compute"></a>계산 크기는 어떻게 조정합니까?
전원 관리 되 SQL 데이터 웨어하우스 hello DWU 설정을 변경 하 여 계산 해야 합니다. 특정 작업에 대해 DWU를 더 많이 추가하면 성능이 [선형적으로][linearly] 향상됩니다.  시스템을 강화하거나 축소할 때 성능이 눈에 띄게 변경되는 DWU 제품을 제공합니다. 

Dwu tooadjust 개별 이러한 방법 중 하나를 사용할 수 있습니다.

* [Azure Portal을 사용하여 계산 능력 조정][Scale compute power with Azure portal]
* [PowerShell을 사용하여 계산 능력 조정][Scale compute power with PowerShell]
* [REST API를 사용하여 계산 능력 조정][Scale compute power with REST APIs]
* [TSQL을 사용하여 계산 능력 조정][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>얼마나 많은 DWU를 사용해야 합니까?

toounderstand 어떤 사용자가 이상적인 DWU 값은 위와 아래로 확장 하 고 데이터를 로드 한 후 몇 가지 쿼리를 실행 해 보십시오. 크기 조정이 빠르기 때문에 1시간 이내에 다양한 성능 수준을 시험해 볼 수 있습니다. 

> [!Note] 
> SQL 데이터 웨어하우스는 많은 양의 데이터를 설계 된 tooprocess 합니다. toosee 특히 큰 Dwu에서 크기 조정에 대 한 실제 성능이 원하는 toouse에 도달 하거나 1TB를 초과 하는 큰 데이터 집합입니다.

찾기에 대 한 권장 작업에 대 한 최상의 DWU hello:

1. 개발 중인 데이터 웨어하우스의 경우 먼저 낮은 DWU 성능 수준을 선택합니다.  적합한 시작 지점은 DW400 또는 DW200입니다.
2. 응용 프로그램 성능 모니터링, 관찰 하기 toohello 성능 비교 hello 수가 선택한 Dwu 관찰 합니다.
3. 결정 양을 빠르거나 늦게 성능 수준에 대 한 있습니다 tooreach hello 최적의 성능 요구 사항에 대 한 선형 눈금을 가정 하 여.
4. Hello 수를 늘리거나 작업 tooperform 비율 toohow 훨씬 빠르거나 늦게에 dwu로의 원하는 합니다. 
5. 비즈니스 요구 사항에 맞는 최적 성능 수준에 도달할 때까지 계속 조정합니다.

> [!NOTE]
>
> 만 쿼리 성능을 hello 작업 계산 노드 간에 분할 될 수 있습니다 하는 경우 더 많은 병렬화에 따라 카운터가 증가 합니다. 확장 하면 성능이 변경 되지 않는 경우 데이터 균일 하지 않게 배포 여부 또는 많은 양의 데이터 이동을 도입 하는 경우 문서 toocheck 튜닝 우리의 성능을 모색 확인 하십시오. 

### <a name="when-should-i-scale-dwus"></a>언제 DWU를 조정해야 하나요?
다음 중요 한 시나리오 hello 변경 dwu로 확장:

1. 선형 검색, 집계 및 CTAS에는 문을 실행 하는 것에 대 한 hello 시스템의 성능을 변경
2. Polybase를 로드할 때 판독기 및 작성기 hello 수를 늘리면
3. 동시 쿼리 및 동시성 슬롯의 최대 수

좋은 경우 tooscale dwu로:

1. 대량의 데이터 로딩 또는 변환 작업을 수행하기 전에 데이터를 더욱 빠르게 사용할 수 있도록 DWU를 확장합니다.
2. 최대 업무 시간 동안 tooaccommodate 다 수의 동시 쿼리를 확장 합니다. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>계산 일시 중지
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

데이터베이스 toopause 개별 이러한 방법 중 하나를 사용 합니다.

* [Azure Portal을 사용하여 계산 일시 중지][Pause compute with Azure portal]
* [PowerShell을 사용하여 계산 일시 중지][Pause compute with PowerShell]
* [REST API를 사용하여 계산 일시 중지][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>계산 다시 시작
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

데이터베이스 tooresume 개별 이러한 방법 중 하나를 사용 합니다.

* [Azure Portal을 사용하여 계산 다시 시작][Resume compute with Azure portal]
* [PowerShell을 사용하여 계산 다시 시작][Resume compute with PowerShell]
* [REST API를 사용하여 계산 다시 시작][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>데이터베이스 상태 확인 

데이터베이스 tooresume 개별 이러한 방법 중 하나를 사용 합니다.

- [T-SQL을 사용하여 데이터베이스 상태 확인][Check database state with T-SQL]
- [PowerShell을 사용하여 데이터베이스 상태 확인][Check database state with PowerShell]
- [REST API를 사용하여 데이터베이스 상태 확인][Check database state with REST APIs]

## <a name="permissions"></a>권한

크기 조정 hello 데이터베이스에서 설명 하는 hello 사용 권한이 필요 [ALTER DATABASE][ALTER DATABASE]합니다.  일시 중지 및 다시 시작 필요 hello [SQL DB 참가자] [ SQL DB Contributor] 권한, 특히 Microsoft.Sql/servers/databases/action 합니다.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>다음 단계
다음 몇 가지 핵심 성과 추가 개념을 이해 하는 문서 toohelp toohello를 참조 하십시오.

* [워크로드 및 동시성 관리][Workload and concurrency management]
* [테이블 디자인 개요][Table design overview]
* [테이블 배포][Table distribution]
* [테이블 인덱싱][Table indexing]
* [테이블 분할][Table partitioning]
* [테이블 통계][Table statistics]
* [모범 사례][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
