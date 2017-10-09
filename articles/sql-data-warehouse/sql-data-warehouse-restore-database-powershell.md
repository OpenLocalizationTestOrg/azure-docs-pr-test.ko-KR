---
title: "Azure SQL 데이터 웨어하우스 (PowerShell) aaaRestore | Microsoft Docs"
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="96542-103">Azure SQL 데이터 웨어하우스 복원(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="96542-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="96542-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="96542-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="96542-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="96542-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="96542-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="96542-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="96542-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="96542-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="96542-108">이 문서에서 어떻게 toorestore는 Azure SQL 데이터 웨어하우스 PowerShell을 사용 하 여 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="96542-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96542-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="96542-109">Before you begin</span></span>
<span data-ttu-id="96542-110">**DTU 용량을 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="96542-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="96542-111">각 SQL 데이터 웨어하우스는 기본 DTU 할당량이 있는 SQL server (예: myserver.database.windows.net)에 의해 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="96542-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="96542-112">SQL 데이터 웨어하우스를 복원 하려면 먼저 SQL 서버 hello 복원 중인 데이터베이스에 대 한 나머지 충분 한 DTU 할당량에 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="96542-113">toolearn toorequest 또는 toocalculate DTU는 데 필요한 방법을 더 많은 DTU 참조 [DTU 할당량 변경 요청][Request a DTU quota change]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="96542-114">PowerShell 설치 </span><span class="sxs-lookup"><span data-stu-id="96542-114">Install PowerShell</span></span>
<span data-ttu-id="96542-115">순서 toouse SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell 1.0 이상 tooinstall Azure PowerShell 버전을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="96542-116">**Get-Module -ListAvailable -Name AzureRM**을 실행하여 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96542-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="96542-117">hello 최신 버전에서 설치 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="96542-118">Hello 최신 버전의 설치에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="96542-119">활성 또는 일시 중지된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="96542-119">Restore an active or paused database</span></span>
<span data-ttu-id="96542-120">데이터베이스 스냅숏에서 toorestore hello를 사용 하 여 [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96542-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="96542-121">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96542-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="96542-122">Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="96542-123">Hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="96542-124">목록 hello hello 데이터베이스에 대 한 포인트를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="96542-125">RestorePointCreationDate hello를 사용 하 여 원하는 hello 복원 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="96542-126">Hello, 원하는 toohello 복원 지점을 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="96542-127">복원 하는 hello 온라인 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="96542-128">Hello 복원이 완료 된 후 수행 하 여 복구 된 데이터베이스를 구성할 수 있습니다 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="96542-129">삭제된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="96542-129">Restore a deleted database</span></span>
<span data-ttu-id="96542-130">삭제 된 데이터베이스는 toorestore hello를 사용 하 여 [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96542-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="96542-131">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96542-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="96542-132">Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="96542-133">삭제 하는 hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="96542-134">삭제 hello 특정 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="96542-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="96542-135">Hello 삭제 된 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="96542-136">복원 하는 hello 온라인 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="96542-137">Hello 복원이 완료 된 후 수행 하 여 복구 된 데이터베이스를 구성할 수 있습니다 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="96542-138">Azure 지역에서 복원</span><span class="sxs-lookup"><span data-stu-id="96542-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="96542-139">toorecover 데이터베이스를 사용 하 여 hello [복원 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96542-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="96542-140">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96542-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="96542-141">Azure 계정 tooyour를 연결 하 고 사용자 계정과 연결 된 모든 hello 구독 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="96542-142">Hello 데이터베이스 toobe 복원할를 포함 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="96542-143">Toorecover를 hello 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="96542-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="96542-144">Hello 데이터베이스에 대 한 hello 복구 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96542-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="96542-145">Hello 지리적 복원 된 데이터베이스의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="96542-146">tooconfigure hello 복원이 완료 된 후 데이터베이스 참조 [복구 후 데이터베이스를 구성할][Configure your database after recovery]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="96542-147">복구 된 데이터베이스 hello hello 원본 데이터베이스는 TDE 사용 하도록 설정 하는 경우 TDE 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96542-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96542-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96542-148">Next steps</span></span>
<span data-ttu-id="96542-149">Azure SQL 데이터베이스 버전의 hello 비즈니스 연속성 기능에 대 한 toolearn 읽으십시오 hello [Azure SQL 데이터베이스 비즈니스 연속성 개요][Azure SQL Database business continuity overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="96542-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
