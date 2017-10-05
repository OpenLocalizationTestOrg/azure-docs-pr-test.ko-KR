---
title: "Azure SQL Data Warehouse 복원(REST API) | Microsoft Docs"
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="9dfa9-103">Azure SQL 데이터 웨어하우스 복원(REST API)</span><span class="sxs-lookup"><span data-stu-id="9dfa9-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9dfa9-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="9dfa9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="9dfa9-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="9dfa9-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="9dfa9-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="9dfa9-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="9dfa9-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="9dfa9-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="9dfa9-108">이 문서에서는 REST API를 사용하여 Azure SQL 데이터 웨어하우스를 복원하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9dfa9-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9dfa9-109">Before you begin</span></span>
<span data-ttu-id="9dfa9-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="9dfa9-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="9dfa9-111">각 SQL 데이터 웨어하우스는 기본 DTU 할당량이 있는 SQL server (예: myserver.database.windows.net)에 의해 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="9dfa9-112">SQL 데이터 웨어하우스를 복원하기 전에 SQL 서버에 복원 중인 데이터베이스에 대해 충분한 DTU 할당량이 남아 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="9dfa9-113">필요한 DTU를 계산하거나 더 많은 DTU를 요청하는 방법을 알아보려면 [DTU 할당량 변경 요청][Request a DTU quota change]을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="9dfa9-114">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="9dfa9-114">Restore an active or paused database</span></span>
<span data-ttu-id="9dfa9-115">데이터베이스를 복원하려면</span><span class="sxs-lookup"><span data-stu-id="9dfa9-115">To restore a database:</span></span>

1. <span data-ttu-id="9dfa9-116">데이터베이스 복원 지점 가져오기 작업을 사용하여 데이터베이스 복원 지점 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="9dfa9-117">[데이터베이스 복원 요청 만들기][Create database restore request] 작업을 사용하여 복원을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="9dfa9-118">[데이터베이스 작업 상태][Database operation status] 작업을 사용하여 복원 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="9dfa9-119">복원이 완료된 후 [복구 후 데이터베이스 구성][Configure your database after recovery]에 따라 복구된 데이터베이스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="9dfa9-120">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="9dfa9-120">Restore a deleted database</span></span>
<span data-ttu-id="9dfa9-121">삭제된 데이터베이스를 복원하려면:</span><span class="sxs-lookup"><span data-stu-id="9dfa9-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="9dfa9-122">[복원 가능한 삭제된 데이터베이스 나열][List restorable dropped databases] 작업을 사용하여 복원 가능한 모든 삭제된 데이터베이스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="9dfa9-123">[복원 가능한 삭제된 데이터베이스 가져오기][Get restorable dropped database] 작업을 사용하여 복원하려는 삭제된 데이터베이스에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="9dfa9-124">[데이터베이스 복원 요청 만들기][Create database restore request] 작업을 사용하여 복원을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="9dfa9-125">[데이터베이스 작업 상태][Database operation status] 작업을 사용하여 복원 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="9dfa9-126">복원이 완료된 후에 데이터베이스를 구성하려면 [복구 후 데이터베이스 구성][Configure your database after recovery]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9dfa9-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dfa9-127">Next steps</span></span>
<span data-ttu-id="9dfa9-128">Azure SQL Database 버전의 무중단 업무 방식 기능에 대해 알아보려면 [Azure SQL Database 무중단 업무 방식 개요][Azure SQL Database business continuity overview]를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="9dfa9-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
