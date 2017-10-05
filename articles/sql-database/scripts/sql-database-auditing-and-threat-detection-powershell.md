---
title: "PowerShell 예제 감사 위협 감지 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL Database에서 감사 및 위협 감지를 구성하는 Azure PowerShell 예제 스크립트"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="428fd-103">PowerShell을 사용하여 SQL Database 감사 및 위협 감지 구성</span><span class="sxs-lookup"><span data-stu-id="428fd-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="428fd-104">이 PowerShell 예제는 SQL Database 감사 및 위협 감지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="428fd-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="428fd-105">Sample script</span></span>

<span data-ttu-id="428fd-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "감사 및 위협 감지 구성")]</span><span class="sxs-lookup"><span data-stu-id="428fd-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="428fd-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="428fd-107">Clean up deployment</span></span>

<span data-ttu-id="428fd-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="428fd-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="428fd-109">Script explanation</span></span>

<span data-ttu-id="428fd-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-110">This script uses the following commands.</span></span> <span data-ttu-id="428fd-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="428fd-112">명령</span><span class="sxs-lookup"><span data-stu-id="428fd-112">Command</span></span> | <span data-ttu-id="428fd-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="428fd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="428fd-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="428fd-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="428fd-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="428fd-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="428fd-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="428fd-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="428fd-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="428fd-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="428fd-119">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="428fd-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="428fd-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="428fd-121">Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="428fd-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="428fd-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="428fd-123">데이터베이스에 대한 감사 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="428fd-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="428fd-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="428fd-125">데이터베이스에 대한 위협 감지 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="428fd-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="428fd-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="428fd-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="428fd-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="428fd-128">Next steps</span></span>

<span data-ttu-id="428fd-129">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="428fd-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="428fd-130">추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428fd-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
