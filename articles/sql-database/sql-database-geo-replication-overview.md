---
title: "aaaFailover 그룹 및 활성 지리적 복제-Azure SQL 데이터베이스 | Microsoft Docs"
description: "활성 지리적 복제와 자동 장애 조치 그룹 hello Azure 데이터 센터 중 하나에서 데이터베이스 및 가동 중단의 hello 이벤트에서 autoomatically 장애 조치의 toosetup 4 복제본이 있습니다."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>개요: 장애 조치 그룹 및 활성 지역 복제
활성 지리적 복제 하면 tooconfigure toofour hello에 읽기 가능한 보조 데이터베이스를 동일한 또는 다른 데이터 센터 위치 (지역). 보조 데이터베이스는 쿼리 및 데이터 센터 가동 중단 또는 hello 불가능 tooconnect toohello 주 데이터베이스의 hello 경우에서 장애 조치에 대해 사용할 수 있습니다. hello 장애 조치 hello 사용자의 hello 응용 프로그램에 의해 수동으로 시작 해야 합니다. 장애 조치 후 새 주 서버 hello는 다른 연결 끝점을 있습니다. 

> [!NOTE]
> 활성 지역 복제는 모든 지역의 현재 모든 서비스 계층에 있는 모든 데이터베이스에 대해 제공됩니다.
>  

Azure SQL 데이터베이스 자동 장애 조치 그룹 (에서-미리 보기)는 SQL 데이터베이스 기능 tooautomatically 지리적 복제 관계, 연결 및 규모에 장애 조치 관리 합니다. Hello 고객 이득 hello 기능 tooautomatically 국가별의 치명적 오류 또는 SQL 데이터베이스 서비스의 hello 전체 또는 부분 손실이 발생 하는 기타 계획 되지 않은 이벤트 후 hello 보조 지역에서 여러 관련된 데이터베이스 복구 기본 지역의 hello 가용성입니다. 또한 hello 읽기 가능한 보조 데이터베이스 toooffload 읽기 전용 작업을 사용할 수 있습니다.  자동 장애 조치 그룹이 여러 데이터베이스를 포함 하기 때문에 주 서버 hello 구성 되어야 합니다. 기본 및 보조 서버 hello에 있어야 합니다. 동일한 구독 합니다. 자동 장애 조치 그룹 hello 그룹 tooonly 한 보조 서버에서 다른 지역에 모든 데이터베이스의 복제를 지원합니다. 활성 지리적 복제, 자동 장애 조치 그룹 없이 모든 지역에서 too4 보조 복제본을 수 있습니다.

주 데이터베이스 실패 이유 또는 단순히 오프 라인으로 전환 하는 요구 toobe 및을 활성 지리적 복제를 사용 하는 경우에 보조 데이터베이스의 장애 조치 tooany를 시작할 수 있습니다. 모든 보조 복제본은 자동으로 연결 된 toohello hello 보조 데이터베이스의 활성화 된 tooone 장애 조치의 경우 새 주 데이터베이스입니다. 자동 장애 조치를 사용 하는 경우 (에서-미리 보기) toomanage 데이터베이스 복구 및 hello 그룹 결과 자동 장애 조치에서의 hello 데이터베이스 중 하나 또는 여러에 영향을 주는 모든 중단을 그룹화 합니다. 응용 프로그램 요구 사항에 가장 잘 맞는 hello 자동 장애 조치 정책을 구성할 수 있습니다 또는 옵트아웃 하 고 수동 정품 인증을 사용할 수 있습니다. 또한 자동 장애 조치 그룹(미리 보기 상태)은 장애 조치하는 동안 변경되지 않는 읽기-쓰기 및 읽기 전용 수신기 끝점을 제공합니다. 자동 또는 수동 장애 조치 정품 인증을 사용 하 든 hello 그룹 tooprimary에 모든 보조 데이터베이스를 전환 하는 장애 조치입니다. Hello 데이터베이스 장애 조치 완료 되 면 hello DNS 레코드에는 자동으로 업데이트 된 tooredirect hello 끝점이 모두 toohello 새 영역입니다.

활성 지역 복제를 사용하여 서버 또는 탄력적 풀에 있는 개별 데이터베이스 또는 데이터베이스 집합의 복제 및 장애 조치를 관리할 수 있습니다. 사용 하 여 해당 하는 작업을 수행할 수 hello [Azure 포털](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [TRANSACT-SQL](sql-database-geo-replication-transact-sql.md), 또는 hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)합니다. 장애 조치 후 서버 및 데이터베이스에 대 한 hello 인증 요구 사항을 hello 새 주 데이터베이스에 구성 되어를 확인 합니다. 자세한 내용은 [재해 복구 후의 SQL Database 보안](sql-database-geo-replication-security-config.md)을 참조하세요. 이 두 tooactive 지리적 복제 및 자동 장애 조치 그룹 (에서-미리 보기) 적용 됩니다.

