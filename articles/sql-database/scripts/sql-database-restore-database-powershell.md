---
title: "aaaPowerShell 예제-복원-백업-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toorestore 지역 중복 백업에서 Azure SQL 데이터베이스"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="69887-103">PowerShell toorestore 백업에서 Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="69887-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="69887-104">이 PowerShell 스크립트 예에서는 지역 중복 백업에서 Azure SQL 데이터베이스를 복원 하 고는 삭제 된 Azure SQL 데이터베이스 tooits 최신 백업, 복원 및 Azure SQL 데이터베이스 tooa 특정 지정 시간의 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="69887-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="69887-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="69887-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="69887-106">Clean up deployment</span></span>

<span data-ttu-id="69887-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69887-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="69887-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="69887-108">Script explanation</span></span>

<span data-ttu-id="69887-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-109">This script uses hello following commands.</span></span> <span data-ttu-id="69887-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="69887-111">명령</span><span class="sxs-lookup"><span data-stu-id="69887-111">Command</span></span> | <span data-ttu-id="69887-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="69887-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69887-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69887-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="69887-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69887-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="69887-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="69887-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="69887-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69887-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="69887-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="69887-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="69887-118">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69887-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="69887-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="69887-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="69887-120">데이터베이스의 지역 중복 백업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="69887-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="69887-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="69887-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="69887-122">SQL 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="69887-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="69887-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="69887-124">Azure SQL Database를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="69887-125">Get AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="69887-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="69887-126">복원할 수 있는 삭제된 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="69887-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="69887-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69887-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="69887-128">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69887-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69887-129">Next steps</span></span>

<span data-ttu-id="69887-130">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="69887-131">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69887-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
