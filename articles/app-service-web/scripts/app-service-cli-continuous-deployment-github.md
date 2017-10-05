---
title: "Azure CLI 스크립트 샘플 - GitHub의 연속 배포를 사용하여 웹앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - GitHub의 연속 배포를 사용하여 웹앱 만들기"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="290b9-103">GitHub의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="290b9-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="290b9-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 GitHub 리포지토리의 연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="290b9-105">연속 배포를 사용하지 않는 GitHub 배포는 [웹앱 만들기 및 GitHub의 코드 배포](app-service-cli-deploy-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="290b9-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="290b9-106">이 샘플에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-106">In this sample, you will need:</span></span>

* <span data-ttu-id="290b9-107">관리 권한이 있는 응용 프로그램 코드를 포함하는 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="290b9-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="290b9-108">GitHub 계정에 대한 [PAT(개인 액세스 토큰)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)</span><span class="sxs-lookup"><span data-stu-id="290b9-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="290b9-109">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="290b9-110">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="290b9-111">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="290b9-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="290b9-112">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="290b9-112">Sample script</span></span>

<span data-ttu-id="290b9-113">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "GitHub의 연속 배포를 사용하여 웹앱 만들기")]</span><span class="sxs-lookup"><span data-stu-id="290b9-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="290b9-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="290b9-114">Script explanation</span></span>

<span data-ttu-id="290b9-115">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-115">This script uses the following commands.</span></span> <span data-ttu-id="290b9-116">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="290b9-117">명령</span><span class="sxs-lookup"><span data-stu-id="290b9-117">Command</span></span> | <span data-ttu-id="290b9-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="290b9-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="290b9-119">az group create</span><span class="sxs-lookup"><span data-stu-id="290b9-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="290b9-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="290b9-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="290b9-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="290b9-122">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="290b9-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="290b9-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="290b9-124">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="290b9-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="290b9-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="290b9-126">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="290b9-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="290b9-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="290b9-128">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="290b9-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="290b9-129">Next steps</span></span>

<span data-ttu-id="290b9-130">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="290b9-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="290b9-131">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="290b9-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