활성 지리적 복제 이용 하 여 hello [Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) tooasynchronously SQL Server의 기술 hello 주 데이터베이스 tooa 보조 데이터베이스 읽기 커밋된 스냅숏 격리 (RCSI)를 사용 하 여 커밋된 트랜잭션을 복제 합니다. 자동 장애 조치 그룹 활성 지리적 복제 하지만 동일한 비동기 복제 메커니즘을 사용 하는 hello 위에 hello 그룹 의미 체계를 제공 합니다. 지정된 된 지점에 있는 동안 hello 보조 데이터베이스는 hello 주 데이터베이스 보다 약간 있을 수 있으며, hello 보조 데이터는 toonever 있는 부분 트랜잭션이 있습니다. 지역 간 중복성을 영구히의 응용 프로그램 tooquickly 복구를 전체 데이터 센터 또는 자연 재해, 심각한 사용자 오류 또는 악의적인 행위로 인해 발생 하는 데이터 센터의 일부분을 수 있습니다. hello 특정 RPO 데이터에서 찾을 수 있습니다 [개요의 비즈니스 연속성](sql-database-business-continuity.md)합니다.

hello 다음 그림의 예가 나와 활성 지리적 복제 구성 된 hello North Central US 지역은에서 기본 및 보조 hello 미국 중남부 지역에 있습니다.

