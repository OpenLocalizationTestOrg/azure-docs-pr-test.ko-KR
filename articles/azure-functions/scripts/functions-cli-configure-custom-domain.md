---
title: "CLI 스크립트 샘플-aaaAzure 매핑하는 사용자 지정 도메인 tooa 함수 앱 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Azure의 사용자 지정 도메인 tooa 함수 앱 맵."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="44c93-103">사용자 지정 도메인 tooa 함수 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="44c93-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="44c93-104">이 샘플 스크립트 관련된 리소스를 사용 하 여 함수 앱을 만들고 다음 매핑합니다 `www.<yourdomain>` tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="44c93-105">toomap tooa 사용자 지정 도메인을 소비 계획 아니라 앱 서비스 계획에 함수 앱 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="44c93-106">Azure Functions는 A 레코드를 사용한 사용자 지정 도메인 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="44c93-107">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="44c93-108">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="44c93-109">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="44c93-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="44c93-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="44c93-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="44c93-111">Script explanation</span></span>

<span data-ttu-id="44c93-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-112">This script uses hello following commands.</span></span> <span data-ttu-id="44c93-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="44c93-114">명령</span><span class="sxs-lookup"><span data-stu-id="44c93-114">Command</span></span> | <span data-ttu-id="44c93-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="44c93-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="44c93-116">az group create</span><span class="sxs-lookup"><span data-stu-id="44c93-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="44c93-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="44c93-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="44c93-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="44c93-119">Hello 함수 앱에 필요한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="44c93-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="44c93-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="44c93-121">앱 서비스 계획이 필요 toomap 사용자 지정 도메인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="44c93-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="44c93-122">az functionapp create</span></span>]() | <span data-ttu-id="44c93-123">함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-123">Creates a function app.</span></span> |
| [<span data-ttu-id="44c93-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="44c93-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="44c93-125">사용자 지정 도메인 tooa 함수 응용 프로그램을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44c93-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44c93-126">Next steps</span></span>

<span data-ttu-id="44c93-127">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="44c93-128">추가 기능 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서]()합니다.</span><span class="sxs-lookup"><span data-stu-id="44c93-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
