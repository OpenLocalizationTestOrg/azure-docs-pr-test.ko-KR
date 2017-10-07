---
title: "aaaAzure CLI 스크립트 샘플-웹 응용 프로그램을 만들고 로컬 Git 리포지토리에서 코드 배포 | Microsoft Docs"
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
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="36773-103">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="36773-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="36773-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 로컬 Git 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="36773-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="36773-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="36773-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="36773-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="36773-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="36773-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="36773-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="36773-109">Script explanation</span></span>

<span data-ttu-id="36773-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-110">This script uses hello following commands.</span></span> <span data-ttu-id="36773-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="36773-112">명령</span><span class="sxs-lookup"><span data-stu-id="36773-112">Command</span></span> | <span data-ttu-id="36773-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="36773-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36773-114">az group create</span><span class="sxs-lookup"><span data-stu-id="36773-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="36773-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36773-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="36773-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="36773-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="36773-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36773-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="36773-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="36773-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="36773-119">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36773-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="36773-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="36773-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="36773-121">응용 프로그램 서비스에 대 한 hello 계정 수준 배포 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="36773-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="36773-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="36773-123">로컬 Git 리포지토리에 대한 원본 제어 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36773-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="36773-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="36773-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="36773-125">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36773-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36773-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36773-126">Next steps</span></span>

<span data-ttu-id="36773-127">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="36773-128">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36773-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
