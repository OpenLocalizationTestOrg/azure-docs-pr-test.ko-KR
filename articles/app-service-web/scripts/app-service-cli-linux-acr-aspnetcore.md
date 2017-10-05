---
title: "Azure CLI 스크립트 샘플 - Azure Container Registry의 Docker 컨테이너에서 ASP.NET Core 웹앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Container Registry의 Docker 컨테이너에서 ASP.NET Core 웹앱 만들기"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="2e6de-103">Azure Container Registry의 Docker 컨테이너에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2e6de-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="2e6de-104">이 시나리오에서는 리소스 그룹, Linux App Service 계획 및 웹앱을 만들고 Docker 컨테이너를 사용하여 Azure Container Registry에서 ASP.NET Core 응용 프로그램을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2e6de-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2e6de-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2e6de-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e6de-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2e6de-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2e6de-108">Sample script</span></span>

<span data-ttu-id="2e6de-109">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span><span class="sxs-lookup"><span data-stu-id="2e6de-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2e6de-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2e6de-110">Script explanation</span></span>

<span data-ttu-id="2e6de-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="2e6de-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2e6de-113">명령</span><span class="sxs-lookup"><span data-stu-id="2e6de-113">Command</span></span> | <span data-ttu-id="2e6de-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2e6de-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e6de-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2e6de-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2e6de-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2e6de-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2e6de-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2e6de-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-118">Creates an App Service plan.</span></span> <span data-ttu-id="2e6de-119">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2e6de-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="2e6de-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2e6de-121">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2e6de-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="2e6de-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="2e6de-123">Azure 웹앱에 대한 Docker 컨테이너를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e6de-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e6de-124">Next steps</span></span>

<span data-ttu-id="2e6de-125">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e6de-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2e6de-126">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e6de-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
