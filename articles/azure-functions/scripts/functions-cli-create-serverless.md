---
title: "CLI 스크립트 샘플-aaaAzure 서버가 없는 실행에 대 한 함수 앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 서버를 사용하지 않고 실행하기 위한 함수 앱 만들기"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="303a1-103">서버를 사용하지 않고 실행하기 위한 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="303a1-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="303a1-104">이 샘플 스크립트는 함수에 대한 컨테이너인 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="303a1-105">hello 함수 앱 만든 hello를 사용 하 여 [소비 계획](../functions-scale.md#consumption-plan), 적절 한 서버 작업 이벤트 구동 합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="303a1-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="303a1-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="303a1-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="303a1-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="303a1-109">Sample script</span></span>

<span data-ttu-id="303a1-110">이 스크립트는 hello를 사용 하 여 Azure 함수 앱 만듭니다 [소비 계획](../functions-scale.md#consumption-plan)합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="303a1-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="303a1-111">Script explanation</span></span>

<span data-ttu-id="303a1-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="303a1-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="303a1-114">명령</span><span class="sxs-lookup"><span data-stu-id="303a1-114">Command</span></span> | <span data-ttu-id="303a1-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="303a1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="303a1-116">az group create</span><span class="sxs-lookup"><span data-stu-id="303a1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="303a1-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="303a1-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="303a1-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="303a1-119">Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="303a1-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="303a1-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="303a1-121">Azure Function을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="303a1-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="303a1-122">Next steps</span></span>

<span data-ttu-id="303a1-123">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="303a1-124">추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="303a1-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
