---
title: "PowerShell 예제 Azure SQL Database 이동 SQL 탄력적 풀 | Microsoft Docs"
description: "PowerShell을 사용하여 탄력적 풀 간에 SQL Database를 이동하는 Azure PowerShell 스크립트 샘플"
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
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="2ca99-103">PowerShell을 사용한 탄력적 풀 만들기 및 탄력적 풀 간에 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="2ca99-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="2ca99-104">이 PowerShell 스크립트 예제는 두 개의 탄력적 풀을 만들고 한 탄력적 풀에서 다른 탄력적 풀로 데이터베이스를 이동한 다음 탄력적 풀에서 단일 데이터베이스 성능 수준으로 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2ca99-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2ca99-105">Sample script</span></span>

<span data-ttu-id="2ca99-106">[!code-powershell[기본](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "풀 간에 데이터베이스 이동")]</span><span class="sxs-lookup"><span data-stu-id="2ca99-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2ca99-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="2ca99-107">Clean up deployment</span></span>

<span data-ttu-id="2ca99-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2ca99-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2ca99-109">Script explanation</span></span>

<span data-ttu-id="2ca99-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-110">This script uses the following commands.</span></span> <span data-ttu-id="2ca99-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2ca99-112">명령</span><span class="sxs-lookup"><span data-stu-id="2ca99-112">Command</span></span> | <span data-ttu-id="2ca99-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2ca99-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ca99-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2ca99-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2ca99-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2ca99-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2ca99-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2ca99-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2ca99-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="2ca99-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="2ca99-119">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="2ca99-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2ca99-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="2ca99-121">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="2ca99-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2ca99-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="2ca99-123">데이터베이스 속성을 업데이트하거나 탄력적 풀로/에서 또는 탄력적 풀 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="2ca99-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2ca99-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2ca99-125">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2ca99-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ca99-126">Next steps</span></span>

<span data-ttu-id="2ca99-127">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ca99-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2ca99-128">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca99-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
