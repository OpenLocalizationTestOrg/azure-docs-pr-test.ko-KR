---
title: "SQL 데이터베이스는 다중 테 넌 트 앱으로 로그 분석 aaaUse | Microsoft Docs"
description: "설정 하 고 hello Azure SQL 데이터베이스 샘플 Wingtip SaaS 응용 프로그램으로 로그 분석 (OMS) 사용"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>설정 하 고 로그 분석 (OMS) hello Wingtip SaaS 앱과 함께 사용

이 자습서에서는 탄력적 풀 및 데이터베이스 모니터링을 위해 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*를 설정 및 사용하는 방법을 알아봅니다. Hello에 기반 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md), 표시 방법을 toouse *로그 분석* tooaugment hello 모니터링 및 경고 hello Azure 포털에에서 제공 합니다. Log Analytics는 수백 개의 풀과 무수히 많은 데이터베이스를 지원하므로 특히 일정 규모의 모니터링 및 경고에 적합합니다. 또한 여러 Azure 구독에서 다양한 응용 프로그램과 Azure 서비스의 모니터링을 통합할 수 있는 단일 모니터링 솔루션을 제공합니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Log Analytics(OMS) 설치 및 구성
> * 로그 분석 toomonitor 풀 및 데이터베이스를 사용 하 여

toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

Hello 참조 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md) hello SaaS 시나리오 및 패턴 및 모니터링 솔루션의 hello 요구 사항에 미치는 영향에 대 한 내용은 합니다.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Log Analytics(OMS)를 통한 성능 모니터링 및 관리

SQL Database의 경우 데이터베이스 및 풀에 대한 모니터링 및 경고가 가능합니다. 이 기본 제공 모니터링 및 경고는 리소스 관련 및 적은 수의 리소스에 대 한 편리한 있지만 적합된 toomonitoring 대규모 설치를 통해 다양 한 리소스 및 구독 통합된 보기를 제공 하는 데 있습니다.

대규모 시나리오에서는 Log Analytics가 유용할 수 있습니다. 이것은 내보낸된 진단 로그를 통해 분석을 제공 하는 별도 Azure 서비스 및 원격 분석에서 여러 원격 분석을 수집할 수 있는 한 로그 분석 작업에서 수집 된 서비스 사용된 tooquery 수 및 경고를 설정 합니다. Log Analytics는 기본 제공 쿼리 언어와 데이터 시각화 도구를 제공하므로 운영 데이터 분석과 시각화가 가능합니다. SQL 분석 솔루션 hello 몇 가지 미리 정의 된 탄력적 풀 및 데이터베이스 모니터링 및 경고 보기와 쿼리를 제공 하 고 사용자가 직접 임시 쿼리를 추가 하 고 필요에 따라 이러한 저장 수 있습니다. OMS도 사용자 지정 뷰 디자이너를 제공합니다.

Azure 포털 hello와 OMS 로그 분석 작업 영역 및 분석 솔루션을 열 수 있습니다. hello Azure 포털 hello 최신 액세스 포인트 이지만 일부 지역에서는 hello OMS 포털 뒤에 있을 수 있습니다.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Hello 부하 생성기 toocreate 데이터 tooanalyze 시작

1. 열기 **데모 PerformanceMonitoringAndManagement.ps1** hello에 **PowerShell ISE**합니다. 이 스크립트를 열어 둡니다 toorun 원하는 수 만큼 여러 가지 hello 부하 생성 시나리오가이 자습서에서.
1. 보다 작거나 5 개 테 넌 트를 설정한 경우 테 넌 트 tooprovide 더 흥미로운 모니터링 컨텍스트의 일괄 처리를 프로 비전 합니다.
   1. Set **$DemoScenario = 1,** **Provision a batch of tenants**
   1. 키를 눌러 **F5** toorun hello 스크립트입니다.

1. Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**
1. 키를 눌러 **F5** toorun hello 스크립트입니다.

## <a name="get-hello-wingtip-application-scripts"></a>Hello Wingtip 응용 프로그램 스크립트 가져오기

hello Wingtip 티켓 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. 스크립트 파일은 %programfiles%\microsoft hello [학습 모듈 폴더](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)합니다. Hello 다운로드 **학습 모듈** 폴더 tooyour 로컬 컴퓨터의 폴더 구조를 유지 합니다.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>로그 분석 및 hello Azure SQL 분석 솔루션 설치 및 구성

로그 분석은 toobe 구성 해야 하는 별도 서비스입니다. Log Analytics는 로그 분석 작업 영역에 로그 데이터 및 원격 분석과 메트릭을 수집합니다. 작업 영역은 Azure의 다른 리소스와 마찬가지로 리소스이며 생성이 필요합니다. Hello 작업 영역에는 hello에서 만든 toobe 필요 하지 않은 동안 동일한 리소스 그룹으로 hello (가)는 모니터링, 이렇게 하면 hello 가장 적합 합니다. Hello hello Wingtip SaaS 응용 프로그램의 경우에서이 통해 hello 작업 영역 toobe 쉽게 hello 리소스 그룹을 삭제 하 여 hello 응용 프로그램을 삭제 합니다.

