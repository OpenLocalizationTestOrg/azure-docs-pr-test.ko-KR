---
title: "Azure SQL 데이터베이스 백업에서 aaaRestore | Microsoft Docs"
description: "시간 (위쪽 too35 일)에 Azure SQL 데이터베이스 tooa 이전 시점 tooroll 백 수 있도록 하는 지정 시간 복원에 대 한 설명."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>자동화된 데이터베이스 백업을 사용하여 Azure SQL 데이터베이스 복구
SQL Database는 [자동화된 데이터베이스 백업](sql-database-automated-backups.md) 및 [장기 보존에서 백업](sql-database-long-term-retention.md)을 사용한 데이터베이스 복구를 위해 다음 옵션을 제공합니다. 데이터베이스 백업에서 다음으로 복원할 수 있습니다.

* 동일한 논리 서버를 복구 하는 hello에 새 데이터베이스 tooa 지점 hello 보존 기간 내에서 시간을 지정 합니다. 
* 동일한 hello에는 데이터베이스 논리 서버 toohello 삭제 시간 삭제 된 데이터베이스를 복구 합니다.
* 모든 지역에서 모든 논리 서버에 새 데이터베이스에는 지리적으로 복제 된 blob 저장소 (RA-GRS)에 최신 매일 백업을 hello toohello 지점을 복구합니다.

> [!IMPORTANT]
> 복원하는 동안 기존 데이터베이스를 덮어쓸 수는 없습니다.
>

사용할 수도 있습니다 [자동화 된 데이터베이스 백업을](sql-database-automated-backups.md) toocreate는 [데이터베이스 복사](sql-database-copy.md) 모든 지역에서 모든 논리 서버에 있습니다. 

## <a name="recovery-time"></a>복구 시간
여러 가지 요인에 의해 영향을 자동화 된 데이터베이스 백업을 사용 하 여 데이터베이스 복구 시간 toorestore hello: 

* hello hello 데이터베이스 크기
* hello 데이터베이스의 성능 수준을 hello
* 관련 된 트랜잭션 로그의 hello 수
* hello 양의 toobe 필요한 작업이 재생 toorecover toohello 복원 지점
* hello 네트워크 대역폭이 hello 복원 하는 경우는 tooa 다른 지역 
* hello 대상 지역에서 처리 되는 요청 하는 hello 동시 복원 수입니다. 
  
  매우 큰 및/또는 현재 데이터베이스에 대 한 hello 복원에는 몇 시간이 걸릴 수 있습니다. 지역에서 장시간 가동 중단된 경우 다른 지역에서 많은 수의 지리적 복원 요청이 처리 중일 수 있습니다. 많은 요청을 해당 지역에서 데이터베이스에 대 한 hello 복구 시간이 늘어날 수 있습니다. 대부분의 데이터베이스는 12시간 내에 완전히 복원됩니다.
  
기본 제공 기능 toodo 대량 복원 되지 않습니다. hello [Azure SQL 데이터베이스: 전체 서버 복구](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) 스크립트는이 작업을 수행 하는 한 가지 방법은의 예입니다.

> [!IMPORTANT]
> 자동화 된 백업을 사용 하 여 toorecover, hello 구독에서 hello SQL Server 참가자 역할의 멤버 또는 hello 구독 소유자 여야 합니다. Hello Azure 포털, PowerShell 또는 REST API hello를 사용 하 여 복구할 수 있습니다. Transact-SQL은 사용할 수 없습니다. 
> 

## <a name="point-in-time-restore"></a>지정 시간 복원

기존 데이터베이스를 복원할 수 tooan 이전 지정 시간 hello에 새 데이터베이스와 동일한 논리 서버를 사용 하 여 Azure 포털을 hello [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), 또는 hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)합니다. 

> [!TIP]
> 데이터베이스의 지정 시간 복원을 참조 하는 tooperform 방법을 보여 주는 샘플 PowerShell 스크립트에 대 한 [PowerShell을 사용 하 여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)합니다.
>

hello 데이터베이스 수준, 및를 단일 데이터베이스로 앞으로 또는 탄력적 풀에 복원 된 tooany 서비스 계층 또는 성능 수 있습니다. Hello 논리 서버에 있는 충분 한 리소스가 또는 hello 탄력적 풀 toowhich에서 데이터베이스 복원 하는 hello를 확인 합니다. 완료 되 면 hello 복원 된 데이터베이스는 일반, 완벽 하 게 액세스할 수 있는, 온라인 데이터베이스가입니다. 서비스 계층과 성능 수준에 따라 정상 속도로 복원 hello 데이터베이스 대금이 청구 됩니다. Hello 데이터베이스 복원이 완료 될 때까지 요금이 발생 하지 않습니다.

