---
title: "TSQL:Azure SQL Database에 대한 장애 조치(failover) 시작 | Microsoft Docs"
description: "Transact-SQL을 사용하여 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치 시작"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Transact-SQL로 Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치 시작

이 문서에서는 어떻게 tooinitiate 장애 조치 tooa TRANSACT-SQL을 사용 하 여 보조 SQL 데이터베이스입니다. tooconfigure 지리적 복제 참조 [Azure SQL 데이터베이스에 대 한 지리적 복제 구성](sql-database-geo-replication-transact-sql.md)합니다.

tooinitiate 장애 조치 hello 다음이 필요합니다.

* 기본 hello DBManager 켜져 있는 로그인
* 지역 간 복제 한다는 hello 로컬 데이터베이스의 db_ownership이 있어야 합니다.
* Hello 파트너 서버 toowhich DBManager 켜야 지리적 복제를 구성 합니다.
* 최신 버전의 SSMS(SQL Server Management Studio)

> [!IMPORTANT]
> 항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>보조 데이터베이스 toobecome hello 새 주 승격 계획된 된 장애 조치를 시작 합니다.
Hello를 사용할 수 있습니다 **ALTER DATABASE** 보조 hello 기존 기본 toobecome 수준 내리기 계획 된 방식으로 문을 toopromote는 보조 데이터베이스 toobecome hello 새로운 주 데이터베이스입니다. 이 문은 hello 승격 되는 지리적 복제 보조 데이터베이스가 있는 어떤 hello에 hello Azure SQL 데이터베이스 논리 서버 master 데이터베이스에서 실행 됩니다. 이 기능은 hello DR 드릴 하는 동안와 같은 계획 된 장애 조치에 대 한 설계 및 해당 hello 주 데이터베이스에서 사용할 수 있어야 합니다.

hello 명령은 hello 다음 워크플로 수행 합니다.

1. 모든 보류 중인 트랜잭션이 toobe 일으키는 스위치 복제 toosynchronous 모드의 toohello 보조 복제본 및 모든 새 트랜잭션을; 차단 플러시 일시적으로
2. 스위치 hello hello hello 지리적 복제 파트너 관계에서 두 데이터베이스의 역할입니다.  

