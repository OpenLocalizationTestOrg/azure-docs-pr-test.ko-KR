---
title: "Azure SQL Database를 BACPAC 파일로 내보내기 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure SQL Database를 BACPAC 파일로 내보내기"
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
ms.openlocfilehash: faa567ec615a07da8633629fc98e3454c84a8f5f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="export-an-azure-sql-database-to-a-bacpac-file"></a><span data-ttu-id="73478-103">Azure SQL Database를 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="73478-103">Export an Azure SQL database to a BACPAC file</span></span>

<span data-ttu-id="73478-104">다른 플랫폼에 보관하거나 이동하기 위해 데이터베이스를 내보내야 할 경우 데이터베이스 스키마 및 데이터를 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 파일로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-104">When you need to export a database for archiving or for moving to another platform, you can export the database schema and data to a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="73478-105">BACPAC 파일은 메타데이터 및 SQL Server 데이터베이스의 데이터를 포함하는 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73478-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="73478-106">BACPAC 파일은 Azure Blob Storage 또는 온-프레미스 저장소의 로컬 저장소에 저장할 수 있으며 나중에 Azure SQL Database 또는 SQL Server 온-프레미스 설치로 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-106">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="73478-107">Azure SQL Database 자동화된 내보내기는 2017년 3월 1일에 사용이 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-107">Azure SQL Database Automated Export was retired on March 1, 2017.</span></span> <span data-ttu-id="73478-108">[장기 백업 보존](sql-database-long-term-retention.md
) 또는 [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md)을 사용하여 선택한 일정에 따라 PowerShell을 사용해 주기적으로 SQL Database를 보관할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-108">You can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to periodically archive SQL databases using PowerShell according to a schedule of your choice.</span></span> <span data-ttu-id="73478-109">샘플의 경우 GitHub에서 [샘플 PowerShell 스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-109">For a sample, download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a><span data-ttu-id="73478-110">Azure SQL Database를 내보낼 경우 고려 사항</span><span class="sxs-lookup"><span data-stu-id="73478-110">Considerations when exporting an Azure SQL database</span></span>

