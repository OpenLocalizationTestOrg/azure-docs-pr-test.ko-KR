---
title: "aaaPowerShell 예제-복사-Azure SQL 데이터베이스를 새 서버 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toocopy SQL 데이터베이스 tooa 새 서버"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="ecdda-103">PowerShell toocopy SQL 데이터베이스 tooa 새 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ecdda-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="ecdda-104">PowerShell 스크립트 예제에서는 새 서버에 기존 데이터베이스의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="ecdda-105">데이터베이스 tooa 새 서버에 복사</span><span class="sxs-lookup"><span data-stu-id="ecdda-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ecdda-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ecdda-106">Clean up deployment</span></span>

<span data-ttu-id="ecdda-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="ecdda-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ecdda-108">Script explanation</span></span>

<span data-ttu-id="ecdda-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-109">This script uses hello following commands.</span></span> <span data-ttu-id="ecdda-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ecdda-111">명령</span><span class="sxs-lookup"><span data-stu-id="ecdda-111">Command</span></span> | <span data-ttu-id="ecdda-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ecdda-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ecdda-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ecdda-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ecdda-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ecdda-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="ecdda-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="ecdda-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="ecdda-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ecdda-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="ecdda-118">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="ecdda-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="ecdda-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="ecdda-120">현재 시간 hello에 스냅숏 hello를 사용 하는 데이터베이스의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="ecdda-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ecdda-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ecdda-122">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="ecdda-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecdda-123">Next steps</span></span>

<span data-ttu-id="ecdda-124">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ecdda-125">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecdda-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
