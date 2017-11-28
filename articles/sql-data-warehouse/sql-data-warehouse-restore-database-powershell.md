---
title: "Azure SQL Data Warehouse 복원(PowerShell) | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 복원을 위한 PowerShell 작업."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="5ad1c-103">Azure SQL 데이터 웨어하우스 복원(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5ad1c-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5ad1c-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="5ad1c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="5ad1c-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="5ad1c-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="5ad1c-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="5ad1c-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="5ad1c-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="5ad1c-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="5ad1c-108">이 문서에서는 PowerShell을 사용하여 Azure SQL 데이터 웨어하우스를 복원하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ad1c-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5ad1c-109">Before you begin</span></span>
<span data-ttu-id="5ad1c-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ad1c-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="5ad1c-111">각 SQL 데이터 웨어하우스는 기본 DTU 할당량이 있는 SQL server (예: myserver.database.windows.net)에 의해 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="5ad1c-112">SQL 데이터 웨어하우스를 복원하기 전에 SQL 서버에 복원 중인 데이터베이스에 대해 충분한 DTU 할당량이 남아 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="5ad1c-113">필요한 DTU를 계산하거나 더 많은 DTU를 요청하는 방법을 알아보려면 [DTU 할당량 변경 요청][Request a DTU quota change]을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="5ad1c-114">PowerShell 설치 </span><span class="sxs-lookup"><span data-stu-id="5ad1c-114">Install PowerShell</span></span>
<span data-ttu-id="5ad1c-115">SQL 데이터 웨어하우스에서 Azure PowerShell을 사용하려면 Azure PowerShell 버전 1.0 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="5ad1c-116">**Get-Module -ListAvailable -Name AzureRM**을 실행하여 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="5ad1c-117">최신 버전은 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="5ad1c-118">최신 버전 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법][How to install and configure Azure PowerShell]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="5ad1c-119">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="5ad1c-119">Restore an active or paused database</span></span>
<span data-ttu-id="5ad1c-120">스냅숏에서 데이터베이스를 복원하려면 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="5ad1c-121">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="5ad1c-122">Azure 계정에 연결하고 사용자 계정과 연결된 모든 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="5ad1c-123">복원할 데이터베이스가 포함된 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="5ad1c-124">데이터베이스의 복원 지점을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="5ad1c-125">RestorePointCreationDate를 사용하여 원하는 복원 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="5ad1c-126">데이터베이스를 원하는 복원 지점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="5ad1c-127">복원된 데이터베이스가 온라인 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="5ad1c-128">복원이 완료된 후 [복구 후 데이터베이스 구성][Configure your database after recovery]에 따라 복구된 데이터베이스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="5ad1c-129">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="5ad1c-129">Restore a deleted database</span></span>
<span data-ttu-id="5ad1c-130">삭제된 데이터베이스를 복원하려면 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="5ad1c-131">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="5ad1c-132">Azure 계정에 연결하고 사용자 계정과 연결된 모든 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="5ad1c-133">복원할 삭제된 데이터베이스가 포함된 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="5ad1c-134">삭제된 특정 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="5ad1c-135">삭제된 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="5ad1c-136">복원된 데이터베이스가 온라인 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="5ad1c-137">복원이 완료된 후 [복구 후 데이터베이스 구성][Configure your database after recovery]에 따라 복구된 데이터베이스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="5ad1c-138">Azure 지역에서 복원</span><span class="sxs-lookup"><span data-stu-id="5ad1c-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="5ad1c-139">데이터베이스를 복구하려면 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="5ad1c-140">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="5ad1c-141">Azure 계정에 연결하고 사용자 계정과 연결된 모든 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="5ad1c-142">복원할 데이터베이스가 포함된 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="5ad1c-143">복구하려는 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="5ad1c-144">데이터베이스 복구 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="5ad1c-145">지역에서 복원된 데이터베이스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="5ad1c-146">복원이 완료된 후에 데이터베이스를 구성하려면 [복구 후 데이터베이스 구성][Configure your database after recovery]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="5ad1c-147">원본 데이터베이스가 TDE를 사용할 수 있는 경우 복구된 데이터베이스도 TDE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ad1c-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ad1c-148">Next steps</span></span>
<span data-ttu-id="5ad1c-149">Azure SQL Database 버전의 무중단 업무 방식 기능에 대해 알아보려면 [Azure SQL Database 무중단 업무 방식 개요][Azure SQL Database business continuity overview]를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="5ad1c-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
