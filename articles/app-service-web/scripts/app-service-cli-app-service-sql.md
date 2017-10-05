---
title: "Azure CLI 스크립트 샘플 - SQL Database에 웹앱 연결 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - SQL Database에 웹앱 연결"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="14770-103">SQL Database에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="14770-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="14770-104">이 시나리오에서는 Azure SQL Database 및 Azure 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="14770-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="14770-105">그런 다음 앱 설정을 사용하여 SQL Database를 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="14770-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="14770-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14770-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="14770-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="14770-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="14770-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14770-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="14770-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="14770-109">Sample script</span></span>

<span data-ttu-id="14770-110">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="14770-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="14770-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="14770-111">Script explanation</span></span>

<span data-ttu-id="14770-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, SQL Database 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="14770-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="14770-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="14770-114">명령</span><span class="sxs-lookup"><span data-stu-id="14770-114">Command</span></span> | <span data-ttu-id="14770-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="14770-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14770-116">az group create</span><span class="sxs-lookup"><span data-stu-id="14770-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="14770-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="14770-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="14770-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="14770-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-119">Creates an App Service plan.</span></span> <span data-ttu-id="14770-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="14770-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="14770-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="14770-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="14770-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="14770-123">az sql server create</span><span class="sxs-lookup"><span data-stu-id="14770-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="14770-124">SQL Database 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="14770-125">az sql db create</span><span class="sxs-lookup"><span data-stu-id="14770-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="14770-126">SQL Database 서버를 사용하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14770-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="14770-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="14770-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="14770-128">Azure 웹앱에 대한 앱 설정을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="14770-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="14770-129">앱 설정은 앱에 대한 환경 변수로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="14770-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14770-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14770-130">Next steps</span></span>

<span data-ttu-id="14770-131">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14770-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="14770-132">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14770-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
