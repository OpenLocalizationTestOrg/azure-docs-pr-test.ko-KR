---
title: "Azure SQL 데이터베이스 tooa BACPAC 파일 aaaExport | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 Azure SQL 데이터베이스 tooa BACPAC 파일 내보내기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Azure SQL 데이터베이스 tooa BACPAC 파일 내보내기

데이터베이스 스키마와 데이터 tooa hello를 내보낼 수 보관 나 이동 tooanother 플랫폼에 대 한 데이터베이스 tooexport를 할 때 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 파일입니다. BACPAC 파일이 hello 메타 데이터 및 SQL Server 데이터베이스에서 데이터가 포함 된 BACPAC의 확장명을 가진 ZIP 파일입니다. BACPAC 파일은 Azure Blob Storage 또는 온-프레미스 저장소의 로컬 저장소에 저장할 수 있으며 나중에 Azure SQL Database 또는 SQL Server 온-프레미스 설치로 다시 가져올 수 있습니다. 

> [!IMPORTANT] 
> Azure SQL Database 자동화된 내보내기는 2017년 3월 1일에 사용이 중지되었습니다. 사용할 수 있습니다 [장기 백업 보존](sql-database-long-term-retention.md
) 또는 [Azure 자동화](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically 보관 SQL 데이터베이스 사용자가 선택한 tooa 일정에 따라 PowerShell을 사용 하 여 합니다. 샘플을 다운로드 hello [샘플 PowerShell 스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) Github에서 합니다.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Azure SQL Database를 내보낼 경우 고려 사항

* 내보내는 toobe 일관성이 hello 내보내기 작업 중에 쓰기 작업이 전혀 발생 함을 하나 또는 그는 수를 확인 해야 내보내기는 [트랜잭션 별로 일관성 있는](sql-database-copy.md) Azure SQL 데이터베이스의 합니다.
* Tooblob 저장소 내보내는 hello BACPAC 파일의 최대 크기는 200GB입니다. BACPAC 파일 크기가 커지고 tooarchive toolocal 저장소를 내보냅니다.
* 이 문서에서 설명 하는 hello 방법을 사용 하 여 BACPAC 파일 tooAzure 프리미엄 저장소를 내보내기는 지원 되지 않습니다.
* Azure SQL 데이터베이스에서 내보내는 hello 20 시간을 초과 하는 경우에 취소 될 수 있습니다. 내보내기 중 tooincrease 성능, 수행할 수 있습니다.
  * 서비스 수준을 일시적으로 높이기
  * 모든 읽기 및 쓰기 hello 내보내는 동안 작업을 중지 합니다.
  * 모든 대형 테이블에 null이 아닌 값의 [클러스터형 인덱스](https://msdn.microsoft.com/library/ms190457.aspx) 를 사용합니다. 클러스터형 인덱스가 없는 경우 6~12시간 이상 소요되면 내보내기에 실패할 수 있습니다. 이 hello 내보내기 서비스 toocomplete 테이블 스캔 tootry tooexport 전체 테이블 때문입니다. 내보내기는 toorun 테이블 가장 적합 하는 경우 좋은 방법 toodetermine **DBCC SHOW_STATISTICS** 해당 hello 있는지 확인 하 고 *RANGE_HI_KEY* null이 있으며 해당 값의 적절 한 배포 합니다. 자세한 내용은 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)를 참조하세요.

> [!NOTE]
> Bacpac 의도 한 toobe 백업 및 복원 작업에 사용 되지 않습니다. Azure SQL Database에서는 모든 사용자 데이터베이스의 백업이 자동으로 생성됩니다. 자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md) 및 [SQL Database 백업](sql-database-automated-backups.md)을 참조하세요.  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 tooa BACPAC 파일 내보내기

사용 하 여 데이터베이스 tooexport hello [Azure 포털](https://portal.azure.com)를 데이터베이스에 대 한 hello 페이지를 열고 클릭 **내보내기** hello 도구 모음입니다. Hello BACPAC 파일 이름 지정, hello 내보내기에 대 한 hello Azure 저장소 계정 및 컨테이너를 제공 하 고 hello 자격 증명 tooconnect toohello 원본 데이터베이스를 제공 합니다.  

![데이터베이스 내보내기](./media/sql-database-export/database-export.png)

hello toomonitor hello 진행률 내보내기 작업, hello 논리 서버 데이터베이스가 포함 된 hello 내보내기에 대 한 hello 페이지를 엽니다. 너무 아래로 스크롤하여**작업** 클릭 하 고 **가져오기/내보내기** 기록 합니다.

![내보내기 기록](./media/sql-database-export/export-history.png)
![내보내기 기록 상태](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Hello SQLPackage 유틸리티를 사용 하 여 tooa BACPAC 파일 내보내기

SQL tooexport hello를 사용 하 여 데이터베이스 [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 명령줄 유틸리티 참조 [매개 변수 및 속성을 내보내려면](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)합니다. 최신 버전의 hello와 함께 제공 hello SQLPackage 유틸리티 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 [Visual Studio 용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx), 하거나 최신 버전의 hello를 다운로드할 수 있습니다 [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello Microsoft에서 직접 다운로드 센터입니다.

확장 및 대부분의 프로덕션 환경에서 성능에 대 한 hello 활용을 hello SQLPackage 유틸리티 사용 하는 것이 좋습니다. SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.

이 예에서는 어떻게 SqlPackage.exe를 사용 하 여 Active Directory 유니버설 인증을 사용한 데이터베이스 a tooexport:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)를 사용 하 여 tooa BACPAC 파일 내보내기

hello 한 최신 버전의 SQL Server Management Studio는 또한 마법사 tooexport Azure SQL 데이터베이스 tooa BACPAC 파일을 제공합니다. Hello 참조 [데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)합니다.

## <a name="export-tooa-bacpac-file-using-powershell"></a>PowerShell을 사용 하 여 tooa BACPAC 파일 내보내기

사용 하 여 hello [새로 AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit 내보내기 데이터베이스 요청 toohello Azure SQL 데이터베이스 서비스입니다. 데이터베이스의 hello 크기에 따라 hello 내보내기 작업에는 일부 시간 toocomplete를 걸릴 수 있습니다.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

hello의 toocheck hello 상태 내보내기 요청, hello를 사용 하 여 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Hello 후 즉시이 명령을 실행 요청 일반적으로 반환 **상태: InProgress**합니다. 표시 되 면 **상태: 성공** hello 내보내기가 완료 된 것입니다.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>다음 단계

* toolearn 보관 목적에 대 한 데이터베이스는 대체 tooexported로 Azure SQL 데이터베이스 백업의 백업 장기 보존에 대 한 참조 [장기 백업 보존](sql-database-long-term-retention.md)합니다.
- SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.
* toolearn BACPAC tooa SQL Server 데이터베이스 가져오기에 대 한 참조 [BACPCAC tooa SQL Server 데이터베이스를 가져올](https://msdn.microsoft.com/library/hh710052.aspx)합니다.
* SQL Server 데이터베이스에서 BACPAC 내보내기에 대 한 toolearn 참조 [데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) 및 [첫 번째 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)합니다.
* SQL 데이터베이스에 궁금할 toomigration tooAzure로 SQL Server에서 내보내는 경우 참조 [SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.
