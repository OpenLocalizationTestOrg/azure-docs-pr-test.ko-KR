---
title: "PowerShell 예제 모니터링 크기 조정 SQL 탄력적 풀 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL Database에서 SQL 탄력적 풀을 모니터링하고 크기를 조정하는 Azure PowerShell 예제 스크립트"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="a6926-103">PowerShell을 사용하여 Azure SQL Database에서 SQL 탄력적 풀 모니터링 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a6926-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="a6926-104">이 PowerShell 스크립트 예제는 탄력적 풀의 성능 메트릭을 모니터링하고, 더 높은 성능 수준으로 확장하고, 성능 메트릭 중 하나에 경고 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a6926-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a6926-105">Sample script</span></span>

<span data-ttu-id="a6926-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "단일 SQL Database 모니터링 및 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="a6926-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a6926-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="a6926-107">Clean up deployment</span></span>

<span data-ttu-id="a6926-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a6926-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a6926-109">Script explanation</span></span>

<span data-ttu-id="a6926-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-110">This script uses the following commands.</span></span> <span data-ttu-id="a6926-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a6926-112">명령</span><span class="sxs-lookup"><span data-stu-id="a6926-112">Command</span></span> | <span data-ttu-id="a6926-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a6926-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="a6926-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6926-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a6926-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6926-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a6926-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a6926-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a6926-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a6926-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a6926-119">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a6926-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a6926-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a6926-121">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a6926-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="a6926-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="a6926-123">데이터베이스의 크기 사용량 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="a6926-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a6926-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a6926-125">메트릭 기반 경고 규칙을 추가하거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="a6926-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a6926-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="a6926-127">탄력적 풀 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="a6926-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a6926-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a6926-129">나중에 DTU를 자동으로 모니터링하도록 경고 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="a6926-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6926-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a6926-131">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a6926-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6926-132">Next steps</span></span>

<span data-ttu-id="a6926-133">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6926-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a6926-134">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6926-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
