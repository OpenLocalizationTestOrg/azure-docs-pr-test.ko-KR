---
title: "PowerShell 예제 복원 백업 Azure SQL database | Microsoft Docs"
description: "지역 중복 백업에서 Azure SQL Database를 복원하는 Azure PowerShell 예제 스크립트"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="0950f-103">PowerShell을 사용하여 백업에서 Azure SQL Database 복원</span><span class="sxs-lookup"><span data-stu-id="0950f-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="0950f-104">이 PowerShell 스크립트 예제는 지역 중복 백업에서 Azure SQL Database를 복원하고 삭제된 Azure SQL Database를 최신 백업으로 복원하며 Azure SQL Database를 특정 시점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0950f-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0950f-105">Sample script</span></span>

<span data-ttu-id="0950f-106">[!code-powershell[기본](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "SQL Database 만들기")]</span><span class="sxs-lookup"><span data-stu-id="0950f-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0950f-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0950f-107">Clean up deployment</span></span>

<span data-ttu-id="0950f-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0950f-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0950f-109">Script explanation</span></span>

<span data-ttu-id="0950f-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-110">This script uses the following commands.</span></span> <span data-ttu-id="0950f-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0950f-112">명령</span><span class="sxs-lookup"><span data-stu-id="0950f-112">Command</span></span> | <span data-ttu-id="0950f-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0950f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0950f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0950f-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="0950f-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="0950f-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0950f-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0950f-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="0950f-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0950f-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="0950f-119">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="0950f-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="0950f-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="0950f-121">데이터베이스의 지역 중복 백업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="0950f-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0950f-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="0950f-123">SQL 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="0950f-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0950f-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="0950f-125">Azure SQL Database를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="0950f-126">Get AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="0950f-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="0950f-127">복원할 수 있는 삭제된 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="0950f-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0950f-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0950f-129">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0950f-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0950f-130">Next steps</span></span>

<span data-ttu-id="0950f-131">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0950f-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0950f-132">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0950f-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
