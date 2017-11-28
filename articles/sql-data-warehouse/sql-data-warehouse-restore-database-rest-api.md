---
title: "Azure SQL 데이터 웨어하우스 (REST API) aaaRestore | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 복원을 위한 REST API 작업."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="c7b28-103">Azure SQL 데이터 웨어하우스 복원(REST API)</span><span class="sxs-lookup"><span data-stu-id="c7b28-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c7b28-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="c7b28-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c7b28-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="c7b28-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="c7b28-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c7b28-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="c7b28-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="c7b28-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="c7b28-108">이 문서에서 사용 하 여 Azure SQL 데이터 웨어하우스 toorestore REST API를 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c7b28-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c7b28-109">Before you begin</span></span>
<span data-ttu-id="c7b28-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7b28-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="c7b28-111">각 SQL 데이터 웨어하우스는 기본 DTU 할당량이 있는 SQL server (예: myserver.database.windows.net)에 의해 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="c7b28-112">SQL 데이터 웨어하우스를 복원 하려면 먼저 SQL 서버 hello 복원 중인 데이터베이스에 대 한 나머지 충분 한 DTU 할당량에 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="c7b28-113">toolearn toorequest 또는 toocalculate DTU는 데 필요한 방법을 더 많은 DTU 참조 [DTU 할당량 변경 요청][Request a DTU quota change]합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="c7b28-114">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="c7b28-114">Restore an active or paused database</span></span>
<span data-ttu-id="c7b28-115">toorestore 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="c7b28-115">toorestore a database:</span></span>

1. <span data-ttu-id="c7b28-116">Hello 데이터베이스 복원 지점을 Get 작업을 사용 하 여 데이터베이스 복원 지점 hello 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="c7b28-117">Hello를 사용 하 여 복원 시작 [데이터베이스 복원 요청 만들기] [ Create database restore request] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="c7b28-118">Hello를 사용 하 여 복원의 hello 상태를 추적 [데이터베이스 작업 상태] [ Database operation status] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b28-119">Hello 복원이 완료 된 후 수행 하 여 복구 된 데이터베이스를 구성할 수 있습니다 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="c7b28-120">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="c7b28-120">Restore a deleted database</span></span>
<span data-ttu-id="c7b28-121">삭제 된 데이터베이스는 toorestore:</span><span class="sxs-lookup"><span data-stu-id="c7b28-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="c7b28-122">복원 가능한 삭제 된 데이터베이스의 모든 hello를 사용 하 여 나열 [목록 복원 가능 삭제 데이터베이스] [ List restorable dropped databases] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="c7b28-123">가져오기 hello 세부 정보를 삭제 하는 hello 데이터베이스에 대 한 toorestore hello를 사용 하 여 [Get 복원 가능 삭제 데이터베이스] [ Get restorable dropped database] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="c7b28-124">Hello를 사용 하 여 복원 시작 [데이터베이스 복원 요청 만들기] [ Create database restore request] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="c7b28-125">Hello를 사용 하 여 복원의 hello 상태를 추적 [데이터베이스 작업 상태] [ Database operation status] 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b28-126">tooconfigure hello 복원이 완료 된 후 데이터베이스 참조 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c7b28-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7b28-127">Next steps</span></span>
<span data-ttu-id="c7b28-128">Azure SQL 데이터베이스 버전의 hello 비즈니스 연속성 기능에 대 한 toolearn 읽으십시오 hello [Azure SQL 데이터베이스 비즈니스 연속성 개요][Azure SQL Database business continuity overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b28-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
