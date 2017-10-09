---
title: "Azure SQL 데이터베이스에 대 한 aaaQuery performance insight | Microsoft Docs"
description: "쿼리 성능 모니터링 hello 대부분 CPU 사용 Azure SQL 데이터베이스에 대 한 쿼리를 식별 합니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Azure SQL 데이터베이스 Query Performance Insight
관리 하 고 관계형 데이터베이스의 hello 성능 조정 상당한 기술력과 시간 투자를 필요로 하는 어려운 과제가 되 고 합니다. Query Performance Insight 있습니다 toospend를 hello 다음을 제공 하 여 데이터베이스 성능 문제 해결 시간이 줄어듭니다.

* 데이터베이스 리소스(DTU) 사용에 대한 보다 자세한 정보를 확인합니다. 
* hello 잠재적으로 향상 된 성능을 위해 튜닝할 수 있는 CPU/기간/실행 수 별 상위 쿼리 합니다.
* 쿼리의 hello 세부 정보로 다운 기능 toodrill hello, 해당 텍스트 및 리소스 사용률의 기록 보기. 
* [SQL Azure 데이터베이스 관리자](sql-database-advisor.md)  



## <a name="prerequisites"></a>필수 조건
* Query Performance Insight를 위해서는 데이터베이스에서 [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx) 가 활성 상태여야 합니다. Hello 포털 tooturn 쿼리 저장소를 실행 하지 않는 경우 묻는 있습니다.

## <a name="permissions"></a>권한
hello 다음 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) 필요한 toouse Query Performance Insight 사용 권한은: 

* **판독기**, **소유자**, **참가자**, **SQL DB 참가자**, 또는 **SQL Server 참가자** 사용 권한은 tooview hello 리소스를 소비한 상위 쿼리 및 차트를 필요 합니다. 
* **소유자**, **참가자**, **SQL DB 참가자**, 또는 **SQL Server 참가자** 권한은 필요한 tooview 쿼리 텍스트입니다.

## <a name="using-query-performance-insight"></a>Query Performance Insight 사용
Query Performance Insight은 쉽게 toouse입니다.

