---
title: "백업에서 Azure SQL Database 복원 | Microsoft Docs"
description: "Azure SQL 데이터베이스를 이전 시점(최대 35일)에 롤백할 수 있는 특정 시점 복원에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 20b33edbb3fade08c0f25e2fd5089b7ebf285fdd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a><span data-ttu-id="fb945-103">자동화된 데이터베이스 백업을 사용하여 Azure SQL 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="fb945-103">Recover an Azure SQL database using automated database backups</span></span>
<span data-ttu-id="fb945-104">SQL Database는 [자동화된 데이터베이스 백업](sql-database-automated-backups.md) 및 [장기 보존에서 백업](sql-database-long-term-retention.md)을 사용한 데이터베이스 복구를 위해 다음 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-104">SQL Database provides these options for database recovery using [automated database backups](sql-database-automated-backups.md) and [backups in long-term retention](sql-database-long-term-retention.md).</span></span> <span data-ttu-id="fb945-105">데이터베이스 백업에서 다음으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-105">You can restore from a database backup to:</span></span>

* <span data-ttu-id="fb945-106">보존 기간 내에 지정된 지점으로 복구된 동일한 논리 서버의 새 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="fb945-106">A new database on the same logical server recovered to a specified point in time within the retention period.</span></span> 
* <span data-ttu-id="fb945-107">삭제된 데이터베이스에 대한 삭제 시간으로 복구된 동일한 논리 서버의 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="fb945-107">A database on the same logical server recovered to the deletion time for a deleted database.</span></span>
* <span data-ttu-id="fb945-108">지역 복제 Blob Storage(RA-GRS)의 최신 매일 백업 지점으로 복구된 지역의 논리 서버에 있는 새 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-108">A new database on any logical server in any region recovered to the point of the most recent daily backups in geo-replicated blob storage (RA-GRS).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb945-109">복원하는 동안 기존 데이터베이스를 덮어쓸 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-109">You cannot overwrite an existing database during restore.</span></span>
>

<span data-ttu-id="fb945-110">[자동화된 데이터베이스 백업](sql-database-automated-backups.md)을 사용하여 모든 지역에 있는 논리 서버에 [데이터베이스 복사본](sql-database-copy.md)을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-110">You can also use [automated database backups](sql-database-automated-backups.md) to create a [database copy](sql-database-copy.md) on any logical server in any region.</span></span> 

## <a name="recovery-time"></a><span data-ttu-id="fb945-111">복구 시간</span><span class="sxs-lookup"><span data-stu-id="fb945-111">Recovery time</span></span>
<span data-ttu-id="fb945-112">자동화된 데이터베이스 백업을 사용하여 데이터베이스를 복원하기 위한 복구 시간은 다음과 같은 다양한 요인의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-112">The recovery time to restore a database using automated database backups is impacted by several factors:</span></span> 

* <span data-ttu-id="fb945-113">데이터베이스의 크기</span><span class="sxs-lookup"><span data-stu-id="fb945-113">The size of the database</span></span>
* <span data-ttu-id="fb945-114">데이터베이스의 성능 수준</span><span class="sxs-lookup"><span data-stu-id="fb945-114">The performance level of the database</span></span>
* <span data-ttu-id="fb945-115">관련된 트랜잭션 로그의 수</span><span class="sxs-lookup"><span data-stu-id="fb945-115">The number of transaction logs involved</span></span>
* <span data-ttu-id="fb945-116">복원 지점으로 복구하기 위해 재생해야 하는 작업의 양</span><span class="sxs-lookup"><span data-stu-id="fb945-116">The amount of activity that needs to be replayed to recover to the restore point</span></span>
* <span data-ttu-id="fb945-117">다른 지역으로 복원되는 경우의 네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="fb945-117">The network bandwidth if the restore is to a different region</span></span> 
* <span data-ttu-id="fb945-118">대상 지역에서 처리되는 동시 복원 요청의 수</span><span class="sxs-lookup"><span data-stu-id="fb945-118">The number of concurrent restore requests being processed in the target region.</span></span> 
  
  <span data-ttu-id="fb945-119">매우 큰 및/또는 활성 데이터베이스의 경우 복원에는 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-119">For a very large and/or active database, the restore may take several hours.</span></span> <span data-ttu-id="fb945-120">지역에서 장시간 가동 중단된 경우 다른 지역에서 많은 수의 지리적 복원 요청이 처리 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-120">If there is prolonged outage in a region, it is possible that there are large numbers of geo-restore requests being processed by other regions.</span></span> <span data-ttu-id="fb945-121">많은 요청이 있는 경우 해당 지역에 데이터베이스의 복구 시간이 늘어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-121">When there are many requests, the recovery time may increase for databases in that region.</span></span> <span data-ttu-id="fb945-122">대부분의 데이터베이스는 12시간 내에 완전히 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-122">Most database restores complete within 12 hours.</span></span>
  
