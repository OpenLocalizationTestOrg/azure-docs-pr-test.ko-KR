---
title: "CLI 스크립트 샘플-aaaAzure 연결 웹 응용 프로그램 tooCosmos DB | Microsoft Docs"
description: "Azure CLI 스크립트 예제-웹 응용 프로그램 tooCosmos DB 연결"
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
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="8fadf-103">웹 앱 tooCosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="8fadf-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="8fadf-104">이 시나리오에서는 toocreate Azure Cosmos DB 계정 및 Azure 웹 앱에 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="8fadf-105">그런 다음 응용 프로그램 설정을 사용 하 여 hello Cosmos DB toohello 웹 앱을 연결할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8fadf-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8fadf-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8fadf-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8fadf-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8fadf-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8fadf-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8fadf-110">Script explanation</span></span>

<span data-ttu-id="8fadf-111">이 스크립트 명령 toocreate 리소스 그룹, 웹 응용 프로그램, Cosmos DB 및 관련 된 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="8fadf-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8fadf-113">명령</span><span class="sxs-lookup"><span data-stu-id="8fadf-113">Command</span></span> | <span data-ttu-id="8fadf-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8fadf-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8fadf-115">az group create</span><span class="sxs-lookup"><span data-stu-id="8fadf-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8fadf-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8fadf-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8fadf-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8fadf-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-118">Creates an App Service plan.</span></span> <span data-ttu-id="8fadf-119">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8fadf-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="8fadf-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8fadf-121">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8fadf-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="8fadf-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="8fadf-123">Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="8fadf-124">이 hello 데이터가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="8fadf-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="8fadf-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="8fadf-126">Hello에 대 한 목록 hello 선택 키 Cosmos DB 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="8fadf-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="8fadf-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="8fadf-128">Azure 웹앱에 대한 앱 설정을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="8fadf-129">앱 설정은 앱에 대한 환경 변수로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8fadf-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fadf-130">Next steps</span></span>

<span data-ttu-id="8fadf-131">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8fadf-132">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fadf-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
