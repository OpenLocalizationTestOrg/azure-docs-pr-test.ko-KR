---
title: "aaaPowerShell 예제 감사 위협 검색-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 tooconfigure 감사 및 위협 검색의 Azure SQL 데이터베이스"
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
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="75b37-103">PowerShell tooconfigure SQL 데이터베이스 감사 및 위협 검색을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="75b37-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="75b37-104">이 PowerShell 예제는 SQL Database 감사 및 위협 감지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="75b37-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="75b37-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="75b37-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="75b37-106">Clean up deployment</span></span>

<span data-ttu-id="75b37-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="75b37-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="75b37-108">Script explanation</span></span>

<span data-ttu-id="75b37-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-109">This script uses hello following commands.</span></span> <span data-ttu-id="75b37-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="75b37-111">명령</span><span class="sxs-lookup"><span data-stu-id="75b37-111">Command</span></span> | <span data-ttu-id="75b37-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75b37-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="75b37-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75b37-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="75b37-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="75b37-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="75b37-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="75b37-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="75b37-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="75b37-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="75b37-118">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="75b37-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="75b37-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="75b37-120">Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="75b37-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="75b37-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="75b37-122">데이터베이스에 대 한 hello 감사 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="75b37-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="75b37-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="75b37-124">데이터베이스에 대한 위협 감지 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="75b37-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75b37-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="75b37-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="75b37-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75b37-127">Next steps</span></span>

<span data-ttu-id="75b37-128">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="75b37-129">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75b37-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
