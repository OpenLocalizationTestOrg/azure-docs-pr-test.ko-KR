---
title: "SQL Server DB tooAzure aaaMigrate SQL 데이터베이스 | Microsoft Docs"
description: "Toomigrate SQL Server 데이터베이스 tooAzure SQL 데이터베이스에 알아봅니다."
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
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a><span data-ttu-id="0e57c-103">SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0e57c-103">Migrate your SQL Server database tooAzure SQL Database</span></span>

<span data-ttu-id="0e57c-104">SQL Server 이동 데이터베이스 tooAzure SQL 데이터베이스는 세 부분 프로세스-먼저 준비 다음 내보내기 및 다음 hello 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-104">Moving your SQL Server database tooAzure SQL Database is a three part process - you first prepare, then export, and then import hello database.</span></span> <span data-ttu-id="0e57c-105">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-105">In this tutorial, you learn to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e57c-106">마이그레이션 tooAzure SQL 데이터베이스에 대 한 SQL Server에 데이터베이스를 준비 hello를 사용 하 여 [데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span><span class="sxs-lookup"><span data-stu-id="0e57c-106">Prepare a database in a SQL Server for migration tooAzure SQL Database using hello [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span></span>
> * <span data-ttu-id="0e57c-107">Hello 데이터베이스 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="0e57c-107">Export hello database tooa BACPAC file</span></span>
> * <span data-ttu-id="0e57c-108">Azure SQL 데이터베이스로 hello BACPAC 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e57c-108">Import hello BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="0e57c-109">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e57c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e57c-110">Prerequisites</span></span>

