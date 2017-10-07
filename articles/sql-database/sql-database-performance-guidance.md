---
title: "aaaAzure SQL 데이터베이스 성능 지침을 조정 | Microsoft Docs"
description: "이 문서를 사용 하는 서비스 계층 toochoose 응용 프로그램에 대해 확인할 수 있습니다. 같은 방법으로 tootune Azure SQL 데이터베이스에서 많은 정보를 응용 프로그램 tooget hello 프로그램 또한 권장합니다."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Azure SQL Database에서 성능 튜닝

Azure SQL 데이터베이스는 [권장 사항을](sql-database-advisor.md) 데이터베이스의 tooimprove 성능을 사용 하 여 또는 Azure SQL 데이터베이스 하도록 할 수 있습니다 [tooyour 응용 프로그램을 자동으로 조정](sql-database-automatic-tuning.md) 변경 내용을 적용 하 고 작업의 성능을 향상 됩니다.

권장 사항을 적용할 수 없는 및 성능 문제에 아직, 메서드 tooimprove 공연 다음 hello를 사용할 수 있습니다.
1. 증가 [서비스 계층](sql-database-service-tiers.md) 더 많은 리소스 tooyour 데이터베이스를 제공 합니다.
2. 응용 프로그램을 튜닝하고 성능을 향상시킬 수 있는 몇 가지 모범 사례를 적용합니다. 
3. 인덱스 및 toomore 데이터를 효율적으로 사용 하는 쿼리를 변경 하 여 hello 데이터베이스를 튜닝 합니다.

어떤 toodecide 필요 하기 때문에 이들은 수동 방법을 [서비스 계층](sql-database-service-tiers.md) toorewrite 응용 프로그램이 나 데이터베이스 코드 해야 하는 hello 변경 내용을 배포할 또는 선택 합니다.

## <a name="increasing-performance-tier-of-your-database"></a>데이터베이스의 성능 계층 늘리기

Azure SQL Database는 사용자가 선택할 수 있는 4가지 [서비스 계층](sql-database-service-tiers.md)(기본, 표준, 프리미엄, 프리미엄 RS)을 제공합니다(성능은 데이터베이스 처리량 단위 또는 [DTU](sql-database-what-is-a-dtu.md)로 측정함). 각 서비스 계층에서는 SQL 데이터베이스를 사용할 수 및 해당 서비스 수준에 대 한 예측 가능한 성능을 보장 hello 리소스를 엄격 하 게 격리 됩니다. 이 문서에서는 응용 프로그램에 대 한 hello 서비스 계층을 선택 하는 데 도움이 되는 지침을 제공 합니다. Azure SQL 데이터베이스에서 많은 정보를 응용 프로그램 tooget hello 프로그램을 튜닝할 수 있습니다 하는 방법으로 살펴봅니다.

> [!NOTE]
> 이 문서는 Azure SQL Database의 단일 데이터베이스에 대한 성능 지침을 중심으로 살펴봅니다. 성능 지침 관련된 tooelastic 풀 참조 [탄력적 풀에 대 한 가격 및 성능 고려 사항은](sql-database-elastic-pool-guidance.md)합니다. 그러나 대부분의 튜닝 권장 구성에서 탄력적 풀의이 문서 toodatabases hello를 적용 하 고 유사한 성능 이점을 얻을 수 있는 note 합니다.
> 

* **기본**: 1 시간 동안 1 시간, 각 데이터베이스에 대 한 hello 기본 서비스 계층 제공 정확한 성능 예측 합니다. Basic 데이터베이스에서는 여러 개의 동시 요청이 없는 작은 데이터베이스에 충분한 우수한 성능을 지원합니다. 다음은 기본 서비스 계층을 사용할 때 일반적인 사용 사례입니다.
  * **Azure SQL Database를 방금 시작한 경우**. 개발 중인 응용 프로그램은 높은 성능 수준이 필요하지 않은 경우가 많습니다. 기본 데이터베이스는 낮은 가격대의 이상적인 데이터베이스 개발 또는 테스트 환경입니다.
  * **사용자가 한 명인 데이터베이스를 가지고 있는 경우**. 사용자 한 명을 데이터베이스와 연결하는 응용 프로그램은 일반적으로 동시성과 성능 요구 사항이 높지 않습니다. 이러한 응용 프로그램은 hello Basic 서비스 계층 후보로 합니다.
