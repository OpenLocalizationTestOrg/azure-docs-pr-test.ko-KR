---
title: "Azure CLI 스크립트 샘플 - GitHub의 배포를 사용하여 웹앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - GitHub의 배포를 사용하여 웹앱 만들기"
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
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="5ee65-103">GitHub의 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5ee65-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="5ee65-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 연속 배포를 사용하지 않고 공용 GitHub 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="5ee65-105">연속 배포를 사용하는 GitHub 배포는 [GitHub의 연속 배포를 사용하여 웹앱 만들기](app-service-cli-continuous-deployment-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ee65-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ee65-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ee65-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5ee65-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ee65-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5ee65-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5ee65-109">Sample script</span></span>

<span data-ttu-id="5ee65-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "GitHub의 배포를 사용하여 웹앱 만들기")]</span><span class="sxs-lookup"><span data-stu-id="5ee65-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5ee65-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5ee65-111">Script explanation</span></span> 

<span data-ttu-id="5ee65-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-112">This script uses the following commands.</span></span> <span data-ttu-id="5ee65-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5ee65-114">명령</span><span class="sxs-lookup"><span data-stu-id="5ee65-114">Command</span></span> | <span data-ttu-id="5ee65-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5ee65-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5ee65-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5ee65-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5ee65-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5ee65-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5ee65-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5ee65-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5ee65-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5ee65-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5ee65-121">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5ee65-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="5ee65-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="5ee65-123">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="5ee65-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="5ee65-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="5ee65-125">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5ee65-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ee65-126">Next steps</span></span>

<span data-ttu-id="5ee65-127">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ee65-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5ee65-128">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee65-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
