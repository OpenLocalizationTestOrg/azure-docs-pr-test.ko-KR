---
title: "aaaWhat은 hello Azure SQL 데이터베이스 서비스는? | Microsoft Docs"
description: "소개 tooSQL 데이터베이스 가져오기: 기술 세부 정보 및 성능이 나와 Microsoft의 관계형 데이터베이스 관리 시스템 (RDBMS) hello 클라우드에서 합니다."
keywords: "소개 toosql, 소개 toosql, 이란 sql 데이터베이스"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>Hello Azure SQL 데이터베이스 서비스는 무엇입니까? 

SQL Database는 관계형 데이터, 공간, JSON 및 XML과 같은 구조를 지원하는 Microsoft Azure의 범용 관계형 데이터베이스 서비스입니다. [동적으로 확장 가능한 성능](sql-database-service-tiers.md)을 제공하고 고도의 분석 및 보고를 위한 [columnstore 인덱스](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) 및 고도의 트랜잭션 처리를 위한 [메모리 내 OLTP](sql-database-in-memory.md)와 같은 옵션을 제공합니다. Microsoft는 모든 업데이트 및 패치 적용 hello SQL 코드 베이스 원활 하 게 처리 하 고 hello 기본 인프라의 모든 관리를 추상화 합니다. 

Hello와 동시에 코드 베이스를 공유 하는 SQL 데이터베이스 [Microsoft SQL Server 데이터베이스 엔진](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)합니다. Microsoft의 클라우드 우선 전략을 SQL Server의 최신 기능 hello은 출시 된 첫 번째 tooSQL 데이터베이스 및 다음 tooSQL 서버 자체입니다. 이 방법을 사용 하면 hello로 최신 SQL Server과 기능을 제공 패치 기능에 오버 헤드가 없습니다 또는 수백만 개의 데이터베이스에 대해 테스트 한-업그레이드 하 고 이러한 새로운 기능을 사용 합니다. 별도로 공지된 새로운 기능에 대한 내용은 다음을 참조하세요.

