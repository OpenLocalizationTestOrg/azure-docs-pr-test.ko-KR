---
title: "aaaAzure CLI 스크립트 샘플-GitHub에서 배포와 함께 웹 앱 만들기 | Microsoft Docs"
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="faafe-103">GitHub의 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="faafe-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="faafe-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 연속 배포를 사용하지 않고 공용 GitHub 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="faafe-105">연속 배포를 사용하는 GitHub 배포는 [GitHub의 연속 배포를 사용하여 웹앱 만들기](app-service-cli-continuous-deployment-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="faafe-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="faafe-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="faafe-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="faafe-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="faafe-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="faafe-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="faafe-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="faafe-110">Script explanation</span></span> 

<span data-ttu-id="faafe-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-111">This script uses hello following commands.</span></span> <span data-ttu-id="faafe-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="faafe-113">명령</span><span class="sxs-lookup"><span data-stu-id="faafe-113">Command</span></span> | <span data-ttu-id="faafe-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="faafe-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="faafe-115">az group create</span><span class="sxs-lookup"><span data-stu-id="faafe-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="faafe-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="faafe-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="faafe-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="faafe-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="faafe-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="faafe-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="faafe-120">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="faafe-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="faafe-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="faafe-122">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="faafe-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="faafe-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="faafe-124">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="faafe-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="faafe-125">Next steps</span></span>

<span data-ttu-id="faafe-126">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="faafe-127">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="faafe-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
