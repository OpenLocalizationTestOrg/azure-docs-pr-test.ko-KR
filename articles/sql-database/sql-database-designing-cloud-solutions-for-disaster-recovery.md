---
title: "Azure SQL 데이터베이스를 사용 하 여 aaaDesign 항상 사용 가능한 서비스 | Microsoft Docs"
description: "Azure SQL Database를 사용하여 항상 사용 가능한 서비스를 위한 응용 프로그램 디자인에 대해 알아봅니다."
keywords: "클라우드 재해 복구, 재해 복구 솔루션, 앱 데이터 백업, 지역에서 복제, 무중단 업무 방식 계획"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Azure SQL Database를 사용하여 항상 사용 가능한 서비스 디자인

사용을 빌드하고 Azure SQL 데이터베이스에서 항상 사용 가능한 서비스를 배포 하는 경우 [장애 조치 그룹 및 활성 지리적 복제](sql-database-geo-replication-overview.md) tooprovide 복원 력 tooregional 오류 및 치명적 작동 중단 및 사용에 대 한 빠른 복구 toohello 보조 데이터베이스입니다. 이 문서 일반적인 응용 프로그램 패턴을 중점적으로 다루며 hello 이점과 hello 응용 프로그램 배포 요구 사항 대상으로 hello 서비스 수준 계약에 따라 각 옵션의 장단점을 설명 트래픽 대기 시간 및 비용입니다. 탄력적 풀의 활성 지역 복제에 대한 자세한 내용은 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>디자인 패턴 1: 함께 배치된 데이터베이스와 클라우드 재해 복구에 대한 활성-수동 배포
이 옵션은 다음 특징 hello로 응용 프로그램에 가장 적합 한:

* 단일 Azure 지역의 활성 인스턴스
* 읽기 / 쓰기 (RW)에 대 한 강력한 종속성 toodata 액세스
* Hello 웹 응용 프로그램과 hello 데이터베이스 간에 지역 간 연결 toolatency 캡슐화 된 트래픽과 비용 인해 허용 되지 않는    

이 경우 hello 응용 프로그램 배포 토폴로지는 모든 응용 프로그램 구성 요소는 영향을 않고 하나의 단위로 toofailover 국가별 재해를 처리 하기 위한 최적화 됩니다. 지리적 중복성을 위해 hello 응용 프로그램 논리와 hello 데이터베이스 복제 tooanother 지역 있더라도 hello 정상 조건 하에서 hello 응용 프로그램 작업에 사용 되지 않습니다. hello 보조 지역에 hello 응용 프로그램에 구성 된 toouse SQL 연결 문자열 toohello 보조 데이터베이스 여야 합니다. 트래픽 관리자 설정 toouse [장애 조치 라우팅 방법을](../traffic-manager/traffic-manager-configure-failover-routing-method.md)합니다.  

> [!NOTE]
> [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)는 이 문서 전체에서 설명을 위한 용도로만 사용됩니다. 장애 조치(failover) 라우팅 메서드를 지원하는 모든 부하 분산 솔루션을 사용할 수 있습니다.    
>

다음 다이어그램 hello 중단 하기 전에이 구성을 보여 줍니다.

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Hello 기본 지역에서 중단, 후 hello SQL 데이터베이스 서비스는 hello 해당 주 데이터베이스에 액세스할 수 없고 hello 자동 장애 조치 정책 hello 매개 변수를 기준으로 장애 조치 toohello 보조 데이터베이스를 트리거할 검색 합니다. 응용 프로그램 SLA에 따라 tooconfigure hello 중단의 hello 검색과 자체 hello 장애 조치 사이의 유예 기간을 결정할 수 있습니다. 유예 기간을 구성 hello 위험이 감소의 데이터 손실 toohello 하는 경우 hello 중지가 치명적인 hello 영역의 가용성을 신속 하 게 복원할 수 없습니다. Hello 장애 조치 그룹 트리거 hello hello 데이터베이스의 장애 조치 전에 hello 끝점 장애 조치가 hello 트래픽 관리자가 시작 되 면 hello 웹 응용 프로그램은 수 tooreconnect toohello 데이터베이스가 아닙니다. hello 응용 프로그램의 시도 tooreconnect는 hello 데이터베이스 장애 조치가 완료 되는 즉시 자동으로 성공 합니다. 