<span data-ttu-id="fb945-123">대량 복원을 위한 기본 제공 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-123">There is no built-in functionality to do bulk restore.</span></span> <span data-ttu-id="fb945-124">[Azure SQL Database: Full Server Recovery](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) 스크립트는 이 작업을 수행하는 한 가지 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-124">The [Azure SQL Database: Full Server Recovery](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script is an example of one way of accomplishing this task.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb945-125">자동화된 백업을 사용하여 복구하려면 구독에서 SQL Server 참여자 역할의 구성원이거나 구독 소유자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-125">To recover using automated backups, you must be a member of the SQL Server Contributor role in the subscription or be the subscription owner.</span></span> <span data-ttu-id="fb945-126">Azure 포털, PowerShell 또는 REST API를 사용하여 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-126">You can recover using the Azure portal, PowerShell, or the REST API.</span></span> <span data-ttu-id="fb945-127">Transact-SQL은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-127">You cannot use Transact-SQL.</span></span> 
> 

## <a name="point-in-time-restore"></a><span data-ttu-id="fb945-128">지정 시간 복원</span><span class="sxs-lookup"><span data-stu-id="fb945-128">Point-In-Time Restore</span></span>

<span data-ttu-id="fb945-129">Azure Portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase) 또는 [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)를 사용하여 동일한 논리 서버에 새 데이터베이스로서 기존 데이터베이스를 이전 시점으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-129">You can restore an existing database to an earlier point in time as a new database on the same logical server using the Azure portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), or the [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="fb945-130">데이터베이스에 대한 특정 시점 복원을 수행하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-130">For a sample PowerShell script showing how to perform a point-in-time restore of a database, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
>

<span data-ttu-id="fb945-131">모든 서비스 계층 또는 성능 수준으로, 단일 데이터베이스로서 또는 탄력적 풀에 데이터베이스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-131">The database can be restored to any service tier or performance level, and as a single database or into an elastic pool.</span></span> <span data-ttu-id="fb945-132">논리 서버 또는 데이터베이스를 복원하는 탄력적 풀에 충분한 리소스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-132">Ensure you have sufficient resources on the logical server or in the elastic pool to which you are restoring the database.</span></span> <span data-ttu-id="fb945-133">완료되면 복원된 데이터베이스는 일반적이고 완벽하게 액세스할 수 있는 온라인 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-133">Once complete, the restored database is a normal, fully accessible, online database.</span></span> <span data-ttu-id="fb945-134">복원된 데이터베이스는 서비스 계층 및 성능 수준에 따라 정상 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-134">The restored database is charged at normal rates based on its service tier and performance level.</span></span> <span data-ttu-id="fb945-135">데이터베이스 복원이 완료될 때까지 요금이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-135">You do not incur charges until the database restore is complete.</span></span>

<span data-ttu-id="fb945-136">일반적으로 복구를 위해 이전 지점까지 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-136">You generally restore a database to an earlier point for recovery purposes.</span></span> <span data-ttu-id="fb945-137">이렇게 하는 경우 원본 데이터베이스에 대한 대체로 복원된 데이터베이스를 처리하거나 데이터를 검색하고 원래 데이터베이스를 업데이트하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-137">When doing so, you can treat the restored database as a replacement for the original database or use it to retrieve data from and then update the original database.</span></span> 

