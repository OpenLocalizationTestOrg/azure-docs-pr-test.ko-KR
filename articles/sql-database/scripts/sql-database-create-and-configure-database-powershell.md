---
title: "Azure SQL 데이터베이스 aaaPowerShell 예제-만들기 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toocreate Azure SQL 데이터베이스"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="86440-103">PowerShell toocreate 단일 Azure SQL 데이터베이스를 사용 하 고 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="86440-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="86440-104">이 PowerShell 스크립트 예제는 Azure SQL Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="86440-105">Hello 스크립트 성공적으로 실행 되 면 모든 Azure 서비스에서 SQL 데이터베이스에 액세스할 수는 hello 및 hello IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="86440-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="86440-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="86440-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="86440-107">Clean up deployment</span></span>

<span data-ttu-id="86440-108">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86440-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="86440-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="86440-109">Script explanation</span></span>

<span data-ttu-id="86440-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-110">This script uses hello following commands.</span></span> <span data-ttu-id="86440-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="86440-112">명령</span><span class="sxs-lookup"><span data-stu-id="86440-112">Command</span></span> | <span data-ttu-id="86440-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="86440-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="86440-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86440-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="86440-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86440-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="86440-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="86440-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="86440-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86440-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="86440-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="86440-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="86440-119">Hello 입력 한 IP 주소 범위에서 hello 서버의 방화벽 규칙 tooallow 액세스 tooall SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86440-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="86440-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="86440-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="86440-121">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86440-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="86440-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86440-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="86440-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="86440-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86440-124">Next steps</span></span>

<span data-ttu-id="86440-125">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="86440-126">추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86440-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