![지역에서 복제 관계](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Hello 보조 데이터베이스를 읽을 수 있으므로 작업을 보고와 같은 사용된 toooffload 읽기 전용 작업을 수 있습니다. 활성 지리적 복제를 사용 하는 경우 가능한 toocreate hello에 대 한 보조 데이터베이스 hello에 hello 주 하지만와 동일한 지역 hello 응용 프로그램의 복원 력을 toocatastrophic 오류 증가 하지 않습니다. 자동 장애 조치 그룹(미리 보기 상태)을 사용하는 경우 보조 데이터베이스는 항상 다른 지역에 만들어집니다.

또한 toodisaster 복구 활성 지리적 복제는 다음 시나리오는 hello에 사용할 수 있습니다.

* **데이터베이스 마이그레이션**: 최소 가동 중지 시간을 활성 지리적 복제 toomigrate 하나의 서버 tooanother 온라인에서 데이터베이스를 사용할 수 있습니다.
* **응용 프로그램 업그레이드**: 응용 프로그램을 업그레이드하는 동안 추가 보조 데이터베이스를 장애 복구 복사본으로 만들 수 있습니다.

tooachieve 실제 비즈니스 연속성, 데이터 센터 간 데이터베이스 중복성 추가 것 hello 솔루션의 일부분에 불과합니다. 치명적인 오류 필요 hello 서비스를 구성 하는 모든 구성 요소와 모든 종속 서비스의 복구 후에 응용 프로그램 (서비스)에 종단 간를 복구 합니다. 이러한 구성 요소의 예로 hello 클라이언트 소프트웨어 (예를 들어 사용자 지정 JavaScript 사용 하 여 브라우저), 웹 프런트 엔드, 저장소 및 DNS를 들 수 있습니다. 모든 구성 요소는 복원 력이 toohello 동일한 오류 및 응용 프로그램의 hello 복구 시간 목표 (RTO) 내에서 사용할 수 있게 합니다. 따라서 모든 종속 서비스 tooidentify 필요 하 고 hello 보장 및 제공 하는 기능을 이해 합니다. 그런 다음 적절 한 단계 tooensure 하는 동안 서비스 함수 hello 종속 된 hello 서비스의 장애 조치를 수행 해야 합니다. 재해 복구를 위한 솔루션 설계에 대한 자세한 내용은 [활성 지역 복제를 사용하여 재해 복구를 위한 클라우드 솔루션 설계](sql-database-designing-cloud-solutions-for-disaster-recovery.md)를 참조하세요.

## <a name="active-geo-replication-capabilities"></a>활성 지역 복제 기능
hello 활성 지리적 복제 기능에서는 hello를 다음 필수 기능을 제공 합니다.
* **자동 비동기 복제**: tooan 기존 데이터베이스를 추가 하 여 보조 데이터베이스 에서만 만들 수 있습니다. 모든 Azure SQL 데이터베이스 서버에서 보조 hello는 만들 수 있습니다. 를 만든 후 보조 데이터베이스 hello hello 주 데이터베이스에서 복사 하는 hello 데이터로 채워집니다. 이 프로세스를 시드라고 합니다. 보조 데이터베이스를 생성 하 고 시드 된 후 업데이트 toohello 주 데이터베이스는 비동기적으로 자동으로 toohello 보조 데이터베이스를 복제 합니다. 비동기 복제는 복제 된 toohello 보조 데이터베이스를 되기 전에 트랜잭션은 hello 주 데이터베이스에서 커밋됩니다 의미 합니다. 
* **읽기 가능한 보조 데이터베이스**: 읽기 전용 작업을 사용 하 여 hello 동일 하거나 서로 다른 보안 주체 hello 주 데이터베이스에 액세스 하기 위해 사용 되는 응용 프로그램에서 보조 데이터베이스를 액세스할 수 있습니다. hello 보조 데이터베이스에서에서 작동 스냅숏 격리 모드 tooensure 복제의 기본 hello hello 업데이트 (로그 재생) 쿼리가 hello 보조에서 실행 하 여 지연 되지 않습니다.

   > [!NOTE]
   > 업데이트가 있는 경우 스키마 hello hello 보조 데이터베이스에 스키마 잠금이 필요로 하는 기본에서에서 수신 하는지 hello 로그 재생 hello 보조 데이터베이스에서 지연 됩니다. 
   > 

* **읽기 가능한 보조 복제본을 여러**: 둘 이상의 보조 데이터베이스 중복성 및 hello 주 데이터베이스와 응용 프로그램에 대 한 보호 수준을 증가 합니다. 여러 보조 데이터베이스가 있으면 hello 보조 데이터베이스 중 하나에 오류가 발생 해도 hello 응용 프로그램 보호가 유지 됩니다. Hello 응용 프로그램이 노출 될 보조 데이터베이스를 하나만 실패할 경우 새 보조 데이터베이스를 만들 때까지 toohigher 위험 합니다.

   > [!NOTE]
   > 활성 지리적 복제 toobuild 전 세계적으로 분산된 응용 프로그램을 사용 하는 경우 필요한 tooprovide 읽기 전용 액세스 toodata 4 개 이상의 영역에는 보조 데이터베이스 (체인으로 알려진 프로세스)의 보조을 만들 수 있습니다. 이렇게 하면 거의 제한이 없는 규모의 데이터베이스 복제를 수행할 수 있습니다. 또한 체인 hello 주 데이터베이스에서 복제의 hello 오버 헤드를 줄입니다. hello 대신 hello 리프 대부분 보조 데이터베이스에서 hello 증가 복제 지연 됩니다. 에서도 확인할 수 있습니다. 
   >

* **탄력적 풀 데이터베이스 지원**: 모든 탄력적 풀의 모든 데이터베이스에 대해 활성 지역 복제를 구성할 수 있습니다. hello 보조 데이터베이스는 다른 탄력적 풀에 있는 수 있습니다. 일반 데이터베이스에 대 한 보조 hello 탄력적 풀 수 있고 그 반대로 hello 서비스 계층은으로 hello 동일 합니다. 
* **Hello 보조 데이터베이스의 구성 가능한 성능 수준을**: 보조 데이터베이스를 기본 hello에 비해 더 낮은 성능 수준으로 만들 수 있습니다. 기본 및 보조 데이터베이스는 필수 toohave hello와 동일한 서비스 계층입니다. 이 방법은 권장 되지 않습니다 응용 프로그램에 대 한 높은 데이터베이스 쓰기 활동 hello 증가 복제 지연 장애 조치 후 hello 상당한 데이터 손실 위험을 증가 하기 때문에 있습니다. 또한 새 hello 될 때까지 장애 조치 hello 응용 프로그램의 성능이 저하 되어 후 기본는 업그레이드 된 tooa 더 높은 성능 수준입니다. hello Azure 포털에 로그 IO 백분율 차트 제공 좋은 방법 tooestimate hello 필요한 toosustain hello 복제 부하를 보조 hello의 최소한의 성능 수준입니다. 예를 들어 주 데이터베이스를 P6 (1000 DTU) 보조 50 %hello 필요한 toobe 최소한 해당 로그 IO 백분율 이며 P4 (500 DTU). Hello 로그 IO 사용 하 여 데이터를 검색할 수도 있습니다 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) 또는 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) 데이터베이스 뷰.  Hello SQL 데이터베이스 성능 수준에 대 한 자세한 내용은 참조 하십시오. [SQL 데이터베이스 옵션 및 성능](sql-database-service-tiers.md)합니다. 
* **사용자 제어 장애 조치 및 장애 복구**: 보조 데이터베이스에 명시적으로 언제 든 지 hello 응용 프로그램 또는 hello 사용자가 주 역할로 전환 된 toohello 될 수 있습니다. 실제 정지 hello 하는 동안 "계획 되지 않은" 옵션 사용 하는지는 즉시 보조 toobe hello 주를 올립니다. 실패 한 주 hello 복구 하 고 ´ ï ´ 다시 hello 시스템 자동으로 표시 hello 보조 데이터베이스로 기본을 복구할 hello 새 주 데이터베이스를 최신 상태로 전환 합니다. 복제의 비동기 특성 toohello, 기한 적은 양의 데이터 손실 될 수 있습니다 계획 되지 않은 장애 조치를 수행 하는 동안 기본 hello 가장 최근 변경 내용을 toohello 보조 복제 되기 전에 실패 하는 경우. 여러 개의 보조 복제본으로 한 기본 장애 조치, hello 시스템 hello 복제 관계를 자동으로 재구성 하 고 링크 hello 새로 보조 toohello 남아 있는 모든 사용자 개입이 필요 없이 기본 승격 합니다. Hello 장애 조치를 발생 시킨 hello 중단 완화 될 후 바람직한 tooreturn hello 응용 프로그램 toohello 기본 지역 수 있습니다. hello 장애 조치 명령은 hello로 호출할지, toodo "계획 된" 옵션입니다. 
* **자격 증명 및 방화벽 규칙을 동기화 유지**:를 사용 하는 것이 좋습니다 [데이터베이스 방화벽 규칙](sql-database-firewall-configure.md) 지리적으로 복제 된 데이터베이스에 대 한 이러한 규칙 hello 데이터베이스 tooensure로 복제할 수 있도록 모든 보조 데이터베이스의 경우 기본 hello와 같은 방화벽 규칙을 hello 합니다. 이 방법은 toomanually 구성 하 고 모두 hello 주 데이터베이스와 보조 데이터베이스를 호스팅하는 서버에서 방화벽 규칙을 유지 관리 하는 고객에 대 한 hello 필요성을 제거 합니다. 마찬가지로, 사용 하 여 [포함 된 데이터베이스 사용자](sql-database-manage-logins.md) 데이터에 대 한 액세스 사용 주 및 보조 데이터베이스는 항상 동일한 사용자의 자격 증명 이므로 장애 조치 중 없습니다 중단 hello 게 로그인이 있는 due toomismatches 및 암호입니다. Hello 추가 [Azure Active Directory](../active-directory/active-directory-whatis.md), 고객 사용자 액세스 tooboth 기본 및 보조 데이터베이스를 관리할 수 있습니다 및 데이터베이스에 대 한 자격 증명을 완전히 관리에 필요한 hello를 제거 합니다.

