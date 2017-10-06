---
title: "Transact SQL와 Azure SQL 데이터베이스의 지역 간 복제 aaaConfigure | Microsoft Docs"
description: "Transact-SQL을 사용하여 Azure SQL Database에 대한 지역에서 복제 구성"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>TRANSACT-SQL로 Azure SQL Database에 대한 활성 지역 복제 구성

이 문서에서는 어떻게 tooconfigure 활성 지리적 복제는 Azure SQL 데이터베이스 TRANSACT-SQL에 대 한 합니다.

TRANSACT-SQL을 사용 하 여 tooinitiate 장애 조치 참조 [TRANSACT-SQL와 Azure SQL 데이터베이스에 대 한 계획 되거나 계획 되지 않은 장애 조치의 시작](sql-database-geo-replication-failover-transact-sql.md)합니다.

> [!NOTE]
> 재해 복구용 활성 지리적 복제 (읽기 가능한 보조 복제본)를 사용 하는 경우 응용 프로그램 tooenable 자동 및 투명 장애 내의 모든 데이터베이스에 대 한 장애 조치 그룹을 구성 해야 합니다. 이 기능은 미리 보기 상태입니다. 자세한 내용은 [자동 장애 조치 그룹 및 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.
> 
> 

tooconfigure 활성 지리적 복제 hello 다음 필요한 TRANSACT-SQL을 사용 하 여:

* Azure 구독
* Azure SQL 데이터베이스 논리 서버 <MyLocalServer> 및 SQL 데이터베이스 <MyDB> -tooreplicate 원하는 hello 주 데이터베이스
* 하나 이상의 논리 Azure SQL 데이터베이스 서버 < MySecondaryServer(n)-> 보조 데이터베이스에서는 hello 파트너 서버 될 hello 논리 서버
* 기본 hello DBManager 켜져 있는 로그인
* 지역 간 복제 한다는 hello 로컬 데이터베이스의 db_ownership이 있어야 합니다.
* Hello 파트너 서버 toowhich DBManager 켜야 지리적 복제를 구성 합니다.
* hello 최신 버전 SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> 항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>보조 데이터베이스 추가
Hello를 사용할 수 있습니다 **ALTER DATABASE** 문 toocreate 파트너 서버에서 보조 데이터베이스 지리적으로 복제 합니다. Hello 서버 포함 hello 데이터베이스 toobe 복제의 hello master 데이터베이스에서이 문을 실행 합니다. hello 지리적으로 복제 된 데이터베이스 (hello "기본 데이터베이스")에 적용 됩니다 hello 데이터베이스 복제 되 고 기본적으로이 hello로 이름과 같은 이름을 hello hello 주 데이터베이스와 같은 서비스 수준입니다. hello 보조 데이터베이스 읽기 가능 인지 또는 읽을 수 없는 수와 단일 데이터베이스가 될 수 있습니다 또는 탄력적인 풀에 있습니다. 자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.
Hello 보조 데이터베이스를 만들고 시드 된 후 데이터 hello 주 데이터베이스에서 비동기적으로 복제를 시작 합니다. 다음 hello 단계에서는 어떻게 tooconfigure 지리적 복제 Management Studio를 사용 하 여 합니다. 단계 toocreate 읽을 수 없는 및 읽기 가능한 보조 복제본을 단일 데이터베이스 또는 탄력적 풀에서 제공 됩니다.

> [!NOTE]
> 데이터베이스가 기본 hello 이름이 hello로 지정 된 파트너 서버 hello에 있는 데이터베이스 hello 명령이 실패 합니다.
> 

### <a name="add-readable-secondary-single-database"></a>읽을 수 있는 보조(단일 데이터베이스) 추가
다음 단계를 단일 데이터베이스로 읽기 가능한 보조 toocreate hello를 사용 합니다.

1. Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. Hello 다음을 사용 하 여 **ALTER DATABASE** 문 toomake 보조 서버에서 읽기 가능한 보조 데이터베이스와 지역 복제 주에 로컬 데이터베이스입니다.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. 클릭 **Execute** toorun hello 쿼리 합니다.

### <a name="add-readable-secondary-elastic-pool"></a>읽을 수 있는 보조(탄력적 풀) 추가
다음 단계 toocreate 탄력적 풀의 읽기 가능한 보조 hello를 사용 합니다.

1. Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. Hello 다음을 사용 하 여 **ALTER DATABASE** 문 toomake 탄력적 풀의 보조 서버에서 읽기 가능한 보조 데이터베이스와 지역 복제 주에 로컬 데이터베이스입니다.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. 클릭 **Execute** toorun hello 쿼리 합니다.

## <a name="remove-secondary-database"></a>보조 데이터베이스 제거
Hello를 사용할 수 있습니다 **ALTER DATABASE** 문을 toopermanently 보조 데이터베이스와 주 도메인 컨트롤러 간의 hello 복제 파트너 관계를 종료 합니다. 이 문은 주 데이터베이스가 있는 어떤 hello에 hello master 데이터베이스에서 실행 됩니다. Hello 관계 종료 후 hello 보조 데이터베이스 일반 읽기 / 쓰기 데이터베이스가 됩니다. Hello 연결 toosecondary 데이터베이스 중단 된 hello 명령이 성공 수 있지만 연결이 복원 된 후 보조 hello 읽기 / 쓰기 수입니다. 자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.

지리적 복제 파트너 관계에서 단계 tooremove 지리적 복제 보조를 다음 hello를 사용 합니다.

1. Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. Hello 다음을 사용 하 여 **ALTER DATABASE** 문 tooremove 지리적 복제 보조 합니다.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. 클릭 **Execute** toorun hello 쿼리 합니다.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>활성 지역 복제 구성 및 상태 모니터링

모니터링 작업 hello 지리적 복제 구성의 모니터링 및 데이터 복제 상태 모니터링에 포함 됩니다.  Hello를 사용할 수 있습니다 **sys.dm_geo_replication_links** hello Azure SQL 데이터베이스 논리 서버에 hello master 데이터베이스 tooreturn 정보 각 데이터베이스에 대 한 모든 기존 복제 링크에 대 한 동적 관리 뷰. 이 보기는 각 주 데이터베이스와 보조 데이터베이스 간의 복제 링크 hello에 대 한 한 행을 포함 합니다. Hello를 사용할 수 있습니다 **sys.dm_replication_link_status** 동적 관리 뷰를 tooreturn 행 복제 복제 링크에 현재 참여 하는 각 Azure SQL 데이터베이스에 대 한 합니다. 주 및 보조 데이터베이스가 포함됩니다. 지정된 된 주 데이터베이스에 대 한 연속 복제 링크를 두 개 이상 있는 경우이 테이블 각 hello 관계의 한 행을 포함 합니다. hello 뷰가 hello 논리 master를 포함 하는 모든 데이터베이스에서 생성 됩니다. 그러나 hello 논리 master에서이 뷰를 쿼리하면 빈 집합이 반환 됩니다. Hello를 사용할 수 있습니다 **sys.dm_operation_status** hello 복제 링크의 hello 상태를 포함 하 여 작업 한 모든 데이터베이스에 대 한 동적 관리 tooshow hello 상태를 확인 합니다. 자세한 내용은 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 및 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)를 참조하세요.

다음 단계 toomonitor 활성 지리적 복제 파트너 관계 hello를 사용 합니다.

1. Management Studio에서 tooyour Azure SQL 데이터베이스 논리 서버를 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. 지리적 복제 링크가 있는 hello 문을 tooshow 다음 모든 데이터베이스를 사용 합니다.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. 클릭 **Execute** toorun hello 쿼리 합니다.
5. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **MyDB**, 클릭 하 고 **새 쿼리**합니다.
6. 다음 문은 tooshow hello 복제 사용 하 여 hello 만큼 이전 성과 MyDB의 보조 데이터베이스의 복제 시간.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. 클릭 **Execute** toorun hello 쿼리 합니다.
8. 문을 tooshow hello 가장 최근의 지리적 복제 작업 MyDB 데이터베이스와 관련 된 다음 hello를 사용 합니다.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. 클릭 **Execute** toorun hello 쿼리 합니다.

## <a name="next-steps"></a>다음 단계
* 장애 조치 그룹 및 활성 지리적 복제에 대해 자세히 toolearn 참조- [장애 조치 그룹](sql-database-geo-replication-overview.md)
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)

