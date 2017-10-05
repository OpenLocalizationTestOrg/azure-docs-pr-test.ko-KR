---
title: "Azure CLI 스크립트 - MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기"
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
ms.openlocfilehash: 916c92cab39306352fdf9dff0e0685fd61832d16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a><span data-ttu-id="ca356-103">Azure CLI를 사용하여 MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="ca356-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span></span>

<span data-ttu-id="ca356-104">이 샘플은 Azure CLI를 사용하여 MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ca356-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ca356-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ca356-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca356-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ca356-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ca356-108">Sample script</span></span>

<span data-ttu-id="ca356-109">[!code-azurecli-interactive[기본](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "MongoDB 앱에 대한 Azure Cosmos DB 연결 문자열 가져오기")]</span><span class="sxs-lookup"><span data-stu-id="ca356-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ca356-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ca356-110">Clean up deployment</span></span>

<span data-ttu-id="ca356-111">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ca356-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ca356-112">Script explanation</span></span>

<span data-ttu-id="ca356-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-113">This script uses the following commands.</span></span> <span data-ttu-id="ca356-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ca356-115">명령</span><span class="sxs-lookup"><span data-stu-id="ca356-115">Command</span></span> | <span data-ttu-id="ca356-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ca356-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ca356-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ca356-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ca356-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ca356-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="ca356-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="ca356-120">Azure Cosmos DB 계정을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="ca356-121">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="ca356-121">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="ca356-122">계정에 대한 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-122">Gets the connection string for the account.</span></span>|
| [<span data-ttu-id="ca356-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="ca356-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ca356-124">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ca356-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca356-125">Next steps</span></span>

<span data-ttu-id="ca356-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca356-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ca356-127">추가 Azure Cosmos DB CLI 스크립트 샘플은 [Azure Cosmos DB CLI 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca356-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
