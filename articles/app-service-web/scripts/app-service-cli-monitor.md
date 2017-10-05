---
title: "Azure CLI 스크립트 샘플 - 웹 서버 로그를 사용하여 웹앱 모니터링 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 웹 서버 로그를 사용하여 웹앱 모니터링"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="0a445-103">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="0a445-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="0a445-104">이 시나리오에서는 리소스 그룹, App Service 계획, 웹앱을 만들고 웹 서버 로그를 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="0a445-105">그런 다음 검토하기 위해 로그 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a445-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0a445-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="0a445-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a445-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0a445-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0a445-109">Sample script</span></span>

<span data-ttu-id="0a445-110">[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "로그 모니터링")]</span><span class="sxs-lookup"><span data-stu-id="0a445-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0a445-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0a445-111">Script explanation</span></span>

<span data-ttu-id="0a445-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="0a445-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0a445-114">명령</span><span class="sxs-lookup"><span data-stu-id="0a445-114">Command</span></span> | <span data-ttu-id="0a445-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0a445-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a445-116">az group create</span><span class="sxs-lookup"><span data-stu-id="0a445-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0a445-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0a445-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="0a445-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0a445-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-119">Creates an App Service plan.</span></span> <span data-ttu-id="0a445-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="0a445-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="0a445-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0a445-122">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0a445-123">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="0a445-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="0a445-124">Azure 웹앱에서 유지하는 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="0a445-125">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="0a445-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="0a445-126">Azure 웹앱의 로그를 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a445-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a445-127">Next steps</span></span>

<span data-ttu-id="0a445-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a445-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0a445-129">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a445-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
