---
title: "Azure SQL Database 백업에서 단일 테이블 복원 | Microsoft Docs"
description: "Azure SQL 데이터베이스 백업에서 단일 테이블을 복원하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="edc4b-103">Azure SQL 데이터베이스 백업에서 단일 테이블을 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="edc4b-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="edc4b-104">SQL 데이터베이스의 일부 데이터를 실수로 변경했지만 이제 영향을 받는 단일 테이블을 복구하려는 상황에 처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="edc4b-105">이 문서에서는 SQL 데이터베이스 [자동 백업](sql-database-automated-backups.md)중 하나에서 데이터베이스의 단일 테이블을 복원하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="edc4b-106">준비 단계: 테이블 이름 바꾸기 및 데이터베이스의 복사본 복원</span><span class="sxs-lookup"><span data-stu-id="edc4b-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="edc4b-107">복원된 복사본으로 대체하려는 Azure SQL 데이터베이스의 테이블을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="edc4b-108">Microsoft SQL Management Studio를 사용하여 테이블 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="edc4b-109">예를 들어 테이블의 이름을 &lt;table name&gt;_old로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="edc4b-110">차단되지 않으려면 이름을 바꾸는 테이블에서 실행 중인 작업이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="edc4b-111">문제가 발생하면 유지 관리 기간 동안 이 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="edc4b-112">[지정 지점 복원](sql-database-recovery-using-backups.md#point-in-time-restore) 단계를 사용하여 복구하려는 시점으로 데이터베이스의 백업을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="edc4b-113">복원된 데이터베이스의 이름은 **Adventureworks2012_2016-01-01T22-12Z**와 같은 DBName+TimeStamp 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="edc4b-114">이 단계는 서버에서 기존 데이터베이스 이름을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="edc4b-115">이것은 안전 조치이며 현재 데이터베이스를 삭제하고 프로덕션 사용을 위해 복원된 데이터베이스의 이름을 변경하기 전에 사용자가 복원된 데이터베이스를 확인하려는 용도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="edc4b-116">SQL 데이터베이스 마이그레이션 도구를 사용하여 복원된 데이터베이스에서 테이블 복사</span><span class="sxs-lookup"><span data-stu-id="edc4b-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="edc4b-117">[SQL 데이터베이스 마이그레이션 마법사](https://sqlazuremw.codeplex.com)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="edc4b-118">SQL Database 마이그레이션 마법사를 열고 **프로세스 선택** 페이지에서 **분석/마이그레이션의 데이터베이스**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL 데이터베이스 마이그레이션 마법사 - 프로세스 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="edc4b-120">**서버에 연결** 대화 상자에서 다음 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="edc4b-121">서버 이름: **SQL server**</span><span class="sxs-lookup"><span data-stu-id="edc4b-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="edc4b-122">응용 프로그램: **SQL Server Authentication**</span><span class="sxs-lookup"><span data-stu-id="edc4b-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="edc4b-123">로그인: **로그인**</span><span class="sxs-lookup"><span data-stu-id="edc4b-123">Login: **Your login**</span></span>
   * <span data-ttu-id="edc4b-124">암호: **암호**</span><span class="sxs-lookup"><span data-stu-id="edc4b-124">Password: **Your password**</span></span>
   * <span data-ttu-id="edc4b-125">데이터베이스: **Master DB (모든 데이터베이스 나열)**</span><span class="sxs-lookup"><span data-stu-id="edc4b-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="edc4b-126">기본적으로 마법사는 사용자의 로그인 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="edc4b-127">저장하지 않으려면 **로그인 정보 삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 1단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="edc4b-129">**원본 선택** 대화 상자에서는 **준비 단계** 섹션의 복원된 데이터베이스 이름을 원본으로 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 2단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="edc4b-131">**개체 선택** 대화 상자에서는 **특정 데이터베이스 개체 선택** 옵션을 선택한 다음 대상 서버로 마이그레이션하려는 테이블(다수 가능)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="edc4b-132">![SQL 데이터베이스 마이그레이션 마법사 - 개체 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="edc4b-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="edc4b-133">**스크립트 마법사 요약** 페이지에서 SQL 스크립트를 생성할 준비가 되었는지 묻는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="edc4b-134">또한 나중에 사용할 TSQL 스크립트를 저장하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="edc4b-135">![SQL 데이터베이스 마이그레이션 마법사 - 스크립트 마법사 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="edc4b-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="edc4b-136">**결과 요약** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="edc4b-137">![SQL 데이터베이스 마이그레이션 마법사 - 결과 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="edc4b-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="edc4b-138">**대상 서버 연결 설정** 페이지에서 **서버에 연결**을 클릭한 다음 세부 정보를 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="edc4b-139">**서버 이름**: 대상 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="edc4b-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="edc4b-140">**인증**: **SQL Server 인증**</span><span class="sxs-lookup"><span data-stu-id="edc4b-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="edc4b-141">로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="edc4b-142">**데이터베이스**: **마스터 DB(모든 데이터베이스를 나열)**.</span><span class="sxs-lookup"><span data-stu-id="edc4b-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="edc4b-143">이 옵션은 대상 서버에 있는 모든 데이터베이스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-143">This option lists all the databases on the target server.</span></span>
     
     ![SQL 데이터베이스 마이그레이션 마법사 - 대상 서버 연결 설정](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="edc4b-145">**연결**을 클릭하고 테이블을 이동하려는 대상 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="edc4b-146">이전에 생성된 스크립트의 실행을 완료해야 하고 대상 데이터베이스로 복사된 새로 이동시킨 테이블이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="edc4b-147">확인 단계</span><span class="sxs-lookup"><span data-stu-id="edc4b-147">Verification step</span></span>

- <span data-ttu-id="edc4b-148">새로 복사된 테이블을 쿼리하고 테스트하여 데이터가 그대로 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="edc4b-149">확인되면 이름이 바뀐 테이블 형식 **준비 단계** 섹션을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc4b-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="edc4b-150">(예를 들어 &lt;테이블 이름&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="edc4b-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="edc4b-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edc4b-151">Next steps</span></span>
[<span data-ttu-id="edc4b-152">SQL 데이터베이스 자동 백업</span><span class="sxs-lookup"><span data-stu-id="edc4b-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