- **[SQL 데이터베이스에 대 한 azure 로드맵](https://azure.microsoft.com/roadmap/?category=databases)**: 새로운 기능 및 향후 예정 사항 다음 장소 toofind 합니다. 
- **[Azure SQL Database 블로그](https://azure.microsoft.com/blog/topics/database)**: SQL Database 뉴스 및 기능에 대한 SQL Server 제품 팀 구성원 블로그를 확인할 수 있습니다. 

SQL Database는 가동 중지 시간 없이 기본 제공 지능형 최적화, 전역 확장성과 가용성 및 고급 보안 옵션을 포함하여 동적 확장성을 제공하는 여러 서비스 수준에서 별도로 관리하지 않고도 예측 가능한 성능을 제공합니다. 이러한 기능을 사용 하면 빠른 응용 프로그램 개발 및 사용자 시간 toomarket를 가속화 하는 데 보다는에 시간을 단축 하 고 리소스 toomanaging 가상 컴퓨터 및 인프라 할당 toofocus 있습니다. hello 38 데이터 서비스는 현재 SQL 데이터베이스에 중점을 둡니다 hello world 더 많은 데이터 센터가 정기적으로 온라인 상태가 toorun 사용할 수 있는 가까운 데이터 센터에서 데이터베이스.

> [!NOTE]
> Azure의 플랫폼 보안에 대한 자세한 내용을 보려면 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/security/)를 참조하세요.
>

## <a name="scalable-performance-and-pools"></a>확장 가능한 성능 및 풀

SQL Database에서 각 데이터베이스는 보장된 성능 수준에서 고유한 [서비스 계층](sql-database-service-tiers.md)으로 서로 격리되고 이식 가능합니다. SQL 데이터베이스는 서로 다른 요구 사항에 대 한 다양 한 성능 수준을 제공 하 고 toobe 풀링된 toomaximize hello 리소스 사용 및 비용을 절감 하는 데이터베이스를 활성화 합니다.

### <a name="adjust-performance-and-scale-without-downtime"></a>가동 중지 시간 없이 성능 및 규모 조정

SQL 데이터베이스는 toosupport tooheavyweight 경량 데이터베이스 작업 4 개의 서비스 계층을 제공: Basic, Standard, Premium 및 프리미엄 RS 합니다. 저렴 한 비용으로 매달 작은, 단일 데이터베이스에서 첫 번째 응용 프로그램을 작성 하 고 변경할 수 해당 서비스 계층 수동으로 또는 프로그래밍 방식으로 솔루션의 요구 하는 시간 toomeet hello에 있습니다. Tooyour 앱 또는 tooyour 고객 가동 중지 시간 없이 성능을 조정할 수 있습니다. 동적 확장성 데이터베이스 tootransparently 리소스 요구 사항 및 사용 하도록 설정 하면 tooonly hello 리소스에 대 한 지불이 필요할 때 해야 변경 toorapidly 응답할 수 있습니다.

   ![scaling](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>탄력적 풀 toomaximize 리소스 사용률

많은 비즈니스 및 응용 프로그램에 대 한 단일 데이터베이스 수 toocreate 되 전화를 성능 위로 또는 아래로 필요에 따라 사용 패턴은 상대적으로 예측 하는 경우에 특히는 충분 합니다. 하지만 예측할 수 없는 사용 패턴을 사용 하는 경우 그 수 하드 toomanage 비용 및 비즈니스 모델. [탄력적 풀](sql-database-elastic-pool.md) 디자인된 toosolve이이 문제가 됩니다. hello 개념은 간단 합니다. 개별 데이터베이스 보다는 성능 리소스 tooa 풀 이상을 할당 하 고 hello 풀의 hello 축적 성능 리소스에 대 한 아닌 단일 데이터베이스 성능에 대 한 비용을 지불 합니다. 

   ![탄력적 풀](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

탄력적 풀과 리소스에 대 한 수요가 변경 됨에 따라 데이터베이스 성능 및 축소를 걸기에 toofocus가 필요는 없습니다. hello 풀링된 데이터베이스 리소스를 소비 hello 성능 hello 탄력적 풀의 필요에 따라 합니다. 풀링된 데이터베이스 소비 하지만 개별 데이터베이스 사용 하지 않는 경우에 비용 예측 가능한 게 hello 풀 hello도 초과 하지 않습니다. 더구나 수 [추가 하 고 데이터베이스 toohello 풀 제거](sql-database-elastic-pool-manage-portal.md)는 소수의 사용자가 제어 하는 예산 내에서 데이터베이스 toothousands에서 응용 프로그램을 확장 합니다. 또한 제어 hello 최소 수 있습니다 및 hello 풀 tooensure hello 풀에서 데이터베이스가 없습니다. 모든 사용에 사용할 수 있는 toodatabases 최대 리소스 풀 리소스 및 풀링된 모든 데이터베이스에 최소 보장된 리소스 용량이 있는지 hello 합니다. 탄력적 풀을 사용 하 여 SaaS 응용 프로그램에 대 한 디자인 패턴에 대해 자세히 toolearn 참조 [SQL 데이터베이스를 사용한 다중 테 넌 트 SaaS 응용 프로그램에 대 한 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)합니다.

### <a name="blend-single-databases-with-pooled-databases"></a>단일 데이터베이스와 풀링된 데이터베이스의 혼합

사용자는 단일 데이터베이스와 탄력적 풀 중 어느 한 쪽으로만 한정되지는 않습니다. 탄력적 풀을 사용 하 여 단일 데이터베이스를 혼합 하 고 신속 하 고 쉽게 단일 데이터베이스 및 탄력적 풀의 hello 서비스 계층을 변경할 수 있습니다 tooadapt tooyour 상황입니다. Hello 전원와 Azure의 도달 범위를 혼합 및 일치 다른 Azure SQL 데이터베이스 toomeet 고유한 응용 프로그램 디자인 요구 사항, 비용 드라이브 및 리소스 효율성을 사용 하 여 서비스와 새로운 비즈니스 기회 잠금을 해제할 수 있습니다.

### <a name="extensive-monitoring-and-alerting-capabilities"></a>광범위한 모니터링 및 경고 기능

하지만 단일 데이터베이스와 탄력적 풀의 상대 성능을 hello 어떻게 비교할 수 있습니까? 알 수 있을까요 hello 마우스 오른쪽 단추로 클릭 하 여 중지 아래로 전화 때? Hello를 사용 하 여 [기본 제공 성능 모니터링](sql-database-performance.md) 및 [경고](sql-database-insights-alerts-portal.md) hello 성능 등급에 따라 함께 도구 [단일 데이터베이스에 대 한 데이터베이스 트랜잭션 단위 (DTUs) 및 탄력적 풀에 대 한 탄력적 Dtu (Edtu)](sql-database-what-is-a-dtu.md)합니다. 이러한 도구를 사용 하 여 신속 하 게 평가할 수 확장 또는 축소 현재 기준의 hello 영향 또는 프로젝트 성능 요구 합니다. 자세한 내용은 [SQL 데이터베이스 옵션 및 성능: 각 서비스 계층에서 사용할 수 있는 것 이해](sql-database-service-tiers.md) 를 참조하세요.

또한 SQL Database는 쉬운 모니터링을 위해 [메트릭 및 진단 로그를 내보낼](sql-database-metrics-diag-logging.md) 수 있습니다. SQL 데이터베이스 toostore 리소스 사용량, 작업자 및 세션 및 Azure 이러한 리소스 중 하나에 대 한 연결을 구성할 수 있습니다.

- **Azure Storage**: 작은 가격으로 방대한 양의 원격 분석을 보관하는 경우
- **Azure Event Hub**: 사용자 지정 모니터링 솔루션 또는 핫 파이프라인과 SQL Database 원격 분석을 통합하는 경우
- **Azure Log Analytics**: 보고, 경고 및 완화 기능을 사용하는 기본 제공 모니터링 솔루션의 경우

    ![아키텍처](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>가용성 기능

Azure의 업계 선도적인 99.99% 가용성 [SLA](http://azure.microsoft.com/support/legal/sla/)(서비스 수준 계약)를 Microsoft에서 관리되는 전 세계 데이터 센터 네트워크의 지원을 받아 앱을 연중 무휴(24/7)로 실행할 수 있습니다. 또한 SQL Database는 다음을 포함하여 기본 제공 [비즈니스 연속성 및 글로벌 확장성](sql-database-business-continuity.md) 기능을 제공합니다.

- **[자동 백업](sql-database-automated-backups.md)**: SQL Database는 전체, 차등 및 트랜잭션 로그 백업을 자동으로 수행합니다.
- **[지정 시간 복원](sql-database-recovery-using-backups.md)**: SQL 데이터베이스 hello 자동 백업 보존 기간 내의 지정 시간 복구 tooany 지점을 지원 합니다.
- **[활성 지리적 복제](sql-database-geo-replication-overview.md)**: SQL 데이터베이스를 통해 toofour 읽기 가능한 보조 복제본을 tooconfigure hello 중 하나에서 동일한 데이터베이스 또는 Azure 데이터 센터를 전역으로 분산 합니다.  예를 들어 SaaS 응용 프로그램의 동시 읽기 전용 트랜잭션 높은 볼륨이 있는 카탈로그 데이터베이스와를 설정한 경우 사용 하 여 활성 지리적 복제 tooenable 글로벌 눈금 읽고 tooread 워크 로드 되는 기본 hello에 병목 현상을 제거 합니다. 
- **[장애 조치 그룹](sql-database-geo-replication-overview.md)**: SQL 데이터베이스 있습니다 tooenable 고가용성 및 투명 한 지리적 복제 및 데이터베이스와 탄력적 풀의 큰 집합의 장애 조치를 포함 하는 세계적인 규모의 부하 분산 합니다. 장애 조치 그룹 및 활성 지리적 복제 사용 생성 세계적으로 분산 된 SaaS 응용 프로그램을 최소한의 관리 오버 헤드 모든 hello 복잡 한 모니터링, 라우팅 및 오케스트레이션 tooSQL 데이터베이스 장애 조치를 종료 합니다.

## <a name="built-in-intelligence"></a>기본 제공 인텔리전스

SQL 데이터베이스 성능과 응용 프로그램의 보안을 극대화 하 고 실행 하 고 관리 데이터베이스의 hello 비용을 크게 줄일 수 있습니다 수 있도록 기본 제공 intelligence를 얻을 수 있습니다. 수백만 개의 고객 24 시간 작업을 실행, SQL 데이터베이스 수집 하 고 완전히 hello 백그라운드 고객 개인 정보를 유지 하는 동안 많은 양의 원격 분석 데이터를 처리 합니다. 지속적으로 다양 한 알고리즘은 hello 서비스 알아보고 응용 프로그램과 함께 적용할 수 있도록 hello 원격 분석 데이터를 평가 해야 합니다. 이 분석에 따르면 hello 서비스를 생성 하 성능 권장 사항 맞춤형된 tooyour 특정 작업을 향상 합니다. 

### <a name="automatic-performance-tuning"></a>자동 성능 튜닝

SQL 데이터베이스 hello에 대 한 자세한 정보를 toomonitor 해야 하는 쿼리를 제공 합니다. SQL 데이터베이스는 데이터베이스 패턴을 인식 하 고 있습니다 tooadapt 데이터베이스 스키마 tooyour 작업을 활성화 합니다. SQL Database는 [SQL Database Advisor](sql-database-advisor.md)를 사용하여 성능 튜닝 권장 구성을 제공하고 튜닝 작업을 검토하고 적용할 수 있습니다. 그러나 지속적으로 데이터베이스를 모니터링하는 것은 특히 많은 데이터베이스를 처리할 때 힘들고 지루한 작업입니다. 거 대 한 수의 데이터베이스를 관리할 수 있습니다 불가능 한 toodo 효율적으로 된 경우에 모든 사용 가능한 도구 및 SQL 데이터베이스 및 Azure 포털에서 제공 하는 보고서. 모니터링 수동으로 데이터베이스를 튜닝 하는 대신 해야 할 몇 가지 모니터링 및 튜닝 작업 tooSQL hello 위임 자동 튜닝 기능을 사용 하 여 데이터베이스입니다. SQL 데이터베이스는 자동으로 권장 구성, 테스트를 적용 하 고 각 튜닝 작업 tooensure hello 성능을 향상 계속 확인 합니다. SQL 데이터베이스는 이러한 방식으로 제어 되 고 안전한 방법으로 tooyour 작업을 자동으로 적응합니다. 자동 튜닝 있음을 나타내고 데이터베이스 성능 hello 신중 하 게 모니터링 하 고 모든 튜닝 작업 전후의 비교 작업을 튜닝 하는 hello 되돌려지는 hello 성능을 개선 하지 않습니다.

오늘를 다 실행 여러 파트너의 [다중 테 넌 트 SaaS 앱](sql-database-design-patterns-multi-tenancy-saas-applications.md) 자동 성능 toomake 있는지 응용 프로그램 항상 안정적이 고 예측 가능한 성능 튜닝에 점을 SQL 데이터베이스를 기반으로 합니다. 이 기능에는 고객을 위해 hello 위험을 hello 밤 hello 가운데에 성능 문제가 발생 한을 크게 줄여 줍니다. 또한 고객 기반의 일부 SQL Server를 사용 하므로 hello 사용 중인 SQL Server 고객에 게 SQL 데이터베이스 toohelp에서 인덱싱 같은 권장 사항을 제공 합니다.

SQL Database에서 사용할 수 있는 두 가지 자동 튜닝 측면이 있습니다.

- **[자동 인덱스 관리](sql-database-automatic-tuning.md#automatic-index-management)**: 데이터베이스에 추가되어야 하는 인덱스 및 제거되어야 하는 인덱스를 식별합니다.
- **[자동 계획 수정](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**: 문제가 있는 계획을 식별하고 SQL 계획 성능 문제를 해결합니다(출시 예정, SQL Server 2017에서 이미 사용 가능).

### <a name="adaptive-query-processing"></a>적응 쿼리 처리

또한 hello 추가 하 고 [적응 쿼리 처리](/sql/relational-databases/performance/adaptive-query-processing) 기능 tooSQL 다중 문 테이블 반환 함수에 대 한 인터리브 방식된으로 실행을 포함 하 여 데이터베이스의 제품군 모드 메모리 부여 피드백 일괄 처리 및 모드 적응 조인 일괄 처리 . 각각의 적응 쿼리 처리 기능 적용 유사한 "알아보고 조정" 방법을 추가 주소 성능 문제 관련된 toohistorically 다루기 쿼리 최적화 문제 수 있도록 지원 합니다.

### <a name="intelligent-threat-detection"></a>지능형 위협 검색

 [SQL 위협 요소 탐지](sql-database-threat-detection.md) 활용 [SQL 데이터베이스 감사](sql-database-auditing.md) toocontinuously 모니터 Azure SQL 데이터베이스 tooaccess 중요 한 데이터의 잠재적으로 위험한 시도 합니다. SQL 위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다. 사용자는 의심스러운 데이터베이스 활동, 잠재적 취약성 및 SQL 삽입 공격은 물론 비정상적인 데이터베이스 액세스 패턴에 대한 경고를 받게 됩니다. SQL 위협 검색 경고가 의심 스러운 활동의 세부 정보를 제공 하 고 방법에 대 한 작업을 권장 tooinvestigate hello 위협을 완화 합니다. 사용자는 시도 tooaccess에서 hello 이벤트 결과 위반를 주거나 이들을 착취 hello 데이터베이스의에서 데이터를 하는 경우 hello 의심 스러운 이벤트 toodetermine를 탐색할 수 있습니다. 위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안을 관리 합니다.

## <a name="advanced-security-and-compliance"></a>고급 보안 및 규정 준수

SQL 데이터베이스는 다양 한 제공 [기본 제공 보안 및 규정 준수 기능](sql-database-security-overview.md) toohelp 응용 프로그램에 다양 한 보안 및 규정 준수 요구 사항을 충족 합니다. 

### <a name="auditing-for-compliance-and-security"></a>규정 준수 및 보안에 대한 감사

[SQL 데이터베이스 감사](sql-database-auditing.md) 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다. 감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.

### <a name="data-encryption-at-rest"></a>휴지 상태의 암호화

SQL 데이터베이스 [투명 한 데이터 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) 의 hello 데이터베이스에 연결 된 백업, 실시간 암호화 / 해독을 수행 하 여 악의적인 활동의 hello 취약점 으로부터 보호 하 고 미사용 트랜잭션 로그 파일 toohello 응용 프로그램 변경 하지 않고도 합니다. 2017년 5월부터 시작하여 새로 만든 모든 Azure SQL Database는 TDE(투명한 데이터 암호화)를 사용하여 자동으로 보호됩니다. TDE는 저장소 미디어의 도난 방지 하는 많은 규정 준수 표준 tooprotect에 필요한 휴지 암호화 기술을 입증 된 SQL의 합니다. 고객은 Azure 키 자격 증명 모음을 사용 하 여 안전 하 고 규격 방식에서 hello TDE 암호화 키 및 기타 암호 관리할 수 있습니다.

### <a name="data-encryption-in-motion"></a>진행 중인 데이터 암호화

SQL 데이터베이스는 hello만 시스템 toooffer 보호 데이터베이스 이동 중인을 미사용 및 쿼리를 처리 하는 동안 중요 한 데이터의 [항상 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine)합니다. 상시 암호화는 최상의 데이터를 제공 하는 업계 중심 hello 도난 중요 한 데이터를 포함 하는 위반에 대 한 보안. 예를 들어 상시 암호화, 고객의 신용 카드 번호를 저장 쿼리 처리 중에 항상 그렇지는 hello 데이터베이스에서 암호화 데이터를 권한이 부여 된 직원 또는 tooprocess 해야 하는 응용 프로그램에서 사용 하 여 hello 시점에서 암호 해독을 허용 합니다.

### <a name="dynamic-data-masking"></a>동적 데이터 마스킹

[SQL 데이터베이스 동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md) toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한 합니다. 동적 데이터 마스킹 고객 toodesignate를 사용 하 여 toosensitive 데이터를 무단된 액세스를 방지할 수 어느 정도의 hello 중요 한 데이터 tooreveal hello 응용 프로그램 계층에 미치는 영향을 최소화 합니다. hello 데이터베이스의 hello 데이터는 변경 되지 않으면 지정 된 데이터베이스 필드를 통해 hello hello 쿼리 결과 집합에서 중요 한 데이터를 숨기는 정책 기반 보안 기능.

### <a name="row-level-security"></a>행 수준 보안

[행 수준 보안](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) 쿼리를 실행 하는 hello 사용자의 hello 특성에 따라 데이터베이스 테이블에서 고객 toocontrol 액세스 toorows 수 있습니다 (같은 그룹 멤버십 또는 실행 컨텍스트별). 행 수준 보안 (RLS) hello 설계 및 응용 프로그램의 보안 코딩을 간소화 합니다. RLS 사용 하면 데이터 행 액세스에 tooimplement 제한 사항이 있습니다. 예를 들어 작업 자가 관련 tootheir 부서는 데이터 행만 액세스할 수 있는지를 확인 하거나 고객의 데이터 액세스 tooonly hello 데이터 관련 tootheir 회사를 제한 합니다.

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Azure Active Directory 통합 및 Multi-Factor Authentication

Toocentrally 하면 데이터베이스 사용자 및 기타 Microsoft 서비스와 id를 관리 하는 SQL 데이터베이스 사용 [Azure Active Directory 통합](sql-database-aad-authentication.md)합니다. 이 기능은 사용 권한 관리를 간소화하고 보안을 향상시킵니다. Azure Active Directory 지원 [다단계 인증](sql-database-ssms-mfa-authentication.md) 단일 사인 인 프로세스를 지원 하면서 (MFA) tooincrease 데이터 및 응용 프로그램 보안 합니다.

### <a name="compliance-certification"></a>규정 준수 인증

SQL Database는 일반 감사에 참여하고 몇 가지 준수 표준에 대해 인증됩니다. 자세한 내용은 참조 hello [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)여기서 hello의 최신 목록을 찾을 수 있습니다 [SQL 데이터베이스 규정 준수 인증](https://azure.microsoft.com/support/trust-center/services/)합니다.

## <a name="easy-to-use-tools"></a>사용하기 쉬운 도구

SQL Database로 응용 프로그램을 빌드하고 관리하는 작업의 편의성과 생산성을 높이세요. SQL 데이터베이스를 통해 수행할 작업에 가장 잘 toofocus: 유용한 앱을 작성 합니다. 이미 설치된 도구와 기술을 사용하여 SQL Database에서 관리하고 개발할 수 있습니다.

- **[Azure 포털 hello](https://portal.azure.com/)**: 모든 Azure 서비스를 관리 하기 위한 웹 기반 응용 프로그램 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: SQL Server tooSQL 데이터베이스에서에서 모든 SQL 인프라를 관리 하기 위한, 무료로 다운로드할 수 있는 클라이언트 응용 프로그램
- **[Visual Studio의 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**: SQL Server 관계형 데이터베이스, Azure SQL Database, Integration Services 패키지, Analysis Services 데이터 모델 및 Reporting Services 보고서를 개발하는 체험 다운로드 가능한 클라이언트 응용 프로그램
- **[Visual Studio Code](https://code.visualstudio.com/docs)**: Windows, macOS 등 및 hello를 포함 하 여 확장을 지 원하는 Linux 용 코드 편집기, 무료 다운로드 가능한 오픈 소스 [확장명이 mssql](https://aka.ms/mssql-marketplace) Microsoft SQL Server를 쿼리 하기 위한 Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스

SQL 데이터베이스는 Python, Java, Node.js, PHP, Ruby, 및 hello MacOS에서.NET, Linux 및 Windows를 사용한 응용 프로그램 작성을 지원합니다. SQL 데이터베이스 지원 hello 동일 [연결 라이브러리](sql-database-libraries.md) SQL 서버로 합니다.

## <a name="engage-with-hello-sql-server-engineering-team"></a>Hello SQL Server 엔지니어링 팀에 문의

- [DBA 스택 교환(영문)](https://dba.stackexchange.com/questions/tagged/sql-server): 데이터베이스 관리 관련 질문
- [Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/sql-server): 개발 관련 질문
- [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): 기술 관련 질문
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): 버그 및 요청 기능 보고
- [Reddit](https://www.reddit.com/r/SQLServer/): SQL Server 관련 토론

## <a name="next-steps"></a>다음 단계

- Hello 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/sql-database/) 단일 데이터베이스 및 탄력적 풀 비용 비교 및 계산기에 대 한 합니다.

- 이 빠른 시작 했는지 tooget 참조:

  - [Hello Azure 포털에서에서 SQL 데이터베이스 만들기](sql-database-get-started-portal.md)  
  - [Hello Azure CLI로 SQL 데이터베이스 만들기](sql-database-get-started-cli.md)
  - [PowerShell을 사용하여 SQL Database 만들기](sql-database-get-started-powershell.md)

- 일련의 Azure CLI 및 PowerShell 샘플은 다음을 참조하세요.
  - [SQL Database에 대한 Azure CLI 샘플](sql-database-cli-samples.md)
  - [SQL Database에 대한 Azure PowerShell 샘플](sql-database-powershell-samples.md)