* <span data-ttu-id="fb945-138">***데이터베이스 바꾸기:*** 복원된 데이터베이스를 원래 데이터베이스에 대한 대체로 여기는 경우 성능 수준 및 서비스 계층이 적절한지 확인하고 필요한 경우 데이터베이스의 크기를 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-138">***Database replacement:*** If the restored database is intended as a replacement for the original database, you should verify the performance level and/or service tier are appropriate and scale the database if necessary.</span></span> <span data-ttu-id="fb945-139">원본 데이터베이스의 이름을 바꿀 수 있으며 T-SQL에서 ALTER DATABASE 명령을 사용하여 복원된 데이터베이스에 원래 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-139">You can rename the original database and then give the restored database the original name using the ALTER DATABASE command in T-SQL.</span></span> 
* <span data-ttu-id="fb945-140">***데이터 복구:*** 복원된 데이터베이스에서 데이터를 가져와 사용자 또는 응용 프로그램 오류로부터 복구하려면 복원된 데이터베이스에서 원본 데이터베이스로 데이터를 추출하는 데 필요한 데이터 복구 스크립트를 작성하고 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-140">***Data recovery:*** If you plan to retrieve data from the restored database to recover from a user or application error, you need to write and execute the necessary data recovery scripts to extract data from the restored database to the original database.</span></span> <span data-ttu-id="fb945-141">복원 작업을 완료하는 데 긴 시간이 걸리지만 복원 중인 데이터베이스가 복원 과정 내내 데이터베이스 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-141">Although the restore operation may take a long time to complete, the restoring database is visible in the database list throughout the restore process.</span></span> <span data-ttu-id="fb945-142">복원하는 동안 데이터베이스를 삭제하는 경우 작업이 취소되고 복원이 완료되지 않은 데이터베이스에 대해서는 비용이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-142">If you delete the database during the restore, the restore operation is canceled and you are not charged for the database that did not complete the restore.</span></span> 

### <a name="azure-portal"></a><span data-ttu-id="fb945-143">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fb945-143">Azure portal</span></span>

