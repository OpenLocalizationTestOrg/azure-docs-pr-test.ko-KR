---
title: "aaaAzure MongoDB 앱에 대 한 CLI 스크립트 Get Azure Cosmos DB 연결 문자열 | Microsoft Docs"
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
ms.openlocfilehash: 9b0a4bf020039c9bf9554b4199a279622c15a15d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-hello-azure-cli"></a><span data-ttu-id="f1377-103">Hello Azure CLI를 사용 하 여 MongoDB 앱에 대 한 Azure Cosmos DB 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="f1377-103">Get an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI</span></span>

<span data-ttu-id="f1377-104">이 샘플 hello Azure CLI를 사용 하 여 MongoDB 앱에 대 한 Azure Cosmos DB 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f1377-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f1377-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f1377-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f1377-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f1377-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1377-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="f1377-109">Clean up deployment</span></span>

<span data-ttu-id="f1377-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f1377-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f1377-111">Script explanation</span></span>

<span data-ttu-id="f1377-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-112">This script uses hello following commands.</span></span> <span data-ttu-id="f1377-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f1377-114">명령</span><span class="sxs-lookup"><span data-stu-id="f1377-114">Command</span></span> | <span data-ttu-id="f1377-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f1377-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1377-116">az group create</span><span class="sxs-lookup"><span data-stu-id="f1377-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f1377-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1377-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="f1377-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="f1377-119">Azure Cosmos DB 계정을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="f1377-120">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="f1377-120">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="f1377-121">Hello 계정에 대 한 hello 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-121">Gets hello connection string for hello account.</span></span>|
| [<span data-ttu-id="f1377-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="f1377-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f1377-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1377-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1377-124">Next steps</span></span>

<span data-ttu-id="f1377-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f1377-126">추가 Azure Cosmos DB CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Cosmos DB CLI 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1377-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
