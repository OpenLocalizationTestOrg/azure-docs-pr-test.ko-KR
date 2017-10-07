---
title: "aaaAzure CLI 스크립트 샘플-Docker 컨테이너에서 ASP.NET Core 웹 앱을 만들 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Docker 컨테이너에서 ASP.NET Core 웹앱 만들기"
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
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="837fc-103">Docker 컨테이너에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="837fc-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="837fc-104">이 시나리오에서는 toocreate 리소스 그룹 Linux 응용 프로그램 서비스 계획 및 웹 앱 및 Docker 컨테이너를 사용 하 여 ASP.NET Core 응용 프로그램 배포 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="837fc-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="837fc-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="837fc-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="837fc-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="837fc-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="837fc-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="837fc-109">Script explanation</span></span>

<span data-ttu-id="837fc-110">이 스크립트 명령 toocreate 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="837fc-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="837fc-112">명령</span><span class="sxs-lookup"><span data-stu-id="837fc-112">Command</span></span> | <span data-ttu-id="837fc-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="837fc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="837fc-114">az group create</span><span class="sxs-lookup"><span data-stu-id="837fc-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="837fc-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="837fc-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="837fc-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="837fc-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-117">Creates an App Service plan.</span></span> <span data-ttu-id="837fc-118">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="837fc-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="837fc-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="837fc-120">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="837fc-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="837fc-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="837fc-122">Hello Azure 웹 앱에 대 한 hello Docker 컨테이너를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="837fc-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="837fc-123">Next steps</span></span>

<span data-ttu-id="837fc-124">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="837fc-125">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="837fc-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
