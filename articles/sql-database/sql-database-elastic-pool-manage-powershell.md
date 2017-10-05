---
title: "PowerShell: Azure SQL 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "PowerShell을 사용하여 탄력적 풀을 관리하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="b4123-103">PowerShell을 사용하여 탄력적 풀 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="b4123-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="b4123-104">이 항목에서는 PowerShell을 사용하여 확장 가능한 [탄력적 풀](sql-database-elastic-pool.md)을 만들고 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="b4123-105">[Azure Portal](https://portal.azure.com/), REST API 또는 [C#](sql-database-elastic-pool-manage-csharp.md)을 사용하여 Azure 탄력적 풀을 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="b4123-106">[Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="b4123-107">탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="b4123-107">Create an elastic pool</span></span>
<span data-ttu-id="b4123-108">[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet을 사용하여 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="b4123-109">풀, 최소 및 최대 DTU당 eDTU 값은 서비스 계층 값(Basic, Standard, Premium 또는 Premium RS)에 의해 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="b4123-110">[탄력적 풀 및 풀링된 데이터베이스에 대한 eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="b4123-111">탄력적 풀에 풀링된 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b4123-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="b4123-112">[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet을 사용하고 **ElasticPoolName** 매개 변수를 대상 풀로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="b4123-113">기존 데이터베이스를 탄력적 풀로 이동하려면 [데이터베이스를 탄력적 풀로 이동](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="b4123-114">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="b4123-114">Complete script</span></span>
<span data-ttu-id="b4123-115">이 스크립트는 Azure 리소스 그룹 및 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="b4123-116">대화 상자가 나타나면 (Azure 자격 증명 아닌) 새 서버에 대한 관리자 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="b4123-117">탄력적 풀을 만들기 및 풀링된 여러 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="b4123-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="b4123-118">탄력적 풀에 많은 수의 데이터베이스를 만드는 작업은 한 번에 단일 데이터베이스만을 만들 수 있는 포털 또는 PowerShell cmdlet을 사용하는 경우와 같은 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="b4123-119">탄력적 풀로 만들기를 자동화하려면 [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="b4123-120">탄력적 풀로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="b4123-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="b4123-121">[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)를 사용하여 데이터베이스를 탄력적 풀에 넣거나 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="b4123-122">탄력적 풀의 성능 설정 변경</span><span class="sxs-lookup"><span data-stu-id="b4123-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="b4123-123">성능이 저하되는 경우 규모 증가에 맞게 풀의 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="b4123-124">[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="b4123-125">-Dtu 매개 변수를 풀당 eDTU로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="b4123-126">가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="b4123-127">탄력적 풀에 대한 저장소 한도 변경</span><span class="sxs-lookup"><span data-stu-id="b4123-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="b4123-128">[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet을 사용하여 _-StorageMB_ 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="b4123-129">저장소 한도(MB)를 제공합니다(예를 들어 2097152는 2TB의 저장소 한도를 설정).</span><span class="sxs-lookup"><span data-stu-id="b4123-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="b4123-130">가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4123-131">1500eDTU 이상인 프리미엄 풀에 대한 풀당 기본 최대 데이터 저장소는 750GB입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="b4123-132">_풀당 최대 데이터 저장소 크기_를 증가시키려면 이 저장소 한도를 명시적으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="b4123-133">750GB 이상의 저장소가 있는 프리미엄 풀은 현재 미국 동부 2, 미국 서부, 미국 버지니아 주 정부, 유럽 서부, 독일 중부, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중부 및 캐나다 동부 지역에서 현재 공개 미리 보기 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="b4123-134">풀 관련 작업 상태 확인</span><span class="sxs-lookup"><span data-stu-id="b4123-134">Get the status of pool operations</span></span>
<span data-ttu-id="b4123-135">탄력적 풀을 만드는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="b4123-136">[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet을 사용하여 생성 및 업데이트를 포함한 풀 작업의 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="b4123-137">데이터베이스를 탄력적 풀에 넣거나 뺄 때의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="b4123-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="b4123-138">데이터베이스를 이동하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-138">Moving a database can take time.</span></span> <span data-ttu-id="b4123-139">[Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet을 사용하여 이동 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="b4123-140">탄력적 풀에 대한 리소스 사용량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4123-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="b4123-141">원본 풀 한도의 백분율로 검색할 수 있는 메트릭:</span><span class="sxs-lookup"><span data-stu-id="b4123-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="b4123-142">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="b4123-142">Metric name</span></span> | <span data-ttu-id="b4123-143">설명</span><span class="sxs-lookup"><span data-stu-id="b4123-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b4123-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="b4123-144">cpu\_percent</span></span> |<span data-ttu-id="b4123-145">풀 한도의 백분율로 평균 계산 사용률</span><span class="sxs-lookup"><span data-stu-id="b4123-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="b4123-146">실제\_데이터\_읽기\_%</span><span class="sxs-lookup"><span data-stu-id="b4123-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="b4123-147">풀 한도에 따른 백분율로 평균 I/O 사용률</span><span class="sxs-lookup"><span data-stu-id="b4123-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b4123-148">로그\_쓰기\_%</span><span class="sxs-lookup"><span data-stu-id="b4123-148">log\_write\_percent</span></span> |<span data-ttu-id="b4123-149">풀 한도의 백분율로 평균 쓰기 리소스 사용률</span><span class="sxs-lookup"><span data-stu-id="b4123-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="b4123-150">DTU\_소비\_%</span><span class="sxs-lookup"><span data-stu-id="b4123-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="b4123-151">풀에 대한 eDTU 한도의 백분율로 평균 eDTU 사용률</span><span class="sxs-lookup"><span data-stu-id="b4123-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="b4123-152">저장소\_percent</span><span class="sxs-lookup"><span data-stu-id="b4123-152">storage\_percent</span></span> |<span data-ttu-id="b4123-153">풀의 저장소 한도의 백분율로 평균 저장소 사용률</span><span class="sxs-lookup"><span data-stu-id="b4123-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="b4123-154">작업 자\_%</span><span class="sxs-lookup"><span data-stu-id="b4123-154">workers\_percent</span></span> |<span data-ttu-id="b4123-155">풀의 한도에 따른 백분율로 최대 동시 작업자(요청)</span><span class="sxs-lookup"><span data-stu-id="b4123-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b4123-156">세션\_%</span><span class="sxs-lookup"><span data-stu-id="b4123-156">sessions\_percent</span></span> |<span data-ttu-id="b4123-157">풀의 한도에 따른 백분율로 최대 동시 세션</span><span class="sxs-lookup"><span data-stu-id="b4123-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b4123-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="b4123-158">eDTU_limit</span></span> |<span data-ttu-id="b4123-159">이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 DTU 설정</span><span class="sxs-lookup"><span data-stu-id="b4123-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="b4123-160">저장소\_제한</span><span class="sxs-lookup"><span data-stu-id="b4123-160">storage\_limit</span></span> |<span data-ttu-id="b4123-161">이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 저장소 제한 설정(MB)</span><span class="sxs-lookup"><span data-stu-id="b4123-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="b4123-162">eDTU\_사용</span><span class="sxs-lookup"><span data-stu-id="b4123-162">eDTU\_used</span></span> |<span data-ttu-id="b4123-163">이 간격에 풀에서 사용한 평균 eDTU</span><span class="sxs-lookup"><span data-stu-id="b4123-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="b4123-164">저장소\_사용</span><span class="sxs-lookup"><span data-stu-id="b4123-164">storage\_used</span></span> |<span data-ttu-id="b4123-165">이 간격에 풀에서 사용한 평균 저장소(바이트)</span><span class="sxs-lookup"><span data-stu-id="b4123-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="b4123-166">**메트릭 세분성/보존 기간:**</span><span class="sxs-lookup"><span data-stu-id="b4123-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="b4123-167">데이터는 5분 단위로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="b4123-168">데이터 보존 기간은 35일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="b4123-169">이 cmdlet 및 API는 한 번의 호출로 검색할 수 있는 행의 수를 1000행(5분 단위로 약 3일치 데이터)으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="b4123-170">하지만 이 명령을 서로 다른 시작/종료 시간 간격으로 여러 번 호출하여 더 많은 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="b4123-171">메트릭을 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="b4123-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="b4123-172">탄력적 풀에서 데이터베이스의 리소스 사용량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4123-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="b4123-173">이러한 API는 단일 데이터베이스의 리소스 사용률을 모니터링하는 데 사용되는 API와 동일합니다. 단, 의미 체계 측면에서, 검색된 메트릭이 해당 풀에 대해 설정된 데이터베이스당 최대 eDTU 백분율(또는 CPU나 IO와 같은 기본 메트릭에 대해 동급의 용량)로 표시된다는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="b4123-174">예를 들어, 이 메트릭에서 50% 사용률은 특정 리소스 사용률이 상위 풀의 리소스에 대한 데이터베이스당 최대값 한도의 50%임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="b4123-175">메트릭을 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="b4123-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="b4123-176">탄력적 풀 리소스에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="b4123-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="b4123-177">탄력적 풀에 경고 규칙을 추가하여 탄력적 풀이 설정한 사용률 임계값에 도달할 경우 [URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx)에 전자 메일 알림 또는 경고 문자열을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="b4123-178">Add-AzureRmMetricAlertRule cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4123-179">탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="b4123-180">탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="b4123-181">마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="b4123-182">탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="b4123-183">이 예제에서는 탄력적 풀의 eDTU 소비가 특정 임계값을 초과할 때 알림을 받기 위해 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="b4123-184">자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4123-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="b4123-185">탄력적 풀의 모든 데이터베이스에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="b4123-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="b4123-186">탄력적 풀의 모든 데이터베이스에 경고 규칙을 추가하여 리소스가 경고에 의해 설정된 사용률 임계값에 도달할 경우 [URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx) 에 전자 메일 알림 또는 경고 문자열을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4123-187">탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="b4123-188">탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="b4123-189">마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="b4123-190">탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="b4123-191">이 예제에서는 해당 데이터베이스의 DTU 사용량이 지정된 특정 임계값을 초과할 경우 알림을 받기 위해 탄력적 풀의 각 데이터베이스에 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="b4123-192">구독에서 여러 풀에 걸친 리소스 사용 데이터 수집 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="b4123-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="b4123-193">구독에 데이터베이스가 많은 경우 각 탄력적 풀을 개별적으로 모니터링하는 작업은 번거롭습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="b4123-194">대신, 리소스 사용량을 모니터링하고 분석하기 위해 여러 풀 및 해당 데이터베이스에서 리소스 사용 데이터를 수집하기 위해 SQL 데이터베이스 PowerShell cmdlet 및 T-SQL 쿼리를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="b4123-195">이러한 일련의 Powershell 스크립트의 [샘플 구현](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) 은 작동 내용 및 사용 방법에 대한 설명서와 함께 GitHub SQL Server 샘플 리포지토리에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="b4123-196">이 샘플 구현을 사용하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="b4123-197">[스크립트 및 설명서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="b4123-198">사용자 환경에 대한 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="b4123-199">탄력적 풀이 호스팅되는 하나 이상의 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="b4123-200">수집된 메트릭을 저장할 원격 분석 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="b4123-201">스크립트의 실행 기간을 지정하는 스크립트를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="b4123-202">높은 수준에서 스크립트는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="b4123-203">지정된 Azure 구독(또는 지정된 서버 목록)에 모든 서버를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="b4123-204">각 서버에 대한 백그라운드 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-204">Runs a background job for each server.</span></span> <span data-ttu-id="b4123-205">작업은 일정한 간격으로 루프에서 실행되고 서버에서 모든 풀에 대한 원격 분석 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="b4123-206">그러면 지정된 원격 분석 데이터베이스에 수집된 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="b4123-207">각 풀에서 데이터베이스의 목록을 열거하여 데이터베이스 리소스 사용 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="b4123-208">그러면 원격 분석 데이터베이스에 수집된 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="b4123-209">탄력적 풀 및 해당 데이터베이스의 상태를 모니터링하도록 원격 분석 데이터베이스에서 수집된 메트릭을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="b4123-210">또한 스크립트는 원격 분석 데이터베이스에 미리 정의된 TVF(테이블 값 함수)를 설치하여 지정된 기간 동안 메트릭을 집계하도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="b4123-211">예를 들어 TVF의 결과는 "주어진 기간에 최대 eDTU 사용률을 포함한 상위 N개의 탄력적 풀 창"을 표시하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="b4123-212">필요에 따라 Excel 또는 Power BI와 같은 분석 도구를 사용하여 수집된 데이터를 쿼리하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="b4123-213">예제: 탄력적 풀 및 해당 데이터베이스에 대한 리소스 사용 메트릭 검색</span><span class="sxs-lookup"><span data-stu-id="b4123-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="b4123-214">이 예에서는 지정된 탄력적 풀 및 모든 데이터베이스에 대한 사용 메트릭을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="b4123-215">수집된 데이터는 형식이 지정되어 .csv 형식 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="b4123-216">이 파일은 Excel에서 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="b4123-217">탄력적 풀 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="b4123-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="b4123-218">데이터베이스당 최소 eDTU 또는 데이터베이스당 최대 eDTU를 변경하는 작업은 일반적으로 5분 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="b4123-219">풀당 eDTU를 변경하는 작업은 풀에 있는 모든 데이터베이스에서 사용한 공간의 전체 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="b4123-220">변경 시간은 100GB당 평균 90분 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="b4123-221">예를 들어 풀에 있는 모든 데이터베이스에서 사용 중인 총 공간이 200GB일 경우, 풀당 풀 eDTU를 변경하는 예상 대기 시간은 3시간 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b4123-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4123-222">Next steps</span></span>
* <span data-ttu-id="b4123-223">[탄력적 작업 만들기](sql-database-elastic-jobs-overview.md) 탄력적 작업은 풀의 데이터베이스 개수에 관계없이 T-SQL 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="b4123-224">[Azure SQL 데이터베이스를 사용하여 규모 확장](sql-database-elastic-scale-introduction.md)참조: 탄력적 도구를 사용하여 규모를 확장하거나 데이터를 이동하거나 쿼리 또는 트랜잭션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4123-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
