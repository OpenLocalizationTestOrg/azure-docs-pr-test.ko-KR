---
title: "Azure CLI 스크립트 - Azure Cosmos DB 컨테이너 처리량 확장 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Cosmos DB 컨테이너 처리량 확장"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="a0ac5-103">Azure CLI를 사용하여 Azure Cosmos DB 컨테이너 처리량 확장</span><span class="sxs-lookup"><span data-stu-id="a0ac5-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="a0ac5-104">이 샘플에서는 모든 종류의 Azure Cosmos DB 컨테이너에 대한 컨테이너 처리량을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a0ac5-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a0ac5-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a0ac5-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a0ac5-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a0ac5-108">Sample script</span></span>

<span data-ttu-id="a0ac5-109">[!code-azurecli-interactive[기본](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Azure Cosmos DB 처리량 확장")]</span><span class="sxs-lookup"><span data-stu-id="a0ac5-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a0ac5-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="a0ac5-110">Clean up deployment</span></span>

<span data-ttu-id="a0ac5-111">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a0ac5-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a0ac5-112">Script explanation</span></span>

<span data-ttu-id="a0ac5-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-113">This script uses the following commands.</span></span> <span data-ttu-id="a0ac5-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a0ac5-115">명령</span><span class="sxs-lookup"><span data-stu-id="a0ac5-115">Command</span></span> | <span data-ttu-id="a0ac5-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a0ac5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a0ac5-117">az group create</span><span class="sxs-lookup"><span data-stu-id="a0ac5-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a0ac5-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a0ac5-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="a0ac5-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="a0ac5-120">Azure Cosmos DB 계정을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="a0ac5-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="a0ac5-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="a0ac5-122">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a0ac5-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0ac5-123">Next steps</span></span>

<span data-ttu-id="a0ac5-124">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a0ac5-125">추가 Azure Cosmos DB CLI 스크립트 샘플은 [Azure Cosmos DB CLI 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ac5-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
