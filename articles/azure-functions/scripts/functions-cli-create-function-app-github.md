---
title: "aaaCreate 함수 앱 GitHub에서 코드 함수를 배포 하 고 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 함수 앱 만들기 및 GitHub의 함수 코드 배포"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="af2e2-103">함수 앱 만들기 및 GitHub의 함수 코드 배포</span><span class="sxs-lookup"><span data-stu-id="af2e2-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="af2e2-104">이 샘플 스크립트는 hello를 사용 하는 함수 앱 만듭니다 [소비 계획](../functions-scale.md#consumption-plan) 과 해당 관련된 리소스 (하지 않고 연속 배포) 공용 GitHub 리포지토리에서 함수 코드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="af2e2-105">GitHub의 지속적인 함수 코드 전송에 관해서는 [함수 앱 만들기 및 GitHub에서 지속적으로 배포](functions-cli-create-function-app-github-continuous.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="af2e2-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="af2e2-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="af2e2-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="af2e2-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="af2e2-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="af2e2-109">Sample script</span></span>

<span data-ttu-id="af2e2-110">이 샘플은 Azure 함수 앱을 만들고 GitHub의 함수 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="af2e2-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="af2e2-111">Script explanation</span></span>

<span data-ttu-id="af2e2-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="af2e2-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="af2e2-114">명령</span><span class="sxs-lookup"><span data-stu-id="af2e2-114">Command</span></span> | <span data-ttu-id="af2e2-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="af2e2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af2e2-116">az group create</span><span class="sxs-lookup"><span data-stu-id="af2e2-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="af2e2-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="af2e2-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="af2e2-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="af2e2-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="af2e2-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="af2e2-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="af2e2-121">Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="af2e2-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="af2e2-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="af2e2-123">Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="af2e2-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af2e2-124">Next steps</span></span>

<span data-ttu-id="af2e2-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="af2e2-126">추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af2e2-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
