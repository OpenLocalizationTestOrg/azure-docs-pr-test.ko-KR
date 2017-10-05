---
title: "BACPAC 파일을 가져와 Azure SQL 데이터베이스 만들기 | Microsoft Docs"
description: "BACPAC 파일을 가져와 새 Azure SQL 데이터베이스를 만듭니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="70950-103">새 Azure SQL Database로 BACPAC 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="70950-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="70950-104">아카이브에서 데이터베이스를 가져오거나 다른 플랫폼에서 마이그레이션하는 경우 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 파일에서 데이터베이스 스키마 및 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="70950-105">BACPAC 파일은 메타데이터 및 SQL Server 데이터베이스의 데이터를 포함하는 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="70950-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="70950-106">BACPAC 파일은 Azure Blob Storage(표준 저장소만 해당)에서 또는 온-프레미스 위치의 로컬 저장소에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="70950-107">가져오기 속도를 최대화하려면 P6처럼 더 높은 서비스 계층과 성능 수준을 지정한 다음 가져오기가 성공하면 적절하게 규모 감축하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="70950-108">또한 가져오기 후의 데이터베이스 호환성 수준은 원본 데이터베이스의 호환성 수준에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70950-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="70950-109">Azure SQL Database로 데이터베이스를 마이그레이션한 후에는 데이터베이스를 현재 호환성 수준에서(AdventureWorks2008R2 데이터베이스에 대해 수준 100) 또는 더 높은 수준에서 작동하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="70950-110">특정 호환성 수준에서 데이터베이스를 운영하기 위한 옵션 및 그 영향에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="70950-111">또한 호환성 수준과 관련된 추가 데이터베이스 수준 설정에 대한 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="70950-112">새 데이터베이스로 BACPAC을 가져오려면 먼저 Azure SQL Database 논리 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="70950-113">SQLPackage를 사용하여 Azure SQL Database로 SQL Server 데이터베이스를 마이그레이션하는 방법을 보여주는 자습서는 [SQL Server 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="70950-114">Azure Portal을 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="70950-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="70950-115">이 문서에서는 [Azure Portal](https://portal.azure.com)을 사용하여 Azure Blob Storage에 저장된 BACPAC 파일로 Azure SQL Database를 만드는 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="70950-116">Azure Portal을 사용하여 가져오기는 Azure Blob Storage에서 BACPAC 파일을 가져오는 것만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="70950-117">Azure Portal을 사용하여 가져오려면 해당 데이터베이스의 페이지를 열고 도구 모음에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="70950-118">저장소 계정 및 컨테이너를 지정하고 가져올 BACPAC 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="70950-119">새 데이터베이스의 크기(일반적으로 원본과 동일)를 선택하고 대상 SQL Server 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![데이터베이스 가져오기](./media/sql-database-import/import.png)

<span data-ttu-id="70950-121">가져오기 작업의 진행률을 모니터링하려면 가져올 데이터베이스가 포함된 논리 서버에 대한 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70950-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="70950-122">아래로 **작업**이 나올 때까지 스크롤한 다음 **가져오기/내보내기** 기록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="70950-123">가져오기 작업의 진행률 모니터링</span><span class="sxs-lookup"><span data-stu-id="70950-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="70950-124">가져오기 작업의 진행률을 모니터링하려면 가져올 데이터베이스에 논리 서버의 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70950-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="70950-125">아래로 **작업**이 나올 때까지 스크롤한 다음 **가져오기/내보내기** 기록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="70950-126">![가져오기](./media/sql-database-import/import-history.png) ![가져오기 상태](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="70950-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="70950-127">데이터베이스가 서버에서 라이브 상태인지 확인하려면 **SQL 데이터베이스**를 클릭하고 새 데이터베이스를 **온라인** 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="70950-128">SQLPackage를 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="70950-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="70950-129">[SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 명령줄 유틸리티를 사용하여 SQL 데이터베이스를 가져오려면 [매개 변수 및 속성 가져오기](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="70950-130">SQLPackage 유틸리티는 최신 버전의 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 [Visual Studio용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)가 함께 제공되며, Microsoft 다운로드 센터에서 직접 최신 버전의 [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="70950-131">대부분의 프로덕션 환경에서 규모 및 성능에 SQLPackage 유틸리티를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="70950-132">BACPAC 파일을 사용하는 마이그레이션에 관한 SQL Server 고객 자문 팀 블로그는 [BACPAC 파일을 사용하여 SQL Server에서 Azure SQL Database로 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="70950-133">로컬 저장소에서 Azure SQL Database 논리 서버(이 예에서는 **mynewserver20170403**)로 **AdventureWorks2008R2** 데이터베이스를 가져오는 방법에 대한 스크립트 예제는 다음 SQLPackage 명령을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="70950-134">이 스크립트는 이름이 **myMigratedDatabase**이고, 서비스 계층이 **프리미엄**이고, 서비스 목표가 **P6**인 새 데이터베이스를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70950-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="70950-135">각자 환경에 맞게 적절한 값으로 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70950-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage 가져오기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="70950-137">Azure SQL Database 논리 서버는 포트 1433에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="70950-138">회사 방화벽 내에서 Azure SQL Database 논리 서버로 연결을 시도하면 성공적인 연결을 위해 회사 방화벽에서 이 포트가 열려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="70950-139">이 예제는 Active Directory 유니버설 인증으로 SqlPackage.exe를 사용하여 데이터베이스를 가져오는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70950-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="70950-140">PowerShell을 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="70950-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="70950-141">[New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet을 사용하여 Azure SQL Database 서비스에 데이터베이스 가져오기 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="70950-142">데이터베이스 크기에 따라 가져오기 작업을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70950-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="70950-143">가져오기 요청의 상태를 확인하려면 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70950-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="70950-144">요청 직후에 이 명령을 실행하면 **Status: InProgress**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="70950-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="70950-145">**Status: Succeeded**가 표시되면 가져오기가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70950-145">When you see **Status: Succeeded** the import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="70950-146">다른 스크립트 예제는 [BACPAC 파일에서 데이터베이스 가져오기](scripts/sql-database-import-from-bacpac-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70950-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70950-147">Next steps</span></span>
* <span data-ttu-id="70950-148">가져온 SQL 데이터베이스에 연결하고 쿼리하는 방법을 알아보려면 [SQL Server Management Studio를 사용하여 SQL 데이터베이스에 연결하고 샘플 T-SQL 쿼리 수행](sql-database-connect-query-ssms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="70950-149">BACPAC 파일을 사용한 마이그레이션에 관한 SQL Server 고객 자문 팀 블로그는 [BACPAC 파일을 사용하여 SQL Server에서 Azure SQL Database로 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="70950-150">성능 권장 사항을 비롯한 전체 SQL Server 데이터베이스 마이그레이션 프로세스에 대한 설명은 [Azure SQL Database에 SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70950-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



