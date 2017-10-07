---
title: "aaaAzure CLI 스크립트 샘플-Visual Studio Team Services에서 연속 배포와 함께 웹 앱 만들기 | Microsoft Docs"
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="ff5e1-103">Visual Studio Team Services의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ff5e1-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="ff5e1-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 Visual Studio Team Services 리포지토리의 연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="ff5e1-105">이 샘플에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-105">For this sample, you will need:</span></span>

* <span data-ttu-id="ff5e1-106">관리 권한이 있는 응용 프로그램 코드를 포함하는 Visual Studio Team Services 리포지토리</span><span class="sxs-lookup"><span data-stu-id="ff5e1-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="ff5e1-107">Visual Studio Team Services 계정용 [PAT(개인 액세스 토큰)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate).</span><span class="sxs-lookup"><span data-stu-id="ff5e1-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ff5e1-108">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ff5e1-109">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ff5e1-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ff5e1-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ff5e1-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ff5e1-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ff5e1-112">Script explanation</span></span>

<span data-ttu-id="ff5e1-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-113">This script uses hello following commands.</span></span> <span data-ttu-id="ff5e1-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ff5e1-115">명령</span><span class="sxs-lookup"><span data-stu-id="ff5e1-115">Command</span></span> | <span data-ttu-id="ff5e1-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ff5e1-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff5e1-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ff5e1-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ff5e1-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff5e1-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ff5e1-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ff5e1-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ff5e1-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ff5e1-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ff5e1-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ff5e1-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="ff5e1-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="ff5e1-124">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="ff5e1-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ff5e1-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ff5e1-126">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff5e1-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff5e1-127">Next steps</span></span>

<span data-ttu-id="ff5e1-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ff5e1-129">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e1-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
