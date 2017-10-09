---
title: "Azure Portal: SQL Database 지역에서 복제 | Microsoft Docs"
description: "Azure SQL 데이터베이스에 대 한 지리적 복제를 hello Azure 포털 및 시작 장애 조치 구성"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Azure SQL 데이터베이스에 대 한 활성 지리적 복제를 hello Azure 포털 및 시작 장애 조치 구성

이 문서에서는 어떻게 tooconfigure 활성 지리적 복제 SQL 데이터베이스에 대 한 hello에 [Azure 포털](http://portal.azure.com) 및 tooinitiate 장애 조치 합니다.

Azure 포털 hello로 장애 조치 tooinitiate 참조 [hello Azure 포털으로 Azure SQL 데이터베이스에 대 한 계획 되거나 계획 되지 않은 장애 조치의 시작](sql-database-geo-replication-portal.md)합니다.

tooconfigure 활성 지리적 복제 hello Azure 포털을 사용 하 여 리소스를 수행 하는 hello가 필요 합니다.

* Azure SQL 데이터베이스: tooreplicate tooa 서로 다른 지리적 위치 영역을 사용 하지 않겠다고 hello 주 데이터베이스입니다.

> [!Note]
활성 지리적 복제 데이터베이스 hello에 사이 여야 합니다. 동일한 구독 합니다.

## <a name="add-a-secondary-database"></a>보조 데이터베이스 추가
hello 다음 단계를 만듭니다 새로운 보조 데이터베이스는 지리적 복제 파트너 관계에 있습니다.  

보조 데이터베이스 tooadd hello 구독 소유자 또는 공동 소유자 여야 합니다.

hello 보조 데이터베이스 hello hello 주 데이터베이스로 이름과 같은 이름을 가지 며 hello 기본적으로, 동일한 서비스 수준 hello 보조 데이터베이스는 단일 데이터베이스나 탄력적 풀의 데이터베이스 수 있습니다. 자세한 내용은 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.
보조 hello를 만들고 시드 된 후 데이터 hello 주 데이터베이스 toohello 새 보조 데이터베이스에서 복제를 시작 합니다.

> [!NOTE]
> (예를 들어 이전 지리적 복제 관계를 종료) 결과로 hello 파트너 데이터베이스가 이미 있는 경우 hello 명령이 실패 합니다.
> 

1. Hello에 [Azure 포털](http://portal.azure.com), tooset 지리적 복제에 대해 원하는 toohello 데이터베이스를 검색 합니다.
2. Hello SQL 데이터베이스 페이지에서 선택 **지리적 복제**, 한 다음 hello 지역 toocreate hello 보조 데이터베이스를 선택 합니다. Hello 주 데이터베이스를 호스트 하는 hello 지역 이외의 다른 모든 영역을 선택할 수 있지만 hello 권장 [쌍을 이루는 지역](../best-practices-availability-paired-regions.md)합니다.
   
    ![지역에서 복제 구성](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. 선택 하거나 hello 서버와 보조 데이터베이스 hello에 대 한 가격 책정 계층을 구성 합니다.
   
    ![보조 구성](./media/sql-database-geo-replication-portal/create-secondary.png)
4. 필요에 따라 보조 데이터베이스 tooan 탄력적 풀을 추가할 수 있습니다. 풀에서 toocreate hello 보조 데이터베이스를 클릭 **탄력적 풀** hello 대상 서버에서 풀을 선택 합니다. 풀은 hello 대상 서버에 이미 있어야 합니다. 이 워크플로는 풀을 만들지 않습니다.
5. 클릭 **만들기** tooadd hello 보조 합니다.
6. hello 보조 데이터베이스가 만들어지고 hello 시드 프로세스를 시작 합니다.
   
    ![보조 구성](./media/sql-database-geo-replication-portal/seeding0.png)
7. 프로세스를 시드 hello 완료 되 면 hello 보조 데이터베이스의 상태를 표시 합니다.
   
    ![시드 완료](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>장애 조치(Failover) 시작

hello 보조 데이터베이스는 주 바뀌면된 toobecome hello 수 있습니다.  

1. Hello에 [Azure 포털](http://portal.azure.com), toohello hello 지리적 복제 파트너 관계의 주 데이터베이스를 검색 합니다.
2. Hello SQL 데이터베이스 블레이드에서 선택 **모든 설정을** > **지리적 복제**합니다.
3. Hello에 **보조** 목록, 선택 hello 데이터베이스 toobecome 원하는 클릭 하 고 새로운 주 hello **장애 조치**합니다.
   
    ![장애 조치](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. 클릭 **예** toobegin hello 장애 조치 합니다.

즉시 hello 명령 hello 주 역할로 hello 보조 데이터베이스를 전환합니다. 

두 데이터베이스 모두에서 사용할 수 없는 (0 too25 초의 hello 순서) hello 역할이 전환 된 하는 동안 짧은 간격이 있습니다. Hello 주 데이터베이스에 자동으로 부여 된 여러 보조 데이터베이스, hello 명령 하는 경우 다시 구성 합니다. 다른 보조 복제본 tooconnect toohello 새로운 주를 hello 합니다. hello 전체 작업에는 일반적인 환경에서 분 toocomplete 보다 작은 수행 해야 합니다. 

> [!NOTE]
> 이 명령은 중단 시 hello 데이터베이스의 빠른 복구를 위해 설계 되었습니다. 데이터 동기화 없이 장애 조치(Failover)를 트리거합니다(강제 장애 조치).  경우 hello 기본 온라인 상태이 고 hello 명령이 일부 데이터가 손실 될 때 트랜잭션을 커밋하기 발생할 수 있습니다. 
> 
> 

## <a name="remove-secondary-database"></a>보조 데이터베이스 제거
이 작업에는 영구적으로 hello 복제 toohello 보조 데이터베이스를 종료 하 고 변경 내용을 hello hello 보조 tooa 일반 읽기 / 쓰기 데이터베이스의 역할을 합니다. 보조 데이터베이스를 toohello hello 연결 중단 된 경우 hello 명령은 성공 하지만 연결이 복원 된 후에 읽기 / 쓰기 보조있지 않습니다 하 게 될 때까지 hello 합니다.  

1. Hello에 [Azure 포털](http://portal.azure.com), toohello hello 지리적 복제 파트너 관계의 주 데이터베이스를 검색 합니다.
2. Hello SQL 데이터베이스 페이지에서 선택 **지리적 복제**합니다.
3. Hello에 **보조** 목록, tooremove hello 지리적 복제 파트너 관계에서 선택 hello 데이터베이스.
4. **복제 중지**를 클릭합니다.
   
    ![보조 제거](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. 확인 창이 열립니다. 클릭 **예** hello 지리적 복제 파트너 관계에서 tooremove hello 데이터베이스. (설정 tooa 읽기 / 쓰기 데이터베이스 복제의 일부가 아닌.)

## <a name="next-steps"></a>다음 단계
* 활성 지리적 복제에 대해 자세히 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)합니다.
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.

