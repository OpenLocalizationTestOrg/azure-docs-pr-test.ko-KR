---
title: "Azure CLI 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="a5c7f-103">전세계에 고가용성 아키텍처를 가진 웹앱 확장</span><span class="sxs-lookup"><span data-stu-id="a5c7f-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="a5c7f-104">이 시나리오에서는 리소스 그룹, 두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="a5c7f-105">실행이 완료되면 가장 낮은 네트워크 대기 시간에 따라 웹앱의 전역적 가용성을 제공하는 가용성이 좋은 아키텍처를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a5c7f-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a5c7f-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="a5c7f-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="a5c7f-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a5c7f-109">Sample script</span></span>

<span data-ttu-id="a5c7f-110">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "지리적 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="a5c7f-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a5c7f-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a5c7f-111">Script explanation</span></span>

<span data-ttu-id="a5c7f-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, Traffic Manager 프로필 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="a5c7f-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a5c7f-114">명령</span><span class="sxs-lookup"><span data-stu-id="a5c7f-114">Command</span></span> | <span data-ttu-id="a5c7f-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a5c7f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a5c7f-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a5c7f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a5c7f-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a5c7f-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a5c7f-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a5c7f-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-119">Creates an App Service plan.</span></span> <span data-ttu-id="a5c7f-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a5c7f-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a5c7f-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a5c7f-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a5c7f-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="a5c7f-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="a5c7f-124">Azure Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="a5c7f-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="a5c7f-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="a5c7f-126">Azure Traffic Manager 프로필에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a5c7f-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5c7f-127">Next steps</span></span>

<span data-ttu-id="a5c7f-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a5c7f-129">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5c7f-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
