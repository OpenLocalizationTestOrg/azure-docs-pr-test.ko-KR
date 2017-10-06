---
title: "PowerShell: Azure SQL 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toouse PowerShell toomanage 탄력적 풀입니다."
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="d2157-103">PowerShell을 사용하여 탄력적 풀 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d2157-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="d2157-104">이 항목에서는 toocreate 하 고 확장 가능한 관리 [탄력적 풀](sql-database-elastic-pool.md) PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="d2157-105">또한 생성 하 고 hello를 사용 하 여 Azure 탄력적 풀 관리 수 [Azure 포털](https://portal.azure.com/), REST API 또는 [C#](sql-database-elastic-pool-manage-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="d2157-106">[Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="d2157-107">탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="d2157-107">Create an elastic pool</span></span>
<span data-ttu-id="d2157-108">hello [새로 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="d2157-109">eDTU 풀, min 및 max Dtu에 대 한 hello 값 (예: Basic, Standard, Premium 또는 프리미엄 RS) hello 서비스 계층 값으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="d2157-110">[탄력적 풀 및 풀링된 데이터베이스에 대한 eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2157-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="d2157-111">탄력적 풀에 풀링된 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d2157-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="d2157-112">사용 하 여 hello [새로 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet 및 집합 hello **ElasticPoolName** toohello 대상 풀 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="d2157-113">기존 데이터베이스를 탄력적 풀으로 toomove 참조 [탄력적 풀에 데이터베이스를 이동](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="d2157-114">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="d2157-114">Complete script</span></span>
<span data-ttu-id="d2157-115">이 스크립트는 Azure 리소스 그룹 및 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="d2157-116">메시지가 나타나면 관리자 사용자 이름 및 암호 hello 새 서버 (하지 Azure 자격 증명)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="d2157-117">탄력적 풀을 만들기 및 풀링된 여러 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="d2157-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="d2157-118">탄력적 풀의 많은 데이터베이스 생성 했으면 다음 hello 포털 또는 한 번에 하나의 데이터베이스만 만드는 PowerShell cmdlet을 사용 하 여 시간을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="d2157-119">참조를 탄력적 풀으로 tooautomate 생성 [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="d2157-120">탄력적 풀로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="d2157-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="d2157-121">내부 또는 외부로 hello로 탄력적 풀 데이터베이스를 이동할 수 [집합 AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="d2157-122">탄력적 풀의 성능 설정 변경</span><span class="sxs-lookup"><span data-stu-id="d2157-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="d2157-123">성능이 저하 되 면 hello 풀 tooaccommodate 성장의 hello 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="d2157-124">사용 하 여 hello [집합 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2157-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="d2157-125">풀 당 hello-Dtu 매개 변수 toohello Edtu를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="d2157-126">가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2157-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="d2157-127">탄력적 풀에 대 한 hello 저장소 용량 한도 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="d2157-128">사용 하 여 hello [집합 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="d2157-129">Hello 저장소 용량 한도 (MB) (예를 들어 2097152 집합 hello 저장소 제한 too2 테라바이트)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="d2157-130">가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2157-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2157-131">이상 1500 Edtu와 풀 프리미엄에 대 한 풀 당 hello 기본 최대 데이터 저장소는 750 GB입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="d2157-132">더 높은 tooobtain hello _최대 풀 당 데이터 저장소 크기_, hello 저장소 용량 한도 명시적으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="d2157-133">프리미엄 750 g B 이상의 저장소 풀은 현재 공개 미리 보기 영역을 다음 hello에: 미국 동부 2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="d2157-134">그룹 작업의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-134">Get hello status of pool operations</span></span>
<span data-ttu-id="d2157-135">탄력적 풀을 만드는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="d2157-136">그룹 작업 만들기 및 업데이트, 사용 하 여 hello 등의 tootrack hello 상태 [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2157-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="d2157-137">내부 / 외부로 탄력적 풀 데이터베이스를 이동 하는 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="d2157-138">데이터베이스를 이동하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-138">Moving a database can take time.</span></span> <span data-ttu-id="d2157-139">Hello를 사용 하 여 이동 상태를 추적 [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2157-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="d2157-140">탄력적 풀에 대한 리소스 사용량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2157-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="d2157-141">Hello 리소스 풀 제한의 백분율로 검색할 수 있는 메트릭:</span><span class="sxs-lookup"><span data-stu-id="d2157-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="d2157-142">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="d2157-142">Metric name</span></span> | <span data-ttu-id="d2157-143">설명</span><span class="sxs-lookup"><span data-stu-id="d2157-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d2157-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="d2157-144">cpu\_percent</span></span> |<span data-ttu-id="d2157-145">Hello 풀의 hello도 비율로 평균 계산 활용률입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-146">실제\_데이터\_읽기\_%</span><span class="sxs-lookup"><span data-stu-id="d2157-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="d2157-147">Hello 풀의 hello 제한을 기준 평균 I/O 활용률입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-148">로그\_쓰기\_%</span><span class="sxs-lookup"><span data-stu-id="d2157-148">log\_write\_percent</span></span> |<span data-ttu-id="d2157-149">평균 쓰기 리소스 활용률 hello 풀의 hello도 비율로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-150">DTU\_소비\_%</span><span class="sxs-lookup"><span data-stu-id="d2157-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="d2157-151">Hello 풀에 대 한 eDTU도 비율로 평균 eDTU 사용량</span><span class="sxs-lookup"><span data-stu-id="d2157-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="d2157-152">저장소\_percent</span><span class="sxs-lookup"><span data-stu-id="d2157-152">storage\_percent</span></span> |<span data-ttu-id="d2157-153">저장소 사용 hello 풀의 hello 저장소 용량 한도의 비율로 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-154">작업 자\_%</span><span class="sxs-lookup"><span data-stu-id="d2157-154">workers\_percent</span></span> |<span data-ttu-id="d2157-155">Hello 풀의 hello 제한을 기준 최대 동시 작업자 (요청 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-156">세션\_%</span><span class="sxs-lookup"><span data-stu-id="d2157-156">sessions\_percent</span></span> |<span data-ttu-id="d2157-157">Hello 풀의 hello 제한을 기준 최대 동시 세션</span><span class="sxs-lookup"><span data-stu-id="d2157-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="d2157-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="d2157-158">eDTU_limit</span></span> |<span data-ttu-id="d2157-159">이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 DTU 설정</span><span class="sxs-lookup"><span data-stu-id="d2157-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="d2157-160">저장소\_제한</span><span class="sxs-lookup"><span data-stu-id="d2157-160">storage\_limit</span></span> |<span data-ttu-id="d2157-161">이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 저장소 제한 설정(MB)</span><span class="sxs-lookup"><span data-stu-id="d2157-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="d2157-162">eDTU\_사용</span><span class="sxs-lookup"><span data-stu-id="d2157-162">eDTU\_used</span></span> |<span data-ttu-id="d2157-163">이 기간에 hello 풀에 사용 된 평균 Edtu 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="d2157-164">저장소\_사용</span><span class="sxs-lookup"><span data-stu-id="d2157-164">storage\_used</span></span> |<span data-ttu-id="d2157-165">Hello 풀 (바이트)이이 기간에 사용 하는 평균 저장소</span><span class="sxs-lookup"><span data-stu-id="d2157-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="d2157-166">**메트릭 세분성/보존 기간:**</span><span class="sxs-lookup"><span data-stu-id="d2157-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="d2157-167">데이터는 5분 단위로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="d2157-168">데이터 보존 기간은 35일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="d2157-169">이 cmdlet 및 API hello too1000 행 (약 5 분 세분성의 3 일) 한 번의 호출에서에서 검색할 수 있는 행 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="d2157-170">하지만이 명령을 호출할 수 여러 번 다른 시작/종료 시간 간격 tooretrieve 더 많은 데이터</span><span class="sxs-lookup"><span data-stu-id="d2157-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="d2157-171">tooretrieve hello 메트릭:</span><span class="sxs-lookup"><span data-stu-id="d2157-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="d2157-172">탄력적 풀에서 데이터베이스의 리소스 사용량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2157-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="d2157-173">이러한 Api 의미 체계 차이점에 따라 hello 제외 하 고 단일 데이터베이스의 리소스 사용률을 hello 모니터링에 사용 되는 Api hello와 동일 hello 됩니다: 메트릭을 검색 (또는 해당 cap hello에 대 한 데이터베이스 최대 Edtu 당 hello에 대 한 백분율로 표현 CPU, IO와 같은 메트릭을 기본) 해당 풀에 대해 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="d2157-174">예를 들어 이러한 메트릭 중 하나의 50% 사용률이 hello 부모 풀에서 해당 리소스에 대 한 데이터베이스 캡 제한 당 hello의 50% 수준에서 특정 리소스 소비량 hello 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="d2157-175">tooretrieve hello 메트릭:</span><span class="sxs-lookup"><span data-stu-id="d2157-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="d2157-176">경고 tooan 탄력적 풀 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="d2157-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="d2157-177">탄력적 풀 toosend tooan 전자 메일 알림 또는 문자열이 너무 경고 경고 규칙을 추가할 수 있습니다[URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx) hello 탄력적 풀 설정 하는 사용률 임계값 도달 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d2157-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="d2157-178">Hello AzureRmMetricAlertRule 추가 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2157-179">탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="d2157-180">탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="d2157-181">마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="d2157-182">탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="d2157-183">이 예제에서는 탄력적 풀의 eDTU 소비가 특정 임계값을 초과할 때 알림을 받기 위해 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="d2157-184">자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2157-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="d2157-185">탄력적 풀의 경고 tooall 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="d2157-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="d2157-186">탄력적 풀 toosend에 tooall 데이터베이스 전자 메일 알림 또는 문자열이 너무 경고 경고 규칙을 추가할 수 있습니다[URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx) 때 리소스 hello 경고에 의해 설정 사용 임계값에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2157-187">탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="d2157-188">탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="d2157-189">마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="d2157-190">탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="d2157-191">이 예제에서는 해당 데이터베이스의 DTU 사용이 특정 임계값을 초과 되 면 알림을 받는 탄력적 풀에는 경고 tooeach hello 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="d2157-192">구독에서 여러 풀에 걸친 리소스 사용 데이터 수집 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="d2157-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="d2157-193">하나의 구독에 여러 데이터베이스를 포함할 경우 각 탄력적인 풀 별도로 번거로운 toomonitor 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="d2157-194">대신, SQL 데이터베이스 PowerShell cmdlet 및 T-SQL 쿼리 결합된 toocollect 리소스 사용 현황 데이터를 여러 풀, 모니터링 및 분석 리소스 사용을 위해 데이터베이스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="d2157-195">A [샘플 구현](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) 이러한 집합의 powershell 스크립트에서에서 찾을 수 있습니다 그 기능에 대 한 설명서와 함께 hello GitHub SQL Server 샘플 리포지토리 방법과 toouse 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="d2157-196">toouse이 샘플 구현에서는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="d2157-197">Hello 다운로드 [스크립트 및 설명서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="d2157-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="d2157-198">사용자 환경에 대 한 hello 스크립트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="d2157-199">탄력적 풀이 호스팅되는 하나 이상의 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="d2157-200">Hello 수집 된 메트릭이 있는 toobe 저장 된 원격 분석 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="d2157-201">Hello 스크립트 실행의 hello 스크립트 toospecify hello 기간을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="d2157-202">상위 수준 hello 스크립트는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="d2157-203">지정된 Azure 구독(또는 지정된 서버 목록)에 모든 서버를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="d2157-204">각 서버에 대한 백그라운드 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-204">Runs a background job for each server.</span></span> <span data-ttu-id="d2157-205">hello 작업이 정기적으로 루프에서 실행 되 고 모든 hello 풀 hello 서버에 대 한 원격 분석 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="d2157-206">Hello 지정 된 원격 분석 데이터베이스를 hello 수집 된 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="d2157-207">각 풀 toocollect hello 데이터베이스 리소스 사용 현황 데이터에는 데이터베이스의 목록을 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="d2157-208">Hello 원격 분석 데이터베이스를 hello 수집 된 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="d2157-209">hello hello 원격 분석 데이터베이스에 수집 된 메트릭을 수 탄력적 풀과 hello 데이터베이스 분석된 toomonitor hello 상태.</span><span class="sxs-lookup"><span data-stu-id="d2157-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="d2157-210">또한 hello 스크립트는 지정된 된 시간 창에 대 한 hello 원격 분석 데이터베이스 toohelp 집계 hello 메트릭을에 미리 정의 된 테이블 반환 함수 (TVF)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="d2157-211">예를 들어 hello TVF의 결과 수 있습니다 사용할 tooshow "상위 n 개 탄력적 풀에 지정된 된 기간 hello 최대 eDTU 사용률이."</span><span class="sxs-lookup"><span data-stu-id="d2157-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="d2157-212">필요에 따라 Excel 또는 Power BI tooquery와 같은 분석 도구를 사용 하 고 hello 수집 된 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="d2157-213">예제: 탄력적 풀 및 해당 데이터베이스에 대한 리소스 사용 메트릭 검색</span><span class="sxs-lookup"><span data-stu-id="d2157-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="d2157-214">이 예에서는 지정된 된 탄력적 풀 및 모든 데이터베이스에 대 한 hello 소비 메트릭을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="d2157-215">수집 된 데이터 서식이 설정 된를 tooa.csv 형식된 파일을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="d2157-216">Excel로 hello 파일을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="d2157-217">탄력적 풀 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="d2157-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="d2157-218">5 분 이내에 완료 데이터베이스 마다 데이터베이스 또는 최대 Edtu 당 hello 최소 Edtu를 일반적으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="d2157-219">Hello Edtu 풀 당 변경 hello hello 풀의 모든 데이터베이스에 사용 되는 공간의 총 금액에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="d2157-220">변경 시간은 100GB당 평균 90분 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="d2157-221">예를 들어 hello 총 공간에서 사용 하는 경우 hello 풀의 모든 데이터베이스는 200GB, 다음 hello 필요한 hello 풀 eDTU 풀 당 변경에 대 한 대기 시간은 3 시간 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d2157-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2157-222">Next steps</span></span>
* <span data-ttu-id="d2157-223">[탄력적 작업을 만들](sql-database-elastic-jobs-overview.md) 탄력적 작업을 사용 하면 임의 개수의 hello 풀의 데이터베이스에 대해 T-SQL 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="d2157-224">참조 [Azure SQL 데이터베이스를 사용한 수평 확장](sql-database-elastic-scale-introduction.md): out tooscale 탄력적 도구를 사용 하 여 데이터를 이동, 쿼리 또는 트랜잭션을 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2157-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
