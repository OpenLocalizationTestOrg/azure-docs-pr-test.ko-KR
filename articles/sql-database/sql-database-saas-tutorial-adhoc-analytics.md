---
title: "여러 Azure SQL 데이터베이스에 걸쳐 aaaRun 임시 분석 쿼리 | Microsoft Docs"
description: "Hello Wingtip SaaS 다중 테 넌 트 응용 프로그램에서 여러 SQL 데이터베이스에 걸쳐 임시 분석 쿼리를 실행 합니다."
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>모든 Wingtip SaaS 테넌트에서 임시 분석 쿼리 실행

이 자습서에서는 쿼리를 실행할 분산 테 넌 트 데이터베이스의 전체 집합 hello tooenable 임시 분석 합니다. 탄력적 쿼리는 사용 되는 tooenable 분산 쿼리, 추가 분석 데이터베이스를 배포 해야 (toohello 카탈로그 서버). 이러한 쿼리는 hello Wingtip SaaS 응용 프로그램의 hello 일상적인 운영 데이터에 포함 된 정보를 추출할 수 있습니다.


이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]

> * 각 데이터베이스에서 전역 뷰 hello에 대 한 수 있도록 하는 테 넌 트 간에 효율적인 쿼리
> * 어떻게 toodeploy 임시 분석 데이터베이스
> * Toorun 모든 테 넌 트 데이터베이스에서 쿼리를 분산 하는 방법



toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.
* SSMS(SQL Server Management Studio)가 설치되었습니다. SSMS 설치 하 고 toodownload 참조 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.


## <a name="ad-hoc-analytics-pattern"></a>임시 분석 패턴

Hello 좋은 기회 SaaS 응용 프로그램 중 하나 toouse hello 방대한 양의 hello 클라우드에 저장 하는 테 넌 트 데이터입니다. 이 데이터 toogain 이해력 hello 작업 및 응용 프로그램, 테 넌 트, 사용자, 기본 설정, 동작, 등의 사용을 사용 합니다. 이러한 정보는 기능 개발, 활용성 향상 및 기타 앱 및 서비스 투자를 유도할 수 있습니다.

단일 다중 테넌트 데이터베이스에 있을 때 이 데이터에 액세스하는 것은 쉽지만 잠재적인 수천 개의 데이터베이스 규모로 분산되는 경우는 그렇게 쉽지 않습니다. 한 가지 방법은 toouse [탄력적 쿼리](sql-database-elastic-query-overview.md), 분산된 된 집합의 공통 스키마로 데이터베이스 간 쿼리 할 수 있게 합니다. 탄력적 쿼리에서 단일을 사용 하 여 *h e a d* hello에 미러 테이블이 나 뷰가 (테 넌 트) 데이터베이스를 분산 하는 외부 테이블은 정의 되는 데이터베이스입니다. 쿼리를 제출할 toothis 헤드 데이터베이스는 컴파일된 tooproduce hello 쿼리 필요에 따라 toohello 테 넌 트 데이터베이스 적용의 부분으로 분산된 쿼리 계획 합니다. 탄력적 쿼리에서 hello 분할 맵을 사용 하 여 hello 테 넌 트 데이터베이스의 hello 카탈로그 데이터베이스 tooprovide hello 위치에 있습니다. 설정 및 쿼리는 일반 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)을 사용하여 바로 진행되며 Power BI 또는 Excel 같은 도구에서의 임시 쿼리를 지원합니다.

쿼리 hello 테 넌 트 데이터베이스를 배포 하 여 탄력적 쿼리 라이브 프로덕션 데이터에 대 한 즉시 정보를 제공 합니다. 그러나 탄력적인 쿼리는 잠재적으로 많은 데이터베이스에서 데이터를 가져오고, 쿼리 대기 시간이 해당 하는 쿼리에 대 한 보다 높은 수 tooa 단일 다중 테 넌 트 데이터베이스를 전송 됩니다. 디자인 toominimize hello 반환 되는 데이터를 쿼리할 때 주의 해야 합니다. 탄력적 쿼리는 종종 가장 자주 사용 하는 것과 반대로 toobuilding 또는 복잡 한 분석 쿼리 또는 보고서도 적은 양의 실시간 데이터를 쿼리 하기 위한 적합 합니다. 쿼리 성능이 좋지, hello 속도가 확인 [실행 계획](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) hello 쿼리의 어떤 부분 toohello 원격 데이터베이스와 반환 되는 데이터의 양을 아래로 밀어넣은 toosee 합니다. 때때로 테넌트 데이터를 분석 쿼리에 최적화된 전용 데이터베이스 또는 데이터 웨어하우스로 추출하는 경우 복잡한 분석 처리를 필요로 하는 쿼리가 효율적으로 제공됩니다. 이 패턴 hello에 대해서는 설명 [테 넌 트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md)합니다. 

