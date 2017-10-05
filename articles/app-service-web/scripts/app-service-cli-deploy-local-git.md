---
title: "Azure CLI 스크립트 샘플 - 웹앱 만들기 및 Git 리포지토리의 코드 배포 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 웹앱 만들기 및 Git 리포지토리의 코드 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="ec8af-103">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="ec8af-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="ec8af-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 로컬 Git 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ec8af-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ec8af-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ec8af-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8af-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ec8af-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ec8af-108">Sample script</span></span>

<span data-ttu-id="ec8af-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포")]</span><span class="sxs-lookup"><span data-stu-id="ec8af-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ec8af-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ec8af-110">Script explanation</span></span>

<span data-ttu-id="ec8af-111">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-111">This script uses the following commands.</span></span> <span data-ttu-id="ec8af-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ec8af-113">명령</span><span class="sxs-lookup"><span data-stu-id="ec8af-113">Command</span></span> | <span data-ttu-id="ec8af-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ec8af-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ec8af-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ec8af-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ec8af-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ec8af-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ec8af-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ec8af-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ec8af-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ec8af-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ec8af-120">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ec8af-121">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="ec8af-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="ec8af-122">App Service에 대한 계정 수준 배포 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="ec8af-123">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="ec8af-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="ec8af-124">로컬 Git 리포지토리에 대한 원본 제어 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="ec8af-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ec8af-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ec8af-126">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ec8af-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec8af-127">Next steps</span></span>

<span data-ttu-id="ec8af-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8af-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ec8af-129">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8af-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
