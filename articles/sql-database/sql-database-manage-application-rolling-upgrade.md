---
title: "Azure SQL 데이터베이스-aaaRolling 응용 프로그램 업그레이드 | Microsoft Docs"
description: "자세한 내용은 방법 클라우드 응용 프로그램의 Azure SQL 데이터베이스 지역에서 복제 toouse toosupport 온라인 업그레이드 합니다."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>SQL Database 활성 지역 복제를 사용하여 클라우드 응용 프로그램의 롤링 업그레이드 관리
> [!NOTE]
> [활성 지역 복제](sql-database-geo-replication-overview.md)는 현재 모든 계층의 모든 데이터베이스에 대해 제공됩니다.
> 

자세한 내용은 방법 toouse [지리적 복제](sql-database-geo-replication-overview.md) tooenable SQL 데이터베이스의에서 롤링 업그레이드 클라우드 응용 프로그램의 경우. 업그레이드는 중단 작업이기 때문에 무중단 업무 방식 계획 및 디자인의 일부여야 합니다. Hello 조정의 두 가지 방법에 살펴보기이 문서에서 업그레이드 작업을 하 고 hello 이점 및 각 옵션의 장단점을 설명 합니다. 이 여기서 해결 hello에 대 한 웹 사이트 연결 된 tooa 단일 데이터베이스의 데이터 계층으로 구성 된 간단한 응용 프로그램을 사용 합니다. 목표는 tooupgrade 버전 1의 중요 한 영향 주지 않고 응용 프로그램 tooversion hello 2 hello 최종 사용자 환경에 합니다. 

Hello 업그레이드 옵션을 평가할 때 hello를 요인에 따라이 좋습니다.

* 업그레이드 중에 응용 프로그램 가용성에 미치는 영향 시간 hello 응용 프로그램 기능 제한 또는 저하 됨 수 있습니다.
* 업그레이드 오류가 발생할 경우 다시 tooroll 기능입니다.
* Hello 응용 프로그램에서 관련 없는 치명적인 오류가 hello 업그레이드 하는 동안 발생 하는 경우의 보안 문제가 있습니다.
* 총 달러 비용.  추가적인 중복성이 구현 및 hello 업그레이드 프로세스에서 사용 된 hello 임시 구성 요소의 증분 비용이 포함 됩니다. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>재해 복구에 대해 데이터베이스 백업을 사용하는 응용 프로그램 업그레이드
응용 프로그램 자동 데이터베이스 백업에 의존 하 고 재해 복구에 대 한 지역에서 복원을 사용 하 여, 경우 일반적으로 배포 된 tooa 단일 Azure 지역입니다. 이 경우 hello 업그레이드 프로세스는 hello 업그레이드에 포함 된 모든 응용 프로그램 구성 요소의 백업 배포를 만들려면 포함 됩니다. Azure 트래픽 관리자 (WATM)를 활용 하 여 hello 장애 조치 프로필로 됩니다 toominimize hello 최종 사용자 중단.  다음 다이어그램 hello hello 운영 환경을 이전 toohello 업그레이드 프로세스를 보여 줍니다. 끝점 hello <i>contoso 1.azurewebsites.net</i> toobe 업그레이드 하는 hello 응용 프로그램의는 프로덕션 슬롯을 나타냅니다. tooenable hello 기능 tooroll 다시 hello 업그레이드, 완벽 하 게 동기화 된 hello 응용 프로그램의 복사본으로 단계 슬롯을 만들어야 합니다. hello 다음 단계는 hello 업그레이드에 필요한 tooprepare hello 응용 프로그램.

1. Hello 업그레이드에 대 한 단계 슬롯을 만듭니다. toodo 보조 데이터베이스 (1)을 만들고 hello에는 동일한 웹 사이트를 배포 하는 동일한 Azure 지역에 있습니다. 프로세스를 시드 hello에 완료 되 면 hello 보조 toosee를 모니터링 합니다.
2. <i>contoso-1.azurewebsites.net</i>을 온라인 끝점으로 하고 <i>contoso-2.azurewebsites.net</i>을 오프라인으로 하여 WATM에서 장애 조치(failover) 프로필을 만듭니다. 