<span data-ttu-id="fb945-144">Azure Portal을 사용하여 특정 시점으로 복구하려면 데이터베이스에 대한 페이지를 열고 도구 모음에서 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-144">To recover to a point in time using the Azure portal, open the page for your database and click **Restore** on the toolbar.</span></span>

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a><span data-ttu-id="fb945-146">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="fb945-146">Deleted database restore</span></span>
<span data-ttu-id="fb945-147">삭제된 데이터베이스 복원을 사용하면 Azure Portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase) 또는 [REST(createMode=Restore)](https://msdn.microsoft.com/library/azure/mt163685.aspx)를 사용하여 삭제된 데이터베이스를 동일한 논리 서버의 삭제된 데이터베이스에 대한 삭제 시간으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-147">You can restore a deleted database to the deletion time for a deleted database on the same logical server using the Azure portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), or the [REST (createMode=Restore)](https://msdn.microsoft.com/library/azure/mt163685.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="fb945-148">삭제된 데이터베이스를 복원하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-148">For a sample PowerShell script showing how to restore a deleted database, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="fb945-149">Azure SQL Database 서버 인스턴스를 삭제하면 모든 해당 데이터베이스도 삭제되고 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-149">If you delete an Azure SQL Database server instance, all its databases are also deleted and cannot be recovered.</span></span> <span data-ttu-id="fb945-150">현재는 삭제된 서버 복원에 대한 지원이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-150">There is currently no support for restoring a deleted server.</span></span>
> 

### <a name="azure-portal"></a><span data-ttu-id="fb945-151">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fb945-151">Azure portal</span></span>

<span data-ttu-id="fb945-152">Azure Portal을 사용하여 [보존 기간](sql-database-service-tiers.md) 중에 삭제된 데이터베이스를 복구하려면 서버에 대한 페이지를 열고 작업 영역에서 **삭제된 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-152">To recover a deleted database during its [retention period](sql-database-service-tiers.md) using the Azure portal, open the page for your server and in the Operations area, click **Deleted databases**.</span></span>

![삭제된 데이터베이스 복원-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![삭제된 데이터베이스 복원-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a><span data-ttu-id="fb945-155">지역 복원</span><span class="sxs-lookup"><span data-stu-id="fb945-155">Geo-restore</span></span>
<span data-ttu-id="fb945-156">가장 최근의 지리적 복제 전체 및 차등 백업에서 Azure 지역에 있는 모든 서버의 SQL Database를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-156">You can restore a SQL database on any server in any Azure region from the most recent geo-replicated full and differential backups.</span></span> <span data-ttu-id="fb945-157">지리적 복원은 지역 중복 백업을 해당 원본으로 사용하고 가동 중단으로 인해 데이터베이스 또는 데이터 센터에 액세스할 수 없는 경우에도 데이터베이스를 복구하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-157">Geo-restore uses a geo-redundant backup as its source and can be used to recover a database even if the database or datacenter is inaccessible due to an outage.</span></span> 

<span data-ttu-id="fb945-158">지리적 복원은 데이터베이스가 호스팅되는 지역에 사고가 발생하여 데이터베이스를 사용할 수 없게 되었을 때를 위한 기본 복구 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-158">Geo-restore is the default recovery option when your database is unavailable because of an incident in the region where the database is hosted.</span></span> <span data-ttu-id="fb945-159">지역에서 대규모 인시던트로 인해 데이터베이스 응용 프로그램을 사용할 수 없게 되면 지역에서 복제된 백업에서 다른 지역에 있는 서버로 데이터베이스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-159">If a large-scale incident in a region results in unavailability of your database application, you can restore a database from the geo-replicated backups to a server in any other region.</span></span> <span data-ttu-id="fb945-160">차등 백업을 만들 때와 다른 지역에 있는Azure Blob에 지역에서 복제될 때 사이에 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-160">There is a delay between when a differential backup is taken and when it is geo-replicated to an Azure blob in a different region.</span></span> <span data-ttu-id="fb945-161">재해가 발생한 경우 최대 1시간 동안의 데이터가 손실되므로 이 지연은 최대 1시간일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-161">This delay can be up to an hour, so, if a disaster occurs, there can be up to one hour data loss.</span></span> <span data-ttu-id="fb945-162">다음 그림에서는 다른 지역에서 마지막으로 사용할 수 있는 백업에서 데이터베이스의 복원을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-162">The following illustration shows restore of the database from the last available backup in another region.</span></span>

![geo-restore](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> <span data-ttu-id="fb945-164">지역 복원을 수행하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-164">For a sample PowerShell script showing how to perform a geo-restore, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
> 

<span data-ttu-id="fb945-165">지역 보조 복제본에 대한 지정 시간 복원은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-165">Point-in-time restore on a geo-secondary is not currently supported.</span></span> <span data-ttu-id="fb945-166">주 데이터베이스에서만 지정 시간 복원을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-166">Point-in-time restore can be done only on a primary database.</span></span> <span data-ttu-id="fb945-167">지역 복원 기능을 사용하여 가동 중단에서 복구하는 방법에 대한 자세한 내용은 [가동 중단에서 복구](sql-database-disaster-recovery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-167">For detailed information about using geo-restore to recover from an outage, see [Recover from an outage](sql-database-disaster-recovery.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb945-168">백업에서 복원은 RPO와 ERT(예상 복구 시간)가 가장 긴 SQL Database에서 사용할 수 있는 재해 복구 솔루션 중 가장 기본적인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-168">Recovery from backups is the most basic of the disaster recovery solutions available in SQL Database with the longest RPO and Estimate Recovery Time (ERT).</span></span> <span data-ttu-id="fb945-169">기본 데이터베이스를 사용하는 솔루션의 경우 지역에서 복원은 12시간의 ERT에서 적절한 DR 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-169">For solutions using Basic databases, geo-restore is frequently a reasonable DR solution with an ERT of 12 hours.</span></span> <span data-ttu-id="fb945-170">복구 시간을 줄여야 하는 대규모 표준 또는 프리미엄 데이터베이스를 사용하는 솔루션의 경우 [활성 지역 복제](sql-database-geo-replication-overview.md)를 사용하도록 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-170">For solutions using larger Standard or Premium databases that require shorter recovery times, you should consider using [active geo-replication](sql-database-geo-replication-overview.md).</span></span> <span data-ttu-id="fb945-171">활성 지역 복제는 지속적으로 복제된 보조 데이터베이스에 대한 장애 조치를 시작하도록 하여 훨씬 더 낮은 RPO와 ERT를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-171">Active geo-replication offers a much lower RPO and ERT as it only requires you initiate a failover to a continuously replicated secondary.</span></span> <span data-ttu-id="fb945-172">비즈니스 연속성 선택에 대한 자세한 내용은 [비즈니스 연속성](sql-database-business-continuity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-172">For more information on business contiuity choices, see [over of business continuity](sql-database-business-continuity.md).</span></span>
> 

### <a name="azure-portal"></a><span data-ttu-id="fb945-173">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fb945-173">Azure portal</span></span>

<span data-ttu-id="fb945-174">Azure Portal을 사용하여 해당 [보존 기간](sql-database-service-tiers.md) 동안 데이터베이스를 지역 복원하려면 SQL Databases 페이지를 연 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-174">To geo-restore a database during its [retention period](sql-database-service-tiers.md) using the Azure portal, open the SQL Databases page and then click **Add**.</span></span> <span data-ttu-id="fb945-175">**Select source**(소스 선택) 텍스트 상자에서 **백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-175">In the **Select source** text box, select **Backup**.</span></span> <span data-ttu-id="fb945-176">선택한 서버 또는 지역에서 복구를 수행할 백업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-176">Specify the backup from which to perform the recovery in the region and on the server of your choice.</span></span> 

## <a name="programmatically-performing-recovery-using-automated-backups"></a><span data-ttu-id="fb945-177">자동화된 백업을 사용하여 프로그래밍 방식으로 복구 수행</span><span class="sxs-lookup"><span data-stu-id="fb945-177">Programmatically performing recovery using automated backups</span></span>
<span data-ttu-id="fb945-178">앞서 설명한 것처럼 Azure Portal 외에, Azure PowerShell 또는 REST API를 사용하여 데이터베이스 복구를 프로그래밍 방식으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-178">As previously discussed, in addition to the Azure portal, database recovery can be performed programmatically using Azure PowerShell or the REST API.</span></span> <span data-ttu-id="fb945-179">다음 표는 사용 가능한 명령의 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-179">The following tables describe the set of commands available.</span></span>

### <a name="powershell"></a><span data-ttu-id="fb945-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb945-180">PowerShell</span></span>
| <span data-ttu-id="fb945-181">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="fb945-181">Cmdlet</span></span> | <span data-ttu-id="fb945-182">설명</span><span class="sxs-lookup"><span data-stu-id="fb945-182">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fb945-183">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fb945-183">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase) |<span data-ttu-id="fb945-184">하나 이상의 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-184">Gets one or more databases.</span></span> |
| [<span data-ttu-id="fb945-185">Get-AzureRMSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="fb945-185">Get-AzureRMSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="fb945-186">복원할 수 있는 삭제된 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-186">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="fb945-187">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="fb945-187">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |<span data-ttu-id="fb945-188">데이터베이스의 지역 중복 백업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-188">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="fb945-189">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fb945-189">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |<span data-ttu-id="fb945-190">SQL 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-190">Restores a SQL database.</span></span> |
|  | |

### <a name="rest-api"></a><span data-ttu-id="fb945-191">REST API</span><span class="sxs-lookup"><span data-stu-id="fb945-191">REST API</span></span>
| <span data-ttu-id="fb945-192">API</span><span class="sxs-lookup"><span data-stu-id="fb945-192">API</span></span> | <span data-ttu-id="fb945-193">설명</span><span class="sxs-lookup"><span data-stu-id="fb945-193">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fb945-194">REST(createMode=Recovery)</span><span class="sxs-lookup"><span data-stu-id="fb945-194">REST (createMode=Recovery)</span></span>](https://msdn.microsoft.com/library/azure/mt163685.aspx) |<span data-ttu-id="fb945-195">데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-195">Restores a database</span></span> |
| [<span data-ttu-id="fb945-196">데이터베이스 만들기 또는 업데이트 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="fb945-196">Get Create or Update Database Status</span></span>](https://msdn.microsoft.com/library/azure/mt643934.aspx) |<span data-ttu-id="fb945-197">복원 작업 동안 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-197">Returns the status during a restore operation</span></span> |
|  | |

## <a name="summary"></a><span data-ttu-id="fb945-198">요약</span><span class="sxs-lookup"><span data-stu-id="fb945-198">Summary</span></span>
<span data-ttu-id="fb945-199">자동 백업은 사용자 및 응용 프로그램 오류, 우발적인 데이터베이스 삭제 및 장시간의 가동 중단에서 데이터베이스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-199">Automatic backups protect your databases from user and application errors, accidental database deletion, and prolonged outages.</span></span> <span data-ttu-id="fb945-200">이 기본 제공 기능은 모든 서비스 계층 및 성능 수준에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb945-200">This built-in capability is available for all service tiers and performance levels.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fb945-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb945-201">Next steps</span></span>
* <span data-ttu-id="fb945-202">비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="fb945-202">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="fb945-203">Azure SQL 데이터베이스 자동화 백업에 대한 자세한 내용은 [SQL 데이터베이스 자동화 백업](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="fb945-203">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="fb945-204">장기 백업 보존에 대해 알아보려면 [장기 백업 보존](sql-database-long-term-retention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-204">To learn about long-term backup retention, see [Long-term backup retention](sql-database-long-term-retention.md)</span></span>
* <span data-ttu-id="fb945-205">Azure Portal을 사용하여 Azure Recovery Services 자격 증명 모음에서 자동화된 백업의 장기 보존에서 구성, 관리 및 복원하려면 [Configure and use long-term backup retention](sql-database-long-term-backup-retention-configure.md)(장기 백업 보존 관리 구성 및 사용)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-205">To configure, manage, and restore from long-term retention of automated backups in an Azure Recovery Services vault using the Azure portal, see [Configure and use long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span> 
* <span data-ttu-id="fb945-206">빠른 복구 옵션에 대해 알아보려면 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb945-206">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
