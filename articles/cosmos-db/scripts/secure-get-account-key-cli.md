---
title: "aaaAzure CLI 스크립트 Get 계정 키가 Azure Cosmos DB | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Cosmos DB의 계정 키 가져오기"
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
ms.openlocfilehash: d6462b3eebc8bc6935a6fa07dcae37a33e5f382e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-hello-azure-cli"></a><span data-ttu-id="98a9c-103">Hello Azure CLI를 사용 하 여 Azure Cosmos DB에 대 한 계정 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="98a9c-103">Get account keys for Azure Cosmos DB using hello Azure CLI</span></span>

<span data-ttu-id="98a9c-104">이 샘플은 모든 종류의 Azure Cosmos DB 계정의 계정 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="98a9c-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="98a9c-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="98a9c-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="98a9c-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="98a9c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="98a9c-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="98a9c-109">Clean up deployment</span></span>

<span data-ttu-id="98a9c-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="98a9c-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="98a9c-111">Script explanation</span></span>

<span data-ttu-id="98a9c-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-112">This script uses hello following commands.</span></span> <span data-ttu-id="98a9c-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="98a9c-114">명령</span><span class="sxs-lookup"><span data-stu-id="98a9c-114">Command</span></span> | <span data-ttu-id="98a9c-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="98a9c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="98a9c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="98a9c-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="98a9c-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="98a9c-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="98a9c-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="98a9c-119">Azure Cosmos DB 계정을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="98a9c-120">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="98a9c-120">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="98a9c-121">Hello SQL 데이터베이스를 호스트 하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-121">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="98a9c-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="98a9c-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="98a9c-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="98a9c-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98a9c-124">Next steps</span></span>

<span data-ttu-id="98a9c-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="98a9c-126">추가 Azure Cosmos DB CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Cosmos DB CLI 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a9c-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
