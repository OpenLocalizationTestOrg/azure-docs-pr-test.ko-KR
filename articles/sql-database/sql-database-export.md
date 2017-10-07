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
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a><span data-ttu-id="2ee2a-103">Azure SQL 데이터베이스 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-103">Export an Azure SQL database tooa BACPAC file</span></span>

<span data-ttu-id="2ee2a-104">데이터베이스 스키마와 데이터 tooa hello를 내보낼 수 보관 나 이동 tooanother 플랫폼에 대 한 데이터베이스 tooexport를 할 때 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-104">When you need tooexport a database for archiving or for moving tooanother platform, you can export hello database schema and data tooa [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="2ee2a-105">BACPAC 파일이 hello 메타 데이터 및 SQL Server 데이터베이스에서 데이터가 포함 된 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="2ee2a-106">BACPAC 파일은 Azure Blob Storage 또는 온-프레미스 저장소의 로컬 저장소에 저장할 수 있으며 나중에 Azure SQL Database 또는 SQL Server 온-프레미스 설치로 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-106">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="2ee2a-107">Azure SQL Database 자동화된 내보내기는 2017년 3월 1일에 사용이 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-107">Azure SQL Database Automated Export was retired on March 1, 2017.</span></span> <span data-ttu-id="2ee2a-108">사용할 수 있습니다 [장기 백업 보존](sql-database-long-term-retention.md
) 또는 [Azure 자동화](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically 보관 SQL 데이터베이스 사용자가 선택한 tooa 일정에 따라 PowerShell을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-108">You can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically archive SQL databases using PowerShell according tooa schedule of your choice.</span></span> <span data-ttu-id="2ee2a-109">샘플을 다운로드 hello [샘플 PowerShell 스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) Github에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-109">For a sample, download hello [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a><span data-ttu-id="2ee2a-110">Azure SQL Database를 내보낼 경우 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2ee2a-110">Considerations when exporting an Azure SQL database</span></span>

* <span data-ttu-id="2ee2a-111">내보내는 toobe 일관성이 hello 내보내기 작업 중에 쓰기 작업이 전혀 발생 함을 하나 또는 그는 수를 확인 해야 내보내기는 [트랜잭션 별로 일관성 있는](sql-database-copy.md) Azure SQL 데이터베이스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-111">For an export toobe transactionally consistent, you must ensure either that no write activity is occurring during hello export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span></span>
* <span data-ttu-id="2ee2a-112">Tooblob 저장소 내보내는 hello BACPAC 파일의 최대 크기는 200GB입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-112">If you are exporting tooblob storage, hello maximum size of a BACPAC file is 200 GB.</span></span> <span data-ttu-id="2ee2a-113">BACPAC 파일 크기가 커지고 tooarchive toolocal 저장소를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-113">tooarchive a larger BACPAC file, export toolocal storage.</span></span>
* <span data-ttu-id="2ee2a-114">이 문서에서 설명 하는 hello 방법을 사용 하 여 BACPAC 파일 tooAzure 프리미엄 저장소를 내보내기는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-114">Exporting a BACPAC file tooAzure premium storage using hello methods discussed in this article is not supported.</span></span>
* <span data-ttu-id="2ee2a-115">Azure SQL 데이터베이스에서 내보내는 hello 20 시간을 초과 하는 경우에 취소 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-115">If hello export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span></span> <span data-ttu-id="2ee2a-116">내보내기 중 tooincrease 성능, 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-116">tooincrease performance during export, you can:</span></span>
  * <span data-ttu-id="2ee2a-117">서비스 수준을 일시적으로 높이기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-117">Temporarily increase your service level.</span></span>
  * <span data-ttu-id="2ee2a-118">모든 읽기 및 쓰기 hello 내보내는 동안 작업을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-118">Cease all read and write activity during hello export.</span></span>
  * <span data-ttu-id="2ee2a-119">모든 대형 테이블에 null이 아닌 값의 [클러스터형 인덱스](https://msdn.microsoft.com/library/ms190457.aspx) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-119">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span></span> <span data-ttu-id="2ee2a-120">클러스터형 인덱스가 없는 경우 6~12시간 이상 소요되면 내보내기에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-120">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span></span> <span data-ttu-id="2ee2a-121">이 hello 내보내기 서비스 toocomplete 테이블 스캔 tootry tooexport 전체 테이블 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-121">This is because hello export service needs toocomplete a table scan tootry tooexport entire table.</span></span> <span data-ttu-id="2ee2a-122">내보내기는 toorun 테이블 가장 적합 하는 경우 좋은 방법 toodetermine **DBCC SHOW_STATISTICS** 해당 hello 있는지 확인 하 고 *RANGE_HI_KEY* null이 있으며 해당 값의 적절 한 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-122">A good way toodetermine if your tables are optimized for export is toorun **DBCC SHOW_STATISTICS** and make sure that hello *RANGE_HI_KEY* is not null and its value has good distribution.</span></span> <span data-ttu-id="2ee2a-123">자세한 내용은 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-123">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2ee2a-124">Bacpac 의도 한 toobe 백업 및 복원 작업에 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-124">BACPACs are not intended toobe used for backup and restore operations.</span></span> <span data-ttu-id="2ee2a-125">Azure SQL Database에서는 모든 사용자 데이터베이스의 백업이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-125">Azure SQL Database automatically creates backups for every user database.</span></span> <span data-ttu-id="2ee2a-126">자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md) 및 [SQL Database 백업](sql-database-automated-backups.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-126">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span></span>  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a><span data-ttu-id="2ee2a-127">Hello Azure 포털을 사용 하 여 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-127">Export tooa BACPAC file using hello Azure portal</span></span>

<span data-ttu-id="2ee2a-128">사용 하 여 데이터베이스 tooexport hello [Azure 포털](https://portal.azure.com)를 데이터베이스에 대 한 hello 페이지를 열고 클릭 **내보내기** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-128">tooexport a database using hello [Azure portal](https://portal.azure.com), open hello page for your database and click **Export** on hello toolbar.</span></span> <span data-ttu-id="2ee2a-129">Hello BACPAC 파일 이름 지정, hello 내보내기에 대 한 hello Azure 저장소 계정 및 컨테이너를 제공 하 고 hello 자격 증명 tooconnect toohello 원본 데이터베이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-129">Specify hello BACPAC filename, provide hello Azure storage account and container for hello export, and provide hello credentials tooconnect toohello source database.</span></span>  

![데이터베이스 내보내기](./media/sql-database-export/database-export.png)

<span data-ttu-id="2ee2a-131">hello toomonitor hello 진행률 내보내기 작업, hello 논리 서버 데이터베이스가 포함 된 hello 내보내기에 대 한 hello 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-131">toomonitor hello progress of hello export operation, open hello page for hello logical server containing hello database being exported.</span></span> <span data-ttu-id="2ee2a-132">너무 아래로 스크롤하여**작업** 클릭 하 고 **가져오기/내보내기** 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-132">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

<span data-ttu-id="2ee2a-133">![내보내기 기록](./media/sql-database-export/export-history.png)
![내보내기 기록 상태](./media/sql-database-export/export-history2.png)</span><span class="sxs-lookup"><span data-stu-id="2ee2a-133">![export history](./media/sql-database-export/export-history.png)
![export history status](./media/sql-database-export/export-history2.png)</span></span>

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a><span data-ttu-id="2ee2a-134">Hello SQLPackage 유틸리티를 사용 하 여 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-134">Export tooa BACPAC file using hello SQLPackage utility</span></span>

<span data-ttu-id="2ee2a-135">SQL tooexport hello를 사용 하 여 데이터베이스 [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 명령줄 유틸리티 참조 [매개 변수 및 속성을 내보내려면](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-135">tooexport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span></span> <span data-ttu-id="2ee2a-136">최신 버전의 hello와 함께 제공 hello SQLPackage 유틸리티 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 [Visual Studio 용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx), 하거나 최신 버전의 hello를 다운로드할 수 있습니다 [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello Microsoft에서 직접 다운로드 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-136">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="2ee2a-137">확장 및 대부분의 프로덕션 환경에서 성능에 대 한 hello 활용을 hello SQLPackage 유틸리티 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-137">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="2ee2a-138">SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="2ee2a-139">이 예에서는 어떻게 SqlPackage.exe를 사용 하 여 Active Directory 유니버설 인증을 사용한 데이터베이스 a tooexport:</span><span class="sxs-lookup"><span data-stu-id="2ee2a-139">This example shows how tooexport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a><span data-ttu-id="2ee2a-140">SQL Server Management Studio (SSMS)를 사용 하 여 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-140">Export tooa BACPAC file using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="2ee2a-141">hello 한 최신 버전의 SQL Server Management Studio는 또한 마법사 tooexport Azure SQL 데이터베이스 tooa BACPAC 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-141">hello newest versions of SQL Server Management Studio also provide a wizard tooexport an Azure SQL Database tooa BACPAC file.</span></span> <span data-ttu-id="2ee2a-142">Hello 참조 [데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-142">See hello [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span></span>

## <a name="export-tooa-bacpac-file-using-powershell"></a><span data-ttu-id="2ee2a-143">PowerShell을 사용 하 여 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="2ee2a-143">Export tooa BACPAC file using PowerShell</span></span>

<span data-ttu-id="2ee2a-144">사용 하 여 hello [새로 AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit 내보내기 데이터베이스 요청 toohello Azure SQL 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-144">Use hello [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit an export database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="2ee2a-145">데이터베이스의 hello 크기에 따라 hello 내보내기 작업에는 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-145">Depending on hello size of your database, hello export operation may take some time toocomplete.</span></span>

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

<span data-ttu-id="2ee2a-146">hello의 toocheck hello 상태 내보내기 요청, hello를 사용 하 여 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-146">toocheck hello status of hello export request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="2ee2a-147">Hello 후 즉시이 명령을 실행 요청 일반적으로 반환 **상태: InProgress**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-147">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="2ee2a-148">표시 되 면 **상태: 성공** hello 내보내기가 완료 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-148">When you see **Status: Succeeded** hello export is complete.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2ee2a-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ee2a-149">Next steps</span></span>

* <span data-ttu-id="2ee2a-150">toolearn 보관 목적에 대 한 데이터베이스는 대체 tooexported로 Azure SQL 데이터베이스 백업의 백업 장기 보존에 대 한 참조 [장기 백업 보존](sql-database-long-term-retention.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-150">toolearn about long-term backup retention of an Azure SQL database backup as an alternative tooexported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span></span>
- <span data-ttu-id="2ee2a-151">SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-151">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="2ee2a-152">toolearn BACPAC tooa SQL Server 데이터베이스 가져오기에 대 한 참조 [BACPCAC tooa SQL Server 데이터베이스를 가져올](https://msdn.microsoft.com/library/hh710052.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-152">toolearn about importing a BACPAC tooa SQL Server database, see [Import a BACPCAC tooa SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span></span>
* <span data-ttu-id="2ee2a-153">SQL Server 데이터베이스에서 BACPAC 내보내기에 대 한 toolearn 참조 [데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) 및 [첫 번째 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-153">toolearn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span></span>
* <span data-ttu-id="2ee2a-154">SQL 데이터베이스에 궁금할 toomigration tooAzure로 SQL Server에서 내보내는 경우 참조 [SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee2a-154">If you are exporting from SQL Server as a prelude toomigration tooAzure SQL Database, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>
