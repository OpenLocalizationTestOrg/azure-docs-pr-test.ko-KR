---
title: "aaaPowerShell 예제-활성 지역에서 복제-단일 Azure SQL 데이터베이스 | Microsoft Docs"
description: "단일 Azure SQL 데이터베이스에 대 한 활성 지리적 복제를 azure PowerShell 예제 스크립트 tooset"
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
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="0cb79-103">단일 Azure SQL 데이터베이스에 대 한 PowerShell tooconfigure 활성 지리적 복제를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0cb79-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="0cb79-104">이 PowerShell 스크립트 예제는 단일 Azure SQL 데이터베이스에 대 한 활성 지리적 복제를 구성 하 고 tooa hello Azure SQL 데이터베이스의 보조 복제본으로 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="0cb79-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0cb79-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0cb79-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0cb79-106">Clean up deployment</span></span>

<span data-ttu-id="0cb79-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0cb79-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0cb79-108">Script explanation</span></span>

<span data-ttu-id="0cb79-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-109">This script uses hello following commands.</span></span> <span data-ttu-id="0cb79-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0cb79-111">명령</span><span class="sxs-lookup"><span data-stu-id="0cb79-111">Command</span></span> | <span data-ttu-id="0cb79-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0cb79-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0cb79-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0cb79-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0cb79-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0cb79-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0cb79-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0cb79-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0cb79-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="0cb79-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="0cb79-118">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="0cb79-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0cb79-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="0cb79-120">데이터베이스 속성을 업데이트하거나 탄력적 풀 내부, 외부 또는 내외부 상호 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="0cb79-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0cb79-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="0cb79-122">기존 데이터베이스에 대한 보조 데이터베이스를 만들고 데이터 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="0cb79-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0cb79-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="0cb79-124">하나 이상의 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="0cb79-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0cb79-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="0cb79-126">보조 데이터베이스 toobe 기본 tooinitiate 장애 조치를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="0cb79-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="0cb79-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="0cb79-128">Azure SQL 데이터베이스와 리소스 그룹 또는 SQL Server 간의 hello 지역 간 복제 링크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="0cb79-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0cb79-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="0cb79-130">SQL 데이터베이스와 보조 데이터베이스를 지정된 하는 hello 간의 데이터 복제를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="0cb79-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0cb79-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0cb79-132">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0cb79-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cb79-133">Next steps</span></span>

<span data-ttu-id="0cb79-134">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0cb79-135">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb79-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
