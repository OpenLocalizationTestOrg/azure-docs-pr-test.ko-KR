---
title: "다중 테 넌 트 SaaS 응용 프로그램에서 많은 Azure SQL 데이터베이스의 aaaMonitor 성능을 | Microsoft Docs"
description: "모니터링 및 관리 데이터베이스 및 hello Azure SQL 데이터베이스 Wingtip SaaS 응용 프로그램 풀의 성능"
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
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Hello Wingtip SaaS 응용 프로그램의 성능을 모니터링합니다

이 자습서에서는 SaaS 응용 프로그램에서 사용되는 몇 가지 주요 성능 관리 시나리오를 살펴봅니다. 부하 생성기 toosimulate 동작을 사용 하 여 모든 테 넌 트 데이터베이스에서 기본 제공 모니터링 hello 및 SQL 데이터베이스와 탄력적 풀의 경고 기능을 보여 줍니다.

hello Wingtip SaaS 앱 각 장소 (테 넌 트)의 해당 데이터베이스에 있는 단일 테 넌 트 데이터 모델을 사용 합니다. 대부분의 SaaS 응용 프로그램 처럼 hello 테 넌 트 작업 부하 패턴은 드물게 발생 하 고 예측할 수 없는 것으로 예상 합니다. 예를 들어 티켓 판매는 아무 때나 발생할 수 있습니다. tootake 활용이 일반적인 데이터베이스 사용 패턴, 테 넌 트 데이터베이스를 탄력적 데이터베이스 풀으로 배포 됩니다. 탄력적 풀에서 많은 데이터베이스 리소스를 공유 하 여 솔루션의 hello 비용을 최적화 합니다. 이 유형의 패턴을는 중요 한 toomonitor 데이터베이스 균등 하 게 풀 리소스 사용량 tooensure 로드 하는 합리적으로 풀에 걸쳐 있습니다. 또한 개별 데이터베이스에 리소스가 충분 한지 및 풀에 도달 하지 tooensure 해야 자신의 [eDTU](sql-database-what-is-a-dtu.md) 제한 합니다. 이 자습서 방법으로 toomonitor 탐색 하 고 데이터베이스 및 풀 관리 방법과 tootake 작업에서 응답 toovariations에 정정 작업입니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]

> * 제공 된 부하 생성기를 실행 하 여 hello 테 넌 트 데이터베이스에서의 사용을 시뮬레이션 합니다.
> * 올바르게 응답 하지 않는 부하 toohello 증가 하는 대로 모니터 hello 테 넌 트 데이터베이스
> * 탄력적 풀 응답 toohello 높아지는 데이터베이스 부하에 hello 수직 확장
> * 두 번째 탄력적 풀 tooload 균형 데이터베이스 활동을 프로 비전


toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

## <a name="introduction-toosaas-performance-management-patterns"></a>소개 tooSaaS 성능 관리 패턴

데이터베이스 성능 관리 컴파일 및 성능 데이터 분석 및 다음 매개 변수 toomaintain 응용 프로그램에 대 한 적절 한 응답 시간을 조정 하 여 toothis 데이터 반응으로 구성 됩니다. 여러 테 넌 트를 호스팅하는 경우 탄력적 데이터베이스 풀은 비용 효율적인 방식으로 tooprovide 하 고 예측할 수 없는 작업이 있는 데이터베이스 그룹에 대 한 리소스를 관리 합니다. 특정 워크로드 패턴의 경우 풀에서 관리하면 S3 데이터베이스 두 개만 이점을 얻을 수 있습니다.

