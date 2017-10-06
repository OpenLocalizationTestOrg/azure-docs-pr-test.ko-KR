---
title: "데이터베이스 복구-SQL 데이터베이스-aaaCloud 비즈니스 연속성 | Microsoft Docs"
description: "Azure SQL 데이터베이스에서 클라우드 무중단 업무 방식 및 데이터베이스 복구를 지원하고 중요 업무용 클라우드 응용 프로그램을 계속해서 실행할 수 있도록 하는 방법을 알아봅니다."
keywords: "무중단 업무 방식, 클라우드 무중단 업무 방식, 데이터베이스 재해 복구, 데이터베이스 복구"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Azure SQL 데이터베이스의 비즈니스 연속성 개요

이 개요에서는 Azure SQL 데이터베이스 비즈니스 연속성 및 재해 복구를 제공 하는 hello 기능을 설명 합니다. 옵션, 권장 사항 및 데이터베이스와 응용 프로그램 toobecome를 사용할 수 없는 발생 하거나 데이터가 손실 될 수 있는 중단 이벤트에서 복구에 대 한 자습서에 알아봅니다. 사용자 또는 응용 프로그램 오류 데이터 무결성에 영향을 줍니다, Azure 지역에 있는 중단 또는 응용 프로그램 유지 관리에 필요한 때 어떤 toodo에 알아봅니다.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Tooprovide 비즈니스 연속성을 사용할 수 있는 SQL 데이터베이스 기능

SQL 데이터베이스는 자동화된 백업 및 선택적 데이터베이스 복제를 비롯한 여러 가지 비즈니스 연속성 기능을 제공합니다. 이러한 기능은 최근 트랜잭션에 대한 ERT(예상 복구 시간) 및 잠재적 데이터 손실에 대해 각기 다른 특성을 갖습니다. 이러한 옵션을 이해하면 적절한 옵션을 선택할 수 있습니다. 대부분의 시나리오에서 이러한 옵션을 함께 사용할 수 있습니다. 비즈니스 연속성 계획을 개발할 때는 toounderstand hello 최대 허용 가능한 시간 전에 hello 강제 이벤트 이후 완전히 복구 하는 hello 응용 프로그램-이것은 복구 시간 목표 (RTO) 해야 합니다. 또한 toounderstand 해야 hello 강제 이벤트 이후 복구할 때 hello 최대한 최근 데이터 업데이트 (시간 간격) hello 응용 프로그램의 손실을 허용할 수 있는-이 복구 지점 목표 (RPO).

테이블 비교를 수행 하는 hello ERT 및 RPO hello 3 가장 일반적인 시나리오에 대 한 hello 합니다.

| 기능 | 기본 계층 | 표준 계층 | 프리미엄 계층 |
| --- | --- | --- | --- |
| 백업에서 특정 시점 복원 |7일 이내의 모든 복원 지점 |35일 이내의 모든 복원 지점 |35일 이내의 모든 복원 지점 |
| 지리적으로 복제된 백업에서 지역 복원 |ERT < 12시간, RPO < 1시간 |ERT < 12시간, RPO < 1시간 |ERT < 12시간, RPO < 1시간 |
| Azure 백업 자격 증명 모음에서 복원 |ERT < 12시간, RPO < 1주 |ERT < 12시간, RPO < 1주 |ERT < 12시간, RPO < 1주 |
| 활성 지역 복제 |ERT < 30초, RPO < 5초 |ERT < 30초, RPO < 5초 |ERT < 30초, RPO < 5초 |

### <a name="use-database-backups-toorecover-a-database"></a>데이터베이스 백업을 toorecover 데이터베이스를 사용 하 여

