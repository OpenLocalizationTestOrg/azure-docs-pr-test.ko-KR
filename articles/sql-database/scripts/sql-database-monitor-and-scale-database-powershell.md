---
title: "PowerShell 예제 모니터링 크기 조정 단일 Azure SQL Database | Microsoft Docs"
description: "단일 Azure SQL Database를 모니터링하고 크기를 조정하는 Azure PowerShell 예제 스크립트"
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="2d73b-103">PowerShell을 사용하여 단일 SQL Database 모니터링 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2d73b-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="2d73b-104">이 PowerShell 스크립트 예제는 데이터베이스의 성능 메트릭을 모니터링하고, 더 높은 성능 수준으로 확장하고, 성능 메트릭 중 하나에 경고 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2d73b-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2d73b-105">Sample script</span></span>

<span data-ttu-id="2d73b-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "단일 SQL Database 모니터링 및 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="2d73b-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2d73b-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="2d73b-107">Clean up deployment</span></span>

<span data-ttu-id="2d73b-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2d73b-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2d73b-109">Script explanation</span></span>

<span data-ttu-id="2d73b-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-110">This script uses the following commands.</span></span> <span data-ttu-id="2d73b-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2d73b-112">명령</span><span class="sxs-lookup"><span data-stu-id="2d73b-112">Command</span></span> | <span data-ttu-id="2d73b-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2d73b-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="2d73b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d73b-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2d73b-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2d73b-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2d73b-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2d73b-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2d73b-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="2d73b-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="2d73b-119">데이터베이스의 크기 사용량 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="2d73b-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2d73b-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="2d73b-121">데이터베이스 속성을 업데이트하거나 탄력적 풀로/에서 또는 탄력적 풀 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="2d73b-122">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="2d73b-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="2d73b-123">나중에 DTU를 자동으로 모니터링하도록 경고 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="2d73b-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d73b-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2d73b-125">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2d73b-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d73b-126">Next steps</span></span>

<span data-ttu-id="2d73b-127">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d73b-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2d73b-128">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d73b-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
