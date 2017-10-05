---
title: "Azure CLI 스크립트 샘플 - 함수 앱에 사용자 지정 도메인 매핑 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure의 함수 앱에 사용자 지정 도메인을 매핑합니다."
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
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="1b97a-103">함수 앱에 사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="1b97a-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="1b97a-104">이 샘플 스크립트는 관련된 리소스를 사용하여 함수 앱을 만든 다음 여기에 `www.<yourdomain>`을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="1b97a-105">사용자 지정 도메인에 매핑하려면 함수 앱이 소비 계획이 아니라 App Service 계획에서 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="1b97a-106">Azure Functions는 A 레코드를 사용한 사용자 지정 도메인 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1b97a-107">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1b97a-108">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="1b97a-109">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b97a-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="1b97a-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1b97a-110">Sample script</span></span>

<span data-ttu-id="1b97a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "함수 앱에 사용자 지정 도메인 매핑")]</span><span class="sxs-lookup"><span data-stu-id="1b97a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1b97a-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1b97a-112">Script explanation</span></span>

<span data-ttu-id="1b97a-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-113">This script uses the following commands.</span></span> <span data-ttu-id="1b97a-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1b97a-115">명령</span><span class="sxs-lookup"><span data-stu-id="1b97a-115">Command</span></span> | <span data-ttu-id="1b97a-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1b97a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1b97a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="1b97a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1b97a-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1b97a-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="1b97a-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="1b97a-120">함수 앱에 필요한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="1b97a-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="1b97a-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="1b97a-122">사용자 지정 도메인을 매핑하는 데 필요한 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="1b97a-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="1b97a-123">az functionapp create</span></span>]() | <span data-ttu-id="1b97a-124">함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-124">Creates a function app.</span></span> |
| [<span data-ttu-id="1b97a-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="1b97a-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="1b97a-126">함수 앱에 사용자 지정 도메인을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1b97a-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b97a-127">Next steps</span></span>

<span data-ttu-id="1b97a-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b97a-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1b97a-129">추가 Functions CLI 스크립트 샘플은 [Azure Functions 설명서]()에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b97a-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
