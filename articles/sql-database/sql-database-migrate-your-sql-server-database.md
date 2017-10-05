---
title: "SQL Server DB를 Azure SQL Database로 마이그레이션 | Microsoft Docs"
description: "SQL Server 데이터베이스를 Azure SQL Database로 마이그레이션하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: 375d3ea0230e7d3fd0fc02ca7e0b8a7a76c24a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a><span data-ttu-id="e0a9b-103">SQL Server 데이터베이스를 Azure SQL Database로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e0a9b-103">Migrate your SQL Server database to Azure SQL Database</span></span>

<span data-ttu-id="e0a9b-104">SQL Server 데이터베이스를 Azure SQL Database로 옮기는 과정은 먼저 데이터베이스를 준비하고, 내보내고 나서, 가져오는 세 부분의 프로세스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-104">Moving your SQL Server database to Azure SQL Database is a three part process - you first prepare, then export, and then import the database.</span></span> <span data-ttu-id="e0a9b-105">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-105">In this tutorial, you learn to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0a9b-106">DMA([Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595))를 사용하여 Azure SQL Database로의 마이그레이션을 위해 SQL Server에서 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="e0a9b-106">Prepare a database in a SQL Server for migration to Azure SQL Database using the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span></span>
> * <span data-ttu-id="e0a9b-107">데이터베이스를 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-107">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="e0a9b-108">BACPAC 파일을 Azure SQL Database로 가져오기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-108">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="e0a9b-109">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0a9b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0a9b-110">Prerequisites</span></span>