![미디어](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

풀 및 풀의 hello 데이터베이스 모니터링된 tooensure 성능의 허용 가능한 범위 내에서 유지 해야 합니다. 튜닝 hello 풀 구성 toomeet hello 작업의 요구 사항을 hello 집계는 hello 풀 Edtu hello에 대 한 적절 한 되도록 하는 모든 데이터베이스의 전체 작업 합니다. 값을 조정 hello 데이터베이스당 min 및 데이터베이스당 최대 eDTU 값 tooappropriate 특정 응용 프로그램 요구 사항에 대 한 합니다.

### <a name="performance-management-strategies"></a>성능 관리 전략

* tooavoid toomanually 모니터 성능 있는 것이 가장 효과적 너무**일반 범위를 벗어나는 들어가지 않도록 데이터베이스 또는 풀을 트리거할 경고 설정**합니다.
* toorespond tooshort 용어 변동은 풀의 hello 집계 성능 수준에 hello **풀 eDTU 수준 위로 또는 아래로 확장 될 수 있습니다**합니다. 이 변동 정기적으로 또는 예측 가능한 단위로 발생 하는 경우 **hello 풀 크기 조정 toooccur 예약된을 자동으로 될 수 있습니다**합니다. 예를 들어 워크로드가 가볍다고 알고 있는 경우 야간 또는 주말 중으로 규모를 축소할 수 있습니다.
* toorespond toolonger 용어 변동 사항이 나 변경 사항을 hello 데이터베이스 개수, **개별 데이터베이스를 다른 풀으로 이동할 수 있습니다**합니다.
* toorespond tooshort 용어 증가 *개별* 데이터베이스 로드 **개별 데이터베이스를 풀에서 제거 하 고 개별 성능 수준이 할당 수**합니다. Hello 부하는 감소 되 면 hello 데이터베이스 수 다음 반환할 toohello 풀입니다. 이 배열은 미리 알려져 있는 경우 데이터베이스는 이동할 수 미리 tooensure hello 데이터베이스 항상에 필요한 hello 리소스 및 tooavoid 영향 hello 풀의 다른 데이터베이스에 있습니다. 이 요구 사항을 발생 하는 인기 있는 이벤트에 대 한 티켓 판매 러시 장소 같은 예측 가능한 경우이 관리 동작은 hello 응용 프로그램에 통합할 수 있습니다.

hello [Azure 포털](https://portal.azure.com) 기본 제공 모니터링 및 대부분의 리소스에 경고를 제공 합니다. SQL Database의 경우 데이터베이스 및 풀에 대한 모니터링 및 경고가 가능합니다. 이 기본 제공 모니터링 및 경고 리소스 관련 이므로 적은 수의 리소스에 대 한 편리한 toouse 이지만 많은 리소스를 작업할 때 매우 편리 하 게 됩니다.

여러 리소스로 작업하는 대규모 시나리오의 경우 [Log Analytics(OMS)](sql-database-saas-tutorial-log-analytics.md)를 사용할 수 있습니다. 이것은 여러 서비스에서 원격 분석을 수집하고 쿼리 및 경고 설정에 사용할 수 있는 Log Analytics 작업 영역에서 수집된 로그 분석 많은 서비스에서 원격 분석 수집 및 수 사용된 tooquery 있으며 경고를 설정 합니다.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Hello Wingtip 응용 프로그램 소스 코드 및 스크립트 가져오기

hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. [Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.

## <a name="provision-additional-tenants"></a>추가 테넌트 프로비전

풀 하는 두 개의 점으로만 S3 데이터베이스와 함께 비용 효율적인 동안 hello 자세한에 있는 데이터베이스는 비용 효율적인 hello 풀 hello 효과 평균을 구하여 hello 됩니다. 성능 모니터링과 관리가 규모별로 작동하는 방법을 잘 이해하기 위해 이 자습서에서 적어도 20개의 데이터베이스를 배포해야 합니다.

이미 이전 자습서의 테 넌 트의 일괄 처리를 프로 비전, toohello 건너뜁니다 [모든 테 넌 트 데이터베이스에서 시뮬레이션 사용량이](#simulate-usage-on-all-tenant-databases) 섹션.

1. 열기... \\학습 모듈\\성능 모니터링 및 관리\\*데모 PerformanceMonitoringAndManagement.ps1* hello에 *PowerShell ISE*합니다. 이 자습서를 실행하는 동안 여러 시나리오를 실행할 때 이 스크립트를 열어 두세요.
1. **$DemoScenario** = **1**, **Provision a batch of tenants** 설정
1. 키를 눌러 **F5** toorun hello 스크립트입니다.

hello 스크립트는 5 분 이내에 17 테 넌 트를 배포 합니다.

hello *새로 TenantBatch* 스크립트 중첩 또는 연결 된 집합을 사용 하 여 [리소스 관리자](../azure-resource-manager/index.md) 기본적으로 hello 데이터베이스를 복사 하는 테 넌 트, 일괄 처리를 만드는 템플릿을 **basetenantdb** hello 카탈로그 server toocreate hello 새 테 넌 트 데이터베이스를 만든 다음 등록 hello 카탈로그에서 이러한 및 마지막으로 형식과 hello 테 넌 트 이름 및 위치를 초기화 합니다. 이 hello 방식으로 hello 앱 프로 비전 하는 새 테 넌 트와 일치 합니다. 변경 내용을 너무*basetenantdb* 적용된 tooany 새 테 넌 트 그 후 사용자를 프로 비전 됩니다. Hello 참조 [스키마 관리 자습서](sql-database-saas-tutorial-schema-management.md) toomake 스키마 너무 어떻게 변경 되는지 toosee*기존* 데이터베이스 테 넌 트 (hello를 포함 하 여 *basetenantdb* 데이터베이스).

## <a name="simulate-usage-on-all-tenant-databases"></a>모든 테넌트 데이터베이스에 대한 사용 시뮬레이션

hello *데모 PerformanceMonitoringAndManagement.ps1* 스크립트는 모든 테 넌 트 데이터베이스에 대해 실행 되는 작업 부하를 시뮬레이션 하는 제공 합니다. hello 부하 hello 사용 가능한 부하 시나리오 중 하나를 사용 하 여 생성 됩니다.

| 데모 | 시나리오 |
|:--|:--|
| 2 | 표준 강도 부하(약 40 DTU) 생성 |
| 3 | 데이터베이스별로 버스트가 더 길고 더 잦은 부하 생성|
| 4 | 데이터베이스별로 DTU 버스트가 더 높은(약 80 DTU) 부하 생성|
| 5 | 표준 부하에 더하여 단일 테넌트의 높은 부하 생성(약 95 DTU)|
| 6 | 여러 풀에 걸쳐 불균형 부하 생성|

hello 부하 생성기 적용 되는 *가상* CPU 전용 로드 tooevery 테 넌 트 데이터베이스입니다. hello 생성기 호출 하는 저장된 프로시저 주기적으로 hello 부하를 생성 하는 각 테 넌 트 데이터베이스에 대 한 작업을 시작 합니다. hello 부하 수준 (Edtu), 지속 시간 및 간격을 예측할 수 없는 테 넌 트 작업을 시뮬레이션 하는 모든 데이터베이스에 걸쳐 다양 합니다.

1. 열기... \\학습 모듈\\성능 모니터링 및 관리\\*데모 PerformanceMonitoringAndManagement.ps1* hello에 *PowerShell ISE*합니다. 이 자습서를 실행하는 동안 여러 시나리오를 실행할 때 이 스크립트를 열어 두세요.
1. **$DemoScenario** = **2**를 설정하고, *일반 강도 부하를 생성*합니다.
1. 키를 눌러 **F5** tooapply 부하 tooall 테 넌 트 데이터베이스.

Wingtip SaaS 앱 이며 SaaS 앱에 대 한 hello 실제 부하는 일반적으로 드물게 발생 하 고 예측할 수 없는 합니다. toosimulate이 임의 부하를 모든 테 넌 트 간의 분산 hello 부하 생성기 생성 합니다. 몇 분 정도 hello 다음 섹션에서에서 toomonitor hello 부하를 시도 하기 전에 3-5 분 동안 hello 부하 생성기를 실행 하므로 hello 부하 패턴 tooemerge 필요 합니다.

> [!IMPORTANT]
> hello 부하 생성기는 일련의 작업으로 로컬 PowerShell 세션에서 실행 중입니다. Hello 유지 *데모 PerformanceMonitoringAndManagement.ps1* 탭 열기! Hello 탭을 종료 하거나 컴퓨터를 일시 중단, hello 부하 생성기를 중지 합니다. hello 부하 생성기에 남아는 *작업 호출* 상태 hello 생성기 시작 된 후 프로 비전 되는 새 테 넌 트에 부하를 생성 합니다. 사용 하 여 *Ctrl-c* toostop 새 작업 및 끝내기 hello 스크립트를 호출 합니다. hello 부하 생성기는 toorun, 기존 테 넌 트에만 계속 합니다.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 리소스 사용 모니터링

적용 되 고 결과 hello에서 로드 하는 toomonitor hello 자원 배정 현황 hello 테 넌 트 데이터베이스를 포함 하는 hello 포털 toohello 풀을 엽니다.

1. 열기 hello [Azure 포털](https://portal.azure.com) toohello 찾아보기 및 *tenants1-&lt;사용자&gt;*  서버입니다.
1. 아래로 스크롤하여 탄력적 풀을 찾은 다음 **Pool1**을 클릭합니다. 이 풀에는 지금까지 만든 모든 hello 테 넌 트 데이터베이스 포함 되어 있습니다.

Hello 관찰 **탄력적 풀 모니터링** 및 **탄력적 데이터베이스 모니터링** 차트입니다.

hello 풀의 리소스 사용률은 hello 풀의 모든 데이터베이스에 대 한 hello 집계 데이터베이스 사용. hello 데이터베이스 차트 hello 5 개의 가장 많이 사용 데이터베이스를 보여 줍니다.

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Hello 풀 외에 추가 데이터베이스 때문에 상위 5 개 hello, hello 풀 사용률이 hello 상위 5 개 데이터베이스가 차트에 반영 되지 않은 활동을 보여 줍니다. 추가 세부 정보를 보려면 **데이터베이스 리소스 사용률**을 클릭합니다.

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Hello 풀에서 성능 경고를 설정 합니다.

트리거를 실행 하는 hello 풀에 대 한 경고를 설정 \>다음과 같이 사용률이 75%:

1. 열기 *Pool1* (hello에 *tenants1-\<사용자\>*  서버) hello에 [Azure 포털](https://portal.azure.com)합니다.
1. **경고 규칙**, **+ 경고 추가**를 차례로 클릭합니다.

   ![경고 추가](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. **높은 DTU** 등과 같은 이름을 제공
1. Hello 다음 값을 설정 합니다.
   * **메트릭 = eDTU 백분율**
   * **조건 = 보다 큼**.
   * **임계값 = 75**.
   * **'를 ' hello를 통해 마지막 30 분**합니다.
1. 전자 메일 주소 toohello 추가 *추가 관리자 email(s)* 상자 한 클릭 **확인**합니다.

   ![경고 설정](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>사용 중인 풀 확장

Hello 집계 부하 수준을 최대한 활용 hello 풀 eDTU 사용량 100%에 도달 하는 풀 toohello 지점에 증가 한 다음 개별 데이터베이스 성능 영향을, hello 풀의 모든 데이터베이스에 대 한 쿼리 응답 시간이 느려질 수 있으므로 잠재적으로.

**단기**, hello 풀 tooprovide 추가 리소스를 확장 하거나 hello 풀에서 데이터베이스를 제거 하십시오 (옮겨 tooother 풀, 내부 또는 외부로 hello 풀 tooa 독립 실행형 서비스 계층).

**장기적인**, 쿼리를 최적화 하는 것이 좋습니다. 또는 인덱스 사용 tooimprove 데이터베이스 성능. Hello에 따라 응용 프로그램의 민감도 tooperformance 발급의 모범 사례 tooscale를 풀 eDTU 사용량 100%에 도달 하기 전에 합니다. 경고 toowarn를 사용 하 여 사전에 있습니다.

Hello 생성기에서 생성 된 hello 부하가 증가 하 여 사용 중인 풀을 시뮬레이션할 수 있습니다. 인해 hello 데이터베이스 tooburst 더 자주 및 총 부하를 증가, 더 긴 hello에 대 한 hello 풀에 hello 요구 사항을 hello 개별 데이터베이스를 변경 하지 않고 있습니다. Hello 풀 수직 확장은 hello 포털 또는 PowerShell에서 쉽게 설정할 수 있습니다. 이 연습에서는 hello 포털을 사용 합니다.

1. 설정 *$DemoScenario* = **3**, _데이터베이스당 더 긴를 더 자주 필요 생성 부하_ 의 hello 집계 로드 tooincrease hello 강도 각 데이터베이스에 필요한 hello 최대 부하를 변경 하지 않고 hello 풀입니다.
1. 키를 눌러 **F5** tooapply 부하 tooall 테 넌 트 데이터베이스.

1. 너무 이동**Pool1** hello Azure 포털의에서.

모니터 hello hello 위쪽 차트에서 풀 eDTU 사용량을 증가합니다. Hello 새 더 높은 부하 tookick 몇 분 정도 걸리는 있고 toohit 최대 사용률을 시작 하는 hello 풀 신속 하 게 나타납니다 신속 하 게 hello 풀 오버 로드 hello 부하 hello 새 패턴으로 steadies,으로 합니다.

1. tooscale hello 풀을 클릭 하 여 **풀 구성** hello의 hello 위쪽 **Pool1** 페이지.
1. Hello 조정 **풀 eDTU** 너무 설정**100**합니다. Hello 풀 edtu로 변경 하는 경우에 (이 여전히 데이터베이스당 최대 50 eDTU) hello 데이터베이스당 설정을 변경 하지 않습니다. Hello hello 오른쪽에 hello 데이터베이스당 설정을 볼 수 있습니다 **풀 구성** 페이지.
1. 클릭 **저장** toosubmit hello 요청 tooscale hello 풀입니다.

너무 돌아가서**Pool1** > **개요** tooview hello 차트를 모니터링 합니다. Hello (몇 개의 데이터베이스와 임의 로드가 하지는 않지만 항상 쉽게 toosee 내릴 일정 시간 동안 실행 될 때까지) hello 풀 더 많은 리소스를 제공 하는 효과 모니터링 합니다. 보고 동안 hello 차트 약 염두에서 100 %hello 위쪽에 hello에 낮은 차트 100 %hello 여전히 50 Edtu 데이터베이스당 최대는 여전히 50 Edtu를으로 이제 차트 100 Edtu를 나타냅니다.

데이터베이스는 온라인 상태이 고 hello 프로세스 전체에서 완벽 하 게 사용할 수 있는 상태로 유지 합니다. Hello에서 마지막 순간 각 데이터베이스는 준비 toobe hello 새 풀 eDTU를 사용 하도록 설정 하는 대로 모든 활성 연결 분리 됩니다. 응용 프로그램 코드 삭제 tooretry 연결 작성 항상 등과 toohello 데이터베이스 hello 수직 풀의 데이터베이스를 다시 연결 됩니다.

## <a name="load-balance-between-pools"></a>풀 간의 부하 분산

대체는 tooscaling hello 풀을 두 번째 풀을 만들고 데이터베이스 테이블로 이동 toobalance hello 두 개의 풀을 hello 간의 로드 합니다. 에이 hello 새 풀을 만들어야 toodo hello와 동일한 서버를 먼저 hello 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com)개방형 hello **tenants1-&lt;사용자&gt;**  서버입니다.
1. 클릭 **+ 새 풀** toocreate hello 현재 서버에서 풀입니다.
1. Hello에 **탄력적 데이터베이스 풀** 템플릿:

    1. 설정 **이름** 너무*Pool2*합니다.
    1. 가격 책정 계층으로 hello 둡니다 **표준 풀**합니다.
    1. **구성 풀**을 클릭합니다.
    1. 설정 **풀 eDTU** 너무*50 eDTU*합니다.
    1. 클릭 **데이터베이스를 추가할** toosee 너무 추가할 수 있는 hello 서버의 데이터베이스 목록이*Pool2*합니다.
    1. 모든 10 개의 데이터베이스 toomove 이러한 toohello 새 풀을 선택한 다음 클릭 **선택**합니다. Hello 부하 생성기를 실행 된 했으므로, 경우 hello 서비스 이미 알고 있는 성능 프로필 hello 기본 50 eDTU 크기 보다 더 큰 풀 걸리며 100 eDTU 설정으로 시작 하는 것이 좋습니다.

    ![권장 사항](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. 이 자습서에 대 한 hello 기본 50 Edtu 하 고 클릭 **선택** 다시 합니다.
    1. 선택 **확인** toocreate hello 새 풀 및 toomove hello에 데이터베이스를 선택 합니다.

Hello 풀을 만들고 hello 데이터베이스 이동 하는 몇 분이 걸립니다. 데이터베이스를 이동 하는 마지막 순간 hello까지 온라인 상태이 고 완전히 액세스할 수 있도록 유지 하는 대로 이때 모든 열린 연결이 닫힙니다. 몇 가지 재시도 논리를 설정한 상태로 클라이언트는 다음 toohello 데이터베이스 hello 새 풀에 연결 합니다.

너무 찾아보기**Pool2** (hello에 *tenants1* 서버) tooopen 풀 hello 및 성능을 모니터링 합니다. 표시 되지 않는 경우 프로 비전 hello 새 풀 toocomplete을 기다립니다.

이제 *Pool1*의 리소스 사용량이 떨어지고 *Pool2*에 유사한 부하가 걸려 있는 것으로 나타나야 합니다.

## <a name="manage-performance-of-a-single-database"></a>단일 데이터베이스의 성능 관리

Hello 풀 구성에 따라 지속적인된 높은 부하에서 발생 하는 풀에서 단일 데이터베이스의 경우 hello 풀의 toodominate hello 리소스는 경향이 및 다른 데이터베이스에 영향을 줄 수 것입니다. Hello 작업이 일정 시간 동안 가능성이 toocontinue 인 경우 hello 풀에서 hello 데이터베이스를 일시적으로 이동할 수 있습니다. 이렇게 하면 hello 데이터베이스 toohave hello 추가 리소스가 필요한 하 고 다른 데이터베이스 hello에서 격리 합니다.

이 연습 티켓 인기 있는 함께 대 한 판매에 이동 하는 경우 높은 부하가 발생 하는 Contoso 함께 Hall의 hello 효과 시뮬레이션 합니다.

1. Hello 열기... \\ *데모 PerformanceMonitoringAndManagement.ps1* 스크립트입니다.
1. **$DemoScenario = 5를 설정하고, 표준 부하에 더하여 단일 테넌트에 대한 높은 부하(약 95 DTU)를 생성합니다.**
1. **$SingleTenantDatabaseName = contosoconcerthall** 설정
1. 사용 하 여 hello 스크립트 실행 **F5**합니다.


1. Hello에 [Azure 포털](https://portal.azure.com) 열고 **Pool1**합니다.
1. Hello 검사 **탄력적 풀 모니터링** 차트 및 풀 eDTU 사용량 증가 hello 찾아보십시오. 2 분 정도로 후 hello 더 높은 부하에서 tookick 시작 해야 하 고 hello 풀 사용률이 100%에 도달 있는지 신속 하 게 나타납니다.
1. Hello 검사 **탄력적 데이터베이스 모니터링** 지난 시간 hello에서 hello 가장 많이 사용 데이터베이스를 보여 주는 표시 합니다. hello *contosoconcerthall* hello 5 가장 많이 사용 하는 데이터베이스 중 하나로 데이터베이스 곧 나타납니다.
1. **Hello 탄력적 데이터베이스 모니터링 클릭** **차트** hello 열리는 **데이터베이스 리소스 사용률** hello 데이터베이스를 모니터링할 수 있는 페이지. 이렇게 하면 hello에 대 한 hello 표시 격리 *contosoconcerthall* 데이터베이스입니다.
1. 데이터베이스의 hello 목록에서 클릭 **contosoconcerthall**합니다.
1. 클릭 **가격 책정 계층 (배율 Dtu)** tooopen hello **성능을 구성** 페이지 hello 데이터베이스에 대 한 독립 실행형 성능 수준을 설정할 수 있습니다.
1. Hello 클릭 **표준** hello 표준 계층에 tooopen hello 크기 조정 옵션을 탭 합니다.
1. Hello 슬라이드 **DTU 슬라이더** tooright tooselect **100** Dtu입니다. 참고가 해당 toohello 서비스 목표 **S3**합니다.
1. 클릭 **적용** toomove hello hello 풀에서 데이터베이스와 쉽게는 *표준 S3* 데이터베이스입니다.
1. 크기 조정 되 면 완료, hello contosoconcerthall 데이터베이스에는 모니터 hello 영향 및 hello 탄력적 풀 및 데이터베이스 블레이드에서 Pool1 합니다.

Hello contosoconcerthall 데이터베이스에 로드 양이 많으면 hello subsides 되 면 신속 하 게 반환 해야 toohello 풀 tooreduce 비용입니다. 확실 하지 않으면 하는 경우에 설정할 수 있습니다 경고 hello 데이터베이스에 있는 수행 됩니다 트리거할 해당 DTU 사용량 hello 데이터베이스당 아래로 떨어질 경우 hello 풀에 최대 합니다. 풀로 데이터베이스 이동은 연습 5에서 설명합니다.

## <a name="other-performance-management-patterns"></a>다른 성능 관리 패턴

**선점형 배율** hello 실습 위의 방법을 tooscale 격리 된 데이터베이스를 알고 있는 데이터베이스 toolook에 대 한 탐색 있습니다. Contoso 함께 Hall의 hello 관리에 Wingtips hello 임박 했음을 알리는 티켓이 판매 정보를 얻으려면 경우 hello 데이터베이스 이동 되었을 hello 풀에서 미리 합니다. 그렇지 않으면 가능성이 필요 했을 것 hello 풀 또는 hello 데이터베이스 toospot에 알림을 일어나 되었습니다. 이 대 한 hello에서 toolearn hello 풀 성능 저하의 메시지가에 다른 테 넌 트 않을 있습니다. 와 경우 hello 테 넌 트 hello 풀에서 Azure 자동화 runbook toomove hello 데이터베이스를 설정할 수 있으며 다음 백업에서 다시 정의 된 일정에 따라 추가 리소스는 필요한 기간을 예측할 수 있습니다.

**테 넌 트 셀프 서비스 크기 조정** 배율 쉽게 hello 관리 API 통해 호출 하는 작업 이기 때문에 쉽게 hello 기능 tooscale 테 넌 트 데이터베이스를 테 넌 트 웹 응용 프로그램에 빌드하고 수 SaaS 서비스의 기능으로 제공 합니다. 예를 들어 self-administer 아마도 직접 연결 된 위쪽 / 아래쪽 크기 조정 하는 테 넌 트를 통해 tootheir 청구!

**일정 toomatch 사용 패턴에 위와 아래로 풀 크기 조정**

집계 테 넌 트 사용은 예측 가능한 사용 패턴을 따릅니다, 여기서 아래로 일정에 따라 Azure 자동화 tooscale 풀을 사용할 수 있습니다. 예를 들어 리소스 요구 사항이 떨어지는 것으로 알고 있는 평일 오후 6시 후에 풀을 축소하고 오전 6시 전에 다시 확장할 수 있습니다.



## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 제공 된 부하 생성기를 실행 하 여 hello 테 넌 트 데이터베이스에서의 사용을 시뮬레이션 합니다.
> * 올바르게 응답 하지 않는 부하 toohello 증가 하는 대로 모니터 hello 테 넌 트 데이터베이스
> * 탄력적 풀 응답 toohello 높아지는 데이터베이스 부하에 hello 수직 확장
> * 두 번째 탄력적 풀 tooload 균형 hello 데이터베이스 활동을 프로 비전

[단일 테넌트 복원 자습서](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>추가 리소스

* 추가 [hello Wingtip SaaS 응용 프로그램 배포를 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [SQL 탄력적 풀](sql-database-elastic-pool.md)
* [Azure Automation](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) - Log Analytics 설정 및 사용 자습서
