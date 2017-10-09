---
title: "Azure SQL 데이터베이스의 데이터베이스 성능 aaaMonitoring | Microsoft Docs"
description: "Azure tools 및 동적 관리 뷰를 이용한 데이터베이스 모니터링의 hello 옵션에 알아봅니다."
keywords: "데이터베이스 모니터링, 클라우드 데이터베이스 성능"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 데이터베이스 성능 모니터링
Azure의 SQL 데이터베이스의 hello 성능을 모니터링 하는 hello 리소스 사용률 상대 toohello 수준을 선택 하면 데이터베이스 성능 모니터링으로 시작 합니다. 모니터링 하면 데이터베이스 크기가 리소스는 최대값을 초과, 때문에 문제가 하는지 여부를 확인 하 고 다음 시간 tooadjust hello 성능 수준 인지를 결정 하 고 [서비스 계층](sql-database-service-tiers.md) 데이터베이스입니다. Hello에 그래픽 도구를 사용 하 여 데이터베이스를 모니터링할 수 있습니다 [Azure 포털](https://portal.azure.com) SQL을 사용 하 여 또는 [동적 관리 뷰](https://msdn.microsoft.com/library/ms188754.aspx)합니다.

## <a name="monitor-databases-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 데이터베이스를 모니터링 합니다.
Hello에 [Azure 포털](https://portal.azure.com/), 데이터베이스를 선택 하 고 hello를 클릭 하 여 단일 데이터베이스의 사용량을 모니터링할 수 **모니터링** 차트입니다. 그러면는 **메트릭을** hello를 클릭 하 여 변경할 수 있는 창 **차트 편집** 단추입니다. 다음 메트릭 hello를 추가 합니다.

* CPU 비율
* DTU 비율
* 데이터 IO 비율
* 데이터베이스 크기 비율

이러한 메트릭은 다음을 추가 했으므로 tooview 계속할 수 있습니다 hello에서 해당 **모니터링** hello에 대 한 자세한 내용은 포함 하는 차트 **메트릭을** 창. 모든 4 개의 메트릭에서 hello 평균 사용률 백분율 상대 toohello **DTU** 데이터베이스입니다. Hello 참조 [서비스 계층](sql-database-service-tiers.md) Dtu에 대 한 세부 정보에 대 한 문서입니다.

![데이터베이스 성능의 서비스 계층 모니터링.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Hello 성능 메트릭에 경고를 구성할 수 있습니다. Hello 클릭 **추가 경고** hello 단추 **메트릭을** 창. 결제 경고가 hello 마법사 tooconfigure를 따릅니다. Hello 메트릭이 특정 임계값을 초과 하는 경우 또는 hello 메트릭이 특정 임계값 미만으로 떨어질 경우 hello 옵션 tooalert를 해야 합니다.

예를 들어 데이터베이스 toogrow에 hello 작업 부하를 예상 되는 경우 선택할 수 있습니다 tooconfigure 전자 메일 경고를 데이터베이스에는 80 %hello 성능 메트릭 중 하나에 도달할 때마다. 이 조기 경고 toofigure 때 tooswitch toohello 다음으로 높은 성능 수준 해야할 아웃로 사용할 수 있습니다.

hello 성능 메트릭 수 toodowngrade tooa 성능이 저하 되 고 있는지 확인 하기을 유용할 수 있습니다. Standard S2 데이터베이스를 사용 하 고 데이터베이스 평균 hello 모든 성능 메트릭을 표시 언제 든 지 10% 이상을 사용 하지 않는 것으로 가정 합니다. Hello 데이터베이스 표준 s 1에서 잘 작동 하는 가능성이 높습니다. 하지만 갑작스러운 작업량 증가 나 변동을 hello 의사 결정 toomove tooa 낮은 성능 수준 하기 전에 고려해 야 합니다.

## <a name="monitor-databases-using-dmvs"></a>DMV를 사용하여 데이터베이스 모니터링
hello 같은 hello 포털에 표시 되는 사용할 수 있는 메트릭이 시스템 뷰를 통해: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello 논리에서 **마스터** 서버, 데이터베이스 및 [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) hello 사용자 데이터베이스에 있습니다. 사용 하 여 **sys.resource_stats** 긴 기간으로 toomonitor 세분화 된 데이터를 적게 필요 합니다. 사용 하 여 **sys.dm_db_resource_stats** toomonitor 해야 할 경우 보다 작은 시간 프레임 내에서 더 세분화 된 데이터입니다. 자세한 내용은 [Azure SQL 데이터베이스 성능 지침](sql-database-single-database-monitor.md#monitor-resource-use)을 참조하세요.

> [!NOTE]
> **sys.dm_db_resource_stats**는 Web 및 Business Edition 데이터베이스에서 사용할 때 빈 결과 집합을 반환합니다.
>
>

### <a name="monitor-resource-use"></a>리소스 사용 모니터링

[SQL Database Query Performance Insight](sql-database-query-performance.md) 및 [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx)를 사용하여 리소스 사용량을 모니터링할 수 있습니다.

또한 다음 두 가지 뷰를 사용하여 사용을 모니터링할 수도 있습니다.

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Hello를 사용할 수 있습니다 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) 모든 SQL 데이터베이스에 대 한 보기입니다. hello **sys.dm_db_resource_stats** 보기 데이터 상대 toohello 서비스 계층에 대 한 최근의 리소스 사용을 표시 합니다. CPU, 데이터 I/O, 로그 쓰기 및 메모리의 평균 백분율을 15초마다 기록하고 1시간 동안 보관합니다.

이 뷰는 리소스 사용률에 대한 훨씬 구체적인 정보를 제공하므로 현재 상태 분석 또는 문제 해결에 **sys.dm_db_resource_stats**를 먼저 사용해야 합니다. 예를 들어이 쿼리는 hello 평균 및 최대 리소스 사용 hello 현재 데이터베이스에 대 한 hello를 통해 지난 시간 보여 줍니다.

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

다른 쿼리에 대 한 참조의 hello 예제 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)합니다.

#### <a name="sysresourcestats"></a>sys.resource_stats
hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello에서 보기 **마스터** 데이터베이스에 가장 특정 서비스 계층과 성능 수준에서 SQL 데이터베이스의 hello 성능을 모니터링 하는 데 도움이 되는 추가 정보 . hello 데이터는 수집 5 분 마다 며 약 35 일 동안 유지 됩니다. 이 뷰는 SQL Database가 리소스를 사용하는 방법에 대한 장기적인 기록 분석에 유용합니다.

hello 다음 그래프 각 시간에 대 한 hello CPU 리소스 사용 P2 성능 수준 hello 사용 하 여 Premium 데이터베이스에 대 한 주 보여줍니다. 이 그래프 월요일에 시작, 5 작업 일을 보여 주는 주말 훨씬 적은 hello 응용 프로그램에서 발생 하는 경우.

![SQL Database 리소스 사용](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Hello 데이터에서이 데이터베이스에 현재 있습니다 최대 CPU 부하를 약간 넘은 50 %CPU 상대 toohello P2 성능 수준 (화요일 정오)를 사용 합니다. CPU hello 응용 프로그램의 리소스 프로필에서 hello 중요 한 요소 이면 p 2는 워크 로드를 항상 hello 성능 수준 tooguarantee에 맞는 오른쪽 hello를 결정할 수 있습니다. 시간이 지남에 따라 응용 프로그램 toogrow 하려는 경우 있도록 것이 좋습니다 toohave 추가 리소스 버퍼 hello 응용 프로그램 하지 않는 hello 성능 수준의 제한에 도달 하지 못합니다. Hello 성능 수준을 높인 데이터베이스 되지 않은 경우에 충분 한 전력 tooprocess 요청 효과적으로, 특히 대기 시간에 민감한 환경에서에서 발생할 수 있는 고객에 게 표시 되 오류를 방지할 수 있습니다. 예로 지 원하는 hello 데이터베이스 호출 결과에 따른 웹 페이지를 색칠 하는 응용 프로그램 데이터베이스.

다른 응용 프로그램 종류는 동일한 그래프 다르게 hello를 해석할 수 있습니다. 예를 들어 응용 프로그램 매일 tooprocess 급여 데이터를 시도 하는 hello 하는 경우이 종류의 "일괄 작업" 모델 동일한 차트 수행할 수 제대로 P1 성능 수준입니다. hello P1 성능 수준이 hello P2 성능 수준에서 100 Dtu too200 Dtu에 있습니다. hello P1 성능 수준이 hello P2 성능 수준의 절반 hello 성능을 제공합니다. 따라서 P2에서 CPU 사용의 50%는 P1에서 100% CPU 사용과 같습니다. Hello 응용 프로그램 시간 제한을 지정 되지 않은 경우 것 수 인지는 중요 하지 작업 2.5 시간 toofinish 2 시간이 걸리든 오늘이 작업이 수행을 가져옵니다. 이 범주의 응용 프로그램은 아마 P1 성능 수준을 사용할 것입니다. Hello 있다는 사실을 hello 하루 리소스 사용량이 낮은, "큰 최대 부하" hello 일의 뒷부분에 나오는 hello 낮아지는 중 하나로 보내는 넘어가게 수 있도록 하는 동안 시간 동안 활용할 수 있습니다. hello 작업 수 시간 내에 완료 매일으로 hello P1 성능 수준이 응용 프로그램의 (와), 이러한 종류 향상 될 수 있습니다.

Azure SQL 데이터베이스 노출 소비 된 각 활성 데이터베이스 hello에 대 한 리소스 정보 **sys.resource_stats** hello의 보기 **마스터** 각 서버에 데이터베이스입니다. hello 표에 hello 데이터는 5 분 간격으로 집계 됩니다. Hello Basic, Standard 및 Premium 서비스 계층에서는 hello 데이터 수 보다 많은 양을 사용할 5 분 tooappear hello 표에 되므로이 데이터를 거의 실시간 분석 아닌 기록 분석에 더 유용한 합니다. 쿼리 hello **sys.resource_stats** toosee hello toovalidate 필요할 때 원하는 hello 성능 배달 hello 예약을 선택 했는지 여부 및 데이터베이스의 최근 기록을 보기.

> [!NOTE]
> 연결 된 toohello 해야 **마스터** 프로그램 논리 SQL 데이터베이스 서버 tooquery의 데이터베이스 **sys.resource_stats** 예제 따르는 hello에 합니다.
> 
> 

이 예제에서는이 뷰의 hello 데이터 노출 하는 방법을 보여 줍니다.

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![hello sys.resource_stats 카탈로그 뷰](./media/sql-database-performance-guidance/sys_resource_stats.png)

hello 다음 예제에 나와 hello를 사용할 수 있는 다양 한 방법 **sys.resource_stats** 카탈로그 SQL 데이터베이스 리소스를 사용 하는 방법에 대 한 보기 tooget 정보:

1. 주 리소스 지난 hello toolook 데이터베이스 userdb1 hello에 대 한 사용 하 여,이 쿼리를 실행할 수 있습니다.
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. 워크 로드에 맞는 hello 성능 수준에 얼마나 잘 tooevaluate, 필요한 toodrill 아래로 hello 리소스 메트릭의 각 측면에: CPU, 읽기, 쓰기, 작업자 수 및 세션 수입니다. 같습니다. 수정 된 쿼리를 사용 하 여 **sys.resource_stats** tooreport hello 이러한 리소스 메트릭의 평균 및 최대 값:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. 각 리소스 메트릭의 평균 및 최대 값 hello에 대 한이 정보를 통해 선택한 hello 성능 수준에 워크 로드에 맞는 얼마나 잘 평가할 수 있습니다. 일반적으로의 평균 값 **sys.resource_stats** hello 목표 크기를 정하는 기준 toouse를 제공 합니다. 기본 측정 기준이 되어야 합니다. 예를 들어 사용 중일 수 있습니다 hello Standard 서비스 계층 S2 성능 수준으로 됩니다. hello 평균 CPU 및 I/O 읽기에 대 한 백분율을 사용 및 40% 미만입니다. 쓰기는, hello 평균 작업자 수가 50을 밑 및 hello 평균 세션 수가 200입니다. 사용자의 작업이 S1 성능 수준 hello에 적합 하 게 합니다. 데이터베이스 크기 hello 작업자 및 세션 제한에 맞도록 쉽게 toosee가 합니다. toosee tooCPU, 읽기 및 쓰기 간주 데이터베이스와 더 낮은 성능 수준에 맞는지 여부 hello 더 낮은 성능 수준의 DTU 수를 hello hello 프로그램 현재 성능 수준의 DTU 수로 나누고 hello 결과 100을 곱합니다.
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    hello 결과 백분율로 hello 두 성능 수준 간에 hello 상대적인 성능 차이입니다. 리소스 사용 하지 않는이 크기를 초과 하는 작업에 적합 하 게 hello 낮은 성능 수준입니다. 그러나 모든 범위의 리소스 사용 값 toolook 필요 고 데이터베이스 작업이 낮은 성능 수준 hello에 맞습니다. 얼마나 자주 백분율로 결정 합니다. hello 다음 쿼리 출력 hello 백분율을 계산 하이 예에서 40%의 hello 임계값에 따라 리소스 차원 별로 맞춤 다음과 같습니다.
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    실행 하 여 데이터베이스 서비스 수준 목표 SLO ()에 따라, 사용자의 작업이 hello 낮은 성능 수준에 적합 한지 여부를 결정할 수 있습니다. 데이터베이스 작업 SLO가 99.9 %hello 앞의 쿼리 값을 반환 세 리소스 차원 모두에 대해 99.9% 보다 큰 경우 가능성이 작업 hello 낮은 성능 수준에 맞게 조정 합니다.
   
    Hello 맞춤 백분율을 보면 toohello 다음 상위 성능 수준 toomeet SLO 이동 해야 하는지 여부에 대 한 정보 들이 제공 됩니다. 예를 들어 userdb1 hello 다음 지난 주 hello에 대 한 CPU 사용을 보여 줍니다.
   
   | 평균 CPU 사용률 | 최대 CPU 사용률 |
   | --- | --- |
   | 24.5 |100.00 |
   
    평균 CPU hello hello 데이터베이스의 성능 수준을 hello에도 적합 hello 성능 수준의 hello 제한의 1/4입니다. 하지만 hello 최 댓 값 hello 데이터베이스 성능 수준 hello hello 제한에 도달 하면 표시 됩니다. Toomove toohello 다음으로 높은 성능 수준 필요 한가요? 살펴보고 여러 번 작업 도달 100%와 tooyour 데이터베이스 작업 SLO 비교 합니다.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    이 쿼리는 값을 반환 하는 경우 모든 hello 세 리소스 차원에 대해 99.9% 보다 작은 어느 이동 toohello 다음으로 높은 성능 수준 하거나 hello SQL 데이터베이스에서 응용 프로그램 튜닝 기법 tooreduce hello 로드를 사용 하십시오.
4. 이 연습도 고려 hello에 예상 되는 작업 증가 사용 하 여 향후 합니다.

탄력적 풀에 대 한이 섹션에 설명 된 hello 기술로 hello 풀의 개별 데이터베이스를 모니터링할 수 있습니다. 하지만 전체 hello 풀을 모니터링할 수 있습니다. 자세한 내용은 [탄력적 풀 모니터링 및 관리](sql-database-elastic-pool-manage-portal.md)를 참조하세요.


### <a name="maximum-concurrent-requests"></a>동시 요청이 최대인 경우
SQL 데이터베이스에서이 TRANSACT-SQL 쿼리를 실행 하는 동시 요청의 toosee hello 수 있습니다:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

온-프레미스 SQL Server 데이터베이스의 tooanalyze hello 작업 수정이 쿼리 toofilter 원하는 tooanalyze hello 특정 데이터베이스에 있습니다. 예를 들어 MyDatabase 라는 온-프레미스 데이터베이스를 설정한 경우이 TRANSACT-SQL 쿼리 반환 hello 동시 요청 수가 해당 데이터베이스에 있는 합니다.

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

이는 단일 시점의 스냅숏일 뿐입니다. toocollect 필요한 tooget의 작업 및 동시 요청 요구 사항, 시간이 지남에 따라 많은 샘플이 있습니다.

### <a name="maximum-concurrent-logins"></a>최대 동시 로그인 수
로그인의 hello 주파수 이해 하면 사용자 및 응용 프로그램 패턴 tooget을 분석할 수 있습니다. 이 또는이 문서에서 설명 하는 기타 제한 도달 하지는 있는지 테스트 환경 toomake에 현실의 부하를 실행할 수도 있습니다. 동시 로그인 수 또는 기록을 표시할 수 있는 단일 쿼리 또는 동적 관리 뷰(DMV)는 없습니다.

여러 클라이언트를 사용 하는 경우 hello 동일한 연결 문자열 hello 서비스가 각 로그인을 인증 합니다. 10 명의 사용자가 동시에 연결 하는 경우 동일한 사용자 이름과 암호를 사용 하 여 tooa 데이터베이스 hello, 10 개의 동시 로그인 있을 것입니다. 이 제한은 hello 로그인 및 인증의 toohello 기간에만 적용 됩니다. Hello 같은 10 사용자가 toohello 데이터베이스 순차적으로 연결 hello 동시 로그인 수는 1 보다 클 수 없습니다.

> [!NOTE]
> 현재이 제한을 toodatabases 탄력적 풀에 적용 되지 않습니다.
> 
> 

### <a name="maximum-sessions"></a>최대 세션 수
SQL 데이터베이스에서이 TRANSACT-SQL 쿼리를 실행 하는 현재 활성 세션의 toosee hello 수 있습니다:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

온-프레미스 SQL Server 작업을 분석 하는 경우 특정 데이터베이스에서 쿼리 toofocus hello를 수정 합니다. 이 쿼리 tooAzure SQL 데이터베이스를 이동 하려는 경우 hello 데이터베이스에 대 한 가능한 세션 요구를 확인할 수 있습니다.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

역시 이러한 쿼리도 지정 시간 수를 반환합니다. 시간이 지남에 따라 여러 샘플을 수집 하는 경우에 hello 잘 이해할 수 세션의 사용 해야 합니다.

SQL 데이터베이스 분석을 위해에 가져올 수 있습니다 기록 통계 세션 hello를 쿼리하여 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) 뷰와 hello 검토 **active_session_count** 열입니다. 
