---
title: "Azure PowerShell 스크립트 - MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기"
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
ms.openlocfilehash: e44e35cc7d11db48cd82e470ce8226b3c8cc220a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="601a3-103">PowerShell을 사용하여 MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="601a3-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="601a3-104">이 샘플은 PowerShell을 사용하여 MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="601a3-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="601a3-105">Sample script</span></span>

<span data-ttu-id="601a3-106">[!code-powershell[주](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Azure Cosmos DB 계정에서 MongoDB 연결 문자열 가져오기")]</span><span class="sxs-lookup"><span data-stu-id="601a3-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="601a3-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="601a3-107">Clean up deployment</span></span>

<span data-ttu-id="601a3-108">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="601a3-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="601a3-109">Script explanation</span></span>

<span data-ttu-id="601a3-110">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-110">This script uses the following commands.</span></span> <span data-ttu-id="601a3-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="601a3-112">명령</span><span class="sxs-lookup"><span data-stu-id="601a3-112">Command</span></span> | <span data-ttu-id="601a3-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="601a3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="601a3-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="601a3-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="601a3-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="601a3-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="601a3-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="601a3-117">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="601a3-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="601a3-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="601a3-119">Azure CosmosDB 계정에 대한 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="601a3-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="601a3-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="601a3-121">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="601a3-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="601a3-122">Next steps</span></span>

<span data-ttu-id="601a3-123">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="601a3-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="601a3-124">추가 Azure Cosmos DB PowerShell 스크립트 샘플은 [Azure Cosmos DB PowerShell 스크립트](../powershell-samples.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="601a3-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>