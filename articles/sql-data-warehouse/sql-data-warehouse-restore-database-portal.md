---
title: "Azure SQL Data Warehouse 복원(Azure Portal) | Microsoft Docs"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="e4892-103">Azure SQL Data Warehouse 복원(포털)</span><span class="sxs-lookup"><span data-stu-id="e4892-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e4892-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="e4892-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e4892-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="e4892-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="e4892-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="e4892-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="e4892-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="e4892-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="e4892-108">이 문서에서는 Azure Portal을 사용하여 Azure SQL Data Warehouse를 복원하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e4892-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e4892-109">Before you begin</span></span>
<span data-ttu-id="e4892-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4892-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="e4892-111">SQL Data Warehouse의 각 인스턴스는 기본 DTU(데이터 처리량 단위) 할당량이 있는 SQL Server(예 : myserver.database.windows.net)에 의해 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="e4892-112">SQL Data Warehouse를 복원하기 전에 SQL Server에 복원 중인 데이터베이스에 대해 충분한 DTU 할당량이 남아 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="e4892-113">DTU 할당량을 계산하거나 더 많은 DTU를 요청하는 방법을 알아보려면 [DTU 할당량 변경 요청][Request a DTU quota change]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4892-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="e4892-114">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="e4892-114">Restore an active or paused database</span></span>
<span data-ttu-id="e4892-115">데이터베이스를 복원하려면</span><span class="sxs-lookup"><span data-stu-id="e4892-115">To restore a database:</span></span>

1. <span data-ttu-id="e4892-116">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e4892-117">왼쪽 창에서 **찾아보기**를 선택한 다음 **SQL Servers**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="e4892-119">서버를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-119">Find your server, and then select it.</span></span>

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="e4892-121">복원하려는 SQL Data Warehouse 인스터스를 찾아서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![복원할 SQL Data Warehouse의 인스턴스 선택](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="e4892-123">Data Warehouse 블레이드의 위쪽에서 **복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![복원 선택](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="e4892-125">새 **데이터베이스 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="e4892-126">최신 **복원 지점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="e4892-127">최신 복원 지점을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="e4892-128">복원 지점은 UTC(협정 세계시)로 표시되기 때문에 기본 옵션이 최신 복원 지점이 아닐 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![복원 지점 선택](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="e4892-130">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-130">Select **OK**.</span></span>
9. <span data-ttu-id="e4892-131">데이터베이스 복원 프로세스가 시작되고 **알림**을 사용하여 프로세스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="e4892-132">복원이 완료된 후 [복구 후 데이터베이스 구성][Configure your database after recovery]에 따라 복구된 데이터베이스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="e4892-133">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="e4892-133">Restore a deleted database</span></span>
<span data-ttu-id="e4892-134">삭제된 데이터베이스를 복원하려면:</span><span class="sxs-lookup"><span data-stu-id="e4892-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="e4892-135">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e4892-136">왼쪽 창에서 **찾아보기**를 선택한 다음 **SQL Servers**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![찾아보기 > SQL Servers 선택](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="e4892-138">서버를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-138">Find your server, and then select it.</span></span>

    ![서버 선택](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="e4892-140">서버 블레이드의 **작업** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="e4892-141">**삭제된 데이터베이스** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-141">Select the **Deleted databases** tile.</span></span>

    ![삭제된 데이터베이스 타일 선택](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="e4892-143">복원할 삭제된 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-143">Select the deleted database that you want to restore.</span></span>

    ![복원할 데이터베이스 선택](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="e4892-145">새 **데이터베이스 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-145">Specify a new **Database name**.</span></span>

    ![데이터베이스에 대한 이름 추가](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="e4892-147">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-147">Select **OK**.</span></span>
9. <span data-ttu-id="e4892-148">데이터베이스 복원 프로세스가 시작되고 **알림**을 사용하여 프로세스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4892-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="e4892-149">복원이 완료된 후에 데이터베이스를 구성하려면 [복구 후 데이터베이스 구성][Configure your database after recovery]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4892-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e4892-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4892-150">Next steps</span></span>
<span data-ttu-id="e4892-151">Azure SQL Database 버전의 무중단 업무 방식 기능에 대해 알아보려면 [Azure SQL Database 무중단 업무 방식 개요][Azure SQL Database business continuity overview]를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="e4892-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
