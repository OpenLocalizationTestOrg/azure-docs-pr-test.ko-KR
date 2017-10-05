---
title: "Azure CLI 스크립트 샘플 - Azure CLI 2.0을 사용하여 수동으로 웹앱 크기 조정 | Microsoft Docs"
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
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="a21ea-103">수동으로 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a21ea-103">Scale a web app manually</span></span>

<span data-ttu-id="a21ea-104">이 시나리오에서는 리소스 그룹, App Service 계획 및 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="a21ea-105">그런 다음 단일 인스턴스에서 여러 인스턴스로 App Service 계획의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a21ea-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a21ea-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="a21ea-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a21ea-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a21ea-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a21ea-109">Sample script</span></span>

<span data-ttu-id="a21ea-110">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "수동 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="a21ea-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a21ea-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a21ea-111">Script explanation</span></span>

<span data-ttu-id="a21ea-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="a21ea-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a21ea-114">명령</span><span class="sxs-lookup"><span data-stu-id="a21ea-114">Command</span></span> | <span data-ttu-id="a21ea-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a21ea-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a21ea-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a21ea-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a21ea-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a21ea-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a21ea-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a21ea-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-119">Creates an App Service plan.</span></span> <span data-ttu-id="a21ea-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a21ea-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a21ea-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a21ea-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a21ea-123">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="a21ea-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="a21ea-124">App Service 계획의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a21ea-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a21ea-125">Next steps</span></span>

<span data-ttu-id="a21ea-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a21ea-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a21ea-127">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a21ea-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