이 시퀀스는 hello hello 역할 전환 하 고 데이터 손실 없이 므 전에 두 데이터베이스의 동기화를 보장 합니다. 두 데이터베이스 모두에서 사용할 수 없는 (0 too25 초의 hello 순서) hello 역할이 전환 된 하는 동안 짧은 간격이 있습니다. Hello 주 데이터베이스에 여러 보조 데이터베이스, hello 명령 하는 경우는 자동으로 재구성 hello 다른 보조 복제본 tooconnect toohello 새로운 주입니다.  hello 전체 작업에는 일반적인 환경에서 분 toocomplete 보다 작은 수행 해야 합니다. 자세한 내용은 [ALTER DATABASE(Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 및 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.

단계 tooinitiate 계획된 된 장애 조치를 수행 하는 hello를 사용 합니다.

1. Management Studio에서 toohello Azure SQL 데이터베이스 논리 서버는 지리적 복제 보조 데이터베이스가 있는 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. Hello 다음을 사용 하 여 **ALTER DATABASE** 문 tooswitch hello 보조 데이터베이스 toohello 주 역할입니다.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. 클릭 **Execute** toorun hello 쿼리 합니다.

> [!NOTE]
> 드문 경우 이지만 있기 hello 작업을 완료할 수 없습니다 및 걸린 나타날 수 있습니다. 이 경우 hello 사용자 hello 강제 장애 조치 명령을 실행 하 고 데이터 손실 허용 수 있습니다.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>보조 데이터베이스를 toohello hello 주 데이터베이스에서 계획 되지 않은 장애 조치의 시작
Hello를 사용할 수 있습니다 **ALTER DATABASE** 문을 toopromote는 보조 데이터베이스 toobecome hello 새로운 주 데이터베이스에 기존 기본 toobecome hello hello 강등 강제 된 계획 되지 않은 방식으로 보조 한 번에 hello 때 주 데이터베이스를 더 이상 사용할 수 없습니다. 이 문은 hello 승격 되는 지리적 복제 보조 데이터베이스가 있는 어떤 hello에 hello Azure SQL 데이터베이스 논리 서버 master 데이터베이스에서 실행 됩니다.

복원 중인 데이터베이스의 가용성을 hello 중요 하며 일부 데이터 손실이 허용 되는 경우이 기능은 재해 복구를 위해 설계 되었습니다. 강제 장애 조치를 호출 하면 보조 데이터베이스 즉시 hello 주 데이터베이스가 되 고 승인을 쓰기 트랜잭션 시작 hello 지정. Hello 원래 주 데이터베이스는이 새 주 데이터베이스와 수 tooreconnect를 즉시 증분 백업을 hello 원래 주 데이터베이스에서 라인 상태가 되며 hello 이전 주 데이터베이스 hello 새로운 주 데이터베이스;에 대 한 보조 데이터베이스에 만들어집니다. 그 다음은 단순히 hello 새 주 데이터베이스의 동기화 복제 합니다.

그러나 지정 시간 복원 지원 되지 않으므로 hello 보조 데이터베이스에서 커밋된 toorecover 데이터 하지 않고자 한다면 hello 사용자 경우 toohello 이전 주 데이터베이스 되지 않은 복제 toohello 새로운 주 데이터베이스 hello 강제 장애 조치 발생 하기 전에 hello 사용자가 필요로 tooengage 지원 toorecover이 데이터가 손실 됩니다.

Hello 주 데이터베이스에 여러 보조 데이터베이스, hello 명령 하는 경우는 자동으로 재구성 hello 다른 보조 복제본 tooconnect toohello 새로운 주입니다.

다음 단계 tooinitiate 예기치 않은 장애 조치가 hello를 사용 합니다.

1. Management Studio에서 toohello Azure SQL 데이터베이스 논리 서버는 지리적 복제 보조 데이터베이스가 있는 연결 합니다.
2. Hello 데이터베이스 폴더를 열고, hello 확장 **시스템 데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭 **마스터**, 클릭 하 고 **새 쿼리**합니다.
3. Hello 다음을 사용 하 여 **ALTER DATABASE** 문 tooswitch hello 보조 데이터베이스 toohello 주 역할입니다.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. 클릭 **Execute** toorun hello 쿼리 합니다.

> [!NOTE]
> 주 데이터베이스와 보조 데이터베이스 모두 온라인 상태일 때 hello 명령이 실행 될 경우 hello 이전 기본 되도록 새 보조 데이터베이스 데이터 동기화 하지 않아도 즉시 hello 합니다. 기본 hello는 커밋 트랜잭션을 hello 명령이 일부 데이터가 손실 될 때 발생할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* 장애 조치 후 서버 및 데이터베이스에 대 한 hello 인증 요구 사항을 hello 새 주 데이터베이스에 구성 되어를 확인 합니다. 자세한 내용은 [재해 복구 후의 SQL Database 보안](sql-database-geo-replication-security-config.md)을 참조하세요.
* 활성 지리적 복제를 사전 복구 및 복구 후 단계를 포함 하 고 재해 복구 훈련과 수행을 사용 하 여 재해 후 복구 toolearn 참조 [재해 복구](sql-database-disaster-recovery.md)
* 활성 지역 복제에 대한 Sasha Nosov의 블로그 게시물은 [새로운 지역에서 복제 기능에 대한 주요 내용](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)을 참조하세요.
* 클라우드 응용 프로그램 toouse 활성 지리적 복제를 디자인 하는 방법에 대 한 정보를 참조 하십시오. [지리적 복제를 사용 하 여 비즈니스 연속성을 위한 클라우드 응용 프로그램 디자인](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* 탄력적 풀의 활성 지역 복제 사용에 대한 자세한 내용은 [탄력적 풀 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)을 참조하세요.
* 무중단 업무 방식에 대한 개략적 정보는 [무중단 업무 방식 개요](sql-database-business-continuity.md)를 참조하세요.