> [!NOTE]
> tooachieve hello 응용 프로그램 및 hello 데이터베이스의 장애 조치를 완벽 하 게 조정, 직접 모니터링 방법을 시도해 볼 하 고 hello 웹 응용 프로그램 끝점 및 hello 데이터베이스의 수동 장애 조치를 사용 해야 합니다.
>

모두 hello 응용 프로그램의 끝점 및 hello 데이터베이스의 hello 장애 조치 완료 되 면 hello 응용 프로그램을 다시 시작 시작 hello 영역 B에서에서 hello 사용자 요청을 처리 및 hello 주 데이터베이스에서 이제 이므로 hello 데이터베이스와 함께 유지 됩니다. 2. 지역 Hello 다음 다이어그램은이 시나리오를 보여 줍니다. 모든 다이어그램에서 실선은 활성 연결을 나타내고, 점선은 일시 중단된 연결을 나타내며, 중지 기호는 작업 트리거를 나타냅니다.

![지리적 복제: 장애 조치 toosecondary 데이터베이스입니다. 앱 데이터 백업](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Hello 보조 지역에서 가동 중단 될 경우 주 hello와 hello 보조 데이터베이스 간의 복제 링크 hello 일시 중단 하지만 hello 주 데이터베이스에 영향을 받지 때문에 hello 장애 조치가 트리거됩니다. hello 응용 프로그램의 가용성이 경우 변경 되지 않습니다. 하지만 hello 응용 프로그램 작동 노출 된 하며 따라서 경우에서 높은 위험에 두 영역 실패 연속적으로 합니다.

> [!NOTE]
> 재해 복구를 위해 응용 프로그램 배포 제한 tootwo 영역 hello 구성을 권장 합니다. 즉, 대부분의 hello Azure 지역 있는 두 개의 영역입니다. 이 구성은 두 영역에서 동시에 발생하는 치명적인 오류로부터 응용 프로그램을 보호하지 않습니다.  이러한 발생 가능성이 없는 실패 시 [지리적 복원 작업](sql-database-disaster-recovery.md#recover-using-geo-restore)을 사용하여 세 번째 지역에서 데이터베이스를 복구할 수 있습니다.
>

Hello 중단 완화 될 되 면 hello 보조 데이터베이스는 주 hello로 자동으로 동기화 다시 합니다. 동기화 하는 동안 기본 hello의 성능이 약간 영향을 받을 수 toobe 동기화 해야 하는 데이터 양을 hello에 따라 합니다. hello 다음 다이어그램에서는 hello 보조 지역에서 가동 중단 합니다.

![주 데이터베이스와 동기화된 보조 데이터베이스 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

hello 키 **장점** 이 디자인 패턴의 됩니다.

* hello 동일한 웹 응용 프로그램 배포 tooboth regions입니다 없이 지역별 구성과 추가 논리 tooreact toohello 장애 조치 없습니다. 
* hello 응용 프로그램의 성능을 hello 웹 응용 프로그램으로 장애 조치의 영향을 받지 않습니다 및 hello 데이터베이스는 항상 같은 위치에 배치 합니다.

주 hello **단점이** hello 중복 응용 프로그램은 hello 보조 지역에 대 한 인스턴스는 재해 복구에만 사용 됩니다.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>디자인 패턴 2: 응용 프로그램 부하 분산에 대한 활성-활성 배포
이 클라우드 재해 복구 옵션은 응용 프로그램에 가장 적합 한 특징에 따라 hello로:

* 데이터베이스의 높은 비율과 toowrites를 읽습니다.
* 데이터베이스 읽기 대기 시간 보다 중요 한 hello 최종 사용자 환경에 대 한 hello 쓰기 대기 시간입니다. 
* 읽기 전용 논리가 다른 연결 문자열을 사용하여 읽기-쓰기 논리에서 분리될 수 있음
* 읽기 전용 논리가 hello 최신 업데이트와 완전히 동기화 되는 데이터에 종속 되지 않습니다.  

응용 프로그램에 이러한 특징이 있으면 hello 최종 사용자 연결에 걸쳐 부하 분산 서로 다른 지역에 여러 개의 응용 프로그램 인스턴스가 상당히 개선 될 수 hello 전체적인 최종 사용자 경험 합니다. Hello DR 쌍으로 선택 해야 하는 hello 영역 중 두 및 hello 그룹 장애 조치 이러한 영역에 hello 데이터베이스를 포함 해야 합니다. tooimplement 부하 분산 각 지역의 있어야 끝점과 hello 읽기 / 쓰기 (RW) 연결 된 논리 toohello 읽기 / 쓰기 수신기 hello 그룹 장애 조치의 hello 응용 프로그램의 활성 인스턴스가 있습니다. 해당 hello가 자동으로 시작 됩니다 hello 주 데이터베이스는 중단으로 영향을 보장 합니다. 해당 지역에서 toohello 데이터베이스 hello 읽기 전용 논리 (RO) hello 웹 응용 프로그램에 직접 연결 해야 합니다. 트래픽 관리자 toouse를 설정 해야 [성능 라우팅](../traffic-manager/traffic-manager-configure-performance-routing-method.md) 와 [끝점 모니터링](../traffic-manager/traffic-manager-monitoring.md) 각 응용 프로그램 인스턴스에 대해 사용 하도록 설정 합니다.

패턴 #1에서와 같이 유사한 모니터링 응용 프로그램 배포를 고려해야 합니다. 하지만 #1 패턴과 달리 응용 프로그램을 모니터링 하는 hello 됩니다를 hello 끝점 장애 조치를 트리거합니다.

> [!NOTE]
> 이 패턴에서 둘 이상의 보조 데이터베이스를 사용 하는 동안 hello 영역 B의 보조만 장애 조치에 대해 사용 되며 hello 그룹 장애 조치의 일부가 되어야 합니다.
>

트래픽 관리자 성능 라우팅 toodirect hello 사용자 연결 toohello 응용 프로그램 인스턴스 가장 가까운 toohello 사용자의 지리적 위치에 대해 구성 되어야 합니다. 다음 다이어그램 hello 중단 하기 전에이 구성을 보여 줍니다.

![중단 없는: 성능 라우팅 toonearest 응용 프로그램입니다. 지역에서 복제](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

그룹을 장애 조치 hello hello B. 지역에 보조 영역 A toohello에서 주 데이터베이스의 장애 조치를 자동으로 시작 데이터베이스 정전 hello 영역 A에서에서 검색 된 경우 읽기 / 쓰기 연결 hello 웹 응용 프로그램에 영향을 받지 하므로 hello 읽기 / 쓰기 수신기 끝점 tooregion B도 자동으로 업데이트 됩니다. hello 트래픽 관리자는 hello 오프 라인 끝점 hello 라우팅 테이블에서 제외 됩니다 있지만 라우팅 hello 최종 사용자 트래픽 toohello 나머지 온라인 인스턴스 계속 됩니다. hello 읽기 전용 SQL 연결 문자열에는 영향이 없습니다 hello에 항상 toohello 데이터베이스를 가리키는지으로 같은 지역입니다. 

다음 다이어그램 hello hello hello 장애 조치 후 새 구성을 보여 줍니다.

![장애 조치 후 구성 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

Hello 보조 영역 중 하나에 중단 시간 발생 한 경우 hello 트래픽 관리자는 자동으로 제거 hello 오프 라인 끝점 해당 지역에서 hello 라우팅 테이블에서. hello 복제 채널 toohello 보조 데이터베이스가 해당 지역에서 일시 중단 됩니다. Hello 나머지 영역이이 시나리오에서 추가 사용자 트래픽을 get, 때문에 hello 중단 하는 동안 hello 응용 프로그램의 성능 영향을 미칩니다. 일단 hello 중단 완화 될 hello hello 영향을 받는 지역에 보조 데이터베이스는 즉시와 동기화 될 기본 hello 합니다. Hello 하는 동안 기본 hello의 동기화 성능이 약간 영향을 받을 수 toobe 동기화 해야 하는 데이터 양을 hello에 따라 합니다. hello 다음 다이어그램 2. 지역에서 가동 중단을 보여 줍니다.

![보조 지역에서 중단 클라우드 재해 복구 - 지역에서 복제](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

hello 키 **장점은** 이 디자인의 패턴은 여러 보조 tooachieve hello 최적의 사용자 성능 간에 hello 응용 프로그램 작업 부하를 확장할 수 있습니다. hello **장단점** 이 옵션은:

* Hello 응용 프로그램 인스턴스 및 데이터베이스 간에 읽기 / 쓰기 연결에는 다양 한 비용 및 대기 시간
* Hello 중단 하는 동안 응용 프로그램 성능이 저하 되어

> [!NOTE]
> 유사한 방법을 사용할 수 toooffload 특수화 작업, 비즈니스 인텔리전스 도구 또는 백업을 보고 등의 작업입니다. 이러한 작업 상당히 많은 데이터베이스 리소스를 소비 하는 일반적으로 따라서 것이 좋습니다 지정 하는 hello 중 보조 데이터베이스에 대 한 hello 성능 수준 일치 toohello 예상 작업입니다.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>디자인 패턴 3: 데이터 보존에 대한 활성-수동 배포
이 옵션은 다음 특징 hello로 응용 프로그램에 가장 적합 한:

* 어떤 경우든 데이터 손실은 비즈니스에 큰 위험이 됩니다. hello 중지가 치명적인 하는 경우에 hello 데이터베이스 장애 조치 최후의 수단으로 사용 수 있습니다.
* hello 응용 프로그램 작업의 읽기 전용 및 읽기 / 쓰기 모드를 지원 하며 일정 기간에 대 한 "읽기 전용 모드"에서 작동할 수 있습니다.

이 패턴에서는 hello 응용 프로그램 hello 읽기 / 쓰기 연결 시작 시간 초과 오류가 발생 했습니다. tooread 전용 모드를 전환 합니다. hello 웹 응용 프로그램은 배포 된 tooboth 영역 및 연결 toohello 읽기 / 쓰기 수신기 끝점 및 다른 연결 toohello 읽기 전용 수신기 끝점을 포함 합니다. hello 트래픽 관리자 toouse를 설정 해야 [장애 조치 라우팅](../traffic-manager/traffic-manager-configure-failover-routing-method.md) 와 [끝점 모니터링](../traffic-manager/traffic-manager-monitoring.md) 각 지역에 hello 응용 프로그램 끝점에 대해 사용 하도록 설정 합니다.

다음 다이어그램 hello 중단 하기 전에이 구성을 보여 줍니다.

![장애 조치 전 활성-수동 배포 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

2. 지역에 사용자 트래픽을 toohello 응용 프로그램 인스턴스가 자동으로 전환 hello 트래픽 관리자에서 연결 오류 tooregion A를 발견 하면 이이 패턴을 사용 하 여 설정한 hello 유예 기간 데이터 손실 tooa 충분히 높은 값, 예: 24 시간 동안 중요 합니다. Hello 중단 기간 내에 완화 될 경우 데이터 손실이 방지 됩니다는 확인 합니다. Hello hello 영역 B의에서 웹 응용 프로그램 활성화 되 면 hello 읽기 / 쓰기 작업 실패 하기 시작 합니다. 이 시점에서 toohello 읽기-쓰기 모드로 전환 해야 합니다. 이 모드 hello 요청 자동 경로 toohello 보조 데이터베이스가 됩니다. 치명적인 오류 hello의 hello 대/소문자 hello 유예 기간 내 중단 문제가 완화 되지 않습니다 및 그룹을 장애 조치 hello hello 장애 조치를 트리거합니다. 해당 hello 후 읽기 / 쓰기 수신기를 사용할 수 있으며 hello 호출 tooit 실패 중지 됩니다. 다음 다이어그램 hello에서이 확인할 수 있습니다.

![작동 중단: 읽기 전용 모드의 응용 프로그램 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Hello 유예 기간 내 hello 기본 지역의 hello 가동 중단은 완화 트래픽 관리자 연결의 hello 복원 hello 기본 지역에서 감지 하 고 사용자 트래픽이 백 toohello 응용 프로그램 인스턴스 1. 지역에서 전환 다시 시작 하 고 hello 주 데이터베이스를 사용 하 여 1. 지역에 읽기 / 쓰기 모드에서 작동 하는 해당 응용 프로그램 인스턴스

Hello 영역 B는 중단 시 hello 트래픽 관리자가 영역 B 및 hello 장애 조치 그룹 스위치 hello 읽기 전용 수신기 tooregion A. hello 응용 프로그램 끝점의 hello 오류를 검색 이 중단 hello 최종 사용자 환경에 영향을 주지 않습니다 하지만 hello 중단 하는 동안 hello 주 데이터베이스가 노출 됩니다. 다음 다이어그램 hello에서이 확인할 수 있습니다.

![중단: 보조 데이터베이스 클라우드 재해 복구](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Hello 중단 완화 될 hello 보조 데이터베이스는 즉시 동기화 기본 hello로 고 hello 읽기 전용 수신기 바뀌면된 백 toohello B. 지역에 보조 데이터베이스는 동기화 하는 동안 hello 기본의 성능 약간 영향을 받을 수 toobe 동기화 해야 하는 데이터 양을 hello에 따라 합니다.

이 디자인 패턴에는 다음과 같은 여러 **장점**이 있습니다.

* Hello 임시 중단 하는 동안 데이터 손실을 방지할 수 있습니다.
* 트래픽 관리자가 구성 가능 hello 연결 오류를 검색 하는 속도에 대해서만 가동 중지 시간에 따라 달라 집니다.

hello **단점이** 됩니다.

* 응용 프로그램에는 읽기 전용 모드에 toooperate 수 있어야 합니다.

> [!NOTE]
> Hello 영역은 영구 서비스 중단 시 수동으로 활성화 데이터베이스 장애 조치 한 있습니다 hello 데이터 손실 허용 합니다. hello 응용 프로그램 읽기 / 쓰기 액세스 toohello 데이터베이스와 보조 지역 hello 작동 됩니다.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>무중단 업무 방식 계획: 클라우드 재해 복구에 대한 응용 프로그램 디자인 선택
특정 클라우드 재해 복구 전략을 결합 하거나 응용 프로그램의 toobest 충족 hello 요구 이러한 디자인 패턴을 확장할 수 있습니다.  앞서 언급 했 듯이 hello 선택 하는 전략은 hello toooffer tooyour 고객을 응용 프로그램 배포 토폴로지를 hello SLA 기반으로 합니다. toohelp 결정 하는 데, 다음 표에 hello hello 예상된 데이터 손실 또는 복구 지점 목표 (RPO) 및 복구 예상된 시간 (ERT)를 기반으로 hello 선택 항목을 비교 합니다.

| 패턴 | RPO | ERT |
|:--- |:--- |:--- |
| 배치된 데이터베이스 액세스로 재해 복구에 대한 활성-수동 배포 |읽기-쓰기 액세스 < 5초 |장애 감지 시간 + DNS TTL |
| 응용 프로그램 부하 분산에 대한 활성-활성 배포 |읽기-쓰기 액세스 < 5초 |장애 감지 시간 + DNS TTL |
| 데이터 보존에 대한 활성-수동 배포 |읽기 전용 액세스 < 5초 | 읽기 전용 액세스 = 0 |
||읽기-쓰기 액세스 = 0 | 읽기-쓰기 액세스 = 장애 감지 시간 + 데이터 손실이 있는 유예 기간 |
|||

## <a name="next-steps"></a>다음 단계
* Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [자동화 된 백업을 SQL 데이터베이스](sql-database-automated-backups.md)
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)
* 복구를 위한 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [hello 서비스 개시 백업에서 데이터베이스를 복원 합니다.](sql-database-recovery-using-backups.md)
* 빠른 복구 옵션에 대 한 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)  
* 보관을 위해 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [데이터베이스 복사](sql-database-copy.md)
* 탄력적 풀의 활성 지역 복제에 대한 자세한 내용은 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.
