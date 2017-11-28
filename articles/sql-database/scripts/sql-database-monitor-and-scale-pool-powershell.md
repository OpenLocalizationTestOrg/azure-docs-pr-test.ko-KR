---
title: "aaaPowerShell 예제 모니터-눈금 SQL 탄력적 풀-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toomonitor 및 Azure SQL 데이터베이스에서 SQL 탄력적인 풀 크기 조정"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="21260-103">Azure SQL 데이터베이스에서 SQL 탄력적 풀의 크기를 조정 하 고 PowerShell toomonitor를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="21260-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="21260-104">모니터 hello 탄력적 풀의 성능 메트릭을이 PowerShell 스크립트 예에서는 tooa 높은 성능 수준 확장 하 고 hello 성능 메트릭 중 하나에서 경고 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21260-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="21260-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="21260-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="21260-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="21260-106">Clean up deployment</span></span>

<span data-ttu-id="21260-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21260-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="21260-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="21260-108">Script explanation</span></span>

<span data-ttu-id="21260-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-109">This script uses hello following commands.</span></span> <span data-ttu-id="21260-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="21260-111">명령</span><span class="sxs-lookup"><span data-stu-id="21260-111">Command</span></span> | <span data-ttu-id="21260-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="21260-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="21260-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21260-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="21260-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21260-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21260-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="21260-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="21260-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21260-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="21260-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="21260-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="21260-118">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21260-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="21260-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="21260-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="21260-120">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21260-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="21260-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="21260-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="21260-122">Hello 데이터베이스에 대 한 hello 크기 사용 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21260-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="21260-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="21260-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="21260-124">메트릭 기반 경고 규칙을 추가하거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="21260-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="21260-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="21260-126">탄력적 풀 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="21260-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="21260-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="21260-128">설정 된 경고 규칙 tooautomatically 모니터 Dtu hello 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="21260-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="21260-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21260-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="21260-130">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="21260-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21260-131">Next steps</span></span>

<span data-ttu-id="21260-132">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="21260-133">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21260-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