* **표준**: hello Standard 서비스 계층 향상 된 성능을 예측할 수 있도록 하 고 작업 그룹 및 웹 응용 프로그램 같은 동시 요청이 여러 개 있는 데이터베이스에 대 한 좋은 성능을 제공 합니다. Standard 서비스 계층 데이터베이스를 선택하면 분 단위의 예측 가능한 성능을 기준으로 데이터베이스 응용 프로그램의 규모를 조정할 수 있습니다.
  * **데이터베이스에 여러 개의 동시 요청이 있는 경우**. 한 번에 사용자 두 명 이상을 서비스하는 응용 프로그램에는 일반적으로 더 높은 성능 수준이 필요합니다. 예를 들어 여러 개의 동시 쿼리를 지 원하는 낮은 toomedium IO 트래픽 요구 사항이 있는 작업 그룹 또는 웹 응용 프로그램에 적합 한 후보인 hello Standard 서비스 계층입니다.
* **프리미엄**: hello Premium 서비스 계층에는 예측 가능한 성능을 제공을 통해 각 Premium 데이터베이스에 대 한 두 번째, 두 번째입니다. Hello Premium 서비스 계층을 선택 하면 해당 데이터베이스에 대 한 hello 최대 부하에 따라 데이터베이스 응용 프로그램 크기. hello 계획 제거 성능 차이는 대기 시간에 민감한 작업 예상 보다 더 작은 쿼리가 tootake 발생할 수 있습니다. 이 모델에서 최대 리소스 요구, 성능 차이 또는 쿼리 대기 시간에 대 한 강력한 조건을 toomake 해야 하는 응용 프로그램에 대 한 hello 개발 및 제품 유효성 검사 주기를 단순화할 수 있습니다. 대부분의 프리미엄 서비스 계층 사용 사례는 이러한 특성을 하나 이상 가지고 있습니다.
  * **높은 최고 부하**. 상당한 CPU, 메모리 또는 입/출력 (I/O) toocomplete 필요한 응용 프로그램을 운영 하는 전용, 높은 성능 수준이 필요 합니다. 예를 들어 tooconsume 알려진 데이터베이스 작업 오랜된 시간 동안 여러 CPU 코어 hello Premium 서비스 계층에 대 한 후보입니다.
  * **동시 요청이 많은 경우**. 일부 데이터베이스 응용 프로그램은 트래픽 양이 많은 웹 사이트와 같이 많은 동시 요청을 지원합니다. 기본 및 표준 서비스 계층 hello 데이터베이스 당 동시 요청 수를 제한 합니다. 더 많은 연결을 필요로 하는 응용 프로그램에는 적합 한 예약 크기 toohandle hello 요청의 최대 수 필요한 toochoose를 해야 합니다.
  * **낮은 대기 시간**. 일부 응용 프로그램 tooguarantee hello 데이터베이스의 응답을 최단 시간에 필요 합니다. 를 보다 광범위 한 고객 작업의 일환으로 특정 저장된 프로시저를 호출 하면 해야할 요구 사항 toohave 해당 호출에서 반환 hello 시간의 99 %20 밀리초에서입니다. 이 유형의 hello Premium 서비스 계층에서 응용 프로그램 혜택 toomake 해당 hello 컴퓨팅 성능이 필요한 있는지를 사용할 수 있습니다.
* **프리미엄 RS**: IO 집약적인 작업이 필요 하지 않은 hello 가장 높은 가용성 보장을 위해 RS 프리미엄 계층 hello 마련 합니다. 예로 고성능 워크 로드 또는 hello 데이터베이스는 레코드 hello 시스템 하지는 분석 워크 로드를 테스트 합니다.

SQL 데이터베이스에 대해 필요로 하는 hello 서비스 수준 각 리소스 차원에 대 한 hello 최대 부하 요구 사항에 따라 달라 집니다. 일부 응용 프로그램은 단일 리소스를 매우 적게 사용하는 반면 다른 리소스에 대한 요구 사항은 높습니다.

### <a name="service-tier-capabilities-and-limits"></a>서비스 계층 기능 및 한도

각 서비스 계층에서 필요한 hello 용량에 대해서만 hello 유연성 toopay 갖도록 hello 성능 수준을 설정 합니다. 워크로드가 변함에 따라 [용량을 높거나 낮게 조정](sql-database-service-tiers.md)할 수 있습니다. 예를 들어 hello 백 개학 기념 쇼핑 시즌 중에 데이터베이스 작업 부하가 높은, 설정된 된 시간, 7 ~ 9 월에 대 한 hello 데이터베이스 성능 수준을 hello을 늘릴 수 있습니다. 최대 시즌이 끝나면 성능 수준을 줄일 수 있습니다. 비즈니스의는 클라우드 환경 toohello 계절성을 최적화 하 여 지불을 최소화할 수 있습니다. 이 모델은 소프트웨어 개발 출시 주기에도 적합합니다. 테스트 팀은 테스트 실행 중 용량을 할당하고 테스트가 완료되면 용량을 해제할 수 있습니다. 용량 요청 방식에서는 필요할 때마다 용량에 대해 지불하며 거의 사용하지 않는 전용 리소스에 대한 비용 지출을 방지합니다.