1. 열기... \\학습 모듈\\성능 모니터링 및 관리\\로그 분석\\*데모 LogAnalytics.ps1* hello에 **PowerShell ISE**합니다.
1. 키를 눌러 **F5** toorun hello 스크립트입니다.

이 시점에서 hello Azure 포털 (또는 hello OMS 포털)에 열기 로그 분석 수 있어야 합니다. Hello 로그 분석 작업 영역 및 toobecome 표시에서 수집 된 원격 분석 toobe 몇 분 정도 걸립니다. hello 긴 데이터 hello 더 흥미로운 hello 경험을 수집 하는 hello 시스템을 유지 됩니다. 이제는 것이 toograb 음료-정당한 hello 부하 생성기 여전히 실행 되 고 있는지 확인 하십시오!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>로그 분석을 사용 하 고 데이터베이스 및 SQL 분석 솔루션 toomonitor 풀 hello


이 연습에서는 로그 분석 및 hello 데이터베이스 및 풀에 대 한 수집 되 고 hello 원격 분석에 OMS 포털 toolook hello 엽니다.

1. Toohello 찾아보기 [Azure 포털](https://portal.azure.com) 및 더 많은 서비스를 클릭 하 여 로그 분석을 연 다음 로그 분석 검색:

   ![Log Analytics 열기](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. 명명 된 hello 작업 영역 선택 *wtploganalytics-&lt;사용자&gt;*합니다.

1. 선택 **개요** tooopen hello hello Azure 포털에서에서 로그 분석 솔루션입니다.
   ![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **중요 한**: 몇 분 전에 hello 솔루션은 현재 걸릴 수 있습니다. 기다려 주십시오.

1. 클릭 hello Azure SQL 분석 타일 tooopen에 합니다.

    ![개요](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![분석](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. hello 아래쪽 (필요한 경우 hello 블레이드 새로 고침)에 스크롤 막대가 hello 솔루션 블레이드 스크롤 옆으로 배치에서 보기를 hello 합니다.

1. 세로 hello hello의 시간 슬라이더가 hello에 사용할 수 있는 드릴 다운 탐색기에 또는 개별 리소스 tooopen에서을 클릭 하 여 다양 한 뷰 왼쪽 위 하거나 클릭 탐색 좁은 시간 조각에 toofocus의 모음입니다. 이 보기에서는 특정 리소스에 개별 데이터베이스 또는 풀 toofocus을 선택할 수 있습니다.

    ![차트](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Hello 솔루션 블레이드를 다시 맨 오른쪽 toohello 스크롤하면 나타납니다 tooopen에서을 클릭 하 고 탐색할 수 있는 몇 가지 저장 된 쿼리. 쿼리를 수정하여 실험해 보고, 작성한 쿼리 중 흥미로운 것은 저장하여 나중에 다른 리소스에서 다시 열어 사용할 수 있습니다.

1. Hello 로그 분석 작업 영역 블레이드에서 다시 OMS 포털 tooopen hello 솔루션을 선택 합니다.

    ![OMS](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. Hello OMS 포털의 경고를 구성할 수 있습니다. Hello 경고 hello 데이터베이스 DTU 보기 부분을 클릭 합니다.

1. Hello 로그 검색에에서 하면 표시 되는 보기 hello 메트릭 표시 되는 막대 그래프를 표시 됩니다.

    ![로그 검색](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Hello 도구 모음에서 경고를 클릭 하면 수 toosee hello에 대 한 경고 구성 되 고 변경할 수 있습니다.

    ![경고 규칙 추가 ](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

hello 모니터링 및 OMS 로그 분석 및의 경고는 hello 데이터 hello 리소스 별로 각 리소스 블레이드에서 경고와 달리 hello 작업 영역에 대해 쿼리를 기반으로 합니다. 따라서 데이터베이스마다 하나씩 정의하는 대신 모든 데이터베이스를 살피는 경고를 정의할 수 있습니다. 또는 여러 리소스 유형에 대한 복합 쿼리를 사용하는 경고를 작성합니다. 쿼리는 hello hello 작업 영역에서 사용할 수 있는 데이터에 의해서만 제한 됩니다.

SQL 데이터베이스에 대 한 로그 분석 hello 작업 영역에서 hello 데이터 볼륨에 따라에 대 한 청구 됩니다. 이 자습서에서는 하루에 제한 된 too500MB은 무료 작업 영역에서 만들었습니다. 한도 도달 하면 데이터 toohello 작업 영역을 더 이상 추가 됩니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]
> * Log Analytics(OMS) 설치 및 구성
> * 로그 분석 toomonitor 풀 및 데이터베이스를 사용 하 여

[테넌트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>추가 리소스

* [Hello 초기 Wingtip SaaS 응용 프로그램 배포를 구축 하는 추가 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
