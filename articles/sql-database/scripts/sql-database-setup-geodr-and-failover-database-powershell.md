---
title: "PowerShell 예제 - 활성 지역 복제 - 단일 Azure SQL Database | Microsoft Docs"
description: "단일 Azure SQL Database에 활성 지역 복제를 설정하는 Azure PowerShell 예제 스크립트"
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="1e4ed-103">PowerShell을 사용하여 단일 Azure SQL Database에 대한 활성 지역 복제 구성</span><span class="sxs-lookup"><span data-stu-id="1e4ed-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="1e4ed-104">이 PowerShell 스크립트 예제는 단일 Azure SQL Database에 대해 활성 지역 복제를 구성하고 Azure SQL Database의 보조 복제본으로 장애 조치(failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="1e4ed-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1e4ed-105">Sample scripts</span></span>

<span data-ttu-id="1e4ed-106">[!code-powershell[주](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "단일 데이터베이스에 대한 활성 지역 복제 설정")]</span><span class="sxs-lookup"><span data-stu-id="1e4ed-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1e4ed-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="1e4ed-107">Clean up deployment</span></span>

<span data-ttu-id="1e4ed-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1e4ed-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1e4ed-109">Script explanation</span></span>

<span data-ttu-id="1e4ed-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-110">This script uses the following commands.</span></span> <span data-ttu-id="1e4ed-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1e4ed-112">명령</span><span class="sxs-lookup"><span data-stu-id="1e4ed-112">Command</span></span> | <span data-ttu-id="1e4ed-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1e4ed-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e4ed-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e4ed-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1e4ed-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1e4ed-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="1e4ed-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="1e4ed-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1e4ed-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1e4ed-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="1e4ed-119">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="1e4ed-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1e4ed-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="1e4ed-121">데이터베이스 속성을 업데이트하거나 탄력적 풀 내부, 외부 또는 내외부 상호 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="1e4ed-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="1e4ed-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="1e4ed-123">기존 데이터베이스에 대한 보조 데이터베이스를 만들고 데이터 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="1e4ed-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1e4ed-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="1e4ed-125">하나 이상의 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="1e4ed-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="1e4ed-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="1e4ed-127">장애 조치를 시작하기 위해 보조 데이터베이스로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="1e4ed-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="1e4ed-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="1e4ed-129">Azure SQL 데이터베이스와 리소스 그룹 또는 SQL Server 간의 지역에서 복제 링크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="1e4ed-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="1e4ed-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="1e4ed-131">SQL 데이터베이스와 지정된 보조 데이터베이스 간의 데이터 복제를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="1e4ed-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e4ed-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1e4ed-133">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1e4ed-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e4ed-134">Next steps</span></span>

<span data-ttu-id="1e4ed-135">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1e4ed-136">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e4ed-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
