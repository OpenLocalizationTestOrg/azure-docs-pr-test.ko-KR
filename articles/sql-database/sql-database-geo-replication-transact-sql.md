---
title: "Transact-SQL로 Azure SQL Database에 대한 지역에서 복제 구성 | Microsoft Docs"
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
ms.openlocfilehash: e5011c1c67e051616d53621b72e46ba894ca3c02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>TRANSACT-SQL로 Azure SQL Database에 대한 활성 지역 복제 구성

이 문서에서는 Transact-SQL을 사용하여 Azure SQL Database에 대한 활성 지역 복제를 구성하는 방법을 보여 줍니다.

Transact-SQL을 사용하여 장애 조치(Failover)를 시작하려면 [Transact-SQL로 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치(Failover) 시작](sql-database-geo-replication-failover-transact-sql.md)을 참조하세요.

> [!NOTE]
> 재해 복구를 위해 활성 지역 복제(읽을 수 있는 보조)를 사용하는 경우 자동 및 투명한 장애 조치를 수행할 수 있도록 응용 프로그램 내의 모든 데이터베이스에 대해 장애 조치 그룹을 구성해야 합니다. 이 기능은 미리 보기로 제공됩니다. 자세한 내용은 [자동 장애 조치 그룹 및 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.
> 
> 

Transact-SQL을 사용하여 활성 지역 복제를 구성하려면 다음이 필요합니다.

* Azure 구독
* 논리 Azure SQL Database 서버 <MyLocalServer> 및 SQL 데이터베이스 <MyDB> - 복제하려는 주 데이터베이스입니다.
* 하나 이상의 논리 Azure SQL Database 서버 <MySecondaryServer(n)> - 보조 데이터베이스를 만드는 파트너 서버가 될 논리 서버입니다.
* 주 서버에서 DBManager로 로그인
* 지역에서 복제할 로컬 데이터베이스의 db_ownership 보유
* 지역에서 복제를 구성하는 파트너 서버의 DBManager
* 최신 버전의 SSMS(SQL Server Management Studio)를 설치합니다.

> [!IMPORTANT]
> Microsoft Azure 및 SQL 데이터베이스에 대한 업데이트와 동기화 상태를 유지하려면 항상 최신 버전의 Management Studio를 사용하는 것이 좋습니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>보조 데이터베이스 추가
**ALTER DATABASE** 문을 사용하여 파트너 서버에서 지역에서 복제된 보조 데이터베이스를 만들 수 있습니다. 복제할 데이터베이스를 포함하는 서버의 마스터 데이터베이스에서 이 문을 실행합니다. 지역에서 복제된 데이터베이스("주 데이터베이스")는 복제되는 데이터베이스와 동일한 이름을 가지며 기본적으로 주 데이터베이스와 동일한 서비스 수준을 가집니다. 보조 데이터베이스는 읽을 수 있거나 읽을 수 없을 수 있으며 단일 데이터베이스 또는 탄력적 풀에 있을 수 있습니다. 자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.
보조 데이터베이스가 만들어지고 시드된 후 데이터는 주 데이터베이스에서 비동기적으로 복제를 시작합니다. 다음 단계에서는 Management Studio를 사용하여 지역에서 복제를 구성하는 방법을 설명합니다. 단일 데이터베이스 또는 탄력적 풀로 읽을 수 없는 및 읽을 수 있는 보조를 만드는 단계가 제공됩니다.

> [!NOTE]
> 데이터베이스가 주 데이터베이스와 같은 이름으로 지정된 파트너 서버에 있는 경우 명령이 실패합니다.
> 

### <a name="add-readable-secondary-single-database"></a>읽을 수 있는 보조(단일 데이터베이스) 추가
단일 데이터베이스로 읽을 수 있는 보조를 만들려면 다음 단계를 사용합니다.

1. Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.
2. 데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.
3. 다음 **ALTER DATABASE** 문을 사용하여 로컬 데이터베이스를 지역에서 복제 주 데이터베이스(보조 서버의 읽을 수 있는 보조 데이터베이스와 함께)로 만듭니다.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. **실행** 을 클릭하여 쿼리를 실행합니다.

### <a name="add-readable-secondary-elastic-pool"></a>읽을 수 있는 보조(탄력적 풀) 추가
탄력적 풀에서 읽을 수 있는 보조를 만들려면 다음 단계를 사용합니다.

1. Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.
2. 데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.
3. 다음 **ALTER DATABASE** 문을 사용하여 로컬 데이터베이스를 지역에서 복제 주 데이터베이스(탄력적 풀에 포함된 보조 서버의 읽을 수 있는 보조 데이터베이스와 함께)로 만듭니다.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. **실행** 을 클릭하여 쿼리를 실행합니다.

## <a name="remove-secondary-database"></a>보조 데이터베이스 제거
**ALTER DATABASE** 문을 사용하여 보조 데이터베이스와 주 데이터베이스 간의 복제 파트너 관계를 영구적으로 종료합니다. 이 문은 주 데이터베이스가 상주하는 마스터 데이터베이스에서 실행됩니다. 관계가 종료된 후 보조 데이터베이스는 일반 읽기-쓰기 데이터베이스가 됩니다. 보조 데이터베이스에 대한 연결이 끊어진 경우 명령이 성공하지만 연결이 복원된 후 보조는 읽기-쓰기가 됩니다. 자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.

지역에서 복제 파트너 관계에서 지역에서 복제된 보조 데이터베이스를 제거하려면 다음 단계를 사용합니다.

1. Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.
2. 데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.
3. 다음 **ALTER DATABASE** 문을 사용하여 지역에서 복제된 보조 데이터베이스를 제거합니다.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. **실행** 을 클릭하여 쿼리를 실행합니다.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>활성 지역 복제 구성 및 상태 모니터링

모니터링 작업에는 지역에서 복제 구성의 모니터링 및 데이터 복제 상태 모니터링이 포함됩니다.  마스터 데이터베이스의 **sys.dm_geo_replication_links** 동적 관리 뷰를 사용하여 Azure SQL Database 논리 서버의 각 데이터베이스에 대한 모든 기존 복제 링크에 대한 정보를 반환할 수 있습니다. 이 뷰는 주 및 보조 데이터베이스 간의 각 복제 링크에 대한 행을 포함합니다. **sys.dm_replication_status** 동적 관리 뷰를 사용하여 현재 복제 링크에 참여하는 각 Azure SQL Database에 대한 행을 반환할 수 있습니다. 주 및 보조 데이터베이스가 포함됩니다. 지정된 주 데이터베이스에 두 개 이상의 연속 복제 링크가 있는 경우 이 테이블은 각 관계에 대한 행을 포함합니다. 논리 마스터를 포함한 모든 데이터베이스에 뷰가 생성됩니다. 그러나 논리 마스터에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다. **sys.dm_operation_status** 동적 관리 뷰를 사용하여 복제 링크의 상태를 포함하는 모든 데이터베이스 작업에 대한 상태를 표시할 수 있습니다. 자세한 내용은 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 및 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)를 참조하세요.

활성 지역 복제 파트너 관계를 모니터링하려면 다음 단계를 사용합니다.

1. Management Studio에서 Azure SQL 데이터베이스 논리 서버에 연결합니다.
2. 데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **master**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.
3. 지역에서 복제 링크와 함께 모든 데이터베이스를 표시하려면 다음 문을 사용합니다.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. **실행** 을 클릭하여 쿼리를 실행합니다.
5. 데이터베이스 폴더를 열고 **시스템 데이터베이스** 폴더를 확장한 후 **MyDB**를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.
6. 다음 문을 사용하여 복제 지연 및 MyDB의 보조 데이터베이스의 마지막 복제 시간을 표시합니다.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. **실행** 을 클릭하여 쿼리를 실행합니다.
8. 다음 문을 사용하여 데이터베이스 MyDB와 연결되는 가장 최근의 지역에서 복제 작업을 표시합니다.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. **실행** 을 클릭하여 쿼리를 실행합니다.

## <a name="next-steps"></a>다음 단계
* 장애 조치 그룹과 활성 지역 복제에 대한 자세한 내용은 [장애 조치 그룹](sql-database-geo-replication-overview.md)을 참조하세요.
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)