* 열기 [Azure 포털](https://portal.azure.com/) 및 tooexamine 찾기 데이터베이스입니다. 
  * 왼쪽 메뉴의 지원 및 문제 해결에서 "Query Performance Insight"를 선택합니다.
* Hello 첫 번째 탭에서 상위 리소스 소비 쿼리의 hello 목록을 검토 합니다.
* 개별 쿼리 tooview 세부 정보를 선택 합니다.
* [SQL Azure 데이터베이스 관리자](sql-database-advisor.md) 를 열고 권장 사항을 사용할 수 있는지 확인합니다.
* 슬라이더를 사용 하 여 또는 관찰 간격 아이콘 toochange 확대/축소 합니다.
  
    ![성능 대시보드](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> 몇 시간 데이터는 SQL 데이터베이스 tooprovide query performance insight에 쿼리 저장소에서 캡처하지 toobe가 필요 합니다. 특정 기간 중 쿼리 저장소 활성화 되지 않았습니다 hello 데이터베이스에는 활동이 없는 경우 해당 기간을 표시할 때 hello 차트 비어 있게 됩니다. 실행하지 않는 경우 언제든지 쿼리 저장소를 활성화할 수 있습니다.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>최상위 CPU 소비 쿼리 검토
Hello에 [포털](http://portal.azure.com) 다음 hello지 않습니다.

1. Tooa SQL 데이터베이스를 검색 하 고 클릭 **모든 설정을** > **지원 + 문제 해결** > **쿼리 성능 통찰력**합니다. 
   
    ![Query Performance Insight][1]
   
    hello 상위 쿼리 보기 열리고 hello 상위 CPU 소비 쿼리 나열 됩니다.
2. 자세한 내용은 hello 차트 주위를 클릭 합니다.<br>hello 윗줄 표시 hello 데이터베이스에 대 한 전체 DTU %hello 바 표시 CPU (%) hello 선택한 간격 동안 선택한 hello 쿼리에서 사용 하는 동안 (경우에 예를 들어 **지난 주** 선택 되어 각 막대 1 일을 나타냅니다).
   
    ![최상위 쿼리][2]
   
    hello 아래쪽 표에 표시 쿼리 hello에 대 한 집계 된 정보를 나타냅니다.
   
   * 쿼리 ID – 데이터베이스 내 쿼리의 고유 식별자입니다.
   * 예측 가능한 간격 동안 쿼리당 CPU입니다(집계 함수에 따라 다름).
   * 쿼리당 기간입니다(집계 함수에 따라 다름).
   * 특정 쿼리에 대한 총 실행 수입니다.
     
     선택 하거나 개별 쿼리에 tooinclude의 선택을 취소 하거나 확인란을 사용 하 여 hello 차트에서 제외 합니다.
3. 데이터 만료 되 면 클릭 hello **새로 고침** 단추입니다.
4. 슬라이더 및 확대/축소 단추 toochange 관찰 간격을 사용 하 고 스파이크를 조사할 수 있습니다: ![설정](./media/sql-database-query-performance/zoom.png)
5. 필요에 따라 다른 보기를 원할 경우 **사용자 지정** 탭을 선택하고 다음을 설정합니다.
   
   * 메트릭(CPU, 기간, 실행 횟수)
   * 시간 간격(지난 24시간, 지난주, 지난달) 
   * 쿼리 수
   * 집계 함수
     
     ![설정](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>개별 쿼리 세부 정보 보기
tooview 쿼리 세부 정보:

1. 상위 쿼리의 hello 목록에서 쿼리를 클릭 합니다.
   
    ![세부 정보](./media/sql-database-query-performance/details.png)
2. hello 자세히 보기 열리고 hello 쿼리의 CPU 소비/기간/실행 수 시간에 따라 분리 됩니다.
3. 자세한 내용은 hello 차트 주위를 클릭 합니다.
   
   * Hello 막대는 hello 선택한 쿼리에 사용 된 CPU % 및 상위 차트에 전체 데이터베이스 DTU % 있는 줄을 보여 줍니다.
   * 두 번째 차트 hello 선택한 쿼리에 의해 총 기간을 보여 줍니다.
   * 아래쪽 차트 hello 선택한 쿼리에 의해 실행의 총 수를 보여 줍니다.
     
     ![쿼리 세부 정보][3]
4. 필요에 따라 슬라이더를 사용 하 여, 확대/축소 단추 또는 클릭 **설정을** toocustomize 쿼리 데이터 표시 방법을 또는 다른 기간 toopick 합니다.

## <a name="review-top-queries-per-duration"></a>기간당 최상위 쿼리 검토
최근 업데이트 Query Performance Insight의 hello, 잠재적인 병목 상태를 식별 하는 데 도움이 되는 두 개의 새 메트릭으로 소개: 기간 및 실행 수입니다.<br>

장기 실행 쿼리 긴 리소스 잠금, 다른 사용자를 차단 및 확장성 제한에 대 한 hello 가장 가능성이 있어야 합니다. 또한 hello 적합 한 최적화 됩니다.<br>

장기 실행 쿼리 tooidentify:

1. 선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기
2. 메트릭 toobe 변경 **기간**
3. 쿼리 수 및 관찰 간격 선택
4. 집계 함수 선택
   
   * **Sum** 은 전체 관찰 간격 동안 모든 쿼리 실행 시간을 합합니다.
   * **Max** 는 전체 관찰 간격에는 실행 시간이 최대였던 쿼리를 찾습니다.
   * **Avg** 찾습니다 모든 평균 실행 시간 쿼리 실행 하 고 보여 hello 이러한 평균은에서 위쪽입니다. 
     
     ![쿼리 기간][4]

## <a name="review-top-queries-per-execution-count"></a>실행 횟수당 최상위 쿼리 검토
실행 횟수가 높을 경우 데이터베이스 자체에는 영향을 주지 않고 리소스 사용량이 적어질 수 있지만 전체 응용 프로그램이 느려질 수도 있습니다.

경우에 따라 매우 높은 실행 횟수 않을 tooincrease 네트워크의 라운드트립 합니다. 왕복은 성능에 지대한 영향을 미칩니다. 서로 주체 toonetwork 대기 시간 및 toodownstream 서버 대기 시간입니다. 

예를 들어 여러 데이터 기반 웹 사이트 과도 하 게 모든 사용자 요청에 대해 hello 데이터베이스에 액세스 합니다. 연결 풀링을 사용 하면, hello 증가 하는 동안 네트워크 트래픽 및 hello 데이터베이스 서버의 처리 부하 성능이 떨어질 수 있습니다.  일반 조언을 라운드 트립 tooan 꼭 필요한 tookeep입니다.

tooidentify 쿼리 ("수 다 스러운") 쿼리를 자주 실행 합니다.

1. 선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기
2. 메트릭 toobe 변경 **실행 수**
3. 쿼리 수 및 관찰 간격 선택
   
    ![쿼리 실행 횟수][5]

## <a name="understanding-performance-tuning-annotations"></a>성능 튜닝 주석 이해
Query Performance Insight에서 작업 부하를 탐색 하는 동안 hello 차트 위에 세로 선이 있는 아이콘이 나타날 수 있습니다.<br>

이러한 아이콘은 주석으로, [SQL Azure 데이터베이스 관리자](sql-database-advisor.md)가 수행한 작업에 영향을 미치는 성능을 나타냅니다. 가리키기 주석으로 hello 동작에 대 한 기본 정보를 얻을 수 있습니다:

![쿼리 주석][6]

더 많은 tooknow 이나 관리자의 권장 구성 적용, hello 아이콘을 클릭 합니다. 작업의 세부 정보가 열립니다. 활성 권장 사항은 명령을 사용하여 바로 적용할 수 있습니다.

![쿼리 주석 세부 정보][7]

### <a name="multiple-annotations"></a>여러 주석.
이기는 확대/축소 수준 때문에 다른 닫기 tooeach 되는 주석 됩니다 get으로 축소 하나 있습니다. 이러한 경우 특수 아이콘이 표시됩니다. 이 아이콘을 클릭하면 그룹화된 주석 목록이 표시되는 새 블레이드가 열립니다.
쿼리 및 성능 튜닝 작업의 상관 관계 지정 toobetter 작업을 파악 하는 데 도움이 됩니다. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Query Performance Insight에 대 한 쿼리 저장소 구성을 hello 최적화
Query Performance Insight를 사용 하는 동안 다음 쿼리 저장소 메시지 hello를 발생할 수 있습니다.

* "이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다. 여기를 클릭 toolearn 자세한. "
* "이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다. 여기 toochange 설정 클릭 합니다. " 

이러한 메시지는 일반적으로 쿼리 저장소 수 toocollect 새 데이터가 없는 경우에 나타납니다. 

첫 번째 경우는 쿼리 저장소가 읽기 전용 상태이고 매개 변수가 최적으로 설정되었을 때 발생합니다. 쿼리 저장소의 크기를 늘리거나 쿼리 저장소를 지워서 이 문제를 해결할 수 있습니다.

![qds 단추][8]

두 번째 경우는 쿼리 저장소가 꺼져 있거나 매개 변수가 최적 상태로 설정되어 있지 않을 때 발생합니다. <br>아래 명령을 실행 하 여 또는 포털에서 직접 hello 보존 및 캡처 정책 및 사용 쿼리 저장소를 변경할 수 있습니다.

![qds 단추][9]

### <a name="recommended-retention-and-capture-policy"></a>권장된 보존 및 캡처 정책
보존 정책에는 다음과 같은 두 종류가 있습니다.

* 크기 기반-에 도달 하면 집합 tooAUTO 최대 크기 근처 자동으로 데이터를 정리 합니다.
* 시간 기반-기본적으로 설정 됩니다 म too30 일, 즉, 쿼리 저장소, 공간 부족을 삭제 하는 30 일 보다 오래 된 정보를 쿼리할

캡처 정책은 다음과 같이 설정할 수 있습니다.

* **모두** – 모든 쿼리를 캡처합니다.
* **자동** – 컴파일 및 실행 기간이 중요하지 않고 사용 빈도가 적은 쿼리가 무시됩니다. 실행 횟수, 컴파일 및 런타임 기간에 대한 임계값을 내부적으로 결정합니다. Hello 기본 옵션입니다.
* **없음** – 쿼리 저장소에서 새 쿼리의 캡처를 중지하지만 이미 캡처된 쿼리에 대한 런타임 통계는 계속 수집됩니다.

모든 정책 tooAUTO 및 정리 정책 too30 (일)을 설정 하는 것이 좋습니다.

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

쿼리 저장소의 크기를 늘립니다. 연결 tooa 데이터베이스에서 수행 하 고 쿼리 다음 발급 수 있습니다.

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

하지만 쿼리 저장소를 지울 수 toowait 않도록 이러한 설정을 적용 하는 새 쿼리를 수집 하는 쿼리 저장소 결국 확인 합니다. 

> [!NOTE]
> 다음 쿼리를 실행 하는 hello 쿼리 저장소에에서 현재 정보를 모두 삭제 됩니다. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>요약
Query Performance Insight의 쿼리 작업이 hello 영향 및 toodatabase 리소스 사용의 관계를 이해 하도록 도와 줍니다. 이 기능을 hello 가장 쿼리를 많이 사용 되는 방법을 알아봅니다 쿼리하고 문제가 해지기 전에 hello 것 toofix 쉽게 식별할 수 합니다.

## <a name="next-steps"></a>다음 단계
SQL 데이터베이스의 hello 성능 향상에 대 한 자세한 내용은 클릭 [권장 사항을](sql-database-advisor.md) hello에 **Query Performance Insight** 블레이드입니다.

![성능 관리자](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

