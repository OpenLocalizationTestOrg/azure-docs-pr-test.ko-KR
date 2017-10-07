---
title: "aaaAzure CLI 스크립트 샘플-사용자 지정 도메인 tooa 웹 응용 프로그램을 매핑할 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-맵 사용자 지정 도메인 tooa 웹 응용 프로그램"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="f5794-103">사용자 지정 도메인 tooa 웹 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="f5794-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="f5794-104">이 샘플 스크립트는 웹 앱 앱 서비스에서과 해당 관련된 리소스를 만들고 다음 매핑합니다 `www.<yourdomain>` tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f5794-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f5794-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f5794-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f5794-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f5794-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f5794-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f5794-109">Script explanation</span></span>

<span data-ttu-id="f5794-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-110">This script uses hello following commands.</span></span> <span data-ttu-id="f5794-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f5794-112">명령</span><span class="sxs-lookup"><span data-stu-id="f5794-112">Command</span></span> | <span data-ttu-id="f5794-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f5794-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5794-114">az group create</span><span class="sxs-lookup"><span data-stu-id="f5794-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f5794-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5794-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f5794-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f5794-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f5794-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="f5794-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f5794-119">Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f5794-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="f5794-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="f5794-121">사용자 지정 도메인 tooa 웹 응용 프로그램을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5794-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5794-122">Next steps</span></span>

<span data-ttu-id="f5794-123">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f5794-124">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5794-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
