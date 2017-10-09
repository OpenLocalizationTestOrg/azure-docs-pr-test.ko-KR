---
title: "SQL 데이터베이스 자동, 지역 중복 백업을 aaaAzure | Microsoft Docs"
description: "SQL Database는 몇 분마다 로컬 데이터베이스 백업을 자동으로 만들고 Azure 읽기 액세스 지역 중복 저장소를 사용하여 지리적 중복을 제공합니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>자동 SQL Database 백업에 대한 자세한 정보

SQL 데이터베이스는 자동으로 데이터베이스 백업을 만듭니다 하 고 Azure 읽기 액세스 지역 중복 저장소 (RA-GRS) tooprovide 지리적 중복을 사용 합니다. 이러한 백업은 추가 비용 없이 자동으로 만들어집니다. 발생 하는 toomake toodo을 어느 것에 필요 하지 않습니다. 데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다. 사용자 고유의 저장소 컨테이너에 tookeep 백업 하려는 경우 장기 백업 보존 정책을 구성할 수 있습니다. 자세한 내용은 [장기 보존](sql-database-long-term-retention.md)을 참조하세요.

## <a name="what-is-a-sql-database-backup"></a>SQL Database 백업이란?

SQL 데이터베이스에서는 SQL Server 기술 toocreate 사용 [전체](https://msdn.microsoft.com/library/ms186289.aspx), [차등](https://msdn.microsoft.com/library/ms175526.aspx), 및 [트랜잭션 로그](https://msdn.microsoft.com/library/ms191429.aspx) 백업 합니다. 일반적으로 hello 트랜잭션 로그 백업을 hello 주파수 hello 성능 수준 및 데이터베이스 작업의 크기에 따라 5-10 분 마다 발생 합니다. 전체 및 차등 백업과 함께 트랜잭션 로그 백업을 허용 toorestore 데이터베이스 tooa 특정 지정 시간 toohello hello 데이터베이스를 호스팅하는 동일한 서버입니다. 데이터베이스를 복원 하면 hello 서비스 수치는 전체, 차등 및 트랜잭션 로그 백업을 할 toobe 복원 합니다.


이러한 백업을 사용하여 다음을 수행할 수 있습니다.

* Hello 보존 기간 내의 데이터베이스 tooa에-시간을 복원 합니다. 이 작업 hello에 새 데이터베이스를 만드는 hello 원래 데이터베이스와 같은 서버입니다.
* 삭제 된 삭제 된 데이터베이스 toohello 시간 또는 hello 보존 기간 내에서 언제 든 지 복원 합니다. hello에만 삭제 하는 hello 데이터베이스를 복원할 수 같은 서버 hello 원래 데이터베이스를 만들었습니다.
* Tooanother 지리적 지역의 데이터베이스를 복원 합니다. 이 지리적 재해에서 toorecover를 시기 있습니다 서버 및 데이터베이스에 액세스할 수 없습니다. Hello world에서 아무 곳 이나 모든 기존 서버에 새 데이터베이스를 만듭니다. 
* Azure Recovery Services 자격 증명 모음에 저장된 특정 백업에서 데이터베이스를 복원합니다. 이렇게 하면 toorun hello 응용 프로그램의 이전 버전 또는 이전 버전의 hello 데이터베이스 toosatisfy 규정 준수 요청 toorestore 있습니다. [장기 보존](sql-database-long-term-retention.md)을 참조하세요.
* tooperform 복원 하는 참조 [백업에서 데이터베이스를 복원](sql-database-recovery-using-backups.md)합니다.

> [!NOTE]
> Azure 저장소에 hello 용어 *복제* toocopying 파일 tooanother 한 위치에서에서 참조 합니다. SQL의 *데이터베이스 복제* 참조 tookeeping toomultiple 보조 데이터베이스가 주 데이터베이스와 동기화 합니다. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>무료 백업 저장소가 얼마나 포함되어 있습니까?
SQL 데이터베이스 프로 비전 된 최대 데이터베이스 저장소의 too200% 최대 추가 비용 없이 백업 저장소로 제공합니다. 예를 들어, 프로비전된 DB의 크기가 250GB인 Standard DB 인스턴스가 있으면 추가 비용 없이 500GB의 백업 저장소를 갖습니다. 데이터베이스 백업 저장소를 제공 하는 hello를 초과 하면 Azure 지원에 문의 하 여 tooreduce hello 보존 기간을 선택할 수 있습니다. 다른 옵션은 toopay hello 표준 읽기 액세스 지리적 중복 저장소 (RA-GRS) 요금이 청구 되는 추가 백업 저장소에 있습니다. 

## <a name="how-often-do-backups-happen"></a>백업이 얼마나 자주 수행됩니까?
매주 전체 데이터베이스 백업이 수행되고, 일반적으로 몇 시간마다 차등 데이터베이스 백업이 수행되며, 일반적으로 5 - 10분마다 트랜잭션 로그 백업이 수행됩니다. hello 첫 번째 전체 백업은 데이터베이스를 만든 직후에 예약 됩니다. 일반적으로 30 분 이내 완료 하지만 hello 데이터베이스가 크기가 큰 경우에 더 오래 걸릴 수 있습니다. 예를 들어 hello 초기 백업을 복원 된 데이터베이스 또는 데이터베이스 복사본에 더 오래 걸릴 수 있습니다. Hello 첫 번째 전체 백업 후 모든 향후 백업을 자동으로 예약 되 고 hello 백그라운드에서 자동으로 관리 합니다. 모든 데이터베이스 백업 hello 정확한 시점 hello SQL 데이터베이스 서비스에 의해 결정은 보내는 전반적인 hello 균형을 조정 시스템 작업 합니다. 

hello 백업 저장소 지역 간 복제 hello Azure 저장소 복제 일정에 따라 발생합니다.

## <a name="how-long-do-you-keep-my-backups"></a>백업 보존 기간
각 SQL 데이터베이스 백업 보존 기간은 hello를 기반으로 하는 [서비스 계층](sql-database-service-tiers.md) hello 데이터베이스의 합니다. 데이터베이스에 대 한 보존 기간 hello에서:


* 기본 서비스 계층은 7일입니다.
* 표준 서비스 계층은 35일입니다.
* 프리미엄 서비스 계층은 35일입니다.

Hello Standard 또는 Premium 서비스 계층 tooBasic에서 데이터베이스를 다운 그레이드 hello 백업이 7 일 동안 저장 됩니다. 7일보다 오래된 모든 기존 백업은 더 이상 사용할 수 없게 됩니다. 

기본 서비스 계층 tooStandard hello 또는 Premium에서 데이터베이스를 업그레이드 하는 경우 35 일이 넘으면 될 때까지 SQL 데이터베이스 기존 백업을 유지 합니다. 새 백업이 발생하면 새 백업을 35일 동안 보관합니다.

SQL 데이터베이스 hello에 hello 백업을 보관 데이터베이스를 삭제 하면 온라인 데이터베이스에 대 한 개가 있습니다. 예를 들어 보존 기간이 7일인 기본 데이터베이스를 삭제한다고 가정해 봅시다. 4일 된 백업은 앞으로 3일 동안 더 보관됩니다.

> [!IMPORTANT]
> Hello Azure SQL server를 호스팅하는 SQL 데이터베이스를 삭제 하면 toohello 서버에 속하는 모든 데이터베이스가 삭제 되 고 복구할 수 없습니다. 삭제된 서버는 복원할 수 없습니다.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>어떻게 tooextend hello 백업 보존 기간?
응용 프로그램에 대 한 긴 시간 동안 사용할 수 있는 hello 백업이 필요한 경우에 개별 데이터베이스 (LTR 정책)에 대 한 hello 장기 백업 보존 정책을 구성 하 여 hello 기본 보존 기간을 확장할 수 있습니다. 이렇게 하면 35 일 tooup too10 년 동안의 tooextend hello 작성 it 보존 기간이 있습니다. 자세한 내용은 [장기 보존](sql-database-long-term-retention.md)을 참조하세요.

Hello 주별 전체 데이터베이스 백업을 자동으로 복사 된 tooyour 됩니다 Azure 포털 또는 API를 사용 하 여 hello LTR 정책 tooa 데이터베이스를 추가 하면 Azure 백업 서비스 자격 증명 모음을 소유 합니다. 데이터베이스에 암호화 된 경우 TDE hello 백업이 미사용 자동으로 암호화 됩니다.  hello 서비스 자격 증명 모음에는 타임 스탬프 및 hello LTR 정책에 따른 만료 된 백업을 자동으로 삭제 됩니다.  하지 않으면 하므로 필요 toomanage hello에 대 한 백업 일정 또는 hello 정리 하는 방법에 대 한 문제를 모두 해결 hello 오래 된 파일입니다. hello 복원 API 지원 hello 자격 증명 모음에는 hello에 저장 된 백업 자격 증명 모음에 SQL 데이터베이스와 같은 구독을 hello 합니다. 이러한 백업을 hello Azure 포털 또는 PowerShell tooaccess 사용할 수 있습니다.

> [!TIP]
> 방법 tooguide 참조 [장기 백업 보존 Azure SQL 데이터베이스에서에서 복원 및 구성](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>백업이 암호화되나요?

Azure SQL Database에 TDE를 사용할 때 백업이 암호화됩니다. 모든 새 Azure SQL Database는 기본적으로 사용한 TDE로 구성됩니다. TDE에 대한 자세한 내용은 [Azure SQL Database를 사용한 투명한 데이터 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- 데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다. 다른 Azure SQL 데이터베이스 비즈니스 연속성 솔루션 hello, 참조에 대 한 정보 toolearn [비즈니스 연속성 개요](sql-database-business-continuity.md)합니다.
- toorestore tooa 지정 시간 hello Azure 포털을 사용 하 여 참조 [hello Azure 포털을 사용 하 여 시간에 복원 데이터베이스 tooa 지점을](sql-database-recovery-using-backups.md)합니다.
- PowerShell을 사용 하 여 시간에 toorestore tooa 지점 참조 [복원 PowerShell을 사용 하 여 시간에 데이터베이스 tooa 지점을](scripts/sql-database-restore-database-powershell.md)합니다.
- tooconfigure, 관리 및 Azure 포털에서 참조 hello를 사용 하는 Azure 복구 서비스 자격 증명 모음에 대 한 자동화 된 백업의 장기간 보관에서 복원 [Azure 포털 hello 사용 하 여 관리 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다.
- tooconfigure를 관리 및 PowerShell을 사용 하는 Azure 복구 서비스 자격 증명 모음에 대 한 자동화 된 백업의 장기간 보관에서 복원, 참조 [PowerShell을 사용 하 여 장기 백업 보존 관리](sql-database-long-term-backup-retention-configure.md)합니다.