<span data-ttu-id="e0a9b-111">이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-111">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="e0a9b-112">SSMS([SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms))의 최신 버전을 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-112">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="e0a9b-113">SSMS를 설치하면 다양한 데이터베이스 개발 작업을 자동화하는 데 사용할 수 있는 명령줄 유틸리티인 SQLPackage의 최신 버전도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-113">Installing SSMS also installs the newest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span> 
- <span data-ttu-id="e0a9b-114">DMA([Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595))를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-114">Installed the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="e0a9b-115">마이그레이션할 데이터베이스를 식별했고 이에 대한 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-115">You have identified and have access to a database to migrate.</span></span> <span data-ttu-id="e0a9b-116">이 자습서에서는 SQL Server 2008R2 이상의 인스턴스에서 [SQL Server 2008R2 AdventureWorks OLTP 데이터베이스](https://msftdbprodsamples.codeplex.com/releases/view/59211)를 사용하지만 사용자가 선택한 모든 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-116">This tutorial uses the [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> <span data-ttu-id="e0a9b-117">호환성 문제를 해결하려면 [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-117">To fix compatibility issues, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span></span>

## <a name="prepare-for-migration"></a><span data-ttu-id="e0a9b-118">마이그레이션 준비</span><span class="sxs-lookup"><span data-stu-id="e0a9b-118">Prepare for migration</span></span>

<span data-ttu-id="e0a9b-119">마이그레이션할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-119">You are ready to prepare for migration.</span></span> <span data-ttu-id="e0a9b-120">**[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)**를 사용하여 Azure SQL Database에 마이그레이션하기 위한 데이터베이스의 준비 상태를 평가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-120">Follow these steps to use the **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** to assess the readiness of your database for migration to Azure SQL Database.</span></span>

1. <span data-ttu-id="e0a9b-121">**Data Migration Assistant**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-121">Open the **Data Migration Assistant**.</span></span> <span data-ttu-id="e0a9b-122">마이그레이션하려는 데이터베이스가 포함된 SQL Server 인스턴스에 연결된 모든 컴퓨터에서 DMA를 실행할 수 있으며 SQL Server 인스턴스를 호스트하는 컴퓨터에는 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-122">You can run DMA on any computer with connectivity to the SQL Server instance containing the database that you plan to migrate, you do not need to install it on the computer hosting the SQL Server instance.</span></span>

     ![Data Migration Assistant 열기](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="e0a9b-124">왼쪽 메뉴에서 **+ 새로 만들기**를 클릭하여 **평가** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-124">In the left-hand menu, click **+ New** to create an **Assessment** project.</span></span> <span data-ttu-id="e0a9b-125">양식에 **프로젝트 이름**을 입력하고(다른 값은 모두 기본값으로 유지) **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-125">Fill in the form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="e0a9b-126">**옵션** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-126">The **Options** page opens.</span></span>

     ![새 Data Migration Assistant 프로젝트](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="e0a9b-128">**옵션** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-128">On the **Options** page, click **Next**.</span></span> <span data-ttu-id="e0a9b-129">**Select sources**(소스 선택) 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-129">The **Select sources** page opens.</span></span>

     ![새 데이터 마이그레이션 옵션](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="e0a9b-131">**Select sources**(소스 선택) 페이지에서 마이그레이션할 서버가 포함된 SQL Server 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-131">On the **Select sources** page, enter the name of SQL Server instance containing the server you plan to migrate.</span></span> <span data-ttu-id="e0a9b-132">필요한 경우 이 페이지에서 다른 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-132">Change the other values on this page if necessary.</span></span> <span data-ttu-id="e0a9b-133">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-133">Click **Connect**.</span></span>

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="e0a9b-135">**Select sources**(소스 선택) 페이지의 **Add sources**(소스 추가) 부분에서 호환성을 테스트할 데이터베이스의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-135">In the **Add sources** portion of the **Select sources** page, select the checkboxes for the databases to be tested for compatibility.</span></span> <span data-ttu-id="e0a9b-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-136">Click **Add**.</span></span>

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="e0a9b-138">**Start Assessment**(평가 시작)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-138">Click **Start Assessment**.</span></span>

     ![새 데이터 마이그레이션 평가 시작](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="e0a9b-140">평가가 완료되면 먼저 데이터베이스가 마이그레이션하는 데 충분히 호환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-140">When the assessment completes, first look to see if the database is sufficiently compatible to migrate.</span></span> <span data-ttu-id="e0a9b-141">녹색 원에 있는 확인 표시를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-141">Look for the checkmark in a green circle.</span></span>

     ![새 데이터 마이그레이션 호환 평가 결과](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="e0a9b-143">결과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-143">Review the results.</span></span> <span data-ttu-id="e0a9b-144">표시된 **SQL Server 기능 패리티** 결과를 기본적으로 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-144">The **SQL Server feature parity** results shown are the default results to review.</span></span> <span data-ttu-id="e0a9b-145">특히 지원되지 않는 기능, 부분적으로 지원되는 기능 및 권장 작업에 대해 제공된 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-145">Specifically review the information about unsupported and partially supported features, and the provided information about recommended actions.</span></span> 

     ![새 데이터 마이그레이션 평가 패리티](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="e0a9b-147">왼쪽 위에서 해당 옵션을 클릭하여 **호환성 문제**를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-147">Review the **Compatibility issues** by clicking that option in the upper left.</span></span> <span data-ttu-id="e0a9b-148">특히 마이그레이션 차단, 동작 변경 내용 및 각 호환성 수준에 대해 사용되지 않는 기능에 대한 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-148">Specifically review the information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="e0a9b-149">AdventureWorks2008R2 데이터베이스의 경우 SQL Server 2008 이후 전체 텍스트 검색의 변경 내용 및 SQL Server 2000 이후 SERVERPROPERTY('LCID')의 변경 내용을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-149">For the AdventureWorks2008R2 database, review the changes to Full-Text Search since SQL Server 2008 and the changes to SERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="e0a9b-150">이러한 변경 사항의 자세한 내용에 대한 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-150">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="e0a9b-151">변경된 다양한 검색 옵션 및 전체 텍스트 검색에 대한 설정</span><span class="sxs-lookup"><span data-stu-id="e0a9b-151">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="e0a9b-152">Azure SQL Database에 데이터베이스를 마이그레이션한 후에 데이터베이스의 현재 호환성 수준(AdventureWorks2008R2 데이터베이스의 경우 100 수준) 또는 더 높은 수준에서 작동하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-152">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="e0a9b-153">특정 호환성 수준에서 데이터베이스를 운영하기 위한 옵션 및 그 영향에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-153">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="e0a9b-154">또한 호환성 수준과 관련된 추가 데이터베이스 수준 설정에 대한 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-154">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>
   >

10. <span data-ttu-id="e0a9b-155">필요에 따라 JSON 파일로 보고서를 저장하려면 **보고서 내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-155">Optionally, click **Export report** to save the report as a JSON file.</span></span>
11. <span data-ttu-id="e0a9b-156">Data Migration Assistant를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-156">Close the Data Migration Assistant.</span></span>

## <a name="export-to-bacpac-file"></a><span data-ttu-id="e0a9b-157">BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-157">Export to BACPAC file</span></span> 

<span data-ttu-id="e0a9b-158">BACPAC 파일은 메타데이터 및 SQL Server 데이터베이스의 데이터를 포함하는 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-158">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="e0a9b-159">BACPAC 파일은 보관이나 마이그레이션(예: SQL Server에서 Azure SQL Database로)을 위해 Azure Blob Storage 또는 로컬 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-159">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server to Azure SQL Database.</span></span> <span data-ttu-id="e0a9b-160">트랜잭션 측면에서 일관되도록 내보내려는 경우 내보내기 중에 쓰기 작업이 발생하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-160">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export.</span></span>

<span data-ttu-id="e0a9b-161">SQLPackage 명령줄 유틸리티를 사용하여 로컬 저장소로 AdventureWorks2008R2 데이터베이스를 내보내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-161">Follow these steps to use the SQLPackage command-line utility to export the AdventureWorks2008R2 database to local storage.</span></span>

1. <span data-ttu-id="e0a9b-162">Windows 명령 프롬프트를 열고 디렉터리를 **130** 버전의 SQLPackage가 있는 폴더(예: **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-162">Open a Windows command prompt and change your directory to a folder in which you have the **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="e0a9b-163">명령 프롬프트에서 다음 SQLPackage 명령을 실행하여 **localhost**의 **AdventureWorks2008R2** 데이터베이스를 **AdventureWorks2008R2.bacpac**로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-163">Execute the following SQLPackage command at the command prompt to export the **AdventureWorks2008R2** database from **localhost** to **AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="e0a9b-164">이러한 값을 사용자 환경에 맞는 적절한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-164">Change any of these values as appropriate to your environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 내보내기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="e0a9b-166">실행이 완료되면 생성된 BACPAC 파일이 sqlpackage 실행 파일이 있는 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-166">Once the execution is complete the generated BACPAC file is stored in the directory where the sqlpackage executable is located.</span></span> <span data-ttu-id="e0a9b-167">이 예제에서는 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-167">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="e0a9b-168">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="e0a9b-168">Log in to the Azure portal</span></span>

<span data-ttu-id="e0a9b-169">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-169">Log in to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e0a9b-170">SQLPackage 명령줄 유틸리티를 실행하고 있는 컴퓨터에서 로그온하면 5단계의 방화벽 규칙 만들기가 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-170">Logging on from the computer from which you are running the SQLPackage command-line utility eases the creation of the firewall rule in step 5.</span></span>

## <a name="create-a-sql-server-logical-server"></a><span data-ttu-id="e0a9b-171">SQL Server 논리 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-171">Create a SQL server logical server</span></span>

<span data-ttu-id="e0a9b-172">[SQL Server 논리 서버](sql-database-features.md)는 여러 데이터베이스에 대한 중앙 관리 지점의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-172">A [SQL server logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="e0a9b-173">마이그레이션된 Adventure Works OLTP SQL Server 데이터베이스를 포함하도록 SQL Server 논리 서버를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-173">Follow these steps to create a SQL server logical server to contain the migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="e0a9b-174">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-174">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="e0a9b-175">**새로 만들기** 페이지에서 검색 창에 **sql server**를 입력하고 필터링된 목록에서 **SQL Database(논리 서버)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-175">Type **sql server** in the search window on the **New** page, and select **SQL database (logical server)** from the filtered list.</span></span>

    ![논리 서버 선택](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="e0a9b-177">**모두** 페이지에서 **SQL server(논리 서버)**를 클릭한 다음 **SQL Server(논리 서버)** 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-177">On the **Everything** page, click **SQL server (logical server)** and then click **Create** on the **SQL Server (logical server)** page.</span></span>

    ![논리 서버 만들기](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="e0a9b-179">위의 이미지에 표시된 대로 다음과 같은 정보를 사용하여 SQL Server(논리 서버) 형식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-179">Fill out the SQL server (logical server) form with the following information, as shown on the preceding image:</span></span>     

   | <span data-ttu-id="e0a9b-180">설정</span><span class="sxs-lookup"><span data-stu-id="e0a9b-180">Setting</span></span>       | <span data-ttu-id="e0a9b-181">제안 값</span><span class="sxs-lookup"><span data-stu-id="e0a9b-181">Suggested value</span></span> | <span data-ttu-id="e0a9b-182">설명</span><span class="sxs-lookup"><span data-stu-id="e0a9b-182">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="e0a9b-183">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-183">**Server name**</span></span> | <span data-ttu-id="e0a9b-184">전역적으로 고유한 이름 입력</span><span class="sxs-lookup"><span data-stu-id="e0a9b-184">Enter any globally unique name</span></span> | <span data-ttu-id="e0a9b-185">유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-185">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="e0a9b-186">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-186">**Server admin login**</span></span> | <span data-ttu-id="e0a9b-187">유효한 이름 입력</span><span class="sxs-lookup"><span data-stu-id="e0a9b-187">Enter any valid name</span></span> | <span data-ttu-id="e0a9b-188">유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-188">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="e0a9b-189">**암호**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-189">**Password**</span></span> | <span data-ttu-id="e0a9b-190">유효한 암호 입력</span><span class="sxs-lookup"><span data-stu-id="e0a9b-190">Enter any valid password</span></span> | <span data-ttu-id="e0a9b-191">암호는 8자 이상이어야 하며 대문자, 소문자, 숫자 및 영숫자가 아닌 문자 범주 중 세 가지 범주의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-191">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="e0a9b-192">**구독**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-192">**Subscription**</span></span> | <span data-ttu-id="e0a9b-193">구독 선택</span><span class="sxs-lookup"><span data-stu-id="e0a9b-193">Select a subscription</span></span> | <span data-ttu-id="e0a9b-194">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-194">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="e0a9b-195">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-195">**Resource group**</span></span> | <span data-ttu-id="e0a9b-196">기존 리소스 그룹을 선택하거나 새 그룹을 만듭니다(예: **myResourceGroup**).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-196">Choose an existing resource group or create a new group, such as **myResourceGroup**</span></span> |  <span data-ttu-id="e0a9b-197">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-197">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="e0a9b-198">**위치**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-198">**Location**</span></span> | <span data-ttu-id="e0a9b-199">새 서버의 유효한 위치 입력</span><span class="sxs-lookup"><span data-stu-id="e0a9b-199">Enter any valid location for the new server</span></span> | <span data-ttu-id="e0a9b-200">지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-200">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![논리 서버 만들기 양식 완료](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="e0a9b-202">**만들기**를 클릭하여 논리 서버를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-202">Click **Create** to provision the logical server.</span></span> <span data-ttu-id="e0a9b-203">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-203">Provisioning takes a few minutes.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e0a9b-204">서버 이름, 서버 관리자 로그인 이름 및 암호를 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-204">Remember your server name, server admin login name, and password.</span></span> <span data-ttu-id="e0a9b-205">이 자습서의 뒷부분에서 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-205">You need these values later in this tutorial.</span></span>
>

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="e0a9b-206">서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-206">Create a server-level firewall rule</span></span>

<span data-ttu-id="e0a9b-207">방화벽 규칙을 만들어서 특정 IP 주소에 대한 방화벽을 열지 않으면 SQL Database 서비스는 외부 응용 프로그램 및 도구가 서버 또는 서버의 데이터베이스에 연결되지 않도록 방지하는 [서버 수준에 방화벽](sql-database-firewall-configure.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-207">The SQL Database service creates a [firewall at the server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="e0a9b-208">SQLPackage 명령줄 유틸리티를 실행하는 컴퓨터의 IP 주소에 대한 SQL Database 서버 수준 방화벽 규칙을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-208">Follow these steps to create a SQL Database server-level firewall rule for the IP address of the computer from which you are running the SQLPackage command-line utility.</span></span> <span data-ttu-id="e0a9b-209">이렇게 하면 SQLPackage를 Azure SQL Database 방화벽을 통해 SQL Server 데이터베이스 논리 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-209">This enables SQLPackage to connect to the SQL serverDatabase logical server through the Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="e0a9b-210">왼쪽 메뉴에서 **모든 리소스**를 클릭하고 **모든 리소스** 페이지에서 새 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-210">Click **All resources** from the left-hand menu and click your new server on the **All resources** page.</span></span> <span data-ttu-id="e0a9b-211">서버에 대한 개요 페이지가 열리고 추가 구성을 위한 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-211">The overview page for your server opens and provides options for further configuration.</span></span>

     ![논리 서버 개요](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="e0a9b-213">개요 페이지의 왼쪽 메뉴에서 **설정** 아래 **방화벽**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-213">Click **Firewall** in the left-hand menu under **Settings** on the overview page.</span></span> <span data-ttu-id="e0a9b-214">SQL Database 서버에 대한 **방화벽 설정** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-214">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="e0a9b-215">도구 모음에서 **클라이언트 IP 추가**를 클릭하여 현재 사용 중인 컴퓨터의 IP 주소를 추가한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-215">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="e0a9b-216">이 IP 주소에 대한 서버 수준 방화벽 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-216">A server-level firewall rule is created for this IP address.</span></span>

     ![set server firewall rule](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="e0a9b-218">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-218">Click **OK**.</span></span>

<span data-ttu-id="e0a9b-219">이제 SQL Server Management Studio 또는 이전에 만든 서버 관리자 계정을 사용하여 이 IP 주소에서 원하는 다른 도구를 사용하여 모든 데이터베이스 및 이 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-219">You can now connect to all databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="e0a9b-220">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-220">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="e0a9b-221">회사 네트워크 내에서 연결을 시도하는 경우 포트 1433을 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-221">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="e0a9b-222">이 경우 IT 부서에서 포트 1433을 열지 않으면 Azure SQL Database 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-222">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="import-a-bacpac-file-to-azure-sql-database"></a><span data-ttu-id="e0a9b-223">Azure SQL Database에 BACPAC 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-223">Import a BACPAC file to Azure SQL Database</span></span> 

<span data-ttu-id="e0a9b-224">최신 버전의 SQLPackage 명령줄 유틸리티를 사용하면 지정한 [서비스 계층 및 성능 수준](sql-database-service-tiers.md)에서 Azure SQL Database를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-224">The newest versions of the SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="e0a9b-225">가져오기 작업 동안 최상의 성능을 위해 높은 서비스 계층 및 성능 수준을 선택한 다음 서비스 계층 및 성능 수준이 즉시 필요한 것보다 높은 경우 가져오기 작업 후에 규모를 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-225">For best performance during import, select a high service tier and performance level and then scale down after import if the service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="e0a9b-226">SQLPackage 명령줄 유틸리티를 사용하여 Azure SQL Database에 AdventureWorks2008R2 데이터베이스를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-226">Follow these steps use the SQLPackage command-line utility to import the AdventureWorks2008R2 database to Azure SQL Database.</span></span> <span data-ttu-id="e0a9b-227">이 작업에 SQL Server Management Studio를 사용할 수 있지만 SQLPackage가 대부분의 프로덕션 환경에서 유연성을 극대화하고 성능을 최적화할 수 있는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-227">While you can use SQL Server Management Studio for this task, SQLPackage is the preferred method for most production environments for maximum flexibility and best performance.</span></span> <span data-ttu-id="e0a9b-228">[Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)(BACPAC 파일을 사용하여 SQL Server에서 Azure SQL Database로 마이그레이션)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-228">See [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

- <span data-ttu-id="e0a9b-229">로컬 저장소의 **AdventureWorks2008R2** 데이터베이스를 이전에 만든 SQL Server 논리 서버에 대한 로컬 저장소에서 서비스 계층이 **Premium**이고 서비스 목표가 **P6**인 새 데이터베이스로 가져오려면 명령 프롬프트에서 다음 SQLPackage 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-229">Execute the following SQLPackage command at the command prompt to import the **AdventureWorks2008R2** database from local storage to the SQL server logical server that you previously created to a new database, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="e0a9b-230">꺽쇠 괄호 안의 값을 SQL Server 논리 서버에 대한 적절한 값으로 바꾸고 새 데이터베이스의 이름을 지정합니다(꺽쇠 괄호도 바꿈).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-230">Replace the values in angle brackets with appropriate values for your SQL server logical server and specify a name for the new database (also replace the angle brackets).</span></span> <span data-ttu-id="e0a9b-231">데이터베이스 버전 및 서비스 목표의 값을 환경에 맞게 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-231">You can also choose to change the values for database edition and service objectgive as appropriate to your environment.</span></span> <span data-ttu-id="e0a9b-232">이 자습서에서는 마이그레이션된 데이터베이스를 **myMigratedDatabase**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-232">For the purpose of this tutorial, the migrated database is called **myMigratedDatabase**.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 가져오기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="e0a9b-234">SQL Server 논리 서버는 포트 1433을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-234">A SQL server logical server listens on port 1433.</span></span> <span data-ttu-id="e0a9b-235">회사 방화벽 내에서 SQL Server 논리 서버로 연결을 시도하면 성공적인 연결을 위해 회사 방화벽에서 이 포트가 열려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-235">If you are attempting to connect to a SQL server logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

## <a name="connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="e0a9b-236">SSMS(SQL Server Management Studio)를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="e0a9b-236">Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="e0a9b-237">SQL Server Management Studio를 사용하여 Azure SQL Database 서버 및 새롭게 마이그레이션된 데이터베이스(이 자습서에서는 **myMigratedDatabase**)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-237">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server and newly migrated database, called **myMigratedDatabase** in this tutorial.</span></span> <span data-ttu-id="e0a9b-238">SQLPackage를 실행한 다른 컴퓨터에서 SQL Server Management Studio를 실행하는 경우 이전 절차의 단계를 사용하여 이 컴퓨터에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-238">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using the steps in the previous procedure.</span></span>

1. <span data-ttu-id="e0a9b-239">SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-239">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="e0a9b-240">**서버에 연결** 대화 상자에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-240">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="e0a9b-241">**서버 유형**: 데이터베이스 엔진을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-241">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="e0a9b-242">**서버 이름**: **mynewserver20170403.database.windows.net**과 같은 정규화된 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-242">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="e0a9b-243">**인증**: SQL Server 인증을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-243">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="e0a9b-244">**로그인**: 서버 관리자 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-244">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="e0a9b-245">**암호**: 서버 관리자 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-245">**Password**: Enter the password for your server admin account</span></span>
 
    ![ssms로 연결](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="e0a9b-247">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-247">Click **Connect**.</span></span> <span data-ttu-id="e0a9b-248">개체 탐색기 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-248">The Object Explorer window opens.</span></span> 

4. <span data-ttu-id="e0a9b-249">개체 탐색기에서 **데이터베이스**를 확장한 다음 **myMigratedDatabase**를 확장하여 샘플 데이터베이스에 있는 개체를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-249">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** to view the objects in the sample database.</span></span>

## <a name="change-database-properties"></a><span data-ttu-id="e0a9b-250">데이터베이스 속성 변경</span><span class="sxs-lookup"><span data-stu-id="e0a9b-250">Change database properties</span></span>

<span data-ttu-id="e0a9b-251">SQL Server Management Studio를 사용하여 서비스 계층, 성능 수준 및 호환성 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-251">You can change the service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span> <span data-ttu-id="e0a9b-252">가져오기 단계 중에 최고의 성능을 위해 더 높은 성능의 계층 데이터베이스를 가져오는 것이 좋지만, 가져오기가 완료된 후 규모를 축소하여 가져온 데이터베이스를 적극적으로 사용할 준비가 될 때까지 비용을 절약하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-252">During the import phase, we recommend that you import to a higher performance tier database for best performance, but that you scale down after the import completes to save money until you are ready to actively use the imported database.</span></span> <span data-ttu-id="e0a9b-253">호환성 수준을 변경하면 Azure SQL Database 서비스의 최신 기능에 대한 성능과 액세스가 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-253">Changing the compatibility level may yield better performance and access to the newest capabilities of the Azure SQL Database service.</span></span> <span data-ttu-id="e0a9b-254">이전 데이터베이스를 마이그레이션할 경우 해당 데이터베이스 호환성 수준은 가져오는 데이터베이스와 호환 가능한 가장 낮은 지원 수준으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-254">When you migrate an older database, its database compatibility level is maintained at the lowest supported level that is compatible with the database being imported.</span></span> <span data-ttu-id="e0a9b-255">자세한 내용은 [Azure SQL Database의 호환성 수준 130을 통해 개선된 쿼리 성능](sql-database-compatibility-level-query-performance-130.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-255">For more information, see [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).</span></span>

1. <span data-ttu-id="e0a9b-256">개체 탐색기에서 **myMigratedDatabase**를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-256">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="e0a9b-257">데이터베이스에 연결된 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-257">A query window opens connected to your database.</span></span>

2. <span data-ttu-id="e0a9b-258">다음 명령을 실행하여 서비스 계층을 **Standard**로, 성능 수준을 **S1**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-258">Execute the following command to set the service tier to **Standard** and the performance level to **S1**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![서비스 계층 변경](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. <span data-ttu-id="e0a9b-260">다음 명령을 실행하여 데이터베이스 호환성 수준을 **130**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-260">Execute the following command to change the database compatibility level to **130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![호환성 수준 변경](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="e0a9b-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0a9b-262">Next steps</span></span> 
<span data-ttu-id="e0a9b-263">이 자습서에서는 데이터베이스를 준비하고 내보내며 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-263">In this tutorial you prepared, exported and imported your database.</span></span> <span data-ttu-id="e0a9b-264">다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-264">You learned to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0a9b-265">Azure SQL Database로의 마이그레이션을 위해 SQL Server에서 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="e0a9b-265">Prepare a database in a SQL Server for migration to Azure SQL Database</span></span>
> * <span data-ttu-id="e0a9b-266">데이터베이스를 BACPAC 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-266">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="e0a9b-267">BACPAC 파일을 Azure SQL Database로 가져오기</span><span class="sxs-lookup"><span data-stu-id="e0a9b-267">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="e0a9b-268">데이터의 보안을 설정하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-268">Advance to the next tutorial to learn how to secure your database.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="e0a9b-269">[Azure SQL Database 보안](sql-database-security-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="e0a9b-269">[Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>


