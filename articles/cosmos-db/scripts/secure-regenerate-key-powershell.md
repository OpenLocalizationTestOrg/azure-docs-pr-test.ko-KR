---
title: "Azure PowerShell 스크립트 - Azure Cosmos DB 계정 키 재생성 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Azure Cosmos DB 계정 키 재생성"
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
ms.openlocfilehash: 187d7b0839e1cd94122d4455c11eda05673f5acc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-powershell"></a><span data-ttu-id="5b98b-103">PowerShell을 사용하여 Azure Cosmos DB 계정 키 재생성</span><span class="sxs-lookup"><span data-stu-id="5b98b-103">Regenerate an Azure Cosmos DB account key using PowerShell</span></span>

<span data-ttu-id="5b98b-104">이 샘플은 Azure CLI를 사용하여 모든 종류의 Azure Cosmos DB 계정 키를 재생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-104">This sample regenerates any kind of Azure Cosmos DB account key using the Azure CLI.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5b98b-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5b98b-105">Sample script</span></span>

<span data-ttu-id="5b98b-106">[!code-powershell[기본](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "Azure Cosmos DB 계정 키 재생성")]</span><span class="sxs-lookup"><span data-stu-id="5b98b-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "Regenerate Azure Cosmos DB account keys")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5b98b-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="5b98b-107">Clean up deployment</span></span>

<span data-ttu-id="5b98b-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5b98b-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5b98b-109">Script explanation</span></span>

<span data-ttu-id="5b98b-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-110">This script uses the following commands.</span></span> <span data-ttu-id="5b98b-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5b98b-112">명령</span><span class="sxs-lookup"><span data-stu-id="5b98b-112">Command</span></span> | <span data-ttu-id="5b98b-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5b98b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b98b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b98b-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="5b98b-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b98b-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5b98b-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="5b98b-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5b98b-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="5b98b-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="5b98b-119">Azure CosmosDB 계정에 대한 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="5b98b-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b98b-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="5b98b-121">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5b98b-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b98b-122">Next steps</span></span>

<span data-ttu-id="5b98b-123">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b98b-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="5b98b-124">추가 Azure Cosmos DB PowerShell 스크립트 샘플은 [Azure Cosmos DB PowerShell 스크립트](../powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b98b-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>