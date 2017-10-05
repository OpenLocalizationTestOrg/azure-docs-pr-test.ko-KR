---
title: "Azure CLI 스크립트 샘플 - Redis Cache에 웹앱 연결 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Redis Cache에 웹앱 연결"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="8366d-103">Redis Cache에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="8366d-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="8366d-104">이 시나리오에서는 Azure Redis Cache 및 Azure 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="8366d-105">그런 다음 앱 설정을 사용하여 Redis Cache를 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8366d-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8366d-106">Sample script</span></span>

<span data-ttu-id="8366d-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="8366d-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8366d-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8366d-108">Script explanation</span></span>

<span data-ttu-id="8366d-109">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, Redis Cache 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="8366d-110">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8366d-111">명령</span><span class="sxs-lookup"><span data-stu-id="8366d-111">Command</span></span> | <span data-ttu-id="8366d-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8366d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8366d-113">az group create</span><span class="sxs-lookup"><span data-stu-id="8366d-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8366d-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8366d-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8366d-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8366d-116">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-116">Creates an App Service plan.</span></span> <span data-ttu-id="8366d-117">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8366d-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="8366d-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8366d-119">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8366d-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="8366d-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="8366d-121">새 Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="8366d-122">데이터가 저장될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="8366d-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="8366d-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="8366d-124">Redis Cache 인스턴스에 대한 액세스 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="8366d-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="8366d-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="8366d-126">Azure 웹앱에 대한 앱 설정을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="8366d-127">앱 설정은 앱에 대한 환경 변수로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8366d-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8366d-128">Next steps</span></span>

<span data-ttu-id="8366d-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8366d-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8366d-130">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8366d-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
