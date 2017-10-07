---
title: "aaaCreate tooan Azure Cosmos DB에 연결 하는 Azure 함수 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Azure Cosmos DB tooan 연결 하는 Azure 함수 만들기"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="98f35-103">Tooan Azure Cosmos DB에 연결 하는 Azure 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="98f35-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="98f35-104">이 샘플 스크립트는 Azure 함수 응용 프로그램을 만들고 tooan Azure Cosmos DB 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="98f35-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="98f35-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="98f35-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="98f35-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="98f35-108">Sample script</span></span>

<span data-ttu-id="98f35-109">이 샘플 Azure 함수 응용 프로그램을 만들고 Cosmos DB 끝점 및 액세스 키 tooapp 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="98f35-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="98f35-110">Clean up deployment</span></span>

<span data-ttu-id="98f35-111">Hello 스크립트 예제를 실행 한 후 hello 다음 명령은 사용된 tooremove hello 리소스 그룹 수 및 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="98f35-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="98f35-112">Script explanation</span></span>

<span data-ttu-id="98f35-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-113">This script uses hello following commands.</span></span> <span data-ttu-id="98f35-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="98f35-115">명령</span><span class="sxs-lookup"><span data-stu-id="98f35-115">Command</span></span> | <span data-ttu-id="98f35-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="98f35-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="98f35-117">az login</span><span class="sxs-lookup"><span data-stu-id="98f35-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="98f35-118">로그인 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="98f35-119">az group create</span><span class="sxs-lookup"><span data-stu-id="98f35-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="98f35-120">위치와 함께 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="98f35-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="98f35-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="98f35-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="98f35-122">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="98f35-122">Create a storage account</span></span> |
| [<span data-ttu-id="98f35-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="98f35-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="98f35-124">새로운 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="98f35-124">Create a new function app</span></span> |
| [<span data-ttu-id="98f35-125">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="98f35-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="98f35-126">DocumentDB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="98f35-126">Create documentdb database</span></span> |
| [<span data-ttu-id="98f35-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="98f35-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="98f35-128">정리</span><span class="sxs-lookup"><span data-stu-id="98f35-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="98f35-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98f35-129">Next steps</span></span>

<span data-ttu-id="98f35-130">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="98f35-131">추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98f35-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




