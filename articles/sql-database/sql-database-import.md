---
title: "aaaImport BACPAC 파일을 Azure SQL 데이터베이스 toocreate | Microsoft Docs"
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
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="383d7-103">가져올 BACPAC 파일 tooa 새 Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="383d7-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="383d7-104">Tooimport 보관에서 데이터베이스를 필요한 시기나 hello 데이터베이스 스키마 및 데이터를 가져올 수를 다른 플랫폼에서 마이그레이션하는 경우는 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="383d7-105">BACPAC 파일이 hello 메타 데이터 및 SQL Server 데이터베이스에서 데이터가 포함 된 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="383d7-106">BACPAC 파일은 Azure Blob Storage(표준 저장소만 해당)에서 또는 온-프레미스 위치의 로컬 저장소에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="383d7-107">toomaximize hello 가져오기 속도 더 높은 서비스 계층과 성능 수준을, P6, 예:를 지정 하 고 hello 가져오기에 성공한 후 적절 하 게 toodown 규모 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="383d7-108">또한 hello 가져오기 후 hello 데이터베이스 호환성 수준 hello 원본 데이터베이스의 호환성 수준을 hello은 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="383d7-109">프로그램 데이터베이스 tooAzure SQL 데이터베이스를 마이그레이션한 후 toooperate hello 데이터베이스의 현재 호환성 수준 (수준 100 hello AdventureWorks2008R2 데이터베이스에 대 한) 또는 더 높은 수준에서 데이터베이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="383d7-110">Hello 의미 및 특정 호환성 수준에서 데이터베이스를 운영 하기 위한 옵션에 대 한 자세한 내용은 참조 하십시오. [ALTER DATABASE 호환성 수준](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="383d7-111">참고 항목 [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) 추가 데이터베이스 수준 설정에 대 한 정보에 대 한 관련 toocompatibility 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="383d7-112">tooimport BACPAC tooa 새 데이터베이스를 먼저 만들어야 합니다 Azure SQL 데이터베이스 논리 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="383d7-113">SQL Server toomigrate tooAzure SQL 데이터베이스를 데이터베이스 방법 보여 주는 자습서 SQLPackage를 사용 하 여 참조 [SQL Server 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="383d7-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="383d7-114">Azure Portal을 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="383d7-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="383d7-115">이 문서에서는 hello를 사용 하 여 Azure blob 저장소에 저장 된 BACPAC 파일에서 Azure SQL 데이터베이스를 만드는 방법을 설명 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="383d7-116">가져오기 hello만 Azure 포털을 사용 하 여 Azure blob 저장소에서 BACPAC 파일을 가져와 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="383d7-117">Azure 포털, 데이터베이스 및 클릭에 대 한 열기 hello 페이지 사용 하 여 데이터베이스 tooimport hello **가져오기** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="383d7-118">Hello 저장소 계정 및 컨테이너를 지정 하 고 원하는 tooimport hello BACPAC 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="383d7-119">Hello 크기 hello 새 데이터베이스를 선택 (일반적으로 hello 동일 원점으로) hello 대상 SQL Server 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![데이터베이스 가져오기](./media/sql-database-import/import.png)

<span data-ttu-id="383d7-121">hello toomonitor hello 진행률 가져오기 작업, hello 논리 서버 데이터베이스가 포함 된 hello 가져올에 대 한 hello 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="383d7-122">너무 아래로 스크롤하여**작업** 클릭 하 고 **가져오기/내보내기** 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="383d7-123">가져오기 작업의 hello 진행률 모니터링</span><span class="sxs-lookup"><span data-stu-id="383d7-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="383d7-124">hello toomonitor hello 진행률 가져오기 작업, 서버에 대 한 hello 논리는 hello에 데이터베이스를 가져오는 중 가져온 hello 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="383d7-125">너무 아래로 스크롤하여**작업** 클릭 하 고 **가져오기/내보내기** 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="383d7-126">![가져오기](./media/sql-database-import/import-history.png) ![가져오기 상태](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="383d7-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="383d7-127">tooverify hello 데이터베이스 라이브 hello 서버에서를 클릭 하 여 **SQL 데이터베이스** hello 새 데이터베이스를 확인 하 고 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="383d7-128">SQLPackage를 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="383d7-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="383d7-129">SQL tooimport hello를 사용 하 여 데이터베이스 [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 명령줄 유틸리티 참조 [속성 및 매개 변수](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="383d7-130">최신 버전의 hello와 함께 제공 hello SQLPackage 유틸리티 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 [Visual Studio 용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx), 하거나 최신 버전의 hello를 다운로드할 수 있습니다 [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello Microsoft에서 직접 다운로드 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="383d7-131">확장 및 대부분의 프로덕션 환경에서 성능에 대 한 hello 활용을 hello SQLPackage 유틸리티 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="383d7-132">SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="383d7-133">다음 스크립트 예제는 방법에 대 한 SQLPackage 명령을 hello 참조 tooimport hello **AdventureWorks2008R2** 로컬 저장소 tooan Azure SQL 데이터베이스 논리 서버를 호출에서 데이터베이스 **mynewserver20170403** 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="383d7-134">이 스크립트에는 hello 라는 새 데이터베이스를 만드는 방법을 보여 줍니다. **myMigratedDatabase**의 서비스 계층으로 **프리미엄**, 및의 서비스 목표 **P6**합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="383d7-135">적절 한 tooyour 환경으로 이러한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage 가져오기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="383d7-137">Azure SQL Database 논리 서버는 포트 1433에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="383d7-138">Tooconnect tooan Azure SQL 데이터베이스 논리 서버에서 회사 방화벽 내에서 시도 하는 경우 있습니다 toosuccessfully 연결을 위해이 포트 hello 회사 방화벽에서 열려 있는 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="383d7-139">이 예에서는 어떻게 SqlPackage.exe를 사용 하 여 Active Directory 유니버설 인증을 사용한 데이터베이스 a tooimport:</span><span class="sxs-lookup"><span data-stu-id="383d7-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="383d7-140">PowerShell을 사용하여 BACPAC 파일에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="383d7-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="383d7-141">사용 하 여 hello [새로 AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit 가져오기 데이터베이스 요청 toohello Azure SQL 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="383d7-142">데이터베이스의 hello 크기에 따라 hello 가져오기 작업에는 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="383d7-143">hello의 toocheck hello 상태 가져오기 요청, hello를 사용 하 여 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="383d7-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="383d7-144">Hello 후 즉시이 명령을 실행 요청 일반적으로 반환 **상태: InProgress**합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="383d7-145">표시 되 면 **상태: 성공** hello 가져오기 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="383d7-146">다른 스크립트 예제는 [BACPAC 파일에서 데이터베이스 가져오기](scripts/sql-database-import-from-bacpac-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383d7-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="383d7-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="383d7-147">Next steps</span></span>
* <span data-ttu-id="383d7-148">toolearn tooconnect tooand 가져온된 SQL 데이터베이스를 쿼리 하는 방법 참조 [샘플 T-SQL 쿼리를 수행 하 고 SQL Server Management Studio를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-ssms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="383d7-149">SQL Server 고객 자문 팀 블로그 마이그레이션에 대 한 BACPAC 파일을 사용 하 여 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="383d7-150">Hello 전체 SQL Server 데이터베이스 마이그레이션 프로세스의 성능 권장 사항을 비롯 한 자세한 내용은 참조 하십시오. [SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="383d7-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



