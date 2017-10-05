---
title: "함수 앱 만들기 및 GitHub의 함수 코드 배포 | Microsoft Docs"
description: "함수 앱 만들기 및 GitHub의 함수 코드 배포"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="cd89b-103">App Service 만들기</span><span class="sxs-lookup"><span data-stu-id="cd89b-103">Create an App Service</span></span>

<span data-ttu-id="cd89b-104">이 샘플 스크립트는 관련 리소스를 통해 [소비 계획](../functions-scale.md#consumption-plan)을 사용하여 함수 앱을 만들고 GitHub 리포지토리의 함수 코드를 연속적으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="cd89b-105">이 샘플에서는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-105">In this sample, you need:</span></span>

* <span data-ttu-id="cd89b-106">관리 권한이 있는 함수 코드를 포함하는 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="cd89b-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="cd89b-107">GitHub 계정에 대한 [PAT(개인 액세스 토큰)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)</span><span class="sxs-lookup"><span data-stu-id="cd89b-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cd89b-108">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cd89b-109">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="cd89b-110">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd89b-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cd89b-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="cd89b-111">Sample script</span></span>

<span data-ttu-id="cd89b-112">이 샘플은 Azure 함수 앱을 만들고 GitHub의 함수 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="cd89b-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span><span class="sxs-lookup"><span data-stu-id="cd89b-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cd89b-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="cd89b-114">Script explanation</span></span>

<span data-ttu-id="cd89b-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="cd89b-116">이 스크립트는 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-116">This script uses the following:</span></span>

| <span data-ttu-id="cd89b-117">명령</span><span class="sxs-lookup"><span data-stu-id="cd89b-117">Command</span></span> | <span data-ttu-id="cd89b-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="cd89b-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cd89b-119">az group create</span><span class="sxs-lookup"><span data-stu-id="cd89b-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cd89b-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cd89b-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="cd89b-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cd89b-122">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cd89b-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="cd89b-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="cd89b-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="cd89b-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="cd89b-125">Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cd89b-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd89b-126">Next steps</span></span>

<span data-ttu-id="cd89b-127">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd89b-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cd89b-128">추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd89b-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
