---
title: "aaaCreate 함수 앱 GitHub에서 코드 함수를 배포 하 고 | Microsoft Docs"
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
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="e8692-103">App Service 만들기</span><span class="sxs-lookup"><span data-stu-id="e8692-103">Create an App Service</span></span>

<span data-ttu-id="e8692-104">이 샘플 스크립트는 hello를 사용 하는 함수 앱 만듭니다 [소비 계획](../functions-scale.md#consumption-plan) 과 해당 관련된 리소스를 지속적으로 GitHub 리포지토리에서 함수 코드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="e8692-105">이 샘플에서는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-105">In this sample, you need:</span></span>

* <span data-ttu-id="e8692-106">관리 권한이 있는 함수 코드를 포함하는 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="e8692-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="e8692-107">GitHub 계정에 대한 [PAT(개인 액세스 토큰)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)</span><span class="sxs-lookup"><span data-stu-id="e8692-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e8692-108">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e8692-109">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e8692-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e8692-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="e8692-111">Sample script</span></span>

<span data-ttu-id="e8692-112">이 샘플은 Azure 함수 앱을 만들고 GitHub의 함수 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e8692-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="e8692-113">Script explanation</span></span>

<span data-ttu-id="e8692-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="e8692-115">이 스크립트는 hello 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-115">This script uses hello following:</span></span>

| <span data-ttu-id="e8692-116">명령</span><span class="sxs-lookup"><span data-stu-id="e8692-116">Command</span></span> | <span data-ttu-id="e8692-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="e8692-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8692-118">az group create</span><span class="sxs-lookup"><span data-stu-id="e8692-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e8692-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8692-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="e8692-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e8692-121">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e8692-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="e8692-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="e8692-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="e8692-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="e8692-124">Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8692-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8692-125">Next steps</span></span>

<span data-ttu-id="e8692-126">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e8692-127">추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8692-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
