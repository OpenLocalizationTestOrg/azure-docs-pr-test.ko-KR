---
title: "Azure SQL 데이터 웨어하우스 (Azure 포털) aaaRestore | Microsoft Docs"
description: "Azure SQL Data Warehouse 복원을 위한 Azure Portal 작업"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="62ad4-103">Azure SQL Data Warehouse 복원(포털)</span><span class="sxs-lookup"><span data-stu-id="62ad4-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="62ad4-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="62ad4-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="62ad4-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="62ad4-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="62ad4-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="62ad4-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="62ad4-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="62ad4-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="62ad4-108">이 문서에서는 toorestore Azure SQL 데이터 웨어하우스를 사용 하 여 Azure 포털을 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62ad4-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="62ad4-109">Before you begin</span></span>
<span data-ttu-id="62ad4-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="62ad4-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="62ad4-111">SQL Data Warehouse의 각 인스턴스는 기본 DTU(데이터 처리량 단위) 할당량이 있는 SQL Server(예 : myserver.database.windows.net)에 의해 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="62ad4-112">SQL 데이터 웨어하우스를 복원 하기 전에 SQL server에 복원 하려는 hello 데이터베이스에 대 한 DTU 할당량이 충분히 남아 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="62ad4-113">toolearn toocalculate DTU 할당량 또는 toorequest 자세한 Dtu 확인 하려면 어떻게 해야 [DTU 할당량 변경 요청][Request a DTU quota change]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="62ad4-114">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="62ad4-114">Restore an active or paused database</span></span>
<span data-ttu-id="62ad4-115">toorestore 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="62ad4-115">toorestore a database:</span></span>

1. <span data-ttu-id="62ad4-116">Toohello 로그인 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="62ad4-117">Hello 왼쪽된 창에서 선택 **찾아보기**를 선택한 후 **SQL server**합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="62ad4-119">서버를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-119">Find your server, and then select it.</span></span>

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="62ad4-121">From, toorestore 원하고 선택 SQL 데이터 웨어하우스의 hello 인스턴스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![SQL 데이터 웨어하우스 toorestore의 hello 인스턴스를 선택 합니다.](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="62ad4-123">데이터 웨어하우스 블레이드 hello의 hello 위쪽 선택 **복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![복원 선택](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="62ad4-125">새 **데이터베이스 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="62ad4-126">선택 hello 최신 **복원 지점을**합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="62ad4-127">Hello 최신 복원 지점을 선택 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="62ad4-128">복원 지점을 utc (협정 세계시)로 표시, 되므로 hello 기본 옵션 hello 최근 복원 지점 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![복원 지점 선택](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="62ad4-130">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-130">Select **OK**.</span></span>
9. <span data-ttu-id="62ad4-131">hello 데이터베이스 복원 프로세스가 시작 됩니다 및 사용 하 여 **알림** toomonitor hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="62ad4-132">수행 하 여 복구 된 데이터베이스를 구성할 수 hello 복원이 완료 된 후 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="62ad4-133">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="62ad4-133">Restore a deleted database</span></span>
<span data-ttu-id="62ad4-134">삭제 된 데이터베이스는 toorestore:</span><span class="sxs-lookup"><span data-stu-id="62ad4-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="62ad4-135">Toohello 로그인 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="62ad4-136">Hello 왼쪽된 창에서 선택 **찾아보기**를 선택한 후 **SQL server**합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="62ad4-138">서버를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-138">Find your server, and then select it.</span></span>

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="62ad4-140">Toohello 아래로 스크롤하여 **작업** 서버 블레이드의 섹션.</span><span class="sxs-lookup"><span data-stu-id="62ad4-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="62ad4-141">선택 hello **삭제 데이터베이스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-141">Select hello **Deleted databases** tile.</span></span>

    ![Hello 삭제 된 데이터베이스 타일을 선택 합니다.](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="62ad4-143">Toorestore hello 삭제 된 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-143">Select hello deleted database that you want toorestore.</span></span>

    ![데이터베이스 toorestore 선택](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="62ad4-145">새 **데이터베이스 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-145">Specify a new **Database name**.</span></span>

    ![Hello 데이터베이스에 대 한 이름을 추가 합니다.](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="62ad4-147">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-147">Select **OK**.</span></span>
9. <span data-ttu-id="62ad4-148">hello 데이터베이스 복원 프로세스가 시작 됩니다 및 사용 하 여 **알림** toomonitor hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="62ad4-149">tooconfigure hello 복원이 완료 된 후 데이터베이스 참조 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="62ad4-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62ad4-150">Next steps</span></span>
<span data-ttu-id="62ad4-151">Azure SQL 데이터베이스 버전을 읽을 hello의 hello 비즈니스 연속성 기능에 대 한 toolearn [Azure SQL 데이터베이스 비즈니스 연속성 개요][Azure SQL Database business continuity overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="62ad4-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
