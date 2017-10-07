---
title: "aaaAzure CLI 스크립트 샘플-웹 앱 만들기 및 배포 환경 준비 코드 tooa | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-웹 응용 프로그램을 만들고 코드 tooa 스테이징 환경 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="4635d-103">웹 앱을 만들고 코드 tooa 스테이징 환경 배포</span><span class="sxs-lookup"><span data-stu-id="4635d-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="4635d-104">이 샘플 스크립트 웹 응용 프로그램 앱 서비스의 "준비"를 호출 하는 추가 배포 슬롯으로 만들고 "스테이징" 슬롯 샘플 앱 toohello 다음 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4635d-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4635d-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4635d-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4635d-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4635d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4635d-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4635d-109">Script explanation</span></span>

<span data-ttu-id="4635d-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-110">This script uses hello following commands.</span></span> <span data-ttu-id="4635d-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4635d-112">명령</span><span class="sxs-lookup"><span data-stu-id="4635d-112">Command</span></span> | <span data-ttu-id="4635d-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4635d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4635d-114">az group create</span><span class="sxs-lookup"><span data-stu-id="4635d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4635d-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4635d-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4635d-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4635d-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4635d-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="4635d-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4635d-119">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4635d-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="4635d-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="4635d-121">배포 슬롯을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="4635d-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="4635d-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="4635d-123">Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="4635d-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="4635d-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="4635d-125">브라우저에서 Azure 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="4635d-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="4635d-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="4635d-127">지정된 배포 슬롯을 프로덕션으로 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4635d-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4635d-128">Next steps</span></span>

<span data-ttu-id="4635d-129">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4635d-130">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4635d-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
