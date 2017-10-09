---
title: "Azure Cosmos DB에 대 한 방화벽 CLI 스크립트-만들기 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Cosmos DB에 대한 방화벽 만들기"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d4bee4f37906033c96826b9662d2ba396325c792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-hello-azure-cli"></a><span data-ttu-id="63e92-103">Azure Cosmos DB: hello Azure CLI를 사용 하는 방화벽 만들기</span><span class="sxs-lookup"><span data-stu-id="63e92-103">Azure Cosmos DB: Create a firewall using hello Azure CLI</span></span>

<span data-ttu-id="63e92-104">이 샘플 CLI 스크립트는 종류에 관계없이 Azure Cosmos DB 계정에 대해 방화벽 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="63e92-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="63e92-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="63e92-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="63e92-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="63e92-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]

## <a name="clean-up-deployment"></a><span data-ttu-id="63e92-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="63e92-109">Clean up deployment</span></span>

<span data-ttu-id="63e92-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="63e92-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="63e92-111">Script explanation</span></span>

<span data-ttu-id="63e92-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-112">This script uses hello following commands.</span></span> <span data-ttu-id="63e92-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="63e92-114">명령</span><span class="sxs-lookup"><span data-stu-id="63e92-114">Command</span></span> | <span data-ttu-id="63e92-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="63e92-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63e92-116">az group create</span><span class="sxs-lookup"><span data-stu-id="63e92-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="63e92-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="63e92-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="63e92-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="63e92-119">Azure Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-119">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="63e92-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="63e92-120">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="63e92-121">Azure CosmosDB 계정 tooinclude 방화벽 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-121">Updates an Azure CosmosDB account tooinclude firewall settings.</span></span> |
| [<span data-ttu-id="63e92-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="63e92-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="63e92-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="63e92-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63e92-124">Next steps</span></span>

<span data-ttu-id="63e92-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="63e92-126">추가 Azure Cosmos DB CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Cosmos DB CLI 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63e92-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