SQL 데이터베이스는 자동으로 전체 데이터베이스 백업의 조합을 매주 수행, 매시간, 차등 데이터베이스 백업 및 트랜잭션 로그 백업을 모든 5-10 분 후에 tooprotect 비즈니스 데이터 손실이 발생 하지 않도록에서 합니다. 이러한 백업은 35 일 hello Standard 및 Premium 서비스 계층의 데이터베이스에 대 한 hello Basic 서비스 계층의 데이터베이스에 대 한 일에 대 한 지역 중복 저장소에 저장 됩니다. 자세한 내용은 [서비스 계층](sql-database-service-tiers.md)을 참조하세요. Hello 보존 기간은 서비스 계층에 대 한 비즈니스 요구 사항에 맞지 않으면 하 여 hello 보존 기간을 늘릴 수 있습니다 [hello 서비스 계층을 변경](sql-database-service-tiers.md)합니다. hello 전체 및 차등 데이터베이스 백업은 복제 된 tooa [쌍 이룬된 데이터 센터](../best-practices-availability-paired-regions.md) 데이터 센터 중단 으로부터 보호 합니다. 자세한 내용은 [자동 데이터베이스 백업](sql-database-automated-backups.md)을 참조하세요.

Hello 기본 보존 기간에 응용 프로그램에 대해 충분 하지 않으면 데이터베이스 장기 보존 정책을 구성 하 여 확장할 수 있습니다. 자세한 내용은 [장기 보존](sql-database-long-term-retention.md)을 참조하세요.

이러한 데이터베이스 자동 백업이 toorecover 모두 데이터 센터와 tooanother 데이터 센터 내에서 다양 한 중단 이벤트에서 데이터베이스를 사용할 수 있습니다. 자동 데이터베이스 백업을 사용 하 여, hello 예상 복구 시간 hello hello에 동일한 복구 데이터베이스의 총 수를 비롯 한 여러 요인에 따라 달라 집니다 hello 시간 같은 hello 데이터베이스 크기, hello 트랜잭션 로그 크기 및 네트워크 대역폭에 영역입니다. hello 복구 시간은 일반적으로 12 시간 미만입니다. Tooanother 데이터 영역을 복구할 때는 hello 데이터 손실을 hello 지역 중복 저장소의 시간별 차등 데이터베이스 백업에서 제한 된 too1 시간입니다.

> [!IMPORTANT]
> 자동화 된 백업을 사용 하 여 toorecover, SQL Server 참가자 역할 hello 또는 hello 구독 소유자의 구성원 이어야 합니다.-참조 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)합니다. Hello Azure 포털, PowerShell 또는 REST API hello를 사용 하 여 복구할 수 있습니다. Transact-SQL은 사용할 수 없습니다.
>

다음 조건의 응용 프로그램의 경우, 자동화된 백업을 비즈니스 연속성 및 복구 메커니즘으로 사용합니다.

* 중요 업무용으로 간주되지 않습니다.
* 연계된 SLA가 없으므로 24시간 이상의 가동 중지가 발생해도 재무적 책임이 없습니다.
* 속도가 느린 데이터 변경 (시간당 낮은 트랜잭션)이 있으며 tooan를 손실 시간 변경의 사용할 수 있는 데이터 손실 합니다.
* 비용에 민감합니다.

빠른 복구가 필요한 경우 [활성 지역 복제](sql-database-geo-replication-overview.md)(다음에 설명)를 사용합니다. 35 일 보다 오래 된 기간에서 toobe 수 toorecover 데이터를 유지 해야 하는 경우 사용 하 여 [장기 백업 보존](sql-database-long-term-retention.md)합니다. 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>활성 지리적 복제 및 자동 장애 조치 (에서-미리 보기) 그룹 tooreduce 복구 시간과 제한 관련 된 데이터 손실 복구를 사용 하 여

