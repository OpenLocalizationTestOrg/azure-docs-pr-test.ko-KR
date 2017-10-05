---
title: "함수 앱 만들기 및 GitHub의 함수 코드 배포 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 함수 앱 만들기 및 GitHub의 함수 코드 배포"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="5d9b9-103">함수 앱 만들기 및 GitHub의 함수 코드 배포</span><span class="sxs-lookup"><span data-stu-id="5d9b9-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="5d9b9-104">이 샘플 스크립트는 관련된 리소스를 통해 [소비 계획](../functions-scale.md#consumption-plan)을 사용하여 함수 앱을 만든 다음 연속 배포를 사용하지 않고 공용 GitHub 리포지토리의 함수 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="5d9b9-105">GitHub의 지속적인 함수 코드 전송에 관해서는 [함수 앱 만들기 및 GitHub에서 지속적으로 배포](functions-cli-create-function-app-github-continuous.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5d9b9-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5d9b9-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5d9b9-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5d9b9-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5d9b9-109">Sample script</span></span>

<span data-ttu-id="5d9b9-110">이 샘플은 Azure 함수 앱을 만들고 GitHub의 함수 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="5d9b9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "GitHub의 배포를 사용하여 함수 앱 만들기")]</span><span class="sxs-lookup"><span data-stu-id="5d9b9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5d9b9-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5d9b9-112">Script explanation</span></span>

<span data-ttu-id="5d9b9-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="5d9b9-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-114">This script uses the following commands:</span></span>

| <span data-ttu-id="5d9b9-115">명령</span><span class="sxs-lookup"><span data-stu-id="5d9b9-115">Command</span></span> | <span data-ttu-id="5d9b9-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5d9b9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d9b9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5d9b9-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5d9b9-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d9b9-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="5d9b9-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5d9b9-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5d9b9-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="5d9b9-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="5d9b9-122">Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="5d9b9-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="5d9b9-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="5d9b9-124">Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d9b9-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d9b9-125">Next steps</span></span>

<span data-ttu-id="5d9b9-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5d9b9-127">추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9b9-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
