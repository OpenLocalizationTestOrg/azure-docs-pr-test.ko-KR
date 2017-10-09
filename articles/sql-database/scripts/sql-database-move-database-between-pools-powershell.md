---
title: "aaaPowerShell 예제 이동 Azure SQL 데이터베이스 SQL 탄력적인 풀 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toomove PowerShell을 사용 하 여 탄력적 풀 간에 SQL 데이터베이스"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="cc5c5-103">PowerShell toocreate 탄력적 풀을 사용 하 고 탄력적 풀 간에 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="cc5c5-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="cc5c5-104">이 PowerShell 스크립트 예에서는 두 개의 탄력적 풀을 만듭니다 및 데이터베이스 한 탄력적 풀에서 다른 탄력적 풀으로 이동한 다음 데이터베이스는 탄력적인 풀 tooa 단일 데이터베이스 성능 수준을 벗어났습니다 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="cc5c5-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="cc5c5-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cc5c5-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="cc5c5-106">Clean up deployment</span></span>

<span data-ttu-id="cc5c5-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="cc5c5-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="cc5c5-108">Script explanation</span></span>

<span data-ttu-id="cc5c5-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-109">This script uses hello following commands.</span></span> <span data-ttu-id="cc5c5-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cc5c5-111">명령</span><span class="sxs-lookup"><span data-stu-id="cc5c5-111">Command</span></span> | <span data-ttu-id="cc5c5-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="cc5c5-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cc5c5-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cc5c5-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="cc5c5-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cc5c5-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="cc5c5-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="cc5c5-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="cc5c5-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="cc5c5-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="cc5c5-118">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="cc5c5-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cc5c5-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="cc5c5-120">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="cc5c5-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cc5c5-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="cc5c5-122">데이터베이스 속성을 업데이트하거나 탄력적 풀로/에서 또는 탄력적 풀 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="cc5c5-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cc5c5-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cc5c5-124">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="cc5c5-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc5c5-125">Next steps</span></span>

<span data-ttu-id="cc5c5-126">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cc5c5-127">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc5c5-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
