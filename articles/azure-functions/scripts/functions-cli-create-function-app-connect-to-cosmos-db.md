---
title: "Azure Cosmos DB에 연결하는 Azure Function 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Cosmos DB에 연결하는 Azure Function 만들기"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="9f0a6-103">Azure Cosmos DB에 연결하는 Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="9f0a6-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="9f0a6-104">이 예제 스크립트는 Azure 함수 앱을 만들고 Azure Cosmos DB 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9f0a6-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9f0a6-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="9f0a6-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9f0a6-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="9f0a6-108">Sample script</span></span>

<span data-ttu-id="9f0a6-109">이 샘플은 Azure 함수 앱을 만들고 앱 설정에 Cosmos DB 끝점 및 액세스 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="9f0a6-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Azure Cosmos DB에 연결하는 Azure Function 만들기")]</span><span class="sxs-lookup"><span data-stu-id="9f0a6-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9f0a6-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="9f0a6-111">Clean up deployment</span></span>

<span data-ttu-id="9f0a6-112">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9f0a6-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="9f0a6-113">Script explanation</span></span>

<span data-ttu-id="9f0a6-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-114">This script uses the following commands.</span></span> <span data-ttu-id="9f0a6-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9f0a6-116">명령</span><span class="sxs-lookup"><span data-stu-id="9f0a6-116">Command</span></span> | <span data-ttu-id="9f0a6-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9f0a6-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f0a6-118">az login</span><span class="sxs-lookup"><span data-stu-id="9f0a6-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="9f0a6-119">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="9f0a6-119">Login to Azure.</span></span> |
| [<span data-ttu-id="9f0a6-120">az group create</span><span class="sxs-lookup"><span data-stu-id="9f0a6-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9f0a6-121">위치와 함께 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9f0a6-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="9f0a6-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="9f0a6-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="9f0a6-123">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9f0a6-123">Create a storage account</span></span> |
| [<span data-ttu-id="9f0a6-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="9f0a6-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="9f0a6-125">새로운 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9f0a6-125">Create a new function app</span></span> |
| [<span data-ttu-id="9f0a6-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="9f0a6-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="9f0a6-127">DocumentDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9f0a6-127">Create documentdb database</span></span> |
| [<span data-ttu-id="9f0a6-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="9f0a6-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="9f0a6-129">정리</span><span class="sxs-lookup"><span data-stu-id="9f0a6-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f0a6-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f0a6-130">Next steps</span></span>

<span data-ttu-id="9f0a6-131">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9f0a6-132">추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0a6-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




