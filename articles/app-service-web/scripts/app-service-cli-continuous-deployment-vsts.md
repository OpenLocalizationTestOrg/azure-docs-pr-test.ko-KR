---
title: "Azure CLI 스크립트 샘플 - Visual Studio Team Services의 연속 배포를 사용하여 웹앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Visual Studio Team Services의 연속 배포를 사용하여 웹앱 만들기"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="b93a5-103">Visual Studio Team Services의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b93a5-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="b93a5-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 Visual Studio Team Services 리포지토리의 연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="b93a5-105">이 샘플에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-105">For this sample, you will need:</span></span>

* <span data-ttu-id="b93a5-106">관리 권한이 있는 응용 프로그램 코드를 포함하는 Visual Studio Team Services 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b93a5-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="b93a5-107">Visual Studio Team Services 계정용 [PAT(개인 액세스 토큰)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate).</span><span class="sxs-lookup"><span data-stu-id="b93a5-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b93a5-108">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b93a5-109">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="b93a5-110">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b93a5-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b93a5-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b93a5-111">Sample script</span></span>

<span data-ttu-id="b93a5-112">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Visual Studio Team Services의 연속 배포를 사용하여 웹앱 만들기")]</span><span class="sxs-lookup"><span data-stu-id="b93a5-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b93a5-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b93a5-113">Script explanation</span></span>

<span data-ttu-id="b93a5-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-114">This script uses the following commands.</span></span> <span data-ttu-id="b93a5-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b93a5-116">명령</span><span class="sxs-lookup"><span data-stu-id="b93a5-116">Command</span></span> | <span data-ttu-id="b93a5-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b93a5-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b93a5-118">az group create</span><span class="sxs-lookup"><span data-stu-id="b93a5-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b93a5-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b93a5-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b93a5-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b93a5-121">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b93a5-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b93a5-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b93a5-123">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b93a5-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="b93a5-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="b93a5-125">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="b93a5-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="b93a5-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="b93a5-127">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b93a5-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b93a5-128">Next steps</span></span>

<span data-ttu-id="b93a5-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b93a5-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b93a5-130">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93a5-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