### <a name="why-service-tiers"></a>왜 서비스 계층인가?
각 데이터베이스 작업이 다를 수 있지만 hello 서비스 계층의 목적은 다양 한 성능 수준에서 tooprovide 성능 예측 가능성입니다. 데이터베이스 리소스 요구사항이 큰 고객은 더 많은 전용 컴퓨팅 환경에서 작업할 수 있습니다.

## <a name="tune-your-application"></a>응용 프로그램 튜닝
기존의 온-프레미스 SQL Server에서 hello 초기 용량 계획은 분리 된 경우가 많았습니다 hello 프로세스의 프로덕션 환경에서 응용 프로그램을 실행 합니다. 하드웨어 및 제품 라이선스를 먼저 구입하고 성능 튜닝을 나중에 수행합니다. Azure SQL 데이터베이스를 사용 하 여는 것이 좋습니다 toointerweave hello 프로세스의 응용 프로그램을 실행 하 고 튜닝 하는 것입니다. 요청 시 용량에 대 한 지불 hello 모델을 사용 하면 응용 프로그램 toouse hello 필요한 최소한의 리소스만 이제 종종 잘못 된 응용 프로그램에 대 한 미래 증가 계획의 추측 값에 따라 하드웨어에서 과도 프로 비전 하는 대신 튜닝할 수 있습니다. 일부 고객 수 하지 tootune 응용 프로그램을 선택한 대신 toooverprovision 하드웨어 리소스를 선택 합니다. 이 방법은 toochange 사용량이 많은 기간 중에 주요 응용 프로그램이 원하는 것이 좋습니다 될 수 있습니다. 그러나 응용 프로그램 튜닝 최소화할 수 리소스 요구 사항 및 월별 비용 hello 서비스 계층을 사용 하 여 Azure SQL 데이터베이스의 경우.

### <a name="application-characteristics"></a>응용 프로그램의 특성
Azure SQL 데이터베이스 서비스 계층 설계 된 tooimprove 성능 안정성 및 예측성 응용 프로그램에 대 한 않지만, 성능 수준에서 hello 리소스는 응용 프로그램 toobetter 활용할 프로그램 튜닝 몇 가지 모범 사례 수 있습니다. 갖지만 많은 응용 프로그램 성능이 크게 향상 하 여 tooa 전환 더 높은 성능 수준이 나 서비스 계층을 추가 튜닝 toobenefit 높은 수준의 서비스에서 일부 응용 프로그램 필요 합니다. 성능 향상을 위해 이러한 특성을 가진 응용 프로그램에 대한 추가 응용 프로그램 튜닝을 고려하십시오.

