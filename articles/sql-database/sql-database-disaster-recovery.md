---
title: "aaaSQL 데이터베이스 재해 복구 | Microsoft Docs"
description: "Azure SQL 데이터베이스 활성 지리적 복제 및 지리적 복원 기능 toorecover 지역의 데이터 센터 가동 중단 또는 사용 하 여 오류에서 데이터베이스 hello 하는 방법에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Azure SQL 데이터베이스 또는 장애 조치 tooa 보조 복원
Azure SQL 데이터베이스는 hello 다음 가동 중단에서 복구에 대 한 기능을 제공 합니다.

* [활성 지역 복제](sql-database-geo-replication-overview.md)
* [지역 복원](sql-database-recovery-using-backups.md#point-in-time-restore)

이러한 시나리오를 지 원하는 hello 기능과 비즈니스 연속성 시나리오에 대 한 toolearn 참조 [비즈니스 연속성](sql-database-business-continuity.md)합니다.

### <a name="prepare-for-hello-event-of-an-outage"></a>중단의 hello 이벤트에 대 한 준비
활성 지리적 복제 또는 지역 중복 백업을 사용 하 여 복구 tooanother 데이터 영역에 성공 해야 tooprepare 다른 데이터 센터 가동 중단 toobecome hello 새 주 서버에서 서버 해야 hello 필요 발생으로 잘 정의 된 단계 문서화 하 고 테스트 된 tooensure 부드러운 복구 합니다. 이러한 준비 단계는 다음과 같습니다.

* 다른 지역 toobecome hello 새 주 서버에서 논리 서버 hello를 식별 합니다. 활성 지리적 복제 사용이 하나 이상 및 아마도 각 보조 서버 hello 됩니다. 에 지역에서 복원은 일반적으로 됩니다 서버 hello에 [쌍을 이루는 지역](../best-practices-availability-paired-regions.md) 데이터베이스의 위치를 가리키는 hello 영역에 대 한 합니다.
* 식별 하 고, 필요에 따라, hello 서버 수준 방화벽 규칙을 정의 필요한에 사용자를 위한 tooaccess hello 새로운 주 데이터베이스입니다.
* 방법을 tooredirect 사용자 toohello 새 주 서버와 같은 연결 문자열을 변경 하 여 또는 DNS 항목을 변경 하 여 확인 합니다.
* 를 식별 하 고 필요에 따라 만들기, hello hello hello 새 주 서버에서 master 데이터베이스에 존재 하 고 있는 경우 이러한 로그인 hello master 데이터베이스에서 적절 한 권한이 있는지 확인 해야 하는 로그인 합니다. 자세한 내용은 [재해 복구 후 Azure SQL 데이터베이스 보안](sql-database-geo-replication-security-config.md)
* 가 toobe 업데이트 toomap toohello 새로운 주 데이터베이스를 필요로 하는 경고 규칙을 식별 합니다.
* Hello 현재 주 데이터베이스에서 문서 hello 감사 구성
* [재해 복구 훈련](sql-database-disaster-recovery-drills.md)을 수행합니다. 지역에서 복원에 대 한 중단은 toosimulate 삭제 하거나 hello 원본 데이터베이스 toocause 응용 프로그램 연결 실패의 이름을 바꿀 수 있습니다. 활성 지리적 복제에 대 한 중단 toosimulate hello 웹 응용 프로그램 또는 연결 된 가상 컴퓨터 toohello 데이터베이스 또는 장애 조치 hello 데이터베이스 toocause 응용 프로그램 연결 실패를 해제할 수 있습니다.

## <a name="when-tooinitiate-recovery"></a>때 tooinitiate 복구
hello 복구 작업 hello 응용 프로그램에 영향을 줍니다. Hello SQL 연결 문자열 또는 DNS를 사용 하 여 리디렉션을 변경 해야 하 고 데이터가 영구적으로 손실 될 수 있습니다. 따라서 hello 중단 가능성이 toolast 응용 프로그램의 복구 시간 목표 보다 긴 경우에 수행 되어야 합니다. Hello 응용 프로그램은 배포 된 tooproduction 때 hello 응용 프로그램 상태를 정기적으로 모니터링 하 고 같은 hello 복구 포인트 tooassert이 보장 되는 데이터가 hello를 사용 해야:

1. Hello 응용 프로그램 계층 toohello 데이터베이스에서 영구 연결이 실패 합니다.
2. Azure 포털 hello 광범위 한 영향을 사용 하 여 hello 영역의 인시던트에 대 한 경고를 보여 줍니다.
3. hello Azure SQL 데이터베이스 서버가 저하 됨으로 표시 됩니다.

응용 프로그램 허용 오차 toodowntime 및 가능한 비즈니스 책임에 따라 hello 다음 복구 옵션을 고려할 수 있습니다.

사용 하 여 hello [복구 가능한 데이터베이스](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget hello 최신 지리적 복제 복원 지점입니다.

## <a name="wait-for-service-recovery"></a>서비스 복구 대기
hello Azure 팀은 충분히 toorestore 서비스 가용성 신속 하 게 최대한 하지만 hello 근본 원인에 따라 걸리는 시간 또는 날짜 처럼 합니다.  응용 프로그램 상당한 가동 중지 시간을 허용할 수 있는 경우에 복구 toocomplete hello에 대 한 단순히 대기할 수 있습니다. 이 경우에 사용자의 조치가 필요하지 않습니다. hello 현재 서비스 상태를 확인할 수 있습니다이 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/)합니다. Hello 영역의 hello 복구 후 응용 프로그램의 가용성을 복원 됩니다.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>보조 데이터베이스 toogeo 복제 장애 조치
응용 프로그램의 가동 중지 시간으로 인해 비즈니스 책임이 발생할 수 있는 경우 응용 프로그램에서 지역에서 복제된 데이터베이스를 사용해야 합니다. 프로그램 중단 시 다른 지역에 응용 프로그램 tooquickly 복원 가용성 hello를 활성화 합니다. 너무 방법에 대해 알아봅니다[지리적 복제를 구성](sql-database-geo-replication-portal.md)합니다.

hello toorestore 가용성 데이터베이스 하면 필요한 tooinitiate hello 장애 조치 toohello 지리적 복제 보조 hello 지원 방법 중 하나를 사용 하 여 합니다.

Hello 가이드 toofail tooa 지리적 복제 보조 데이터베이스에 대해 다음 중 하나를 사용 합니다.

* [Azure 포털을 사용 하 여 tooa 지리적 복제 보조 장애 조치합니다](sql-database-geo-replication-portal.md)
* [장애 조치 tooa 지리적 복제 보조 PowerShell을 사용 하 여](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [장애 조치 T-SQL을 사용 하 여 tooa 지리적 복제 보조](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>지역 복원을 사용한 복구
응용 프로그램의 가동 중지 시간 비즈니스 책임 내보내지지 않습니다 경우 사용할 수 있습니다 [지역에서 복원은](sql-database-recovery-using-backups.md) 메서드 toorecover로 응용 프로그램 데이터베이스입니다. 최신 지역 중복 백업에서 hello 데이터베이스의 복사본을 만듭니다.

## <a name="configure-your-database-after-recovery"></a>복구 후 데이터베이스 구성
지리적 복제 장애 조치 또는 지역에서 복원은 toorecover 중단에서 중 하나를 사용 하는 경우 hello 일반 응용 프로그램 기능을 다시 시작 될 수 있도록 hello 연결 toohello 새 데이터베이스가 제대로 구성 되어 있는지 확인 해야 합니다. 이것은 작업 tooget의 검사 목록 복구 된 데이터베이스 생성 준비 상태입니다.

### <a name="update-connection-strings"></a>연결 문자열 업데이트
복구 된 데이터베이스는 다른 서버에 상주 합니다, 하기 때문에 tooupdate 응용 프로그램의 연결 문자열 toopoint toothat 서버가 필요 합니다.

Hello 적절 한 개발 언어에 대 한 연결 문자열을 변경 하는 방법에 대 한 자세한 내용은 참조 프로그램 [연결 라이브러리](sql-database-libraries.md)합니다.

### <a name="configure-firewall-rules"></a>방화벽 규칙 구성
Toomake hello 방화벽 규칙 구성 서버와 일치 하는 hello 데이터베이스 항목에 hello 주 서버와 주 데이터베이스에 대해 구성 된 하는 필요 합니다. 자세한 내용은 [방법: 방화벽 설정 구성(Azure SQL 데이터베이스)](sql-database-configure-firewall-settings.md)을 참조하세요.

### <a name="configure-logins-and-database-users"></a>로그인 및 데이터베이스 사용자 구성
응용 프로그램에서 사용 하는 모든 hello 로그인 복구 된 데이터베이스를 호스트 하 고 있는 hello 서버에 존재 하는지 toomake가 필요 합니다. 자세한 내용은 [지역에서 복제를 위한 보안 구성](sql-database-geo-replication-security-config.md)을 참조하세요.

> [!NOTE]
> 재해 복구 훈련 동안 서버 방화벽 규칙 및 로그인(및 해당 사용 권한)을 구성하고 테스트해야 합니다. 이 서버 수준 개체 및 해당 구성 하지 못할 hello 중단 중입니다.
> 
> 

### <a name="setup-telemetry-alerts"></a>원격 분석 경고 설정
기존 경고 규칙 설정이 업데이트 된 toomap toohello 복구 된 데이터베이스와 hello 다른 서버 인지 toomake가 필요 합니다.

데이터베이스 경고 규칙에 대한 자세한 내용은 [경고 알림 수신](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) 및 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.

### <a name="enable-auditing"></a>감사 사용
감사 하는 경우 필요한 tooaccess 프로그램 데이터베이스가 tooenable 필요한 hello 데이터베이스 복구 후 감사 합니다. 자세한 내용은 [Database 감사](sql-database-auditing.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
* Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [자동화 된 백업을 SQL 데이터베이스](sql-database-automated-backups.md)
* 비즈니스 연속성 디자인 및 복구 시나리오에 대 한 toolearn 참조 [연속성 시나리오](sql-database-business-continuity.md)
* 복구를 위한 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [hello 서비스 개시 백업에서 데이터베이스를 복원 합니다.](sql-database-recovery-using-backups.md)