또한 toousing 데이터베이스 백업에 대 한 데이터베이스 복구는 비즈니스에 문제가 발생 하는 경우, 사용할 수 있습니다 [활성 지리적 복제](sql-database-geo-replication-overview.md) tooconfigure toofour hello 지역에 읽기 가능한 보조 데이터베이스를 데이터베이스 toohave의 사용자 선택입니다. 이러한 보조 데이터베이스는 비동기 복제 메커니즘을 사용 하 여 hello 주 데이터베이스와 동일 하 게 됩니다. 이 기능은 데이터 센터 중단이 발생 하는 경우에 중단을 비즈니스 또는 응용 프로그램 업그레이드를 사용 하는 동안 사용 되는 tooprotect입니다. 활성 지리적 복제에 사용 되는 tooprovide 쿼리 성능을 향상 toogeographically에 분산 하 여 사용자가 읽기 전용 쿼리 될 수도 있습니다.

tooenable 자동화 하 고 지리적으로 복제 된 데이터베이스를 구성 해야 하는 투명 한 장애 조치 hello를 사용 하 여 그룹화 [그룹 자동 장애 조치](sql-database-geo-replication-overview.md) SQL 데이터베이스 (에서-미리 보기)의 기능입니다.

Hello 주 데이터베이스가 예기치 않게 오프 라인 이거나 tootake 오프 라인으로 유지 관리 작업에 대 한 신속 하 게 보조 toobecome hello 주 (장애 조치)을 승격 하 고 구성할 수 tooconnect 승격 toohello 주 응용 프로그램입니다. 응용 프로그램은 hello 장애 조치 그룹 수신기를 사용 하 여 toohello 데이터베이스를 연결 하는 경우 장애 조치 후 toochange hello SQL 연결 문자열 구성이 필요는 없습니다. 계획된 장애 조치를 사용할 경우 데이터는 손실되지 않습니다. 예기치 않은 장애 조치가 있는 일부 적은 양의 비동기 복제의 아주 최근 트랜잭션의 toohello 특성 인해 데이터가 손실 될 수 있습니다. 자동 장애 조치 그룹 (에서-미리 보기)를 사용 하 여 hello 장애 조치 정책 toominimize hello 잠재적 데이터 손실을 사용자 지정할 수 있습니다. 장애 조치 후 이후 장애 복구를 수행할 수 있습니다-따라 tooa 계획 또는 때 hello 데이터 센터가 다시 온라인 상태로 돌아온 합니다. 모든 경우에 사용자는 약간의 가동 중지 시간이 발생 하 고 tooreconnect 필요 합니다.

> [!IMPORTANT]
> toouse 활성 지리적 복제 및 자동 장애 조치 그룹 (에서-미리 보기)을 수행 해야 하거나 hello 구독 소유자 또는 SQL Server의 관리 권한이 있어야 합니다. 구성 및 하거나 REST API Azure 구독 사용 권한 또는 TRANSACT-SQL을 사용 하 여 SQL Server 권한을 가진 hello hello Azure 포털, PowerShell을 사용 하 여 장애 조치할 수 있습니다.
> 

응용 프로그램이 다음 조건에 맞는 경우 활성 지역 복제 및 자동 장애 조치 그룹(미리 보기 상태)을 사용합니다.

* 중요 업무용입니다.
* 24시간 이상의 가동 중지 시간을 허용하지 않는 SLA(서비스 수준 약정)가 있습니다.
* 가동 중지는 재무적 책임을 유발할 수 있습니다.
* 데이터 변경 속도가 높고 1시간에 해당하는 데이터 손실은 허용할 수 없는 수준입니다.
* 활성 지리적 복제의 추가 비용 hello hello 잠재적인 재무 책임과 비즈니스 관련된 손실을 보다 낮습니다.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>사용자 또는 응용 프로그램 오류 발생 이후 데이터베이스 복구
*어느 누구도 완벽하지는 않습니다. 사용자가 실수로 데이터를 삭제할 수도 있고, 의도치 않게 중요한 테이블을 삭제할 수도 있고, 전체 데이터베이스를 삭제할 수도 있습니다. 또는 응용 프로그램 tooan 응용 프로그램 결함 인해 잘못 된 데이터와 적절 한 데이터를 실수로 덮어쓸 수 있습니다.