일반적으로 데이터베이스 tooan 복원 복구를 위해 이전 지점입니다. 처리할 수 있도록 수행 하는 경우 hello hello 원래 데이터베이스에 대 한 대체 값으로 데이터베이스 복원 또는 tooretrieve 데이터를 사용 및 다음 hello 원래 데이터베이스를 업데이트 합니다. 

* ***대체 데이터베이스:*** 복원 hello 데이터베이스 hello 원래 데이터베이스에 대 한 대체 값으로 사용 되는 경우 경우 hello 성능 수준을 확인 해야 및/또는 서비스 계층 하 고 필요에 따라 hello 데이터베이스 크기. Hello 원래 데이터베이스 이름을 바꿀 수 있으며 다음 복원 하는 hello 데이터베이스 hello 원래 이름을 t-sql에서 hello ALTER DATABASE 명령을 사용 하 여 부여할 수 있습니다. 
* ***데이터 복구:*** toowrite 필요 하 고 복원 하는 hello 데이터베이스 toohello에서 hello 필요한 데이터 복구 스크립트 tooextract 데이터를 실행 하 tooretrieve 데이터에서 사용자 또는 응용 프로그램 오류 로부터 데이터베이스 toorecover hello 복원 하려는 경우 원래 데이터베이스입니다. Hello 복원 작업은 시간이 오래 toocomplete 걸릴 수 있습니다, 데이터베이스를 복원 하는 hello 이지만 hello 복원 과정에서 hello 데이터베이스 목록에 표시 합니다. Hello 복원 중 hello 데이터베이스를 삭제 하는 경우 hello 복원 작업이 취소 되 고 hello 복원을 완료 하지 못한 hello 데이터베이스에 대 한 청구 되지 않습니다. 

### <a name="azure-portal"></a>Azure portal