## <a name="auto-failover-group-capabilities"></a>자동 장애 조치 그룹 기능

자동 장애 조치 그룹 기능은 그룹 수준 복제 및 자동 장애 조치를 지원하여 활성 지역 복제의 강력한 추상화를 제공합니다. 또한 hello 추가 수신기 끝점을 제공 하 여 장애 조치 후 hello 필요 toochange hello SQL 연결 문자열을 제거 됩니다. 

* **장애 조치 그룹**: 다른 지역의 두 서버 (기본 및 보조 서버) 간에 하나 이상의 장애 조치 그룹을 만들 수 있습니다. 각 그룹은 일부 또는 모든 주 복제본은 tooan 정전 hello 기본 지역으로 인해 사용할 수 없게 되는 경우 하나의 단위로 복구 하는 하나 또는 여러 데이터베이스를 포함할 수 있습니다.  
* **주 서버**: hello hello 장애 조치 그룹의 주 데이터베이스를 호스팅하는 서버입니다.
* **보조 서버**: hello hello 장애 조치 그룹에 보조 데이터베이스를 호스팅하는 서버입니다. hello 보조 서버 hello에 있을 수 없습니다 hello 주 서버와 동일한 영역입니다.
* **추가 데이터베이스 toofailover 그룹**: 서버 내에서 여러 데이터베이스를 넣을 수도 있고 내는 탄력적인 풀 hello에 동일한 그룹 장애 조치 합니다. 보조 데이터베이스를 자동으로 만듭니다 독립 실행형 데이터베이스 toohello 그룹을 추가 하는 경우 동일한 버전 및 성능 수준 hello를 사용 하 여 합니다. Hello 주 데이터베이스는 탄력적인 풀에 있으면 hello 보조가 자동으로 생성 hello 탄력적 풀 hello로 동일한 이름입니다. Hello 보조 서버에서 보조 데이터베이스에 이미 있는 데이터베이스를 추가 하는 경우 해당 지리적 복제 hello 그룹에 의해 상속 됩니다.

   > [!NOTE]
   > 이미 hello 그룹 장애 조치의 포함 되지 않은 서버에서 보조 데이터베이스를 포함 하는 데이터베이스를 추가할 때 새 보조 데이터베이스 hello 보조 서버에 만들어집니다. 
   >

