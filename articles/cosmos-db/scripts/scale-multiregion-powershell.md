---
title: "Azure Cosmos DB에 대 한 PowerShell 스크립트-다중 지역 aaaAzure 복제 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Azure Cosmos DB에 대한 다중 지역 복제"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="54d71-103">PowerShell을 사용하여 Azure Cosmos DB 데이터베이스 계정을 여러 하위 지역에서 복제 및 장애 조치 우선 순위 구성</span><span class="sxs-lookup"><span data-stu-id="54d71-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="54d71-104">이 샘플은 Azure Cosmos DB 데이터베이스 계정을 여러 하위 지역에서 복제하고 PowerShell을 사용하여 장애 조치 우선 순위를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="54d71-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="54d71-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="54d71-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="54d71-106">Clean up deployment</span></span>

<span data-ttu-id="54d71-107">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="54d71-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="54d71-108">Script explanation</span></span>

<span data-ttu-id="54d71-109">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-109">This script uses hello following commands.</span></span> <span data-ttu-id="54d71-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="54d71-111">명령</span><span class="sxs-lookup"><span data-stu-id="54d71-111">Command</span></span> | <span data-ttu-id="54d71-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="54d71-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="54d71-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="54d71-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="54d71-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="54d71-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="54d71-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="54d71-116">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="54d71-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="54d71-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="54d71-118">Hello 데이터베이스 계정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="54d71-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="54d71-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="54d71-120">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="54d71-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54d71-121">Next steps</span></span>

<span data-ttu-id="54d71-122">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/)합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="54d71-123">추가 Azure Cosmos DB PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Cosmos DB PowerShell 스크립트를](../powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54d71-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
