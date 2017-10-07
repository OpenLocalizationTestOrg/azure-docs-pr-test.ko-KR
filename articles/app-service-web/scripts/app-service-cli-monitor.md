---
title: "웹 서버 로그가 포함 된 웹 앱을 모니터링 하는 CLI 스크립트 샘플-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="74777-103">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="74777-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="74777-104">이 시나리오에서는 리소스 그룹, 앱 서비스 계획, 웹 앱 만들고 hello 웹 응용 프로그램 tooenable 웹 서버 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="74777-105">그런 다음 검토를 위해 hello 로그 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="74777-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="74777-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="74777-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="74777-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="74777-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="74777-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="74777-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="74777-110">Script explanation</span></span>

<span data-ttu-id="74777-111">이 스크립트 명령 toocreate 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="74777-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="74777-113">명령</span><span class="sxs-lookup"><span data-stu-id="74777-113">Command</span></span> | <span data-ttu-id="74777-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="74777-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74777-115">az group create</span><span class="sxs-lookup"><span data-stu-id="74777-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="74777-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74777-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74777-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="74777-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="74777-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74777-118">Creates an App Service plan.</span></span> <span data-ttu-id="74777-119">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="74777-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="74777-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="74777-121">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74777-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="74777-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="74777-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="74777-123">Azure 웹앱에서 유지하는 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="74777-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="74777-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="74777-125">Azure 웹 앱 tooyour 로컬 컴퓨터의 hello 다운로드 hello 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74777-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74777-126">Next steps</span></span>

<span data-ttu-id="74777-127">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74777-128">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74777-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