## <a name="get-hello-wingtip-application-scripts"></a>Hello Wingtip 응용 프로그램 스크립트 가져오기

hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. [Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.

## <a name="create-ticket-sales-data"></a>티켓 판매 데이터 만들기

더 흥미로운 데이터 집합에 대해 쿼리를 toorun hello 티켓 생성기를 실행 하 여 티켓 판매 데이터를 만듭니다.

1. Hello에 *PowerShell ISE*개방형 hello... \\학습 모듈\\운영 분석\\임시 분석\\*데모 AdhocAnalytics.ps1* 스크립팅하고 hello 다음 값을 설정 합니다.
   * **$DemoScenario** = 1, **모든 부문에서 이벤트 티켓을 구입합니다**.
2. 키를 눌러 **F5** 하 hello 스크립트를 실행 하 고 티켓 판매를 생성 합니다. Hello 스크립트를 실행 하는 동안이 자습서에서는 hello 단계를 계속 합니다. hello에 hello 티켓 데이터를 쿼리 *임시 분산 쿼리를 실행* 섹션에서 toothat 연습을 얻으면 계속 실행 되므로 hello 티켓 생성기 toocomplete 동안 대기 합니다.

## <a name="explore-hello-global-views"></a>Hello 전역 보기를 탐색 합니다.

hello Wingtip SaaS 응용 프로그램 hello 테 넌 트 데이터베이스 스키마에 단일 테 넌 트 관점에서 정의 되며 테 넌 트 당 데이터베이스 모델을 사용 하 여 만들어집니다. 테넌트 전용 정보는 하나의 테이블 *Venue*에 존재하며 이 테이블에는 항상 하나의 행이 있고 따라서 기본 키가 없는 힙으로 실현됩니다. Hello 스키마의 다른 테이블과 관련 된 toobe 필요 하지 않은 toohello *장소* 존재할 수 없으므로 일반적인 사용 시에 테 넌 트 hello 데이터가 속한 확실 하지 않을 테이블입니다.

그러나 모든 데이터베이스를 쿼리할 때 반드시 테 넌 트 별로 분할 된 단일 논리 데이터베이스의 일부 이면 처럼 탄력적 쿼리가 hello 데이터를 처리할 수 있습니다. tooachieve 추가 toohello 테 넌 트 데이터베이스 테 넌 트 id에 전역으로 쿼리되지 않는 hello 테이블의 각 프로젝트에이 'g l o b 뷰 집합. 예를 들어 hello *VenueEvents* 보기 추가 계산 *VenueId* hello에서 toohello 열 프로젝션 *이벤트* 테이블입니다. 통해 hello hello 헤드 데이터베이스에서 외부 테이블을 정의 하 여 *VenueEvents* (아니라 hello 기반이 *이벤트* 테이블), 탄력적 쿼리는 기준으로 조인 아래로 수 toopush *VenueId* 각 원격 데이터베이스에서 (아닌 hello 헤드 데이터베이스) 병렬로 실행 될 수 있도록 합니다. 그 결과 쿼리가 많은 경우 성능이 크게 증가 하는 반환 되는 데이터 양을 hello 횟수가 상당히 줄어들게 됩니다. 이러한 전역 보기는 모든 테넌트 데이터베이스(및 *basetenantdb*)에서 미리 생성됩니다.

1. SSMS를 열고 및 [연결 toohello tenants1-&lt;사용자&gt; 서버](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)합니다.
2. **데이터베이스**를 확장하고 **contosoconcerthall**을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.
3. Hello hello 단일 테 넌 트 테이블과 hello 전역 보기 간 쿼리 tooexplore hello 차이 다음을 실행 합니다.

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

이러한 보기에서는 hello *VenueId* 을 hello 장소 이름의 접근 방식은 해시 고유한 값을 사용 하는 toointroduce 수으로 계산 합니다. 이 방법은 toohello도 이와 비슷하게 hello 테 넌 트 키 hello 카탈로그에서 사용 하기 위해 계산 됩니다.

hello의 tooexamine hello 정의 *운송 수단* 보기:

1. **개체 탐색기**에서 **contosoconcethall** > **뷰**를 확장합니다.

   ![뷰](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. **dbo.Venues**를 마우스 오른쪽 단추로 클릭합니다.
3. **뷰 스크립팅** > **CREATE** > **새 쿼리 편집기 창**를 선택합니다.

스크립트의 다른 hello *장소* toosee 뷰 hello 더 추가 하는 방법을 *VenueId*합니다.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>임시 분산 쿼리에 사용 되는 hello 데이터베이스 배포

이 연습 배포 hello *adhocanalytics* 데이터베이스입니다. 이 모든 테 넌 트 데이터베이스에서 쿼리 하는 데 hello 스키마를 포함 하는 hello 헤드 데이터베이스입니다. hello 데이터베이스는 기존 카탈로그 서버 hello 샘플 응용 프로그램의 모든 관리 관련 데이터베이스에 사용 되는 hello 서버 이며 배포 toohello입니다.

1. 열기... \\학습 모듈\\운영 분석\\임시 분석\\*데모 AdhocAnalytics.ps1* hello에 *PowerShell ISE* 및 집합 hello 다음 값:
   * **$DemoScenario** = 2, **임시 분석 데이터베이스 배포**.

2. 키를 눌러 **F5** toorun 스크립트 hello 만들고 hello *adhocanalytics* 데이터베이스입니다.

Hello 다음 섹션을 사용 하는 toorun 분산 쿼리에 사용할 수 있도록 스키마 toohello 데이터베이스를 추가 합니다.

## <a name="configure-hello-database-for-running-distributed-queries"></a>분산된 쿼리를 실행 하기 위한 hello 데이터베이스 구성

이 연습 모든 테 넌 트 데이터베이스에서 쿼리할 수 있는 스키마 (hello 외부 데이터 원본 및 외부 테이블 정의) toohello 임시 분석 데이터베이스를 추가 합니다.

1. SQL Server Management Studio를 열고 toohello hello 이전 단계에서 만든 임시 분석 데이터베이스를 연결 합니다. hello 데이터베이스의 이름 hello adhocanalytics 됩니다.
2. SSMS에서...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*을 엽니다.
3. Hello SQL 스크립트를 검토 하 고 hello 다음에 유의 하십시오.

   탄력적 쿼리는 데이터베이스 범위 자격 증명 tooaccess 각 hello 테 넌 트 데이터베이스를 사용합니다. 이 자격 증명 toobe hello는 모든 데이터베이스에서 사용할 수 있는 되어야 하며 일반적으로 데 필요한 tooenable 이러한 임시 쿼리 hello 최소 권한을 부여 해야 합니다.

    ![자격 증명 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   hello를 외부 데이터 원본에에서 정의 된 toouse hello 테 넌 트 분할 맵을 hello 카탈로그 데이터베이스입니다. 를 사용 하 여이 hello 외부 데이터 원본으로 쿼리는 hello 쿼리가 실행 될 때 hello 카달로그에 등록 하는 분산된 tooall 데이터베이스입니다. 이 초기화 스크립트 hello 현재 서버를 검색 하 여 hello 카탈로그 데이터베이스의 hello 위치를 가져옵니다 서버 이름은 각 배포에 대해 다르기 때문에 (@@servername) hello 스크립트가 실행 됩니다.

    ![외부 데이터 원본 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   hello 이전 섹션에서 설명 하 고 정의 된 전역 보기 hello를 참조 하는 외부 테이블 hello **배포 SHARDED(VenueId) =**합니다. 때문에 각 *VenueId* tooa 단일 데이터베이스 매핑됩니다 hello 다음 섹션에 나와 있는 것 처럼이 많은 시나리오에 대 한 성능이 향상 합니다.

    ![외부 테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   로컬 테이블 hello *VenueTypes* 만들고 채운입니다. 이 참조 데이터 테이블 모든 테 넌 트 데이터베이스에서 일반적으로 이므로 로컬 테이블로 사용 하 고 hello 일반 데이터로 채워진 나타낼 수 있습니다. 일부 쿼리 hello 줄어들 수 있습니다에 대 한 데이터의 양을 hello 테 넌 트 데이터베이스과 hello 간에 이동 *adhocanalytics* 데이터베이스입니다.

    ![테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   이런이 방식으로 참조 테이블을 포함 하는 경우 수 있는지 tooupdate hello 테이블 스키마 및 데이터 hello 테 넌 트 데이터베이스를 업데이트할 때마다.

4. 키를 눌러 **F5** toorun 스크립트 hello 및 hello 초기화 *adhocanalytics* 데이터베이스입니다. 

이제 배포된 쿼리를 실행하고 모든 테넌트 간에 정보를 수집할 수 있습니다.

## <a name="run-ad-hoc-distributed-queries"></a>임시 배포된 쿼리 실행

이제 해당 hello *adhocanalytics* 데이터베이스 설정 계속 진행 하 고, 일부 분산된 쿼리를 실행 합니다. Hello 쿼리 처리를 발생 하는에 대 한 hello 실행 계획을 포함 합니다. 

Hello 실행 계획을 검사할 때 세부 정보에 대 한 hello 계획 아이콘 위로 마우스를 가져가고 합니다. 

중요 한 toonote 설정은 **배포 SHARDED(VenueId) =** hello 외부 데이터 소스를 정의 하는 경우에 다양 한 시나리오에 대 한 성능이 향상 됩니다. 때문에 각 *VenueId* tooa 매핑합니다 단일 데이터베이스 필터링은 쉽게 실행 취소할 원격으로 반환 하면서만 hello 데이터 필요 합니다.

1. SSMS에서 \\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql*을 엽니다.
2. 연결 된 toohello 준수할 **adhocanalytics** 데이터베이스입니다.
3. 선택 hello **쿼리** 메뉴 **실제 실행 계획 포함**
4. Hello를 강조 표시 *현재 등록 되어 있는 지역?* 쿼리 및 키를 눌러 **F5**합니다.

   hello 쿼리 방법을 보여 주기 위해, hello 전체 장소 목록을 반환 하 고 쉬운지 tooquery 모든 테 넌 트와 각 테 넌 트의 데이터를 반환 합니다.

   Hello 계획 검사 하 고 hello 전체 비용 hello 원격 쿼리 하므로 진행 중인 tooeach 테 넌 트 데이터베이스와 hello 위치 정보를 선택 하면 단순히 we're 확인 합니다.

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. 다음 쿼리 선택 hello 및 키를 눌러 **F5**합니다.

   Hello 테 넌 트 데이터베이스 및 hello 로컬에서 데이터를 조인 하는이 쿼리 *VenueTypes* 테이블 (하므로 로컬은 hello에서 테이블 *adhocanalytics* 데이터베이스).

   Hello 계획을 검사 하 고 해당 hello 참조 하므로 각 테 넌 트의 위치 정보 (dbo 쿼리 비용의 대부분은 hello 원격 쿼리. 지역) 한 후 로컬 hello 사용 하 여 빠른 로컬 연결을 수행 *VenueTypes* 테이블 toodisplay hello에 대 한 알기 쉬운 이름.

   ![원격 및 로컬 데이터에 조인](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. 이제 선택 하는 hello *일 기준 hello 대부분 티켓 판매 된?* 쿼리 및 키를 눌러 **F5**합니다.

   이 쿼리는 좀 더 복잡한 조인 및 집계를 수행합니다. 중요 한 toonote은 대부분 hello 처리의 원격으로 수행 되 고 다시 한 번 당사는 다시 필요한 하루 각 장소 집계 티켓 판매 개수에 대 한 단일 행만 반환 하는 hello 행만입니다.

   ![쿼리](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]

> * 모든 테넌트 데이터베이스에서 분산 쿼리 실행
> * 임시 분석 데이터베이스를 배포 하 고 스키마 tooit toorun 분산 쿼리를 추가 합니다.


이제 hello 시도 [테 넌 트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md) tooexplore 더 복잡 한 분석 처리에 대 한 데이터 tooa 별도 분석 데이터베이스 추출...

## <a name="additional-resources"></a>추가 리소스

* 추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [탄력적 쿼리](sql-database-elastic-query-overview.md)
