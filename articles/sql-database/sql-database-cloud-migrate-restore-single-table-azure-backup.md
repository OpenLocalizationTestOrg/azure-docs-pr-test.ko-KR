---
title: "Azure SQL 데이터베이스 백업에서 단일 테이블 aaaRestore | Microsoft Docs"
description: "어떻게 toorestore 단일은 Azure SQL 데이터베이스 백업에서을 테이블에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="54747-103">어떻게 toorestore 단일은 Azure SQL 데이터베이스 백업에서을 테이블합니다</span><span class="sxs-lookup"><span data-stu-id="54747-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="54747-104">실수로 SQL 데이터베이스의 일부 데이터를 수정 하는 상황이 발생할 수 있습니다 하 고 나면 toorecover hello 단일 영향을 받는 테이블 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="54747-105">이 문서에서 설명 하는 방법을 toorestore는 단일 테이블에 있는 데이터베이스 hello SQL 데이터베이스 중 하나를 [자동 백업](sql-database-automated-backups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="54747-106">준비 단계: hello 테이블 이름을 바꾸고 hello 데이터베이스의 복사본을 복원</span><span class="sxs-lookup"><span data-stu-id="54747-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="54747-107">Hello tooreplace 복원 hello 복사본으로 지정 하 여 Azure SQL 데이터베이스에는 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="54747-108">Microsoft SQL Management Studio toorename hello 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="54747-109">예를 들어 hello 테이블 이름 바꾸기 &lt;테이블 이름&gt;_old 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="54747-110">차단 되 고 tooavoid 바꾸려는 hello 테이블에서 실행 중인 작업이 없을 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="54747-111">문제가 발생하면 유지 관리 기간 동안 이 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="54747-112">프로그램 데이터베이스 tooa 지정 시간 toorecover toousing hello 원하는의 백업을 복원 [지점 In_Time 복원](sql-database-recovery-using-backups.md#point-in-time-restore) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="54747-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="54747-113">hello DBName + 타임 스탬프 형식으로 복원 하는 hello 데이터베이스의 hello 이름은 됩니다. 예를 들어 **01 01T22 12Z Adventureworks2012_2016**합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="54747-114">이 단계 hello 서버에서 기존 데이터베이스 이름을 hello 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="54747-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="54747-115">안전 조치 이며 것은 tooallow tooverify hello 복원할 데이터베이스의 현재 데이터베이스를 삭제 한 프로덕션 용도로 hello 복원 된 데이터베이스의 이름을 바꾸거나 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="54747-116">Hello SQL 데이터베이스 마이그레이션 도구를 사용 하 여 데이터베이스를 복원 하는 hello에서 복사 hello 테이블</span><span class="sxs-lookup"><span data-stu-id="54747-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="54747-117">다운로드 및 설치 hello [SQL 데이터베이스 마이그레이션 마법사](https://sqlazuremw.codeplex.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="54747-118">Hello의 SQL 데이터베이스 마이그레이션 마법사 열기 hello **프로세스 선택** 페이지에서 선택 **분석/마이그레이션 데이터베이스**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL 데이터베이스 마이그레이션 마법사 - 프로세스 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="54747-120">Hello에 **tooServer 연결** 대화 상자에서 다음 설정을 hello 적용:</span><span class="sxs-lookup"><span data-stu-id="54747-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="54747-121">서버 이름: **SQL server**</span><span class="sxs-lookup"><span data-stu-id="54747-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="54747-122">응용 프로그램: **SQL Server Authentication**</span><span class="sxs-lookup"><span data-stu-id="54747-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="54747-123">로그인: **로그인**</span><span class="sxs-lookup"><span data-stu-id="54747-123">Login: **Your login**</span></span>
   * <span data-ttu-id="54747-124">암호: **암호**</span><span class="sxs-lookup"><span data-stu-id="54747-124">Password: **Your password**</span></span>
   * <span data-ttu-id="54747-125">데이터베이스: **Master DB (모든 데이터베이스 나열)**</span><span class="sxs-lookup"><span data-stu-id="54747-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="54747-126">기본적으로 hello 마법사는 로그인 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="54747-127">저장하지 않으려면 **로그인 정보 삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 1단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="54747-129">Hello에 **원본 선택** 대화 상자, hello에서 데이터베이스 이름 선택 hello 복원 **준비 단계** 를 소스로 섹션 및 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 2단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="54747-131">Hello에 **개체 선택** 대화 상자, 선택 hello **특정 데이터베이스 개체 선택** 옵션을 선택한 다음 hello table(or tables) 원하는 toomigrate toohello 대상 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="54747-132">![SQL 데이터베이스 마이그레이션 마법사 - 개체 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="54747-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="54747-133">Hello에 **스크립트 마법사 요약** 페이지 **예** 용인지 준비 toogenerate SQL 스크립트에 대 한 프롬프트 메시지가 나타날 때.</span><span class="sxs-lookup"><span data-stu-id="54747-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="54747-134">Hello 옵션 toosave hello TSQL 스크립트 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54747-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="54747-135">![SQL 데이터베이스 마이그레이션 마법사 - 스크립트 마법사 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="54747-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="54747-136">Hello에 **결과 요약** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="54747-137">![SQL 데이터베이스 마이그레이션 마법사 - 결과 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="54747-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="54747-138">Hello에 **대상 서버 연결 설정** 페이지에서 클릭 **tooServer 연결**, hello 세부 정보를 다음과 같이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="54747-139">**서버 이름**: 대상 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="54747-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="54747-140">**인증**: **SQL Server 인증**</span><span class="sxs-lookup"><span data-stu-id="54747-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="54747-141">로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="54747-142">**데이터베이스**: **마스터 DB(모든 데이터베이스를 나열)**.</span><span class="sxs-lookup"><span data-stu-id="54747-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="54747-143">이 옵션은 hello 대상 서버에서 모든 hello 데이터베이스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-143">This option lists all hello databases on hello target server.</span></span>
     
     ![SQL 데이터베이스 마이그레이션 마법사 - 대상 서버 연결 설정](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="54747-145">클릭 **연결**선택, toomove hello 테이블을 클릭 한 다음 hello 대상 데이터베이스 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="54747-146">Hello 이전에 생성 된 스크립트를 실행을 완료 해야이 하 고 hello 복사한 toohello 대상 데이터베이스 테이블을 새로 이동 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54747-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="54747-147">확인 단계</span><span class="sxs-lookup"><span data-stu-id="54747-147">Verification step</span></span>

- <span data-ttu-id="54747-148">쿼리하고 새로 복사 hello 테이블 toomake hello 데이터가 그대로 유지 되는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="54747-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="54747-149">이름을 바꿀 hello 테이블 형식에 따라 삭제할 수 있습니다 **준비 단계** 섹션.</span><span class="sxs-lookup"><span data-stu-id="54747-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="54747-150">(예를 들어 &lt;테이블 이름&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="54747-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54747-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54747-151">Next steps</span></span>
[<span data-ttu-id="54747-152">SQL 데이터베이스 자동 백업</span><span class="sxs-lookup"><span data-stu-id="54747-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