* **"번잡한" 동작으로 인해 성능이 느려지는 응용 프로그램**. 수 다 스러운 응용 프로그램에는 과도 한 데이터 액세스 작업 중요 한 toonetwork 대기 시간을 확인 합니다. 이러한 종류의 데이터 액세스 작업 toohello SQL 데이터베이스의 응용 프로그램 tooreduce hello 번호 toomodify를 할 수 있습니다. 예를 들어 임시 쿼리를 일괄 처리 또는 이동 hello 쿼리 toostored 프로시저와 같은 기술을 사용 하 여 응용 프로그램 성능을 향상 시킬 수 있습니다. 자세한 내용은 [쿼리 일괄 처리](#batch-queries)를 참조하세요.
* **전체 단일 시스템에서 지원할 수 없는 집중적인 워크로드를 가진 데이터베이스**. Hello 가장 높은 Premium 성능 수준의 hello 리소스를 초과 하는 데이터베이스 hello 작업 확장에서 이점을 얻을 수 있습니다. 자세한 내용은 아래의 [교차-데이터베이스 분할](#cross-database-sharding) 및 [기능 분할](#functional-partitioning) 섹션을 참조하세요.
* **최적이 아닌 쿼리를 포함하고 있는 응용 프로그램**. 응용 프로그램, 불완전 하 게 쿼리를 튜닝 하는 hello 데이터 액세스 계층에서 특히 하지에서 이점을 얻을 수은 높은 성능 수준입니다. 예를 들어 WHERE 절이 없거나 인덱스가 누락되거나 통계가 오래된 쿼리가 있습니다. 이러한 응용 프로그램은 표준 쿼리 성능 튜닝 기술을 사용하는 것이 도움이 됩니다. 자세한 내용은 아래의 [인덱스 누락](#identifying-and-adding-missing-indexes) 및 [쿼리 튜닝 및 힌팅](#query-tuning-and-hinting) 섹션을 참조하세요.
* **최적이 아닌 데이터 액세스 설계를 포함하고 있는 응용 프로그램**. 교착 상태와 같이 본질적인 데이터 액세스 동시성 문제가 있는 응용 프로그램은 더 높은 성능 수준에서 이점을 얻을 수 없습니다. Azure 캐싱 서비스 hello로 hello 클라이언트 쪽에 데이터를 캐싱하여 하 여 hello Azure SQL 데이터베이스에 대 한 왕복 또는 다른 캐싱 기술을 줄이는 것이 좋습니다. [응용 프로그램 계층 캐싱](#application-tier-caching)을 참조하세요.

## <a name="tune-your-database"></a>데이터베이스 튜닝
이 섹션에서는 tootune Azure SQL 데이터베이스 toogain hello 최상의 성능을 응용 프로그램에 사용 하 고 hello 가장 낮은 성능 수준에서 실행할 수 있는 몇 가지 방법을 표시 합니다. 기존의 SQL Server 튜닝 모범 사례를 일치 하는 이러한 기술 중 일부 항목도 있지만 특정 tooAzure SQL 데이터베이스입니다. 경우에 따라 데이터베이스 toofind 영역 toofurther 조정에 대 한 리소스를 소비 하는 hello를 검토 하 고 Azure SQL 데이터베이스에서 기존 SQL Server 기술을 toowork 확장할 수입니다.

### <a name="identify-performance-issues-using-azure-portal"></a>Azure Portal을 사용하여 성능 문제 식별
hello hello Azure 포털의에서 도구를 다음 분석 하 고 SQL 데이터베이스 성능 문제를 수정할 수 있습니다.

* [쿼리 성능 Insight](sql-database-query-performance.md)
* [SQL 데이터베이스 관리자](sql-database-advisor.md)

hello Azure 포털에 이러한 도구에 대 한 자세한 정보 및 방법 toouse 해당 합니다. tooefficiently 진단 하 고 문제를 해결 권장 hello Azure 포털의에서 hello 도구를 수행 합니다. Hello 수동 튜닝 누락 된 인덱스 및 특별 한 경우에 쿼리를 튜닝 하는 것에 대 한 다음에 논의 하는 접근 방식을 사용 하는 것이 좋습니다.

[성능 모니터링](sql-database-single-database-monitor.md) 문서에서 Azure SQL Database의 문제를 식별하는 방법에 대해 자세히 알아보세요.

### <a name="identifying-and-adding-missing-indexes"></a>누락된 인덱스 식별 및 추가
OLTP 데이터베이스 성능에서 일반적인 문제는 toohello 물리적 데이터베이스 디자인을 관련 됩니다. 데이터베이스 스키마를 (부하 또는 데이터 볼륨에서) 대규모로 테스트하지 않고 설계 및 배송하는 경우가 많습니다. 안타깝게도,는 hello 성능 쿼리 계획의 작은 규모에 허용 될 수도 있지만 프로덕션 수준의 데이터 볼륨에서 성능이 크게 저하 됩니다. 이 문제의 가장 일반적인 소스 hello는 적절 한 인덱스 toosatisfy 필터 또는 쿼리에 다른 제한의 hello 부족 합니다. 인덱스 누락으로 인해 인덱스 검색으로도 충분한 상황에서도 테이블 검색을 수행하는 경우가 많습니다.

이 예제에서는 hello 선택한 쿼리 계획은 seek 인덱스 검색을 사용 합니다.

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![인덱스가 누락된 쿼리 계획](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL Database는 일반적인 인덱스 누락 조건을 찾아서 해결하는 데 도움이 될 수 있습니다. Azure SQL 데이터베이스에 기본 제공 되는 Dmv는 쿼리 컴파일 중인 인덱스 크게 줄일 수 hello 예상 비용 toorun 쿼리를 살펴봅니다. 쿼리를 실행 하는 동안 SQL 데이터베이스 각 쿼리 계획을 실행 하는 얼마나 자주을 추적 하 고 해당 인덱스 존재 했던 하나 쿼리 계획과 hello를 실행 하는 hello 시간 간격은 상상한 트랙 hello 예상 합니다. 이러한 Dmv tooquickly 추측 tooyour 물리적 데이터베이스 디자인을 변경 하는 데이터베이스 및 실제 작업 부하에 대 한 전반적인 작업 부하 비용 효과 향상 시킬 수 있습니다 사용할 수 있습니다.

이 쿼리 tooevaluate 잠재적인 누락 된 인덱스를 사용할 수 있습니다.

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

이 예제에서는 hello 쿼리 결과가이 권장 사항:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

를 만든 후 해당 동일한 SELECT 문을 검색이 검색을 대신 사용 하 고 다음 hello 계획을 보다 효율적으로 실행 하는 다른 계획에서 선택:

![수정된 인덱스가 있는 쿼리 계획](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

hello 키 정보는 해당 hello 공유의 I/O 용량, 상용 시스템 전용된 서버 시스템 보다 더 제한적입니다. 불필요 한 I/O tootake를 최대한 활용 hello Azure SQL 데이터베이스 서비스 계층의 각 성능 수준의 DTU hello에 hello 시스템 최소화 중요할 경우 적절 한 물리적 데이터베이스 설계 선택 사항은 고 수 있는 크게 hello 개별 쿼리의 대기 시간, 동시 요청 크기 단위 별로 처리 hello 처리량을 향상 시킬 hello 비용 필요한 toosatisfy hello 쿼리를 최소화 합니다. 인덱스 Dmv 누락 hello에 대 한 자세한 내용은 참조 [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx)합니다.

### <a name="query-tuning-and-hinting"></a>쿼리 튜닝 및 힌팅
Azure SQL 데이터베이스의 hello 쿼리 최적화 프로그램에는 비슷한 toohello 기존의 SQL Server 쿼리 최적화 프로그램은 합니다. 대부분의 쿼리 및 hello 쿼리 최적화 프로그램에 대 한 모델 제한도 추론 이해 hello 튜닝에 대 한 유용한 hello tooAzure SQL 데이터베이스를 적용 합니다. Azure SQL 데이터베이스에서 쿼리를 튜닝 하면 집계 리소스 요구를 줄이는 추가적인 이점을 제공 hello 발생할 수 있습니다. 응용 프로그램 낮은 성능 수준에서 실행할 수 있기 때문에 튜닝 되지 않은 해당 보다 비용이 낮은 수 toorun 수 있습니다.

SQL Server에서 일반적 이며 tooAzure SQL 데이터베이스도 적용 되는 예는 hello 최적화 프로그램에서 "확인" 매개 변수를 쿼리 하는 방법입니다. 컴파일하는 동안 hello 쿼리 최적화 프로그램에서 더 최적의 쿼리 계획을 생성할 수 있는지 여부를 hello 매개 변수 toodetermine의 현재 값을 평가 합니다. 이 전략은 종종 알려진된 매개 변수 값 없이 컴파일된 계획 보다 상당히 빠른 tooa 쿼리 계획 발생할 수 있습니다, 있지만 현재 작동 분판인 모두 SQL Server 및 Azure SQL 데이터베이스에 있습니다. Hello 매개 변수 하지 일부 경우에 따라 hello 매개 변수 스니핑이 경우도 있지만 hello 생성 된 계획은 작업의 매개 변수 값의 전체 집합 hello에 대 한 만족 스 럽 지. Microsoft는 의도 보다 세밀 하 게 지정 하 고 매개 변수 스니핑의 hello 기본 동작을 재정의할 수 있도록 쿼리 힌트 (지시문)를 포함 합니다. 종종 힌트를 사용 하는 경우는 hello 기본 SQL Server 또는 Azure SQL 데이터베이스 동작은 특정 고객 작업에 대 한 완벽 한 경우 해결할 수 있습니다.

다음 예제에서는 hello hello 쿼리 프로세서 수 성능 및 리소스 요구 사항을 모두 만족 스 럽 지 않은 계획을 생성 하는 방법을 보여 줍니다. 또한 이 예에서는 쿼리 힌트를 사용하는 경우 SQL Database에 대한 쿼리 실행 시간 및 리소스 요구 사항을 줄일 수 있음을 보여 줍니다.

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

hello 설정 된 코드는 데이터 분포를 왜곡가 있는 테이블을 만듭니다. hello 최적의 쿼리 계획에 다른 어떤 매개 변수를 선택할 기반으로 합니다. 그러나 hello 계획 캐싱 동작이 hello 가장 일반적인 매개 변수 값에 기반 하 여 hello 쿼리를 다시 컴파일하십시오 항상 하지 않습니다. 따라서 캐시 되 고 다른 계획을 더 나은 선택한 계획을 평균 수 있습니다 하는 경우에 여러 값에 대해 사용 되는 최적이 아닌 계획이 toobe에 대 한 것이 같습니다. 그런 다음 hello 쿼리 계획 하나에 특별 쿼리 힌트는에 점을 제외 하 고는 동일, 두 개의 저장된 프로시저를 만듭니다.

**예(1부)**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**예(2부)**

(권장 hello 결과 원격 분석 데이터 결과 hello 구별 되도록 hello 예제 2 부를 시작 하기 전에 10 분 이상를 대기 합니다.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

이 예제에서 각 부분의 시도 toorun 매개 변수가 있는 insert 문을 1, 000 번 (toogenerate 테스트 데이터 집합으로 충분 한 부하 toouse). 저장된 프로시저를 실행할 때 hello 쿼리 프로세서는 toohello 프로시저 (매개 변수 "스니핑") 한 첫 번째 컴파일 중에 전달 되는 hello 매개 변수 값을 검사 합니다. hello 프로세서 hello 결과 계획을 캐시 하며 hello 매개 변수 값이 다른 경우에 이후 호출에 사용 합니다. 모든 경우에에서 hello에 최적의 계획을 사용할 수 있습니다. Tooguide hello 최적화 프로그램 toopick hello 쿼리를 처음으로 컴파일할에서 hello 특정 사례 보다 평균적인 사례 hello에 대 한 향상 된 계획에 필요한 경우가 있습니다. 이 예제에서는 hello 초기 계획을에서는 모든 행 toofind hello 매개 변수와 일치 하는 각 값을 읽는 "scan" 계획을 생성 합니다.

![스캔 계획을 사용하여 쿼리 튜닝](./media/sql-database-performance-guidance/query_tuning_1.png)

Hello 값 1을 사용 하 여 hello 프로시저를 실행 했기 때문에 결과 계획 hello hello 값 1에 대 한 최적의 hello 테이블의 다른 모든 값에 대 한 만족 스 럽 지 합니다. hello 결과 가능성이 hello 계획 더 느리게 수행 하 고 많은 리소스를 사용 하기 때문에 임의로 계획 각각 toopick 있었다면에 원하는 되어 있지 않습니다.

사용 하 여 hello 테스트를 실행 하는 경우 `SET STATISTICS IO` 도`ON`,이 예에서 논리적 스캔 작업이 hello hello 백그라운드 수행 됩니다. 1,148 읽기 (되지 않는 hello 평균적인 사례가 행을 하나만 tooreturn 경우 비효율적인) hello 계획에 따라 작업이 수행 되는지 확인할 수 있습니다.

![논리적 스캔을 사용하여 쿼리 튜닝](./media/sql-database-performance-guidance/query_tuning_2.png)

hello 예제의 두 번째 부분은 hello hello 컴파일 프로세스 중 쿼리 힌트 tootell hello 최적화 프로그램 toouse 특정 값을 사용합니다. 이 경우 강제로 hello 쿼리 프로세서 tooignore hello 값 hello 매개 변수로 전달 되는 대신 tooassume `UNKNOWN`합니다. 이 hello 평균적인 빈도 (기울이기 무시) hello 표에 있는 값으로를 tooa 나타냅니다. hello 결과 계획은 빠릅니다 및이 예제의 1 부에서 hello 계획 보다 평균적으로 더 적은 리소스를 사용 하는 검색 기반 계획:

![쿼리 힌트를 사용하여 쿼리 튜닝](./media/sql-database-performance-guidance/query_tuning_3.png)

Hello에서 hello 효과 볼 수 있습니다 **sys.resource_stats** 테이블 (에 hello 테스트 및 hello 데이터 hello 테이블을 채우는 하는 경우를 실행 하는 hello 시간에서 지연). 이 예에서는, 1 부 hello 22시 25분: 00 기간 중에 실행 되었고 2 부 22시 35분: 00에 실행에 대 한 hello 이전 시간대 더 많은 리소스가 사용 (으로 인해 계획 효율성 향상) 이후 하나 hello 보다 해당 시간대에서 합니다.

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![쿼리 튜닝 예의 결과](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> 이 예에서 hello 볼륨 의도적으로 작은 경우에 비 최적 매개 변수로의 hello 효과 특히 더 큰 데이터베이스에서 상당한 수 있습니다. 극단적인 경우 hello 차이 느린 경우 시와 빠른 경우 초 사이일 수 있습니다.
> 
> 

검사할 수 **sys.resource_stats** toodetermine 테스트에 대 한 hello 리소스가 다른 테스트에 비해 더 많거나 적은 리소스를 사용 하는 여부. 데이터를 비교할 때 구분 테스트의 hello 타이밍 hello에 없는 있는 hello에 동일한 5 분 창 **sys.resource_stats** 보기. hello hello 연습 ´ ֲ toominimize hello 총을 사용 하는 리소스의 양과 toominimize hello 최대 리소스에 없습니다. 일반적으로 대기 시간의 코드를 최적화할 경우 리소스 소비가 감소합니다. 응용 프로그램 tooan hello 변경 내용이 필요한 및 hello 변경 하지 않는 hello 응용 프로그램에서 쿼리 힌트를 사용할 수 있는 사람에 대 한 hello 고객 환경 저하 있는지 확인 합니다.

작업 쿼리를 반복 집합에 있는 경우 종종 의미 toocapture 고 hello 최소 리소스 크기 단위 필요한 toohost hello 데이터베이스 계획과 hello 최적 성을 계획 선택의 유효성을 검사 합니다. 경우에 따라 유효성을 검사 한 후 hello 계획 toohelp 수 있도록 하 하 여 성능이 저하 되지 다시 확인 합니다. [쿼리 힌트(Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx)에 대해 더 자세히 알아볼 수 있습니다.

### <a name="cross-database-sharding"></a>교차-데이터베이스 분할
Azure SQL 데이터베이스는 상용 하드웨어에서 실행, 때문에 단일 데이터베이스에 대 한 hello 용량 한도 기존의 온-프레미스 SQL Server 설치의 경우 보다 낮습니다. 일부 고객 hello 작업 Azure SQL 데이터베이스에서 단일 데이터베이스의 hello 제한 내에 포함 하지 않는 경우 여러 데이터베이스 간에 분할 기법 toospread 데이터베이스 작업을 사용 합니다. 현재 Azure SQL Database에 분할 기법을 사용하는 대부분의 고객은 여러 데이터베이스에서 단일 규격으로 데이터를 분할합니다. 이 접근 방식에 대 한 toounderstand OLTP 응용 프로그램에 종종 tooonly 한 행 이나 tooa 소규모 행 그룹 hello 스키마에 적용 되는 트랜잭션을 수행 해야 합니다.

> [!NOTE]
> 이제 SQL 데이터베이스 분할 라이브러리 tooassist를 제공합니다. 자세한 내용은 [탄력적 데이터베이스 클라이언트 라이브러리 개요](sql-database-elastic-database-client-library.md)를 참조하세요.
> 
> 

예를 들어 데이터베이스에 있는 경우 고객 이름, 주문 및 주문 세부 정보 (예: SQL Server와 함께 제공 되는 기존 예제 Northwind 데이터베이스 hello)를 있습니다 수 분할이 데이터를 여러 데이터베이스로 hello로 고객을 그룹화 하 여 관련 주문 및 주문 정보 정보입니다. 단일 데이터베이스에 유지 되는 hello 고객의 데이터를 보장할 수 있습니다. hello 응용 프로그램 데이터베이스에 여러 데이터베이스에 걸쳐 hello 부하를 효과적으로 분배 여러 고객을 분할 합니다. 분할에서 고객 뿐만 아니라 피할 수 hello 최대 데이터베이스 크기 제한 되지만 Azure SQL 데이터베이스도 처리할 수에 맞는 각 개별 데이터베이스가 상태로 hello 다른 성능 수준의 hello 제한 보다 훨씬 큰 경우에 작업의 DTU입니다.

데이터베이스 분할 솔루션에 대 한 hello 집계 리소스 용량을 줄 지는 않습니다 이지만 여러 데이터베이스 간에 분산 된 매우 큰 솔루션 지원에 매우 효과적입니다. 각 데이터베이스는 서로 다른 성능 수준 toosupport 매우 큰 "효율적인" 데이터베이스를 리소스 요구 사항이 높은에 실행할 수 있습니다.

### <a name="functional-partitioning"></a>기능 분할
SQL Server 사용자는 단일 데이터베이스 내에 여러 기능을 결합하는 경우가 많습니다. 예를 들어 응용 프로그램에 저장소에 대 한 논리 toomanage 인벤토리를 해당 데이터베이스에 재고, 구매 주문과 저장된 프로시저, 월말의 보고 기능을 관리 하는 인덱싱되지 않으며 구체화 된 뷰를 추적와 연결 된 논리가 될 수 있습니다. 이 방법을 통해 쉽게 tooadminister hello 데이터베이스 백업 작업에 대 한 것 이지만 응용 프로그램의 모든 기능에서 있습니다 toosize hello 하드웨어 toohandle hello 최대 부하가 필요 합니다.

Azure SQL 데이터베이스의 확장 아키텍처를 사용 하는 경우 서로 다른 데이터베이스로 응용 프로그램의 좋은 생각 toosplit 서로 다른 기능 이므로. 이 기법을 사용하면 각 응용 프로그램은 독립적으로 확장됩니다. 응용 프로그램이 점점 (및 부하 hello 데이터베이스 증가를 hello) 관리자에 게 hello 응용 프로그램에서 각 함수에 대 한 독립적인 성능 수준을 선택할 수 있습니다. Hello 제한 되어 있으며,이 아키텍처에서 응용 프로그램는 단일 상용 시스템은 여러 컴퓨터 간에 분산 되는 hello 부하 때문에 처리할 수 있는 보다 클 수 있습니다.

### <a name="batch-queries"></a>쿼리 일괄 처리
대용량을 사용 하 여 데이터를 액세스 하는 응용 프로그램에 대 한 임시 쿼리를 자주 상당한 양의 응답 시간이 소비 됩니다 hello 응용 프로그램 계층과 hello Azure SQL 데이터베이스 계층 사이의 네트워크 통신에. Hello 둘 다 하는 경우에 응용 프로그램 및 Azure SQL 데이터베이스 데이터 액세스 작업 수가 많은 동일한 데이터 센터 두 hello 사이의 hello 네트워크 대기 시간이 늘어날 수 수 hello에 있습니다. round tooreduce hello 네트워크 이름 한 번 hello 데이터에 대 한 액세스 작업, toocompile 또는 hello 옵션 tooeither 일괄 처리 hello 임시 쿼리를 사용 하는 것이 좋습니다 저장 프로시저로 합니다. Hello 임시 쿼리를 일괄 처리 하는 경우에 단일 여행 tooAzure SQL 데이터베이스에서에서 하나의 큰 일괄 처리로 여러 개의 쿼리를 보낼 수 있습니다. 저장된 프로시저에서 임시 쿼리를 컴파일하는 경우에 hello 하면 일괄 처리 하는 경우 같은 결과 얻을 수 있습니다. 사용 하 여 저장된 프로시저 또한 hello를 사용할 수 있도록 Azure SQL 데이터베이스의 hello 쿼리 계획을 캐시 하는 hello 가능성 이점이 hello 제공 저장 프로시저를 다시.

일부 응용 프로그램은 쓰기를 많이 사용합니다. 경우에 따라 toobatch 함께 기록 하는 방법을 고려 하 여 데이터베이스에서 hello 총 I/O 부하를 줄일 수 있습니다. 흔히 이렇게 하려면 저장된 프로시저 및 임시 배치 내에서 트랜잭션을 자동 커밋하는 대신 명시적 트랜잭션을 사용하기만 하면 됩니다. 사용 가능한 다양한 기법을 평가하려면 [Azure에서 SQL Database 응용 프로그램의 일괄 처리 기법](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx)을 참조하세요. 사용자 고유의 작업 부하 toofind hello 적합 한 모델 일괄 처리를 위해 사용해 보십시오. 모델을 가질 수 있는 있는지 toounderstand 보다 약간에 있을 다른 트랜잭션 일관성은 보장 합니다. 리소스 사용을 최소화 하는 hello 올바른 작업 찾기 위해서는 일관성과 성능 절충이 hello 잘 조합 합니다.

### <a name="application-tier-caching"></a>응용 프로그램 계층 캐싱
일부 데이터베이스 응용 프로그램에는 읽기 작업이 많은 워크로드가 포함되어 잇습니다. 레이어를 캐싱 hello 데이터베이스에서 hello 부하를 줄일 수 있습니다 및 Azure SQL 데이터베이스를 사용 하 여 hello 성능 수준 필요한 toosupport 데이터베이스를 잠재적으로 줄일 수 있습니다. 와 [Azure Redis Cache](https://azure.microsoft.com/services/cache/), hello 데이터를 한 번만 읽을 수는 읽기 작업이 많은 경우 (또는 시스템 구성 된 방식에 따라 응용 프로그램 계층 시스템 당 한 번), 다음 SQL 데이터베이스 외부에서 해당 데이터를 저장 합니다. 이 방법은 tooreduce 데이터베이스 부하 (CPU 및 I/O 읽기) 이지만 트랜잭션 일관성에 영향을 줄 hello 캐시에서 읽고 있는 hello 데이터 hello 데이터베이스의 hello 데이터와 동기화 될 수 있으므로 합니다. 많은 응용 프로그램에서 비일관성이 어느 정도 허용되지만 모든 워크로드에 대해 허용되는 것은 아닙니다. 응용 프로그램 계층 캐싱 전략을 구현할 경우 응용 프로그램 요구 사항을 완전히 이해해야 합니다.

## <a name="next-steps"></a>다음 단계
* 서비스 계층에 대한 자세한 내용은 [Azure SQL Database 옵션 및 성능](sql-database-service-tiers.md)
* 탄력적 풀에 대한 자세한 내용은 [Azure 탄력적 풀이란?](sql-database-elastic-pool.md)을 참조하세요.
* 성능 및 탄력적인 풀에 대 한 정보를 참조 하십시오. [때 tooconsider 탄력적 풀](sql-database-elastic-pool-guidance.md)

