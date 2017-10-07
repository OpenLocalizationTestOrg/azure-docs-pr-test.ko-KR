---
title: "CLI 스크립트 샘플-aaaAzure 연결 웹 응용 프로그램 tooa redis 캐시 | Microsoft Docs"
description: "Azure CLI 스크립트 예제-웹 응용 프로그램 tooa redis 캐시를 연결 합니다."
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="c6970-103">웹 앱 tooa redis 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="c6970-104">이 시나리오에서는 toocreate Azure redis 캐시 및 Azure 웹 앱 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="c6970-105">그런 다음 응용 프로그램 설정을 사용 하 여 hello redis 캐시 toohello 웹 앱을 연결할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c6970-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c6970-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c6970-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c6970-107">Script explanation</span></span>

<span data-ttu-id="c6970-108">이 스크립트 명령 toocreate 리소스 그룹에서 웹 응용 프로그램에서 redis 캐시와 관련 된 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="c6970-109">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c6970-110">명령</span><span class="sxs-lookup"><span data-stu-id="c6970-110">Command</span></span> | <span data-ttu-id="c6970-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c6970-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6970-112">az group create</span><span class="sxs-lookup"><span data-stu-id="c6970-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c6970-113">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6970-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c6970-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c6970-115">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-115">Creates an App Service plan.</span></span> <span data-ttu-id="c6970-116">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="c6970-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c6970-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c6970-118">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c6970-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="c6970-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="c6970-120">새 Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="c6970-121">이 hello 데이터가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="c6970-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="c6970-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="c6970-123">Hello redis 캐시 인스턴스에 대 한 hello 선택 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="c6970-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="c6970-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="c6970-125">Azure 웹앱에 대한 앱 설정을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="c6970-126">앱 설정은 앱에 대한 환경 변수로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6970-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6970-127">Next steps</span></span>

<span data-ttu-id="c6970-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6970-129">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6970-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