* **읽기 / 쓰기 Failover 수신기**:으로 형성 된 A DNS CNAME 레코드  **&lt;장애 조치 그룹 이름&gt;. database.windows.net** toohello 현재 주 서버 URL을 가리키는 합니다. 읽기 / 쓰기 SQL 응용 프로그램 hello 허용 tootransparently hello 기본 장애 조치 후 변경 될 때 toohello 주 데이터베이스를 다시 연결 합니다. 
* **장애 조치 그룹 읽기 전용 수신기**:으로 형성 된 A DNS CNAME 레코드  **&lt;장애 조치 그룹 이름&gt;. secondary.database.windows.net** toohello 보조 서버 URL을 가리키는 합니다. 읽기 전용 tootransparently 연결 된 SQL 응용 프로그램 hello 허용 toohello 보조 데이터베이스 hello를 사용 하 여 부하 분산 규칙을 지정 합니다. 필요에 따라 읽기 전용 hello를 원하는 경우 트래픽 toobe 자동으로 리디렉션하여 toohello 주 서버 hello 보조 서버를 사용할 수 없는 경우 지정할 수 있습니다.
* **자동 장애 조치 정책**: 기본적으로 hello 그룹 장애 조치는 자동 장애 조치 정책으로 구성 됩니다. hello 시스템 hello 오류가 검색 되는 즉시 장애 조치를 트리거합니다. Toocontrol hello hello 응용 프로그램에서 워크플로 장애 조치 하려는 경우 자동 장애 조치를 해제할 수 있습니다. 
* **수동 장애 조치**: hello 자동 장애 조치 구성에 관계 없이 언제 든 수동으로 장애 조치를 시작할 수 있습니다. 자동 장애 조치 정책 구성 된 수동 장애 조치 없는 경우에 hello 그룹 장애 조치에에서 필요한 toorecover 데이터베이스입니다. 강제 장애 조치 또는 친숙한 장애 조치(전체 데이터 동기화 사용)를 시작할 수 있습니다. 후자의 hello 사용된 toorelocate hello 활성 서버 toohello 기본 지역 될 수 있습니다. 장애 조치 완료 되 면 hello DNS 레코드는 자동으로 업데이트 된 tooensure 연결 toohello 올바른 서버입니다.
* **데이터 손실 된 경우 유예 기간이**: 비동기 복제 hello 장애 조치를 사용 하 여 hello 기본 및 보조 데이터베이스를 동기화 하기 때문에 데이터 손실이 발생할 수 있습니다. 응용 프로그램의 허용 오차 toodata 손실 hello 자동 장애 조치 정책 tooreflect를 지정할 수 있습니다. 구성 하 여 **GracePeriodWithDataLossHours**, hello 시스템 데이터가 손실 될 가능성이 tooresult 있는 hello 장애 조치를 시작 하기 전에 대기 하는 시간을 제어할 수 있습니다. 

   > [!NOTE]
   > Hello 그룹의 hello 데이터베이스가 여전히 온라인 상태 인지 시스템을 감지 하는 경우 (예를 들어 hello 중단만 영향을 주지 hello 서비스 제어 평면) hello 값에 관계 없이 전체 데이터 동기화 (친숙 한 장애 조치) hello 장애 조치를 즉시 활성화 설정한 **GracePeriodWithDataLossHours**합니다. 이 동작은 hello 복구 중 데이터가 손실 되지 않습니다 보장 합니다. hello 유예 기간 친숙 한 장애 조치 하는 경우에 적용이 됩니다. Hello 유예 기간이 만료 되기 전에 hello 중단 완화는 hello 장애 조치 활성화 되지 않았습니다.
   >

* **여러 장애 조치 그룹**: hello에 대 한 여러 장애 조치 그룹을 구성할 수 있습니다 된 장애 조치 하는 서버 toocontrol hello 범위의 동일한 쌍입니다. 각 그룹은 독립적으로 장애 조치됩니다. 탄력적 풀을 사용 하 여 다중 테 넌 트 응용 프로그램에는 각 풀의이 기능 toomix 주 데이터베이스와 보조 데이터베이스를 사용할 수 있습니다. 이 방법은 hello 테 넌 트의 절반 중단 tooonly의 hello 영향을 줄일 수 있습니다.

## <a name="best-practices-of-building-highly-available-service"></a>항상 사용 가능한 서비스를 빌드하는 모범 사례