<span data-ttu-id="0e57c-111">toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-111">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="0e57c-112">최신 버전의 설치 된 hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="0e57c-112">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="0e57c-113">SSMS 설치 hello SQLPackage 사용 하는 데이터베이스 개발 태스크의 범위 tooautomate 일 수 있는 명령줄 유틸리티의 최신 버전도 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-113">Installing SSMS also installs hello newest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span> 
- <span data-ttu-id="0e57c-114">설치 된 hello [데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span><span class="sxs-lookup"><span data-stu-id="0e57c-114">Installed hello [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="0e57c-115">액세스 tooa 데이터베이스 toomigrate 있고 식별.</span><span class="sxs-lookup"><span data-stu-id="0e57c-115">You have identified and have access tooa database toomigrate.</span></span> <span data-ttu-id="0e57c-116">이 자습서에서는 hello [SQL Server 2008 r2 AdventureWorks OLTP 데이터베이스](https://msftdbprodsamples.codeplex.com/releases/view/59211) SQL Server 2008 r2 또는 최신, 인스턴스에 하지만 사용자가 선택한 모든 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-116">This tutorial uses hello [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> <span data-ttu-id="0e57c-117">toofix 호환성 문제를 사용 하 여 [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span><span class="sxs-lookup"><span data-stu-id="0e57c-117">toofix compatibility issues, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span></span>

## <a name="prepare-for-migration"></a><span data-ttu-id="0e57c-118">마이그레이션 준비</span><span class="sxs-lookup"><span data-stu-id="0e57c-118">Prepare for migration</span></span>

<span data-ttu-id="0e57c-119">마이그레이션에 대 한 준비 tooprepare 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-119">You are ready tooprepare for migration.</span></span> <span data-ttu-id="0e57c-120">이러한 단계 toouse hello에 따라  **[데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello 마이그레이션 tooAzure SQL 데이터베이스에 대 한 데이터베이스의 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-120">Follow these steps toouse hello **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** tooassess hello readiness of your database for migration tooAzure SQL Database.</span></span>

1. <span data-ttu-id="0e57c-121">열기 hello **데이터 Migration Assistant**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-121">Open hello **Data Migration Assistant**.</span></span> <span data-ttu-id="0e57c-122">Toomigrate 계획, hello 호스트 컴퓨터에 SQL Server 인스턴스를 hello tooinstall 불필요 DMA 연결 toohello SQL Server 인스턴스에 포함 된 hello 데이터베이스와 모든 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-122">You can run DMA on any computer with connectivity toohello SQL Server instance containing hello database that you plan toomigrate, you do not need tooinstall it on hello computer hosting hello SQL Server instance.</span></span>

     ![Data Migration Assistant 열기](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="0e57c-124">Hello 왼쪽 메뉴에서 클릭 **+ 새로 만들기** toocreate는 **평가** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="0e57c-124">In hello left-hand menu, click **+ New** toocreate an **Assessment** project.</span></span> <span data-ttu-id="0e57c-125">Hello 형식으로 입력 한 **프로젝트 이름** (다른 모든 값의 기본값 유지 해야)를 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-125">Fill in hello form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="0e57c-126">hello **옵션** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-126">hello **Options** page opens.</span></span>

     ![새 Data Migration Assistant 프로젝트](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="0e57c-128">Hello에 **옵션** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-128">On hello **Options** page, click **Next**.</span></span> <span data-ttu-id="0e57c-129">hello **원본을 선택** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-129">hello **Select sources** page opens.</span></span>

     ![새 데이터 마이그레이션 옵션](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="0e57c-131">Hello에 **원본을 선택** 페이지 toomigrate 계획 hello 서버를 포함 하는 SQL Server 인스턴스의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-131">On hello **Select sources** page, enter hello name of SQL Server instance containing hello server you plan toomigrate.</span></span> <span data-ttu-id="0e57c-132">필요한 경우이 페이지의 다른 값 hello 하는 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-132">Change hello other values on this page if necessary.</span></span> <span data-ttu-id="0e57c-133">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-133">Click **Connect**.</span></span>

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="0e57c-135">Hello에 **원본을 추가** hello 부분의 **원본을 선택** 페이지 hello 데이터베이스 toobe 호환성에 대 한 테스트에 대 한 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-135">In hello **Add sources** portion of hello **Select sources** page, select hello checkboxes for hello databases toobe tested for compatibility.</span></span> <span data-ttu-id="0e57c-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-136">Click **Add**.</span></span>

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="0e57c-138">**Start Assessment**(평가 시작)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-138">Click **Start Assessment**.</span></span>

     ![새 데이터 마이그레이션 평가 시작](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="0e57c-140">Hello 평가 완료 되 면 먼저 찾습니다 toosee hello 데이터베이스가 충분히 호환 toomigrate 경우.</span><span class="sxs-lookup"><span data-stu-id="0e57c-140">When hello assessment completes, first look toosee if hello database is sufficiently compatible toomigrate.</span></span> <span data-ttu-id="0e57c-141">녹색 원에 hello 확인 표시를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-141">Look for hello checkmark in a green circle.</span></span>

     ![새 데이터 마이그레이션 호환 평가 결과](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="0e57c-143">Hello 결과 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-143">Review hello results.</span></span> <span data-ttu-id="0e57c-144">hello **대응 되는 SQL Server 기능** 표시 된 결과 hello 기본 결과 tooreview 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-144">hello **SQL Server feature parity** results shown are hello default results tooreview.</span></span> <span data-ttu-id="0e57c-145">특히 부분적으로 지원 되 고 지원 되지 않는 기능에 대 한 hello 정보 및 권장된 조치에 대 한 정보를 제공 하는 hello 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-145">Specifically review hello information about unsupported and partially supported features, and hello provided information about recommended actions.</span></span> 

     ![새 데이터 마이그레이션 평가 패리티](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="0e57c-147">검토 hello **호환성 문제** hello 홈페이지에서 해당 옵션을 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-147">Review hello **Compatibility issues** by clicking that option in hello upper left.</span></span> <span data-ttu-id="0e57c-148">특히 검토 hello 마이그레이션 블로 커가, 동작 변경 내용에 대 한 정보 및 각 호환성 수준에 대 한 기능을 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-148">Specifically review hello information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="0e57c-149">Hello AdventureWorks2008R2 데이터베이스에 대 한 hello 변경 내용을 검토 tooFull 텍스트 검색 SQL Server 2008 및 hello 이후 SQL Server 2000 이후로 tooSERVERPROPERTY('LCID')를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-149">For hello AdventureWorks2008R2 database, review hello changes tooFull-Text Search since SQL Server 2008 and hello changes tooSERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="0e57c-150">이러한 변경 사항의 자세한 내용에 대한 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-150">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="0e57c-151">변경된 다양한 검색 옵션 및 전체 텍스트 검색에 대한 설정</span><span class="sxs-lookup"><span data-stu-id="0e57c-151">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="0e57c-152">프로그램 데이터베이스 tooAzure SQL 데이터베이스를 마이그레이션한 후 toooperate hello 데이터베이스의 현재 호환성 수준 (수준 100 hello AdventureWorks2008R2 데이터베이스에 대 한) 또는 더 높은 수준에서 데이터베이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-152">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="0e57c-153">Hello 의미 및 특정 호환성 수준에서 데이터베이스를 운영 하기 위한 옵션에 대 한 자세한 내용은 참조 하십시오. [ALTER DATABASE 호환성 수준](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-153">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="0e57c-154">참고 항목 [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) 추가 데이터베이스 수준 설정에 대 한 정보에 대 한 관련 toocompatibility 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-154">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>
   >

10. <span data-ttu-id="0e57c-155">필요에 따라 **보고서 내보내기** toosave hello 보고서를 JSON 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-155">Optionally, click **Export report** toosave hello report as a JSON file.</span></span>
11. <span data-ttu-id="0e57c-156">데이터 마이그레이션 길잡이 닫기 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-156">Close hello Data Migration Assistant.</span></span>

## <a name="export-toobacpac-file"></a><span data-ttu-id="0e57c-157">내보내기 tooBACPAC 파일</span><span class="sxs-lookup"><span data-stu-id="0e57c-157">Export tooBACPAC file</span></span> 

<span data-ttu-id="0e57c-158">BACPAC 파일이 hello 메타 데이터 및 SQL Server 데이터베이스에서 데이터가 포함 된 BACPAC의 확장명을 가진 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-158">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="0e57c-159">BACPAC 파일을 저장할 수 있습니다 또는 마이그레이션-보관 하기 위한 로컬 저장소 또는 Azure blob 저장소에과 같은 SQL Server tooAzure SQL 데이터베이스에서.</span><span class="sxs-lookup"><span data-stu-id="0e57c-159">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server tooAzure SQL Database.</span></span> <span data-ttu-id="0e57c-160">트랜잭션 측면에서 일치 하는 내보내기 toobe에 대 한 확인 해야 하거나 없는 쓰기 작업이 hello 내보내기 작업 중에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-160">For an export toobe transactionally consistent, you must ensure either that no write activity is occurring during hello export.</span></span>

<span data-ttu-id="0e57c-161">이러한 단계 toouse hello SQLPackage 명령줄 유틸리티 tooexport hello AdventureWorks2008R2 데이터베이스 toolocal 저장소를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-161">Follow these steps toouse hello SQLPackage command-line utility tooexport hello AdventureWorks2008R2 database toolocal storage.</span></span>

1. <span data-ttu-id="0e57c-162">Windows 명령 프롬프트를 열고 hello 해야 디렉터리 tooa 폴더를 변경 **130** SQLPackage의-같은 버전 **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-162">Open a Windows command prompt and change your directory tooa folder in which you have hello **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="0e57c-163">다음 명령 프롬프트 tooexport hello hello에서 SQLPackage 명령을 hello 실행 **AdventureWorks2008R2** 에서 데이터베이스를 **localhost** 너무**AdventureWorks2008R2.bacpac**.</span><span class="sxs-lookup"><span data-stu-id="0e57c-163">Execute hello following SQLPackage command at hello command prompt tooexport hello **AdventureWorks2008R2** database from **localhost** too**AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="0e57c-164">적절 한 tooyour 환경으로 다음이 값 중 하나를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-164">Change any of these values as appropriate tooyour environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 내보내기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="0e57c-166">Hello 실행이 완료 되 면 hello 생성 된 BACPAC 파일 실행 hello sqlpackage가 있는 hello 디렉터리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-166">Once hello execution is complete hello generated BACPAC file is stored in hello directory where hello sqlpackage executable is located.</span></span> <span data-ttu-id="0e57c-167">이 예제에서는 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-167">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="0e57c-168">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="0e57c-168">Log in toohello Azure portal</span></span>

<span data-ttu-id="0e57c-169">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-169">Log in toohello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0e57c-170">Hello SQLPackage 명령줄 유틸리티를 실행 하 고 있는 hello 컴퓨터에서 로그온 hello 생성 hello 방화벽 규칙의 5 단계에서 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-170">Logging on from hello computer from which you are running hello SQLPackage command-line utility eases hello creation of hello firewall rule in step 5.</span></span>

## <a name="create-a-sql-server-logical-server"></a><span data-ttu-id="0e57c-171">SQL Server 논리 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="0e57c-171">Create a SQL server logical server</span></span>

<span data-ttu-id="0e57c-172">[SQL Server 논리 서버](sql-database-features.md)는 여러 데이터베이스에 대한 중앙 관리 지점의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-172">A [SQL server logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="0e57c-173">이러한 단계에 따라 SQL server 논리 서버 toocontain hello toocreate Adventure Works OLTP SQL Server 데이터베이스 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="0e57c-173">Follow these steps toocreate a SQL server logical server toocontain hello migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="0e57c-174">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-174">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="0e57c-175">형식 **sql server** hello hello 검색 창에서 **새로 만들기** 선택한 페이지 **SQL 데이터베이스 (논리 서버)** hello에서 필터링 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-175">Type **sql server** in hello search window on hello **New** page, and select **SQL database (logical server)** from hello filtered list.</span></span>

    ![논리 서버 선택](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="0e57c-177">Hello에 **모든** 페이지 **SQL server (논리 서버)** 클릭 하 고 **만들기** hello에 **SQL Server (논리 서버)** 페이지 .</span><span class="sxs-lookup"><span data-stu-id="0e57c-177">On hello **Everything** page, click **SQL server (logical server)** and then click **Create** on hello **SQL Server (logical server)** page.</span></span>

    ![논리 서버 만들기](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="0e57c-179">Hello 이미지 앞에 표시 된 대로 hello SQL server (논리 서버) 양식을 사용 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-179">Fill out hello SQL server (logical server) form with hello following information, as shown on hello preceding image:</span></span>     

   | <span data-ttu-id="0e57c-180">설정</span><span class="sxs-lookup"><span data-stu-id="0e57c-180">Setting</span></span>       | <span data-ttu-id="0e57c-181">제안 값</span><span class="sxs-lookup"><span data-stu-id="0e57c-181">Suggested value</span></span> | <span data-ttu-id="0e57c-182">설명</span><span class="sxs-lookup"><span data-stu-id="0e57c-182">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="0e57c-183">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="0e57c-183">**Server name**</span></span> | <span data-ttu-id="0e57c-184">전역적으로 고유한 이름 입력</span><span class="sxs-lookup"><span data-stu-id="0e57c-184">Enter any globally unique name</span></span> | <span data-ttu-id="0e57c-185">유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-185">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="0e57c-186">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="0e57c-186">**Server admin login**</span></span> | <span data-ttu-id="0e57c-187">유효한 이름 입력</span><span class="sxs-lookup"><span data-stu-id="0e57c-187">Enter any valid name</span></span> | <span data-ttu-id="0e57c-188">유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-188">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="0e57c-189">**암호**</span><span class="sxs-lookup"><span data-stu-id="0e57c-189">**Password**</span></span> | <span data-ttu-id="0e57c-190">유효한 암호 입력</span><span class="sxs-lookup"><span data-stu-id="0e57c-190">Enter any valid password</span></span> | <span data-ttu-id="0e57c-191">암호가 8 자 이상 있어야 하며 hello 다음 범주 중 세 범주의 문자를 포함 해야 합니다: 대문자, 소문자, 숫자 및 영숫자가 아닌 문자.</span><span class="sxs-lookup"><span data-stu-id="0e57c-191">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="0e57c-192">**구독**</span><span class="sxs-lookup"><span data-stu-id="0e57c-192">**Subscription**</span></span> | <span data-ttu-id="0e57c-193">구독 선택</span><span class="sxs-lookup"><span data-stu-id="0e57c-193">Select a subscription</span></span> | <span data-ttu-id="0e57c-194">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-194">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="0e57c-195">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="0e57c-195">**Resource group**</span></span> | <span data-ttu-id="0e57c-196">기존 리소스 그룹을 선택하거나 새 그룹을 만듭니다(예: **myResourceGroup**).</span><span class="sxs-lookup"><span data-stu-id="0e57c-196">Choose an existing resource group or create a new group, such as **myResourceGroup**</span></span> |  <span data-ttu-id="0e57c-197">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-197">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="0e57c-198">**위치**:</span><span class="sxs-lookup"><span data-stu-id="0e57c-198">**Location**</span></span> | <span data-ttu-id="0e57c-199">새 서버 hello에 대 한 올바른 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-199">Enter any valid location for hello new server</span></span> | <span data-ttu-id="0e57c-200">지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-200">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![논리 서버 만들기 양식 완료](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="0e57c-202">클릭 **만들기** tooprovision hello 논리 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-202">Click **Create** tooprovision hello logical server.</span></span> <span data-ttu-id="0e57c-203">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-203">Provisioning takes a few minutes.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0e57c-204">서버 이름, 서버 관리자 로그인 이름 및 암호를 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-204">Remember your server name, server admin login name, and password.</span></span> <span data-ttu-id="0e57c-205">이 자습서의 뒷부분에서 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-205">You need these values later in this tutorial.</span></span>
>

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="0e57c-206">서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="0e57c-206">Create a server-level firewall rule</span></span>

<span data-ttu-id="0e57c-207">SQL 데이터베이스 서비스 hello 만듭니다는 [hello 서버 수준 방화벽](sql-database-firewall-configure.md) 외부 응용 프로그램 및 도구는 방화벽 규칙 tooopen hello를 만들지 않으면 toohello 서버나 hello 서버에 있는 모든 데이터베이스를 연결 하지 못하도록 방지 하 특정 IP 주소에 대 한 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-207">hello SQL Database service creates a [firewall at hello server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="0e57c-208">이러한 단계 toocreate hello SQLPackage 명령줄 유틸리티를 실행 하 고 있는 hello 컴퓨터의 hello IP 주소에 대 한 SQL 데이터베이스 서버 수준 방화벽 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-208">Follow these steps toocreate a SQL Database server-level firewall rule for hello IP address of hello computer from which you are running hello SQLPackage command-line utility.</span></span> <span data-ttu-id="0e57c-209">이 통해 SQLPackage tooconnect toohello SQL serverDatabase 논리 서버 hello Azure SQL 데이터베이스 방화벽을 통해.</span><span class="sxs-lookup"><span data-stu-id="0e57c-209">This enables SQLPackage tooconnect toohello SQL serverDatabase logical server through hello Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="0e57c-210">클릭 **모든 리소스** hello 왼쪽 메뉴에서 새 서버 hello에 클릭 **모든 리소스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0e57c-210">Click **All resources** from hello left-hand menu and click your new server on hello **All resources** page.</span></span> <span data-ttu-id="0e57c-211">서버에 대 한 개요 페이지 hello 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-211">hello overview page for your server opens and provides options for further configuration.</span></span>

     ![논리 서버 개요](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="0e57c-213">클릭 **방화벽** hello 왼쪽 메뉴 아래에서 **설정을** hello 개요 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-213">Click **Firewall** in hello left-hand menu under **Settings** on hello overview page.</span></span> <span data-ttu-id="0e57c-214">hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-214">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="0e57c-215">클릭 **클라이언트 IP 추가** hello 컴퓨터의 hello 도구 모음 tooadd hello IP 주소에 현재 사용 하 고이 클릭 한 다음 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-215">Click **Add client IP** on hello toolbar tooadd hello IP address of hello computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="0e57c-216">이 IP 주소에 대한 서버 수준 방화벽 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-216">A server-level firewall rule is created for this IP address.</span></span>

     ![set server firewall rule](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="0e57c-218">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-218">Click **OK**.</span></span>

<span data-ttu-id="0e57c-219">이제 tooall 데이터베이스 SQL Server Management Studio 또는 이전에 만든 hello 서버 관리자 계정을 사용 하 여이 IP 주소에서 선택한 다른 도구를 사용 하 여이 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-219">You can now connect tooall databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="0e57c-220">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-220">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0e57c-221">회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-221">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0e57c-222">이 경우에 IT 부서는 포트 1433을 엽니다 하지 않는 한 tooyour Azure SQL 데이터베이스 서버를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-222">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a><span data-ttu-id="0e57c-223">BACPAC 파일 tooAzure SQL 데이터베이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e57c-223">Import a BACPAC file tooAzure SQL Database</span></span> 

<span data-ttu-id="0e57c-224">hello 한 최신 버전의 hello SQLPackage 명령줄 유틸리티에 지정 된 Azure SQL 데이터베이스를 만들기 위한 지원을 제공 [서비스 계층과 성능 수준](sql-database-service-tiers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-224">hello newest versions of hello SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="0e57c-225">가져오기 중 최상의 성능을 위해 높은 서비스 계층과 성능 수준을 선택 하 고 hello 서비스 계층과 성능 수준을 즉시 필요한 것 보다 높은 경우 가져온 후 다음 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-225">For best performance during import, select a high service tier and performance level and then scale down after import if hello service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="0e57c-226">이 단계 사용 하 여 hello SQLPackage 명령줄 유틸리티 tooimport hello AdventureWorks2008R2 데이터베이스 tooAzure SQL 데이터베이스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-226">Follow these steps use hello SQLPackage command-line utility tooimport hello AdventureWorks2008R2 database tooAzure SQL Database.</span></span> <span data-ttu-id="0e57c-227">이 작업에 대 한 SQL Server Management Studio를 사용할 수 있지만 SQLPackage는 최대한의 유연성 및 최상의 성능을 위해 대부분의 프로덕션 환경에 대 한 hello 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-227">While you can use SQL Server Management Studio for this task, SQLPackage is hello preferred method for most production environments for maximum flexibility and best performance.</span></span> <span data-ttu-id="0e57c-228">참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-228">See [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

- <span data-ttu-id="0e57c-229">다음 명령 프롬프트 tooimport hello hello에서 SQLPackage 명령을 hello 실행 **AdventureWorks2008R2** 로컬 저장소 toohello SQL server 논리 서버에서 해당 하면 이전에 만든된 tooa 새 데이터베이스를 서비스 데이터베이스 계층 **프리미엄**, 및의 서비스 목표 **P6**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-229">Execute hello following SQLPackage command at hello command prompt tooimport hello **AdventureWorks2008R2** database from local storage toohello SQL server logical server that you previously created tooa new database, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="0e57c-230">꺾쇠 괄호 hello 값을 SQL server 논리 서버에 대 한 적절 한 값으로 교체 하 고 hello 새 데이터베이스 (또한 replace hello 꺾쇠 괄호)에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-230">Replace hello values in angle brackets with appropriate values for your SQL server logical server and specify a name for hello new database (also replace hello angle brackets).</span></span> <span data-ttu-id="0e57c-231">또한 적절 한 tooyour 환경으로 데이터베이스 버전 및 서비스 objectgive toochange hello 값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-231">You can also choose toochange hello values for database edition and service objectgive as appropriate tooyour environment.</span></span> <span data-ttu-id="0e57c-232">이 자습서의 hello 용도로 hello 마이그레이션된 데이터베이스 라고 **myMigratedDatabase**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-232">For hello purpose of this tutorial, hello migrated database is called **myMigratedDatabase**.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 가져오기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="0e57c-234">SQL Server 논리 서버는 포트 1433을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-234">A SQL server logical server listens on port 1433.</span></span> <span data-ttu-id="0e57c-235">Tooconnect tooa SQL server 논리 서버에서 회사 방화벽 내에서 시도 하는 경우 있습니다 toosuccessfully 연결을 위해이 포트 hello 회사 방화벽에서 열려 있는 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-235">If you are attempting tooconnect tooa SQL server logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

## <a name="connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="0e57c-236">SSMS(SQL Server Management Studio)를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="0e57c-236">Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="0e57c-237">SQL Server Management Studio tooestablish 연결 tooyour Azure SQL 데이터베이스 서버 및 라는 새로 마이그레이션된 데이터베이스를 사용 하 여 **myMigratedDatabase** 이 자습서에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-237">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server and newly migrated database, called **myMigratedDatabase** in this tutorial.</span></span> <span data-ttu-id="0e57c-238">SQLPackage를 실행 하는 다른 컴퓨터에 SQL Server Management Studio를 실행 하는 경우 hello 단계를 사용 하 여 hello 이전 절차에서이 컴퓨터에 대 한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-238">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using hello steps in hello previous procedure.</span></span>

1. <span data-ttu-id="0e57c-239">SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-239">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="0e57c-240">Hello에 **tooServer 연결** 대화 상자에 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-240">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>
   - <span data-ttu-id="0e57c-241">**서버 유형**: 데이터베이스 엔진을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-241">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="0e57c-242">**서버 이름**: **mynewserver20170403.database.windows.net**과 같은 정규화된 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-242">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="0e57c-243">**인증**: SQL Server 인증을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-243">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="0e57c-244">**로그인**: 서버 관리자 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-244">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="0e57c-245">**암호**: 서버 관리자 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-245">**Password**: Enter hello password for your server admin account</span></span>
 
    ![ssms로 연결](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="0e57c-247">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-247">Click **Connect**.</span></span> <span data-ttu-id="0e57c-248">hello 개체 탐색기 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-248">hello Object Explorer window opens.</span></span> 

4. <span data-ttu-id="0e57c-249">개체 탐색기에서 확장 **데이터베이스** 펼친 다음 **myMigratedDatabase** hello 샘플 데이터베이스의 tooview hello 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-249">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="change-database-properties"></a><span data-ttu-id="0e57c-250">데이터베이스 속성 변경</span><span class="sxs-lookup"><span data-stu-id="0e57c-250">Change database properties</span></span>

<span data-ttu-id="0e57c-251">Hello 서비스 계층, 성능 수준 및 SQL Server Management Studio를 사용 하 여 호환성 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-251">You can change hello service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span> <span data-ttu-id="0e57c-252">Hello 가져오기 단계 중 최상의 성능을 위해 tooa 더 높은 성능 계층 데이터베이스를 가져올 하지만 hello 가져오기 가져온된 데이터베이스를 hello 준비 tooactively 사용 될 때까지 toosave money 완료 된 후 확장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-252">During hello import phase, we recommend that you import tooa higher performance tier database for best performance, but that you scale down after hello import completes toosave money until you are ready tooactively use hello imported database.</span></span> <span data-ttu-id="0e57c-253">Hello 호환성 수준을 변경 더 나은 성능과 액세스 toohello hello Azure SQL 데이터베이스 서비스의 최신 기능을 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-253">Changing hello compatibility level may yield better performance and access toohello newest capabilities of hello Azure SQL Database service.</span></span> <span data-ttu-id="0e57c-254">이전 데이터베이스를 마이그레이션하는 경우 가져올 hello 데이터베이스와 호환 되는 지원 hello 가장 낮은 수준에서의 데이터베이스 호환성 수준이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-254">When you migrate an older database, its database compatibility level is maintained at hello lowest supported level that is compatible with hello database being imported.</span></span> <span data-ttu-id="0e57c-255">자세한 내용은 [Azure SQL Database의 호환성 수준 130을 통해 개선된 쿼리 성능](sql-database-compatibility-level-query-performance-130.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e57c-255">For more information, see [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).</span></span>

1. <span data-ttu-id="0e57c-256">개체 탐색기에서 **myMigratedDatabase**를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-256">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="0e57c-257">쿼리 창에 연결 된 tooyour 데이터베이스를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-257">A query window opens connected tooyour database.</span></span>

2. <span data-ttu-id="0e57c-258">너무 명령 tooset hello 서비스 계층을 따라 hello 실행**표준** 성능 수준에 너무 hello 및**S1**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-258">Execute hello following command tooset hello service tier too**Standard** and hello performance level too**S1**.</span></span>

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

3. <span data-ttu-id="0e57c-260">실행 명령 toochange hello 데이터베이스 호환성 수준이 너무 다음 hello**130**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-260">Execute hello following command toochange hello database compatibility level too**130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![호환성 수준 변경](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="0e57c-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e57c-262">Next steps</span></span> 
<span data-ttu-id="0e57c-263">이 자습서에서는 데이터베이스를 준비하고 내보내며 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-263">In this tutorial you prepared, exported and imported your database.</span></span> <span data-ttu-id="0e57c-264">다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-264">You learned to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e57c-265">마이그레이션 tooAzure SQL 데이터베이스에 대 한 SQL Server에 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-265">Prepare a database in a SQL Server for migration tooAzure SQL Database</span></span>
> * <span data-ttu-id="0e57c-266">Hello 데이터베이스 tooa BACPAC 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="0e57c-266">Export hello database tooa BACPAC file</span></span>
> * <span data-ttu-id="0e57c-267">Azure SQL 데이터베이스로 hello BACPAC 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e57c-267">Import hello BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="0e57c-268">다음 자습서 toolearn toohello 어떻게 발전 toosecure 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e57c-268">Advance toohello next tutorial toolearn how toosecure your database.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="0e57c-269">[Azure SQL Database 보안](sql-database-security-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="0e57c-269">[Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>