이러한 시나리오에서 복구 옵션은 다음과 같습니다.

### <a name="perform-a-point-in-time-restore"></a>지정 시간 복원 수행
시간이 hello 데이터베이스 보존 기간 내에 있는 hello 자동화 된 백업을 toorecover 양호 지점 시간 내에 알려진 사용자 데이터베이스 tooa의 복사본을 사용할 수 있습니다. Hello 데이터베이스가 복원 된 후 hello 원본 데이터베이스를 복원 하는 hello 데이터베이스로 바꿉니다 하거나 hello 원본 데이터베이스에 복원 하는 hello 데이터에서 필요한 hello 데이터를 복사 합니다. Hello 데이터베이스 활성 지리적 복제를 사용 하는 경우에 hello 원래 데이터베이스에 복원 하는 hello 복사본에서 hello 필요한 데이터를 복사 하는 것이 좋습니다. 데이터베이스를 복원 하는 hello와 hello 원래 데이터베이스를 대체 하는 경우 tooreconfigure 필요 하 고 (있는 큰 데이터베이스에 다소 시간이 걸릴 수 있습니다) 활성 지리적 복제를 다시 동기화 합니다.

데이터베이스 tooa 지정 시간으로 복원 하는 자세한 단계 및 자세한 내용은 hello Azure 포털 또는 PowerShell을 사용 하 여, 참조 [지정 시간 복원](sql-database-recovery-using-backups.md#point-in-time-restore)합니다. Transact-SQL을 사용하여 복구할 수는 없습니다.

### <a name="restore-a-deleted-database"></a>삭제된 데이터베이스 복원
를 hello 데이터베이스를 삭제 하지만 논리 서버 hello 삭제 되지 않은 경우 삭제 된 hello 삭제 데이터베이스 toohello 지정을 복원할 수 있습니다. 이렇게 하면 데이터베이스 백업 toohello 복원 논리 동일한 SQL server 삭제 되었습니다. 새 이름 또는 hello 복원 된 데이터베이스를 지정 하거나 hello 원래 이름을 사용 하 여 복원할 수 있습니다.

Azure 포털 또는 PowerShell을 사용 하 여 참조 하 고 hello를 사용 하 여 삭제 된 데이터베이스를 복원 하는 자세한 단계에 대 한 자세한 내용은 [삭제 된 데이터베이스 복원](sql-database-recovery-using-backups.md#deleted-database-restore)합니다. Transact-SQL을 사용하여 복원할 수는 없습니다.

> [!IMPORTANT]
> Hello 논리 서버를 삭제 하면 삭제 된 데이터베이스를 복구할 수 없습니다.
>
>

### <a name="restore-from-azure-backup-vault"></a>Azure 백업 자격 증명 모음에서 복원
자동화 된 백업에 대 한 현재 보존 기간 hello 외부 hello 데이터 손실이 발생 하는 경우 데이터베이스가 장기 보존을 위해 구성 된 Azure 백업 자격 증명 모음 tooa 새 데이터베이스에 매주 백업에서 복원할 수 있습니다. 이 시점에서 hello 원본 데이터베이스를 복원 하는 hello 데이터베이스로 바꿉니다 하거나 hello 원본 데이터베이스에 복원 하는 hello 데이터베이스에서 필요한 hello 데이터를 복사 합니다. 이전 버전 데이터베이스의 이전 tooa 주요 응용 프로그램 업그레이드의 tooretrieve 해야 할 경우는 감사자 또는 법적 순서에서 요청을 충족 hello Azure 백업 자격 증명 모음에에서 저장 된 전체 백업을 사용 하 여 데이터베이스를 만들 수 있습니다.  자세한 내용은 [장기 보존](sql-database-long-term-retention.md)을 참조하세요.

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>데이터베이스 tooanother 영역 Azure 지역 데이터 센터 중단에서 복구
<!-- Explain this scenario -->

드문 경우지만 Azure 데이터 센터에서 가동 중단이 발생할 수 있습니다. 가동 중단이 발생하면 몇 분 내지 몇 시간 동안 지속될 수 있는 업무 중단이 발생합니다.

* 한 가지 방법은 hello 데이터 센터 중단 올려 놓을 때 다시 온라인에 데이터베이스 toocome에 대 한 toowait 합니다. 이 toohave hello를 오프 라인 데이터베이스를 감당할 수 있는 응용 프로그램에 적합 합니다. 예를 들어 개발 프로젝트 또는 무료 평가판 않아도 toowork에 지속적으로 됩니다. 데이터 센터에 중단을 알지 못하는 hello 중단이 지속 될 수 있습니다는 기간 하므로이 옵션은 잠시 동안 데이터베이스에 필요 하지 않으면 합니다.
* 두 번째 방법은 tooeither 장애 tooanother 데이터 영역을 통해 hello 지역 중복 데이터베이스 백업이 (지역에서 복원은)를 사용 하 여 데이터베이스를 복구 또는 활성 지리적 복제를 사용 하는 경우. 백업에서 데이터베이스를 복구하는 데는 몇 시간이 걸리지만 장애 조치는 몇 초면 끝납니다.

작업을 수행 하는 경우 시간을 예상 하면 toorecover, 어느 정도 발생 하는 데이터 손실에 따라 다릅니다 toouse를 결정 하는 방법 응용 프로그램에서 이러한 비즈니스 연속성 기능입니다. 실제로, 데이터베이스 백업 및 응용 프로그램 요구 사항에 따라 활성 지리적 복제를 조합한 toouse를 선택할 수 있습니다. 이러한 비즈니스 지속성 기능을 사용하는 독립 실행형 데이터베이스 및 탄력적 풀에 대한 응용 프로그램 디자인 고려 사항에 대한 자세한 내용은[ 클라우드 재해 복구를 위해 응용 프로그램 디자인](sql-database-designing-cloud-solutions-for-disaster-recovery.md) 및 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.

hello 다음 섹션에서는 데이터베이스 백업 또는 활성 지리적 복제를 사용 하 여 hello 단계 toorecover의 개요. 자세한 단계는 계획 요구 사항, post 복구 단계 및 방법 toosimulate 중단 tooperform 재해 복구 드릴 하는 방법에 대 한 정보를 포함 하 여를 참조 하십시오. [SQL 데이터베이스 가동 중단에서 복구](sql-database-disaster-recovery.md)합니다.

### <a name="prepare-for-an-outage"></a>가동 중단에 대비
Hello 비즈니스 연속성 기능 사용에 관계 없이 다음 작업을 수행 해야 합니다.

* 식별 하 고 서버 수준 방화벽 규칙, 로그인 및 master 데이터베이스 수준 사용 권한을 포함 하 여 hello 대상 서버를 준비 합니다.
* 확인 방법을 tooredirect 클라이언트 및 클라이언트 응용 프로그램 toohello 새 서버
* 감사 설정 및 경고와 같은 다른 종속성을 문서화합니다.

적절한 준비 없이 장애 조치나 데이터베이스 복구 이후에 응용 프로그램을 온라인 상태로 전환하면 추가 시간이 소요되고, 바쁜 업무 중 문제 해결이 필요할 수도 있어 비효율적입니다.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Tooa 지리적 복제 보조 데이터베이스 장애 조치
활성 지역 복제 및 자동 장애 조치 그룹(미리 보기 상태)을 복구 메커니즘으로 사용할 경우 자동 장애 조치 정책을 구성하거나 [수동 장애 조치](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database)를 사용할 수 있습니다. 시작 되 면 hello 장애 조치 원인 hello 보조 toobecome 새로운 기본 및 준비 toorecord 새 트랜잭션이 hello 및 tooqueries-아직 복제 하지 않은 hello 데이터에 대 한 최소한의 데이터 손실에 응답 합니다. 에 대 한 내용은 hello 장애 조치 프로세스를 디자인, [클라우드 재해 복구를 위해 응용 프로그램 디자인](sql-database-designing-cloud-solutions-for-disaster-recovery.md)합니다.

> [!NOTE]
> Hello 데이터 센터가 다시 온라인 상태가 되 hello 이전 보관 자동으로 toohello 새로운 주에 다시 연결 하 고 데이터베이스가 됩니다. 계획된 된 장애 조치를 수동으로 시작할 수 toorelocate hello 기본 백 toohello 원래 영역 해야 할 경우 (failback) 합니다. 
> 

### <a name="perform-a-geo-restore"></a>지역 복원 수행
복구 메커니즘으로 지역 중복 저장소 복제와 자동화된 백업을 함께 사용하는 경우 [지역 복원을 사용하여 데이터베이스 복구를 시작](sql-database-disaster-recovery.md#recover-using-geo-restore)합니다. 일반적으로 발생 12 시간 이내에 복구-데이터 손실이 가장 tooone 시간에 의해 결정 hello를 촬영 하 고 복제를 사용 하 여 시간별 차등 백업을 마지막 합니다. Hello 복구 완료 될 때까지 hello 데이터베이스가 없습니다 toorecord 모든 트랜잭션을 인지 tooany 쿼리 응답 합니다. 데이터베이스 toohello 마지막 사용할 수 있는 지정 시간으로 복원이 하는 동안 hello 지역 보조 tooany 지점 지정 시간으로 복원할 현재 지원 되지 않습니다.

> [!NOTE]
> Toohello 복구 된 데이터베이스에 대해 응용 프로그램 전환 하기 전에 hello 데이터 센터 온라인 상태가 되 면 hello 복구를 취소할 수 있습니다.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>사후 장애 조치(failover)/복구 작업 수행
복구 메커니즘 중 하나에서 복구 후 사용자와 응용 프로그램을 백업 하기 전에 추가 작업을 수행 하 고 실행 하는 hello를 수행 해야 합니다.

* 리디렉션 클라이언트 및 클라이언트 응용 프로그램 toohello 새 서버와 복원 된 데이터베이스
* 적절 한 서버 수준 방화벽 규칙이 tooconnect 사용자에 대 한 마련 되어 있는지 확인 (사용 또는 [데이터베이스 수준 방화벽](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* 적절한 로그인 및 master 데이터베이스 수준 사용 권한이 설정되었는지 확인합니다(또는 [포함된 사용자](https://msdn.microsoft.com/library/ff929188.aspx)사용).
* 필요에 따라 감사를 구성합니다.
* 필요에 따라 경고를 구성합니다.

## <a name="upgrade-an-application-with-minimal-downtime"></a>최소 가동 중단으로 응용 프로그램 업그레이드
응용 프로그램 업그레이드와 같은 계획된 유지 관리로 인해 응용 프로그램을 오프라인 상태로 전환해야 하는 경우도 있습니다. [응용 프로그램 업그레이드 관리](sql-database-manage-application-rolling-upgrade.md) 롤링 업그레이드 하면 클라우드 응용 프로그램 toominimize 가동 중지 시간 동안 toouse 활성 지리적 복제 tooenable 업그레이드 하는 방법에 대해 설명 하 고 문제가 발생 한 경우 복구 경로 지정 합니다. 

## <a name="next-steps"></a>다음 단계
독립 실행형 데이터베이스 및 탄력적 풀에 대한 응용 프로그램 디자인 고려 사항에 대한 자세한 내용은[ 클라우드 재해 복구를 위해 응용 프로그램 디자인](sql-database-designing-cloud-solutions-for-disaster-recovery.md) 및 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.