* <span data-ttu-id="73478-111">내보내기 작업에서 트랜잭션이 일치하도록 내보내기 중에나 Azure SQL Database의 [트랜잭션 일치 복사본](sql-database-copy.md)에서 내보내는 중에는 쓰기 활동이 발생하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-111">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span></span>
* <span data-ttu-id="73478-112">Blob Storage로 내보내는 경우 BACPAC 파일의 최대 크기는 200GB입니다.</span><span class="sxs-lookup"><span data-stu-id="73478-112">If you are exporting to blob storage, the maximum size of a BACPAC file is 200 GB.</span></span> <span data-ttu-id="73478-113">더 큰 BACPAC 파일을 보관하려면 로컬 저장소로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="73478-113">To archive a larger BACPAC file, export to local storage.</span></span>
* <span data-ttu-id="73478-114">이 문서에서 설명하는 방법을 사용하여 Azure Premium Storage에서 BACPAC 파일을 내보낼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-114">Exporting a BACPAC file to Azure premium storage using the methods discussed in this article is not supported.</span></span>
* <span data-ttu-id="73478-115">Azure SQL Database에서 내보내기 작업이 20시간을 초과하면 취소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-115">If the export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span></span> <span data-ttu-id="73478-116">내보내는 중에 성능을 향상시키기 위해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-116">To increase performance during export, you can:</span></span>
  * <span data-ttu-id="73478-117">서비스 수준을 일시적으로 높이기</span><span class="sxs-lookup"><span data-stu-id="73478-117">Temporarily increase your service level.</span></span>
  * <span data-ttu-id="73478-118">내보내기 중에 모든 읽기 및 쓰기 작업 중단</span><span class="sxs-lookup"><span data-stu-id="73478-118">Cease all read and write activity during the export.</span></span>
  * <span data-ttu-id="73478-119">모든 대형 테이블에 null이 아닌 값의 [클러스터형 인덱스](https://msdn.microsoft.com/library/ms190457.aspx) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-119">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span></span> <span data-ttu-id="73478-120">클러스터형 인덱스가 없는 경우 6~12시간 이상 소요되면 내보내기에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-120">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span></span> <span data-ttu-id="73478-121">전체 테이블 내보내기를 시도하려면 내보내기 서비스에서 테이블 스캔을 완료해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="73478-121">This is because the export service needs to complete a table scan to try to export entire table.</span></span> <span data-ttu-id="73478-122">테이블이 내보내기에 최적화되었는지 확인하는 좋은 방법은 **DBCC SHOW_STATISTICS**를 실행하고 *RANGE_HI_KEY*가 null이 아닌지와 해당 값이 잘 배포되어 있는지 검토하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="73478-122">A good way to determine if your tables are optimized for export is to run **DBCC SHOW_STATISTICS** and make sure that the *RANGE_HI_KEY* is not null and its value has good distribution.</span></span> <span data-ttu-id="73478-123">자세한 내용은 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-123">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="73478-124">BACPAC는 백업에 사용되는 목적이 아니며 작업을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-124">BACPACs are not intended to be used for backup and restore operations.</span></span> <span data-ttu-id="73478-125">Azure SQL Database에서는 모든 사용자 데이터베이스의 백업이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="73478-125">Azure SQL Database automatically creates backups for every user database.</span></span> <span data-ttu-id="73478-126">자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md) 및 [SQL Database 백업](sql-database-automated-backups.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-126">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span></span>  
> 

## <a name="export-to-a-bacpac-file-using-the-azure-portal"></a><span data-ttu-id="73478-127">Azure Portal을 사용하여 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="73478-127">Export to a BACPAC file using the Azure portal</span></span>

<span data-ttu-id="73478-128">[Azure Portal](https://portal.azure.com)을 사용하여 데이터베이스를 내보내려면 데이터베이스에 대한 페이지를 열고 도구 모음에서 **내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-128">To export a database using the [Azure portal](https://portal.azure.com), open the page for your database and click **Export** on the toolbar.</span></span> <span data-ttu-id="73478-129">BACPAC 파일 이름을 지정하고, 내보내기에 필요한 Azure Storage 계정 및 컨테이너를 제공하고, 원본 데이터베이스에 연결할 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-129">Specify the BACPAC filename, provide the Azure storage account and container for the export, and provide the credentials to connect to the source database.</span></span>  

![데이터베이스 내보내기](./media/sql-database-export/database-export.png)

<span data-ttu-id="73478-131">내보내기 작업의 진행률을 모니터링하려면 내보낼 데이터베이스가 포함된 논리 서버에 대한 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73478-131">To monitor the progress of the export operation, open the page for the logical server containing the database being exported.</span></span> <span data-ttu-id="73478-132">아래로 **작업**이 나올 때까지 스크롤한 다음 **가져오기/내보내기** 기록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-132">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

<span data-ttu-id="73478-133">![내보내기 기록](./media/sql-database-export/export-history.png)
![내보내기 기록 상태](./media/sql-database-export/export-history2.png)</span><span class="sxs-lookup"><span data-stu-id="73478-133">![export history](./media/sql-database-export/export-history.png)
![export history status](./media/sql-database-export/export-history2.png)</span></span>

## <a name="export-to-a-bacpac-file-using-the-sqlpackage-utility"></a><span data-ttu-id="73478-134">SQLPackage 유틸리티를 사용하여 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="73478-134">Export to a BACPAC file using the SQLPackage utility</span></span>

<span data-ttu-id="73478-135">[SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 명령줄 유틸리티를 사용하여 SQL Database를 내보내려면 [매개 변수 및 속성 내보내기](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-135">To export a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span></span> <span data-ttu-id="73478-136">SQLPackage 유틸리티는 최신 버전의 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 [Visual Studio용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)가 함께 제공되며, Microsoft 다운로드 센터에서 직접 최신 버전의 [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-136">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="73478-137">대부분의 프로덕션 환경에서 규모 및 성능에 SQLPackage 유틸리티를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-137">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="73478-138">BACPAC 파일을 사용하는 마이그레이션에 관한 SQL Server 고객 자문 팀 블로그는 [BACPAC 파일을 사용하여 SQL Server에서 Azure SQL Database로 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="73478-139">이 예제는 Active Directory 유니버설 인증으로 SqlPackage.exe를 사용하여 데이터베이스를 내보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="73478-139">This example shows how to export a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-to-a-bacpac-file-using-sql-server-management-studio-ssms"></a><span data-ttu-id="73478-140">SSMS(SQL Server Management Studio)를 사용하여 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="73478-140">Export to a BACPAC file using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="73478-141">또한 최신 버전의 SQL Server Management Studio에서는 Azure SQL Database를 BACPAC 파일로 내보내기 위한 마법사도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-141">The newest versions of SQL Server Management Studio also provide a wizard to export an Azure SQL Database to a BACPAC file.</span></span> <span data-ttu-id="73478-142">[데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-142">See the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span></span>

## <a name="export-to-a-bacpac-file-using-powershell"></a><span data-ttu-id="73478-143">PowerShell을 사용하여 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="73478-143">Export to a BACPAC file using PowerShell</span></span>

<span data-ttu-id="73478-144">[New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet을 사용하여 Azure SQL Database 서비스에 데이터베이스 내보내기 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-144">Use the [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet to submit an export database request to the Azure SQL Database service.</span></span> <span data-ttu-id="73478-145">데이터베이스 크기에 따라 내보내기 작업을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73478-145">Depending on the size of your database, the export operation may take some time to complete.</span></span>

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

<span data-ttu-id="73478-146">내보내기 요청의 상태를 확인하려면 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73478-146">To check the status of the export request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="73478-147">이 요청 직후에 이 명령을 실행하면 **Status: InProgress**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="73478-147">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="73478-148">**Status : Succeeded**가 표시되면 내보내기가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="73478-148">When you see **Status: Succeeded** the export is complete.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="73478-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73478-149">Next steps</span></span>

* <span data-ttu-id="73478-150">보관을 위해 데이터베이스를 내보내는 방법의 대안으로 사용되는 Azure SQL Database 백업의 장기 백업 보존에 대해 알아보려면 [장기 백업 보존](sql-database-long-term-retention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-150">To learn about long-term backup retention of an Azure SQL database backup as an alternative to exported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span></span>
- <span data-ttu-id="73478-151">BACPAC 파일을 사용하는 마이그레이션에 관한 SQL Server 고객 자문 팀 블로그는 [BACPAC 파일을 사용하여 SQL Server에서 Azure SQL Database로 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-151">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="73478-152">SQL Server Database에 BACPAC를 가져오는 방법에 대해 자세히 알아보려면 [SQL Server Database로 BACPCAC 가져오기](https://msdn.microsoft.com/library/hh710052.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-152">To learn about importing a BACPAC to a SQL Server database, see [Import a BACPCAC to a SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span></span>
* <span data-ttu-id="73478-153">SQL Server Database에서 BACPAC를 내보내는 방법을 알아보려면 [데이터 계층 응용 프로그램 내보내기](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) 및 [첫 번째 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-153">To learn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span></span>
* <span data-ttu-id="73478-154">마이그레이션에 대한 사전 준비로 SQL Server에서 Azure SQL Database로 내보내는 경우 [Azure SQL Database에 SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73478-154">If you are exporting from SQL Server as a prelude to migration to Azure SQL Database, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>
