---
title: "SQL Database: DTU란? | Microsoft Docs"
description: "Azure SQL Database 트랜잭션 단위가 무엇인지 이해합니다."
keywords: "데이터베이스 옵션, 데이터베이스 성능"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>DTU(데이터베이스 트랜잭션 단위) 및 eDTU(탄력적 데이터베이스 트랜잭션 단위) 설명
이 문서에서는 데이터베이스 트랜잭션 단위 (DTUs) 및 탄력적 데이터베이스 트랜잭션 단위 (Edtu)에 도달 하면 어떤 일이 생기 hello 최대 Dtu 또는 Edtu를 설명 합니다.  

## <a name="what-are-database-transaction-units-dtus"></a>DTU(데이터베이스 트랜잭션 단위)란?
내에서 특정 성능 수준에서 단일 Azure SQL 데이터베이스에 대 한는 [서비스 계층](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels), Microsoft 특정 수준의 해당 데이터베이스에 대 한 리소스 (Azure 클라우드 hello에 다른 데이터베이스의 독립적인) 보증을 제공 하 고는 예측 가능한 성능 수준을 합니다. 이 리소스 양은 DTU(데이터베이스 트랜잭션 단위) 수로 계산되며 CPU, 메모리, I/O(데이터 및 트랜잭션 로그 I/O)의 혼합된 측정치입니다. 이러한 리소스 중 hello 비율에 따라 결정 원래 되었으며는 [OLTP 벤치 마크의 작업](sql-database-benchmark-overview.md) 실제 OLTP 워크 로드의 일반적인 toobe 설계 되었습니다. 작업 이러한 리소스 중 아무 메서드나 hello 금액을 초과 하면 처리량은 제한 된 느린 성능 및 시간 제한. 작업에서 사용 하는 hello 리소스 hello Azure 클라우드의에서 hello 리소스 사용 가능한 tooother SQL 데이터베이스에 영향을 주지 않는 및 다른 작업에서 사용 하는 hello 리소스 hello 리소스 사용 가능한 tooyour SQL 데이터베이스 영향을 주지 않습니다.

![경계 상자](./media/sql-database-what-is-a-dtu/bounding-box.png)

Dtu는 이해 다양 한 성능 수준에서 Azure SQL 데이터베이스 및 서비스 계층 간의 리소스의 상대적인 양을 hello에 대 한 가장 유용 합니다. 예를 들어 데이터베이스의 hello 성능 수준을 높여 hello Dtu를 두 배로 toodoubling hello 집합이 리소스 사용 가능한 toothat 데이터베이스과 같습니다. 예를 들어 1750 DTU를 사용하는 프리미엄 P11 데이터베이스는 5개의 DTU를 사용하는 기본 데이터베이스보다 350배 더 많은 DTU 계산 기능을 제공합니다.  

작업을 사용 하 여 hello (DTU) 리소스 소비에 깊이 이해할 toogain [Azure SQL 데이터베이스 Query Performance Insight](sql-database-query-performance.md) 에:

- 잠재적으로 향상 된 성능을 위해 튜닝할 수 있는 CPU/기간/실행 수에 따라 hello 상위 쿼리를 식별 합니다. I/O 집약적인 쿼리 hello 사용에서 이점을 얻을 수는 예를 들어 [메모리 내 최적화 기술을](sql-database-in-memory.md) toomake 좋은 hello 사용 가능한 메모리가 특정 서비스 계층과 성능 수준에서 사용 하 여 합니다.
- 쿼리의 hello 세부 정보로 드릴 다운, 해당 텍스트 및 리소스 사용률의 기록을 확인 합니다.
- [SQL Database Advisor](sql-database-advisor.md)에서 수행한 작업을 표시하는 성능 조정 권장 사항에 액세스합니다.

있습니다 수 [서비스 계층을 변경할](sql-database-service-tiers.md) 언제 라도 최소한의 가동 중지 시간 tooyour 응용 프로그램 (일반적으로 평균 4 초 미만). 많은 비즈니스 및 앱에 대 한 수 toocreate 데이터베이스 않으며 전화 주문형 성능 위로 또는 아래로 사용 패턴은 상대적으로 예측 하는 경우에 특히는 충분 합니다. 하지만 예측할 수 없는 사용 패턴을 사용 하는 경우 그 수 하드 toomanage 비용 및 비즈니스 모델. 이 시나리오에서는 탄력적 풀 Edtu hello 풀에 여러 데이터베이스 간에 공유 되는 여러 함께 사용할 수 있습니다.

