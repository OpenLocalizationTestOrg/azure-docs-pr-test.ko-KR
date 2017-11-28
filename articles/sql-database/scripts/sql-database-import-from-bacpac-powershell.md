---
title: "aaaPowerShell 예제-가져오기-bacpac 파일 Azure SQL 데이터베이스 | Microsoft Docs"
description: "SQL 데이터베이스에 azure PowerShell 예제 스크립트 tooimport bacpac 타일"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="d48f0-103">PowerShell tooimport bacpac 파일을 사용 하 여 Azure SQL 데이터베이스에</span><span class="sxs-lookup"><span data-stu-id="d48f0-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="d48f0-104">이 PowerShell 스크립트 예제는 **bacpac** 파일의 데이터베이스를 Azure SQL Database에 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d48f0-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d48f0-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d48f0-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d48f0-106">Clean up deployment</span></span>

<span data-ttu-id="d48f0-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d48f0-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d48f0-108">Script explanation</span></span>

<span data-ttu-id="d48f0-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-109">This script uses hello following commands.</span></span> <span data-ttu-id="d48f0-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d48f0-111">명령</span><span class="sxs-lookup"><span data-stu-id="d48f0-111">Command</span></span> | <span data-ttu-id="d48f0-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d48f0-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d48f0-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d48f0-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d48f0-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d48f0-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d48f0-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d48f0-116">Hello SQL 데이터베이스를 호스트 하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="d48f0-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="d48f0-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="d48f0-118">Hello 입력 한 IP 주소 범위에서 hello 서버의 방화벽 규칙 tooallow 액세스 tooall SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="d48f0-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="d48f0-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="d48f0-120">A.bacpac 파일 가져오기와 hello 서버에 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="d48f0-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d48f0-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d48f0-122">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d48f0-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d48f0-123">Next steps</span></span>

<span data-ttu-id="d48f0-124">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d48f0-125">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f0-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