Azure SQL 데이터베이스의 고객 hello를 사용 하는 항상 사용 가능한 서비스 toobuild 다음이 지침을 따라야 합니다.
- **장애 조치(failover) 그룹 사용**: 다른 지역의 두 서버(기본 및 보조 서버) 간에 하나 이상의 장애 조치(failover) 그룹을 만들 수 있습니다. 각 그룹은 일부 또는 모든 주 복제본은 tooan 정전 hello 기본 지역으로 인해 사용할 수 없게 되는 경우 하나의 단위로 복구 하는 하나 또는 여러 데이터베이스를 포함할 수 있습니다. hello 그룹 장애 조치 동일 서비스 목표 기본 hello로 hello로 지역 보조 데이터베이스를 만듭니다. 같은 서비스 수준 목표도 hello로 구성 된 기존 지리적 복제 관계 toohello 장애 조치 그룹 확인 되었는지 hello 지역-보조를 추가 하는 경우 기본 hello 합니다.
- **OLTP 워크 로드에 대 한 읽기 / 쓰기 수신기를 사용 하 여**: OLTP 작업 사용을 수행할 때  **&lt;장애 조치 그룹 이름&gt;. database.windows.net** hello 서버 URL과 hello 연결 될 때 자동으로 지정 된 toohello 주입니다. 이 URL hello 장애 조치 후 변경 되지 않습니다.  
참고 hello 장애 조치 hello hello 클라이언트 연결을 리디렉션된 toohello 새 주 후에 hello 클라이언트 DNS 캐시를 새로 고칠 수 있도록 DNS 레코드를 업데이트 하는 작업이 포함 됩니다.
- **읽기 전용 작업에 대 한 읽기 전용 수신기를 사용 하 여**: hello 응용 프로그램에서 hello 보조 데이터베이스를 논리적으로 격리 된 읽기 전용 작업이 있는 데이터의 허용 toocertain 부실을 설정한 경우 사용할 수 있습니다. 읽기 전용 세션 사용에 대 한  **&lt;장애 조치 그룹 이름&gt;. secondary.database.windows.net** 내용이 자동으로 지정 된 toohello 보조 되므로 hello 서버 URL과 hello 연결 합니다. 또한 **ApplicationIntent=ReadOnly**를 사용하여 연결 문자열 읽기 의도를 표시하는 것이 좋습니다. 
- **성능 저하를 위해 준비할**: SQL 장애 조치 의사 결정은 hello 나머지 hello 응용 프로그램 또는 사용 하는 다른 서비스와에서는 독립적입니다. hello 응용 프로그램의 한 영역 및 다른 일부 구성 요소와 "mixed" 될 수 있습니다. tooavoid hello 저하 hello DR 영역의 hello 중복 응용 프로그램 배포를 확인 하 고 hello이이 문서의 지침을 따릅니다.  
참고 hello 응용 프로그램 hello DR 지역에 없는 toouse 다른 연결 문자열입니다.  
- **데이터 손실에 대 한 준비**: 가동 중단 감지 되 면 SQL 자동으로 트리거하는 읽기 / 쓰기 failover 한 최상의 데이터 손실 toohello 0은 합니다. 그렇지 않으면 때까지 대기 하 여 지정한 hello 기간 **GracePeriodWithDataLossHours**합니다. **GracePeriodWithDataLossHours**를 지정한 경우 데이터 손실에 대비합니다. 일반적으로 중단 시에 Azure에서는 가용성을 우선으로 합니다. 데이터가 손실 될 수 없는 경우 확인 되었는지 tooset **GracePeriodWithDataLossHours** 24 시간과 같이 tooa 충분히 큰 수입니다. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>주 데이터베이스 업그레이드 또는 다운그레이드
주 데이터베이스 tooa 다양 한 성능 수준을 다운 그레이드 하거나 업그레이드할 수 있습니다 (hello 내에서 동일한 서비스 계층) 모든 보조 데이터베이스가 연결을 끊지 않고 합니다. 업그레이드 하는 경우 hello 보조 데이터베이스를 먼저 업그레이드 하 고 다음 hello 주를 업그레이드 하는 것이 좋습니다. Hello 순서를 반대로 다운 그레이드 하는 경우: 먼저 hello 주를 다운 그레이드 하 고 다음 hello 보조 데이터베이스를 다운 그레이드 합니다. 업그레이드 하거나 hello 데이터베이스 tooa 다양 한 서비스 계층을 다운 그레이드할 때이 권장 사항은 적용 됩니다. 

> [!NOTE]
> Hello 장애 조치 그룹 구성의 일부분으로 보조 데이터베이스를 만든 경우 것은 권장된 toodowngrade hello 보조 데이터베이스가 아닙니다. 이 tooensure 데이터 계층에 충분 한 용량 tooprocess 하면 정기 작업 후 장애 조치 활성화 됩니다. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Hello 중요 한 데이터 손실을 방지
광역 네트워크의 높은 대기 시간이 toohello 인해 연속 복사는 비동기 복제 메커니즘을 사용합니다. 비동기 복제를 수행하면 오류가 발생하는 경우에 일부 데이터 손실은 불가피합니다. 그러나 일부 응용 프로그램은 데이터 손실이 없어야 합니다. tooprotect 이러한 중요 업데이트, 응용 프로그램 개발자 hello를 호출할 수 [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) hello 트랜잭션을 커밋한 직후 시스템 프로시저입니다. 호출 **sp_wait_for_database_copy_sync** hello 마지막으로 커밋된 트랜잭션의 될 때까지 호출 스레드 블록 hello toohello 보조 데이터베이스를 전송 합니다. 그러나 것 대기 하지 않는 전송 hello 트랜잭션 toobe 재생 하 고 보조 hello에서 커밋 되었습니다. **sp_wait_for_database_copy_sync** 범위가 지정 된 tooa 특정 연속 복사 링크입니다. Hello 연결 권한 toohello 주 데이터베이스와 모든 사용자는이 절차를 호출할 수 있습니다.