![데이터베이스 소개 tooSQL: 단일 계층 및 수준으로 데이터베이스 Dtu](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>eDTU(탄력적 데이터베이스 트랜잭션 단위)란?
대신 항상 하지 필요 여부에 관계 없이 사용할 수 있는 SQL 데이터베이스 리소스 (DTUs) tooa 전용된 집합을 제공 하는, 보다로 데이터베이스를 배치할 수는 [탄력적 풀](sql-database-elastic-pool.md) 리소스 풀을 공유 하는 SQL 데이터베이스 서버에서 간에 이러한 데이터베이스입니다. 탄력적 데이터베이스 트랜잭션 단위 또는 Edtu로 측정 된 탄력적 풀의 리소스를 공유 하는 hello입니다. 탄력적 풀 여러 다양 한 있는 데이터베이스 및 예측할 수 없는 사용 패턴에 대 한 간단한 비용 효율적인 솔루션 toomanage hello 성능 목표를 제공 합니다. 한 데이터베이스가 없습니다. 모든 hello 리소스를 사용 하는지 보장할 수는 탄력적인 풀의 hello 풀와도 최소한의 리소스는 항상 탄력적 풀의 사용 가능한 tooa 데이터베이스. 자세한 내용은 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

![데이터베이스 소개 tooSQL: Edtu 계층 및 수준](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

풀은 집합 가격에 대한 eDTU 수 집합이 제공됩니다. Hello 탄력적 풀에서 개별 데이터베이스 hello 유연성 tooauto 단위 hello 구성 된 경계 내에서 제공 됩니다. 부하가 큰 상태에서 데이터베이스 부하량에서 데이터베이스를 소비 작은 toohello 포인트 없는 부하 상태에서 데이터베이스 없는 Edtu를 사용 하지만 많은 Edtu toomeet 수요가 사용할 수 있습니다. Hello 전체 풀에 대 한 리소스를 프로 비전 하 여 보다는 데이터베이스 마다 관리 작업은 간단 하며 hello 풀에 대 한 예측 가능한 예산을 해야 합니다.

추가 Edtu hello 풀의 hello 데이터베이스에 중단 시간 없이 데이터베이스 및 영향을 주지 기존 풀 tooan 추가할 수 있습니다. 마찬가지로 더 이상 필요하지 않은 추가 eDTU는 언제든지 기존 풀에서 제거할 수 있습니다. 추가 하거나 뺄 데이터베이스 toohello 풀 수 또는 다른 데이터베이스에 대 한 부하가 tooreserve Edtu에서 Edtu 데이터베이스의 한도 hello 금액을 사용할 수 있습니다. 데이터베이스는 예측 가능한 방식으로 사용 하는 경우 리소스를 있습니다 수 hello 풀 밖으로 이동 하 고 예측 가능한 양의 가용 필요한 리소스를 단일 데이터베이스로 구성 되어 있습니다.

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>내 작업에 필요한 Dtu hello 수는 어떻게 확인할 수 있습니까?
Hello toomigrate 기존 온-프레미스 또는 SQL Server 가상 컴퓨터 작업 부하 tooAzure SQL 데이터베이스를 원하는 경우 사용할 수 있습니다 [DTU 계산기](http://dtucalculator.azurewebsites.net/) 필요한 Dtu tooapproximate hello 수 있습니다. 기존 Azure SQL 데이터베이스 작업 부하에 대해 사용할 수 있습니다 [SQL 데이터베이스 Query Performance Insight](sql-database-query-performance.md) toounderstand 프로그램 데이터베이스 리소스 사용 (DTUs) tooget에 깊이 이해할 방법 toooptimize 작업 합니다. Hello를 사용할 수도 있습니다 [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget hello 리소스 소비량에 대 한 정보 hello 지난 1 시간입니다. 카탈로그 뷰 또는 hello [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) 수 또한 될 쿼리 tooget hello hello 마지막 14 일에 대 한 동일한 데이터의 5 분 평균 낮은 충실도에 있지만 합니다.

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>리소스의 탄력적 풀의 이점이 있다면 어떻게 알 수 있나요?
풀은 특정 사용 패턴을 가진 많은 데이터베이스에 적합합니다. 주어진 데이터 베이스에 대해, 이 패턴은 상대적으로 사용률 급증이 드물고 평균 사용률이 낮음으로 규정됩니다. SQL 데이터베이스는 자동으로 기존 SQL 데이터베이스 서버에서 데이터베이스의 hello 기록 리소스 사용량을 평가 하 고 hello Azure 포털에서에서 hello 적절 한 풀 구성을 권장 합니다. 자세한 내용은 [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool.md)를 참조하세요.

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>내 최대 DTU에 도달한 경우 어떻게 되나요?
성능 수준에 맞게 조정 된 및 관리 tooprovide hello 필요한 리소스 toorun 데이터베이스 작업을 선택한 서비스 계층/성능 수준에 대 한 허용 toohello 최대 제한 합니다. 작업은 CPU/데이터/로그 IO 제한 중 하나에서 hello 제한에 도달, hello 최대 허용 수준 tooreceive hello 리소스를 계속 하지만 쿼리에 대 한 대기 시간이 증가 가능성이 toosee 됩니다. 이러한 제한으로 나타나지 모든 오류가 발생 하지만 hello 작업에서 속도가 느려지는 대신 hello 속도가 느려지는 심하게 쿼리 타이밍을 시작 하는 경우. 허용되는 최대 동시 사용자 세션/요청(작업자 스레드) 제한에 도달하면 명시적 오류가 표시됩니다. 메모리, 데이터 I/O 및 트랜잭션 로그 I/O가 아닌 CPU 리소스의 제한 사항에 대한 자세한 내용은 [Azure SQL Database 리소스 제한](sql-database-resource-limits.md) 을 참조하세요.

## <a name="next-steps"></a>다음 단계
* 참조 [서비스 계층](sql-database-service-tiers.md) hello Dtu와 Edtu와 탄력적 풀에 대 한 단일 데이터베이스에 대해 사용할 수에 대 한 내용은 합니다.
* 메모리, 데이터 I/O 및 트랜잭션 로그 I/O가 아닌 CPU 리소스의 제한 사항에 대한 자세한 내용은 [Azure SQL Database 리소스 제한](sql-database-resource-limits.md) 을 참조하세요.
* 참조 [SQL 데이터베이스 Query Performance Insight](sql-database-query-performance.md) toounderstand (DTUs) 소비 합니다.
* 참조 [SQL 데이터베이스 벤치 마크 개요](sql-database-benchmark-overview.md) hello OLTP 벤치 마크의 작업 뒤에 있는 toounderstand hello 방법론 DTU blend toodetermine hello을 사용 합니다.