Azure 포털, 데이터베이스 및 클릭에 대 한 열기 hello 페이지 toorecover tooa 이유가 시간 hello **복원** hello 도구 모음입니다.

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>삭제된 데이터베이스 복원
삭제 된 데이터베이스 toohello 삭제 시간을 복원할 수 Azure 포털을 사용 하 여 동일한 논리 서버 hello hello에 삭제 된 데이터베이스에 대 한 [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), 또는 hello [REST (createMode = 복원)](https://msdn.microsoft.com/library/azure/mt163685.aspx)합니다. 

> [!TIP]
> 샘플 PowerShell 스크립트 toorestore 삭제 된 데이터베이스 참조 하는 방법을 보여 주는 [PowerShell을 사용 하 여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)합니다.
>

> [!IMPORTANT]
> Azure SQL Database 서버 인스턴스를 삭제하면 모든 해당 데이터베이스도 삭제되고 복구할 수 없습니다. 현재는 삭제된 서버 복원에 대한 지원이 제공되지 않습니다.
> 

### <a name="azure-portal"></a>Azure portal

삭제 된 toorecover 하는 동안 데이터베이스는 [보존 기간](sql-database-service-tiers.md) hello Azure 포털 hello 작업 영역에서 서버에 대해 열린 hello 페이지를 사용 하 여 클릭 **데이터베이스를 삭제 했습니다**합니다.

![삭제된 데이터베이스 복원-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![삭제된 데이터베이스 복원-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>지역 복원
Hello 가장 최근의 지리적 복제 전체 및 차등 백업에서 어떠한 Azure 지역 에서도 모든 서버에서 SQL 데이터베이스를 복원할 수 있습니다. 지리적 복원은 지역 중복 백업 원본으로 사용 하 고 사용된 toorecover hello 데이터베이스 또는 데이터 센터 중단 tooan 인해 액세스할 수 없는 경우에 데이터베이스 수 있습니다. 

지역에서 복원은 hello 데이터베이스가 호스트 되는 hello 영역의 인시던트 때문에 데이터베이스를 사용할 수 없는 경우 hello 기본 복구 옵션입니다. 하는 경우 데이터베이스 응용 프로그램의 사용할 수 없게 된 지역 결과에서 대규모 인시던트를 다른 지역에 hello 지리적으로 복제 된 백업 tooa 서버에서 데이터베이스를 복원할 수 있습니다. 차등 백업이 수행 되는 때 사이의 tooan Azure 지역으로 복제 되었을 때 지연이 blob 다른 지역에 있습니다. 이 지연 될 수 있습니다 tooan 시간을 따라서 재해가 발생할 경우 있을 수 있습니다를 tooone 시간 데이터가 손실 됩니다. 다음 그림 hello hello 사용 가능한 마지막 백업의 다른 지역에에서 hello 데이터베이스의 복원을 보여 줍니다.

![geo-restore](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> 샘플 PowerShell에 대 한 지역에서 복원은 tooperform 참조 하는 방법을 보여 주는 스크립트 [PowerShell을 사용 하 여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)합니다.
> 

지역 보조 복제본에 대한 지정 시간 복원은 현재 지원되지 않습니다. 주 데이터베이스에서만 지정 시간 복원을 수행할 수 있습니다. 지역에서 복원은 toorecover 중단에서을 사용 하는 방법에 대 한 자세한 내용은 참조 [가동 중단에서 복구](sql-database-disaster-recovery.md)합니다.

> [!IMPORTANT]
> 백업에서 복구는 hello 가장 기본적인 hello 재해 복구 솔루션으로 SQL 데이터베이스에서 사용할 수 있는 가장 긴 RPO 및 예상 복구 시간 (ERT) hello 합니다. 기본 데이터베이스를 사용하는 솔루션의 경우 지역에서 복원은 12시간의 ERT에서 적절한 DR 솔루션입니다. 복구 시간을 줄여야 하는 대규모 표준 또는 프리미엄 데이터베이스를 사용하는 솔루션의 경우 [활성 지역 복제](sql-database-geo-replication-overview.md)를 사용하도록 고려해야 합니다. 활성 지리적 복제에서는 훨씬 짧기 RPO 및 ERT 하면 다음과 장애 조치 tooa 지속적으로 복제 보조를 시작 합니다. 비즈니스 연속성 선택에 대한 자세한 내용은 [비즈니스 연속성](sql-database-business-continuity.md)을 참조하세요.
> 

### <a name="azure-portal"></a>Azure portal

toogeo 복원 하는 동안 데이터베이스 a의 [보존 기간](sql-database-service-tiers.md) hello Azure 포털을 사용 하 여 hello SQL 데이터베이스 페이지를 열고 클릭 **추가**합니다. Hello에 **선택 소스** 텍스트 상자의 **백업**합니다. Hello 지역에 및 선택한 hello 서버에는 tooperform hello 복구가에서 hello 백업을 지정 합니다. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>자동화된 백업을 사용하여 프로그래밍 방식으로 복구 수행
앞에서 설명한 대로 또한 toohello 데이터베이스를 복구 하는 Azure 포털, Azure PowerShell을 사용 하 여 프로그래밍 방식으로 수행할 수 있습니다 또는 환영 REST API. 다음 표에서 hello hello 명령 집합을 사용할 수 있는 설명 합니다.

### <a name="powershell"></a>PowerShell
| Cmdlet | 설명 |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |하나 이상의 데이터베이스를 가져옵니다. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | 복원할 수 있는 삭제된 데이터베이스를 가져옵니다. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |데이터베이스의 지역 중복 백업을 가져옵니다. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |SQL 데이터베이스를 복원합니다. |
|  | |

### <a name="rest-api"></a>REST API
| API | 설명 |
| --- | --- |
| [REST(createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |데이터베이스를 복원합니다. |
| [데이터베이스 만들기 또는 업데이트 상태 가져오기](https://msdn.microsoft.com/library/azure/mt643934.aspx) |복원 작업 중 반환 hello 상태 |
|  | |

## <a name="summary"></a>요약
자동 백업은 사용자 및 응용 프로그램 오류, 우발적인 데이터베이스 삭제 및 장시간의 가동 중단에서 데이터베이스를 보호합니다. 이 기본 제공 기능은 모든 서비스 계층 및 성능 수준에 사용할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)
* Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [자동화 된 백업을 SQL 데이터베이스](sql-database-automated-backups.md)
* 장기 백업 보존에 대 한 toolearn 참조 [장기 백업 보존](sql-database-long-term-retention.md)
* tooconfigure, 관리 및 Azure 포털에서 참조 hello를 사용 하는 Azure 복구 서비스 자격 증명 모음에 대 한 자동화 된 백업의 장기간 보관에서 복원 [구성 및 사용 하 여 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다. 
* 빠른 복구 옵션에 대 한 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)  
