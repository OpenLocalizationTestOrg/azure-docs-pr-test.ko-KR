---
title: "aaaAzure CLI 스크립트 샘플-Azure CLI 2.0을 사용 하 여 수동으로 웹 응용 프로그램의 크기를 조정 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure CLI 2.0을 사용하여 수동으로 웹앱 크기 조정"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="125cd-103">수동으로 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="125cd-103">Scale a web app manually</span></span>

<span data-ttu-id="125cd-104">이 시나리오에서는 리소스 그룹 toocreate 배웁니다 앱 서비스 계획 및 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="125cd-105">단일 인스턴스 toomultiple 인스턴스에서 hello 앱 서비스 계획을 확장 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="125cd-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="125cd-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="125cd-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="125cd-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="125cd-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="125cd-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="125cd-110">Script explanation</span></span>

<span data-ttu-id="125cd-111">이 스크립트 명령 toocreate 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="125cd-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="125cd-113">명령</span><span class="sxs-lookup"><span data-stu-id="125cd-113">Command</span></span> | <span data-ttu-id="125cd-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="125cd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="125cd-115">az group create</span><span class="sxs-lookup"><span data-stu-id="125cd-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="125cd-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="125cd-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="125cd-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="125cd-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-118">Creates an App Service plan.</span></span> <span data-ttu-id="125cd-119">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="125cd-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="125cd-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="125cd-121">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="125cd-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="125cd-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="125cd-123">Hello 앱 서비스 계획의 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="125cd-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="125cd-124">Next steps</span></span>

<span data-ttu-id="125cd-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="125cd-126">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="125cd-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
