---
title: "Azure CLI 스크립트 샘플 - Cosmos DB에 웹앱 연결 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Cosmos DB에 웹앱 연결"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="757dc-103">웹앱을 Cosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="757dc-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="757dc-104">이 시나리오에서는 Azure Cosmos DB 계정 및 Azure Web App을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="757dc-105">그런 다음 앱 설정을 사용하여 Cosmos DB를 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="757dc-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="757dc-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="757dc-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="757dc-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="757dc-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="757dc-109">Sample script</span></span>

<span data-ttu-id="757dc-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="757dc-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="757dc-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="757dc-111">Script explanation</span></span>

<span data-ttu-id="757dc-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, Cosmos DB 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="757dc-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="757dc-114">명령</span><span class="sxs-lookup"><span data-stu-id="757dc-114">Command</span></span> | <span data-ttu-id="757dc-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="757dc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="757dc-116">az group create</span><span class="sxs-lookup"><span data-stu-id="757dc-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="757dc-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="757dc-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="757dc-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="757dc-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-119">Creates an App Service plan.</span></span> <span data-ttu-id="757dc-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="757dc-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="757dc-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="757dc-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="757dc-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="757dc-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="757dc-124">Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="757dc-125">데이터가 저장될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="757dc-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="757dc-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="757dc-127">지정된 Cosmos DB 계정에 대한 선택키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="757dc-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="757dc-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="757dc-129">Azure 웹앱에 대한 앱 설정을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="757dc-130">앱 설정은 앱에 대한 환경 변수로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="757dc-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="757dc-131">Next steps</span></span>

<span data-ttu-id="757dc-132">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="757dc-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="757dc-133">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757dc-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