> [!NOTE]
> **sp_wait_for_database_copy_sync**는 장애 조치 후 데이터 손실을 방지하지만 읽기 액세스를 위한 전체 동기화를 보장하지 않습니다. hello로 인해 지연이 발생 한 **sp_wait_for_database_copy_sync** 프로시저 호출 중요 한 hello 호출의 hello 시 hello 트랜잭션 로그의 hello 크기에 따라 달라 집니다. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>장애 조치(failover) 그룹 및 활성 지역 복제를 프로그래밍 방식으로 관리
설명한 것 처럼, 자동 장애 조치 그룹 (에서-미리 보기) 및 활성 지리적 복제 Azure PowerShell을 사용 하 여 프로그래밍 방식으로 관리할 수 있습니다 및 REST API hello 합니다. 다음 표에서 hello hello 명령 집합을 사용할 수 있는 설명 합니다.

**Azure 리소스 관리자 API 및 역할 기반 보안**: 활성 지리적 복제 hello를 포함 하 여 관리를 위한 Azure 리소스 관리자 Api 집합이 포함 되어 [Azure SQL 데이터베이스 REST API](https://docs.microsoft.com/rest/api/sql/) 및 [Azure PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview)합니다. 이러한 Api는 hello 리소스 그룹을 사용 해야 하 고 역할 기반 보안 (RBAC)를 지원 합니다. Tooimplement 역할을 액세스 하는 방법에 대 한 자세한 내용은 참조 하십시오. [신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-what-is.md)합니다.

> [!NOTE]
> 활성 지역 복제의 여러 새로운 기능은 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 기반 [Azure SQL REST API](https://msdn.microsoft.com/library/azure/mt163571.aspx) 및 [Azure SQL Database PowerShell cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx)에서만 지원됩니다. hello [(클래식) REST API](https://msdn.microsoft.com/library/azure/dn505719.aspx) 및 [(클래식) Azure SQL 데이터베이스 cmdlet](https://msdn.microsoft.com/library/azure/dn546723.aspx) Azure 리소스 관리자 기반 Api를 사용 하는 것이 좋습니다 hello를 사용 하 여 이전 버전과 호환성을 위해 지원 됩니다. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>SQL 데이터베이스 장애 조치를 사용 하 여 TRANSACT-SQL을 사용 하 여 관리

| 명령 | 설명 |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |기존 데이터베이스에 대 한 보조 서버에 추가 인수 toocreate 보조 데이터베이스를 사용 하 고 데이터 복제 시작 |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |장애 조치 나 FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch 보조 데이터베이스 toobe 기본 tooinitiate 장애 조치를 사용 하 여 |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |보조 ON 서버 제거 tooterminate SQL 데이터베이스와 보조 데이터베이스를 지정된 하는 hello 간의 데이터 복제를 사용 합니다. |
| [sys.geo_replication_links(Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx) |Hello Azure SQL 데이터베이스 논리 서버에 각 데이터베이스에 대 한 모든 기존 복제 링크에 대 한 정보를 반환합니다. |
| [sys.dm_geo_replication_link_status(Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) |가져옵니다 마지막 복제 시간, 마지막 복제 지연 시간 및 지정된 된 SQL 데이터베이스에 대 한 hello 복제 링크에 대 한 기타 정보 hello 합니다. |
| [sys.dm_operation_status(Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx) |Hello 복제 링크의 hello 상태를 비롯 한 모든 데이터베이스 작업에 대 한 hello 상태가 표시 됩니다. |
| [sp_wait_for_database_copy_sync(Azure SQL Database)](https://msdn.microsoft.com/library/dn467644.aspx) |커밋된 모든 트랜잭션이 복제 되 고 hello 활성 보조 데이터베이스에서 승인할 때까지 응용 프로그램 toowait hello 하면 됩니다. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>SQL 데이터베이스 장애 조치를 사용 하 여 PowerShell을 사용 하 여 관리

| Cmdlet | 설명 |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |하나 이상의 데이터베이스를 가져옵니다. |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |기존 데이터베이스에 대한 보조 데이터베이스를 만들고 데이터 복제를 시작합니다. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |보조 데이터베이스 toobe 기본 tooinitiate 장애 조치를 전환합니다. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |SQL 데이터베이스와 보조 데이터베이스를 지정된 하는 hello 간의 데이터 복제를 종료합니다. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Azure SQL 데이터베이스와 리소스 그룹 또는 SQL Server 간의 hello 지역 간 복제 링크를 가져옵니다. |
| [New-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   장애 조치 그룹을 만들고 주 및 보조 서버 모두에 등록합니다|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Hello 서버에서 그룹을 장애 조치 hello를 제거 하 고 모든 보조 데이터베이스가 포함 된 hello 그룹 삭제 |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | 검색 hello 장애 조치 그룹 구성 |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Hello 그룹 장애 조치의 hello 구성을 수정합니다 |
| [Switch-AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | 트리거 hello 장애 조치 그룹 toohello 보조 서버로 장애 조치 |
|  | |

> [!IMPORTANT]
> 샘플 스크립트에 대해서는 [활성 지역 복제를 사용하여 단일 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [활성 지역 복제를 사용하여 풀된 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md) 및 [단일 데이터베이스에 대한 장애 조치(failover) 그룹 구성 및 장애 조치(failover)(미리 보기)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)를 참조하세요.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>SQL 데이터베이스 장애 조치 hello REST API를 사용 하 여 관리
| API | 설명 |
| --- | --- |
| [데이터베이스 생성 또는 업데이트(createMode=Restore)](/rest/api/sql/Databases/CreateOrUpdate) |주 보조 데이터베이스 또는 보조 데이터베이스를 만들거나, 업데이트하거나, 복원합니다. |
| [데이터베이스 만들기 또는 업데이트 상태 가져오기](/rest/api/sql/Databases/CreateOrUpdate) |만들기 작업 하는 동안 hello 상태를 반환 합니다. |
| [보조 데이터베이스를 주 데이터베이스로 설정(계획된 장애 조치(failover))](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Hello 현재 주 복제본 데이터베이스에서 장애 조치 하 여 기본 있는 복제본 데이터베이스를 설정 합니다. |
| [보조 데이터베이스를 주 데이터베이스로 설정(계획되지 않은 장애 조치(failover))](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Hello 현재 주 복제본 데이터베이스에서 장애 조치 하 여 기본 있는 복제본 데이터베이스를 설정 합니다. 이 작업으로 인해 데이터가 손실될 수 있습니다. |
| [복제 링크 가져오기](/rest/api/sql/replicationlinks/get) |지역에서 복제 파트너 관계의 지정된 SQL 데이터베이스에 대한 특정 복제 링크를 가져옵니다. Hello sys.geo_replication_links 카탈로그 뷰에 표시 hello 정보를 검색합니다. |
| [복제 링크 - 데이터베이스 기준 목록](/rest/api/sql/replicationlinks/listbydatabase) | 지역에서 복제 파트너 관계의 지정된 SQL 데이터베이스에 대한 모든 복제 링크를 가져옵니다. Hello sys.geo_replication_links 카탈로그 뷰에 표시 hello 정보를 검색합니다. |
| [복제 링크 삭제](/rest/api/sql/databases/delete) | 데이터베이스 복제 링크를 삭제합니다. 장애 조치(failover) 중에 수행할 수 없습니다. |
| [장애 조치(failover) 그룹 만들기 또는 업데이트]/rest/api/sql/failovergroups/createorupdate) | 장애 조치(failover) 그룹을 만들거나 업데이트합니다. |
| [장애 조치(failover) 그룹 삭제](/rest/api/sql/failovergroups/delete) | Hello 서버에서 그룹을 장애 조치 hello를 제거합니다. |
| [장애 조치(failover)(계획됨)](/rest/api/sql/failovergroups/failover) | 현재 주 서버 toothis 서버 hello에서에서 장애 조치 합니다. |
| [장애 조치(failover)로 인한 데이터 손실 허용](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |현재 주 서버 toothis 서버 hello 통해 ails 합니다. 이 작업으로 인해 데이터가 손실될 수 있습니다. |
| [장애 조치 그룹 가져오기](/rest/api/sql/failovergroups/get) | 장애 조치(failover) 그룹을 가져옵니다. |
| [서버별 장애 조치(failover) 그룹 나열](/rest/api/sql/failovergroups/listbyserver) | 서버에서 hello 장애 조치 그룹을 나열 합니다. |
| [장애 조치(failover) 그룹 업데이트](/rest/api/sql/failovergroups/update) | 장애 조치(failover) 그룹을 업데이트합니다. |
|  | |

## <a name="next-steps"></a>다음 단계
* 샘플 스크립트에 대해서는 다음을 참조하세요.
   - [활성 지역 복제를 사용하여 단일 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [활성 지역 복제를 사용하여 풀된 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [단일 데이터베이스에 대한 장애 조치(failover) 그룹 구성 및 장애 조치(failover)(미리 보기)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)
* Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [SQL 데이터베이스 자동화 된 백업을](sql-database-automated-backups.md)합니다.
* 복구를 위한 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [hello 서비스 개시 백업에서 데이터베이스를 복원](sql-database-recovery-using-backups.md)합니다.
* 새 주 서버 및 데이터베이스에 대 한 인증 요구 사항에 대 한 toolearn 참조 [재해 복구 후 SQL 데이터베이스 보안](sql-database-geo-replication-security-config.md)합니다.

