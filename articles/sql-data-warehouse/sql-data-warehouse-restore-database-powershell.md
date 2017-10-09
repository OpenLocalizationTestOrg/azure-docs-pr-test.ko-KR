---
title: "Azure SQL 데이터 웨어하우스 (PowerShell) aaaRestore | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 복원을 위한 PowerShell 작업."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Azure SQL 데이터 웨어하우스 복원(PowerShell)
> [!div class="op_single_selector"]
> * [개요][Overview]
> * [포털][Portal]
> * [PowerShell][PowerShell]
> * [REST (영문)][REST]
> 
> 

이 문서에서 어떻게 toorestore는 Azure SQL 데이터 웨어하우스 PowerShell을 사용 하 여 살펴봅니다.

## <a name="before-you-begin"></a>시작하기 전에
**DTU 용량을 확인합니다.** 각 SQL 데이터 웨어하우스는 기본 DTU 할당량이 있는 SQL server (예: myserver.database.windows.net)에 의해 호스팅됩니다.  SQL 데이터 웨어하우스를 복원 하려면 먼저 SQL 서버 hello 복원 중인 데이터베이스에 대 한 나머지 충분 한 DTU 할당량에 해당 hello를 확인 합니다. toolearn toorequest 또는 toocalculate DTU는 데 필요한 방법을 더 많은 DTU 참조 [DTU 할당량 변경 요청][Request a DTU quota change]합니다.

### <a name="install-powershell"></a>PowerShell 설치 
순서 toouse SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell 1.0 이상 tooinstall Azure PowerShell 버전을 해야 합니다.  **Get-Module -ListAvailable -Name AzureRM**을 실행하여 버전을 확인할 수 있습니다.  hello 최신 버전에서 설치 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.  Hello 최신 버전의 설치에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.

## <a name="restore-an-active-or-paused-database"></a>활성 또는 일시 중지된 데이터베이스 복원
데이터베이스 스냅숏에서 toorestore hello를 사용 하 여 [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet.

1. Windows PowerShell을 엽니다.
2. Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.
3. Hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.
4. 목록 hello hello 데이터베이스에 대 한 포인트를 복원 합니다.
5. RestorePointCreationDate hello를 사용 하 여 원하는 hello 복원 지점을 선택 합니다.
6. Hello, 원하는 toohello 복원 지점을 데이터베이스를 복원 합니다.
7. 복원 하는 hello 온라인 인지 확인 합니다.

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> Hello 복원이 완료 된 후 수행 하 여 복구 된 데이터베이스를 구성할 수 있습니다 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.
> 
> 

## <a name="restore-a-deleted-database"></a>삭제된 데이터베이스 복원
삭제 된 데이터베이스는 toorestore hello를 사용 하 여 [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Windows PowerShell을 엽니다.
2. Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.
3. 삭제 하는 hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.
4. 삭제 hello 특정 데이터베이스를 가져옵니다.
5. Hello 삭제 된 데이터베이스를 복원 합니다.
6. 복원 하는 hello 온라인 인지 확인 합니다.

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> Hello 복원이 완료 된 후 수행 하 여 복구 된 데이터베이스를 구성할 수 있습니다 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Azure 지역에서 복원
toorecover 데이터베이스를 사용 하 여 hello [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Windows PowerShell을 엽니다.
2. Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.
3. Hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.
4. Toorecover를 hello 데이터베이스를 가져옵니다.
5. Hello 데이터베이스에 대 한 hello 복구 요청을 만듭니다.
6. Hello 지리적 복원 된 데이터베이스의 hello 상태를 확인 합니다.

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> tooconfigure hello 복원이 완료 된 후 데이터베이스 참조 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.
> 
> 

복구 된 데이터베이스 hello hello 원본 데이터베이스는 TDE 사용 하도록 설정 하는 경우 TDE 설정 됩니다.

## <a name="next-steps"></a>다음 단계
Azure SQL 데이터베이스 버전의 hello 비즈니스 연속성 기능에 대 한 toolearn 읽으십시오 hello [Azure SQL 데이터베이스 비즈니스 연속성 개요][Azure SQL Database business continuity overview]합니다.

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