> [!NOTE]
> 참고 hello 준비 단계 hello 응용 프로그램 hello 프로덕션 슬롯에 영향을 주지 않을 하 고 전체 액세스 모드에서 작동할 수 있습니다.
>  

![SQL 데이터베이스 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Hello 준비 단계가 완료 되 면 hello 응용 프로그램은 실제 업그레이드를 hello 준비가 됩니다. 다음 다이어그램 hello hello 업그레이드 프로세스에 관련 된 hello 단계를 보여 줍니다. 

1. Hello 프로덕션 슬롯 tooread 전용 모드 (3) hello 주 데이터베이스를 설정 합니다. 이렇게 하면 해당 hello hello (V1) 응용 프로그램의 프로덕션 인스턴스에 읽기 전용 이어서 hello V1 및 V2 데이터베이스 인스턴스 간의 데이터 차이 hello 없는 hello 업그레이드 하는 동안 유지 됩니다.  
2. Hello 계획 된 종료 모드 (4)를 사용 하 여 hello 보조 데이터베이스를 분리 합니다. Hello 주 데이터베이스의 완전 하 게 동기화 된 독립 복사본을 만들어집니다. 이 데이터베이스가 업그레이드됩니다.
3. Hello 주 데이터베이스 tooread-쓰기 모드를 설정 하 고 hello 단계 슬롯 (5)의 hello 업그레이드 스크립트를 실행 합니다.     

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Hello 업그레이드가 성공적으로 완료 하는 경우 준비 tooswitch hello 최종 사용자가 준비 된 toohello 복사 hello 응용이 나타납니다. 이제 hello 응용 프로그램의 hello 프로덕션 슬롯 됩니다.  Hello 다이어그램을 다음에 설명 된 대로 몇 가지 더 많은 단계가 포함 됩니다.

1. Hello WATM 프로필의 hello 온라인 끝점을 너무 전환<i>contoso 2.azurewebsites.net</i>, 어떤 포인트 toohello V2 버전의 hello 웹 사이트 (6). 이제 hello 프로덕션 슬롯 hello V2 응용 프로그램을 되며 hello 최종 사용자 트래픽이 directed tooit입니다.  
2. 안전 하 게 할 수 있도록 hello V1 응용 프로그램 구성 요소를 더 이상 필요 제거 (7).   

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Hello 업그레이드 프로세스가 실패할 경우 예를 들어 스크립트를 업그레이드 하는 hello에서는 tooan 오류 인해 hello 단계 슬롯 고려할 손상 됩니다. tooroll 백업 hello 응용 프로그램 toohello 업그레이드 전 상태 hello 프로덕션 슬롯 toofull 액세스의 hello 응용 프로그램을 되돌리면 됩니다. 관련 된 hello 단계 hello 다음 다이어그램에 표시 됩니다.    

1. Hello 데이터베이스 복사본 tooread-쓰기 모드 (8)를 설정 합니다. 이렇게 하면 복원 됩니다 hello 프로덕션 슬롯에서 기능적으로 전체 V1 hello 합니다.
2. Hello 근본 원인 분석을 수행 하 고 hello 단계 슬롯 (9)의 보안이 손상 hello 구성 요소를 제거 합니다. 

이 경우 hello 응용 프로그램의 모든 기능이 작동 하 고 hello 업그레이드 단계를 반복할 수 있습니다.

> [!NOTE]
> hello 롤백 하지 않아도 WATM 프로필의 변경 내용을 이미 가리키도록 너무 대로<i>contoso 1.azurewebsites.net</i> hello 활성 끝점으로 합니다.
> 
> 

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

hello 키 **장점은** 이 옵션은 일련의 간단한 단계를 사용 하 여 단일 지역에서 응용 프로그램을 업그레이드할 수 있습니다. hello 비용 (달러) hello 업그레이드의 상대적으로 낮습니다. 주 hello **단점이** hello 업그레이드 hello 복구 toohello 업그레이드 전 상태 동안 심각한 오류가 발생 한 경우는 포함 된 서로 다른 지역 및 hello 데이터베이스에서 복원 hello 응용 프로그램 배포는 지역에서 복원을 사용 하 여 백업입니다. 이 프로세스를 통해 상당한 가동 중지 시간이 발생합니다.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>재해 복구에 대해 데이터베이스 지역에서 복제를 사용하는 응용 프로그램 업그레이드
비즈니스 연속성에 대 한 지리적 복제를 활용 하는 응용 프로그램을 경우 기본 지역에서 활성 배포와 대기 배포 백업 지역에 배포 된 tooat 최소 두 개의 서로 다른 지역입니다. 또한 toohello 요소 앞에서 언급 한, hello 업그레이드 프로세스는 하도록 보장 해야 합니다.

* hello hello 업그레이드 프로세스 중 언제 든 치명적인 오류 로부터 보호 하는 응용 프로그램은 유지
* hello 활성 구성 요소를 병렬로 hello 응용 프로그램의 hello 지리적 중복 구성 요소가 업그레이드

tooachieve 활성 배포와 세 개의 백업 끝점으로 프로 파일링 이러한 목표는 Azure 트래픽 관리자 (WATM) hello 장애 조치를 사용 하 여를 이용 합니다.  다음 다이어그램 hello hello 운영 환경을 이전 toohello 업그레이드 프로세스를 보여 줍니다. 웹 사이트를 hello <i>contoso 1.azurewebsites.net</i> 및 <i>contoso dr.azurewebsites.net</i> 전체 지리적 중복 hello 응용 프로그램의 프로덕션 슬롯을 나타냅니다. tooenable hello 기능 tooroll 다시 hello 업그레이드, 완벽 하 게 동기화 된 hello 응용 프로그램의 복사본으로 단계 슬롯을 만들어야 합니다. Hello 응용 프로그램 hello 업그레이드 프로세스 중에 치명적인 오류가 발생 하는 경우를 빠르게 복구할 수 tooensure 필요 하기 때문에 hello 단계 슬롯 필요 toobe 지리적 중복도 합니다. hello 다음 단계는 hello 업그레이드에 필요한 tooprepare hello 응용 프로그램.

1. Hello 업그레이드에 대 한 단계 슬롯을 만듭니다. toodo 보조 데이터베이스 (1)을 만들고 hello에서 hello 웹 사이트의 동일한 복사본을 배포 하는 동일한 Azure 지역에 있습니다. 프로세스를 시드 hello에 완료 되 면 hello 보조 toosee를 모니터링 합니다.
2. 지리적 복제 하 여 hello 단계 슬롯에 지리적 중복 보조 데이터베이스를 만들 hello 보조 데이터베이스 toohello 백업 영역 (라고 "지리적 복제 연결"). 프로세스를 시드 hello이 완료 된 (3) 백업 보조 toosee hello를 모니터링 합니다.
3. Hello 백업 영역의 hello 웹 사이트의 대기 복사본을 만들고 toohello 지리적 중복 보조 데이터베이스 (4)에 연결 합니다.  
4. Hello 추가 끝점을 추가 <i>contoso 2.azurewebsites.net</i> 및 <i>contoso 3.azurewebsites.net</i> toohello 장애 조치 프로필 WATM에 오프 라인 (5)의 끝점으로 합니다. 

> [!NOTE]
> 참고 hello 준비 단계 hello 응용 프로그램 hello 프로덕션 슬롯에 영향을 주지 않을 하 고 전체 액세스 모드에서 작동할 수 있습니다.
> 
> 

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Hello 준비 단계가 완료 되 면 hello 단계 슬롯이 hello 업그레이드 준비 되었습니다. 다음 다이어그램 hello hello 업그레이드 단계를 보여 줍니다.

1. Hello 프로덕션 슬롯 tooread 전용 모드 (6) hello 주 데이터베이스를 설정 합니다. 이렇게 하면 해당 hello hello (V1) 응용 프로그램의 프로덕션 인스턴스에 읽기 전용 이어서 hello V1 및 V2 데이터베이스 인스턴스 간의 데이터 차이 hello 없는 hello 업그레이드 하는 동안 유지 됩니다.  
2. Hello 보조 데이터베이스를 분리 hello 계획 된 종료 모드 (7)를 사용 하 여 동일한 지역 hello에 있습니다. Hello 종료 된 후 기본 될 자동으로 hello 주 데이터베이스의 완전 하 게 동기화 된 독립 복사본을 만들어집니다. 이 데이터베이스가 업그레이드됩니다.
3. Hello 단계 슬롯 tooread 쓰기 모드로 hello 주 데이터베이스를 설정 하 고 hello 업그레이드 스크립트 (8)를 실행 합니다.    

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Hello 업그레이드가 성공적으로 완료 하는 경우 준비 tooswitch hello 최종 사용자에 게 toohello V2 버전의 hello 응용 프로그램이 나타납니다. 다음 다이어그램 hello hello 단계를 보여 줍니다.

1. Hello WATM 프로필의 hello 활성 끝점을 너무 전환<i>contoso 2.azurewebsites.net</i>, 이제 toohello V2 버전의 hello 웹 사이트 (9)를 가리킵니다. 이제 프로덕션 슬롯 hello V2 응용 프로그램을 되며 최종 사용자 트래픽이 directed tooit입니다. 
2. 안전 하 게 할 수 있도록 hello V1 응용 프로그램을 더 이상 해야 하는 경우 제거 (10과 11).  

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Hello 업그레이드 프로세스가 실패할 경우 예를 들어 스크립트를 업그레이드 하는 hello에서는 tooan 오류 인해 hello 단계 슬롯 고려할 손상 됩니다. tooroll 백업 hello 응용 프로그램 toohello 업그레이드 전 상태 전체 액세스 권한이 있는 hello 프로덕션 슬롯에서 toousing hello 응용 프로그램을 되돌리면 됩니다. 관련 된 hello 단계 hello 다음 다이어그램에 표시 됩니다.    

1. 집합 hello는 hello 프로덕션 슬롯 tooread-쓰기 모드 (12)의 복사본을 주 데이터베이스입니다. 이렇게 하면 복원 됩니다 hello 프로덕션 슬롯에서 기능적으로 전체 V1 hello 합니다.
2. Hello 근본 원인 분석을 수행 하 고 hello 단계 슬롯 (13 및 14)의 보안이 손상 hello 구성 요소를 제거 합니다. 

이 경우 hello 응용 프로그램의 모든 기능이 작동 하 고 hello 업그레이드 단계를 반복할 수 있습니다.

> [!NOTE]
> hello 롤백 하지 않아도 WATM 프로필의 변경 내용을 이미 가리키도록 너무 대로 <i>contoso 1.azurewebsites.net</i> hello 활성 끝점으로 합니다.
> 
> 

![SQL Database 지역에서 복제 구성 클라우드 재해 복구](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

hello 키 **장점은** 은이 옵션의 hello 업그레이드 하는 동안 비즈니스 연속성을 유지 하면서 hello 응용 프로그램과 병렬로 지리적 중복 복사본을 모두 업그레이드할 수 있습니다. 주 hello **적절 한 균형을** 이중 중복 각 응용 프로그램 구성 요소에 필요 하며 따라서에 주는 영향이 더 높은 달러 됩니다. 또한 더 복잡한 워크플로가 사용됩니다. 

## <a name="summary"></a>요약
hello 문서에서 설명 하는 hello 두 업그레이드 방법 비용 복잡성과 hello 달러만 모두 집중 때 hello 최종 사용자가 제한 된 tooread 전용 작업 hello 시간을 최소화 합니다. 이때는 hello 업그레이드 스크립트의 hello 기간으로 직접 정의 됩니다. Hello 데이터베이스 크기에 의존 하지 않는, 선택, hello 웹 사이트 구성 및 쉽게 제어할 수 없는 기타 요인 hello 서비스 계층 있습니다. 이므로 모든 hello 준비 단계 hello 업그레이드 단계에서 분리 되어 hello 프로덕션 응용 프로그램에 영향을 주지 않고 수행할 수 있습니다. hello 업그레이드 스크립트의 hello 효율성은 업그레이드 중 hello 최종 사용자 환경을 결정 하는 hello 주요 요소입니다. 따라서 hello 가장 좋은 방법은 향상 시킬 수 있습니다는 hello 업그레이드 스크립트를 최대한 효율적으로 만드는 작업을 중심으로 합니다.  

## <a name="next-steps"></a>다음 단계
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.
* Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [SQL 데이터베이스 자동화 된 백업을](sql-database-automated-backups.md)합니다.
* 복구를 위한 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [자동화 된 백업에서 데이터베이스를 복원](sql-database-recovery-using-backups.md)합니다.
* 빠른 복구 옵션에 대 한 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)합니다.


